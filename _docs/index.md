---
title: IOOS NetCDF Application Profile
keywords: sample homepage
tags: [getting_started]
#sidebar: home_sidebar
sidebar: mydoc_sidebar
topnav: topnav
toc: false
#permalink: index.html
summary: Guidelines, links and examples to help the IOOS community to use netCDF and related related technologies like ncSOS, ncISO, OPeNDAP, THREDDS, ERDDAP, etc. to achieve interoperability. 
---

## **IOOS Profile Scope**{: style="color: crimson"}

The Profile defines the bare minimal set of attributes for IOOS Data Providers to include in their NetCDF data files. The Profile allows the NetCDF metadata to overlap with the IOOS SOS metadata in order to ensure a comprehensive cross-walk from NetCDF to IOOS SOS representation via the ncSOS service.
 
While matching the IOOS SOS metadata, the Profile allows the lowest achievable divergence of the IOOS NetCDF files from the NODC/NCEI NetCDF Templates - the Profile includes the Templates' attributes and augment them with a small number of IOOS-specific attributes just to ensure that NetCDF files inherently contain metadata required for the IOOS SOS output in cases when the NODC/NCEI Templates come short. 

In general, a Data Provider may use any metadata attributes in the NetCDF file; however, apart from the IOOS-specific portion, the IOOS Profile highly recommends to restrict the variety to the attributes and values provided by the following Conventions and Templates:

* [**NOAA NCEI NetCDF Templates v2.0**](http://www.nodc.noaa.gov/data/formats/netcdf/). 
* [**Climate and Forecast (CF) Conventions v1.6**](http://cf-pcmdi.llnl.gov/documents/cf-conventions/1.6/cf-conventions.html).
* [**ACDD v1.3**](http://wiki.esipfed.org/index.php/Attribute_Convention_for_Data_Discovery_1-3). 


## [**IOOS Metadata Profile for NetCDF, Version 1.1**{: style="color: crimson"}](./ioos-netcdf-metadata-description-v1-1.html)

This document provides a description of the **valid**{: style="color: green"} IOOS NetCDF Metadata Profile that IOOS Program Office has developed for distribution of the IOOS data using THREDDS or ERDDAP servers. The use of the Profile is strongly recommended to all IOOS Data Providers, including RAs and various DACs.

## [**IOOS Metadata Profile for NetCDF, Version 1.0**{: style="color: crimson"}](./ioos-netcdf-metadata-description-v1-0.html)

This document provides a description of the **deprecated**{: style="color: red"} IOOS NetCDF Metadata Profile.

