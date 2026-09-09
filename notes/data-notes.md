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

