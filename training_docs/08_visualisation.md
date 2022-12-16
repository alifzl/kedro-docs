
## Visualise your pipeline

[Kedro Viz](https://github.com/kedro-org/kedro-viz) shows you how your Kedro data pipelines are structured. You can use it to:

 - See how your datasets and Python functions (nodes) are resolved in Kedro so that you can understand how your data pipeline is built
 - Get a clear picture when you have lots of datasets and nodes by using tags to visualise sub-pipelines
 - Search for nodes and datasets

Follow the [Kedro-Viz installation instructions](https://kedro.readthedocs.io/en/stable/visualisation/kedro-viz_visualisation.html) to get set up.
### Using `kedro-viz`

From your terminal, run below command in your kedro project directory:

```
kedro viz
```

This command will run a server on http://127.0.0.1:4141 and will open up your visualisation on a browser.

> *Note:* If port `4141` is already occupied, you can run Kedro-Viz server on a different port by executing `kedro viz --port <alternative-port>`.

_[Go to the next page](./09_versioning.md)_
