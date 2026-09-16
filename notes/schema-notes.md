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