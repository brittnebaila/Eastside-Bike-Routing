# Eastside Bike Routing 🚲🗺️

A civic GIS + software engineering project exploring how bicycle routing can account for more than distance and travel time.

The project uses municipal open GIS data, bicycle and trail infrastructure, elevation, and spatial analysis to explore routes that may be safer, more comfortable, and more useful for real riders on the Eastside of the Seattle metropolitan area.

## Current Focus

- Building GIS workflows in QGIS
- Working with City of Redmond and Bellevue open GIS data
- Exploring bicycle facilities, trails, and street networks
- Processing USGS elevation data
- Analyzing terrain slope and elevation profiles
- Documenting reproducible GIS workflows with Git and GitHub

## What I'm Exploring

Traditional routing can recommend a technically bikeable route without accounting for what that route actually feels like to ride.

This project explores factors such as:

- Elevation and grade
- Bicycle infrastructure
- Trail and road surface
- Route comfort and accessibility
- Cyclist preferences and experience

## Analysis Highlights

Early spatial analysis on Redmond's bicycle network, built from municipal open data and USGS 1-meter elevation data:

![Slope classification of Redmond bicycle network segments](notes/screenshots/redmond-slope-classification.png)
*Slope classification of bicycle network segments — the terrain input behind cyclist-centered route scoring.*

![Elevation profile along the NE 24th corridor](notes/screenshots/ne24th-elevation-profile.png)
*Elevation profile for a sample corridor, showing what a "bikeable" route actually feels like to ride.*

## Planned Development

### GIS & Spatial Analysis
- Extract grade information for bicycle network segments
- Combine infrastructure, surface, and elevation attributes
- Develop a cyclist-centered route scoring approach

### Web GIS
- Build an interactive prototype map, starting with Leaflet
- Display route characteristics and elevation information
- Compare alternative routes visually
- Level up: rebuild the terrain view with the ArcGIS Maps SDK for JavaScript (SceneView) for 3D slope and elevation visualization

### Spatial Data & Routing
- Introduce PostgreSQL/PostGIS
- Practice spatial SQL
- Build a routable bicycle network
- Compare routes using cyclist-relevant costs

## Project Vision: A City Worth Exploring

Eastside Bike Routing aims to transform traditional bicycle route planning into an inviting, interactive geographic experience for families.

Inspired by illustrated atlases, cozy exploration games, and three-dimensional terrain maps, the project combines geospatial engineering with playful, accessible design.

Rather than simply finding the shortest route between two points, the long-term goal is to help people discover enjoyable places to ride and interesting destinations along the way.

### Planned Experience

- **Illustrated 3D terrain:** A stylized, interactive landscape showing real hills, valleys, streets, and trails.
- **Elevation-aware route planning:** Compare routes using distance, climbing effort, and available bicycle infrastructure.
- **Discoverable destinations:** Highlight parks, playgrounds, cafés, public art, scenic viewpoints, and local landmarks.
- **Family adventure planning:** Explore rides based on distance preferences, climbing difficulty, and desired stops.
- **Interactive route exploration:** Select routes, inspect elevation profiles, and discover nearby points of interest.
- **Accessible design:** Maintain clear navigation, readable geographic information, and a practical 2D alternative.

### Technical Direction

**GIS and data processing**
- QGIS and Python for spatial analysis and automation
- Municipal street and bicycle infrastructure datasets
- Digital elevation models for terrain and grade analysis
- OpenStreetMap and municipal points-of-interest datasets

**Web mapping and visualization**
- Leaflet for the initial 2D prototype
- ArcGIS Maps SDK for JavaScript and SceneView for future 3D terrain visualization
- Custom cartographic styling inspired by illustrated maps and cozy video games
- Spatial database and routing algorithms as the project scales

### Development Roadmap

**Phase 1 — Working Prototype**
- [x] Calculate grade for 21 Redmond street segments
- [x] Display grade-colored streets in Leaflet
- [x] Add interactive grade and length popups
- [x] Add a street-grade legend

**Phase 2 — Citywide GIS Analysis**
- [ ] Process Redmond's complete street network
- [ ] Improve elevation sampling along street geometries
- [ ] Integrate bicycle infrastructure
- [ ] Validate and optimize citywide datasets

**Phase 3 — Routing and Discovery**
- [ ] Build a points-of-interest dataset
- [ ] Develop elevation-aware route comparisons
- [ ] Incorporate destinations and family preferences

**Phase 4 — Illustrated 3D Experience**
- [ ] Implement interactive terrain using ArcGIS SceneView
- [ ] Develop a cohesive storybook-inspired visual style
- [ ] Highlight destinations with playful map symbols
- [ ] Build responsive, accessible exploration tools

### Guiding Principle

**Make geographic information feel like an invitation to explore.**

The map should be visually engaging enough to spark curiosity, but accurate and practical enough to help families make informed cycling decisions.
