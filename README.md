# My TSP Project

A **Traveling Salesman Problem** (TSP) solver in Python, integrated with the **Google Maps Platform** to:

1. **Obtain real-world driving distances** using the **Distance Matrix API**.
2. **Geocode** addresses into latitude/longitude (Geocoding API).
3. **Solve** the TSP using Gurobi.
4. **Display** the route on a map with **actual driving paths** (via the **Directions API**), using the [Folium](https://github.com/python-visualization/folium) library.

## Table of Contents

1. [Features](#features)
2. [Prerequisites](#prerequisites)
3. [Installation](#installation)
4. [How It Works](#how-it-works)
5. [Usage](#usage)
6. [Real-Time Considerations](#real-time-considerations)
7. [Project Structure](#project-structure)
8. [Contributing](#contributing)
9. [License](#license)

---

## Features

- **Gurobi TSP Solver**  
  Uses binary decision variables for each possible route between locations, plus Miller–Tucker–Zemlin (MTZ) constraints for subtour elimination.
- **Real Road Distances**  
  Fetches pairwise distances from the **Google Distance Matrix API** to accurately reflect real-world driving distance or time (depending on your choice).
- **Interactive Map**  
  Uses **Folium** to display the route over actual streets (polyline data from **Google Directions API**).  
- **Extensible**  
  You can easily modify the code to use travel *time* instead of *distance*, integrate new constraints, or scale to more advanced routing problems.

---

## Prerequisites

1. **Google Cloud Platform**  
   - A **Google Maps Platform** project with the APIs enabled:
     - [Distance Matrix API](https://developers.google.com/maps/documentation/distance-matrix)
     - [Geocoding API](https://developers.google.com/maps/documentation/geocoding)
     - [Directions API](https://developers.google.com/maps/documentation/directions)
   - An **API key** with appropriate permissions.
   
2. **Gurobi**  
   - A valid Gurobi license.  
   - [Install Gurobi](https://www.gurobi.com/documentation/) and ensure `gurobipy` is available in your Python environment.
   
3. **Python 3.7+**  
   - Typical libraries: `googlemaps`, `folium`, `gurobipy`, etc.

---

## Installation

1. **Clone** this repository:

   ```bash
   git clone https://github.com/your-username/my-tsp-project.git
