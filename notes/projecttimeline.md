**Eastside Bike Routing Project**
# Six-Week Development Timeline

**Project Objective**

The goal of the Eastside Bike Routing project is to explore how public GIS data can be combined with software engineering to provide better bicycle route information. The project will focus on factors such as elevation and grade, trail or road surface, bicycle infrastructure, and rider comfort.

The project will begin with Bellevue data for GIS training and transition to City of Redmond data as the primary data source as development progresses.

**Week 1: QGIS Foundations**

# Focus: Learn the fundamentals of working with GIS data in QGIS.

## Tasks:
Import municipal GIS data into QGIS.
Understand vector layers and geographic features.
Explore attribute tables.
Practice manually selecting features.
Use expressions to query attributes.
Practice spatial selection.
Learn basic GIS terminology.
Understand coordinate reference systems (CRS).
Practice basic layer styling and visualization.

Current Dataset: City of Bellevue Trails

Deliverable:
A functioning QGIS project containing Bellevue trail data with documented observations and examples of GIS queries and selections.

**Week 2: City of Redmond GIS Data**

# Focus: Transition from the Bellevue learning dataset to Redmond data.

Tasks:

Explore City of Redmond GIS and open-data resources.
Locate available trail and bicycle infrastructure datasets.
Investigate road and transportation data.
Import useful Redmond datasets into QGIS.
Examine the attributes provided by each dataset.
Identify information that is missing.
Document the data sources and their potential uses.

Deliverable:
A Redmond GIS data inventory and QGIS project containing useful bicycle-routing layers.

**Week 3: Elevation and Route Characteristics**

# Focus: Begin adding information that can distinguish an easy or comfortable bicycle route from simply the shortest route.

Tasks:

Locate an appropriate elevation dataset.
Learn the difference between raster and vector GIS data.
Work with a Digital Elevation Model (DEM).
Explore slope and elevation analysis.
Investigate how grade can be associated with road or trail segments.
Research available trail and road surface information.
Begin identifying characteristics that affect bicycle suitability.

Deliverable:
A GIS map combining the Redmond bicycle/trail network with elevation or grade information.

**Week 4: QGIS to Web GIS**

# Focus: Connect GIS analysis with software engineering and web development.

Tasks:

Prepare and clean GIS data for web use.
Export selected GIS data to GeoJSON.
Learn how GIS attributes are represented in GeoJSON.
Load Redmond GIS data into Leaflet.
Display trail and bicycle infrastructure on an interactive web map.
Add basic interaction with geographic features.
Connect GIS attributes to information displayed in the application.

Deliverable:
An interactive web map displaying Redmond bicycle and trail data.

**Week 5: Spatial Data and Routing Logic**

# Focus: Begin developing the logic that could eventually recommend bicycle routes.

Tasks:

Learn introductory spatial SQL concepts.
Begin working with PostGIS.
Explore spatial queries.
Determine which characteristics should influence bicycle route recommendations.
Use cyclist research to help determine important routing factors.
Experiment with a bicycle suitability or comfort score.
Consider factors such as distance, grade, infrastructure, surface, and rider comfort.

Deliverable:
A preliminary bicycle route suitability/scoring model using real GIS data.

**Week 6: Route Comparison Prototype**

# Focus: Combine the previous work into a portfolio-ready prototype.

Tasks:

Select a test origin and destination.
Compare two or more possible bicycle routes.
Calculate or display relevant route characteristics.
Compare distance and elevation/grade.
Include bicycle infrastructure and surface information when available.
Explain why one route may be preferable even if it is longer.
Improve the web-map interface.
Clean up project documentation and GitHub repository.
Document limitations and potential future improvements.

Deliverable:
A working Eastside Bike Routing prototype that demonstrates how GIS data can support bicycle route recommendations beyond simply choosing the shortest route.

**Ongoing Throughout the Six Weeks**

GitHub

Commit work after each project session.
Use descriptive commit messages.
Maintain project notes and README documentation.
Keep raw or unnecessary large datasets out of the repository when appropriate.

User Research

Develop a short questionnaire for local cyclists.
Ask riders what influences their route decisions.
Identify common concerns involving hills, traffic, surfaces, trails, intersections, and safety.
Use findings to inform the routing model.

Portfolio Documentation

Document decisions, challenges, and solutions throughout development.
Explain why specific datasets were selected.
Clearly distinguish between GIS analysis and software-development components.
Maintain screenshots or examples showing project progression.
Six-Week Target

At the end of six weeks, the project should demonstrate a simple but meaningful question:

Can public GIS data help a cyclist choose a route that may be slightly longer but is flatter, safer, better surfaced, or more comfortable to ride?

The prototype does not need to replace a full navigation application. Its purpose is to demonstrate the combination of GIS analysis, spatial data, software engineering, and user-centered problem solving in a real-world transportation project.