---
title: "IOOS Metadata Profile Version 1.2"
keywords: [ioos, metadata, netCDF, 1.2]
tags: [ioos, metadata, netCDF, 1.2]
toc: false
#permalink: index.html
summary:  This is the currently active IOOS Metadata Profile version.  See links in the navbar to the left for previously deprecated versions.
---

## **Revision History**


| Version | Description | Date  |
|:--- |:--- |:--- |
| 1.0 | [Initial version based on the NODC Templates 1.1 and ACDD 1.1](./ioos-metadata-profile-v1-0.html) | 2016-10-01 |
| 1.1 | [Updated version based on the NCEI Templates 2.0 and ACDD 1.3](./ioos-metadata-profile-v1-1.html) | 2016-11-01 |
| **1.2** |**Present Active Version** <br>Updated to reflect new IOOS attribution guidance and ERDDAP implementation: <br>* Add `info_url` <br>* Make `creator_institution`, `creator_url`, and `publisher_url` required <br>* Add `contributor_url` and `contributor_email`<br>* Make `contributor_name`, `contributor_role`, and `institution` recommended (previously were required)<br>* Clarify vocabulary for `contributor_role`<br>* Clarify use of `contributor_name` and `contributor_role` for multiple contributors <br>* Clarify use of `platform` variable  | **2018-12-01** |


## **Notes/Caveats**

