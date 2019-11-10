# Identify Commercial Centers in New Delhi

**Aim:** Identify commercial centers using Points of Interest (POI) data of New Delhi.

There's a lot of open data available about the demographics and geography of the planet. But this information is not necessarily supervised in any particular structure from which insights can be drawn.

This project creates clusters of distinct commercial centers or markets using points of interest data of New Delhi. Points of interest (POI) data provides location information of different places along with their defining tags like school, type of outlets, type of building, etc.

POI data refers to the coordinates (latitudes and longitudes) of any physical entity with a tag describing its type like commercial buildings, schools, hospitals, restaurants, etc.
 
**Objectives:**

* Get Points of Interest from open data sources like open street maps (OSM).
* Understand how spatial location data works
  * Understand spatial vector data types and how to manipulate it using your language of choice.
  * Understand necessary GIS concepts like projections, spatial clustering, etc.
* Figure out a way of clustering these points into commercial centers/markets. You can use standard size polygons also to cluster the points.
* Find and label the most significant clusters, statistically and intuitively. 
* Visualize the resultant commercial centres/markets.

## Description of the files
* `Exploration.ipynb` is the jupyter file containing all the analysis and code for clustering and identifying the commercial centers of New Delhi.
* `shapefiles/` contain the polygon shp file for New Delhi.
* `requirements.txt` contains all the dependencies (python modules) required to run this project.

## Running the project
* Clone this repository by typing following command on the terminal: `git clone https://github.com/theAayushbajaj/Identifying_commercial_centres.git`.

* Run: **pip install requirements.txt** to install all the required dependencies.

* Navigate to the directory containing `Exploration.ipynb` python notebook and run: jupyter notebook to open the analysis file.

## Methodology

### 1. Collect POI data of New Delhi
All the commercial centers form the heart of the city and contain most of the amenities like restaurants, commerical shopping complexes, malls, hospitals, etc. So, we considered 39 such amenities and using `overpy` we collected POI spatial data of the city. Overpy is the python module used for extracting open data from Open Street Maps (OSM) using `Overpass QL` query language. POI data mainly contains:
* Node: Represents amenities with their latitudes, longitudes and tags providing information like type of amenity, name and their address.
* Way: An ordered list of nodes represents a way.
* Relation: A group of elements used to model logical or geographical relationships between objects.

Below is the Scatterplot showing the nodes (POIs) of Jaipur plotted with longitude on x-axis and latitude on y-axis:
![POI Data Scatterplot](https://github.com/theAayushbajaj/Identifying_commercial_centres/blob/master/images/poi_map.png)

Here we can see that much of New Delhi's commercial centres are located in central and east south part of the city.
More clear view by ward can be seen in the plot below
![POI Data Scatterplot by ward](https://github.com/theAayushbajaj/Identifying_commercial_centres/blob/master/images/poi_by_ward.png)
Now we have to seggregate them by further clustering spatially.

### 2. Approach
- Firstly,my approach will be to implement density-based clustering algorithms like DBSCAN,DENCLUE which will give us clusters purely based on how dense the area is in our dataset but things don't end there
- Commercial centres are meant and run in boundaries (wards) so we have to make sure if a person is seeking this data to identify commercial centres based on the current metrices, it's done right.
- Focussing only on density based would be blunder in practical scenario because the algorithm doesnt classifies the difference and availability of all the amenities (assuming an incoming business needs atleast 60-70% of the amenities listed above)

##### Visualizing the clusters
![Clusters](https://github.com/theAayushbajaj/Identifying_commercial_centres/blob/master/images/cluster_ward_scatter.png)

### Points to ponder

- Which cluster lies in which ward numbers?
- Noise identification in above discovered clusters
- Which cluster needs further clustering?
- Key takeaways from those particular clusters in their respective wards like any special kind of place with special feature (historical,political,cultural,geographical)
- Map filling with those cluster number in their wards and saving the shapefile

### Further ranking the inner clusters by ward
![Cluster-2](https://github.com/theAayushbajaj/Identifying_commercial_centres/blob/master/images/cluster-2.png)

![Cluster-1](https://github.com/theAayushbajaj/Identifying_commercial_centres/blob/master/images/cluster-1.png)

![Cluster-0](https://github.com/theAayushbajaj/Identifying_commercial_centres/blob/master/images/cluster-0.png)

### Conclusion and Vision

- We started with fetching location information of the city of New Delhi alongwith few POI features (amenities) and then applied DBSCAN clustering algorithm.
- After that we identified significant clusters and further did some modifications based on population as intuitively more populated areas tend to succeed in becoming major market centres.
- After that we plotted the heatmap(to rank) for visualize most significant ones

- Turns out Janakpuri West,Tilak Nagar,Pitampura,Central Delhi are most significant commercial places in New Delhi (According to the POI data)

- More analysis can be done once more data about places can be compiled viz Historical,Economical,Population data,Cultural
- Clustering can be improved by employing better state of hyperparameters and Spatial Algorithms that justifies proximity as well as other features
