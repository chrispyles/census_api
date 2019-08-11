# Usage

This page gives information on how to use the `census_api` package.

## Before you Start

Before you begin working with the US Census API, you need to obtain an API key. This can be done [here](https://api.census.gov/data/key_signup.html). I recommend putting your API key in a config.py file and adding this file to your `.gitignore` so that your key is saved offline if you intend on saving your results on Github.

## Using the Package

To use the `census_api` package, start by importing the library and the config file in which you placed your API key. In your working file, create an instance of the `CensusQuery` class. This requires you to pass your API key and a string identifying the dataset you would like to query. _As of now, we only support querying the ACS1 (`"acs1"`), ACS5 (`"acs5"`), and SF1 (`"sf1"`) datasets._ You can optionally also pass a year and an [output type](#Outputs) to the class instance.

```python
import config
import census_api
c = CensusQuery(config.api_key, "acs5", year=2016)
```

If you don't pass a year to the `CensusQuery` instance, you must pass it when you call `CensusQuery.query`. If you do pass a year, the year argument is optional in `CensusQuery.query`, but if it is passed, the instance variable will be ignored in favor of the year passed to `CensusQuery.query`.

To actually query the API, you must call `CensusQuery.query`. The required arguments are the list of variables to extract and the state (as its 2-letter abbreviation). You can also narrow your results by optionally passing a county name and a tract FIPS code, but these are not required. If they are not passed, the query returns all counties and all tracts. There is also an optional year argument, discussed in the previous paragraph.

```python
c.query(["NAME", "B00001_001E", "B01001_002M", "B06007PR_031E"], "CA")
```

If we wanted only tract 4010 of Alameda County in 2014, the call would be

```python
c.query(["NAME", "B00001_001E", "B01001_002M", "B06007PR_031E"], "CA", county="Alameda", tract="4010", year=2014)
```

For more information on the variables, see the [Census API documentation](https://api.census.gov/data/2009/acs5/variables.html). This page lists all of the data sets by year, so find the year and dataset that you are looking for and then click on "variables" in its row.

## Outputs

This package supports rendering outputs in two forms: as a `pandas` DataFrame or as a `datascience` Table. The class defaults to a DataFrame, but this is overridden by passing the optional `out` argument when creating the `CensusQuery` instance. This argument defaults to the string `"pd"`, but if `"ds"` is passed instead, the outputs will be Tables rather than DataFrames.

```python
ds_c = CensusQuery(config.api_key, "acs5", year=2016, out="ds")
```

For more information on how to use the package, launch our [Binder](https://mybinder.org/v2/gh/chrispyles/census_api/master?filepath=demo%2Fcensus_api-demo.ipynb).