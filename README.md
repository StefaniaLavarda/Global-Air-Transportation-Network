# Global Air Transportation Network — Network Science Project

This repository contains an individual Network Science project analyzing the **global air transportation network** using the **OpenFlights** dataset.

## Project Overview

- **Nodes:** Airports worldwide  
- **Directed edges:** A route from airport *i* to airport *j* indicates a direct flight connection  
- **Edge weight:** Number of **distinct airlines** operating the route (*i → j*)  
- **Filtering choice:** Only **direct flights** are considered (`stops == 0`) to avoid introducing artificial “shortcut” edges that would distort path-based measures.

## Research Questions

1. **Connectivity:** How connected is the global air transportation network?  
2. **Hubs:** Which airports are structurally most important for global mobility?  
3. **Communities:** Do detected network communities align with geography/countries?

## Data

The project uses the **OpenFlights** datasets:
- `airports.dat` (airport metadata: location, country, codes, etc.)
- `routes.dat` (flight routes between airports)

Data source: OpenFlights (https://openflights.org/data)

### Preprocessing Summary
- Remove routes with missing source/destination airport IDs
- Keep only direct routes: `stops == 0`
- Aggregate routes into weighted edges using:
  - `weight(i, j) = number of distinct airlines flying i → j`
- Remove edges whose endpoints are not present in the airports table (consistency check)

## Main Methods

### Network Analysis (NetworkX)
- Degree (in/out), density, reciprocity
- Weakly/strongly connected components
- Clustering/transitivity
- Bridges and local bridges
- Assortativity (e.g., by country)
- Centrality (degree, betweenness, closeness, PageRank)
- Community detection (Louvain) + comparison with country labels (NMI)

### Visualization
- Geographic visualization visualization in **Gephi** using exported node/edge tables (`nodes_gephi.csv`, `edges_gephi.csv`)

### Machine Learning on Networks
- **Node classification**
- Goal: predict whether an airport is **high betweenness centrality** using **Node2Vec embeddings** + a supervised classifier
- Evaluation with standard metrics (e.g., accuracy, ROC AUC)

## How to Run

1. Download OpenFlights data and place it in `data/`
2. Open and run `project.ipynb` (or the Deepnote notebook)
3. (Optional) Export for Gephi:
   - `nodes_gephi.csv`
   - `edges_gephi.csv`

## Notes

This work is completed individually for a university Network Science course.  
The notebook is designed to be readable and reproducible, with explanations and interpretation of results alongside code.


