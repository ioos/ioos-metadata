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
| **1.2** |**Present Active Version** <br>Updated to reflect new IOOS attribution guidance and ERDDAP implementation: <br>* Add `info_url` <br>* Make `creator_institution`, `creator_url`, and `publisher_url` required <br>* Add `contributor_url`, `contributor_email`, and `contributor_role_vocabulary`<br>* Make `contributor_name`, `contributor_role`, and `institution` recommended (previously were required)<br>* Clarify default vocabulary for `contributor_role` and `contributor_role_vocabulary`<br>* Clarify use of `contributor_name` and `contributor_role` for multiple contributors <br>* Clarify use of `platform` variable  | **2018-12-01** |


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
* consult the `Role` field value in the table to determine the value for each attribute

1. The IOOS Profile allows only one **'platform'** per dataset.  Please see the corresponding [Platform](#platform) section of the profile below for more information.

1. The [**U.S. IOOS National Glider Data Assembly Center**](https://gliders.ioos.us/index.html) currently uses a slightly different [netCDF File Format (V2)](https://ioos.github.io/ioosngdac/ngdac-netcdf-file-format-version-2); work is in progress to harmonize the NGDAC File Format and IOOS Metadata Profile.


## Gold Standard Example Datasets

Consult the [IOOS Metadata Profile "Gold Standard" example netCDF files](gold-standard-examples.html), which follow this profile and can be used as templates to generate compliant datasets.  The Gold Standard datasets are hosted in ERDDAP, however since this profile can be applied to datasets hosted in THREDDS or other comparable data servers.

In addition to the Gold Standard datasets, there are some in-line examples highlighting specific attribute use cases that comply with the profile.



## IOOS Metadata Profile Attributes

### Global

Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
featureType | CF | CF attribute for identifying the featureType, e.g. featureType = "timeSeries". | global | **required**
id | ACDD | An identifier for the data set, provided by and unique within its naming authority. The combination of the **`naming authority`** and the **`id`** should be globally unique, but the **`id`** can be globally unique by itself also. IDs can be URLs, URNs, DOIs, meaningful text strings, a local key, or any other unique string of characters. The **`id`** should not include blanks. | global | **required**
info_url  | IOOS | URL for background information about this dataset. | global | **required**
keywords | ACDD | A comma separated list of key words and phrases. | global | recommended
license  | ACDD | Describe the restrictions to data access and distribution. | global | recommended
naming_authority  | ACDD | The organization that provides the **`id`** for the dataset. <br>The naming authority should be uniquely specified by this attribute; the combination of the **`naming_authority`** and the **`id`** should be a globally unique identifier for the dataset. A reverse-DNS naming is recommended; URIs are also acceptable. <br><br>Example:<br> **`edu.ucar.unidata`** | global | **required**
references  | ACDD | Published or web-based references that describe the data or methods used to produce it. Recommend URIs (such as a URL or DOI) for papers or other references. | global | recommended
standard_name_vocabulary  | ACDD | The name and version of the controlled vocabulary from which variable standard names are taken. Values for any variable's **`standard_name`** attribute must come from the CF Standard Names vocabulary for the dataset to comply with CF. <br><br>The format for the **`standard_name`** attribute must follow the ACDD recommendation ('CF Standard Name Table vXX', where 'XX' is a version of the standard name table), in order to be valid and meet the ACDD conventions.<br><br>If a variables does not have an existing standard_name in the CF-managed list, the variable should not include a **`standard_name`** attribute. In these cases, a standard name can be proposed to the CF community for consideration.<br><br>  Example:<br>**`standard_name_vocabulary = 'CF Standard Name Table v64'`** | global | **required**
summary  | ACDD | One paragraph describing the data set. |  global | recommended
title  | ACDD | One sentence about the data contained within the file. | global | **required**

#### Example

Taken from the [Morro Bay BS1 MET Gold Standard Example](https://standards.sensors.ioos.us/erddap/info/morro-bay-bs1-met/index.html).

```
NC_GLOBAL {
    featureType               TimeSeries
    id                        morro-bay-bs1-met
    info_url                  https://sensors.ioos.us/?sensor_version=v2#metadata/57163/station
    naming_authority          edu.calpoly.marine
    references                http://www.slosea.org/about/dash.php,https://www.cencoos.org/data/shore/morro
    standard_name_vocabulary  CF Standard Name Table v63
    summary                   Timeseries data from 'Morro Bay - BS1 MET' (morro-bay-bs1-met)
    title                     Morro Bay - BS1 MET
}
```

### Attribution

The attributes listed in the table below allow for consistent attribution of datasets within IOOS' national products.  Data providers are encouraged to follow these attribute guidelines exactly to ensure datasets appear with proper attribution.  

Consult the [Gold Standard example datasets](gold-standard-examples.html) for good examples to start from.

Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
contributor_email | IOOS | Email addresses of the individuals or institutions that contributed to the creation of this data. Multiple emails should be given in CSV format, and presented in the same order and number as the names in **`contributor_names`**. | global | recommended
contributor_name | ACDD | The name of any individuals or institutions that contributed to the creation of this data. Combined with the **`contributor_role`**, it provides the full description of the contributor. Multiple names should be given in CSV format. <br><br>Examples: {::nomarkdown}<ul><li><b><code>contributor_name = Pacific Islands Ocean Observing System (PacIOOS)</b></code></li> <li><b><code>contributor_name = Great Lakes Observing System (GLOS),LimnoTech</b></code></li></ul>{:/} | global | recommended
contributor_role | ACDD | The role of any individuals or institutions that contributed to the creation of this data. The CI_RoleCode vocabulary ([NERC](http://vocab.nerc.ac.uk/collection/G04/current/), [GEOIDE](https://geo-ide.noaa.gov/wiki/index.php?title=ISO_19115_and_19115-2_CodeList_Dictionaries#CI_RoleCode)) should be used. Multiple roles should be given in CSV format, and presented in the same order and number as the names in **`contributor_names`**.<br>For the IOOS ncSOS, **`contributor_role = "sponsor"`** defines a person, group, or organization’s full or partial support of an IOOS activity, asset, model, or product. <br><br>Examples:  {::nomarkdown}<ul><li><b><code>contributor_role = sponsor</b></code></li> <li><b><code>contributor_role = sponsor,collaborator</b></code></li></ul>{:/} | global | recommended
contributor_role_vocabulary | IOOS | The URL of the controlled vocabulary used for the **`contributor_role`** attribute. The default is ["http://vocab.nerc.ac.uk/collection/G04/current/"](http://vocab.nerc.ac.uk/collection/G04/current/). | global | recommended
contributor_url | IOOS | The URL of the individuals or institutions that contributed to the creation of this data. Multiple URLs should be given in CSV format, and presented in the same order and number as the names in **`contributor_names`**. | global | recommended
creator_address | IOOS | Street address of the person or organization that collected the data.  | global | recommended
creator_city | IOOS | City of the person or organization that collected the data.  | global | recommended
creator_country | IOOS | Country of the person or organization that operates a platform or network, which collected the observation data. | global | **required**
creator_email  | ACDD | Email address of the person or institution that collected the data. | global | **required**
creator_institution  | ACDD | Institution that collected the data. This should be specified even if it matches the value of **`publisher_institution`**, **`institution`** or if **`creator_type`** is institution. | global | **required**
creator_name  | ACDD | Name of the person or organization that collected the data. <br><br>Follow the guidance described in the **`creator_type`** attribute for how to populate this field depending on whether a person, institution, group, or position. | global | recommended
creator_phone | IOOS | The phone number of the person or group that collected the data. | global | recommended
creator_sector | IOOS | [IOOS classifier](http://mmisw.org/ont/ioos/sector) that best describes the platform (network) operator's societal sector. <br><br>Example:<br> **`creator_sector = "academic"`** | global |**required**
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
publisher_name  | ACDD | Name of the person or group that distributes the data files. <br><br>Follow the guidance described in the **`publisher_type`** attribute for how to populate this field depending on whether a person, institution, group, or position. | global | **required**
publisher_phone | IOOS | The phone number of the person or group that distributes the data files.  | global | recommended
publisher_state | IOOS | State of the person or organization that distributes the data.   | global | recommended
publisher_type | ACDD | Specifies type of publisher with one of the following: 'person', 'group', 'institution', or 'position'. If this attribute is not specified, the publisher is assumed to be a person. | global | recommended
publisher_url  | ACDD/IOOS | URL of the person or group that distributes the data files. Note that this should always reference an institution URL, and not a personal URL, even if **`publisher_type=person`**.   | global | **required**
publisher_postalcode | IOOS | The postal code of the person or organization that distributes the data.   | global | recommended

#### Example

Taken from the [Morro Bay BS1 MET Gold Standard Example](https://standards.sensors.ioos.us/erddap/info/morro-bay-bs1-met/index.html).

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

Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
geophysical_variable:_FillValue<br>geospatial_variable:_FillValue | CF | This value is considered to be a special value that indicates undefined or missing data, and is returned when reading values that were not written. The type of this variable should match the type of the unpacked variable data. {::nomarkdown}<ul>  <li>time:_FillValue = -999999.0f    <li>lat:_FillValue = -999999.0f    <li>lon:_FillValue = -999999.0f    <li>z:_FillValue = -999999.0f    <li>sea_water_temperature:_FillValue = Float.NaN</ul>{:/} | variable | recommended
geophysical_variable:missing_value<br>geospatial_variable:missing_value | CF | This should always be equal to the `_FillValue` attribute and both are used for legacy library support. {::nomarkdown}<ul>  <li>time:missing_value = -999999.0f    <li>lat:missing_value = -999999.0f    <li>lon:missing_value =-999999.0f    <li>z:missing_value = -999999.0f <li>sea_water_temperature:missing_value = Float.NaN</ul>{:/} | variable | recommended
geophysical_variable:standard_name | CF | Standardized field which uses the [CF Standard Names](http://www.cfconventions.org/documents.html/). If a variables does not have an existing standard_name in the CF-managed list, this attribute should not be used. In these cases, a standard name can be proposed to the CF community for consideration and acceptance. | variable | **required**
geophysical_variable:standard_name_uri | IOOS | The URI of a **`standard_name`** in the online vocabulary listed in the global **`standard_name_vocabulary`** attribute.<br><br>Example: {::nomarkdown}<ul> <li> <b><code>sea_water_temperature:standard_name_uri = "http://vocab.nerc.ac.uk/collection/P07/current/CFSN0335/"</code></b> </li>  <li> <b><code>sea_water_temperature:standard_name = "sea_water_temperature"</code></b> </li> </ul>{:/} | variable | recommended
geophysical_variable:units  | CF | Required for most all variables that represent dimensional quantities. The value should come from [**`udunits`**](http://www.unidata.ucar.edu/software/udunits/) authoritative vocabulary, which is documented in the CF standard name table with it's corresponding standard name. The **`udunits`** package includes a file `udunits.dat` which lists its supported unit names. | variable | **required**

#### Example

Taken from the [Morro Bay BS1 MET Gold Standard Example](https://standards.sensors.ioos.us/erddap/info/morro-bay-bs1-met/index.html).

```
Attributes {
    air_temperature {
        _FillValue     -9999.0
        missing_value  -9999.0
        long_name      Air Temperature
        platform       station
        standard_name  air_temperature
        units          degree_Celsius
        urn            http://mmisw.org/ont/cf/parameter/air_temperature
    }
}
```

See the `station` variable below.


### Platform

The correct method for specifying platform metadata has historically been a source of confusion. The IOOS Metadata Profile aims to simplify platform metadata specification with the addition of a few global attributes (**`platform_id`** and **`platform_name`**, as well as the OceanSITES-derived **`wmo_platform_code`**) and clarification of existing standards for global attributes and the platform container variable. Data providers are encouraged to carefully review this section and upstream standards, and especially to review gold standard example datasets.

**Important**: The IOOS Metadata Profile restricts datasets to include only **one platform per dataset**.  This simplifies the dataset structure significantly, allows for attribution that might otherwise be handled by variable-level attributes of the **`platform_variable`** to be replaced by the global attributes described above, and simplifies creation of aggregated datasets in ERDDAP.


Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
platform | ACDD/NCEI |  **Global** attribute specifying the name of the *type* of platform(s) that supported the sensor data used to create this data set or product. Platforms can be of any type, including satellite, ship, station, aircraft or other. The controlled vocabulary must be indicated in the **`platform_vocabulary`** field.<br><br>Example: {::nomarkdown}<ul> <li> <b><code>platform "buoy";</code></b> <li><b><code>platform_vocabulary "https://mmisw.org/ont/ioos/platform";</code></b> </ul>{:/}<br><br>The value of the **`platform`** global attribute is used in generating the [IOOS Asset Identifier]([https://ioos.github.io/conventions-for-observing-asset-identifiers/ioos-assets-v1-0.html]) for the dataset.  Consult the [Rules for Asset Identifier Generation](#rules-for-ioos-asset-identifier-generation) section below this table for details on how this formula works. | global | **required**
platform | CF | **Variable** level attribute to be specified on each data variable with the value of the name of another container variable which contains platform metadata attributes. In the most common use case where a datasets contains a single platform - **a requirement according to this profile** - there will be a single platform container variable (usually named **`station`** or **`platform`**), and every data variable in the dataset will contain a **`platform`** attribute with the name of the platform variable. <br><br>The primary use of this platform variable is to specify CF feature type information (plus some optional additional metadata).  See the [`platform_variable`](#platform-variable) section below. <br><br>Example: {::nomarkdown}<ul> <li> <b><code>sea_water_temperature:platform = "station"</code></b> </ul>{:/}<br><br>  | variable | **required**
platform_id | IOOS | An optional, short identifier for the platform, if the data provider prefers to define an id that differs from the dataset identifier, as specified by the  **`id`** attribute.<br><br>  When **`platform_id`** is defined for a dataset, it is used in place of the **`id`** field in generating the IOOS Asset Identifier (consult the [Rules for Asset Identifier Generation](#rules-for-ioos-asset-identifier-generation) section below). <br><br>Examples: {::nomarkdown}<ul> <li> <b><code>platform_id = "carquinez"</code></b> <li><b><code>platform_id = "cb0102"</code></b> </ul>{:/} | global | recommended
platform_name | IOOS | A descriptive, long name for the platform used in collecting the data.  <br><br>The value of **`platform_name`** will be used to label the platform in downstream applications, such as IOOS' National Products (Environmental Sensor Map, EDS, etc) <br><br>Examples: {::nomarkdown}<ul> <li> <b><code>platform_name = "Morro Bay - BS1 MET"</code></b> <li><b><code>platform_name = "Chesapeake Bay Buoy 102"</code></b> </ul>{:/} | global | **required**
platform_vocabulary | ACDD | Controlled vocabulary for the names used in the **`platform`** attribute.<br><br> It is recommended that this attribute is used in conjunction with the **`platform_variable:type`** attribute. In that case, the recommended value for the **`platform_vocabulary`** attribute is a URL to either the [IOOS Platform Category vocabulary](http://mmisw.org/ont/ioos/platform), or [SeaVoX Platform Categories vocabulary](http://vocab.nerc.ac.uk/collection/L06/current/). <br><br>Example:<br> **`platform_vocabulary = "http://mmisw.org/ont/ioos/platform"`**<br><br>The IOOS Metadata Profile diverges from the NCEI Templates 2.0 in that the use of the "NASA GCMD Platform Keywords 8.1" as a **`platform_vocabulary`** is not allowed.  The reason for this is that the **`platform`** global attribute is used in generating the [IOOS Asset Identifier 1.0](https://ioos.github.io/conventions-for-observing-asset-identifiers/ioos-assets-v1-0.html) for the dataset, and thus requires a single string platform name with no blank characters.  GCMD Platform Keywords do not follow this pattern and therefore are disallowed.| global | **required**
wmo_platform_code | IOOS | The WMO identifier for the platform used to measure the data.<br><br>When a dataset is assigned a **`wmo_platform_code`** it is thereby assigned a secondary Asset Identifier for the **'wmo' `naming_authority`**.  See the  [Rules for Asset Identifier Generation](#rules-for-ioos-asset-identifier-generation) for more information.  <br><br>Examples: {::nomarkdown}<ul> <li> <b><code>wmo_platform_code = "44011"</code></b> </ul>{:/} | global | **required**, if applicable

### Platform Variable

Container variable which exists solely to hold platform metadata attributes, and comply with the CF Discrete Sampling Geometries specification. Data variables must reference the name of this variable in their **`platform`** attribute (described above). The platform variable can be of any data type.

For more information about CF Discrete Sampling Geometries and associated requirements, see the [CF Documentation](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html#discrete-sampling-geometries).

Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
platform_variable:cf_role | [CF](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/build/ch09s05.html) | Specifies the [CF sampling geometry feature type](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/build/ch09.html). Allowed values are `timeseries_id`, `profile_id`, and `trajectory_id`.  | variable | **required**


### Platform Variable (To Remove)

The following platform_variable attributes will be removed and replaced by corresponding global attributes.  `ioos_code` will no longer be used in this profile.  Asset Identifiers will be derived/inferred based on global attribute values.  See [rules](#rules-for-ioos-asset-identifier-generation) for this.  

Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
platform_variable:ioos_code | IOOS | Provides IOOS asset identification similar to **`wmo_code`** and **`nodc_code`**. The attribute is a URN that should follow the "[IOOS Convention for Asset Identification](http://ioos.github.io/conventions-for-observing-asset-identifiers/ioos-assets-v1-0.html)" with a general pattern of _**`urn:ioos:asset_type:authority:label[:discriminant]`**_.  <br><br>Examples: {::nomarkdown}<ul> <li> <b><code>urn:ioos:glider:wmo:4801902:20160218T1913Z</code></b> <li><b><code>urn:ioos:station:us.glos:45024</code></b> </ul>{:/} <br>**NOTE:** interchangeable with **`platform_variable:short_name`** | variable | **required**
platform_variable:long_name | NCEI Templates | Provide a descriptive, long name for this variable. | variable | **required**
platform_variable:short_name | IOOS | Provide a short name for the platform.  Similar to ID, a **`short_name`** can be any unique string of characters that does not include blanks. <br><br>Examples: {::nomarkdown}<ul> <li> <b><code>station_1:short_name = “carquinez”</code></b> <li><b><code>station_1:short_name = “cb0102</code></b> </ul>{:/} <br>**NOTE:** interchangeable with **`platform_variable:ioos_code`** | variable | **required**
platform_variable:type | IOOS | In  conjunction with a **`platform_vocabulary`** attribute, identifies platform's type as defined in the [IOOS Platform Categories vocabulary](https://mmisw.org/ont/ioos/platform), or [SeaVoX Platform Categories vocabulary](http://vocab.nerc.ac.uk/collection/L06/current/"), or any other vocabulary. The URL of the actual vocabulary must be published in the **`platform_vocabulary`** global attribute. <br><br>Alternatively, the **`platform`** and **`platform_vocabulary`** pair of attributes may be used; however, this option is not recommended (see details in the **`platform_vocabulary`** description.) | variable | **required**



#### Example

Taken from the [Morro Bay BS1 MET Gold Standard Example](https://standards.sensors.ioos.us/erddap/info/morro-bay-bs1-met/index.html).

```
Attributes {
    station {
        cf_role        timeseries_id
        ioos_category  Identifier
        ioos_code      urn:ioos:station:edu.calpoly.marine:57163
        long_name      Morro Bay - BS1 MET
        short_name     morro-bay-bs1-met
        type           fixed
    }
}
```

```
NC_GLOBAL {
    platform             fixed
    platform_vocabulary  http://mmisw.org/ont/ioos/platform
}
```


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


## Rules for IOOS Asset Identifier Generation

The [IOOS Asset Identifier 1.0](https://ioos.github.io/conventions-for-observing-asset-identifiers/ioos-assets-v1-0.html) can be constructed from the Metadata Profile attributes as described below. <br><br>  

For reference, the Asset Identifier is composed of the following components:

Asset Identifier = <code><b>urn:ioos:asset_type:authority:label[:component][:discriminant][#functional_parameters]</b></code><br><br>

If **`platform_id`** present:

Asset Identifier = <code><b>'urn:ioos:' + platform + ':' + naming_authority + ':' + platform_id</b></code><br><br>

If **`platform_id`** not present:

Asset Identifier = <code><b>'urn:ioos:' + platform + ':' + naming_authority + ':' + id</b></code><br><br>

For datasets with a **`wmo_platform_code`** global attribute, a second Asset Identifier is also assumed, according to the following rules:

WMO Asset Identifier = <code><b>'urn:ioos:' + platform + ':wmo:' + wmo_platform_code</b></code><br><br>

This means it is possible for a single dataset to have two valid IOOS Asset Identifiers.  It is also possible to define as many custom global 'id' attributes as necessary.  For example, RAs may define their own identification scheme outside those described here, or, if there is another organization (such as NCEI) for which an id is appropriate, it may be included as well (e.g. **`ncei_id = 123456789`** or  **`ncei_accession = 123456789`**).  While these won't technically be considered to be IOOS Asset Identifiers, there is still the opportunity to identify datasets using community-agreed-upon global identifier attributes.

Additional considerations regarding IOOS Asset Identifiers:

* At the moment, the specification constrains the valid **`asset_type`**s to be: glider, station, network, sensor, and survey.  For the purposes of the IOOS Metadata Profile, the values of **`platform'** can be more broad, however the resulting Asset Identifiers may not be valid according to that specification.

* If an **`instrument_variable`** is defined for the dataset, it becomes possible for each data variable associated with it (via the **`:instrument`** variable attribute) to have its own Asset Identifier that is more fully qualified than the global-variable-defined dataset Asset Identifier described above.  See the [documentation](#instrument) for **`instrument_variable:component`** and **`instrument_variable:discriminant`** for details.
<br>
