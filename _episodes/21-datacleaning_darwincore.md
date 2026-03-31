---
title: "Data Cleaning for Darwin Core"
start: true
teaching: 0
exercises: 120
questions:
- "How to convert dates to ISO?"
- "How to match scientific names to GBIF?"
- "How to convert latitudes and longitudes to decimal degrees?"
objectives:
- "Aligning dates to the ISO 8601 standard."
- "Matching scientific names"
- "Converting latitude and longitude variations to decimal degrees North and East."
keypoints:
- "When doing conversions it's best to break out your data into it's component pieces."
- "Dates are messy to deal with. Some packages have easy solutions, otherwise use regular expressions to align date strings to ISO 8601."
- "Latitude and longitudes are like dates, they can be messy to deal with. Take a similar approach."
---

Some usefull links:

* [INBO/tutorials/](https://inbo.github.io/tutorials/tutorials/)
* [INBO/coding-club/](https://inbo.github.io/coding-club/)
* [/trias-project/checklist-recipe/wiki](https://github.com/trias-project/checklist-recipe/wiki)
* [data publication scripts](https://github.com/inbo/mica-occurrences/tree/master)

Now that you know what the mapping is between your raw data and the Darwin Core standard, it's time to start cleaning up 
the data to align with the conventions described in the standard. The following activities are the three most common 
conversions a dataset will undergo to align to the Darwin Core standard:
1. [Ensuring dates follow the ISO 8601 standard](#getting-your-dates-in-order)
2. [Matching scientific names to an authoritative resource](#matching-your-scientific-names-to-gbif)
3. [Ensuring latitude and longitude values are in decimal degrees](#getting-latlon-to-decimal-degrees)

Python is a high-level, general-purpose programming language. Its design philosophy emphasizes code readability with the use of significant indentation. Make sure that Python is installed on your machine.
You can download Python here: [https://www.anaconda.com/](https://www.anaconda.com/)
R is a language and environment for statistical computing and graphics. The core R language is augmented by a large number of extension packages, containing reusable code, documentation, and sample data. You can download R & Rstudio (visual interface) here: [https://posit.co/download/rstudio-desktop/](https://posit.co/download/rstudio-desktop/)

Below is a short summary of each of those conversions as well as some example conversion scripts. The exercises are 
intended to give you a sense of the variability we've seen in datasets and how we went about converting them. While the
examples use the [pandas package for Python](https://pandas.pydata.org/) and the [tidyverse collection of packages for R](https://www.tidyverse.org/)
(in particular the [lubridate](https://cloud.r-project.org/web/packages/lubridate/lubridate.pdf) package),
those are not the only options for dealing with these conversions but simply the ones we use more frequently in our 
experiences. 


# Getting your dates in order
Dates can be surprisingly tricky because people record them in many different ways. For our purposes we must follow 
[ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) which means using a four digit year, two digit month, and two digit 
day with dashes as separators (i.e. `YYYY-MM-DD`). You can also record time in ISO 8601 but make sure to include the time 
zone which can also get tricky if your data take place across time zones and throughout the year where daylight savings 
time may or may not be in effect (and start and end times of daylight savings vary across years). There are packages in 
R and Python that can help you with these vagaries. Finally, it is possible to record time intervals in ISO 8601 using a 
slash (e.g. `2022-01-02/2022-01-12`). Examine the dates in your data to determine what format they are following and what 
amendments need to be made to ensure they are following ISO 8601. Below are some examples and solutions in Python and R 
for them.

ISO 8601 dates can represent moments in time at different resolutions, as well as time intervals, which use "/" as a separator. Date and time are separated by "T". Timestamps can have a time zone indicator at the end. If not, then they are assumed to be local time. When a time is UTC, the letter "Z" is added at the end (e.g. 2009-02-20T08:40Z, which is the equivalent of 2009-02-20T08:40+00:00). 

> ## Tip 
> Focus on getting your package of choice to read the dates appropriately. While you can use [regular expressions](https://en.wikipedia.org/wiki/Regular_expression)
> to replace and substitute strings to align with the ISO convention, it will typically save you time if you work in 
> your package of choice to translate the dates.
{: .callout}
 
| Darwin Core Term | Description | Example   |
|------------------|-------------|-----------|
| [eventDate](https://dwc.tdwg.org/list/#dwc_eventDate) | The date-time or interval during which an Event occurred. For occurrences, this is the date-time when the event was recorded. Not suitable for a time in a geological context. | `1963-03-08T14:07-0600` (8 Mar 1963 at 2:07pm in the time zone six hours earlier than UTC).<br/>`2009-02-20T08:40Z` (20 February 2009 8:40am UTC).<br/>`2018-08-29T15:19` (3:19pm local time on 29 August 2018).<br/>`1809-02-12` (some time during 12 February 1809).<br/>`1906-06` (some time in June 1906).<br/>`1971` (some time in the year 1971).<br/>`2007-03-01T13:00:00Z/2008-05-11T15:30:00Z` (some time during the interval between 1 March 2007 1pm UTC and 11 May 2008 3:30pm UTC).<br/>`1900/1909` (some time during the interval between the beginning of the year 1900 and the end of the year 1909).<br/>`2007-11-13/15` (some time in the interval between 13 November 2007 and 15 November 2007). |

> ## Examples in Openrefine
>
> When dealing with dates using Openrefine, there are a few base tricks that are useful to wrangle your dates in the correct format. 
>
> The examples below show how to use the `Openrefine` and format your data to the ISO-8601 standard.  [Here](https://openrefine.org/docs/manual/grelfunctions#date-functions) is an overview of the Openrefine data functions.
> In openrefine code has to be entered here:
> ![openrefineSplit](../assets/code/refine1.PNG)
> 
> <br/>
> 1.  `01/31/2021 17:00 GMT` <br/>
> Choose `edit cells`, --> `common transforms` --> `toDate`
> Choose `add column based on this column`
>
>     ```
>      value.toDate('yyyy/mm/dd').toString('yyyy-MM-dd')
>     ```
>     If you have multiple date formats in one column.
>     ```
>      value.toDate('MM/yy','MMM-yy').toString('yyyy-MM')
>     ```
>     "If parsing a date with text components in a language other than your system language you can specify a language code as the format1 argument. For example, a French language date such as "10 janvier 2023".
>     ```
>     value.toDate('fr','dd MMM yyyy') 
>     ```
> 2. Another option is to split your date columns in 3 separate columns using the split function. After splitting join the columns in a data format code:
>    ![openrefineSplit](../assets/code/refine2.PNG)
>    
>    ```
>       cells["year"].value + "-" +cells["month"].value + "-" + cells["day"].value
>    ```
>   
{: .solution}


> ## Examples in Python
> 
> When dealing with dates using pandas in Python it is best to create a Series as your time column with the appropriate 
> datatype. Then, when writing your file(s) using [.to_csv()](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_csv.html)
> you can specify the format which your date will be written in using the `date_format` parameter. 
>
> The examples below show how to use the [pandas.to_datetime()](https://pandas.pydata.org/docs/reference/api/pandas.to_datetime.html)
> function to read various date formats. The process can be applied to entire columns (or Series) within a DataFrame.
> <br/>
> 1. `01/31/2021 17:00 GMT`
> 
>    This date follows a typical date construct of `month`**/**`day`**/**`year` `24-hour`**:**`minute` `time-zone`. The 
>    pandas `.to_datetime()` function will correctly interpret these dates without the `format` parameter.
> 
>    ```python
>    import pandas as pd
>    df = pd.DataFrame({'date':['01/31/2021 17:00 GMT']})
>    df['eventDate'] = pd.to_datetime(df['date'], format="%m/%d/%Y %H:%M %Z")
>    df
>    ```
>    ```output
>                       date                 eventDate
>       01/31/2021 17:00 GMT 2021-01-31 17:00:00+00:00
>    ``` 
>    
> 2. `31/01/2021 12:00 EST`
> 
>    This date is similar to the first date but switches the `month` and `day` and identifies a different `time-zone`.
>    The construct looks like `day`**/**`month`**/**`year` `24-hour`**:**`minute` `time-zone`
>    ```python
>    import pandas as pd
>    df = pd.DataFrame({'date':['31/01/2021 12:00 EST']})
>    df['eventDate'] = pd.to_datetime(df['date'], format="%d/%m/%Y %H:%M %Z")
>    df
>    ```
>    ```output
>                       date                 eventDate
>       31/01/2021 12:00 EST 2021-01-31 12:00:00-05:00
>    ``` 
>    
> 3. `January, 01 2021 5:00 PM GMT`
>    
>    ```python
>    import pandas as pd
>    df = pd.DataFrame({'date':['January, 01 2021 5:00 PM GMT']})
>    df['eventDate'] = pd.to_datetime(df['date'],format='%B, %d %Y %I:%M %p %Z')
>    df
>    ```
>    ```output
>                               date                 eventDate
>       January, 01 2021 5:00 PM GMT 2021-01-01 17:00:00+00:00
>    ```
>    
> 4. `1612112400` in seconds since 1970
>    
>    This uses the units of `seconds since 1970` which is common when working with data in [netCDF](https://www.unidata.ucar.edu/software/netcdf/).
>    ```python
>    import pandas as pd
>    df = pd.DataFrame({'date':['1612112400']})
>    df['eventDate'] = pd.to_datetime(df['date'], unit='s', origin='unix')
>    df
>    ```
>    ```output
>             date           eventDate
>       1612112400 2021-01-31 17:00:00
>    ```
> 5. `44227.708333333333`
>    
>    This is the numerical value for dates in Excel because Excel stores dates as sequential serial numbers so that they 
>    can be used in calculations. In some cases, when you export an Excel spreadsheet to CSV, the 
>    dates are preserved as a floating point number.
>    ```python
>    import pandas as pd
>    df = pd.DataFrame({'date':['44227.708333333333']})
>    df['eventDate'] = pd.to_datetime(df['date'].astype(float), unit='D', origin='1899-12-30')
>    df
>    ```
>    ```output
>                     date                     eventDate
>       44227.708333333333 2021-01-31 17:00:00.000000256
>    ```
> 6. Observations with a start date of `2021-01-30` and an end date of `2021-01-31`.
> 
>    Here we store the date as a duration following the ISO 8601 convention. In some cases, it is easier to use a regular 
>    expression or simply paste strings together:
>    ```python
>    import pandas as pd
>    df = pd.DataFrame({'start_date':['2021-01-30'],
>                       'end_date':['2021-01-31']})
>    df['eventDate'] = df['start_time']+'/'+df['end_time']
>    df
>    ```
>    ```output
>       start_time    end_time              eventDate
>       2021-01-30  2021-01-31  2021-01-30/2021-01-31
>    ```
>
{: .solution}

> ## Examples in R
>
> When dealing with dates using R, there are a few base functions that are useful to wrangle your dates in the correct format. An R package that is useful is [lubridate](https://cran.r-project.org/web/packages/lubridate/lubridate.pdf), which is part of the `tidyverse`. It is recommended to bookmark this [lubridate cheatsheet](https://evoldyn.gitlab.io/evomics-2018/ref-sheets/R_lubridate.pdf).
>
> The examples below show how to use the `lubridate` package and format your data to the ISO-8601 standard.
> <br/>
> 1.  `01/31/2021 17:00 GMT`
> 
>    ```r
>    library(lubridate)
>    date_str <- '01/31/2021 17:00 GMT'
>    lubridate::mdy_hm(date_str,tz="UTC")
>    date <- lubridate::format_ISO8601(date) # Separates date and time with a T.
>    date <- paste0(date, "Z") # Add a Z because time is in UTC.
>    ```
>    ```output
>    [1] "2021-01-31T17:00:00Z"
>    ```
> 2. `31/01/2021 12:00 EST`
> 
>    ```r
>    library(lubridate)
>    date_str <- '31/01/2021 12:00 EST'
>    date <- lubridate::dmy_hm(date_str,tz="EST")
>    lubridate::with_tz(date,tz="UTC")
>    date <- lubridate::format_ISO8601(date)
>    date <- paste0(date, "Z")
>    ```
>    ```output
>    [1] "2021-01-31T17:00:00Z"
>    ```
>
> 3. `January, 01 2021 5:00 PM GMT`
>
>    ```r
>    library(lubridate)
>    date_str <- 'January, 01 2021 5:00 PM GMT'
>    date <- lubridate::mdy_hm(date_str, format = '%B, %d %Y %H:%M', tz="GMT")
>    lubridate::with_tz(date,tz="UTC")
>    lubridate::format_ISO8601(date)
>    date <- paste0(date, "Z")
>    ```
>    ```output
>    [1] "2021-01-01T17:00:00Z"
>    ```
>    
> 4. `1612112400` in seconds since 1970
>
>    This uses the units of `seconds since 1970` which is common when working with data in [netCDF](https://www.unidata.ucar.edu/software/netcdf/).
>
>    ```r
>    library(lubridate)
>    date_str <- '1612112400'
>    date_str <- as.numeric(date_str)
>    date <- lubridate::as_datetime(date_str, origin = lubridate::origin, tz = "UTC")
>    date <- lubridate::format_ISO8601(date)
>    date <- paste0(date, "Z")
>    print(date)
>    ```
>    ```output
>    [1] "2021-01-31T17:00:00Z"
>    ```
>    
> 5. `44227.708333333333`
>    
>    This is the numerical value for dates in Excel because Excel stores dates as sequential serial numbers so that they 
>    can be used in calculations. In some cases, when you export an Excel spreadsheet to CSV, the 
>    dates are preserved as a floating point number.
>
>    ```r
>    library(openxlsx)
>    library(lubridate)
>    date_str <- 44227.708333333333
>    date <- as.Date(date_str, origin = "1899-12-30") # If you're only interested in the YYYY-MM-DD
>    fulldate <- openxlsx::convertToDateTime(date_str, tz = "UTC")
>    fulldate <- lubridate::format_ISO8601(fulldate)
>    fulldate <- paste0(fulldate, "Z")
>    print(date)
>    print(fulldate)
>    ```
>    ```output
>    [1] "2021-01-31"
>    [1] "2021-01-31T17:00:00Z"
>    ```
> 6. Observations with a start date of `2021-01-30` and an end date of `2021-01-31`. For added complexity, consider adding in a 4-digit deployment and retrieval time.
> 
>    Here we store the date as a duration following the ISO 8601 convention. In some cases, it is easier to use a regular 
>    expression or simply paste strings together:
>    
>    ```r
>    library(lubridate)
>    event_start <- '2021-01-30'
>    event_finish <- '2021-01-31'
>    
>    deployment_time <- 1002
>    retrieval_time <- 1102
> 
>    Time is recorded numerically (1037 instead of 10:37), so need to change these columns:
>    deployment_time <- substr(as.POSIXct(sprintf("%04.0f", deployment_time), format = "%H%M"), 12, 16)
>    retrieval_time <- substr(as.POSIXct(sprintf("%04.0f", retrieval_time, format = "%H%M"), 12, 16)
>
>    # If you're interested in just pasting the event dates together:
>    eventDate <- paste(event_start, event_finish, sep = "/") 
>
>    # If you're interested in including the deployment and retrieval times in the eventDate:
>    eventDateTime_start <- lubridate::format_ISO8601(as.POSIXct(paste(event_start, deployment_time), tz = "UTC"))
>    eventDateTime_start <- paste0(eventDateTime_start, "Z")
>    eventDateTime_finish <- lubridate::format_ISO8601(as.POSIXct(paste(event_finish, retrieval_time), tz = "UTC"))
>    eventDateTime_finish <- paste0(eventdateTime_finish, "Z")
>    eventDateTime <- paste(eventDateTime_start, eventDateTime_finish, sep = "/") 
>    
>    print(eventDate)
>    print(eventDateTime)
>    ```
>    ```output
>    [1] "2021-01-30/2021-01-31"
>    [1] "2021-01-30T10:02:00Z/2021-01-31T11:02:00Z"
>    ```
{: .solution}

> ## Tip 
> When all else fails, treat the dates as strings and use substitutions/regular expressions to manipulate the strings 
> into ISO 8601. 
{: .callout}

# Matching your scientific names to a taxonomic backbone

## Introduction

Working with different partners/institutes/researchers results in a diversity of taxonomic names to define species. This hardens comparison amongst datasets, as in many occasions, aggrgeation is aimed for or filtering on specific species. By translating all species names to a common taxonomic backbone (ensuring unique ID's for each species name), this can be done. 


| Darwin Core Term         | Description                                                                       | Example                                               |
|--------------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------|
| [scientificNameID](https://dwc.tdwg.org/list/#dwc_scientificNameID) | An identifier for the nomenclatural (not taxonomic) details of a scientific name. | `urn:lsid:ipni.org:names:37829-1:1.3` |                
| [kingdom](https://dwc.tdwg.org/list/#dwc_kingdom) | The full scientific name of the kingdom in which the taxon is classified.         |   `Animalia`, `Archaea`, `Bacteria`, `Chromista`, `Fungi`, `Plantae`, `Protozoa`, `Viruses` |
| [taxonRank](https://dwc.tdwg.org/list/#dwc_taxonRank) | The taxonomic rank of the most specific name in the scientificName.               | `subspecies`, `varietas`, `forma`, `species`, `genus` |


> ## Using the commandline using Python
> This small utility provides the functionality to add the species information from the GBIF backbone to any data table (CSV-style or a > Pandas dataframe)
> by requesting this information via the GBIF API. For each match, the corresponding accepted name is looked for. Nevertheless there will always be errors and control is still essential, the
> acceptedkeys provide the ability to compare species names from different data sources.
> The functionality can be loaded within Python itself by importing the function `extract_species_information` or by running the script from the command line. We will show you on how to use the command line
>
> 1. Create a folder which will be used for name matching. 
>
> 2. Place your CSV (comma separated value) file with the scientific names of the species of interest in that folder. Here we are showing 
>    some of the contents of the file [`species.csv`]({{ page.root }}/data/species.csv).
>    ![screenshot]({{ page.root }}/fig/species_file_screenshot.png){: .image-with-shadow }
>
> 3. Place this Python file [gbif_species_name_match.py](https://github.com/inbo/inbo-pyutils/blob/master/gbif/gbif_name_match/gbif_species_name_match.py) in your name matching folder
>    ![screenshot]({{ page.root }}/fig/python_name_match_file_download.png){: .image-with-shadow }
> 
> 4. Navigate in the Python terminal to the correct folder. 
>    ![screenshot]({{ page.root }}/fig/python_name_match_screenshot.png){: .image-with-shadow }
>
>   
> 5. Run the command > python gbif_species_name_match.py **yourfilename_input.csv** **yourfilename_output**
{: .solution}



> ## Using the Global Names Verifier
> Verify a list of scientific names against biodiversity data-sources. This service parses incoming names, executes exact or fuzzy matching as required, and returns the best-scored result. Optionally, it can also return matches from data-sources selected by a user.
> 1. Create a CSV (comma separated value) file with the scientific name of the species of interest. Here we are showing 
>    some of the contents of the file [`species.csv`]({{ page.root }}/data/species.csv).
>    ![screenshot]({{ page.root }}/fig/species_file_screenshot.png){: .image-with-shadow }
>
> 2. Copy your scientific names to the [Global Names Verifier](https://verifier.globalnames.org/)
> ![screenshot]({{ page.root }}/fig/globalnamesverifier.PNG){: .image-with-shadow }
>  
> 3. Click on Search Names. Don't forget to choose your output format (here choose .csv)
>  
> 4. Hopefully, your names will be matched
>
>    1. In some cases you will have ambiguous matches.
>    2. Capy you response and use it building your Darwin Core file
>  
{: .solution}

# Getting lat/lon to decimal degrees

Latitude (`decimalLatitude`) and longitude (`decimalLongitude`) are the geographic coordinates (in decimal degrees north and east, respectively), using the spatial reference system given in `geodeticDatum` of the geographic center of a location.
* `decimalLatitude`, positive values are north of the Equator, negative values are south of it. All values lie between -90 and 90, inclusive. 
* `decimalLongitude`, positive values are east of the Greenwich Meridian, negative values are west of it. All values lie between -180 and 180, inclusive.

Note, that the requirement for `decimalLatitude` and `decimallLongitude` is they must be in decimal degrees in [WGS84](https://en.wikipedia.org/wiki/World_Geodetic_System). Since this is the requirement for Darwin Core, **OBIS and GBIF will assume data shared using those Darwin Core terms are in the geodetic datum `WGS84`**. We highly recommend checking the coordinate reference system (CRS) of your observations to confirm they are using the same datum and documenting it in the `geodeticDatum` Darwin Core term. If your coordinates are not using `WGS84`, they will need to be converted in order to share the data to OBIS and GBIF since `decimalLatitude` and `decimalLongitude` are required terms. 

Helpful packages for managing CRS and geodetic datum:
* python: [GeoPandas](https://geopandas.org/en/stable/getting_started.html) has a [utility](https://geopandas.org/en/stable/docs/user_guide/projections.html#re-projecting).
* R: [rgdal](https://cran.r-project.org/web/packages/rgdal/index.html) and [sp](https://cran.r-project.org/web/packages/sp/index.html).

> ## Tip 
> If at all possible, it's best to extract out the components of the information you have in order to compile the 
> appropriate field. For example, if you have the coordinates as one lone string `17° 51' 57.96" S 149° 39' 13.32" W`, 
> try to split it out into its component pieces: `17`, `51`, `57.96`, `S`, `149`, `39`, `13.32`, and `W` just be sure to 
> track which values are latitude and which are longitude.
{: .callout}

| Darwin Core Term | Description | Example        |
|------------------|-------------|----------------|
| [decimalLatitude](https://dwc.tdwg.org/list/#dwc_decimalLatitude) | The geographic latitude (in decimal degrees, using the spatial reference system given in geodeticDatum) of the geographic center of a Location. Positive values are north of the Equator, negative values are south of it. Legal values lie between -90 and 90, inclusive. | `-41.0983423`  |
| [decimalLongitude](https://dwc.tdwg.org/list/#dwc_decimalLongitude) | The geographic longitude (in decimal degrees, using the spatial reference system given in geodeticDatum) of the geographic center of a Location. Positive values are east of the Greenwich Meridian, negative values are west of it. Legal values lie between -180 and 180, inclusive. | `-121.1761111` |
| [geodeticDatum](https://dwc.tdwg.org/list/#dwc_geodeticDatum) | The ellipsoid, geodetic datum, or spatial reference system (SRS) upon which the geographic coordinates given in decimalLatitude and decimalLongitude as based. | `WGS84` |

![coordinate_precision](https://imgs.xkcd.com/comics/coordinate_precision.png){: .image-with-shadow }
*Image credit: [xkcd](https://xkcd.com/)*

> ## Examples in Python
> 
> 1. `17° 51' 57.96" S` `149° 39' 13.32" W`
>    * This example assumes you have already split the two strings into discrete components (as shown in the table). An 
>      example converting the full strings `17° 51' 57.96" S` `149° 39' 13.32" W` to decimal degrees can be found [here](https://github.com/MathewBiddle/misc/blob/07d643da831255069fd1f6e936ca0902e21c0d0c/data302_DON_Oxidation_working_hollibaugh_20190514_process.py#L24-L62).
> 
>    lat_degrees | lat_minutes | lat_seconds | lat_hemisphere | lon_degrees | lon_minutes | lon_seconds | lon_hemisphere
>    ------------|----|-------------|----------------|-------------|-------------|-------------|---------------
>    17 | 51 | 57.96 | S | 149 | 39 | 13.32 | W
> 
>    ```python
>    df = pd.DataFrame({'lat_degrees':[17],
>                       'lat_minutes':[51],
>                       'lat_seconds':[57.96],
>                       'lat_hemisphere':['S'],
>                       'lon_degrees': [149], 
>                       'lon_minutes': [39], 
>                       'lon_seconds':[13.32], 
>                       'lon_hemisphere': ['W'],
>                      })
>    
>    df['decimalLatitude'] = df['lat_degrees'] + ( (df['lat_minutes'] + (df['lat_seconds']/60) )/60)
>    df['decimalLongitude'] = df['lon_degrees'] + ( (df['lon_minutes'] + (df['lon_seconds']/60) )/60)
> 
>    # Convert hemisphere S and W to negative values as units should be `degrees North` and `degrees East`
>    df.loc[df['lat_hemisphere']=='S','decimalLatitude'] = df.loc[df['lat_hemisphere']=='S','decimalLatitude']*-1
>    df.loc[df['lon_hemisphere']=='W','decimalLongitude'] = df.loc[df['lon_hemisphere']=='W','decimalLongitude']*-1
>       
>    df[['decimalLatitude','decimalLongitude']]
>    ```
>    ```output
>       decimalLatitude  decimalLongitude
>              -17.8661         -149.6537
>    ```
>
> 2. `33° 22.967' N` `117° 35.321' W`
>    * Similar to above, this example assumes you have already split the two strings into discrete components (as shown 
>      in the table).
>  
>    lat_degrees | lat_dec_minutes | lat_hemisphere | lon_degrees | lon_dec_minutes | lon_hemisphere
>    ------------|-----------------|----------------|-------------|-----------------|---------------
>    33 | 22.967 | N | 117 | 35.321 | W
> 
>    ```python
>    df = pd.DataFrame({'lat_degrees':[33],
>                       'lat_dec_minutes':[22.967],
>                       'lat_hemisphere':['N'],
>                       'lon_degrees': [117], 
>                       'lon_dec_minutes': [35.321], 
>                       'lon_hemisphere': ['W'],
>                      })
>    
>    df['decimalLatitude'] = df['lat_degrees'] + (df['lat_dec_minutes']/60)
>    df['decimalLongitude'] = df['lon_degrees'] + (df['lon_dec_minutes']/60)
>    
>    # Convert hemisphere S and W to negative values as units should be `degrees North` and `degrees East`
>    df.loc[df['lat_hemisphere']=='S','decimalLatitude'] = df.loc[df['lat_hemisphere']=='S','decimalLatitude']*-1
>    df.loc[df['lon_hemisphere']=='W','decimalLongitude'] = df.loc[df['lon_hemisphere']=='W','decimalLongitude']*-1
>    
>    df[['decimalLatitude','decimalLongitude']]
>    ```
>    ```output
>    decimalLatitude  decimalLongitude
>    0        33.382783       -117.588683
>    ```
> 
{: .solution}

> ## Examples in R
> 1. `17° 51' 57.96" S` `149° 39' 13.32" W`
>
>    lat_degrees | lat_minutes | lat_seconds | lat_hemisphere | lon_degrees | lon_minutes | lon_seconds | lon_hemisphere
>    ------------|----|-------------|----------------|-------------|-------------|-------------|---------------
>    17 | 51 | 57.96 | S | 149 | 39 | 13.32 | W
> 
>    ```r
>    library(tibble)
>    tbl <- tibble(lat_degrees = 17,
>                  lat_minutes = 51,
>                  lat_seconds = 57.96,
>                  lat_hemisphere = "S",
>                  lon_degrees = 149,
>                  lon_minutes = 39, 
>                  lon_seconds = 13.32, 
>                  lon_hemisphere = "W")
>    
>    tbl$decimalLatitude <- tbl$lat_degrees + ( (tbl$lat_minutes + (tbl$lat_seconds/60)) / 60 )
>    tbl$decimalLongitude <- tbl$lon_degrees + ( (tbl$lon_minutes + (tbl$lon_seconds/60)) / 60 )
>    
>    tbl$decimalLatitude = as.numeric(as.character(tbl$decimalLatitude))*(-1)
>    tbl$decimalLongitude = as.numeric(as.character(tbl$decimalLongitude))*(-1)
>    ```
>    ```output
>    > tbl$decimalLatitude
>    [1] -17.8661
>    > tbl$decimalLongitude
>    [1] -149.6537
>   ```
>    
>    
> 2. `33° 22.967' N` `117° 35.321' W` 
>
>    lat_degrees | lat_dec_minutes | lat_hemisphere | lon_degrees | lon_dec_minutes | lon_hemisphere
>    ------------|-----------------|----------------|-------------|-----------------|---------------
>    33 | 22.967 | N | 117 | 35.321 | W
>
>    ```r
>    library(tibble)
>    tbl <- tibble(lat_degrees = 33,
>                  lat_dec_minutes = 22.967,
>                  lat_hemisphere = "N",
>                  lon_degrees = 117, 
>                  lon_dec_minutes = 35.321, 
>                  lon_hemisphere = "W")
>    
>    tbl$decimalLatitude <- tbl$lat_degrees + ( tbl$lat_dec_minutes/60 )
>    tbl$decimalLongitude <- tbl$lon_degrees + ( tbl$lon_dec_minutes/60 )
>    
>    tbl$decimalLongitude = as.numeric(as.character(tbl$decimalLongitude))*(-1)
>    ```
>    ```output
>    > tbl$decimalLatitude
>    [1] 33.38278
>    > tbl$decimalLongitude
>    [1] -117.5887
>    ```
> 
> 3. `33° 22.967' N` `117° 35.321' W`
>    * Using the [measurements package](https://cran.r-project.org/web/packages/measurements/measurements.pdf) the `conv_unit()` can work with space separated strings for coordinates.
>
>    lat | lat_hemisphere | lon | lon_hemisphere
>    ----|----------------|-----|---------------
>    33 22.967 | N | 117 35.321 | W
>    
>   ```r
>    tbl <- tibble(lat = "33 22.967",
>                  lat_hemisphere = "N",
>                  lon = "117 35.321", 
>                  lon_hemisphere = "W")
>   
>   tbl$decimalLongitude = measurements::conv_unit(tbl$lon, from = 'deg_dec_min', to = 'dec_deg')
>   tbl$decimalLongitude = as.numeric(as.character(tbl$decimalLongitude))*(-1)
>   
>   tbl$decimalLatitude = measurements::conv_unit(tbl$lat, from = 'deg_dec_min', to = 'dec_deg')
>   ``` 
>   ```output
>    > tbl$decimalLatitude
>    [1] 33.38278
>    > tbl$decimalLongitude
>    [1] -117.5887
>   ```
{: .solution}

You can find some more tutorials on data transformation and publication on the INBO tutorial page: [https://inbo.github.io/tutorials/](https://inbo.github.io/tutorials/)

{% include links.md %}
  
