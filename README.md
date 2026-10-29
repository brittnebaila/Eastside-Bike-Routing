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

### The Vision: Explore Your City

What if planning a family bike ride felt more like exploring a beautiful video game than navigating a traditional map?

Eastside Bike Routing is evolving into an interactive, storybook-inspired 3D cycling map that helps families discover their city. Using real geographic and elevation data, the experience will bring hills, trails, neighborhoods, and local destinations to life through playful cartography.

Families will eventually be able to explore routes based on distance, elevation, and bicycle infrastructure while discovering interesting stops along the way—from parks and playgrounds to public art, scenic viewpoints, and neighborhood cafés.

**The goal is to make cycling more approachable, exploration more rewarding, and geographic information more meaningful for everyday people.**

*Current development:* Building and validating the GIS data pipeline, street-grade analysis, and interactive Leaflet prototype. The illustrated 3D experience and destination discovery features are planned for future development.
