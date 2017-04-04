# GeoObject-PlanetJSON
This tool makes use of gdal and pyshp libraries and projects to convert between
1) Google Earth Keyhole Markup Language or KML file
2) ESRI shapefiles
3) geojson file(in this case from geojson.io)

This allows the user to struture the JSON file to be used by Planet API V1.0 for downloading PlanetScope and RapidEye Assets and can now also support Landsat and Sentinel2 downloads. 

Planet Inc is a company that is currently trying to map the entire planet every single day and as the constellation size increases the data value and repeat cycle increases as well.(https://www.planet.com/) The planet labs API consists of searching for satellite imagery type assets using a structured geojson

## Prerequisites
It assumes you use Python2.7 hopefully >=2.7.12

In the download.py file edit the line with your Planet API Key and save[1].You can install all python dependencies by simply running[2]

```
	1) os.environ['PLANET_API_KEY']="Enter Your Planet Key Here"
	2) pip install -r requirements.txt
```

Command Line Interfaces are extremely useful since they can be created to be platform independent and they provide a short hand method to automate scripts and more concise and powerful means to control a program or operating systems.

## Getting started

The first step is to define a area that is available for download under your Planet API license. It can be done in three ways
 * From geojson.io define your area of interest click on save as GeoJson(A map.geojson file is created)
 * Create kml file of the area of interest
 * Create an esri shapefile and place it along with all supporting files(.shp,.sbx,.prj,.dbf etc)

 
## GeoObject to JSON
This tool can be used to convert from kml(google earth file)/shapefile(ESRI) or geojson file from geojson.io to structured aoi.json used for querying planet datasets using API 1.0. The output is a file aoi.json which can then be used to query and download using cli_jsonparse tool.

```
usage: cli_aoi2json.pyc [-h] [--start START] [--end END] [--cloud CLOUD]
                        [--inputfile INPUTFILE] [--geo GEO]

Tool to convert KML, Shapefile or GeoJSON file to AreaOfInterest.JSON file
with structured query for use with Planet API 1.0

optional arguments:
  -h, --help            show this help message and exit
  --start START         Start date in YYYY-MM-DD?
  --end END             End date in YYYY-MM-DD?
  --cloud CLOUD         Maximum Cloud Cover(0-1) representing 0-100
  --inputfile INPUTFILE
                        Choose a kml/shapefile or geojson file for
                        AOI(KML/SHP/GJSON
  --geo GEO             map.geojson/aoi.kml/aoi.shp file
```

## Converting to Structured JSON
This tool can be used to convert between multiple file formats to a structured json which is accepted by Planet API. It can read Google Earth kml files, ESRI shapefiles as well as geojson files downloaded from map.geojson. For use of use, it is better to use a bounding box to encompass area of interest, multivertex polygon to JSON don't always go well when querying using such complex json structures.

```
For KML Files
python cli_aoi2json.pyc --start 2017-01-01 --end 2017-04-02 --cloud 0.15 --inputfile KML --geo "./lybbox.kml"

For ESRI ShapeFiles
python cli_aoi2json.pyc --start 2017-01-01 --end 2017-04-02 --cloud 0.15 --inputfile SHP --geo "./lybbox.shp"

For GeoJSON Files
python cli_aoi2json.pyc --start 2017-01-01 --end 2017-04-02 --cloud 0.15 --inputfile GJSON --geo "./lybbox.geojson"
```

# Credits

[JetStream](https://jetstream-cloud.org/) A portion of the work is suported by JetStream Grant TG-GEO160014.

Also supported by [Planet Labs Ambassador Program](https://www.planet.com/markets/ambassador-signup/)
