# Routing Problems using Google Maps

A **Traveling Salesman Problem** (TSP) and **Vehicle Routing Problem** (VRP) integrated with the **Google Maps Platform** to:

1. **Obtain real-world driving distances** using the **Distance Matrix API**.
2. **Geocode** addresses into latitude/longitude (Geocoding API).
3. **Solve** the TSP/VRP using Gurobi.
4. **Display** the route on a map with **actual driving paths** (via the **Directions API**), using the [Folium](https://github.com/python-visualization/folium) library.

## Table of Contents

1. [Features](#features)
2. [Prerequisites](#prerequisites)
3. [Installation](#installation)
4. [How It Works](#how-it-works)
5. [Usage](#usage)
6. [Real-Time Considerations](#real-time-considerations)
7. [Contributing](#contributing)
8. [License](#license)

---

## Features

- **Gurobi TSP/VRP Solver**  
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
   git clone https://github.com/RenatoMaynard/Routing-Problems-using-Google-Maps.git  

## How It Works

1. Given a set of **N locations**, the goal is to find the **shortest possible route** that visits each location exactly once and returns to the starting point. 

2. Distance Matrix via Google Maps API
  - You provide a **list of addresses**.
  - The script calls the **`googlemaps.Client.distance_matrix()`** with `mode='driving'`.
  - Google returns a **pairwise distance matrix**, containing **driving distances (or times)** between all locations.
  - This matrix forms the basis of the TSP formulation.
3. Real Driving Path with Google Directions API
  - Once the **optimal order of locations** is determined:
    - Each **pair of consecutive locations** is sent to the **Google Directions API** to obtain the **actual driving path**.
    - The response contains an **`overview_polyline`**, which encodes the path as a sequence of **latitude/longitude points**.
    - These points are **decoded** and prepared for visualization.

4. Route Visualization with Folium
- Using [**Folium**](https://github.com/python-visualization/folium), the script:
    - Plots the **decoded polylines** on a map.
    - Ensures the route **follows actual roads**, not straight lines between locations.
    - Creates an **interactive map**, visually displaying the optimal route as a **red path**, overlaid on real-world geography.
 
## Usage

1. Configure your addresses
   -Edit the list of addresses or coordinates you want to solve for.
2. Run the Code
3. The script will:
   1. Call the Distance Matrix API to build your distance matrix.
   2. Solve the TSP/VRP using Gurobi
   3. Call the Directions API for each leg of the optimal route.
   4. Create a Folium map with markers and real driving polylines.
   5. Save the map to tsp_route.html/vrp_route.html.
4. **Open** tsp_route.html/vrp_route.html to see the route

## Real-Time Considerations
Google’s Distance Matrix API can handle real-time traffic if you specify additional parameters:
  -For instance, you can set departure_time to now or a specific timestamp to factor live or 
 predictive traffic data.
  - You could also switch from distance to duration_in_traffic if you want the actual time with 
  traffic.
In google_api_utils.py, you might do:
```bash
gmaps.distance_matrix(
  origins=addresses,
  destinations=addresses,
  mode='driving',
  departure_time='now',  # or a UNIX timestamp
  traffic_model='best_guess'
)
```
**NOTE:** In order to use the real-time traffic-based durations you must have a Google Maps Plataform Premium plan or pay for it. 

## Contributing
Feel free to open issues or create pull requests:
  1. Fork the repository.
  2. Create a new branch.
  3. Commit changes.
  4. Push to the branch.
  5. Create a Pull Request.

## License
This project is open-sourced under the MIT license.
