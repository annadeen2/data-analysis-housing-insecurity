# data-analysis-housing-insecurity

# Analysis of New York City's unemployment rate throughout 2020 by census tract and median income and market rental rate data sets from 01/2014 to 08/2020

This repository contains data, analytic code, and findings that support portions of an upcoming article on housing insecurity in New York City.

## Data

This analysis uses Jupyter Notebooks, CSVs, and Google spreadsheets.

The CSVs come from the following sources:

- The DEEP-MAPS model of the labor force:
  - `Unemployment-data.csv`: Shows estimates of unemployment and labor force participation by race, education, age, gender, marital status, and citizenship for most census tracts in the U.S., including New York City. The Tract-Level Data for 2020 (retitled unemployment-data.csv for this analysis) can be downloaded from https://www.deepmaps.io/data/.
- Geographic identifiers: 
  - `geoid.csv`: Shows geographic identifiers, or GEOIDs, and census tracts for New York City
- ZIP codes:
  - `zip-tract.csv`: Shows ZIP codes and their corresponding census tracts for the U.S., including New York City

Each of the CSVs contain, among others, the following columns relevant to the analysis:

- `cat` — Estimates of unemployment and labor force participation by category
- `fips` — Federal Information Processing Series, or FIPS, for all of the U.S.
- `laborforce_2020_12` — Labor Force Participants for December 2020
- `employed_2020_12` — Employed People for December 2020
- `unemployment_percent_2020_12` — Percentage of unemployment for December 2020
- `ZIP` — ZIP codes

The Google spreadsheets come from the following sources:

- Zillow Observed Rent Index:
  - `Zip_ZORI_AllHomesPlusMultifamily_SSA`: Raw data of smoothed, seasonally adjusted market rate rent for metropolitan areas across the U.S., including New York City, by zip code.
- Tract-Level Data for 2020:
  - `Zip_ZORI_AllHomesPlusMultifamily_SSA`: Raw data of census tract-level data for unemployment rates across the U.S., including New York City

Each of the spreadsheets contain, among others, the following columns relevant to the analysis:

- `RegionName` — Zip code
- `MsaName` — Metropolitan area
- `2014-01`through `2021-08` — Monthly-level rent

## Methodology

The documents perform the following analyses:

##### Part 1: TKTK

- Description of what you did with the data


##### Part 2: TKTK

- Description of what you did with the data


2.0 (Jacob) - The Googlesheet [`https://docs.google.com/spreadsheets/d/1PV6VLQCc8OjDQaQYwmTnZX43krsblKHOzeeOh8_C78A/edit?usp=sharing`] performs the following analyses:

#### Part 2.1: Vlookup to merge datasets
- Used vlookup to merge the cleaning work Jessica did with `Unemployment-data-file` with 'Zip_ZORI_AllHomesPlusMultifamily_SSA` based on zipcodes in `fullunemp` tab.

#### Part 2.2: SUMIF and AVERAGEIF
- Used SUMIF to add all `cnip_2020_12`, `laborforce_2020_12`, and `employed_2020_12` for zipcodes as they were multiple entries in `Unemployment-data-file ` with the same zipcode.
- Used AVERAGEIF to determine the average unemployment rate in `unemployment_percent_2020_12` for zipcodes as they also had multiple entries in `Unemployment-data-file`

#### Part 2.3: Vlookup to MAPZIP
- Used Vlookup to get the values in the zipcode determination that works best for the flourish map model (seen at the end of the process)

#### Part 2.4: Percent change in ZORI
- Moved to `ZORIpct` tab which had the ZORI for all avaliable zipcodes (contacted Zillow as to why there are gaps, still have not recieved a response) for 2014 and 2021 from January to August.
- Used a percent change formula to see the change and threw some conditional formatting on it for fun.

#### Part 2.5: Merging them all together
- The "mapfilter" tab was used to put the complete list of Unemployment and ZORI for all possible zipcodes in one sheet. Additionally, I added the `cnip_2020_12` as it has the estimated population for each zipcode.
- Once again, vlookup-ed the values to put it in a flourish-friendly zipcode format.

#### Part 2.6: Creating the Flourish Map
- The flourish map can be seen here - https://public.flourish.studio/visualisation/7600601/
- Based on our findings, we determined that the zipcodes with the highest unemployment and high ZORI rates were 11207, 11233 (Brooklyn), 10458, 10462 (Bronx), 11435, 11432, (Queens), and 10039 (Manhattan)


## Outputs

The notebooks output this spreadsheet which contains TKTK: [`output/tktktk.csv`](output/tktktk.csv).
The notebooks output this spreadsheet which contains 2.1 to 2.6 (all analysis on the Googlesheet): [`https://docs.google.com/spreadsheets/d/1PV6VLQCc8OjDQaQYwmTnZX43krsblKHOzeeOh8_C78A/edit?usp=sharing`]


## Running the analysis yourself

You can run the analysis yourself. To do so, you'll need the following installed on your computer:

- Jupyter Notebooks
- Python 3
- Google Sheets
- Microsoft Excel

## Licensing

All code in this repository is available under the [MIT License](https://opensource.org/licenses/MIT). The data file in the output/ directory is available under the [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0) license. All files in the data/ directory are released into the public domain.

## Feedback / Questions?

Contact Anna Deen at anna.deen00@journalism.cuny.edu, Jessica Lerner at jessica.lerner47@journalism.cuny.edu, or Jacob Schermerhorn at jacob.schermerhorn53@journalism.cuny.edu.
