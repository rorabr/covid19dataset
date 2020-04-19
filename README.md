# covid19dataset

Datasets created for the projectcovid19 application and web dashboards for displaying COVID19 pandemic data in JSON.

## Projecting COVID19 pandemic cases

These datasets were created as a result of an attempt to project the confirmed cases of the first
wave of infection of the COVID19 pandemic across the world. The results of these projections are
available online in this link:

[https://rora.com.br/#/covid19delta](https://rora.com.br/#/covid19delta "Projection of the COVID19 confirmed cases")

Most of the information was obtained form the JHU dataset available in github at <https://github.com/CSSEGISandData/COVID-19>.
The population list was obtained from the World Bank Data at <https://data.worldbank.org/indicator/SP.POP.TOTL>.

These are JSON files containing information for charts, tables and statistics. Some information is
repeated across different files.

## covid19_country.json

List of data for each country with a confirmed case of COVID19. It does not contain all countries in the world (yet).
Some information is not accurate (ie longitude and latitude).

```json
{
   "Greece" : {
      "name" : "Greece",
      "country_id" : 46,
      "iso" : "GR",
      "lon" : 21.8243,
      "lat" : 39.0742
   },
   "South Africa" : {
      "name" : "South Africa",
      "country_id" : 90,
      "iso" : "ZA",
      "lon" : 22.9375,
      "lat" : -30.5595
   },
   "Kazakhstan" : {
      "name" : "Kazakhstan",
      "country_id" : 130,
      "iso" : "",
      "lon" : 0,
      "lat" : 0
   },
...
}

```

## covid19_countrydict.json

Dictionary to normalize country names across different datasets to a unique name and discard regions
made up of groups of countries. The key is the country name as listed in the JHU dataset or the World
Bank population data and the right (or content) is the name used in this datasets.

```json

{
   "IDA only" : "",
   "Fragile and conflict affected situations" : "",
   "The Bahamas" : "Bahamas",
   "Republic of Korea" : "South Korea",
   "US" : "United States of America",
   "South Asia" : "",
   "Czechia" : "Czech Republic",
   "Yemen, Rep." : "Yemen",
   "Korea, Dem. People’s Rep." : "North Korea",
   "St. Martin (French part)" : "Saint Martin",
   "Korea, South" : "South Korea",
   "East Timor" : "Timor-Leste",
...
}
```

## covid19_data.json

COVID19 data from JHU grouped by country_id (same as covid19_country.json) and then by date (yyyy-mm-dd format).
Each data record is an array of:

0. Confirmed cases
1. Deaths
2. Recovered
3. Active cases (confirmed - deaths - recovered)
4. Confirmed cases per million of people
5. Deaths per million of people
6. Recovered per million of people
7. Active cases per million of people
8. Death rate in % (confirmed cases divided by deaths)
9. Country's population in millions (or "" if not available)
10. Delta confirmed (between the current date and previous date, 0 for the first date)
11. Delta deaths
12. Delta recovered
13. Delta active cases

```json
{
   "167" : {
      "2020-01-25" : [
         0,
         0,
         0,
         0,
         0,
         0,
         0,
         0,
         "",
         56.3,
         0,
         0,
         0,
         0
      ],
      "2020-01-23" : [
         0,
         0,
         0,
         0,
         0,
         0,
         0,
         0,
...
      ]
   }
}
```

## covid19_charttime.json

Information ready to be displayed as charts and a data table containing the data grouped by country.

## covid19_chartdelta.json

Information ready to be displayed as charts and a data table containing the projections of confirmed
cases and deaths of COVID19 based on the logistic progression obtained by matching the curve to the
confirmed cases data by using a genetic algorythm regression.

## covid19_project.json

COVID19 pandemic projection data. Each projection data is grouped by date of the dataset used and then
by country_id.

```json
{
   "2020-04-14" : {
      "159" : {
        ...
      },
      "7" : {
        ...
      }
    },
    ...
}
```

Each projection contains:

```json
       {
         "key" : "2020-04-14",
         "fitScore" : 0.99630934076487
         "projected" : [
           ...
         ],
         "milestones" : {
            "date0" : "2020-01-22",
            "start" : "2020-03-16",
            "inflection" : "2020-04-02",
            "end" : "2020-04-19"
            "duration" : 34,
         },
         "result" : {
            "x0" : 70.938862150822,
            "L" : 1925.5308832979
            "k" : 0.16437898810714,
         },
         "stats" : {
            "populationLimit" : 16384,
            "generationLimit" : 64,
            "mutationRate" : 0.01,
            "totalTime" : 49.625832080841,
            "generations" : 64
            "startTimestamp" : 1586948150.9424,
            "startVarsGiven" : 0,
            "numberOfVariables" : 3,
            "populationSorted" : 64,
            "individualsRemoved" : 185700,
            "stopTimestamp" : 1586948200.5682,
            "elapsedTime" : 49.625832080841,
            "generationsPerSec" : 1.2896509200237,
            "genWithoutImprov" : 12,
            "genLastWithImprov" : 52,
            "finalScore" : 79425.512205319,
            "stopReason" : "genLimit reached",
         },
         "generatedOn" : "2020-04-15 07:56:40 -0300",
       }

```

The key field is the same date used as grouping (the JHU dataset date used in the projection). The fitScore is the R^2 coeficient of determination of
the logistic progression. Projected is an array of values calculated using the sigmoid function described by the result variables that best fit the
epidemic progression. Milestores are dates related to the begining, midpoint and end of the epidemic as well as duration in days. Results are the
variables of the sigmoid funcion. Stats are statistics generated by the genetic algorythm used to find the results.

## TODO 

Improve documentation

