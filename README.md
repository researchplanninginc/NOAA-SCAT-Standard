# NOAA SCAT Data Standard

<img src="https://cloud.githubusercontent.com/assets/6370202/7496276/df14f7ca-f3d8-11e4-8086-d51a3754dff4.jpg" width="150">

Version 0.2.12.2017

December 2017

This repository contains a proposed data managment standard for observational Shoreline Cleanup Assessment Technique (SCAT) data collected by field survey teams during oil spills and similar incidents to evaluate shoreline oiling, recommend and guide treatment, and document compliance with cleanup endpoints. This draft standard was developed by the National Oceanic and Atmospheric Administration (NOAA) Office of Response and Restoration (OR&R), Emergency Response Division (ERD). This standard is provided to the response community as a common point of reference in the development of electronic field data collection tools, databases and information products for SCAT activities. This is a voluntary standard that will be maintained and updated by NOAA based on input from the response community and the evolution of new technologies.

The draft data standard proposed here includes:

- Recommended Quality Assurance/Quality Control (QAQC) and workflow terminology and steps
- A conceptual data model, consisting of a set of proposed entities and relationships,
- Required core tabular attributes describing these entities,
- Rules for spatial representation of these entities, and required spatial relationships between entities,
- Data interchange file formats and data structures, and
- Minimum documentation requirements.

Currently, this repository contains a draft document in Microsoft Word (.docx) format describing the proposed standard. The markdown version is currently being used for version tracking and collaborative editing. In the future, template spatial and tabular data structures will be deposited here.

##Version Change History


0.2.12.2017
======================
- changed water level field to be more generic (e.g. riverine or non-tidal water level fluctuations)
- changed ESI type to shoreline type to be more generic (e.g. ice/snow shoreline types)
- added appendix on reccommended shoreline type and water level codes and uses
- added GEO/JSON to list of acceptable data interchange file formats
- included synthetic demonstration data in all acceptable file formats 

0.1.10.2017
======================
- added explicit foreign key fields for zones and pits
- changed field names to be unique across tables

0.0.8.2017
======================
- editorial changes to text

0.0.7.2017
======================
- editorial changes to text

0.0.6.2017
======================
- added QAQC languange and reorganized document
- removed non-essential segment fields (backshore character, access, etc.)
- rmoved non-essential STR fields
- removed tide height requirment for surveys
- added specific required formats for data interchange files (SHP/CSV and FGDB)
- added lacustrine and riverine ESI scales to list of acceptable codesets for ESI Type
- added UAS and dog to survey types

0.0.5.2017
======================
- changed title to "data managment standard" to reflect inclusion of QAQC steps etc.
- added plant height overall
- added explicit lat/lon or start-stop lat/lon to pit, zone, and segments
- added start stop date of applicability to segments to track shoreline change over time.
- editorial changes to text
