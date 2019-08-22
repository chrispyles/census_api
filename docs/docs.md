# Docs

This page contains the documentation for the classes and methods in the `census_api` package.

---

**_class_ `census_query.CensusQuery`**

Object to query US Census API


**_method_ `census_query.CensusQuery.query(self, variables, state, county=None, tract="*", year=None)`**


Queries Census API to get data regarding listed variables; if `year` provided, ignores `CensusData` instance year

Args:

* `variables` (`list`): List of variables to extract
* `state` (`str`): Abbreviation for state from which to query data
* `county` (`str`): County name for localized queries
* `tract` (`str`): FIPS code for tract to query data from
* `year` (`int`): Year for which to query data; if provided, ignores instance `year`

Returns:

* `pandas.DataFrame` or `datascience.tables.Table`. The data retrieved from the query



---

**_function_ `utils.get_county_fips(county, state)`**


Uses `addfips` library to get FIPS codes for counties

Args:

* `county` (`str`): County to get FIPS code for
* `state` (`str`): Abbreviation for state that contains `county`

Returns:

* `str`. The FIPS code of `county`



**_function_ `utils.zero_pad_state(state)`**


Returns state FIPS code zero-padded to 2 digits

Args:

* `state` (`str`): The state to get FIPS code for

Returns:

* `str`. The FIPS code for `state`


