# Shoreline Cleanup Assessment Technique (SCAT) Digital Data Standard - Draft

**5/7/2015**

## Purpose

This document describes a proposed data standard for observational Shoreline Cleanup Assessment Technique (SCAT) data collected by field survey teams during oil spills and similar incidents to evaluate shoreline oiling, recommend and guide treatment, and document compliance with cleanup endpoints. The volume of data collected and developed during oil spill response is growing at an ever increasing rate. This places a substantial burden on the response to be able to rapidly digest and interpret those data to inform operational decision making. This growth in the data management workload has been facilitated by the rapid evolution of electronic field data collection tools, data storage systems and common operational displays. Absent a common vision for how these systems will work together, these tools will be unable to provide a pathway to distill these data and translate them into operationally meaningful information.

This draft standard was developed by the National Oceanic and Atmospheric Administration (NOAA) Office of Response and Restoration (OR&R), Emergency Response Division (ERD). While there are a variety of SCAT or similar protocols and processes that exist ([CEDRE, 2006](http://wwz.cedre.fr/en/Our-resources/Documentation/Operational-guides/Surveying-Sites); [MCA, 2007](https://www.gov.uk/government/uploads/system/uploads/attachment_data/file/297968/ukscatman.pdf); [Owens and Sergy, 2000](http://www.shorelinescat.com/Documents/Manuals/Environment%20Canada%202000%20SCAT%20Manual%202nd%20Edition/SCAT%20Manual%20Complete.pdf); [Owens and Sergy 2004](http://www.shorelinescat.com/Documents/Manuals/Environment%20Canada%202004%20Arctic%20SCAT.pdf)), this standard is intended to support the storage and manipulation of data to support the SCAT process as described in the NOAA Shoreline Assessment Manual ([NOAA, 2013](http://response.restoration.noaa.gov/sites/default/files/manual_shore_assess_aug2013.pdf)). This standard is provided to the response community as a common point of reference in the development of electronic field data collection tools, databases and information products for SCAT activities. This is a voluntary standard that will be maintained and updated by NOAA based on input from the response community and the evolution of new technologies.

The draft data standard proposed here includes:

1. A conceptual data model, consisting of a set of proposed entities and relationships,
2. Rules for spatial representation of these entities,
3. Required core tabular attributes describing these entities,
4. Required spatial relationships and logical relationships between entities, and
5. Minimum documentation requirements.

This proposed data standard does not include mandatory logical data model (a set of explicitly required normalized tables, attributes, and relationships) for use in Geographic Information (GIS) or Relational Database Management System (RDBMS) software, though it does suggest these via higher-level concepts. The spatial and attribute data required by the standard are not intended as the entirety of a fully articulated logical data model or database structure. It is expected that databases, applications, or other tools that are used to maintain data compliant with this standard will each have design requirements that require a specific logical model, or a more complex or normalized database structure. In short, the standard is a _standard for a data model_, not a database, database design, or a spatial data storage model.

In addition, the standard is intended to support data management for SCAT carried out for the simplest spill that would require management of digital SCAT data. Data managers may need to extend the standard (and associated logical schema or data model) to include additional conceptual entities (e.g. shoreline cleanup status categories), spatial features, tables, or attributes required for a more complex incident, or adapt to incident-specific requirements. Lastly this standard does not address all the tasks required as part of SCAT data management (see [Lamarche et al., 2007](http://www.shorelinescat.com/Documents/Manuals/Environment%20Canada%202007%20SCAT%20Data%20Management%20Manual.pdf); [NOAA, 2013](http://response.restoration.noaa.gov/sites/default/files/manual_shore_assess_aug2013.pdf)). This standard only describes the required components for formal structured data that are collected by full SCAT teams. Data collected by pre-spill surveys, reconnaissance, field photography, special surveys, or to support administrative status tracking are all generally managed by SCAT data management teams, but these data can be highly spill-specific and are not within the scope of this standard.

## Conceptual Data Model

The standard includes a few core conceptual entities, described below, including shorelines, segments, surveys, surface oil observations, subsurface oil observations and treatment recommendations (Figure 1).  These entities describe general classes of data collected and managed by SCAT.

![Figure 1](https://github.com/researchplanninginc/NOAA-SCAT-Standard/blob/master/graphics/fig1.png?raw=true)

**Figure 1.** Schematic of spatial relationships among conceptual entities over time showing a shoreline partitioned into segments.  SOOs from a survey on Dates 1 and 2 are depicted as blue and red lines coincident with the shoreline for No Oiling Observed and Oiled SOOs respectively.  SSOOs from Date 2 are depicted as red and blue points in the vicinity of the shoreline for No Oiling Observed and Oiled SOOs respectively.  The extent of an STR on Date 3 is depicted as a green line coincident with the shoreline.


####Shoreline Representation
Shorelines are intertidal, fluvial, or lacustrine environments where the land-water interface often changes in position and extent over both long and short time-scales. In order to accurately compare SCAT field data from multiple surveys at a single location it is necessary to reference these observations using a single digital shoreline representation. Shorelines representations are fixed, spatially unchanging extents of shoreline habitat. These may be derived from existing spatial data before a spill occurs or it may be necessary generate the Shoreline Representation after an incident has occurred. Shorelines are typically represented as a one-dimensional digital vector line, but may be represented as polygons (complex wetlands or floodplains) or, rarely, points. If a spill event persists for long enough, shoreline representations may move or change in morphology. 

####Segments
Shoreline segments are relatively fixed, spatially unchanging subsets of a shoreline representation that are used operationally during a spill response to reference specific portions of a shoreline. These may be predefined before surveys take place, or even before a spill occurs; however, they can also be determined in the field by SCAT teams as they conduct initial surveys. Optimally, segments have consistent geomorphic, physical, and administrative characteristics and are fixed in space. If a spill event persists for long enough, segments may move or change in morphology either as a function of change in their parent shoreline representation or within/along an unchanged parent shoreline representation for operational or administrative reasons. Segments are unique and non-overlapping in space at a given point in time. A segment must be a child element of a shoreline representation.

####Surveys
A survey is atime-specific assessment of the oiling conditions along some subset of a shoreline representation. Surveys may or may not cover the entire length of one or more specific segments. Surveys may describe shoreline surveyed by SCAT teams on foot or observed remotely from vessels or aircraft, and do not necessarily represent areas physically occupied by SCAT teams. Surface and subsurface oiling observations made by field teams on a specific survey are child elements of that survey. A survey has no spatial extent beyond those child elements and is thus defined by the aggregate of the spatial extents of those child elements. Surveys may overlap in space and time.  Surveys are associated with structured data such as the date, time and location of the survey as well as a list of the SCAT team members and a formalized generic description of the survey area (see Table 2 below and sections 1-5 of the Shoreline Oil Summary form in [Appendix A](https://github.com/researchplanninginc/NOAA-SCAT-Standard/blob/master/Draft%20SCAT%20Data%20Standard.md#appendix-a--example-shoreline-observation-form)).

####Surface Oiling Observation (SOO)
SOOs (commonly termed oiling zones, where no observed oil is a type of oiling zone) are survey and time-specific representations of consistent observed surface oiling and other shoreline characteristics. SOOs are commonly referenced by start and end points (collected as GPS way points) of the oiling zone along with a description of the oiling characteristics using the SCAT methodology. These start-stop points are matched to the Shoreline Representation discussed above to comply with the topological requirements described in the following sections. This feature matching may be done at the time of data collection or via post-processing. Structured data associated with SOOs contain an across-shore width scalar value and a tidal elevation, but all SOOs that overlap along-shore are typically referenced as separate linear features that are all coincident with the shoreline.  In some circumstances it may be necessary to represent SOOs as polygonal features (e.g. complex wetlands or floodplains) or points. Unless this is required to support unique operational considerations however, it is recommended that SOOs be represented as linear features along a linear shoreline representation. SOOs may potentially overlap in space (different tidal zones along the same shoreline) and time. See Table 3 below and sections 6 of the Shoreline Oil Summary form in [Appendix A](https://github.com/researchplanninginc/NOAA-SCAT-Standard/blob/master/Draft%20SCAT%20Data%20Standard.md#appendix-a--example-shoreline-observation-form) for structured data associated with SOOs.

####Subsurface Oiling Observation (SSOO)
SSOOs are survey and time-specific representations of observed subsurface oiling and other shoreline characteristics. SSOOs are generally explicitly referenced with a single zero-dimensional point together with one or more scalar depth values where oiling was investigated in the field  by excavation of a pit, trench, or core.  As with SOOs, SSOOs may occasionally be referenced as polygons or lines but this is not recommended unless dictated by operational requirements. SSOOs may potentially overlap in space and time – though generally this will not occur if represented by zero-dimensional points. All SSOOs must be a child element of a survey. See Table 4 below and sections 7 of the Shoreline Oil Summary form in [Appendix A](https://github.com/researchplanninginc/NOAA-SCAT-Standard/blob/master/Draft%20SCAT%20Data%20Standard.md#appendix-a--example-shoreline-observation-form) for structured data associated with SOOs.

####Shoreline Treatment Recommendations (STR)
STRs are time-period-specific recommended cleanup actions prescribed/permitted for a given location. STRs may be referenced to surface or subsurface representations of any geometry from partial or complete portions of one or more segments. STRs are not necessarily related to SOOs or SSOOs, or even surveys, though this is often the case. STRs are not required to have an explicit spatial representation, but may instead be described by subsets of a shoreline representation based upon the existence of and relationships between other spatial conceptual entities that are child elements of that shoreline representation (for example, STRs may be referenced by the extent of a specific SSO from a specific survey, or to a specific segment). While STRs are often defined by segments or specific surface or subsurface oiling observations in practice, they have no other mandatory relationships with other entities.

## Required Spatial Data

Specific conceptual entities must have explicit and unique spatial representation as independent vector geometry for use and analysis in GIS software or web mapping applications. At minimum, these include:

- Shoreline Representation
- Segments
- Surface Oiling Observations (SOOs or oiling zones)
- Subsurface Oiling Observations (SSOOs or pits)

Other conceptual entities are also required to have spatial representations, but these do not necessarily have to be stored explicitly as independent vector geometry. Instead these may be stored either as vector geometry, or they may be stored as non-spatial lists or lookup tables of other entities that do have explicit geometry.  These entities include:

- Surveys
- Shoreline Treatment Recommendations

Figure 2 is schematic of entities and their required spatial relationships over time. Surveys are required to have spatial extents consisting only of their children surface and subsurface shoreline observations. As such, the spatial extent of a survey can either be represented by a non-spatial list of its surface and subsurface shoreline observations, or by explicit vector geometry that is identical to the vector geometry of its component SSOO and SOO.  STRs may have spatial extents defined by one or more SOOs or SSOOs, one or more segments, or some other portion of a shoreline representation, or some other spatial extent.  If a STR may be uniquely defined by reference to other entities, then it can be spatially represented by a non-spatial list of these other features.  If a STR has a spatial extent that cannot be uniquely defined by one or more SOOs, SSOOs, or segments, then it must be represented by explicit vector geometry.

All vector geometry features representing entities with explicit spatial representation may either tightly couple the required tabular attributes (see below) with the geometry (e.g. as attributes on a shapefile) or use a relational table structure to store the attributes elsewhere.  In the latter case, every vector geometry feature that is required to have a unique geometric representation must be have a unique ID that relates to only one tabular record.

![SCAT Entities](https://github.com/researchplanninginc/NOAA-SCAT-Standard/blob/master/graphics/SCAT.png?raw=true)

**Figure 2.** Schematic of logical relationships among conceptual entities over time.  Entities with solid outlines are have unique individual spatial representations.  Entities with dashed outlines have spatial extents defined by the spatial representations of other entities.



## Required Spatial Topology

Topology, defined here as the properties of geometric features in two dimensions, is a way to define and explicitly test for properties like adjacency, connectivity, proximity, and coincidence. Certain topological relationships are required by the standard for features with polygonal and linear spatial representations. These relationships are referenced in the descriptions of conceptual entities above. Most importantly, it is required that all linear surface oiling representations (zones) must be coincident with the linear shoreline representation. If any other entities such as subsurface oiling representations, shoreline treatment recommendations, or other entities are represented as linear features, these must also be coincident with the linear shoreline representation. This standard makes reference to spatial relationships described in the DE-9IM model ([Clementini et al., 1993](http://dx.doi.org/10.1007/3-540-56869-7_16); [Egenhoffer and Franzosa, 1991](http://dx.doi.org/10.1080/02693799108927841)) which is implemented in standard GIS software and spatial databases.

The standard requires that these topological relationships exist, but does not have any requirements for how or when these relationships are enforced. For example, raw spatial data (e.g. field collected coordinates) or interim analysis products stored within a GIS or RDBMS software system are not required to comply with these topological rules.  However, the standard does require that topologically compliant data is either: 1.) automatically or regularly generated as part of such software systems and associated data management processes, or 2.) is readily and simply generated when generating data for export or interchange.

The standard requires the following topological relationships:

- All linear features must not self-cross or self-overlap (e.g. must be simple and not complex).
- All linear features must overlap with a linear shoreline.
- Linear features must not cross other linear features of the same type but may overlap other linear features of the same type.
- Linear and polygonal features with multiple parts (e.g. multipart features or collections of features with the same geometry type) are permitted but not required.
- All spatial features must be covered by a polygonal shoreline, intertidal zone, or potentially oiled area if such a feature exists (features may lie exactly on the boundary of a polygonal shoreline, but may not extend beyond)
- Polygonal features may have interior holes, but multipart polygonal features may not have parts contained in interior holes in that feature. These must be represented as separate spatial features.

See figures 3-6 below for illustrative examples. Note that the spatial relationships described here are only required for data transmitted


![Figure 3](https://github.com/researchplanninginc/NOAA-SCAT-Standard/blob/master/graphics/topo_fig1.png?raw=true)

**Figure 3.** Linear features may intersect other linear features at endpoints but may not self-cross, or self-overlap. Linear feature endpoints depicted as dots, whereas feature vertices are not depicted.

![Figure 4](https://github.com/researchplanninginc/NOAA-SCAT-Standard/blob/master/graphics/topo_fig2.png?raw=true)

**Figure 4.** All non-shoreline linear features must overlap linear shoreline features

![Figure 5](https://github.com/researchplanninginc/NOAA-SCAT-Standard/blob/master/graphics/topo_fig3.png?raw=true)

**Figure 5.** All non-shoreline spatial features must be covered by polygonal shoreline features (lie in the interior or along the boundary of the polygonal shoreline feature) if such features exist.

![Figure 6](https://github.com/researchplanninginc/NOAA-SCAT-Standard/blob/master/graphics/topo_fig4.png?raw=true)

**Figure 6.** All polygonal shoreline features may have interior holes, but multipart polygonal features may not have parts contained within interior holes within themselves.

All of these relationships are enforceable and testable in most commercial or open-source vector-based GIS, spatially enabled database software packages, or topology libraries including ArcGIS, Quantum GIS, Oracle Spatial, PostGIS, Java Topology Suite (JTS), and others.

## Required Tabular Attributes

This standard includes a set of core attributes for each conceptual entity represented in a data table. These are listed in the tables below. For entities that require explicit spatial representation, these may be stored in a format that combines spatial and attribute information, or in data tables that are separate from spatial information. NOAA recognizes that each incident presents unique challenges and requirements, so it is anticipated and desirable that this standard may be extended. Data managers and spill response personnel are free to add additional fields to store additional or more specific information, though the field specified in the tables below are mandatory.  Additional codes may be added to the codesets specified below where required to record different or event-specific conditions. This standard requires only that any such changes be included in accompanying documentation or metadata (see the Metadata section below).  Different GIS and database software packages may have different requirements and conventions regarding field naming. As such, the field names included below are intended as suggested field names only. Data managers are free to adopt field names suitable for use in the specific software packages in use during a response. Field names should be fully annotated in accompanying metadata, and compliant with the following criteria:

- Should begin with alphabetical characters.
- Should not include spaces, dashes, or special characters other than underscores.
- Should avoid unmodified words commonly reserved by GIS or RDMS software systems or programming constructs, such as "date", "order", "file", "range", "loop", "by" etc
- Should be limited to 10 characters where possible to meet limitations of the ESRI shapefile format.
- Should be human-readable where possible.



**Table 1.** Required tabular attributes for segments

| **Attribute** | **Description** | **Suggested Field Name** | **Type** | **Codeset or valid values** |
| --- | --- | --- | --- | --- |
| Segment ID | Unique identifier | SEGID | Text | Alphanumeric text string containing identifier sufficient to uniquely identify segment |
| Primary ESI | Primary ESI type of segment | ESI\_PRIM | Text - Codeset | See [NOAA, 2003](http://response.restoration.noaa.gov/sites/default/files/ESI_Guidelines.pdf). |
| Secondary ESI | Secondary ESI types present along segment  | ESI\_SEC  | Text - Codeset  |See [NOAA, 2003](http://response.restoration.noaa.gov/sites/default/files/ESI_Guidelines.pdf). If required, additional fields required to hold additional secondary codes  |
| Backshore type | Boolean indicator of presence of cliff/slope | BACK\_CLIFF | Boolean | T/F |
| Backshore type | Boolean indicator of presence of lowland | BACK\_LOW | Boolean | T/F |
| Backshore type | Boolean indicator of presence of beach | BACK\_BEACH | Boolean | T/F |
| Backshore type | Boolean indicator of presence of Dune | BACK\_DUNE | Boolean | T/F |
| Backshore type | Boolean indicator of presence of wetland | BACK\_WETL | Boolean | T/F |
| Backshore type | Boolean indicator of presence of lagoon | BACK\_LAG | Boolean | T/F |
| Backshore type | Boolean indicator of presence of delta | BACK\_DELTA | Boolean | T/F |
| Backshore type | Boolean indicator of presence of channel | BACK\_CHAN | Boolean | T/F |
| Backshore type | Boolean indicator of presence of manmade | BACK\_MAN | Boolean | T/F |
| Backshore Access | Boolean indicator of presence of access from backshore | ACC\_BACK | Boolean | T/F |
| Alongshore Access | Boolean indicator of presence of alongshore access | ACC\_ALONG | Boolean | T/F |
| Backshore Staging | Boolean indicator of presence of backshore staging areas | STAGE\_BACK | Boolean | T/F |
| Access Description/ Restrictions | Access description | ACC\_DESC | Text | Text description of access and access restrictions |

**Table 2.** Required tabular attributes for Surveys

| **Attribute** | **Description** | **Suggested Field Name** | **Type** | **Codeset or valid values** |
| --- | --- | --- | --- | --- |
| Survey ID | Unique identifier | SURVID | Text | Alphanumeric text string containing identifier sufficient to uniquely identify survey within and across dates |
| Survey Date | Date of start | SURVDATE | Date | Valid date in local time zone |
| Survey Start Time | Time of survey start | START\_TIME | Time | Valid time in local time zone |
| Survey Stop Time | Time of survey end | STOP\_TIME | Time | Valid time in local time zone |
| Tide Height | Primary tide height for period of survey | TIDE\_HGT | Text - Codeset | Codes:<br>L<br>M<br>H |
| Survey By | Personnel conducting survey | SURV\_PER1 | Text | Name and organization of first team member conducting survey. Though not required by standard, this should be pulled from lookup table. Multiple fields required to hold unknown count of multiple values. |
|   |   | SURV\_PER2 | Text | See above. |
|   |   | SURV\_PER3 | Text | See above. |
|   |   | SURV\_PER4 | Text | See above. |
|   |   | SURV\_PER5 | Text | See above. |
|   |   | SURV\_PER6 | Text | See above. |
| Segments | Segment(s) surveyed | SEGMENTS | Text or Lookup Table |   |
| Survey Method | Method used to conduct survey | SURVTYPE | Text - Codeset | Codes:<br>Foot<br>ATV<br>Airboat<br>Boat<br>Helicopter/Aircraft<br>Overlook |



**Table 3.** Required tabular attributes for Surface Oiling Observations (SSOs) or oiling zones

| **Attribute** | **Description** | **Suggested Field Name** | **Type** | **Codeset or valid values** |
| --- | --- | --- | --- | --- |
| Zone ID | Unique identifier | ZONEID | Text | Alphanumeric text string containing identifier sufficient to uniquely identify oiled zone within survey |
| Tidal Zone | Categorical descriptor for average/dominant elevation relative to tidal or other datum | TIDAL\_ZONE | Text - Codeset | Codes:<br>LITZ<br>MITZ<br>UITZ<br>SUTZ<br>L/MITZ<br>M/UITZ<br>U/SITZ<br>L/M/UITZ<br>L/M/U/SITZ |
| Width | Average across-shore width of oiled zone in meters. | WIDTH | Numeric | Floating point values in meters. Zero values permitted only for NO observations. |
| Distribution | Average areal distribution of surface oil as percentage or ratio of substrate of oiled zone or categorical descriptor of same. | OILDIST | Numeric<br>_OR_<br>Text - Codeset | Floating point values as percentage or ratio. Zero values permitted only for NOO observations.  Null values permitted only for observations with discrete oiling counts, unit areas, and sizes. May only be null for NO observations or only for observations with discrete oiling counts, unit areas, and sizes. <br><br>Codes (if codeset used):<br>C<br>B<br>P<br>S<br>T |
| Thickness | Average thickness of surface oil in cm or categorical descriptor of same | OILTHICK | Numeric<br>_OR_<br>Text - Codeset | Floating point values in cm. Zero values permitted only for NO observations.  Null or blank values permitted only for observations with discrete oiling counts, unit areas, and sizes. May only be null or blank for NO observations or only for observations with discrete oiling counts, unit areas, and sizes.<br><br>Codes (if codeset used):<br>TO<br>CV<br>CT<br>ST<br>FL |
| Character | Categorical descriptor of dominant oil character within oiled zone | OILCHAR | Text - Codeset | May only be null or blank only for observations with discrete oiling counts, unit areas, and sizes.<br><br>Codes:<br> FR<br>MS<br>TB<br>PT<br>TC<br>SR<br>AP<br>NO |
| Substrate | Categorical descriptor for location of surface oil (sediment/soil, vegetation canopy, or both) | SUBSTR | Text - Codeset | Null or blank values permitted only for NO observations.<br><br>Codes:<br>S<br>V<br>B |
| Discrete oiling count per unit area | Count per unit area of tarballs or residue balls in oiled zone | TB\_CNT | Numeric | Integer values. Zero values permitted only for NO observations or observations with areal distribution and thickness as above. |
| Discrete oiling count unit area | Unit area of count of tarballs or residue balls in oiled zone | TB\_AREA | Text - Codeset | Null or blank values permitted only for NO observations or observations with areal distribution and thickness as above.<br><br>Codes:<br> M2<br>M<br>100M<br>ZONE |
| Discrete oiling avg. size | Average planimetric diameter in cm of tarballs or residue balls in oiled zone. | TB\_AVSIZE | Numeric | Floating point values in centimeters. Zero, null or blank values permitted only for NO observations or observations with areal distribution and thickness as above. |
| Discrete oiling large size | Largest planimetric diameter in cm of tarballs or residue balls in oiled zone. | TB\_LGSIZE | Numeric | Floating point values in centimeters. Zero, null or blank values permitted only for NO observations or observations with areal distribution and thickness as above. |
| Type of discrete oiling | Dominant categorical descriptor of tarballs, residue balls or other discrete oiling within oiled zone | TB\_TYPE | Text - Codeset | Null or blank values permitted only for NO observations or observations with areal distribution and thickness as above.<br><br>Codes:<br>S<br>W<br>SRB<br> |
| Plant oiling bottom elevation | Average vertical elevation of lowest oiling on plant canopy in cm from sediment surface | P\_OILBOT | Numeric | Floating point values in centimeters. |
| Plant oiling top elevation | Average vertical elevation of highest oiling on plant canopy in cm from sediment substrate | P\_OILTOP | Numeric | Floating point values in centimeters. Zero values only permitted for NO or non-plant oiling observations (Substrate <> P or B). |
| ESI Type | ESI type | ESI | Text - Codeset | See See [NOAA, 2003](http://response.restoration.noaa.gov/sites/default/files/ESI_Guidelines.pdf). |
| Category | Categorical descriptor of relative oiling intensity. | OILCAT | Text - Codeset | Computed. See [NOAA, 2013](http://response.restoration.noaa.gov/sites/default/files/manual_shore_assess_aug2013.pdf). |



**Table 4.** Required tabular attributes for Subsurface Oiling Observations (SSOOs)

| **Attribute** | **Description** | **Suggested Field Name** | **Type** | **Codeset or valid values** |
| --- | --- | --- | --- | --- |
| Pit ID | Unique identifier | PITID | Text | Alphanumeric text string containing identifier sufficient to uniquely identify pit, trench, or core within survey |
| Tidal Zone | Categorical descriptor for average/dominant elevation relative to tidal or other datum | TIDAL\_ZONE | Text - Codeset | Codes:<br>LITZ<br>MITZ<br>UITZ<br>SUTZ<br>L/MITZ<br>M/UIT<br>SU/SITZ<br>L/M/UITZ<br>L/M/U/SITZ |
| Pit depth | Maximum depth of subsurface pit, trench or core in cm below sediment surface. | DEPTH | Numeric | Floating point values in centimeters. No zero values permitted. |
| Oiling top depth | Average depth of the top of observed subsurface oiling in cm below sediment surface. | OIL\_TOP | Numeric | Floating point values in centimeters. Null or blank values only permitted for NO observations. |
| Oiling bottom depth | Average depth of the bottom of observed subsurface oiling in cm below sediment surface. | OIL\_BOT | Numeric | Floating point values in centimeters. Zero, null or blank values permitted only for NO observations. |
| Character | Categorical descriptor of dominant oil character within oiled pit | OILCHAR | Text - Codeset | Null or blank values not permitted.<br><br>Codes:<br>SR<br>SAP<br>OP<br>PP<br>OR<br>OF<br>TR<br>NO |
| Distribution | Average areal distribution of subsurface oil within vertical oil interval as percentage or ratio of surface area in excavated pit, trench, or core or categorical descriptor of same. | OILDIST | Numeric<br>_OR_<br>Text - Codeset | Floating point values as percentage or ratio. Zero values permitted only for NOO observations. <br><br>Codes (if codeset used):<br>C<br>P<br>S<br>T |
| Depth to Water Table | Average depth of the bottom of observed water level in cm below sediment surface | WATER\_DEP | Numeric  | Floating point values in centimeters. |
| Sheen Color | Categorical descriptor of sheen on water table in pit, trench, or core if present | SHEEN | Text - Codeset | Codes:<br>B<br>R<br>S<br>N |
| Clean Below | Boolean indicator of presence of clean sediment below oiled sediment | CLN\_BELOW | Text - Codeset | YN |
| Category | Categorical descriptor of relative oiling intensity in pit | OILCAT | Text - Codeset | Computed. See NOAA, 2013 |



**Table 5.** Required tabular attributes for Shoreline Treatment Recommendations (STRs)

| **Attribute** | **Description** | **Suggested Field Name** | **Type** | **Codeset or valid values** |
| --- | --- | --- | --- | --- |
| STR ID | Unique identifier | STRID | Text | Alphanumeric text string containing identifier sufficient to uniquely identify survey within and across dates |
| Surveys | Survey(s) wherein oiling that required treatment was observed | SURVEYS | Text or Lookup Table | Valid contents for either zones and surveys or segments is required to allow non-explicit spatial description of STR extents.  Alternatively, if STRs are explicitly represented by spatial data, then these attributes may be omitted or blank.   |
| Zones | Zone(s) wherein oiling that required treatment was observed | ZONES | Text or Lookup Table |
| Segments | Segment(s) wherein oiling that required treatment was observed | SEGMENTS | Text or Lookup Table |
| STR Issue Date | Date STR was issued as permit | STR\_ISSUE | Date | Valid date in local time zone |
| STR Completion Date | Date STR was completed | STR\_COMPL | Date | Valid date in local time zone |
| STR Replaced By | Superseding STR | STR\_REPL | Text or lookup table | Either text or lookup table containing or pointing to one or more STR IDs that replaced or superseded if present. |
| Cleanup Recommendations | Recommended cleanup | STR\_CLEANR | Text | Unstructured text |
| Staging / Logistics Constraints | Staging or logistical concerns or waste disposal issues | STR\_STAGE | Text | Unstructured text |
| Ecological Concerns | Ecological concerns for recommended cleanup | STR\_ECOL | Text | Unstructured text |
| Cultural/Historical Concerns | Cultural/Historical concerns for recommended cleanup | STR\_CULT | Text | Unstructured text |
| Safety Concerns | Safety concerns for recommended cleanup | STR\_SFTY | Text | Unstructured text |

## Logical Relationships

In addition to spatial topological rules describing required relationships between spatial features, the standard includes requirements for logical relationships between records in data tables describing the entities involved and records in other data tables and spatial features. The standard has no requirements for how and when these logical relationships are enforced. Relationships may be enforced by rules declared as part of the logical schema of compliant databases, built into the applications that make use of these databases, or checked via Quality Assurance/Quality Control (QAQC) procedures. Briefly, this standard requires:

- All spatial features describing surface oiling representations (zones) or subsurface oiling representations (pits) should have one corresponding record in the data tables containing attributes for those features.
- All tabular records describing surface oiling representations (zones) or subsurface oiling representations (pits) should have one or more corresponding spatial features describing these entities.
- All tabular records describing surface oiling representations (zones) or subsurface oiling representations (pits) should have a parent record in the data table containing information about surveys.
- ll tabular records describing surveys are required to have at least one child record in the data table containing information about surface oiling observations (zones) or subsurface oiling observations.

## Metadata

Documentation sufficient to allow users not participating in data collection or management during a spill event to understand and use SCAT data is a mandatory component of this standard. Metadata is structured information that describes, explains, locates, or otherwise makes it easier to retrieve, use, or manage an information resource  [(NISO, 2004)](http://www.niso.org/publications/press/UnderstandingMetadata.pdf). Because SCAT data have a spatial component by definition, geospatial metadata standards are most appropriate, but any of the following standards is acceptable:

- Federal Geospatial Data Committee (FGDC) Content Standard for Digital Geospatial Metadata ([FGDC, 1998](http://www.fgdc.gov/standards/projects/FGDC-standards-projects/metadata/base-metadata/v2\_0698.pdf))
- ISO 19115 ([ISO, 2014](http://www.iso.org/iso/home/store/catalogue\_ics/catalogue\_detail\_ics.htm?csnumber=53798))
- Project Open Data Metadata Schema v1.1 ([POD, 2015](https://project-open-data.cio.gov/v1.1/schema/))

See references for internet resources specific to each of these standards. Tools enabling rapid and semi-automated creation of compliant metadata, either as stand-alone software or integrated with commercial and open source GIS and database software packages, are widely available. Compliance with a specific metadata standard is encouraged but not mandatory under the SCAT data standard. Regardless of metadata standard applied, documentation sufficient for other users to understand the content, scope, structure, logical relationships, field names and contents, and other important details is required. 

## References

CEDRE, 2006. Surveying Sites Polluted by Oil. An Operational Guide for Conducting an Assessment. Centre de documentation, de recherche et d'experimentations sur les pollutions accidentelles dex eaux, Brest, France, 41 pp. Available online at: [http://wwz.cedre.fr/en/Our-resources/Documentation/Operational-guides/Surveying-Sites](http://wwz.cedre.fr/en/Our-resources/Documentation/Operational-guides/Surveying-Sites)

Clementini, E., P. Di Felice, and P. van Oosterom. 1993. "A small set of formal topological relationships suitable for end-user interaction". In Abel, David; Ooi, Beng Chin. Advances in Spatial Databases: Third International Symposium, SSD '93 Singapore, June 23–25, 1993 Proceedings. Lecture Notes in Computer Science. 692/1993. Springer. pp. 277–295. Available online at: [http://dx.doi.org/10.1007/3-540-56869-7_16](http://dx.doi.org/10.1007/3-540-56869-7_16)

Egenhofer, M.J. and R.D. Franzosa. 1991. Point-set topological spatial relations. International Journal of Geographical Information Systems 5(2):161-174. Available online at: [http://dx.doi.org/10.1080/02693799108927841](http://dx.doi.org/10.1080/02693799108927841)

Federal Geographic Data Committee. FGDC-STD-001-1998. Content standard for digital geospatial metadata (revised June 1998). Federal Geographic Data Committee. Washington, D.C. Available online at: [http://www.fgdc.gov/standards/projects/FGDC-standards-projects/metadata/base-metadata/v2\_0698.pdf](http://www.fgdc.gov/standards/projects/FGDC-standards-projects/metadata/base-metadata/v2\_0698.pdf)

International Standards Organization (ISO). 1998. ISO 8859-1:1998 Information technology - 8-bit single-byte coded graphic character sets - Part 1: Latin alphabet No. 1. International Standards Organization, Geneva, Switzerland. Available online at: [ftp://std.dkuug.dk/JTC1/sc2/wg3/docs/n411.pdf](ftp://std.dkuug.dk/JTC1/sc2/wg3/docs/n411.pdf)

International Standards Organization (ISO). 2014. ISO 19115:2014 Geographic information – Metadata. International Standards Organization, Geneva, Switzerland. Available online at: [http://www.iso.org/iso/home/store/catalogue\_ics/catalogue\_detail\_ics.htm?csnumber=53798](http://www.iso.org/iso/home/store/catalogue\_ics/catalogue\_detail\_ics.htm?csnumber=53798)

Lamarche, A., G.A. Sergy, and E.H. Owens. 2007. Shoreline Cleanup Assessment Technique (SCAT) Data Management Manual, Emergencies Science and Technology Division, Science and Technology Branch, Environment Canada, Ottawa, ON.  Accessible online at: [http://www.shorelinescat.com/Documents/Manuals/Environment%20Canada%202007%20SCAT%20Data%20Management%20Manual.pdf](http://www.shorelinescat.com/Documents/Manuals/Environment%20Canada%202007%20SCAT%20Data%20Management%20Manual.pdf)

MCA, 2007. The UK SCAT Manual. A Field Guide to the Documentation of Oiled Shorelines in the UK. UK Maritime & Coastguard Agency, Southampton, UK. 47 pp. + vi. Accessible online at: [https://www.gov.uk/government/uploads/system/uploads/attachment_data/file/297968/ukscatman.pdf](https://www.gov.uk/government/uploads/system/uploads/attachment_data/file/297968/ukscatman.pdf)

National Oceanic and Atmospheric Administration (NOAA) Office of Response and Restoration. 2013 Shoreline Assessment Manual, 4th Edition. Office of Response and Restoration, National Oceanic and Atmospheric Administration. 73 pp. + appendices.
Accessible online at: [http://response.restoration.noaa.gov/sites/default/files/manual_shore_assess_aug2013.pdf](http://response.restoration.noaa.gov/sites/default/files/manual_shore_assess_aug2013.pdf)

National Oceanic and Atmospheric Administration (NOAA) Office of Response and Restoration. 2002. Environmental Sensitivity Index Guidelines, version 3.0. NOAA Technical Memorandum NOS OR&R 11. Seattle: NOAA, Office of Response and Restoration, Hazardous Materials Response and Assessment Division, 129 p. Accessible online at: [http://response.restoration.noaa.gov/sites/default/files/ESI_Guidelines.pdf](http://response.restoration.noaa.gov/sites/default/files/ESI_Guidelines.pdf)

National Information Standards Organization (NISO). 2004. Understanding Metadata. National Information Standards Organization, Bethesda, MD. Accessible online at: [http://www.niso.org/publications/press/UnderstandingMetadata.pdf](http://www.niso.org/publications/press/UnderstandingMetadata.pdf)

Owens, E.H., and G.A. Sergy. 2000. The SCAT Manual: A Field Guide to the Documentation and Description of Oiled Shorelines. Second Edition. Environment Canada, Edmonton, Alberta, Canada. 108 pages. Accessible online at: [http://www.shorelinescat.com/Documents/Manuals/Environment%20Canada%202000%20SCAT%20Manual%202nd%20Edition/SCAT%20Manual%20Complete.pdf](http://www.shorelinescat.com/Documents/Manuals/Environment%20Canada%202000%20SCAT%20Manual%202nd%20Edition/SCAT%20Manual%20Complete.pdf)

Owens, E.H., and G.A. Sergy. 2004. The Arctic SCAT Manual – A Field Guide to the Documentation and Description of Oiled Shorelines in Arctic Environments. Edmonton, Alberta: Environment Canada. 172 pp. Accessible online at: [http://www.shorelinescat.com/Documents/Manuals/Environment%20Canada%202004%20Arctic%20SCAT.pdf](http://www.shorelinescat.com/Documents/Manuals/Environment%20Canada%202004%20Arctic%20SCAT.pdf)

Project Open Data (POD). 2015. Project Open Data Metadata Schema v1.1. Accessible online at: [https://project-open-data.cio.gov/v1.1/schema/](https://project-open-data.cio.gov/v1.1/schema/)



## Appendix A – Example Shoreline Observation Form

![SCAT Form](https://cloud.githubusercontent.com/assets/6370202/7495807/e4ca6b80-f3d5-11e4-81f4-4375298d2cb4.png?raw=true)

## Appendix B - Data Interchange File Formats and Naming Conventions

To preserve flexibility required for storing data in different formats and manipulating data in different software packages, this standard does not specify explicit file names or formats. It is important however that file names follow a logical and documented naming convention. It is recommended that file names include an explicit date of generation. Further, file names should be compliant with the following criteria:

- Should begin with alphabetical characters.
- Should not include spaces, dashes, or special characters other than underscores.
- Should not include prefix or suffix for data type (e.g. "tbl" for table or "fc" for feature class).

This standard requires that all compliant spatial and associated tabular data must be stored or delivered in a widespread and commonly used commercial format or open-source, cross-platform format. The standard is agnostic regarding data storage and manipulation software, but compliant data must be either implicitly stored in one of the file formats described below (or similar alternative), or be able to be readily and simply converted/exported to a compliant file format to facilitate interchange.

Generally, spatial data should be stored or delivered in one of the following formats:

- ESRI Shapefile (.SHP)
- ESRI File Geodatabase (.GDB)
- ESRI Personal Geodatabase (.MDB)
- GeoJSON/TopoJSON
- Well-Known Text/Well-Known Binary (.WKT, .WKB) 

Tabular data should be stored or delivered in one of the following formats:

- Delimited or comma-separated text (.TXT, .TAB, or .CSV)
- DBase (.DBF)
- Microsoft Access (.MDB)
- Microsoft Excel (.XLS, .XLSX)

File formats such as .AI, .EPS/.PS, .PDF and/or .PSD created from graphics editing applications such as Adobe Illustrator, Adobe Photoshop, Adobe Acrobat or other PDF generating applications or drivers are not acceptable. Similarly, data in the form of file formats such as .DXF or .DWG from Computer Aided Design (CAD) applications are also not compliant with this standard.

Any file format should encode text using the UTF-8 Unicode encoding standard if the internal Unicode encoding is not otherwise specified.
