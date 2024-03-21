---
title: "Gold Standard Examples"
keywords: [ioos, metadata, netCDF, gold-standard]
tags: [ioos, metadata, netCDF, gold-standard]
toc: false
#permalink: gold-standard-examples.html
summary:  Describes gold standard examples for various dataset types and scenarios.
---


## **Overview**

The page provides links to example datasets that satisfy the [IOOS Metadata Profile 1.2](./ioos-metadata-profile-v1-2).

Since the IOOS standard builds off of the [**NOAA NCEI NetCDF Templates**](https://www.nodc.noaa.gov/data/formats/netcdf/), the NCEI "Gold Standard" examples ([HTTP](https://data.nodc.noaa.gov/ncei/example/data/netcdf/), [THREDDS](https://data.nodc.noaa.gov/thredds/catalog/example/catalog.html)) provide a great starting point.

The IOOS Gold Standard Examples focus on IOOS-specific guidelines, and can serve as templates for data providers interested in implementing the profile.  In addition to the dataset links below, IOOS maintains a fully-deployable ERDDAP instance that includes both the example data and configuration files.  Consult the following link for more information:

* [IOOS "ERDDAP Gold Standard" GitHub Repository](https://github.com/ioos/erddap-gold-standard) and [Live ERDDAP server](https://standards.sensors.ioos.us/erddap/index.html)

## **Dataset Types and Examples**

### Fixed station, met package

This is the simplest scenario: an ERDDAP dataset with a single fixed station and a single package.

Links:

* [ERDDAP Dataset](https://erddap.cencoos.org/erddap/tabledap/edu_calpoly_marine_morro_bay_met.html)
* [View in CeNCOOS Data Portal](https://data.cencoos.org/#metadata/57163/station)

### Moored buoy, met package and currents package

In this example, the two packages are broken up into two ERDDAP datasets.

* Met
  * [ERDDAP Dataset (DSG TimeSeries)](https://erddap.secoora.org/erddap/tabledap/edu_usf_marine_comps_c10.html)
  * [In SECOORA Data Portal](https://portal.secoora.org/#metadata/60387/station)
* Currents
  * [ERDDAP Dataset (DSG TimeSeriesProfile)](https://erddap.secoora.org/erddap/tabledap/c10-water-velocity-wfs-central-b.html)
  * [In SECOORA Data Portal](https://portal.secoora.org/#metadata/100167/station)

### Station, multiple packages, single dataset

*Example coming soon...*

### GTS Ingest

The [WQB_04](https://pae-paha.pacioos.hawaii.edu/erddap/info/wqb_04/index.html) and [WQB_05](https://pae-paha.pacioos.hawaii.edu/erddap/info/wqb_05/index.html) PacIOOS buoys are actively used by NDBC for collecting data.

### Moving station, UAV with sub-surface measurements

*Example coming soon...*

### Moving station, series of CTD casts from a cruise

*Example coming soon...*

### Moving station, Wave Glider

*Example coming soon...*
