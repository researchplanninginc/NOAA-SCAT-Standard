  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  <span id="purpose" class="anchor"><span id="shoreline-cleanup-assessment-technique-s" class="anchor"></span></span>![](media/image1.jpeg)   Shoreline Cleanup Assessment Technique (SCAT) Digital Data Management Standard – Draft
  -----------------------------------------------------------------------------------------------------------------------------------------   ======================================================================================
                                                                                                                                              
                                                                                                                                              **6/2017**
  ------------------------------------------------------------------------------------------------------------------------------------------- ----------------------------------------------------------------------------------------
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

1. Purpose
----------

This document describes standards for the storage and management of
observational Shoreline Cleanup Assessment Technique (SCAT) data
collected by field survey teams during oil spills and similar incidents
to evaluate shoreline conditions and oiling, recommend and guide
treatment, and document compliance with cleanup endpoints. The standard
includes guidelines for

The volume of data collected and developed during oil spill response is
growing at an ever increasing rate. This places a substantial burden on
the response to be able to rapidly digest and interpret those data to
inform operational decision making. This growth in the data management
workload has been facilitated by the rapid evolution of electronic field
data collection tools, data storage systems and common operational
displays. Absent a common vision for how these systems will work
together, these tools will be unable to provide a pathway to distill
these data and translate them into operationally meaningful information.