1. The IOOS Metadata Profile is a compound profile that builds off of the [**NOAA NCEI NetCDF Templates v2.0**](https://www.nodc.noaa.gov/data/formats/netcdf/), meaning the full IOOS Metadata Profile is a combination of the NCEI Templates plus IOOS-specific guidance included in this document, such as:
* attributes that are IOOS-specific (i.e. additions to the NCEI Templates)
* attributes with a different role in the NCEI Templates; for example, the attribute **`_FillValue`** is **required** by the NCEI Template; however, in the IOOS Profile it is listed as **recommended** only;  conversely the opposite is possible as well
* attributes with modified or further qualified meanings/definitions

1. The NCEI Templates in turn build off of the ACDD and CF conventions.  Some attributes in the IOOS Profile originate from ACDD and CF (consult the `Convention` field in the table to determine the origin of each attribute).  Links to each are below:
* [NOAA NCEI NetCDF Templates 2.0](https://www.nodc.noaa.gov/data/formats/netcdf/v2.0/)
* [Attribute Convention for Data Discovery 1.3](http://wiki.esipfed.org/index.php/Attribute_Convention_for_Data_Discovery_1-3)
* [Climate and Forecast Conventions (CF) 1.7](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html)

1. In the IOOS Profile, attributes can be either **required** or **recommended**:
* all **required** attributes must have meaningful values assigned to them in accordance with the rules prescribed by the corresponding Convention or Template.
* each and all of the **recommended** attributes may be omitted; however, it is highly desirable that these attributes are included into the netCDF metadata ***AND*** have meaningful values assigned to them.
* consult the `Role` field value in the table to determine the value for each attribute

1. The **`platform_variable:ioos_code`** and **`platform_variable:short_name`** are the only **interchangeable** attributes - either a single **`platform_variable:ioos_code`** or a combination of **`platform_variable:short_name`** with **`naming_authority`** is **required** to ensure that ncSOS will be able to produce the IOOS SOS Asset Identifier for the specific platform (see the [NetCDF to IOOS SOS Crosswalk](https://github.com/ioos/ioos-metadata/blob/gh-pages/_docs/NetCDF-to-SOS%20Mappings_clean_2016-04-07a.xlsx) for details). The rest of attributes ***may not*** be substituted for one another.
 <!-- The **`platform_vocabulary`** attribute is at the moment the only pure ACDD v1.3 attribute that is included in the Profile.-->

1. Consult the NCEI 'Gold Standard' example netCDF files, which precisely follow the NCEI Templates and can be a good starting point for building an IOOS Profile-compliant file.  They are available via the following links:
   * [NCEI 'Gold Standard' netCDF - HTTP](https://data.nodc.noaa.gov/ncei/example/data/netcdf/)
   * [NCEI 'Gold Standard' netCDF - THREDDS](https://data.nodc.noaa.gov/thredds/catalog/example/catalog.html)

1. Consult the IOOS Metadata Profile example datasets, published in the 'Standards' ERDDAP instance.  References for specific attribute usage link from the table to datasets in this service.  
* IOOS Metadata Profile Examples: [https://standards.sensors.ioos.us/erddap](https://standards.sensors.ioos.us/erddap)
* IOOS Metadata Profile ERDDAP dataset examples from the Sensor Cache: [http://erddap.sensors.axds.co/erddap/](http://erddap.sensors.axds.co/erddap/)   

1. The [**U.S. IOOS National Glider Data Assembly Center**](https://gliders.ioos.us/index.html) currently uses a slightly different [netCDF File Format (V2)](https://ioos.github.io/ioosngdac/ngdac-netcdf-file-format-version-2); work is in progress to harmonize the NGDAC File Format and IOOS Metadata Profile.



## **IOOS Metadata Profile Attributes**

### Global

Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
title  | ACDD | One sentence about the data contained within the file. | global | **required**
id | ACDD | An identifier for the data set, provided by and unique within its naming authority. The combination of the **`naming authority`** and the **`id`** should be globally unique, but the **`id`** can be globally unique by itself also. IDs can be URLs, URNs, DOIs, meaningful text strings, a local key, or any other unique string of characters. The **`id`** should not include blanks. | global | **required**
naming_authority  | ACDD | The organization that provides the **`id`** for the dataset. <br>The naming authority should be uniquely specified by this attribute; the combination of the **`naming_authority`** and the **`id`** should be a globally unique identifier for the dataset. A reverse-DNS naming is recommended; URIs are also acceptable. <br><br>Example:<br> **`edu.ucar.unidata`** | global | **required**
summary  | ACDD | One paragraph describing the data set. |  global | recommended
info_url  | IOOS | URL for background information about this dataset. | global | **required**
featureType | CF | CF attribute for identifying the featureType, e.g. featureType = "timeSeries". | global | **required**
keywords | ACDD | A comma separated list of key words and phrases. | global | recommended
license  | ACDD | Describe the restrictions to data access and distribution. | global | recommended
standard_name_vocabulary  | ACDD | Standardized field which uses the [CF Standard Names](http://www.cfconventions.org/documents.html/). If a variables does not have an existing standard_name in the CF-managed list, this attribute should not be used. In these cases, a standard name can be proposed to the CF community for consideration and acceptance. | global | **required**

### Attribution

Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
creator_institution  | ACDD | Institution that collected the data. This should be specified even if it matches the value of **`publisher_institution`**, or if **`creator_type`** is institution. | global | **required**
creator_country | IOOS | Country of the person or organization that operates a platform or network, which collected the observation data. | global | **required**
creator_email  | ACDD | Email address of the person or institution that collected the data. | global | **required**
creator_sector | IOOS | [IOOS classifier](http://mmisw.org/ont/ioos/sector) that best describes the platform (network) operator's societal sector. <br><br>Example:<br> **`creator_sector = "academic"`** | global |**required**
creator_url  | ACDD/IOOS | The URL of the *institution* that collected the data. Note that this should always reference an institution URL, and not a personal URL, even if **`creator_type=person`**.  | global | **required**
creator_name  | ACDD | Name of the person or organization that collected the data. | global | recommended
creator_address | IOOS | Street address of the person or organization that collected the data.  | global | recommended
creator_city | IOOS | City of the person or organization that collected the data.  | global | recommended
creator_state | IOOS | State of the person or organization that collected the data.  | global | recommended
creator_zipcode | IOOS | ZIP code of the person or organization that collected the data.  | global | recommended
creator_phone | IOOS | The phone number of the person or group that collected the data. | global | recommended
creator_type | ACDD | Specifies type of creator with one of the following: 'person', 'group', 'institution', or 'position'. If this attribute is not specified, the creator is assumed to be a person.  | global | recommended
institution  | ACDD | The institution of the person or group that collected the data. | global | recommended
contributor_name | ACDD | The name of any individuals or institutions that contributed to the creation of this data. Combined with the **`contributor_role`**, it provides the full description of the contributor. Multiple names should be given in CSV format. <br><br>Examples: {::nomarkdown}<ul> <li>Pacific Islands Ocean Observing System (PacIOOS)</li> <li>Great Lakes Observing System (GLOS),LimnoTech</li></ul>{:/} | global | recommended
contributor_role | ACDD | The role of any individuals or institutions that contributed to the creation of this data. The CI_RoleCode vocabulary ([NERC](http://vocab.nerc.ac.uk/collection/G04/current/), [GEOIDE](https://geo-ide.noaa.gov/wiki/index.php?title=ISO_19115_and_19115-2_CodeList_Dictionaries#CI_RoleCode)) should be used. Multiple roles should be given in CSV format, and presented in the same order and number as the names in `contributor_names`.<br>For the IOOS ncSOS, **`contributor_role = "sponsor"`** defines a person, group, or organization’s full or partial support of an IOOS activity, asset, model, or product. <br><br>Examples:{::nomarkdown}<ul> <li>sponsor</li> <li> sponsor,collaborator</li></ul>{:/}  | global | recommended
contributor_email | IOOS | Email addresses of the individuals or institutions that contributed to the creation of this data. Multiple emails should be given in CSV format, and presented in the same order and number as the names in `contributor_names`. | global | recommended
contributor_url | IOOS | The URL of the individuals or institutions that contributed to the creation of this data. Multiple URLs should be given in CSV format, and presented in the same order and number as the names in `contributor_names`. | global | recommended
publisher_name  | ACDD | Name of the person or group that distributes the data files. Use the conventions described above when identifying persons and/or institutions when applicable. | global | **required**
publisher_country | IOOS | Country of the person or organization that distributes the data.   | global | **required**
publisher_email  | ACDD | The email address of the person or group that distributes the data files. | global | **required**
publisher_url  | ACDD/IOOS | URL of the person or group that distributes the data files. Note that this should always reference an institution URL, and not a personal URL, even if **`publisher_type=person`**.   | global | **required**
publisher_address | IOOS | Street address of the person or organization that distributes the data.   | global | recommended
publisher_city | IOOS | City of the person or organization that distributes the data.   | global | recommended
publisher_zipcode | IOOS | ZIP code of the person or organization that distributes the data.   | global | recommended
publisher_state | IOOS | State of the person or organization that distributes the data.   | global | recommended
publisher_phone | IOOS | The phone number of the person or group that distributes the data files.  | global | recommended
publisher_type | ACDD | Specifies type of publisher with one of the following: 'person', 'group', 'institution', or 'position'. If this attribute is not specified, the publisher is assumed to be a person. | global | recommended


### Variables

Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
geophysical_variable:platform | ACDD/NCEI | This attribute can be used with a geophysical variable to identify the platform that was used in the collection of the data. The value of the attribute should be set to another variable which contains the details of the platform. See the <em>platform_variable</em> attributes below. <br><br>For an example, see the [NCEI Templates timeSeries example (Stearns Wharf)](https://data.nodc.noaa.gov/thredds/catalog/ioos/sccoos/stearns_wharf/catalog.html?dataset=ioos/sccoos/stearns_wharf/stearns_wharf-2013.nc). | variable | **required**
geophysical_variable:_FillValue<br>geospatial_variable:_FillValue | CF | This value is considered to be a special value that indicates undefined or missing data, and is returned when reading values that were not written: {::nomarkdown}<ul>  <li>time:_FillValue = 0.0f    <li>lat:_FillValue = 0.0f    <li>on:_FillValue = 0.0f    <li>z:_FillValue = 0.0f    <li>sea_water_temperature:_FillValue = 0.0f</ul>{:/} | variable | recommended
geophysical_variable:standard_name | CF | Standardized field which uses the [CF Standard Names](http://www.cfconventions.org/documents.html/). If a variables does not have an existing standard_name in the CF-managed list, this attribute should not be used. In these cases, a standard name can be proposed to the CF community for consideration and acceptance. | variable | **required**
geophysical_variable:units  | CF | Required for most all variables that represent dimensional quantities. The value should come from [**`udunits`**](http://www.unidata.ucar.edu/software/udunits/) authoritative vocabulary, which is documented in the CF standard name table with it's corresponding standard name. The **`udunits`** package includes a file `udunits.dat` which lists its supported unit names. | variable | **required**
instrument_variable:discriminant | IOOS | The value of a **`discriminant`** applies to the like-named field in the IOOS SOS Asset Identifier URN; it ensures that in case of multiple sensors measuring the same **`observedProperty`**, each sensor has a unique ID. <br><br>Examples: {::nomarkdown}<ul> <li>sea_water_temperature:<b>top</b> <li> sea_water_temperature:<b>bottom</b> <li> sea_water_temperature:<b>nortek_adp_514</b></ul>{:/}| variable | **required**, if applicable

### Platform

Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
platform_variable:ioos_code | IOOS | Provides IOOS asset identification similar to **`wmo_code`** and **`nodc_code`**. The attribute is a URN that should follow the "[IOOS Convention for Asset Identification](http://ioos.github.io/conventions-for-observing-asset-identifiers/ioos-assets-v1-0.html)" with a general pattern of _**`urn:ioos:asset_type:authority:label[:discriminant]`**_.  <br><br>Examples: {::nomarkdown}<ul> <li> <b><code>urn:ioos:glider:wmo:4801902:20160218T1913Z</code></b> <li><b><code>urn:ioos:station:us.glos:45024</code></b> </ul>{:/} <br>**NOTE:** interchangeable with **`platform_variable:short_name`** | variable | **required**
platform_variable:long_name | NCEI Templates | Provide a descriptive, long name for this variable. | variable | **required**
platform_variable:short_name | IOOS | Provide a short name for the platform.  Similar to ID, a **`short_name`** can be any unique string of characters that does not include blanks. <br><br>Examples: {::nomarkdown}<ul> <li> <b><code>station_1:short_name = “carquinez”</code></b> <li><b><code>station_1:short_name = “cb0102</code></b> </ul>{:/} <br>**NOTE:** interchangeable with **`platform_variable:ioos_code`** | variable | **required**
platform_variable:type | IOOS | In  conjunction with a **`platform_vocabulary`** attribute, identifies platform's type as defined in the [IOOS Platform Categories vocabulary](https://mmisw.org/ont/ioos/platform), or [SeaVoX Platform Categories vocabulary](http://vocab.nerc.ac.uk/collection/L06/current/"), or any other vocabulary. The URL of the actual vocabulary must be published in the **`platform_vocabulary`** global attribute. <br><br>Alternatively, the **`platform`** and **`platform_vocabulary`** pair of attributes may be used; however, this option is not recommended (see details in the **`platform_vocabulary`** description.) | variable | **required**
platform_vocabulary | ACDD | Controlled vocabulary for the names used in the "platform" attribute.<br><br> It is recommended that this attribute is used in conjunction with the **`platform_variable:type`** attribute. In that case, the recommended value for the **`platform_vocabulary`** attribute is a URL to either the [IOOS Platform Category vocabulary](http://mmisw.org/ont/ioos/platform), or [SeaVoX Platform Categories vocabulary](http://vocab.nerc.ac.uk/collection/L06/current/). <br><br>Example:<br> **`platform_vocabulary = "http://mmisw.org/ont/ioos/platform"`**<br><br>As an alternative (although not recommended), a NetCDF file may follow the NCEI Template v2.0, which suggests the use of "NASA GCMD Platform Keywords Version 8.1" string as the fixed value for the **`platform_vocabulary`**, and does not stipulate for the **`platform_variable:type`**. Instead, the actual type of the platform must be placed in the global **`platform`** attribute as described in the Science Keyword Rules (http://gcmd.nasa.gov/learn/rules.html) for NASA Global Change Master Directory (GCMD) Keywords (http://gcmd.nasa.gov/learn/keywords.html). <br><br>Example:<br> **`platform: In Situ Ocean-based Platforms > MOORINGS`** | global | **required**
platform (global attribute) | ACDD/NCEI |  Name of the *type* of platform(s) that supported the sensor data used to create this data set or product. Platforms can be of any type, including satellite, ship, station, aircraft or other. The controlled vocabulary must be indicated in the `platform_vocabulary` field. <br><br>Example (global variable): {::nomarkdown}<ul> <li> <b><code>platform "buoy";</code></b> <li><b><code>platform_vocabulary "IOOS Platform Vocabulary";</code></b> </ul>{:/} | global | **required**

<br>



<!---







<dl>
<dt><b>Conventions</b>:</dt>
<dd>
Version of the <a href="http://cfconventions.org/">Climate and Forecast metadata conventions</a> followed by the file format specification.
</dd>
<dd>
<b>Value</b>: "CF-1.6"
</dd>

-->

<!--

#####<i>platform</i>#####
<dl>
<dd>
<table>
<tr><th><b>Dimension</b></th><td>None</td></tr>
<tr><th><b>Data Type</b></th><td>int</td></tr>
<tr><th><b>Value Type</b></th><td>Scalar</td></tr>
<tr><th><b>_FillValue</b></th><td>-999</td>
<tr><th><b>Description</b></th><td>Variable to store meta data about the glider platform that measured the profile.  All of the attributes of this variable, with the exception of <b>comment</b> are <b>REQUIRED</b>.  This variable contains a <b>wmo_id</b> attribute to store the <b>WMO ID</b> assigned to this glider by NDBC.  The <b>WMO ID</b> is also stored as a global file attribute to allow for aggregations of all deployments from the platform with that <b>WMO ID</b>.</td></tr>
</table>
</dd>
<dd>
<a href="https://www.unidata.ucar.edu/software/netcdf/docs/netcdf/Data-Model.html">CDL</a> example with <b>REQUIRED</b> attributes and comments on values:
<pre>
    int platform ;
		platform:_FillValue = -999 ;
		platform:comment = "Slocum Glider ru29" ; # Change
		platform:id = "ru29" ; # Change
		platform:instrument = "instrument_ctd" ;
		platform:long_name = "Rutgers University Slocum Glider ru29" ; # Change
		platform:type = "platform" ;
		platform:wmo_id = " " ; # WMO ID specific to this glider
</pre></dd>
</dl>

-->
