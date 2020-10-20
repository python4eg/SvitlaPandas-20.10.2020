# SvitlaPandas-20.10.2020

https://prezi.com/p/w2gt4njjk7xc - Prezi presentation

Code examples from presentation:
```python
import io
import asyncio

import aiohttp #async requests
import pandas as pd


async def get_csv_async(client, type, url):
    async with client.get(url) as response:
        with io.StringIO(await response.text()) as text_io:
            return type, pd.read_csv(text_io)  # it supports file objects as well


async def get_all_csvs_async(covid_statistic_files):
    async with aiohttp.ClientSession() as client:
        futures = [get_csv_async(client, type, url) for type, url in covid_statistic_files.items()]
        return await asyncio.gather(*futures)


if '__main__' == __name__:
    covid_statistic_files = {
        'all': 'https://github.com/owid/covid-19-data/raw/master/public/data/owid-covid-data.csv',
        'tests': 'https://github.com/owid/covid-19-data/raw/master/public/data/testing/covid-testing-all-observations.csv',
        'who': 'https://raw.githubusercontent.com/owid/covid-19-data/master/public/data/who/full_data.csv',
    }
    dfs = asyncio.run(get_all_csvs_async(covid_statistic_files))
```



Table Markdown:
|       | iso_code   | continent   | location   | date                |   total_cases |   new_cases |   new_cases_smoothed |   total_deaths |   new_deaths |   new_deaths_smoothed |   total_cases_per_million |   new_cases_per_million |   new_cases_smoothed_per_million |   total_deaths_per_million |   new_deaths_per_million |   new_deaths_smoothed_per_million |   total_tests |   new_tests |   total_tests_per_thousand |   new_tests_per_thousand |   new_tests_smoothed |   new_tests_smoothed_per_thousand |   tests_per_case |   positive_rate |   tests_units |   stringency_index |   population |   population_density |   median_age |   aged_65_older |   aged_70_older |   gdp_per_capita |   extreme_poverty |   cardiovasc_death_rate |   diabetes_prevalence |   female_smokers |   male_smokers |   handwashing_facilities |   hospital_beds_per_thousand |   life_expectancy |   human_development_index |
|------:|:-----------|:------------|:-----------|:--------------------|--------------:|------------:|---------------------:|---------------:|-------------:|----------------------:|--------------------------:|------------------------:|---------------------------------:|---------------------------:|-------------------------:|----------------------------------:|--------------:|------------:|---------------------------:|-------------------------:|---------------------:|----------------------------------:|-----------------:|----------------:|--------------:|-------------------:|-------------:|---------------------:|-------------:|----------------:|----------------:|-----------------:|------------------:|------------------------:|----------------------:|-----------------:|---------------:|-------------------------:|-----------------------------:|------------------:|--------------------------:|
| 47345 | UKR        | Europe      | Ukraine    | 2020-03-04 00:00:00 |             1 |           1 |              nan     |            nan |            0 |                   nan |                     0.023 |                   0.023 |                          nan     |                        nan |                        0 |                               nan |           nan |         nan |                        nan |                      nan |                  nan |                               nan |              nan |             nan |           nan |              11.11 |  4.37338e+07 |                77.39 |         41.4 |          16.462 |          11.133 |          7894.39 |               0.1 |                 539.849 |                  7.11 |             13.5 |           47.4 |                      nan |                          8.8 |             72.06 |                     0.751 |
| 47353 | UKR        | Europe      | Ukraine    | 2020-03-17 00:00:00 |             5 |           2 |                0.571 |            nan |            0 |                     0 |                     0.114 |                   0.046 |                            0.013 |                        nan |                        0 |                                 0 |           nan |         nan |                        nan |                      nan |                  nan |                               nan |              nan |             nan |           nan |              77.78 |  4.37338e+07 |                77.39 |         41.4 |          16.462 |          11.133 |          7894.39 |               0.1 |                 539.849 |                  7.11 |             13.5 |           47.4 |                      nan |                          8.8 |             72.06 |                     0.751 |
| 47349 | UKR        | Europe      | Ukraine    | 2020-03-13 00:00:00 |             3 |           2 |                0.286 |            nan |            0 |                     0 |                     0.069 |                   0.046 |                            0.007 |                        nan |                        0 |                                 0 |           nan |         nan |                        nan |                      nan |                  nan |                               nan |              nan |             nan |           nan |              50    |  4.37338e+07 |                77.39 |         41.4 |          16.462 |          11.133 |          7894.39 |               0.1 |                 539.849 |                  7.11 |             13.5 |           47.4 |                      nan |                          8.8 |             72.06 |                     0.751 |
