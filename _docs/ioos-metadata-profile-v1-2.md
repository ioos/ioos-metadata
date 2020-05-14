---
title: "IOOS Metadata Profile Version 1.2"
keywords: [ioos, metadata, netCDF, 1.2]
tags: [ioos, metadata, netCDF, 1.2]
toc: false
#permalink: index.html
summary:  This is the currently active IOOS Metadata Profile version.  See links in the navbar to the left for previously deprecated versions.
---

## Revision History


| Version | Description | Date  |
|:--- |:--- |:--- |
| 1.0 | [Initial version based on the NODC Templates 1.1 and ACDD 1.1](./ioos-metadata-profile-v1-0.html) | 2016-10-01 |
| 1.1 | [Updated version based on the NCEI Templates 2.0 and ACDD 1.3](./ioos-metadata-profile-v1-1.html) | 2016-11-01 |
| **1.2** |**Currently Active Version** <br>Updated to reflect new IOOS attribution guidance and ERDDAP implementation: <br>* Add `infoUrl` and `Conventions`<br>* Make `creator_institution`, `creator_url`, `license`, `publisher_url`, and `summary` required <br>* Add `contributor_url`, `contributor_email`, and `contributor_role_vocabulary` (recommended)<br>* Make `contributor_name`, `contributor_role`, `institution`, and `publisher_name` recommended (previously were required)<br>* Clarify default vocabulary for `contributor_role` and `contributor_role_vocabulary`<br>* Clarify use of `contributor_name` and `contributor_role` for multiple contributors <br>* Restrict the profile to allow only a single Platform per dataset; clarify use of 'Platform' variable and related `platform` global and variable attributes <br> * Add global `platform_id`, `platform_name`, and `wmo_platform_code` <br>* Remove `platform_variable:ioos_code`, `platform_variable:short_name`, `platform_variable:long_name` and `platform_variable:type` <br>* Change `creator_zipcode` and `publisher_zipcode` to `creator_postalcode` and `publisher_postalcode` <br> * Add `geophysical_variable:standard_name_url` <br> * Add `gts_ingest` to indicate datasets and variables intended for NDBC/GTS harvest <br> * Add `ioos_ingest` to indicate datasets intended to be harvested into IOOS national products <br> * Add `instrument_variable:component` <br> * Add [Quality Control/QARTOD](#quality-controlqartod) section describing QARTOD flag variable requirements <br> * Add [Requirements for NDBC/GTS Ingest](#requirements-for-ioos-dataset-gts-ingest) section | **2020-01-10** |

## Notes/Caveats

1. The IOOS Metadata Profile is a compound profile that builds off of the [**NOAA NCEI NetCDF Templates v2.0**](https://www.nodc.noaa.gov/data/formats/netcdf/), meaning the full IOOS Metadata Profile is a combination of the NCEI Templates plus IOOS-specific guidance included in this document, such as:
* attributes that are IOOS-specific (i.e. additions to the NCEI Templates)
* attributes where variations exist between the IOOS guidance and the NCEI Templates (e.g. **`platform_vocabulary`**, where NCEI recommendations are specifically disallowed)
* attributes with a different role in the NCEI Templates; for example, the attribute **`_FillValue`** is **required** by the NCEI Template; however, in the IOOS Profile it is listed as **recommended** only;  conversely the opposite is possible as well
* attributes with otherwise modified or further qualified meanings/definitions

1. The NCEI Templates in turn build off of the ACDD and CF conventions.  Some attributes in the IOOS Profile originate from ACDD and CF (consult the `Convention` field in the table to determine the origin of each attribute).  Links to each are below:
* [NOAA NCEI NetCDF Templates 2.0](https://www.nodc.noaa.gov/data/formats/netcdf/v2.0/)
* [Attribute Convention for Data Discovery 1.3](http://wiki.esipfed.org/index.php/Attribute_Convention_for_Data_Discovery_1-3)
* [Climate and Forecast Conventions (CF) 1.7](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html)

1. In the IOOS Profile, attributes can be either **required** or **recommended**:
* all **required** attributes must have meaningful values assigned to them in accordance with the rules prescribed by the corresponding Convention or Template.
* each and all of the **recommended** attributes may be omitted; however, it is highly desirable that these attributes are included into the netCDF metadata ***AND*** have meaningful values assigned to them.
* consult the `Role` field value in the table to determine whether each attribute is required or recommended

1. The IOOS Profile is geared towards datasets containing in situ observations encoded in multidimensional, self-describing formats such as netCDF.  Some aspects of the profile are specific to the [CF Discrete Sampling Geometries](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html#discrete-sampling-geometries) guidance for these types of data, in particular the [Platform](#platform) section.  For datasets for which the DSG do not pertain (e.g. gridded model outputs or other gridded products), attributes in these sections can be omitted and still be compliant with the profile.  To avoid over-complicating the documentation, these Platform-related attributes are listed as '**required**' rather than '**required**, if applicable' because they are required for DSG-compliant datasets that must include a sampling platform.  

1. For in situ observation datasets, the IOOS Profile allows only one **'platform'** per dataset.  Please see the corresponding [Platform](#platform) section of the profile below for more information.

1. The [**U.S. IOOS National Glider Data Assembly Center**](https://gliders.ioos.us/index.html) currently uses a slightly different [netCDF File Format (V2)](https://ioos.github.io/ioosngdac/ngdac-netcdf-file-format-version-2); work is in progress to harmonize the NGDAC File Format and IOOS Metadata Profile.


## Gold Standard Example Datasets

IOOS provides a collection of "Gold Standard" example datasets in ERDDAP to demonstrate implementation of this Metadata Profile.  The Gold Standard datasets can be used as templates for data providers to generate their own compliant datasets in ERDDAP, and include a fully-deployable ERDDAP instance that includes both the example data and configuration files.  Consult the links below for more information:

* [IOOS Metadata Profile "Gold Standard" Example Datasets](gold-standard-examples.html)
* [IOOS "ERDDAP Gold Standard" GitHub Repository](https://github.com/ioos/erddap-gold-standard)

In addition to the Gold Standard datasets, there are some in-line examples included below that highlight specific attribute use cases that comply with the profile.



## IOOS Metadata Profile Attributes

### Dataset Description

The attributes listed below are a collection of high-level attributes recommended largely by the parent conventions of the IOOS Metadata Profile (CF, ACDD).  Their purpose is to describe the dataset in human-readable terms, define specific conventions used by other attributes (**`standard_name_vocabulary`**), or qualify other attributes (**`naming_authority`**).  A high-quality dataset will generally include meaningful values for all of these attributes, even though they are not all required according to the profile.

Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
Conventions| CF | A comma-separated list of the conventions that are followed by the dataset. For files that follow this version of the IOOS Metadata Profile, include the string "IOOS-1.2".<br><br>Example: {::nomarkdown}<ul><li><b><code>Conventions = "CF-1.6, ACDD-1.3, IOOS-1.2"</b></code></li></ul>{:/} | global | **required** |
featureType | CF | CF attribute for identifying the featureType.   <br><br>Example:{::nomarkdown}<ul><li><b><code>featureType = "timeSeries"</b></code></li></ul>{:/} | global | **required**
id | ACDD | An identifier for the data set, provided by and unique within its naming authority. The combination of the **`naming authority`** and the **`id`** should be globally unique, but the **`id`** can be globally unique by itself also. IDs can be URLs, URNs, DOIs, meaningful text strings, a local key, or any other unique string of characters. The **`id`** should not include blanks. | global | **required**
infoUrl  | IOOS | URL for background information about this dataset. This attributed is also required by ERDDAP. | global | **required**
keywords | ACDD | A comma separated list of key words and phrases. | global | recommended
license  | ACDD | Describe the restrictions to data access and distribution. | global | **required**
naming_authority  | ACDD | The organization that provides the **`id`** for the dataset. <br>The naming authority should be uniquely specified by this attribute; the combination of the **`naming_authority`** and the **`id`** should be a globally unique identifier for the dataset. A reverse-DNS naming is recommended; URIs are also acceptable. <br><br>Example:{::nomarkdown}<ul><li><b><code>naming_authority = "edu.ucar.unidata"</b></code></li></ul>{:/} | global | **required**
references  | ACDD/CF | Published or web-based references that describe the data or methods used to produce it. Recommend URIs (such as a URL or DOI) for papers or other references. Multiple references should be separated by commas. | global | recommended
standard_name_vocabulary  | ACDD | The name and version of the controlled vocabulary from which variable standard names are taken. Values for any variable's **`standard_name`** attribute must come from the CF Standard Names vocabulary for the dataset to comply with CF. <br><br>The format for the **`standard_name`** attribute must follow the ACDD recommendation ('CF Standard Name Table vXX', where 'XX' is a version of the standard name table), in order to be valid and meet the ACDD conventions.<br><br>If a variables does not have an existing standard name in the CF-managed list, the variable should not include a **`standard_name`** attribute. In these cases, a standard name can be proposed to the CF community for consideration.<br><br>  Example:<br>{::nomarkdown}<ul><li><b><code>standard_name_vocabulary = "CF Standard Name Table v72"</b></code></li></ul>{:/} | global | **required**
summary  | ACDD | One paragraph describing the data set. |  global | **required**
title  | ACDD | One sentence about the data contained within the file. | global | **required**

#### Example

Taken from the [Morro Bay BS1 MET Gold Standard Example dataset](https://standards.sensors.ioos.us/erddap/info/morro-bay-bs1-met/index.html).

```
NC_GLOBAL {
    Conventions               CF-1.6, ACDD-1.3, IOOS-1.2
    featureType               TimeSeries
    id                        morro-bay-bs1-met
    infoUrl                   https://data.cencoos.org/#metadata/57163/station
    license                   The data may be used and redistributed for free but is not intended for legal use, since it may contain inaccuracies.  Neither the data Contributor, ERD, NOAA, nor the United States Government, nor any of their employees or contractors, makes any warranty, express or implied, including warranties of merchantability and fitness for a particular purpose, or assumes any legal liability for the accuracy, completeness, or usefulness, of this information.
    naming_authority          edu.calpoly.marine
    standard_name_vocabulary  CF Standard Name Table v72
    summary                   Timeseries data from 'Morro Bay - BS1 MET' (morro-bay-bs1-met)
    title                     Morro Bay - BS1 MET
}
```

### Attribution

The attributes listed in the table below allow for consistent attribution of datasets within IOOS' national products.  Data providers are encouraged to follow these attribute guidelines exactly to ensure datasets appear with proper attribution.  

Consult the [Gold Standard Example Datasets](gold-standard-examples.html) for good examples to start from.

Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
contributor_email | IOOS | Email addresses of the individuals or institutions that contributed to the creation of this data. Multiple emails should be given in CSV format, and presented in the same order and number as the names in **`contributor_names`**. | global | recommended
contributor_name | ACDD | The name of any individuals or institutions that contributed to the creation of this data. Combined with the **`contributor_role`**, it provides the full description of the contributor. Multiple names should be given in CSV format. <br><br>Examples: {::nomarkdown}<ul><li><b><code>contributor_name = "Pacific Islands Ocean Observing System (PacIOOS)"</b></code></li> <li><b><code>contributor_name = "Great Lakes Observing System (GLOS),LimnoTech"</b></code></li></ul>{:/} | global | recommended
contributor_role | ACDD | The role of any individuals or institutions that contributed to the creation of this data. The CI_RoleCode vocabulary ([NERC](https://vocab.nerc.ac.uk/collection/G04/current/), [NOAA-NCEI](https://www.ngdc.noaa.gov/wiki/index.php?title=ISO_19115_and_19115-2_CodeList_Dictionaries#CI_RoleCode)) should be used. Multiple roles should be given in CSV format, and presented in the same order and number as the names in **`contributor_names`**.<br>For the IOOS ncSOS, **`contributor_role = "sponsor"`** defines a person, group, or organization’s full or partial support of an IOOS activity, asset, model, or product. <br><br>Examples:  {::nomarkdown}<ul><li><b><code>contributor_role = "sponsor"</b></code></li> <li><b><code>contributor_role = "sponsor, collaborator"</b></code></li></ul>{:/} | global | recommended
contributor_role_vocabulary | IOOS | The URL of the controlled vocabulary used for the **`contributor_role`** attribute. <br><br>The default is ["https://vocab.nerc.ac.uk/collection/G04/current/"](https://vocab.nerc.ac.uk/collection/G04/current/). | global | recommended
contributor_url | IOOS | The URL of the individuals or institutions that contributed to the creation of this data. Multiple URLs should be given in CSV format, and presented in the same order and number as the names in **`contributor_names`**. | global | recommended
creator_address | IOOS | Street address of the person or organization that collected the data.  | global | recommended
creator_city | IOOS | City of the person or organization that collected the data.  | global | recommended
creator_country | IOOS | Country of the person or organization that operates a platform or network, which collected the observation data. | global | **required**
creator_email  | ACDD | Email address of the person or institution that collected the data. | global | **required**
creator_institution  | ACDD | Institution that collected the data. This should be specified even if it matches the value of **`publisher_institution`**, **`institution`** or if **`creator_type`** is institution. | global | **required**
creator_name  | ACDD | Name of the person or organization that collected the data. <br><br>Follow the guidance described in the **`creator_type`** attribute for how to populate this field depending on whether a person, institution, group, or position. | global | recommended
creator_phone | IOOS | The phone number of the person or group that collected the data. <br><br>Example:{::nomarkdown}<ul><li><b><code>creator_phone = "(240) 533-9444"</b></code></li><li><b><code>creator_phone = "+1-240-533-9444"</b></code></li></ul>{:/} | global | recommended
creator_sector | IOOS | [IOOS classifier](https://mmisw.org/ont/ioos/sector) that best describes the platform (network) operator's societal sector. <br><br>Example:{::nomarkdown}<ul><li><b><code>creator_sector = "academic"</b></code></li></ul>{:/} | global |**required**
creator_state | IOOS | State of the person or organization that collected the data.  | global | recommended
creator_type | ACDD | Specifies type of creator with one of the following: 'person', 'group', 'institution', or 'position'. If this attribute is not specified, the creator is assumed to be a person.  | global | recommended
creator_url  | ACDD/IOOS | The URL of the *institution* that collected the data. Note that this should always reference an institution URL, and not a personal URL, even if **`creator_type=person`**.  | global | **required**
creator_postalcode | IOOS | The postal code of the person or organization that collected the data.  | global | recommended
institution  | ACDD | The institution of the person or group that collected the data. | global | recommended
publisher_address | IOOS | Street address of the person or organization that distributes the data.   | global | recommended
publisher_city | IOOS | City of the person or organization that distributes the data.   | global | recommended
publisher_country | IOOS | Country of the person or organization that distributes the data.   | global | **required**
publisher_email  | ACDD | The email address of the person or group that distributes the data files. | global | **required**
publisher_institution  | ACDD | Institution that distributes the data. This should be specified even if **`publisher_type`** is institution (in which case **`publisher_name`** would have an identical value). | global | **required**
publisher_name  | ACDD | Name of the person or group that distributes the data files. <br><br>Follow the guidance described in the **`publisher_type`** attribute for how to populate this field depending on whether a person, institution, group, or position. | global | recommended
publisher_phone | IOOS | The phone number of the person or group that distributes the data files. <br><br>Example:{::nomarkdown}<ul><li><b><code>creator_phone = "(240) 533-9444"</b></code></li><li><b><code>creator_phone = "+1-240-533-9444"</b></code></li></ul>{:/} | global | recommended
publisher_state | IOOS | State of the person or organization that distributes the data.   | global | recommended
publisher_type | ACDD | Specifies type of publisher with one of the following: 'person', 'group', 'institution', or 'position'. If this attribute is not specified, the publisher is assumed to be a person. | global | recommended
publisher_url  | ACDD/IOOS | URL of the person or group that distributes the data files. Note that this should always reference an institution URL, and not a personal URL, even if **`publisher_type=person`**.   | global | **required**
publisher_postalcode | IOOS | The postal code of the person or organization that distributes the data.   | global | recommended

#### Example

Taken from the [Morro Bay BS1 MET Gold Standard Example dataset](https://standards.sensors.ioos.us/erddap/info/morro-bay-bs1-met/index.html).

```
NC_GLOBAL {
    creator_country      USA
    creator_email        marineops at calpoly.edu
    creator_institution  California Polytechnic State University, Center for Coastal Marine Sciences
    creator_name         California Polytechnic State University, Center for Coastal Marine Sciences
    creator_sector       academic
    creator_type         institution
    creator_url          http://www.marine.calpoly.edu/
    institution          California Polytechnic State University, Center for Coastal Marine Sciences
}
```

```
NC_GLOBAL {
    contributor_email            cencoos_communications@mbari.org,feedback@axiomdatascience.com
    contributor_name             Central & Northern California Ocean Observing System (CeNCOOS),Axiom Data Science
    contributor_role             contributor,processor
    contributor_url              http://cencoos.org/,https://www.axiomdatascience.com
    contributor_role_vocabulary  http://vocab.nerc.ac.uk/collection/G04/current/
}
```

```
NC_GLOBAL {
    publisher_country      USA
    publisher_email        marineops at calpoly.edu
    publisher_institution  California Polytechnic State University, Center for Coastal Marine Sciences
    publisher_name         California Polytechnic State University, Center for Coastal Marine Sciences
    publisher_type         institution
    publisher_url          http://www.marine.calpoly.edu/
}
```

### Variables

A collection of variable attributes that should be applied to all geophysical or other measured parameter variable contained in the dataset.  These mostly include illustrations of CF convention attributes, with the addition of IOOS' **`standard_name_url`**.  

**Note:** the table below uses **`geophysical_variable`** as an alias intending to represent any variable containing geophysical data.

Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
geophysical_variable:_FillValue<br>geospatial_variable:_FillValue | CF | This value is considered to be a special value that indicates undefined or missing data, and is returned when reading values that were not written. The type of this variable should match the type of the unpacked variable data. {::nomarkdown}<ul><b><code>  <li>time:_FillValue = -999999.0f    <li>lat:_FillValue = -999999.0f    <li>lon:_FillValue = -999999.0f    <li>z:_FillValue = -999999.0f    <li>sea_water_temperature:_FillValue = Float.NaN</li></b></code></ul>{:/} | variable | recommended
geophysical_variable:missing_value<br>geospatial_variable:missing_value | CF | This should always be equal to the `_FillValue` attribute and both are used for legacy library support. {::nomarkdown}<ul><b><code> <li>time:missing_value = -999999.0f    <li>lat:missing_value = -999999.0f    <li>lon:missing_value =-999999.0f    <li>z:missing_value = -999999.0f <li>sea_water_temperature:missing_value = Float.NaN</li></b></code></ul>{:/} | variable | recommended
geophysical_variable:standard_name | CF | Standardized field which uses the [CF Standard Names](http://www.cfconventions.org/documents.html). If a variables does not have an existing standard_name in the CF-managed list, this attribute should not be used. In these cases, a standard name can be proposed to the CF community for consideration and acceptance. | variable | **required**
geophysical_variable:standard_name_url | IOOS | The URL of a **`standard_name`** in the online vocabulary listed in the global **`standard_name_vocabulary`** attribute.<br><br>Example: {::nomarkdown}<ul> <li> <b><code>sea_water_temperature:standard_name_url = "https://vocab.nerc.ac.uk/collection/P07/current/CFSN0335/"</code></b> </li>  <li> <b><code>sea_water_temperature:standard_name = "sea_water_temperature"</code></b> </li> </ul>{:/} | variable | recommended
geophysical_variable:units  | CF | Required for most all variables that represent dimensional quantities. The value for a geophysical variable's **`units`** attribute should match or be derived from the canonical units specified for the variable's **`standard_name`** in the CF Standard Name table. <br><br>CF units are specified by the  [**`udunits`**](https://www.unidata.ucar.edu/software/udunits/) package, which includes a file `udunits.dat` listing the valid individual unit names (e.g., "g" and "m") from which which composite **`units`** strings can be formed (e.g., "kg m-3"). <br><br>For example, all temperature standard names have canonical units of "K", but often geophysical variables that measure temperature are specified with **`units`** of `degree_Celsius` or some variant thereof. | variable | **required**

#### Example

Taken from the [Morro Bay BS1 MET Gold Standard Example dataset](https://standards.sensors.ioos.us/erddap/info/morro-bay-bs1-met/index.html).

```
Attributes {
    air_temperature {
        _FillValue        -9999.0
        missing_value     -9999.0
        long_name         Air Temperature
        platform          station
        standard_name     air_temperature
        units             degree_Celsius
        standard_name_url http://vocab.nerc.ac.uk/collection/P07/current/CFSN0023/
    }
}
```


### Platform

The method for specifying platform metadata for in situ measurements has historically been a source of confusion. CF Discrete Sampling Geometries (DSG) guidelines represent observing platforms as 'featureTypes' (e.g. 'timeSeries', 'profile', 'trajectory'), and allow multiple platforms to be included in a single file by way of a coordinate variable that uniquely identifies each feature by ID.  For example, each buoy in a timeSeries feature dataset with multiple buoys can be differentiated by storing its identifier in this coordinate variable (referred to as the 'station' dimension in this case).

More information about CF DSG and associated requirements is available in [CF Documentation - Chapter 9](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html#discrete-sampling-geometries).
<br><br>

**Guidelines for Platforms in Datasets**:   

**One platform per dataset:** The IOOS Metadata Profile restricts datasets to contain only a **single physical observing platform per dataset** (e.g. buoy, glider, station, or anything that might be assigned a WMO ID).  This simplifies the dataset structure significantly, and it allows the use of several global attributes to specify platform metadata that might otherwise be found in platform container variable(s) (e.g. **`platform_id`** and **`platform_name`**, as well as the OceanSITES-derived **`wmo_platform_code`**).  It also simplifies the creation of aggregated datasets at the ERDDAP level to create groups of individual platform datasets.

Notes:

Data providers are encouraged to carefully review this section and upstream standards, and especially to review the [Gold Standard](#gold-standard-example-datasets) example datasets to ensure compliance with platform guidance in this profile.

Aggregated ERDDAP datasets: ERDDAP provides the ability to create aggregated datasets from collections of individual datasets.  While this is encouraged as a way to streamline access for end users to related datasets, IOOS will not harvest aggregated datasets into upstream national products, nor will NDBC harvest them for GTS publication.  Therefore, you should set **`gts_ingest=false`** and **`ioos_ingest=false`** flags on any ERDDAP aggregated datasets.

Gridded Datasets: As mentioned in the [Notes/Caveats section](#notescaveats), the Platform rules do not apply to datasets that do not adhere to the CF Discrete Sampling Geometries guidelines (e.g. gridded model outputs or other gridded products).  Attributes in this section can be omitted for such datasets and still be compliant with this profile.  
<br>

**DSG FeatureType Guidance:**

Recommendations on the specific CF DSG featureTypes to use for different platform instrumentation scenarios is as follows:


Platform Type | CF DSG Dataset Type
:--------- | :-------- |
Buoy/Station with:{::nomarkdown}<ul><li>single sensor package <i><b>or</b></i></li><li>multiple sensor packages with identical vertical (height/depth) position and same sampling frequency</li></ul>{:/} | TimeSeries - single station
Buoy/Station with:{::nomarkdown}<ul><li>multiple sensor packages with different vertical (height/depth) positions <i><b>or</b></i></li><li>multiple sensor packages with different sampling frequencies</li></ul>{:/} | TimeSeries - multiple station _**or**_ <br> TimeSeriesProfile - single station _**or**_ <br> ‘single-sensor-per-dataset’
Profiling Glider | TrajectoryProfile

**TimeSeries - single station:** A [DSG TimeSeries feature](http://cfconventions.org/cf-conventions/cf-conventions.html#time-series-data) represents measurements taken at a single location (lat, lon, altitude) over time.  This can be distinguished from TimeSeries - multiple station by having a 'station dimension' of only 1, indicating only a single feature, or station, per dataset.  

**TimeSeries - multiple station:** A [DSG TimeSeries featureType](http://cfconventions.org/cf-conventions/cf-conventions.html#time-series-data) dataset with a 'station dimension' of greater than 1.  TimeSeries - multiple station represents a platform with sensors at different heights as a vertical collection of features where the altitude (depth or height) of each feature reflects the vertical position of each sensor on the platform.   Lat/Lon positions must be the same for each feature.

**TimeSeriesProfile - single station:** A [DSG TimeSeriesProfile feature](http://cfconventions.org/cf-conventions/cf-conventions.html#time-series-profiles) represents a platform with multiple sensors as a vertical profile with a altitude (depth or height) position for each sensor.  This can also be used for profiling sensors like ADCPs.  This metadata profile restricts TimeSeriesProfile datasets to include a 'station dimension' of only 1, indicating a single timeSeries feature (or 'station') per dataset.

**single-sensor-per-dataset:** individual ERDDAP datasets of either TimeSeries or TimeSeriesProfile type that are associated via matching **`platform_id`** and **`wmo_platform_code`** global attributes, breaking a platform's data apart into individual DSG datasets.  Some IOOS RAs use this pattern already, and provide one dataset for sensor package (e.g., CTD, ADCP, met, etc).  The code used to ingest sensor datasets for GTS by NDBC or for Sensor Map by IOOS will perform this aggregation, so data providers need not create aggregations in ERDDAP.  Each individual dataset intended for the GTS must follow the [Requirements for GTS Ingest](#requirements-for-ioos-dataset-gts-ingest) individually.

Note that because neither **`platform_id`** or **`wmo_platform_code`** attributes are required in this profile, any dataset without them will be considered to be specifying data for only one, distinct platform, and aggregation with other datasets by downstream processes at NDBC or IOOS is not guaranteed.   

**TrajectoryProfile:** [A DSG TrajectoryProfile feature](http://cfconventions.org/cf-conventions/cf-conventions.html#trajectory-profiles) represents a series of individual profiles taken along a path across the Earth's surface.  Similar to 'TimeSeriesProfile - single station' this metadata profile restricts TrajectoryProfile to include a 'trajectory dimension' of only 1, indicating a single trajectory feature (glider, ship, or other platform) per dataset.
<br><br>

**Platform Attribution:**

Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
platform | ACDD |  **Global** attribute specifying the name of the *type* of platform(s) that supported the sensor data used to create this data set or product. Platforms can be of any type, including satellite, ship, station, aircraft or other. The controlled vocabulary must be indicated in the **`platform_vocabulary`** field.<br><br>**`platform`** should be a single string with no blank spaces.<br><br>Example: {::nomarkdown}<ul> <li> <b><code>platform = "buoy";</code></b> <li><b><code>platform_vocabulary = "https://mmisw.org/ont/ioos/platform";</code></b> </ul>{:/}<br>The value of the **`platform`** global attribute is used in generating the [IOOS Asset Identifier]([https://ioos.github.io/conventions-for-observing-asset-identifiers/ioos-assets-v1-0.html]) for the dataset.  Consult the [Rules for Asset Identifier Generation](#rules-for-ioos-asset-identifier-generation) section below this table for details on how this formula works. | global | **required**
platform | NCEI | **Variable** level attribute to be specified on each **`geophysical_variable`** (i.e. data variable) with the value indicating the name of a container variable containing platform identifiers. <br><br>Because the IOOS Metadata Profile restricts datasets to a **single platform per dataset**, each dataset must only contain one platform container variable (usually named **`station`** or **`platform`**), and each data variable in the dataset must include a **`platform`** attribute with the name of this variable.  See **`platform_variable:cf_role`** for more information.<br><br>Example: {::nomarkdown}<ul> <li> <b><code>sea_water_temperature:platform = "station"</code></b></li><li><b><code>station:cf_role = "profile_id"</code></b></li> </ul>{:/} | variable | **required**
platform_variable:cf_role | CF | Indicates the values of this variable contain identifiers for the CF DSG [featureType](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html#_features_and_feature_types) features in the dataset. Allowed values are defined in [Chapter 9.5](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html#coordinates-metadata) CF guidelines and consist of: `timeseries_id`, `profile_id`, and `trajectory_id`, depending on the featureType represented in the dataset, as specified by the **`featureType`** global attribute. <br><br>Example: {::nomarkdown}<ul><li><b><code>cf_role = "timeseries_id"</code></b></li></ul>{:/}| variable | **required**
platform_id | IOOS | An optional, short identifier for the platform, if the data provider prefers to define an id that differs from the dataset identifier, as specified by the  **`id`** attribute.<br><br>**`platform_id`** should be a single alphanumeric string with no blank spaces.<br><br>  When **`platform_id`** is defined for a dataset, it is used in place of the **`id`** field in generating the IOOS Asset Identifier (consult the [Rules for Asset Identifier Generation](#rules-for-ioos-asset-identifier-generation) section below).<br><br>Examples: {::nomarkdown}<ul> <li> <b><code>platform_id = "carquinez"</code></b> <li><b><code>platform_id = "cb0102"</code></b> </ul>{:/} | global | recommended
platform_name | IOOS | A descriptive, long name for the platform used in collecting the data.  <br><br>The value of **`platform_name`** will be used to label the platform in downstream applications, such as IOOS' National Products (Environmental Sensor Map, EDS, etc) <br><br>Examples: {::nomarkdown}<ul> <li> <b><code>platform_name = "Morro Bay - BS1 MET"</code></b> <li><b><code>platform_name = "Chesapeake Bay Buoy 102"</code></b> </ul>{:/} | global | **required**
platform_vocabulary | ACDD | Controlled vocabulary for the names used in the **`platform`** attribute.<br><br> The recommended value for the **`platform_vocabulary`** attribute is a URL to either the [IOOS Platform Category vocabulary](https://mmisw.org/ont/ioos/platform), or [NERC SeaVoX Platform Categories vocabulary](https://vocab.nerc.ac.uk/collection/L06/current/). <br><br>Example:{::nomarkdown}<ul> <li> <b><code> platform_vocabulary = "https://mmisw.org/ont/ioos/platform"</code></b> </ul>{:/}<br>The IOOS Metadata Profile diverges from the NCEI Templates 2.0 in that the use of the "NASA GCMD Platform Keywords 8.1" as a **`platform_vocabulary`** is not allowed.  The reason for this is that the **`platform`** global attribute is used in generating the [IOOS Asset Identifier 1.0](https://ioos.github.io/conventions-for-observing-asset-identifiers/ioos-assets-v1-0.html) for the dataset, and thus requires a single string platform name with no blank characters.  GCMD Platform Keywords do not follow this pattern and therefore are disallowed.  See the [Rules for Asset Identifier Generation](#rules-for-ioos-asset-identifier-generation) for more info. | global | **required**
wmo_platform_code | IOOS | The WMO identifier for the platform used to measure the data.  This identifier can be any of the following types:<br>{::nomarkdown}<ul> <li>WMO ID for buoys (numeric, 5 digits)</li><li>WMO ID for gliders (numeric, 7 digits)</li><li>NWS ID (alphanumeric, 5 digits)</ul>{:/} When a dataset is assigned a **`wmo_platform_code`** it is thereby assigned a secondary Asset Identifier for the **'wmo' `naming_authority`**.  See the  [Rules for Asset Identifier Generation](#rules-for-ioos-asset-identifier-generation) for more information.  <br><br>Example: {::nomarkdown}<ul> <li> <b><code>wmo_platform_code = "44011"</code></b> </ul>{:/} | global | **required**, if applicable



### Quality Control/QARTOD

Guidance for implementing [QARTOD](https://ioos.noaa.gov/project/qartod/) quality control flag variables in a standardized fashion.  QARTOD flag variables are associated with data variables using the CF "Ancillary Variables" approach.  More information on this is available in [CF Chapter 3.4](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html#ancillary-data).  

This profile requires that all variables containing results from QARTOD tests be referenced by ancillary variables, and those variables use a valid CF Standard Name to reflect the test performed (see **`qartod_variable:standard_name`** in the table below for a list of suitable standard names).

**Notes:**
* See the [Requirements for GTS Ingest](#requirements-for-ioos-dataset-gts-ingest) section below for important guidelines to properly specify a dataset's QARTOD "Aggregate/Rollup" flag variable for GTS ingest by NDBC.
*  The table below uses **`geophysical_variable`** as an alias intending to represent any variable containing geophysical data, and **`qartod_variable`** as an alias for an ancillary QC flag variable.

Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
geophysical_variable:ancillary_variables | CF | From [CF Chapter 3.4](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html#ancillary-data):{::nomarkdown}<ul> <li>"When one data variable provides metadata about the individual values of another data variable it may be desirable to express this association by providing a link between the variables. For example, instrument data may have associated measures of uncertainty. The attribute <code><b>ancillary_variables</b></code> is used to express these types of relationships. It is a string attribute whose value is a blank separated list of variable names. The nature of the relationship between variables associated via ancillary_variables must be determined by other attributes." </li></ul>{:/}For purposes of the IOOS Metadata Profile, the **`ancillary_variables`** attribute associates the data variable with one or many QARTOD flag variables containing test results. Multiple QARTOD ancillary variables should be represented as a space-separated list of individual test variable names (for cases where data provider includes multiple test results, or includes the QARTOD "Aggregate/Rollup" flag in addition to individual flags, as required by this profile). | variable | **required**, if applicable
qartod_variable:standard_name | CF | The full set of CF Standard Names available to identify QARTOD flag ancillary variables can be found in [Standard Name Table v72](http://cfconventions.org/Data/cf-standard-names/72/build/cf-standard-name-table.html) (March 2020) and includes: {::nomarkdown}<ul><li><code><b>aggregate_quality_flag</b></code>: an Aggregate/Rollup flag combining multiple individual flags</li><li><code><b>attenuated_signal_test_quality_flag</b></code>: Attenuated Signal Test flag</li><li><code><b>climatology_test_quality_flag</b></code>: Climatology Test flag</li><li><code><b>flat_line_test_quality_flag</b></code>: Flat Line Test flag</li><li><code><b>gap_test_quality_flag</b></code>: Timing/Gap Test flag</li><li><code><b>gross_range_test_quality_flag</b></code>: Gross Range Test flag</li><li><code><b>location_test_quality_flag</b></code>: Location Test flag</li><li><code><b>multi_variate_test_quality_flag</b></code>: Multi-variate Test flag</li><li><code><b>neighbor_test_quality_flag</b></code>: Neighbor Test flag </li><li><code><b>rate_of_change_test_quality_flag</b></code>: Rate of Change Test flag</li><li><code><b>spike_test_quality_flag</b></code>: Spike Test flag</li><li><code><b>syntax_test_quality_flag</b></code>:  Syntax Test flag</li></ul>{:/} | variable | **required**, if applicable
qartod_variable:flag_values | CF | The **`flag_values`** and **`flag_meanings`** attributes describe a status flag consisting of mutually exclusive coded values. The **`flag_values`** attribute is the same type as the variable to which it is attached, and contains a list of the possible flag values.  See the below example for recommended usage of **`flag_values`** for QARTOD flagging.  | variable | recommended
qartod_variable:flag_meanings | CF | The **`flag_meanings`** attribute is a string whose value is a blank separated list of descriptive words or phrases, one for each flag value.  If multi-word phrases are used to describe the flag values, then the words within a phrase should be connected with underscores. See the below example for recommended usage of **`flag_meanings`** for QARTOD flagging. | variable | recommended
qartod_variable:references | CF | This should be a URL to a resource that describes the test configuration, parameters used, etc, if such a resource is available. The global `references` attribute can also be used to describe QC methods in general. | variable | recommended

#### Example

Adapted from: [Morro Bay BS1 MET Gold-Standard Example dataset](https://standards.sensors.ioos.us/erddap/info/morro-bay-bs1-met/index.html).

```
  air_temperature {
    String standard_name "air_temperature";
    String long_name "Air Temperature";
    String units "degree_Celsius";
    String ancillary_variables "air_temperature_qc_agg air_temperature_gross_range air_temperature_flat_line";
  }
  air_temperature_qc_agg {
    String standard_name "aggregate_quality_flag";
    String long_name "Air Temperature QARTOD Aggregate Quality Flag";
    String flag_values 1, 2, 3, 4, 9;
    String flag_meanings "PASS NOT_EVALUATED SUSPECT FAIL MISSING";
    String references "http://services.cormp.org/quality.php";
    Int32 _FillValue 2;
  }
  air_temperature_gross_range {
    String standard_name "gross_range_test_quality_flag";
    String long_name "Air Temperature QARTOD Gross Range Test Quality Flag";
    String flag_values 1, 2, 3, 4, 9;
    String flag_meanings "PASS NOT_EVALUATED SUSPECT FAIL MISSING";
    String references "http://services.cormp.org/quality.php";
    Int32 _FillValue 2;
  }
  air_temperature_flat_line {
    String standard_name "flat_line_test_quality_flag";
    String long_name "Air Temperature QARTOD Flat Line Test Quality Flag";
    String flag_values 1, 2, 3, 4, 9;
    String flag_meanings "PASS NOT_EVALUATED SUSPECT FAIL MISSING";
    String references "http://services.cormp.org/quality.php";
    Int32 _FillValue 2;
  }
```

### NDBC/GTS Ingest

A collection of variables that relate to requirements for IOOS datasets to be harvested by NDBC for ingestion and for delivery to the GTS. A description of the specifics of the NDBC/GTS ingest process used by IOOS is available in the [Requirements for GTS Ingest](#requirements-for-ioos-dataset-gts-ingest) section below.  


Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
gts_ingest | IOOS |  **Global** attribute that indicates the data provider intends this dataset to be harvested by NDBC and published on the GTS.<br><br>In order for NDBC to harvest the dataset, this attribute must have a value of **`true`**. | global | **required**, if applicable
gts_ingest | IOOS |  **Variable** attribute, used in concert with the global equivalent, that indicates a variable's data should be harvested by NDBC and published to the GTS.<br><br>In order for NDBC to harvest the variable's data, both the global **`gts_ingest`** attribute and this variable attribute must have a value of **`true`** (in addition to further requirements). <br><br>Refer to the  [GTS requirements](#requirements-for-ioos-dataset-gts-ingest) section below for more detail on these requirements and on the handling of these variables. | variable | **required**, if applicable

#### Example

Taken from [PacIOOS's AWS-HIMB ERDDAP Dataset](https://pae-paha.pacioos.hawaii.edu/erddap/info/AWS-HIMB/index.html).

```
NC_GLOBAL {
    gts_ingest "true";
}

air_temperature {
    String gts_ingest "true";
}

sea_water_temperature {
    String gts_ingest "true";
}

air_temperature_raw {
    String gts_ingest "false";
}

sea_water_temperature_raw {
    String gts_ingest "false";
}
```

### IOOS Ingest

The **`ioos_ingest`** flag is intended to flag datasets that, in the rare case, should **not** be harvested by IOOS national products (such as the IOOS Catalog and Sensor Map).  This allows data providers and ERDDAP operators the ability to exclude datasets that aren't  allowed for these public products on an individual basis.  For example, an IOOS RA might host data owned by a private industry group who places sharing restrictions on their datasets.  Note: RAs who are Certified RICEs must adhere to the NOAA data sharing policy and strive to make data publicly available, regardless of funding relationships with data providers. Therefore, this flag should be used for rare exceptions to this rule.  


Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
ioos_ingest | IOOS |  **Global** attribute that indicates the data provider intends this dataset to be harvested by IOOS national products.<br><br>To exclude a dataset from harvest by IOOS, this attribute must have a value of **`false`**. The default assumption is that all datasets are intended to be harvested. | global | recommended


#### Example

*Coming soon...*


### Instrument

The IOOS Metadata Profile generally follows the NCEI Templates guidance on usage of the **`instrument`** and **`'instrument_variable'`** variables.  IOOS adds two optional attribute variables to any **'instrument_variables'** defined in a dataset to allow compliance with the IOOS Asset Identifier scheme.<br><br>

Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
instrument | NCEI | The IOOS Metadata Profile follows closely the NCEI Templates in specifying instruments used in data collection.  The NCEI Templates dictate that the **`instrument`** attribute can be used in two different ways:<br><br> 1) as a global variable containing a vocabulary-constrained string describing the instrument type or<br><br> 2) as a variable attribute **`:instrument`** that references a global **`'instrument_variable'`** by name that contains additional metadata, if needed.  Consult the NCEI Template documentation for more details.<br><br>  Additionally, the IOOS Metadata Profile defines specific attributes of the **`'instrument_variable'`** that play a role in further qualifying the resulting Asset Identifier for measured variables (if included).  These are described in the following rows. | global | recommended
instrument_variable:component | IOOS | The value of a **`component`** applies to the like-named field in the IOOS SOS Asset Identifier URN; it is used to identify individual, distinct components, or sub-assets (for example, two different sensor types), on a single platform. The **`:component`** is mapped to the Asset Identifier as follows:<br><br> Asset Identifier = <code>urn:ioos:asset_type:authority:label<b>[:component]</b>[:discriminant][#functional_parameters]</code><br><br>See examples below.| variable | recommended, if applicable
instrument_variable:discriminant | IOOS | The value of a **`discriminant`** applies to the like-named field in the IOOS SOS Asset Identifier URN; it ensures that in case of multiple deployments of identical sensors on the same platform (for example, measuring the same **`observedProperty`**), each sensor has a unique ID in the Identifier.  The **`:discriminant`** is mapped to the Asset Identifier as follows:<br><br> Asset Identifier = <code>urn:ioos:asset_type:authority:label[:component]<b>[:discriminant]</b>[#functional_parameters]</code> <br><br>See examples below. | variable | recommended, if applicable

#### Example

Usage of **`component`** with an **`instrument_variable`**:
```
Attributes {
    sea_water_temperature {
      instrument      temperature_sensor
    }
    temperature_sensor {
      component      nortek_adp_514
    }

}
```

Usage of **`discriminant`** with an **`instrument_variable`**:
```
Attributes {
    sea_water_temperature_top {
      instrument      temperature_sensor_top
    }
    sea_water_temperature_bottom {
      instrument      temperature_sensor_bottom
    }
    temperature_sensor_top {
      component      nortek_adp_514
      discriminant   top
    }
    temperature_sensor_bottom {
      component      nortek_adp_514
      discriminant   bottom
    }

}
```
<br><br>

## Requirements for IOOS Dataset NDBC/GTS Ingest

In partnership with IOOS, NOAA [NDBC](https://www.ndbc.noaa.gov/) ingests nonfederal IOOS partner data and delivers a subset of those variables (mainly meteorological and physical oceanographic) through the NWS system and on to the WMO [Global Telecommunication System (GTS)](http://www.wmo.int/pages/prog/www/TEM/GTS/index_en.html).  NDBC also publishes all the data they harvest to their web products. 
| Variables that NDBC accepts | Variables that NDBC delivers to the GTS |
|:--- |:--- |
| Winds (direction, speed, gust) | x (except gust) |
| Air temperature | x | 
| Dew point | x |
| Barometric pressure (sea level) | x |
| Relative humidity |   |
| Shortwave and longwave radiation |   |
| Waves: Directional and non-directional, spectra | x |
| Water temperature (surface, subsurface - 30 depths) | x |
| Salinity (surface, subsurface) | x |
| Current speed/direction (70 depths/bins) | x |
| Water level |   | 
| Dissolved oxygen (surface, bottom) |   | 
| Turbidity |   | 
| Chlorophyll |   | 
| pH |   |
| Eh |   |


NDBC will leverage IOOS RA ERDDAP servers as the central access points for nonfederal IOOS partner data.  This is a departure from the previous data delivery method, where providers and RAs packaged XML files and posted them to an NDBC FTP server. It is critical that RAs work with their regional data providers to ensure their data are available in the RA ERDDAPs, so that NDBC can continue to access those datasets. 
![Data flow](/_docs/images/NDBC-data-flow.png)   

In order to allow NDBC to query and filter the correct subset of datasets in an ERDDAP server and process them consistently and predictably, **data providers must ensure the following dataset attribution requirements are met**.  

Refer to the [Platform](#platform), [GTS Ingest](#gts-ingest), and [Quality Control/QARTOD](#quality-controlqartod) tables above for detailed descriptions of the attributes shown below.

#### For NDBC to pull data for a dataset to the GTS:

1. The dataset should be in ERDDAP
1. The dataset should meet the Single Platform requirement described in the [Platform](#platform) section
1. The dataset should meet requirements for defining the vertical coordinate variable set forth in the [Requirements for Vertical Coordinate Variable](#requirements-for-vertical-coordinate-variable) section
1. The dataset should have a global attribute called **`wmo_platform_code`**, with the numeric WMO ID or alphanumeric NWS ID as the value (see **`wmo_platform_code`** in the [Platform](#platform) section for details on specific ID requirements)
1. The dataset should have a global attribute called **`gts_ingest`** with a value of **`true`**
1. Any variables the RA wants to push to NDBC should have an attribute called **`gts_ingest`** with value of **`true`**
1. The variable should have a **`standard_name`** attribute with a value that's a valid CF Standard Name
1. The variable should include an ancillary variable representing the QARTOD aggregate flag as defined in the [Requirements for the QARTOD Aggregate/Rollup Flag](#requirements-for-the-qartod-aggregaterollup-flag) section
1. The variable should have a **`units`** attribute, with a value that's a valid unit (that is, the units are convertible to the CF canonical unit using the [**`udunits`**](https://www.unidata.ucar.edu/software/udunits/) library) <br><br>

**Note:** it is not a requirement for a variable's QC flag ancillary variables to include a **`gts_ingest`** flag.

#### Requirements for Vertical Coordinate Variable:

In order for NDBC to be able to uniformly identify and interpret the vertical coordinate variable in IOOS datasets to ensure consistent processing, a specific implementation of the CF guidelines for vertical coordinate variables is necessary.  This profile requires the vertical coordinate variable to include the following attributes:

Name | Accepted Values
:--------- | :------- |
axis | 'Z' |
positive | 'up', down' |
units | One of: [meter, meters, inch, foot, yard, mile, miles, US_survey_foot, US_survey_feet, <br> fathom, fathoms, international_inch, international_inches, international_foot, <br> international_feet, international_yard, international_yards, international_mile, <br> international_miles, inches, in, feet, ft, yd, mi] |

**Note:** The vertical position of an individual observation must always be encoded using the vertical coordinate variable (as specified in the CF DSG guidelines) and _cannot_ be included as an attribute on a data variable.

#### Requirements for the QARTOD Aggregate/Rollup Flag:

Currently, IOOS RAs push a custom XML format to NDBC for GTS ingestion, so they can exclude "QC fail" values while generating the XML. ERDDAP datasets will have all observed data, including observations marked "QC fail", so NDBC needs a means to filter QC passing and failing data from the full timeseries.  This will be accomplished using an "ancillary variable" according to the CF [Ancillary Data](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html#ancillary-data) guidelines that represents the QC aggregate/rollup flag for each observation variable marked for GTS ingestion, as described below.  

**Rules governing the 'Aggregate/Rollup' flag variable:**

1. The value of the variable is the UNESCO/QARTOD v2 convention:
    * 9 = Missing
    * 2 = Not Eval
    * 1 = Pass
    * 3 = Suspect
    * 4 = Fail
1. The value of the rollup flag should be the *worst* result out of all of the individual tests. It's called a "Summary Flag" in the [QARTOD Data Flags](https://github.com/ioos/ioos_qc/blob/master/ioos_qc/qartod.py#L46-L77) manual (pg 3).
    * Here's how it's done in the [ioos_qc library](https://github.com/ioos/ioos_qc/blob/3d8efba12644eb37b9ef35e6cdcf35189e789075/ioos_qc/qartod.py#L49-L80) with the [corresponding test](https://github.com/ioos/ioos_qc/blob/3d8efba12644eb37b9ef35e6cdcf35189e789075/tests/test_qartod.py#L1096-L1113).  
1. The variable should have a standard name attribute of **`aggregate_quality_flag`**. See the [QARTOD](#quality-controlqartod) section above for more information.  
1. NDBC should exclude any values that are QC fail (and missing) but include everything else (not eval, pass, suspect) <br> <br>


Notes on GTS ingest and QC flagging:

* Although having **`gts_ingest`** on both the dataset itself and each of its variables is redundant, it allows for more efficient querying across a large ERDDAP server
* Some of the data that NDBC pulls never makes it to the GTS, but it still used in other NDBC products
* If you set **`gts_ingest`** on a variable the NDBC doesn't care about, NDBC will just ignore it.
* RAs may publish ancillary variables with results of individual QC tests, however NDBC will only examine contents of the **`aggregate_quality_flag`** variable for filtering purposes for GTS harvest.  The CF Standard Names table includes several names appropriate for individual QC tests - consult the [QARTOD](#quality-controlqartod) section for the current list.


#### Examples

The [WQB-04](https://pae-paha.pacioos.hawaii.edu/erddap/info/WQB-04/index.html) and [WQB-05](https://pae-paha.pacioos.hawaii.edu/erddap/info/WQB-05/index.html) PacIOOS buoys are actively used by NDBC for collecting data.

<br/>

## Rules for IOOS Asset Identifier Generation

For reference, the [IOOS Asset Identifier 1.0](https://ioos.github.io/conventions-for-observing-asset-identifiers/ioos-assets-v1-0.html) is composed of the following components:

Asset Identifier = **`urn:ioos:asset_type:authority:label[:component][:discriminant][#functional_parameters]``**

The IOOS Asset Identifier can be constructed by combining the Metadata Profile attributes according to their definitions to match the above pattern.<br><br>

**Rules for generating the Asset Identifier from IOOS Metadata Profile attribution:**

If **`platform_id`** present:

Asset Identifier = **`'urn:ioos:' + platform + ':' + naming_authority + ':' + platform_id`**<br><br>

If **`platform_id`** not present:

Asset Identifier = **`'urn:ioos:' + platform + ':' + naming_authority + ':' + id`**<br><br>

For datasets with a **`wmo_platform_code`** global attribute, a second Asset Identifier is also assumed, according to the following rules:

WMO Asset Identifier = **`'urn:ioos:' + platform + ':wmo:' + wmo_platform_code`**

This means it is possible for a single dataset to have two valid IOOS Asset Identifiers.  It is also possible to define as many custom global 'id' attributes as necessary.  For example, RAs may define their own identification scheme outside those described here, or, if there is another organization (such as NCEI) for which an id is appropriate, it may be included as well (e.g. **`ncei_id = 123456789`** or  **`ncei_accession = 123456789`**).  While these won't technically be considered to be IOOS Asset Identifiers, there is still the opportunity to identify datasets using community-agreed-upon global identifier attributes.<br><br>

**Additional considerations regarding IOOS Asset Identifiers:**

* At the moment, the specification constrains the valid **`asset_type`**s to be: glider, station, network, sensor, and survey.  For the purposes of the IOOS Metadata Profile, the values of **`platform'** can be more broad, however the resulting Asset Identifiers may not be valid according to that specification.

* If an **`instrument_variable`** is defined for the dataset, it becomes possible for each data variable associated with it (via the **`:instrument`** variable attribute) to have its own Asset Identifier that is more fully qualified than the global-variable-defined dataset Asset Identifier described above.  See the [documentation](#instrument) for **`instrument_variable:component`** and **`instrument_variable:discriminant`** for details.

IOOS Asset Identifier rules for a dataset with variables that include an **`instrument_variable`** reference:

Asset Identifier = **`'urn:ioos:' + platform + ':' + naming_authority + ':' + platform_id + ':' + instrument_variable:component + ':' + instrument_variable:discriminant`**<br><br>
