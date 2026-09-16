# Eastside Bike Routing — Schema Notes

This document tracks GIS attributes that may be useful to the
Eastside Bike Routing application.

--------------------------------------

## Redmond Trails

### Candidate Routing Fields

| Field | Possible Application Use |
|---|---|
| `d_TrailNam` | Identify/name trail segments |
| `d_TrailCla` | Distinguish trail classifications |
| `d_SurfaceT` | Evaluate trail surface |
| `d_TrailSta` | Determine trail status |
| `d_Bicycle` | Determine bicycle-related access/use |

**Still needs investigation:** Coded values must be decoded before these
fields are used in routing logic.

--------------------------------------

## Redmond Street Centerline

### Candidate Routing Fields

| Field | Possible Application Use |
|---|---|
| `StreetName` | Identify street segments |
| `StreetWidt` | Describe street width |
| `d_Classifi` | Distinguish street classifications |
| `surface` | Evaluate street surface |
| `MaxSpeedLi` | Represent posted speed limit |

**Still needs investigation:** Values such as `MaxSpeedLi = 0` and coded
classification/surface values need to be understood before use.

--------------------------------------

## Redmond Trail Coded Values

The City of Redmond GIS service contains coded-value domains that explain
several abbreviated values in the downloaded shapefile.

### Surface Type (`d_SurfaceT`)

| Code | Meaning |
|---|---|
| PVD | Paved |
| SFT | Soft |
| STR | Stairs |
| UNK | Needs verification |
| WTR | Needs verification |

### Bicycle (`d_Bicycle`)

| Code | Meaning |
|---|---|
| 0 | No |
| 1 | Yes |
| 9 | Unknown |

The downloaded shapefile contains the codes but does not preserve the
human-readable domain definitions visible in Redmond's GIS service.

### Application Relevance

These domains could eventually be translated into application-friendly
values before routing analysis. Bicycle access can determine whether a
trail segment should be considered for a bike route, while surface type
could influence route suitability or rider preference.

--------------------------------------

## Redmond Bicycle Facility

The Bicycle Facility layer provides information about existing and planned
bicycle infrastructure on the left and right sides of roadway segments.

### Existing Facility Domain

| Code | Facility |
|---|---|
| 0 | No On-Street Facility |
| 1 | Bike Lane |
| 2 | Sharrow |
| 5 | Cycle Track |
| 6 | Bike Boulevard |
| 7 | Unknown |
| 8 | No Current Roadway |
| 9 | Shared-Use Path |
| 10 | Shoulder |

The fields `d_Existing_L` and `d_Existing_R` represent existing bicycle
facilities on each side of a segment.

A QGIS expression selecting segments with an existing bike lane on either
side returned 360 features:

`"d_Existing_L" = 1 OR "d_Existing_R" = 1`

QGIS displays human-readable domain labels such as "Bike Lane," while the
underlying GIS service stores coded values such as `1`.

### Routing Value

This layer could help distinguish bicycle routes based on the type of
infrastructure available. Existing and planned facilities should remain
separate so that routing recommendations only use infrastructure that
currently exists.