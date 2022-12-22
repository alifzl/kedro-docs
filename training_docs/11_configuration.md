# Configuration

We recommend that you keep all configuration files in the `conf` directory of a Kedro project. However, if you prefer, you may point Kedro to any other directory and change the configuration paths by setting the `CONF_ROOT` variable in `src/kedro_training/settings.py` as follows:

```python
# ...
CONF_ROOT = "new_conf"
```

## Loading configuration
Kedro-specific configuration (e.g., `DataCatalog` configuration for IO) is loaded using the `ConfigLoader` class:

```python
from kedro.config import ConfigLoader

conf_paths = ["conf/base", "conf/local"]
conf_loader = ConfigLoader(conf_paths)
conf_catalog = conf_loader.get("catalog*", "catalog*/**")
```

This will recursively scan for configuration files firstly in `conf/base/` and then in `conf/local/` directory according to the following rules:

* ANY of the following is true:
  * filename starts with `catalog` OR
  * file is located in a sub-directory whose name is prefixed with `catalog`
* AND file extension is one of the following: `yaml`, `yml`, `json`, `ini`, `pickle`, `xml` or `properties`

Configuration information from files stored in `base` or `local` that match these rules is merged at runtime and returned in the form of a config dictionary:

* If any 2 configuration files located inside the same environment path (`conf/base/` or `conf/local/` in this example) contain the same top-level key, `load_config` will raise a `ValueError` indicating that the duplicates are not allowed.

> *Note:* Any top-level keys that start with `_` character are considered hidden (or reserved) and therefore are ignored right after the config load. Those keys will neither trigger a key duplication error mentioned above, nor will they appear in the resulting configuration dictionary. However, you may still use such keys for various purposes. For example, as [YAML anchors and aliases](https://support.atlassian.com/bitbucket-cloud/docs/yaml-anchors/).

* If 2 configuration files have duplicate top-level keys, but are placed into different environment paths (one in `conf/base/`, another in `conf/local/`, for example) then the last loaded path (`conf/local/` in this case) takes precedence and overrides that key value. `ConfigLoader.get(<pattern>, ...)` will not raise any errors, however a `DEBUG` level log message will be emitted with the information on the over-ridden keys.
* If the same environment path is passed multiple times, a `UserWarning` will be emitted to draw attention to the duplicate loading attempt, and any subsequent loading after the first one will be skipped.


## Additional config environments

In addition to the 2 built-in configuration environments, it is possible to create your own. Your project loads `conf/base/` as the bottom-level configuration environment but allows you to overwrite it with any other environments that you create. You are be able to create environments like `conf/server/`, `conf/test/`, etc. Any additional configuration environments can be created inside `conf` folder and loaded by running the following command:

```bash
kedro run --env=test
```

If no `env` option is specified, this will default to using `local` environment to overwrite `conf/base`.

> *Note*: If, for some reason, your project does not have any other environments apart from `base`, i.e. no `local` environment to default to, you will need to customise `KedroContext` to take `env="base"` in the constructor and then specify your custom `KedroContext` subclass in `src/<python-package>/settings.py` under `CONTEXT_CLASS` key.

If you set the `KEDRO_ENV` environment variable to the name of your environment, Kedro will load that environment for your `kedro run`, `kedro ipython`, `kedro jupyter notebook` and `kedro jupyter lab` sessions.

```bash
export KEDRO_ENV=test
```

> *Note*: If you specify both the `KEDRO_ENV` environment variable and provide the `--env` argument to a CLI command, the CLI argument takes precedence.

_[Go to the next page](./12_transcoding.md)_
