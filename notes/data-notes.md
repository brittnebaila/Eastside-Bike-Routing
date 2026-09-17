# Eastside Bike Routing — Data Notes

## City of Bellevue Trails

**Source:** City of Bellevue Open Data

### Available Attributes
- SiteNbr
- Trail ID
- System Name
- System creation/change metadata

### Potentially Useful Attributes
- Trail ID
- System Name
- SiteNbr

### Missing Information Needed for Bike Routing
- Surface type
- Elevation / grade
- Bicycle suitability
- Trail width
- Permitted uses

### Initial Observations
The dataset provides trail geometry, but it does not appear to contain
enough information by itself to determine whether a trail is appropriate
for bicycle routing.

--------------------------------------

## QGIS Selection Practice

### Selecting Features
I practiced selecting individual trail features directly on the map. 
Selecting a feature highlights its geometry on the map and also selects 
the corresponding record in the attribute table.

### Selecting by Expression
I used Select by Expression to query the `SystemName` field.

**Expression used:**

`"SystemName" = 'BBG'`

**Result:** 98 of the 1,399 trail features were selected.

The yellow lines on the map were QGIS highlighting the selected features. 
They were not a new layer or new trail data. Clearing the selection removed 
the yellow highlighting without changing the original Trails layer.

### What I Learned
- A GIS feature connects geographic geometry with attribute data.
- I can select features manually on the map or query them using their attributes.
- A selection does not change or create data; it identifies a subset of the existing layer.
- `SystemName` contains abbreviated values such as BBG, CMRWP, HP, and KL.
- I do not yet know what all of these codes mean, so I should not use them in routing logic until I understand the dataset documentation.

--------------------------------------

## QGIS Categorized Symbology

I categorized the Trails layer using the `SystemName` attribute.

QGIS identified:
- 13 unique `SystemName` values
- 71 features with a missing `SystemName` value

Categorized symbology changes how features are displayed based on their
attribute values without modifying the underlying data.

### Data Quality Observation
Some trail features contain geometry but are missing a `SystemName`.
This is important because missing attribute values may need to be handled
when the data is later used for analysis or routing.

--------------------------------------

## Coordinate Reference Systems (CRS)

The Trails layer and my QGIS project both use:

**EPSG:3857 — WGS 84 / Pseudo-Mercator**

I temporarily changed the project CRS to **EPSG:4326 — WGS 84** to see how a different coordinate system affects the map.

### What I Learned
- A layer CRS describes how a dataset's coordinates are stored and interpreted.
- The project CRS determines how QGIS displays layers together.
- QGIS can reproject layers on the fly without changing the original data.
- Changing from EPSG:3857 to EPSG:4326 made the map appear wider, even though the trail locations did not change.
- EPSG:4326 uses longitude and latitude, while EPSG:3857 is commonly used for web-map display.
- CRS becomes especially important when combining datasets from different sources or performing spatial analysis.

--------------------------------------

## QGIS Layer Filtering

I practiced filtering the Trails layer using the following expression:

`"SystemName" = 'BBG'`

The filter returned 98 features. The attribute table showed 98 total
features, 98 filtered features, and 0 selected features.

### What I Learned
- Selecting and filtering are different operations in QGIS.
- A selection highlights features but keeps the entire dataset available.
- A filter temporarily limits the layer to features that meet a condition.
- Filtering does not delete features from the original dataset.
- The same expression can be used for different purposes depending on the
  QGIS tool being used.

  --------------------------------------

## Redmond GIS Data Discovery

### Dataset 1: Trails

**Source:** City of Redmond GIS

**Geometry:** Line

**Potentially Useful Attributes:**
- `d_TrailNam` — trail name
- `d_TrailCla` — trail classification
- `d_SurfaceT` — surface type
- `d_TrailSta` — trail status
- `d_Ped` — pedestrian-related attribute
- `d_Bicycle` — bicycle-related attribute
- `d_Owner` — trail owner
- `d_Manager` — trail manager

### Initial Data Exploration

`d_SurfaceT` contains five unique coded values:
- PVD
- SFT
- STR
- UNK
- WTR

`d_Bicycle` contains three unique coded values:
- 0
- 1
- 9

The meanings of these codes still need to be verified using City of Redmond
metadata or domain documentation before they are used in analysis.

### Routing Value

This dataset appears useful for bicycle routing because it contains trail
geometry along with attributes describing surface type, trail classification,
status, and bicycle use. These attributes could eventually help distinguish
between route segments rather than treating every trail as equally suitable
for cycling.

### Dataset 2: Street Centerline

**Source:** City of Redmond GIS

**Geometry:** Line

**Potentially Useful Attributes:**
- `StreetName` — street name
- `FromStreet` / `ToStreet` — segment location/connectivity information
- `StreetWidt` — street width
- `d_Classifi` — street classification
- `d_Status` — street status
- `surface` — surface-related attribute
- `MaxSpeedLi` — maximum speed limit

### Initial Data Exploration

`MaxSpeedLi` contains six unique values:

- 0
- 25
- 30
- 35
- 40
- 45

The values from 25–45 appear to represent posted speed limits based on the
field name. The meaning of `0` should be verified before the field is used
in analysis.

### Routing Value

The Street Centerline dataset appears useful because it provides the street
network along with characteristics such as street classification, width,
surface, and maximum speed limit.

These attributes could eventually be combined with trail and elevation data
to evaluate bicycle route segments based on more than distance alone.

--------------------------------------

## Redmond Elevation and Slope Analysis

### Elevation Data

I downloaded two USGS 3DEP 1-meter DEM tiles covering my initial Redmond
study area.

The DEM data uses:

- CRS: EPSG:26910 — NAD83 / UTM Zone 10N
- Horizontal units: meters
- Pixel resolution: 1 meter
- Data type: Float32

One inspected DEM tile had elevation values ranging from approximately
5 meters to 168 meters.

### Combining Elevation Tiles

I used QGIS Build Virtual Raster to combine the two DEM tiles into:

`redmond-dem.vrt`

A virtual raster allows QGIS to work with multiple source raster files as
one elevation surface without creating another full copy of the original
data.

### Slope Analysis

I used the combined DEM to calculate a new raster:

`redmond-slope-percent.tif`

Slope was calculated as percent grade rather than degrees because percent
grade is more directly useful for bicycle route analysis.

The resulting slope raster had:

- Minimum slope: 0%
- Maximum slope: approximately 80.68%
- Mean slope: approximately 6.17%

The very high maximum values represent steep terrain or localized terrain
features and should not be interpreted as the grade of a bicycle route.

### Slope Visualization

I experimented with Singleband Pseudocolor symbology and focused the display
on slopes from 0–15%.

I created exploratory slope classes around:

- 0–3%
- 3–5%
- 5–8%
- 8–12%
- 12–15%

The 1-meter slope raster is extremely detailed and visually noisy. This
demonstrated that terrain slope alone is not the same as bicycle route grade.

### What I Learned

A DEM represents elevation as raster cells, while the Redmond trails,
streets, and bicycle facilities are vector features.

Calculating slope from the DEM describes the terrain across the entire study
area. For bicycle routing, the next step is to connect elevation information
to actual road and trail segments.

This will eventually allow route segments to include characteristics such as
surface type, bicycle facility type, speed limit, average grade, and maximum
grade.