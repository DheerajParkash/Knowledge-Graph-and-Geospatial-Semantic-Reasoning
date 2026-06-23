# Web of Data — Cultural Heritage & Urban Interaction (RDF Knowledge Graph Project)

## Overview
This project analyzes the relationship between cultural heritage sites and surrounding urban environments using Semantic Web technologies. It builds a knowledge graph from UNESCO World Heritage data and integrates it with city-level data from Wikidata to enable geospatial queries, proximity analysis, and demographic insights.

## Motivation / Problem Statement
Cultural heritage sites interact strongly with nearby cities through tourism, accessibility, and regional development pressure. Understanding these relationships helps in heritage preservation, urban planning, and infrastructure optimization. This project leverages RDF and SPARQL to quantify spatial and demographic interactions around heritage sites.

## Objectives
- Transform UNESCO heritage dataset into an RDF knowledge graph
- Enable semantic and geospatial querying over heritage sites
- Integrate external city data using federated SPARQL queries
- Compute proximity between heritage sites and cities
- Analyze population density around heritage sites within buffer zones

## Dataset
The dataset is derived from the UNESCO World Heritage List and includes:
- Unique site identifiers
- Multilingual site names
- Geographic coordinates (latitude, longitude)
- Inscription details and criteria
- Regional and country classification

### Preprocessing
A Python preprocessing pipeline generates a simplified dataset with:
- `unique_number`
- `iso_code`
- `name_en`
- `latitude`
- `longitude`
- `states_name_en`
- `region_en`
- `coordinates` (WKT format)

This reduced schema supports efficient spatial querying and RDF conversion.

## Knowledge Graph Construction
The dataset is modeled as an RDF graph using the following namespaces:

- `un:` project namespace
- `unhs:` historical site entities
- `loc:` location resources
- `geo:` GeoSPARQL ontology
- `rdfs:` schema labels
- `owl:` ontology definitions

Each heritage site is represented as:
- `un:HistoricalSite`
- Geometry linked via `geo:hasGeometry`
- Coordinates stored in WKT format

## Methodology / Approach

### 1. RDF Data Modeling
Heritage sites are converted into RDF triples with spatial and semantic attributes.

### 2. SPARQL Querying
Local SPARQL queries extract:
- Site names
- Geometries
- Coordinates

### 3. Federated Queries
External city data is retrieved from Wikidata:
- City name
- Population
- Coordinates

### 4. Geospatial Analysis
Using GeoSPARQL:
- Distance computed using `geof:distance`
- Filtering applied for cities within:
  - 100 km radius
  - 150 km radius

### 5. Aggregation
Population values are aggregated per heritage site to estimate urban pressure.

## Key SPARQL Queries

### 1. Heritage Site Extraction
Retrieves site metadata and geometry from RDF graph.

### 2. City Data from Wikidata
Fetches French cities with population and coordinates using federated queries.

### 3. Proximity Query (≤ 100 km)
Joins heritage sites and cities based on geospatial distance.

### 4. Population Aggregation (≤ 150 km)
Computes total population around each heritage site:

- GROUP BY heritage site
- SUM(population)

### 5. Visualization Query
Uses bounding box filtering around a reference point (Amiens Cathedral) for spatial visualization in YasGUI.

## System Architecture
- RDF Knowledge Graph (UNESCO data)
- SPARQL endpoint (local store)
- Federated SPARQL (Wikidata Query Service)
- GeoSPARQL engine for spatial computation
- Visualization via YasGUI

## Results / Key Findings
- Successful integration of heritage and urban datasets using federated RDF queries
- Efficient spatial filtering using GeoSPARQL functions
- Identification of high-population clusters near heritage sites
- Quantification of potential urban pressure on cultural heritage regions

## Technologies Used
- RDF / OWL / RDFS
- SPARQL 1.1 Federated Queries
- GeoSPARQL
- Wikidata Query Service
- Python (data preprocessing)
- YasGUI (SPARQL visualization)

## Usage

1. Load RDF dataset into a SPARQL endpoint
2. Run SPARQL queries for:
   - Site extraction
   - City enrichment
   - Spatial filtering
3. Adjust distance thresholds (100 km / 150 km) as needed
4. Visualize results using YasGUI

## Future Work
- Extend analysis beyond France to global scale
- Integrate temporal tourism and mobility data
- Improve geospatial precision with advanced geodesic models
- Add ML-based prediction of heritage site risk exposure
- Develop interactive dashboards for policymakers

## Author
Dheeraj Parkash  

## License
MIT License