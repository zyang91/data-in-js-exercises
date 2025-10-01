# Data in JS Exercises

## Part 1 - Accessing Data

Work with local and global datasets that are immediately visual and cover different parts of the world. This part focuses on the fundamentals: fetching data from a URL and getting it onto the screen. The manipulations are minimal, focusing on loops and basic property access.

### **Local Data Sources**

* **Philadelphia Polling Places ([GeoJSON](https://opendataphilly.org/datasets/polling-places/)):** Locations of polling places in the city.
* **Pennsylvania Historic Markers ([JSON API](https://share.phmc.pa.gov/markers/)):** Locations and descriptions of state historical markers.
* **Philly 311 Calls ([CSV API](https://opendataphilly.org/datasets/311-service-and-information-requests/)):** A classic urban dataset showing citizen service requests. A pre-cleaned and smaller JSON version might be best to start with.

### **Global Data Sources**

* **USGS Earthquake Catalog:** Real-time [GeoJSON feed](https://earthquake.usgs.gov/earthquakes/feed/v1.0/geojson.php) of earthquakes worldwide.
* **OpenAQ Platform:** Provides a free [API](https://api.openaq.org/) for global air quality data from monitoring stations.
* **World Bank Indicators API:** A vast [repository](https://datahelpdesk.worldbank.org/knowledgebase/articles/889392-about-the-indicators-api-documentation) of country-level development data.

### **Exercise Ideas**

1. **Map of Polling Places in Philadelphia:**
    * **Goal:** Fetch the Polling Places GeoJSON and display each location as a marker on a Leaflet map.
    * **Skills:** Use the `fetch` API to get the GeoJSON. Use a GEOJSON layer in Leaflet (`L.geoJSON()`) to add the data to the map. Access properties like the polling place name from `feature.properties`.
    * **Result:** A map of Philadelphia with a marker for every polling place. Add a popup to each marker that shows the polling place's name when clicked (`L.marker().bindPopup()`).

2. **Map of Historic Markers:**

    Pennsylvania has a process whereby communities can apply to have a historic marker placed at a significant site -- you may have seen these blue and gold signs around, as there are many in Philadelphia (they look like this: ![MOVE Bombing Historic Marker](../../images/pa_historic_marker_move.jpg)). The Pennsylvania Historical and Museum Commission (PHMC) provides a [search interface](https://share.phmc.pa.gov/markers/) for these markers, which is built on top of a JSON API.

    * **Goal:** Fetch the Historic Markers for a given set of filters and display each marker as a circle marker on a Leaflet map.
    * **Skills:** Use the `fetch` API to get the GeoJSON. Use a `forEach` loop on the `features` array of the resulting GeoJSON object. For each feature, access the coordinates from `feature.geometry.coordinates` and properties like the title from `feature.properties`.
    * **Result:** A map of Philadelphia with a marker for every historic marker. Add a popup to each marker that shows the marker's title when clicked (`L.marker().bindPopup()`).

3. **List of Most Recent 311 Calls:**
    * **Goal:** Fetch a simple CSV file containing an array of the most recent 311 calls. Dynamically create an ordered list in the HTML.
    * **Skills:** `fetch` a CSV file. Use `forEach` or a `for...of` loop to iterate through the array. For each call, use `document.createElement('li')` and `element.textContent` to create a list item, then `appendChild` to add it to an existing `<ol>` in the DOM.
    * **Result:** A simple webpage displaying a numbered list of the most recent 311 calls.

4. **Map of Recent Earthquakes:** 🗺️
    * **Goal:** Fetch the GeoJSON feed for all earthquakes in the past 7 days from the USGS and display them on a world map.
    * **Skills:** Use `fetch` to get the GeoJSON feed. Loop through the `features` array. For each earthquake, use its magnitude (`feature.properties.mag`) to determine the radius of a `L.circleMarker` and display its location and title in a popup.
    * **Result:** A dynamic map showing the planet's recent seismic activity, with larger circles for stronger quakes.

5. **List of Countries by Region:**
    * **Goal:** Use the World Bank API to fetch all countries in a specific region (e.g., "Latin America & Caribbean") and display their names in an HTML list.
    * **Skills:** `fetch` data from a JSON-based API. The World Bank API returns an array where the first element contains metadata and the second contains the data array, so students will need to access the correct part of the response (`data[1]`). They'll then loop through this array to create and append `<li>` elements to the DOM.
    * **Result:** A simple webpage listing the countries of a selected world region.

6. **Chart of Air Quality in a Major City:**
    * **Goal:** Pick a major world city (e.g., Delhi, São Paulo, Lagos). Use the OpenAQ API to get the latest 100 PM2.5 measurements and display them on a time-series line chart.
    * **Skills:** `fetch` from an API that requires query parameters (e.g., `?city=Delhi&parameter=pm25`). Process the resulting JSON to create two arrays: one for timestamps (labels) and one for values (data). Pass these arrays to Chart.js to create a line chart.
    * **Result:** A line chart showing recent air pollution trends in a specific city.
