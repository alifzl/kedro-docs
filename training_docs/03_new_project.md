# Create a new project

before starting any Data Science project, you'll mainly doing these 4 steps: 

### 1. Set up the project template

* Create a new project with `kedro new --starter=https://git.mielse.com/data/kedro-starters --directory=pyspark`
* Install project dependencies with `pip install -r src/requirements.txt`
* Configure the following in the `conf` folder:
	* Logging
	* Credentials
	* Any other sensitive / personal content

### 2. Set up the data

* Add data to the `data/` folder
* Reference all datasets for the project in `conf/base/catalog.yml`

### 3. Create the pipeline

* Create the data transformation steps as Python functions
* Construct the pipeline by adding your functions as nodes
* Choose how to run the pipeline: sequentially or in parallel

### 4. Package the project

 * Build the project documentation
 * Package the project for distribution


## Create and set up a new project

In this section, we discuss the project set-up phase, with the following steps:


* Create a new project
* Install dependencies
* Configure the project

----
In the text, we assume that you create an empty project and follow the flow of the tutorial by copying and pasting the example code into the project as I describe. 
However, you may prefer to get up and running more swiftly so we provide the fully configured template project as a [Trumpet Data Science Template](https://git.mielse.com/data/ds-template). 

Follow one or other of these instructions to create the project:

* If you decide to create the example project fully populated with code, navigate to your chosen working directory and run the following: `kedro new --starter=https://git.mielse.com/data/kedro-starters --directory=sample-trumpet`

     - Feel free to name your project as you like, but this guide will assume the project is named **`Kedro Training`**, and that your project is in a sub-folder in your working directory that was created by `kedro new`, named `kedro-training`.

     - Keep the default names for the `repo_name` and `python_package` when prompted.

### Project structure
Take a few minutes to familiarise yourself with the [Kedro project structure](https://kedro.readthedocs.io/en/stable/02_get_started/05_example_project.html#project-directory-structure) by exploring the contents of the `kedro-training` folder that you created from either of the steps you chose above.


## Configure the Data Sources

In order to do so, you should take care of two steps:
  1. configuring `conf/local/credentials.yml` (Credentials of Data Source)
  2. configuring `conf/base/catalog.yml` (Data Source Data Catalog and it's arguments)


### Step1: conf/local/credentials.yml
For security reasons, You shoul dmanually add credentials to `conf/local/credentials.yml` that you would need to load specific data sources like usernames and passwords. 

**You Should take your rightfull credentials from your Team Lead**.

After modifying this, Kedro automatically reads credentials from the `conf` folder and feeds them into the Data Catalog, which is responsible for loading and saving data as inputs and outputs of pipeline nodes. You can configure your credentials once and then reuse them in multiple datasets.

Example of `conf/local/credentials.yml`:

```yaml
trumpet_staging_creds:
    username: [USERNAME]
    password: [PASSWORD]
    con: "mysql+pymysql://[USERNAME]:[PASSWORD]@[HOST]:[PORT]/[SCHEMA]"

```

For security reasons, we strongly recommend not committing any credentials or other secrets to the Version Control System. By default any file inside the `conf` folder (and subfolders) in your Kedro project containing `credentials` in its name will be ignored and not committed to your repository.


### Step2: conf/base/catalog.yml

In this file, you should enter your needfull Data Catalog for your Data Sources like Relational databases and so on.
An example of a correct Data Catalog would be like this:

```yaml
# file-based data catalog
agg_listings_csv:
  type: pandas.CSVDataSet
  filepath: data/01_raw/bi_agg_listing.csv

# DB-based data catalog
trumpet_staging_dim_city:
  type: pandas.SQLTableDataSet
  credentials: trumpet_staging_creds
  table_name: "dim_city"
  load_args:
    columns: [Name,EnglishName]

```

**Note:** You should declare corresponding credentials for your DB-based Data Catalog in the step1.

_[Go to the next page](./04_dependencies.md)_
