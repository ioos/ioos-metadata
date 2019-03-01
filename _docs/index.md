---
title: IOOS Metadata Profile
keywords: [ioos, metadata, netCDF]
tags: [ioos, metadata, netCDF]
toc: false
#permalink: index.html
summary: The IOOS Metadata Profile contains dataset attribution guidelines and examples to help the US IOOS community publish datasets in netCDF and other related data formats in an interoperable manner.  The goal of the metadata profile is to allow users of IOOS' data services, such as ERDDAP, THREDDS, OPeNDAP, and SOS, seamless access and use across individual IOOS data providers' services.
---

## **Overview**

The Profile defines recommended and required global and variable attributes for IOOS data providers to include when publishing their datasets and accompanying services.

Global and variable attributes are concepts of the [netCDF specification](https://www.unidata.ucar.edu/software/netcdf/docs/) which is 'a set of software libraries and self-describing, machine-independent data formats that support the creation, access, and sharing of array-oriented scientific data.'  

The IOOS DMAC data management system has adopted netCDF as a standard data format.  These guidelines are targeted towards netCDF files, however to the degree that they can be applied to other data formats they are referred to as a generalized 'Metadata Profile' rather than a netCDF-specific profile.  They are based on several community netCDF conventions, which each build off of each other in the following order:

- [Climate and Forecast Conventions (CF)](http://cfconventions.org/)
- [Attribute Convention for Data Discovery](http://wiki.esipfed.org/index.php?title=Attribute_Convention_for_Data_Discovery)
- [NOAA NCEI NetCDF Templates](https://www.nodc.noaa.gov/data/formats/netcdf)

Individual releases of the IOOS Metadata Profile (e.g. 1.0, 1.1, 1.2) target specific versions of each of these conventions.  See below for these specific version associations.

The initial versions ([1.0](./ioos-metadata-profile-v1-0.html) and [1.1](./ioos-metadata-profile-v1-1.html)) of the Metadata Profile were developed to provide a mapping between netCDF files and the [IOOS SOS Profile](https://ioos.github.io/sos-guidelines/).  The Metadata Profile defined the bare minimal set of attributes data providers could include in their netCDF data files to provide the THREDDS [ncSOS plugin](https://github.com/asascience-open/ncSOS) software a comprehensive cross-walk to generate all required service metadata for the IOOS SOS Profile.  While matching the IOOS SOS metadata, the Profile allows the lowest achievable divergence from the NCEI NetCDF Templates: it includes the Templates' attributes and augments them with a small number of IOOS-specific attributes, marked as convention type `IOOS` in the guidance tables.

Version [1.2](./ioos-metadata-description-v1-2.html) of the Metadata Profile targets [ERDDAP](https://coastwatch.pfeg.noaa.gov/erddap/index.html) as the future platform for IOOS' in situ ocean observation data services and the eventual replacement for SOS.  Thus, some non backwards-compatible divergence has been introduced, mostly changes from `required` to `recommended` of the IOOS-specific attributes necessary for translation to SOS in previous versions.  The affected `IOOS` attributes are listed here **______________________________________**.  Data providers wishing to maintain ncSOS/IOOS SOS compatibility can refer to this list and add all required IOOS attributes from deprecated Profile 1.1.


## Profile Versions:

### [**IOOS Metadata Profile, Version 1.2** (Current)](./ioos-metadata-profile-v1-2.html)

IOOS Metadata Profile Version 1.2 (released in 2019) is the current **valid**{: style="color: green"} profile, and is based upon the following community conventions:

- [Climate and Forecast Conventions (CF) 1.7](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html)
- [Attribute Convention for Data Discovery 1.3](http://wiki.esipfed.org/index.php/Attribute_Convention_for_Data_Discovery_1-3)
- [NOAA NCEI NetCDF Templates 2.0](https://www.nodc.noaa.gov/data/formats/netcdf/v2.0/)

IOOS data providers, including RAs and DACs are strongly encouraged to follow this profile in publishing datasets and services.

### [**IOOS Metadata Profile, Version 1.1**](./ioos-metadata-profile-v1-1.html)

IOOS Metadata Profile Version 1.1 (**deprecated in 2019**{: style="color: red"}) is based upon the following community conventions:

- [Climate and Forecast Conventions (CF) 1.6](http://cfconventions.org/cf-conventions/v1.6.0/cf-conventions.html)
- [Attribute Convention for Data Discovery 1.3](http://wiki.esipfed.org/index.php/Attribute_Convention_for_Data_Discovery_1-3)
- [NOAA NCEI NetCDF Templates 2.0](https://www.nodc.noaa.gov/data/formats/netcdf/v2.0/)

### [**IOOS Metadata Profile, Version 1.0**](./ioos-metadata-profile-v1-0.html)

IOOS Metadata Profile Version 1.0 (**deprecated in 2016**{: style="color: red"}) is based upon the following community conventions:

- [Climate and Forecast Conventions (CF) 1.6](http://cfconventions.org/cf-conventions/v1.6.0/cf-conventions.html)
- [Attribute Convention for Data Discovery 1.1](http://wiki.esipfed.org/index.php/Attribute_Convention_for_Data_Discovery_1-1)
- [NOAA NCEI NetCDF Templates 1.1](https://www.nodc.noaa.gov/data/formats/netcdf/v1.1/)