This standard was developed by the National Oceanic and Atmospheric
Administration (NOAA) Office of Response and Restoration (OR&R),
Emergency Response Division (ERD). While there are a variety of SCAT or
similar protocols and processes that exist ([CEDRE,
2006](http://wwz.cedre.fr/en/Our-resources/Documentation/Operational-guides/Surveying-Sites);
[MCA,
2007](https://www.gov.uk/government/uploads/system/uploads/attachment_data/file/297968/ukscatman.pdf);
[Owens and Sergy,
2000](http://www.shorelinescat.com/Documents/Manuals/Environment%20Canada%202000%20SCAT%20Manual%202nd%20Edition/SCAT%20Manual%20Complete.pdf);
[Owens and Sergy
2004](http://www.shorelinescat.com/Documents/Manuals/Environment%20Canada%202004%20Arctic%20SCAT.pdf)),
this standard is intended to support the storage and manipulation of
data to support the SCAT process as described in the NOAA Shoreline
Assessment Manual ([NOAA,
2013](http://response.restoration.noaa.gov/sites/default/files/manual_shore_assess_aug2013.pdf)).
This standard is provided to the response community as a common point of
reference in the development of electronic field data collection tools,
databases and information products for SCAT activities. This is a
voluntary standard that will be maintained and updated by NOAA based on
input from the response community and the evolution of new technologies.

The data standard proposed here includes:

1.  Recommended Quality Assurance/Quality Control (QAQC) and workflow
    terminology and steps

2.  A conceptual data model, consisting of a set of proposed entities
    and relationships,

3.  4.  Rules for spatial representation of these entities, and r

5.  equired spatial relationships between entities,

6.  7.  8.  Data interchange file formats and data structures, and

9.  Minimum documentation requirements.

10. 

This proposed data standard does not include mandatory logical data
model (a set of explicitly required normalized tables, attributes, and
relationships) for use in Geographic Information (GIS) or Relational
Database Management System (RDBMS) software, though it does suggest
these via higher-level concepts. The spatial and attribute data required
by the standard are not intended as the entirety of a fully articulated
logical data model or database structure. It is expected that databases,
applications, or other tools that are used to maintain data compliant
with this standard will each have design requirements that require a
specific logical model, or a more complex or normalized database
structure. In short, the standard is a *standard for a data model*, not
a database, database design, or a spatial data storage model.

The standard *does,* however, require the ability of any databases,
applications, or other tools used to actively manage SCAT data to export
the core tabular and spatial entities in one of a few specific formats
using a fixed data structure.

In addition, the standard is intended to support data management for
SCAT carried out for the simplest spill that would require management of
digital SCAT data. Data managers may need to extend the standard (and
associated logical schema or data model) to include additional
conceptual entities (e.g. shoreline cleanup status categories), spatial
features, tables, or attributes required for a more complex incident, or
adapt to incident-specific requirements. Lastly this standard does not
address all the tasks required as part of SCAT data management (see
[Lamarche et al.,
2007](http://www.shorelinescat.com/Documents/Manuals/Environment%20Canada%202007%20SCAT%20Data%20Management%20Manual.pdf);
[NOAA,
2013](http://response.restoration.noaa.gov/sites/default/files/manual_shore_assess_aug2013.pdf)).
This standard only describes the required components for formal
structured data that are collected by full SCAT teams. Data collected by
pre-spill surveys, reconnaissance, field photography, special surveys,
or to support administrative status tracking are all generally managed
by SCAT data management teams, but these data can be highly
spill-specific and are not within the scope of this standard.

<span id="conceptual-data-model" class="anchor"></span>

3. Conceptual Data Model {#conceptual-data-model-1}
------------------------

The standard includes a few core conceptual entities, described below,
including shorelines, segments, surveys, surface oil observations (SOO),
subsurface oil observations (SSOO) and shoreline treatment
recommendations (STRs) (Figure 1). These entities describe general
classes of data collected and managed by SCAT.

![](media/image2.png)

**Figure** **1.** Schematic of spatial relationships among conceptual
entities over time showing a shoreline partitioned into segments. SOOs
from a survey on Dates 1 and 2 are depicted as blue and red lines
coincident with the shoreline for No Oiling Observed and Oiled SOOs
respectively. SSOOs from Date 2 are depicted as red and blue points in
the vicinity of the shoreline for No Oiling Observed and Oiled SOOs
respectively. The extent of an STR on Date 3 is depicted as a green line
coincident with the shoreline.

#### Shoreline Representation

Shorelines are intertidal, fluvial, or lacustrine environments where the
land-water interface often changes in position and extent over both long
and short time-scales. In order to accurately compare SCAT field data
from multiple surveys at a single location it is necessary to reference
these observations using a single digital shoreline representation.
Shorelines representations are fixed extents of shoreline habitat that
are largely spatially unchanging over the timeframe of an incident.
These may be derived from existing spatial data before a spill occurs or
it may be necessary to generate the Shoreline Representation after an
incident has occurred. Shorelines are typically represented as a
one-dimensional digital vector line, but may be represented as polygons
(complex wetlands or floodplains) or, rarely, points. If a spill event
persists for long enough, shoreline representations may move or change
in morphology over that time span.

#### Segments

Shoreline segments are relatively fixed, spatially unchanging subsets of
a shoreline representation that are used operationally during a spill
response to reference specific portions of a shoreline. These may be
predefined before surveys take place, or even before a spill occurs;
however, they can also be determined in the field by SCAT teams as they
conduct initial surveys. Optimally, segments have consistent geomorphic,
physical, and administrative characteristics and are fixed in space. If
a spill event persists for long enough, segments may move or change in
morphology either as a function of change in their parent shoreline
representation or within/along an unchanged parent shoreline
representation for operational or administrative reasons. Segments are
unique and non-overlapping in space at a given point in time. A segment
must be a child element of a shoreline representation.

#### Surveys

A survey is a time-specific assessment of the oiling conditions along
some subset of a shoreline representation. Surveys may or may not cover
the entire length of one or more specific segments. Surveys may describe
shoreline surveyed by SCAT teams on foot or observed remotely from
vessels or aircraft, and do not necessarily represent areas physically
occupied by SCAT teams. Surface and subsurface oiling observations made
by field teams on a specific survey are child elements of that survey. A
survey has no spatial extent beyond those child elements and is thus
defined by the aggregate of the spatial extents of those child elements.
Surveys may overlap in space and time. Surveys are associated with
structured data such as the date, time and location of the survey as
well as a list of the SCAT team members and a formalized generic
description of the survey area (see Table 2 below and sections 1-5 of
the Shoreline Oil Summary form in [Appendix
A](https://github.com/researchplanninginc/NOAA-SCAT-Standard/blob/master/Draft%20SCAT%20Data%20Standard.md#appendix-a--example-shoreline-observation-form)).

#### Surface Oiling Observation (SOO)

SOOs (commonly termed oiling zones, where no observed oil [NOO] is a
type of oiling zone) are survey and time-specific representations of
consistent observed surface oiling and other shoreline characteristics.
SOOs are commonly referenced by start and end points (collected as GPS
way points) of the oiling zone along with a description of the oiling
characteristics using the SCAT methodology. These start-stop points are
matched to the Shoreline Representation discussed above to comply with
the topological requirements described in the following sections. This
feature matching may be done at the time of data collection or via
post-processing. Structured data associated with SOOs contain an
across-shore width scalar value and a tidal elevation, but all SOOs that
overlap along-shore are typically referenced as separate linear features
that are all coincident with the shoreline. In some circumstances it may
be necessary to represent SOOs as polygonal features (e.g. complex
wetlands or floodplains) or points. Unless this is required to support
unique operational considerations, however, it is recommended that SOOs
be represented as linear features along a linear shoreline
representation. SOOs may potentially overlap in space (different tidal
zones along the same shoreline) and time. See Table 3 below and sections
6 of the Shoreline Oil Summary form in [Appendix
A](https://github.com/researchplanninginc/NOAA-SCAT-Standard/blob/master/Draft%20SCAT%20Data%20Standard.md#appendix-a--example-shoreline-observation-form)
for structured data associated with SOOs.

#### Subsurface Oiling Observation (SSOO)

SSOOs are survey and time-specific representations of observed
subsurface oiling and other shoreline characteristics. SSOOs are
generally explicitly referenced with a single zero-dimensional point
together with one or more scalar depth values where oiling was
investigated in the field by excavation of a pit, trench, or core. As
with SOOs, SSOOs may occasionally be referenced as polygons or lines but
this is not done in practice unless dictated by operational
requirements. SSOOs may potentially overlap in space and time – though
generally this will not occur if represented by zero-dimensional points.
All SSOOs must be a child element of a survey. See Table 4 below and
sections 7 of the Shoreline Oil Summary form in [Appendix
A](https://github.com/researchplanninginc/NOAA-SCAT-Standard/blob/master/Draft%20SCAT%20Data%20Standard.md#appendix-a--example-shoreline-observation-form)
for structured data associated with SOOs.

#### Shoreline Treatment Recommendations (STR)

STRs are time-period-specific recommended cleanup actions
prescribed/permitted for a given location. This location can either be
defined by a spatial entity (e.g., a linear or polygonal feature)
specific to the STR, or by referencing the spatial geometry of other
entities. For example, the location of an STR could be the extent of a
specific SSO or set of SSOs from a specific survey, or the entirety of a
certain segment or segments.

3. Recommended QAQC and Workflow Terminology
--------------------------------------------

It is helpful to have a common framework for describing the typical
workflow, processing steps, and Quality Assurance/Quality Control (QAQC)
procedures that commonly take place during the active collection and
management of SCAT data. As such, the standard introduces a common set
of terminology and best practices for field data collection.

The standard identifies the first phase of workflow as the field survey
component. During this phase, field staff are in the field collecting
data electronically or via analog methods, or reviewing the collected
data internally prior to submitting the survey data. During this phase,
the survey data are considered to have a QAQC status of *incomplete*.
After the field personnel have reviewed the data they have collected in
the field, electronic or analog, and submitted to data management staff,
then the survey data are considered to have a QAQC status of
*provisional*, and the survey data ingestion phase of the data
management workflow begins. Note that if data are being collected via
any electronic data collection system, the data may be actually housed
in a centralized location on a commercial cloud, or response specific
server during or immediately after collection, but are not considered as
complete provisional data until review by field staff. Information
products generated as part of this workflow phase vary by response, but
include only items related to field survey effort and status such as the
number of teams in the field and/or reported back, and general survey
areas.

During the survey data ingestion phase of workflow, data are initially
entered into a digital data management system if collected via analog
methods. If entered digitally, an optional transcription verification
QAQC check may take place during this phase of the workflow. Survey data
are then reviewed by a SCAT data manager for survey consistency, wherein
survey data are checked for completeness and logical consistency.
Logical consistency refers to contradictions between individual data
elements within survey data. For example, a zone wherein the categorical
descriptor of the dominant oil character was recorded as “no oil” but
where oil distribution was recorded as a non-zero value. After this QAQC
check, the data are checked for accuracy by the SCAT Coordinator.
Generally this check involves reviewing the collected survey data to
ensure standardized descriptive terms are being used, correct
methodology is being employed, observations of quantitative elements are
calibrated among teams, etc. After these checks, then the field survey
data are considered to have a QAQC status of *approved* and are made
available to other users within the response, and enter the
post-processing phase of the workflow. Prior to approval of field survey
data, information products generated as part of this workflow phase are
typically only metrics related to QAQC status of data in the data
ingestion pipeline.

After field survey data are approved, then the approved field data
themselves are the primary information product.

In many cases, provisional field survey data are used during the data
ingestion workflow phase to begin Shoreline Treatment Recommendation
(STR) development workflow phase. This phase may take place in parallel,
or partially overlapping the data ingestion phase subject to the
requirements of the response, and the prevailing operational tempo.
Typically, STR preparation begins immediately after field survey data
are complete and still provisional with close consultation between field
staff and SCAT coordinator. However, STR preparation and approval within
the wider response often takes some time, and will not be completed
after field survey data are approved. The primary information products
of this workflow phase is the STR itself.

The post-processing phase of the workflow involves the additional
processing of approved SCAT field survey data for a variety of
response-specific data management needs and tasks. Often, this will
involve linear referencing (or, “snapping”) of field collected spatial
data to a common reference shoreline, or other data manipulation and
analysis tasks. Primary information products generated during this
workflow phase vary by response, but typically include maximum precedent
or current oiling spatial data, map, or tabular summary products.
Typically, SCAT field staff, data managers and coordinators jointly
conduct report QAQC checks during this phase to ensure that information
products accurately reflect actual field conditions as described by the
approved survey data.

A schematic of these recommended SCAT data collection workflow phases
and associated QAQC statuses, checkpoints, and information products is
included in Figure 2. Note that during a response with a typical
operational tempo, SCAT field survey data collected on different days,
as well as STRs, will be in all of these workflow phases simultaneously.

![](media/image3.png)
---------------------

**Figure 2.** Schematic of recommended SCAT data collection workflow
phases and associated QAQC statuses, checkpoints, and information
products.

4. Required Spatial Data and Relationships
------------------------------------------

Specific conceptual entities must have explicit and unique spatial
representation as independent vector geometry for use and analysis in
GIS software or web mapping applications. At minimum, these include:

-   Shoreline Representation

-   Segments

-   Surface Oiling Observations (SOOs or oiling zones)

-   Subsurface Oiling Observations (SSOOs or pits)

Other conceptual entities are also required to have spatial
representations, but these do not necessarily have to be stored
explicitly as independent vector geometry. Instead, they may be stored
as lists or lookup tables into other entities that do have explicit
geometry. These entities include:

-   Surveys

-   Shoreline Treatment Recommendations

Figure 3 is a schematic of entities and their required spatial
relationships over time. Surveys are required to have spatial extents
consisting only of their children surface and subsurface shoreline
observations. STRs may have spatial extents defined by one or more SOOs
or SSOOs, one or more segments, or some other portion of a shoreline
representation, or some other spatial extent. If an STR may be uniquely
defined by reference to other entities, then it can be spatially
represented by a non-spatial list of these other features. If an STR has
a spatial extent that cannot be uniquely defined by one or more SOOs,
SSOOs, or segments, then it must be represented by explicit vector
geometry.

-   -   -   -   

-   -   -   -   

<!-- -->

-   -   

![](media/image4.png)

**Figure** **3.** Schematic of logical relationships among conceptual
entities over time. Entities with solid outlines are have unique
individual spatial representations. Entities with dashed outlines have
spatial extents defined by the spatial representations of other
entities.

#### Required Spatial Topology

In addition to logical relationships between entities described above,
the standard also includes rules describing required relationships
between spatial features. These are made explicit using the concept of
topology. Topology, defined here as the properties of geometric features
in two dimensions, is a way to define and explicitly test for properties
like adjacency, connectivity, proximity, and coincidence. Certain
topological relationships are required by the standard for features with
polygonal and linear spatial representations. These relationships are
referenced in the descriptions of conceptual entities above. Most
importantly, it is required that all linear surface oiling
representations (zones) must be coincident with the linear shoreline
representation. If any other entities such as subsurface oiling
representations, shoreline treatment recommendations, or other entities
are represented as linear features, these must also be coincident with
the linear shoreline representation. This standard makes reference to
spatial relationships described in the DE-9IM model (Clementini et al.,
1993; [Egenhoffer and Franzosa,
1991](http://dx.doi.org/10.1080/02693799108927841)) which is implemented
in standard GIS software and spatial databases.

The standard requires that these topological relationships exist, but
does not have any requirements for how or when these relationships are
enforced. For example, raw spatial data (e.g. field collected
coordinates) or interim analysis products stored within a GIS or RDBMS
software system are not required to comply with these topological rules.
However, the standard does require that topologically compliant data is
either: 1.) automatically or regularly generated as part of such
software systems and associated data management processes, or 2.) is
readily and simply generated when generating data for export or
interchange. For example, a survey team might record the location of a
linear SOO (zone) using a GPS device that records points that are not
coincident with the shoreline representation. Storage of these raw
coordinate data is acceptable and encouraged. To generate data compliant
with this standard, however, these raw coordinates must be made
topologically correct by "snapping" these coordinates to the shoreline
representation and generating linear features that comply with the rules
below.

The standard requires the following topological relationships:

-   All linear features must not self-cross or self-overlap (e.g. must
    be simple and not complex).

-   All linear features must overlap with a linear shoreline if the
    relevant shoreline is represented linearly and not as a polygon.

-   Linear features must not cross other linear features of the same
    type but may overlap other linear features of the same type.

-   Linear and polygonal features with multiple parts (e.g. multipart
    features or collections of features with the same geometry type) are
    permitted but not required.

-   All spatial features must be covered by a polygonal shoreline,
    intertidal zone, or potentially oiled area if such a feature exists
    (features may lie exactly on the boundary of a polygonal shoreline,
    but may not extend beyond)

-   Polygonal features may have interior holes, but multipart polygonal
    features may not have parts contained in interior holes in that
    feature. These "islands" must be represented as separate spatial
    features.

See figures 4-7 below for illustrative examples.

![](media/image5.png)

**Figure** **4.** Linear features may intersect other linear features at
endpoints but may not self-cross, or self-overlap. Linear feature
endpoints depicted as dots, whereas feature vertices are not depicted.

![](media/image6.png)

**Figure** **5.** All non-shoreline linear features must overlap linear
shoreline features

![](media/image7.png)

**Figure** **6.** All non-shoreline spatial features must be covered by
polygonal shoreline features (lie in the interior or along the boundary
of the polygonal shoreline feature) if such features exist.

![](media/image8.png)

**Figure** **7.** All polygonal shoreline features may have interior
holes, but multipart polygonal features may not have parts contained
within interior holes (i.e., cannot have an "island" within a hole).

All of these relationships are enforceable and testable in most
commercial or open-source vector-based GIS, spatially enabled database
software packages, or topology libraries including ArcGIS, Quantum GIS,
Oracle Spatial, PostGIS, Java Topology Suite (JTS), and others.

5. Required Tabular Attributes and Logical Relationships
--------------------------------------------------------

This standard includes a set of core attributes for each conceptual
entity represented in a data table. These are listed in the tables
below. For entities that require explicit spatial representation, these
may be stored in a format that combines spatial and attribute
information, or in data tables that are separate from spatial
information. NOAA recognizes that each incident presents unique
challenges and requirements, so it is anticipated and desirable that
this standard may be extended. Data managers and spill response
personnel are free to add additional fields to store additional or more
specific information, though the field specified in the tables below are
mandatory. Additional codes may be added to the codesets specified below
where required to record different or event-specific conditions. This
standard requires only that any such changes be included in accompanying
documentation or metadata (see the Metadata section below). Different
GIS and database software packages may have different requirements and
conventions regarding field naming. As such, the field names included
below are intended as suggested field names only. Data managers are free
to adopt field names suitable for use in the specific software packages
in use during a response. Field names should be fully annotated in
accompanying metadata, and compliant with the following criteria:

-   Should begin with alphabetical characters.

-   Should not include spaces, dashes, or special characters other than
    underscores.

-   Should avoid unmodified words commonly reserved by GIS or RDMS
    software systems or programming constructs, such as "date", "order",
    "file", "range", "loop", "by" etc. For example, "date" is
    unacceptable as a field name, but "obs\_date" is acceptable.

-   Should be limited to 10 characters where possible to meet
    limitations of the ESRI shapefile format.

-   Should be human-readable where possible.

Note that certain attributes of surveys, Surface Oiling Observations
(SSOs) or oiling zones, and Subsurface Oiling Observations (SSOOs) are
always required to be collected in the field at the time of survey,
while other attributes may be assigned after the fact, or
programmatically by data collection or storage software. These
attributes are indicated in a separate column for the relevant
conceptual entities in the tables below. Raw or field collected data
consisting of hardcopy or scanned forms or electronically collected SCAT
field data in any format must include this subset of tabular attributes
for these conceptual entities to be compliant with this standard.

**\
**

**Table 1.** Required tabular attributes for segments. No segment
related data is required to be collected in the field, though this is
possible and permitted.

  **Attribute**     **Description**                                        **Suggested Field Name**   **Type**         **Codeset or valid values**
  ----------------- ------------------------------------------------------ -------------------------- ---------------- --------------------------------------------------------------------------------------------------------------------------
  Segment ID        Unique identifier                                      SEG\_ID                    Text             Alphanumeric text string containing identifier sufficient to uniquely identify segment
  Start date        Beginning date of applicability of shoreline segment   START\_DATE                Date             Valid date in local time zone
  End date          Ending date of applicability of shoreline segment      STOP\_DATE                 Date             Valid date in local time zone
  Start Latitude    Latitude of beginning of linear segment                START\_LAT                 Numeric          Floating point values in decimal degrees.
  Start Longitude   Longitude of beginning of linear segment               START\_LON                 Numeric          Floating point values in decimal degrees.
  End Latitude      Latitude of end of linear segment                      END\_LAT                   Numeric          Floating point values in decimal degrees. Null values permitted only for segments represented as a single point.
  End Longitude     Longitude of end of linear segment                     END\_LON                   Numeric          Floating point values in decimal degrees. Null values permitted only for segments represented as a single point.
  Primary ESI       Primary ESI type of segment                            ESI\_PRIM                  Text - Codeset   Estuarine, Riverine, or Lacustrine Environmental Sensitivity Index (ESI) shoreline classification. See NOAA, 2002; 2013.
                                                                                                                       
                                                                                                                       
                                                                                                                       
                                                                                                                       
                                                                                                                       
                                                                                                                       
                                                                                                                       
                                                                                                                       
                                                                                                                       
                                                                                                                       
                                                                                                                       
                                                                                                                       
                                                                                                                       
                                                                                                                       

**Table 2.** Required tabular attributes for Surveys. Attributes
required to be collected in the field via form or electronic data
collection indicated (“Field Req.”).

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Attribute**       **Field** **Req.**   **Description**                 **Suggested Field Name**   **Type**               **Codeset or valid values**
  ------------------- -------------------- ------------------------------- -------------------------- ---------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Survey ID           No                   Unique identifier               SURV\_ID                   Text                   Alphanumeric text string containing identifier sufficient to uniquely identify survey within and across dates

  Survey Date         Yes                  Date of survey                  SURV\_DATE                 Date                   Valid date in local time zone

  Survey Start Time   Yes                  Time of survey start            START\_TIME                Time                   Valid time in local time zone

  Survey Stop Time    Yes                  Time of survey end              STOP\_TIME                 Time                   Valid time in local time zone

                                                                                                                             

  Survey By           Yes                  Personnel conducting survey     SURV\_PER1                 Text                   Name and organization of first team member conducting survey. Though not required by standard, this should be pulled from lookup table. Multiple fields required to hold unknown count of multiple values.

  Survey By           Yes                                                  SURV\_PER2                 Text                   See above.

  Survey By           Yes                                                  SURV\_PER3                 Text                   See above.

  Survey By           Yes                                                  SURV\_PER4                 Text                   See above.

  Survey By           Yes                                                  SURV\_PER5                 Text                   See above.

  Survey By           Yes                                                  SURV\_PER6                 Text                   See above.

  Segments            No                   Segment(s) surveyed             SEGMENTS                   Text or Lookup Table   

  Survey Method       Yes                  Method used to conduct survey   SURV\_TYPE                 Text - Codeset         Codes:
                                                                                                                             
                                                                                                                             Foot; ATV; Airboat; Boat; Helicopter/Aircraft; Overlook; UAS; Dog
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Table 3.** Required tabular attributes for Surface Oiling Observations
(SSOs) or oiling zones. Attributes required to be collected in the field
via form or electronic data collection indicated (“Field Req.”).

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Attribute**                         **Field** **Req.**   **Description**                                                                                                                 **Suggested Field Name**   **Type**                      **Codeset or valid values**
  ------------------------------------- -------------------- ------------------------------------------------------------------------------------------------------------------------------- -------------------------- ----------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Zone ID                               No                   Unique identifier                                                                                                               ZONE\_ID                   Text                          Alphanumeric text string containing identifier sufficient to uniquely identify oiled zone within survey

  Tidal Zone                            Yes                  Categorical descriptor for average/dominant elevation relative to tidal or other datum                                          TIDAL\_ZONE                Text - Codeset                Codes:
                                                                                                                                                                                                                                                      
                                                                                                                                                                                                                                                      LI; MI; UI; SU; LI/MI; MI/UI; UI/SU; LI/MI/UI; LI/MI/UI/SU

  Start Latitude                        Yes                  Latitude of beginning of linear zone                                                                                            START\_LAT                 Numeric                       Floating point values in decimal degrees.

  Start Longitude                       Yes                  Longitude of beginning of linear zone                                                                                           START\_LON                 Numeric                       Floating point values in decimal degrees.

  End Latitude                          Yes                  Latitude of end of linear zone                                                                                                  END\_LAT                   Numeric                       Floating point values in decimal degrees. Null values permitted only for observations represented as a single point.

  End Longitude                         Yes                  Longitude of end of linear zone                                                                                                 END\_LON                   Numeric                       Floating point values in decimal degrees. Null values permitted only for observations represented as a single point.

  Width                                 Yes                  Average across-shore width of oiled zone in meters                                                                              WIDTH                      Numeric                       Floating point values in meters. Zero values permitted only for NO observations.

  Distribution                          Yes                  Average areal distribution of surface oil as percentage or ratio of substrate of oiled zone or categorical descriptor of same   OIL\_DIST                  Numeric *OR* Text - Codeset   Floating point values as percentage or ratio. Zero values permitted only for NOO observations. Null values permitted only for observations with discrete oiling counts, unit areas, and sizes. May only be null for NO observations or only for observations with discrete oiling counts, unit areas, and sizes.
                                                                                                                                                                                                                                                      
                                                                                                                                                                                                                                                      Codes (if codeset used):
                                                                                                                                                                                                                                                      
                                                                                                                                                                                                                                                      C; B; P; S; T

  Thickness                             Yes                  Average thickness of surface oil in cm or categorical descriptor of same                                                        OIL\_THICK                 Numeric *OR* Text - Codeset   Floating point values in cm. Zero values permitted only for NO observations. Null or blank values permitted only for observations with discrete oiling counts, unit areas, and sizes. May only be null or blank for NO observations or only for observations with discrete oiling counts, unit areas, and sizes.
                                                                                                                                                                                                                                                      
                                                                                                                                                                                                                                                      Codes (if codeset used):
                                                                                                                                                                                                                                                      
                                                                                                                                                                                                                                                      TO; CV; CT; ST; FL

  Character                             Yes                  Categorical descriptor of dominant oil character within oiled zone                                                              OIL\_CHAR                  Text - Codeset                May only be null or blank only for observations with discrete oiling counts, unit areas, and sizes.
                                                                                                                                                                                                                                                      
                                                                                                                                                                                                                                                      Codes:
                                                                                                                                                                                                                                                      
                                                                                                                                                                                                                                                      FR; MS; TB; PT; TC; SR; AP; NO

  Substrate                             Yes                  Categorical descriptor for location of surface oil (sediment/soil, vegetation canopy, or both)                                  SUBSTR                     Text - Codeset                Null or blank values permitted only for NO observations.
                                                                                                                                                                                                                                                      
                                                                                                                                                                                                                                                      Codes:
                                                                                                                                                                                                                                                      
                                                                                                                                                                                                                                                      S;V;B

  Discrete oiling count per unit area   Yes                  Count per unit area of tarballs or residue balls in oiled zone                                                                  TB\_CNT                    Numeric                       Integer values. Zero values permitted only for NO observations or observations with areal distribution and thickness as above.

  Discrete oiling count unit area       Yes                  Area of count of tarballs or residue balls in oiled zone                                                                        TB\_AREA                   Numeric                       Floating point values. Zero, null or blank values permitted only for NO observations or observations with areal distribution and thickness as above.

  Discrete oiling count unit area       Yes                  Units area of count of tarballs or residue balls in oiled zone                                                                  TB\_ARUNIT                 Text - Codeset                Null or blank values permitted only for NO observations or observations with areal distribution and thickness as above.
                                                                                                                                                                                                                                                      
                                                                                                                                                                                                                                                      Codes:
                                                                                                                                                                                                                                                      
                                                                                                                                                                                                                                                      M2; M100; M; ZONE

  Discrete oiling avg. size             Yes                  Average planimetric diameter in cm of tarballs or residue balls in oiled zone.                                                  TB\_AVSIZE                 Numeric                       Floating point values in centimeters. Zero, null or blank values permitted only for NO observations or observations with areal distribution and thickness as above.

  Discrete oiling large size            Yes                  Largest planimetric diameter in cm of tarballs or residue balls in oiled zone.                                                  TB\_LGSIZE                 Numeric                       Floating point values in centimeters. Zero, null or blank values permitted only for NO observations or observations with areal distribution and thickness as above.

  Type of discrete oiling               Yes                  Dominant categorical descriptor of tarballs, residue balls or other discrete oiling within oiled zone                           TB\_TYPE                   Text - Codeset                Null or blank values permitted only for NO observations or observations with areal distribution and thickness as above.
                                                                                                                                                                                                                                                      
                                                                                                                                                                                                                                                      Codes:
                                                                                                                                                                                                                                                      
                                                                                                                                                                                                                                                      F; E; S; W; R; O

  Plant oiling bottom elevation         Yes                  Average vertical elevation of lowest oiling on plant canopy in cm from sediment surface                                         P\_OILBOT                  Numeric                       Floating point values in centimeters.

  Plant oiling top elevation            Yes                  Average vertical elevation of highest oiling on plant canopy in cm from sediment substrate                                      P\_OILTOP                  Numeric                       Floating point values in centimeters. Zero values only permitted for NO or non-plant oiling observations (Substrate \<\> P or B).

  Plant height                          Yes                  Average height of plant canopy in cm from sediment surface                                                                      P\_HEIGHT                  Numeric                       Floating point values in centimeters. Zero values only permitted for NO or non-plant oiling observations (Substrate \<\> P or B).

  ESI Type                              Yes                  ESI type                                                                                                                        ESI                        Text - Codeset                Estuarine, Riverine, or Lacustrine Environmental Sensitivity Index (ESI) shoreline classification. See NOAA, 2002; 2013.

  Category                              No                   Categorical descriptor of relative oiling intensity.                                                                            OIL\_CAT                   Text - Codeset                Computed. See [NOAA, 2013](http://response.restoration.noaa.gov/sites/default/files/manual_shore_assess_aug2013.pdf).
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Table 4.** Required tabular attributes for Subsurface Oiling
Observations (SSOOs). Attributes required to be collected in the field
via form or electronic data collection indicated.

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Attribute**          **Field Req’d**   **Description**                                                                                                                                                                         **Suggested Field Name**   **Type**                      **Codeset or valid values**
  ---------------------- ----------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- -------------------------- ----------------------------- -------------------------------------------------------------------------------------------------------------------
  Pit ID                 No                Unique identifier                                                                                                                                                                       PIT\_ID                    Text                          Alphanumeric text string containing identifier sufficient to uniquely identify pit, trench, or core within survey

  Pit Latitude           Yes               Latitude of pit                                                                                                                                                                         PIT\_LAT                   Numeric                       Floating point values in decimal degrees.

  Pit Longitude          Yes               Longitude of pit                                                                                                                                                                        PIT\_LON                   Numeric                       Floating point values in decimal degrees.

  Tidal Zone             Yes               Categorical descriptor for average/dominant elevation relative to tidal or other datum                                                                                                  TIDAL\_ZONE                Text - Codeset                Codes:
                                                                                                                                                                                                                                                                                            
                                                                                                                                                                                                                                                                                            LITZ; MITZ; UITZ; SUTZ

  Pit depth              Yes               Maximum depth of subsurface pit, trench or core in cm below sediment surface.                                                                                                           DEPTH                      Numeric                       Floating point values in centimeters. No zero values permitted.

  Oiling top depth       Yes               Average depth of the top of observed subsurface oiling in cm below sediment surface.                                                                                                    OIL\_TOP                   Numeric                       Floating point values in centimeters. Null or blank values only permitted for NO observations.

  Oiling bottom depth    Yes               Average depth of the bottom of observed subsurface oiling in cm below sediment surface.                                                                                                 OIL\_BOT                   Numeric                       Floating point values in centimeters. Zero, null or blank values permitted only for NO observations.

  Character              Yes               Categorical descriptor of dominant oil character within oiled pit                                                                                                                       OIL\_CHAR                  Text - Codeset                Null or blank values not permitted.
                                                                                                                                                                                                                                                                                            
                                                                                                                                                                                                                                                                                            Codes:
                                                                                                                                                                                                                                                                                            
                                                                                                                                                                                                                                                                                            SR; SAP; OP; PP; OR; OF; TR; NO

  Distribution           Yes               Average areal distribution of subsurface oil within vertical oil interval as percentage or ratio of surface area in excavated pit, trench, or core or categorical descriptor of same.   OIL\_DIST                  Numeric *OR* Text - Codeset   Floating point values as percentage or ratio. Zero values permitted only for NOO observations.
                                                                                                                                                                                                                                                                                            
                                                                                                                                                                                                                                                                                            Codes (if codeset used):
                                                                                                                                                                                                                                                                                            
                                                                                                                                                                                                                                                                                            C; B; P; S; T

  Depth to Water Table   Yes               Average depth of the bottom of observed water level in cm below sediment surface                                                                                                        WATER\_DEP                 Numeric                       Floating point values in centimeters.

  Sheen Color            Yes               Categorical descriptor of sheen on water table in pit, trench, or core if present                                                                                                       SHEEN                      Text - Codeset                Codes:
                                                                                                                                                                                                                                                                                            
                                                                                                                                                                                                                                                                                            B; R; S; N

  Clean Below            Yes               Boolean indicator of presence of clean sediment below oiled sediment                                                                                                                    CLN\_BELOW                 Boolean                       T/F

  Category               No                Categorical descriptor of relative oiling intensity in pit                                                                                                                              OIL\_CAT                   Text - Codeset                Computed. See NOAA, 2013.
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Logical Relationships
---------------------

The standard includes requirements for logical relationships between
records in data tables describing the entities involved and records in
other data tables and spatial features. The standard has no requirements
for how and when these logical relationships are enforced. Relationships
may be enforced by rules declared as part of the logical schema of
compliant databases, built into the applications that make use of these
databases, or checked via Quality Assurance/Quality Control (QAQC)
procedures. Briefly, this standard requires:

-   All spatial features describing surface oiling representations
    (zones) or subsurface oiling representations (pits) should have one
    corresponding record in the data tables containing attributes for
    those features.

-   All tabular records describing surface oiling representations
    (zones) or subsurface oiling representations (pits) should have one
    or more corresponding spatial features describing these entities.

-   All tabular records describing surface oiling representations
    (zones) or subsurface oiling representations (pits) should have a
    parent record in the data table containing information about the
    survey in which the given observation was made.

-   All tabular records describing surveys are required to have at least
    one child record in the data table containing information about
    surface oiling observations (zones) or subsurface oiling
    observations made in that survey.

**Table 5.** Required tabular attributes for Shoreline Treatment
Recommendations (STRs). No STR related data is required to be collected
in the field, though this is possible and permitted.

  **Attribute**         **Description**                 **Suggested Field Name**   **Type**               **Codeset or valid values**
  --------------------- ------------------------------- -------------------------- ---------------------- -------------------------------------------------------------------------------------------------------------------
  STR ID                Unique identifier               STR\_ID                    Text                   Alphanumeric text string containing identifier sufficient to uniquely identify survey within and across dates
                                                                                                          
                                                                                                          
                                                                                                          
  STR Issue Date        Date STR was issued as permit   STR\_ISSUE                 Date                   Valid date in local time zone
  STR Completion Date   Date STR was completed          STR\_COMPL                 Date                   Valid date in local time zone
  STR Replaced By       Superseding STR                 STR\_REPL                  Text or lookup table   Either text or lookup table containing or pointing to one or more STR IDs that replaced or superseded if present.
                                                                                                          
                                                                                                          
                                                                                                          
                                                                                                          
                                                                                                          

6. Data Interchange File Formats and Naming Conventions
-------------------------------------------------------

This standard requires that all compliant spatial and associated tabular
data, regardless of file formats and structures used to store or
manipulate his data, must be made available in a limited set of
widespread and commonly used commercial, or open-source, cross-platform
formats. Compliant data must be able to be readily and simply
converted/exported to one of these compliant file format to facilitate
interchange.

To preserve flexibility required for storing data in different formats
and manipulating data in different software packages, this standard does
not specify explicit file names or formats. It is important however that
file names follow a logical and documented naming convention. It is
recommended that file names include an explicit date of generation.
Further, file names should be compliant with the following criteria:

-   Should begin with alphabetical characters.

-   Should not include spaces, dashes, or special characters other than
    underscores.

Standard compliant data should made available as multiple ESRI shapefile
(.SHP) and comma-separated text (.CSV) files. All spatial data should be
included as features in shapefiles. Tabular data, if stored separately
from spatial features, should be should made available as one or more
CSV files. Alternatively, all spatial and tabular data may be made
available as a single ESRI File Geodatabase (.GDB) as individual feature
classes and tables. Each conceptual entity (e.g. segments, zones, etc.)
should be stored in a unique shapefile or feature class. If the same
type of conceptual entity is represented by geometries of different
dimensions (e.g. zones stored as both linear and polygonal features)
then a separate unique shapefile or feature class for each geometry type
should be included.

File formats such as .AI, .EPS/.PS, .PDF and/or .PSD created from
graphics editing applications such as Adobe Illustrator, Adobe
Photoshop, Adobe Acrobat or other image generating applications or
drivers are not acceptable. Similarly, data in file formats such as .DXF
or .DWG from Computer Aided Design (CAD) applications are also not
compliant with this standard. Text should be encoded using the UTF-8
Unicode encoding standard if the internal Unicode encoding is not
otherwise specified.

Note that templates for standard-compliant data interchange files in
ESRI shapefile (.SHP), comma-separated text (.CSV) files, and ESRI File
Geodatabase format for each conceptual entity accompany this document.

7. 
---

Metadata
--------

Documentation sufficient to allow users not participating in data
collection or management during a spill event to understand and use SCAT
data is a mandatory component of this standard. Metadata is structured
information that describes, explains, locates, or otherwise makes it
easier to retrieve, use, or manage an information resource [(NISO,
2004)](http://www.niso.org/publications/press/UnderstandingMetadata.pdf).
Because SCAT data have a spatial component by definition, geospatial
metadata standards are most appropriate, but any of the following
standards is acceptable:

-   -   Federal Geospatial Data Committee (FGDC) Content Standard for
    Digital Geospatial Metadata ([FGDC,
    1998](http://www.fgdc.gov/standards/projects/FGDC-standards-projects/metadata/base-metadata/v2_0698.pdf))

-   -   Project Open Data Metadata Schema v1.1 ([POD,
    2015](https://project-open-data.cio.gov/v1.1/schema/))

See references for internet resources specific to each of these
standards. Tools enabling rapid and semi-automated creation of compliant
metadata, either as stand-alone software or integrated with commercial
and open source GIS and database software packages, are widely
available. Compliance with a specific metadata standard is encouraged
but not mandatory under the SCAT data standard. Regardless of the
metadata standard applied, documentation sufficient for other users to
understand the content, scope, structure, logical relationships, field
names and contents, and other important details is required.<span
id="references" class="anchor"></span>

8. References {#references-1}
-------------

CEDRE, 2006. Surveying Sites Polluted by Oil. An Operational Guide for
Conducting an Assessment. Centre de documentation, de recherche et
d'experimentations sur les pollutions accidentelles dex eaux, Brest,
France, 41 pp. Available online at:
<http://wwz.cedre.fr/en/Our-resources/Documentation/Operational-guides/Surveying-Sites>

Clementini, E., P. Di Felice, and P. van Oosterom. 1993. "A small set of
formal topological relationships suitable for end-user interaction". In
Abel, David; Ooi, Beng Chin. Advances in Spatial Databases: Third
International Symposium, SSD '93 Singapore, June 23–25, 1993
Proceedings. Lecture Notes in Computer Science. 692/1993. Springer. pp.
277–295. Available online at:
<http://dx.doi.org/10.1007/3-540-56869-7_16>

Egenhofer, M.J. and R.D. Franzosa. 1991. Point-set topological spatial
relations. International Journal of Geographical Information Systems
5(2):161-174. Available online at:
<http://dx.doi.org/10.1080/02693799108927841>

Federal Geographic Data Committee. FGDC-STD-001-1998. Content standard
for digital geospatial metadata (revised June 1998). Federal Geographic
Data Committee. Washington, D.C. Available online at:
<http://www.fgdc.gov/standards/projects/FGDC-standards-projects/metadata/base-metadata/v2_0698.pdf>

International Standards Organization (ISO). 1998. ISO 8859-1:1998
Information technology - 8-bit single-byte coded graphic character
sets - Part 1: Latin alphabet No. 1. International Standards
Organization, Geneva, Switzerland. Available online at:
<ftp://std.dkuug.dk/JTC1/sc2/wg3/docs/n411.pdf>

International Standards Organization (ISO). 2014. ISO 19115:2014
Geographic information – Metadata. International Standards Organization,
Geneva, Switzerland. Available online at:
<http://www.iso.org/iso/home/store/catalogue_ics/catalogue_detail_ics.htm?csnumber=53798>

Lamarche, A., G.A. Sergy, and E.H. Owens. 2007. Shoreline Cleanup
Assessment Technique (SCAT) Data Management Manual, Emergencies Science
and Technology Division, Science and Technology Branch, Environment
Canada, Ottawa, ON. Accessible online at:
<http://www.shorelinescat.com/Documents/Manuals/Environment%20Canada%202007%20SCAT%20Data%20Management%20Manual.pdf>

MCA, 2007. The UK SCAT Manual. A Field Guide to the Documentation of
Oiled Shorelines in the UK. UK Maritime & Coastguard Agency,
Southampton, UK. 47 pp. + vi. Accessible online at:
<https://www.gov.uk/government/uploads/system/uploads/attachment_data/file/297968/ukscatman.pdf>

National Oceanic and Atmospheric Administration (NOAA) Office of
Response and Restoration. 2013 Shoreline Assessment Manual, 4th Edition.
Office of Response and Restoration, National Oceanic and Atmospheric
Administration. 73 pp. + appendices. Accessible online at:
<http://response.restoration.noaa.gov/sites/default/files/manual_shore_assess_aug2013.pdf>

National Oceanic and Atmospheric Administration (NOAA) Office of
Response and Restoration. 2002. Environmental Sensitivity Index
Guidelines, version 3.0. NOAA Technical Memorandum NOS OR&R 11. Seattle:
NOAA, Office of Response and Restoration, Hazardous Materials Response
and Assessment Division, 129 p. Accessible online at:
<http://response.restoration.noaa.gov/sites/default/files/ESI_Guidelines.pdf>

National Information Standards Organization (NISO). 2004. Understanding
Metadata. National Information Standards Organization, Bethesda, MD.
Accessible online at:
<http://www.niso.org/publications/press/UnderstandingMetadata.pdf>

Owens, E.H., and G.A. Sergy. 2000. The SCAT Manual: A Field Guide to the
Documentation and Description of Oiled Shorelines. Second Edition.
Environment Canada, Edmonton, Alberta, Canada. 108 pages. Accessible
online at:
<http://www.shorelinescat.com/Documents/Manuals/Environment%20Canada%202000%20SCAT%20Manual%202nd%20Edition/SCAT%20Manual%20Complete.pdf>

Owens, E.H., and G.A. Sergy. 2004. The Arctic SCAT Manual – A Field
Guide to the Documentation and Description of Oiled Shorelines in Arctic
Environments. Edmonton, Alberta: Environment Canada. 172 pp. Accessible
online at:
<http://www.shorelinescat.com/Documents/Manuals/Environment%20Canada%202004%20Arctic%20SCAT.pdf>

Project Open Data (POD). 2015. Project Open Data Metadata Schema v1.1.
Accessible online at: <https://project-open-data.cio.gov/v1.1/schema/>

<span id="appendix-a-example-shoreline-observation"
class="anchor"></span>

Appendix A – Example Shoreline Observation Form
-----------------------------------------------

Note that this form, by design, assumes that the user is surveying a
single SCAT segment. This practice is *not* required by this data
standard, though it is permitted.

![](media/image9.png)

<span id="appendix-b---data-interchange-file-forma"
class="anchor"></span>

-   -   -   

<!-- -->

-   -   -   -   -   

<!-- -->

-   -   -   -   
