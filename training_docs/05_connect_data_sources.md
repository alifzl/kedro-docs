# Add your datasets to `data`

In this section, we discuss the data set-up phase. The steps are as follows:

* Add datasets to your `data/` folder, according to [data engineering convention](https://kedro.readthedocs.io/en/stable/12_faq/01_faq.html#what-is-data-engineering-convention)
* Register the datasets with the Data Catalog in `conf/base/catalog.yml`, which is the registry of all data sources available for use by the project. This ensures that your code is reproducible when it references datasets in different locations and/or environments.

You can find further information about [the Data Catalog](https://kedro.readthedocs.io/en/stable/05_data/01_data_catalog.html) in specific documentation covering advanced usage.

## Add your datasets to `data`

The Trumpet-Data-Science tutorial makes use of sample datasets of Trumpet staging database. You will use the data to train a model to predict ___________________ . However, before you get to train the model, you will need to prepare the data for model building by creating a master table.

The Trumpet-Data-Science tutorial has two files and uses two data formats: `.csv` and `.xlsx`. accessible in the `data/01_raw/` folder of your project directory:

* [bi_agg_listing.csv](https://kedro-org.github.io/kedro/bi_agg_listing.csv)
* [bi_agg_listing.xlsx](https://kedro-org.github.io/kedro/bi_agg_listing.xlsx)


## Register the datasets

You now need to register the datasets so they can be loaded by Kedro. All Kedro projects have a `conf/base/catalog.yml` file, and you register each dataset by adding a named entry into the `.yml` file. The entry should include the following:

* File location (path)
* Parameters for the given dataset
* Type of data
* Versioning

Kedro supports a number of different data types, and those supported can be found in the API documentation. Kedro uses [`fssspec`](https://filesystem-spec.readthedocs.io/en/latest/) to read data from a variety of data stores including local file systems, network file systems, cloud object stores and HDFS.


### `csv`

For the spaceflights data, first register the `csv` datasets by adding this snippet to the end of the `conf/base/catalog.yml` file:

```yaml
agg_listings_csv:
  type: pandas.CSVDataSet
  filepath: data/01_raw/bi_agg_listing.csv
```

To check whether Kedro can load the data correctly, open a `kedro ipython` session and run:

```python
agg_listings_df = catalog.load("agg_listings_csv")
agg_listings_df.head()
```

The command loads the dataset named `agg_listings_csv` (as per top-level key in `catalog.yml`) from the underlying filepath `data/01_raw/bi_agg_listing.csv` into the variable `agg_listings_df`, which is of type `pandas.DataFrame`. The `head` method from `pandas` then displays the first five rows of the DataFrame.

When you have finished, close `ipython` session as follows:

```python
exit()
```

### `xlsx`

Now register the `xlsx` dataset by adding this snippet to the end of the `conf/base/catalog.yml` file:

```yaml
agg_listings_excel:
  type: pandas.ExcelDataSet
  filepath: data/01_raw/bi_agg_listing.xlsx
```

To test that everything works as expected, load the dataset within a _new_ `kedro ipython` session and display its first five rows:

```python
agg_listings_df = catalog.load("agg_listings_excel")
agg_listings_df.head()
```
When you have finished, close `ipython` session as follows:

```python
exit()
```

## Custom data

Kedro supports a number of datasets out of the box, but you can also add support for any proprietary data format or filesystem in your pipeline. 

You can find further information about [how to add support for custom datasets](https://kedro.readthedocs.io/en/stable/07_extend_kedro/03_custom_datasets.html) in specific documentation covering advanced usage.



## **All of Conventional databases are now added to template repository. For almost all the cases, there is no need for adding by yourself**


_[Go to the next page](./06_jupyter_notebook_workflow.md)_
