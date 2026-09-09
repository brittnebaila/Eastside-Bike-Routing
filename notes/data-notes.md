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