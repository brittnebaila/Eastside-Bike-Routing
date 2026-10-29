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

### NE 24th Street elevation profile

Tested an approximately 1.08 km section of NE 24th Street using
the Redmond DEM and QGIS Profile Tool.

- Start elevation: ~43 m
- Maximum elevation: ~57 m
- End elevation: ~42–43 m
- Approximate elevation gain to crest: 14 m
- Approximate distance to crest: 730 m
- Average climbing grade to crest: ~1.9%

Observation:
Using only start and end elevation would make this segment appear
nearly flat. The elevation profile reveals a climb followed by a
descent. Bicycle routing will need to account for elevation changes
within routes and direction of travel.

--------------------------------------

## NE 24th Routing Segment

**Source layer:** Redmond Centerline  
**Street:** NE 24th ST  
**Segment:** 185th PL NE → 186th AVE NE

### Useful Existing Attributes

- Street name
- Street width: 40
- Road classification: coded value 2
- Maximum speed limit: 30
- Surface: coded value 1
- Ownership: RED
- Status: ACT

### Attributes I Would Need to Derive

- `length_m`
- `elevation_gain_m`
- `grade_percent`

### Attributes That May Come From Another Dataset

- Bicycle facility type

### Questions About the Source Data

- What does surface code `1` represent?
- What does classification code `2` represent?
- What units are used for `StreetWidth`?

### Source Attribute Definitions

- `Classification = 2` → Minor Arterial
- `MaxSpeedLimit = 30` → 30 mph
- `CalcLength = 322.4` → segment length in feet
- QGIS measurement → approximately 98 m
- `AssetID = Cntl1681` → unique identifier for this centerline segment
- `surface = 1` → definition still needs verification
- `StreetWidth = 40` → likely feet, but still needs verification

### Length Verification

The selected NE 24th Street segment runs from 185th PL NE to
186th AVE NE.

Redmond's `CalcLength` value is 322.4 feet.

A manual QGIS measurement of the same segment was approximately
98 meters.

322.4 ft × 0.3048 ≈ 98.27 m

This confirms that `CalcLength` represents the segment length in feet.

### Derived Segment Length

Created a new field in the processed Redmond routing dataset:

`length_m`

The source dataset provides segment length in feet through `CalcLength`.

Converted the values to meters using:

`length_m = CalcLength × 0.3048`

For the selected NE 24th Street segment:

- AssetID: `Cntl1681`
- Source length: 322.4 ft
- Derived length: ~98.27 m

The calculation was applied to the full Redmond Centerline dataset rather
than manually calculating individual features.

This demonstrates a basic GIS data-processing workflow:

source attribute → transformation → derived routing attribute

### Derived Segment Length

Created a processed working copy of the Redmond Centerline dataset rather
than modifying the original municipal data.

Added a new field:

`length_m`

Calculated metric segment length using:

`length_m = CalcLength × 0.3048`

For the NE 24th Street test segment:

- AssetID: `Cntl1681`
- Source length: 322.4 ft
- Derived length: ~98.27 m

The calculation was applied to the full Redmond Centerline dataset,
demonstrating how a single transformation can create derived attributes
across thousands of features.


### Testing Elevation Sampling

Selected three connected street segments near NE 24th Street to test an
elevation-to-street workflow before applying it to the full network.

Used **Extract Specific Vertices** to extract the first and last vertices
of the selected street segments.

For three street segments, QGIS created six endpoint records. Some points
overlapped because adjacent street segments share endpoints.

Used **Sample Raster Values** with the Redmond DEM to extract elevation
values at the street-segment endpoints.

This transferred elevation information from the raster DEM into attributes
associated with vector point features.


### Joining Elevation to Street Segments

Used `AssetID` as the common identifier to join sampled endpoint elevations
back to their original street segments.

Created start and end elevation attributes for the three test segments.

Example:

`Cntl1681`

- Length: ~98.27 m
- Start elevation: ~54.75 m
- End elevation: ~57.00 m
- Elevation change: ~+2.25 m


### Calculating Street Grade

Created two derived attributes:

`elev_change_m`

Calculated using:

`end elevation - start elevation`

`grade_pct`

Calculated using:

`(elev_change_m / length_m) × 100`

Results for the three test segments:

| AssetID | Length (m) | Start Elev. (m) | End Elev. (m) | Grade |
|---|---:|---:|---:|---:|
| Cntl254 | 65.62 | 53.88 | 47.57 | -9.62% |
| Cntl1680 | 100.71 | 51.48 | 54.75 | +3.25% |
| Cntl1681 | 98.27 | 54.75 | 57.00 | +2.29% |

Positive and negative grades represent the direction in which the line
geometry is stored. A segment that is uphill in one travel direction is
downhill in the opposite direction.

This will be important when the street network is eventually converted
into routing edges.


### Processed Routing Layer

Saved the completed test workflow as a permanent GeoPackage layer:

`redmond_routing_with_elevation`

The analytical layer was saved using:

`EPSG:26910 — NAD83 / UTM zone 10N`

This provides a meter-based projected coordinate system appropriate for
local spatial analysis.

