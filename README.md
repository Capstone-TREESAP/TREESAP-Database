# TREESAP-Database

## Format
The top level file is `db.json`, which contains the list of files that the app should fetch and process. `db.json` contains the following sections:

* UBC Buildings: files which compose the building layer (for example, in shading and cooling mode).

* UBC Boundary: files which compose the outline of campus.
    * Currently only used for validation to ensure all polygons are within the boundaries of campus.

* Calculation Constants: files which compose the constants used for calculating ecosystem services. 
    * These files must contain the two following constants: "Carbon Sequestration Rate" and "Tree Run-off Effects Rate". 
    * This is the only set of files read as json instead of geojson.

* Areas of Interest: files which compose the pre-loaded intersection polygons.
    * Each polygon should contain a "NAME" property, which will be the name displayed in the areas of interest checklist of the app.

* Tree Cover Polygon Datasets: the sets of polygons loaded as tree cover layers in the app.
    * Contains one JSON object for each set of data. The JSON object should be named as the display name in the tree cover layer checklist (for example, "LiDAR 2018").

Most of the JSON items within `db.json` are the same format for simplicity of processing:

```
"Name of object": {
    "files": [list of files containing relevant data]
}
```
The exception is the Tree Cover Polygon Datasets: this section contains one JSON object of the above format for each dataset.

## Adding Data

### Adding a new polygon set

1. Create a geojson file containing the new data
2. Add the file to this database. Preferably, LiDAR datasets will go in the lidar folder with the name format `year_lidar_tree_cover.geojson`, and orthophoto datasets will go in the orthophoto forlder with the name format `year_orthophoto_tree_cover.geojson`
3. Add a section under "Tree Cover Polygon Datasets" with the display name of the new dataset and the path to the relevant files. For example, if a new file `2014_orthophoto_tree_cover.geojson` is added to the orthophoto folder, the "Tree Cover Polygon Datasets" section should be updated to include:
```
"Orthophoto 2014": {
    "files": ["orthophoto/2014_orthophoto_tree_cover.geojson"]
},
```

### Adding areas of interest
1. Create a new geojson file containing the new areas of interest, along with the required NAME property for each
2. Add the file to the database, preferably within the areas_of_interest folder
3. Add the path to the new file under the "Areas of Interest" files section. For example, if a new file `my_areas.geojson` is added to the areas_of_interest folder, `db.json` should include:
```
"Areas of Interest": {
    "files": [
        "areas_of_interest/my_areas.geojson"
    ]
}
```