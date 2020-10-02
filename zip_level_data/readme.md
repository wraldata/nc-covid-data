# NC COVID-19 zip code data

This is a running repository for data captured daily by reporters from WRAL News via the [N.C. Department of Health and Human Services' zip code-level map](https://www.ncdhhs.gov/divisions/public-health/covid19/covid-19-nc-case-count#zip-code-map) of COVID-19 cases and deaths.

## Get the data

Download the time-series data in [CSV](https://github.com/wraldata/nc-covid-data/tree/master/zip_level_data/time_series_data/csv), [full geojson](https://github.com/wraldata/nc-covid-data/tree/master/zip_level_data/time_series_data/full_geojson) or a [reduced filesize geojson](https://github.com/wraldata/nc-covid-data/tree/master/zip_level_data/time_series_data/reduced_geojson). All files are stamped with the datetime in YYYYMMDDHHMM format.

## Methodology

This process of updating this repo is fully automatated as pf Oct. 2.

We're using [py esri dump](https://github.com/openaddresses/pyesridump) to capture the raw data from the [map layer published daily](https://nc.maps.arcgis.com/home/item.html?id=52f127a0767149ec984e91fcc06b06cb#overview) via the State of North Carolina's ArcGIS account. [The rest endpoint is here](https://services.arcgis.com/iFBq2AW9XO0jYYF7/arcgis/rest/services/Covid19byZIPnew/FeatureServer/0).

After the geoJSON file is captured, we use [MapShaper](https://mapshaper.org/) to reduce the file size to 10 percent to speed up load times and download as a simplified geojson file.

We're then use the [pandas library](https://pandas.pydata.org/) to export the file in CSV format and push the resulting files to this GitHub repo.

The scraper runs every 15 minutes.

## Data notes
 - **May 1** Geojson files not captured by WRAL
 - **May 20** DHHS changed its [data dashboard](https://covid19.ncdhhs.gov/dashboard) from ArcGIS to Tableau, which did not allow direct downloads, resulting in an interruption of the data capture.
 - **May 23** After confirming that the state's ArcGIS data was still being updated, WRAL News began capturing the data again from this resource. The state considers the data on its new Tableau dashboard to be the most up-to-date zip code information. But the shapefiles used by that platform are slightly different than those used in the ArcGIS platform (ZIP codes [are not standardized shapes](https://carto.com/blog/zip-codes-spatial-analysis/), per se, and change often). Because both platforms provide some level of data cleaning/geocoding to place addresses in the appropriate zip codes when aggregating cases and deaths, numbers on the state's new dashboard may not align 100% with the ArcGIS data used for WRAL's map.
 - **Aug. 6** NCDHHS noted that laboratory omissions affected data from Aug. 2 to Aug. 5. [They posted an analysis of the changes here](https://files.nc.gov/covid/documents/dashboard/Aug2-5_NCDHHS_DataUpdate.xlsx)
 - **Aug. 10** NCDHHS noted that a laboratory had failed to submit its entire data file on time.
 - **Sept. 25** NCDHHS announced they were now including both PCR and antigen tests in their results of cases and deaths. [They posted an FAQ of the changes here](https://files.nc.gov/covid/documents/dashboard/Antigen-Testing-Frequently-Asked-Questions.pdf), but they'll mean more cases/deaths as of this date going forward.
 - **Sept. 29** NCDHHS reported that technical issues prevented some laboratory data files from being processed, leading to lower cases and test totals on Sept. 29 and higher than normal numbers on Sept. 30
 - **Oct. 2** WRAL switches from a manual to an automated process of capturing zip code-level data.