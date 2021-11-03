# Analysis of New York City's unemployment rate for the year of 2020 by census tract and median income and market rental rate data sets from 01/2014 to 08/2020

This repository contains data, analytic code, and findings that support portions of an  article on housing insecurity in New York City.

## Data

This analysis uses Jupyter Notebooks, CSVs, and Google Sheets.

The CSVs come from the following sources:

#### DEEP-MAPS model of the labor force

`Data/deepmaps_tractdata_december2020_prelim.csv`: Shows estimates of unemployment and labor force participation by race, education, age, gender, marital status, and citizenship for most census tracts in the U.S., including New York City. The Tract-Level Data for 2020 is too large to be added on Github but can be downloaded from https://www.deepmaps.io/data/.

#### Geographic identifiers

`Data/geoid.csv`: Shows geographic identifiers, or GEOIDs, and census tracts for New York City. This data was pared down from a dataset that can be downloaded at [Census Reporter](https://censusreporter.org/data/table/?table=B03002&geo_ids=140|16000US3651000).

#### ZIP codes

`Data/zip-tract.csv`: Shows ZIP codes and their corresponding census tracts for the U.S., including New York City. This data can be downloaded at [HUD USER](https://www.huduser.gov/portal/datasets/usps_crosswalk.html)

Each of the CSVs contain, among others, the following columns relevant to the analysis:

- `cat` — Estimates of unemployment and labor force participation by category
- `fips` — Federal Information Processing Series, or FIPS, for all of the U.S.
- `cnip_2020_12` - An estimate of the population for December 2020
- `laborforce_2020_12` — Labor Force Participants for December 2020
- `employed_2020_12` — Employed People for December 2020
- `unemployment_percent_2020_12` — Percentage of unemployment for December 2020
- `ZIP` — ZIP codes

#### Zillow Data
The Google spreadsheets come from [Zillow](https://www.zillow.com/research/data/) and include the following:

`Zip_ZORI_AllHomesPlusMultifamily_SSA`: Seasonally adjusted market rate rent for metropolitan areas across the U.S., including New York City, by zip code.

The spreadsheet contains, among others, the following columns relevant to the analysis:

- `RegionName` — Zip code
- `MsaName` — Metropolitan area
- `2014-01`through `2021-08` — Monthly-level rent

## Methodology

The notebook `Notebook/01-unemployment-analysis.ipynb` (`Notebook/01-unemployment-analysis.ipynb`) performs the following analyses:

##### Part 1: Creating a CSV file with unemployment data for December 2020 by ZIP code in New York City

- Took the DEEP-MAPS model of the labor force, which contains estimates of unemployment and labor force participation, and used it to create the unemployment percentage for December 2020 for ZIP codes in New York City.

#### Part 1.1: Examining the DEEP-MAPS model of the labor force
- Imported `unemployment-data.csv` into Jupyter Notebook (which can again be downloaded from https://www.deepmaps.io/data/) and changed the `fips` column into a string.

#### Part 1.2: Examining the GEOIDs and census tracks for New York City
- Imported `geoid.csv` (`Data/geoid.csv`) into Jupyter Notebook and shortened the GEOIDs in the `fips` column into FIPS.

#### Part 1.3: Merging data sets and filtering
- Merged `unemployment-data.csv` and `geoid.csv` on an inner join to to create a merged data set for the DEEP-MAPS model of the labor force for New York City only. Then the merged data set was filtered for the total estimates of unemployment and labor force participation in the `cat` column.

#### Part 1.4: Column changes
- The columns of the merged data set were then reduced to contain only the numbers for December 2020. The columns included `fips`, `cnip_2020_12`, `laborforce_2020_12` and `employed_2020_12`. A new column for the unemployment percentage in December 2020 was also created and titled `unemployment_percent_2020_12`. The unemployment percentage was then rounded to two decimals.

#### Part 1.5: Examining ZIP codes and their corresponding census tracts
- Imported `zip-tract.csv` (`Data/zip-tract.csv`) into Jupyter Notebook

#### Part 1.6: Merging data sets and filtering
- Merged `zip-tract.csv` and with the December 2020 data set for labor force in New York City only on an inner join to create a merged data set with the corresponding ZIP codes for the census tracts. The merged data set is then filtered to only include census tracts where the civilian non-institutionalized population is greater than 500.

#### Part 1.7: Exporting
- Exported `unemployment-zip_dec_2020.csv`.

#### Part 2: Joining the Unemployment data to ZORI
- Needed to join the unemployment data to Zillow Observed Rent Index (ZORI) for full picture of an area. (ZORI is a smoothed measure of the typical observed market rate rent across a given region.)

#### Part 2.1: Vlookup to Fuzzy merge datasets
- Used vlookup to merge `Output/unemployment-zip_dec_2020.csv` with `Data/Zip_ZORI_AllHomesPlusMultifamily_SSA.xlsx` based on zipcodes in `fullunemp` tab. The vlookup can be seen in the `ZORIpct_Vlookup` column.

#### Part 2.2: Determining ZORI Percent % Change
- In `ZORIpct_change` tab, determined the percent % from average ZORI values through August from 2014 and 2021. The result can be seen in `pctchange_2014to2021` column.

#### Part 2.3: Zipcodes most frequently in the worst 100 for unemployment
- Counted the most zipcodes which showed up most frequently in our unemployment data using a countif formula. The countif can be seen in 'count_of_top100unemployment' column.

#### Part 2.4: Focused in on target Zipcodes
- Based on the countif for frequency in top 100 worst unemployment rates and the ZORI median value, we determined that we would focus on zipcode 11207, the neighborhood of East New York in Brooklyn, with 10458, the neighborhood of Belmont in the Bronx, and 11435, the neighborhood of Jamaica in Queens as back ups.



## Outputs

The notebooks output this Jupyter Notebook which contains 1.1 to 1.7: `Output/unemployment-zip_dec_2020.csv` (`Output/unemployment-zip_dec_2020.csv`)
The notebooks output this spreadsheet which contains 2.1 to 2.6 (all analyses are on this [Google sheet](`https://docs.google.com/spreadsheets/d/1PV6VLQCc8OjDQaQYwmTnZX43krsblKHOzeeOh8_C78A/edit?usp=sharing`).


## Running the analysis yourself

You can run the analysis yourself. To do so, you'll need the following installed on your computer:

- Python 3
- The Python libraries include Pandas and NumPy

## Licensing

All code in this repository is available under the [MIT License](https://opensource.org/licenses/MIT). The data file in the output/ directory is available under the [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0) license. All files in the data/ directory are released into the public domain.

## Feedback / Questions?

Contact Anna Deen at anna.deen00@journalism.cuny.edu, Jessica Lerner at jessica.lerner47@journalism.cuny.edu, or Jacob Schermerhorn at jacob.schermerhorn53@journalism.cuny.edu.