The current processed routing dataset contains:

- Street geometry
- Municipal street attributes
- `length_m`
- Start elevation
- End elevation
- Elevation change
- Grade percentage

Elevation and grade have currently been calculated for three test segments.
The remaining street segments contain NULL elevation values.

The next step will be to scale the tested elevation workflow across the
full Redmond street network.


### Key GIS Concepts Practiced

- Preserving raw source data and creating processed working datasets
- Converting source measurements into application-ready units
- Extracting vertices from line geometry
- Sampling raster values at vector locations
- Joining spatially derived information using feature identifiers
- Calculating derived terrain attributes
- Understanding directional grade
- Testing a geospatial workflow on a small subset before scaling it
- Using an appropriate projected CRS for local spatial analysis

--------------------------------------
## October 21, 2026 — First Working Leaflet Grade Visualization

### Goal
Move the Redmond street-grade analysis from QGIS into a browser-based web map and use the calculated grade values to control street symbology.

### Preparing the Web Layer
The existing `redmond-21-segment-grades` layer contained the correct grade attributes but used point geometry because it was created from the sampled start endpoints.

To create a web-ready street layer:

- Joined the grade results back to `redmond_routing_with_elevation`
- Used `AssetID` as the join field
- Preserved the original street line geometry
- Copied the calculated grade field into the joined layer
- Limited the output to the 21 analyzed street segments
- Exported the resulting line layer to WGS84 / EPSG:4326 for web mapping
- Saved the working GeoJSON as `web/test-lines.geojson`

This produced 21 street line features containing the calculated grade data.

### Leaflet Prototype
Created the first working Leaflet map in `web/index.html`.

The prototype currently:

- Loads an OpenStreetMap basemap
- Fetches `test-lines.geojson`
- Creates a Leaflet GeoJSON layer
- Automatically zooms to the analyzed street segments
- Reads the calculated grade value for each street
- Styles each segment based on its grade

### Grade Visualization
The prototype currently uses absolute grade so that color represents steepness regardless of the stored direction of the street geometry.

Current prototype categories:

- Green: less than 3%
- Yellow: 3% to less than 6%
- Red: 6% or greater

These categories are being used for visualization and exploration only. They are not intended to represent accessibility, engineering, or safety standards.

### Debugging / Important Finding
The first web map successfully displayed the street geometry, but every segment appeared green.

Browser debugging showed that JavaScript was receiving `null` when requesting:

`grade_pct`

The exported/joined GeoJSON actually stored the calculated values under:

`grade_pct_2`

Because JavaScript converts `null` to `0` when passed through `Math.abs()`, all segments were incorrectly classified as less than 3%.

Updating the Leaflet code to read `grade_pct_2` fixed the issue.

The browser now correctly displays green, yellow, and red street segments according to the calculated grade values.

### Current Data Pipeline
The working pipeline is now:

Municipal street GIS data  
→ DEM elevation data  
→ QGIS endpoint sampling  
→ elevation change  
→ street grade calculation  
→ join results to line geometry  
→ GeoJSON export  
→ JavaScript / Leaflet  
→ interactive browser visualization

### Key Learning
This was the first point in the project where the GIS analysis directly controlled the behavior of the web application.

The colors displayed in Leaflet are not manually assigned. JavaScript reads the grade attribute from each geographic feature and determines its style dynamically.

The 21-segment dataset is serving as a small test area to validate the full GIS-to-web workflow before scaling the analysis to a larger street network.

### Next Steps
- Commit the working Leaflet grade visualization
- Add clickable street segments with grade and length information
- Add a grade legend
- Bring Redmond bicycle-facility data into the web map
- Improve grade analysis by sampling elevation along street segments rather than relying only on endpoints
- Scale beyond the 21-segment test dataset
- Introduce PostGIS and spatial SQL
- Begin route comparison logic
- Later rebuild the terrain experience using ArcGIS Maps SDK for JavaScript SceneView
- Finish with UI and portfolio-case-study polish

--------------------------------------

--------------------------------------

## October 29, 2026 — Leaflet Interactive Map Improvements

### Completed
- Added clickable popups to the 21 analyzed Redmond street segments using Leaflet's `onEachFeature` and `bindPopup()`.
- Popups display street grade percentage (`grade_pct_2`) and segment length in meters (`length_m`).
- Added a map legend explaining the three grade categories:
  - Green: Under 3% — Gentle
  - Yellow: 3–6% — Moderate
  - Red: 6%+ — Steeper
- Preserved existing dynamic street styling and automatic map zoom.
- Tested the updated map successfully using a local Python HTTP server.

### Technical Notes
- Grade calculations currently use start and end elevations from QGIS.
- Grade colors use the absolute value of the calculated grade.
- The current dataset contains 21 street segments.
- The legend categories are prototype classifications, not official cycling safety ratings.

### Next Steps
- Inspect the complete Redmond Centerline dataset.
- Verify citywide DEM coverage and coordinate systems.
- Develop an automated workflow to sample elevations along street geometries.
- Calculate more representative grade metrics before expanding to the full network.