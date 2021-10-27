# data-analysis-housing-insecurity

# Analysis of New York City's unemployment rate throughout 2020 by census tract and median income and market rental rate data sets from 01/2014 to 08/2020

This repository contains data, analytic code, and findings that support portions of an upcoming article on housing insecurity in New York City.

## Data

This analysis uses Jupyter Notebooks, CSVs, and Google spreadsheets.

The CSVs come from the following sources:

- The DEEP-MAPS model of the labor force:
  - `unemployment-data.csv`: Shows estimates of unemployment and labor force participation by race, education, age, gender, marital status, and citizenship for most census tracts in the U.S., including New York City. The Tract-Level Data for 2020 (retitled unemployment-data.csv for this analysis) can be downloaded from https://www.deepmaps.io/data/.
- Geographic identifiers: 
  - `geoid.csv`: Shows geographic identifiers, or GEOIDs, and census tracts for New York City
- ZIP codes:
  - `zip-tract.csv`: Shows ZIP codes and their corresponding census tracts for the U.S., including New York City

Each of the CSVs contain, among others, the following columns relevant to the analysis:

- `cat` — Estimates of unemployment and labor force participation by category
- `fips` — Federal Information Processing Series, or FIPS, for all of the U.S.
- `cnip_2020_12` - An estimate of the population for December 2020
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

The notebook `data-analysis.ipynb` (`Notebook/data-analysis.ipynb`) performs the following analyses:

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

The notebooks output this Jupyter Notebook which contains 1.1 to 1.7: `unemployment-zip_dec_2020.csv` (`Output/unemployment-zip_dec_2020.csv`)
The notebooks output this spreadsheet which contains 2.1 to 2.6 (all analysis on the Googlesheet): [`https://docs.google.com/spreadsheets/d/1PV6VLQCc8OjDQaQYwmTnZX43krsblKHOzeeOh8_C78A/edit?usp=sharing`]


## Running the analysis yourself

You can run the analysis yourself. To do so, you'll need the following installed on your computer:

- Python 3
- The Python libraries include Pandas and NumPy

## Licensing

All code in this repository is available under the [MIT License](https://opensource.org/licenses/MIT). The data file in the output/ directory is available under the [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0) license. All files in the data/ directory are released into the public domain.

## Feedback / Questions?

Contact Anna Deen at anna.deen00@journalism.cuny.edu, Jessica Lerner at jessica.lerner47@journalism.cuny.edu, or Jacob Schermerhorn at jacob.schermerhorn53@journalism.cuny.edu.
