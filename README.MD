README

## A Warning
Zip codes (ZCs) and zip code tabulation areas (ZCTAs) are not the same thing and thus don't map 1:1. They are generally clsoe, but not exact and that is a limitation to my method that needs to be acknowledged. ZCs are created by the United States Postal Service (USPS) to make delivery routes more efficient. ZCs don't have associated geogrpahic boundaries. ZCTAs are created by the US Census Bureau from census blocks and have associated shape files. These shape files can cross state boundaries and the main file can be downloaded [here](https://www.census.gov/cgi-bin/geo/shapefiles/index.php?year=2020&layergroup=ZIP+Code+Tabulation+Areas). This is a large file and isn't included in this repository. Instructions on how to convert it to a file useable in the provided nbotebooks is below. More information about ZCTAs can be found [here](https://www.census.gov/programs-surveys/geography/guidance/geo-areas/zctas.html).

#### My process

###### Convert Main 2020 Shape File to GeoJSON
In order to work with the main 2020 shape file in the Jupyter notebooks, it first needs to be converted to a GeoJSON file. To do this, I loaded the shape file into [QGIS software](https://qgis.org/) and exported the layer containing all ZCTAs to a GeoJSON file. This file is ~1.3G and may take awhile to export. Once the file is ready, it can be placed in the data folder of this repo to run the ParseStatesFromMainFile.ipynb file.

###### Mapping ZCs to ZCTAs by Location
I used the zip code prefixes [wiki page](https://en.wikipedia.org/wiki/List_of_ZIP_Code_prefixes) in order to map ZCTAs to all 50 states, DC, Puerto Rico, Guam, and the Virgin Islands. This data is stored in a csv file in the data folder, and uses the first 3 digits of a ZC to map to a state/territory. To reiterate, these don't map 1:1 and will not produce/follow exact state boundaries/shapes. However, for my use case this method was close enough. The jupyter notebook file ParseStatesFromMainFile.ipynb does this mapping. 


###### Simplifying the Shape Files for each Location to Reduce File Size
In order to facilitate faster loading/drawing time in my mapping applications, I simplified the geometries for each shape in the GeoJSON files by location. This is done in the SimplifyGeometriesZCTAs.ipynb file. The file contains a custom function where you can specify the toleance when simplifying. A larger tolerance will result in smaller GeoJSON files and faster mapping time at the cost of more shoppy ZCTA shapes. For my use case I settled on a tolerance value of 0.0005 as the best balance of these trade-offs. The simplified GeoJSON files with a tolerance of 0.0005 are provided in the 2020 Census Simplified Folder.

###### Example Map
![Georgia 2020 ZCTAs](https://github.com/aha1994/zcta2020/blob/main/img/Georgia%20ZCTAs%202020%20Example.PNG) ![Michigan 2020 ZCTAs](https://github.com/aha1994/zcta2020/blob/main/img/Michigan%20ZCTAs%202020%20Example.PNG) ![Kansas 2020 ZCTAs](https://github.com/aha1994/zcta2020/blob/main/img/Kansas%20ZCTAs%202020%20Example.PNG)



Hopefully these files/notebooks can provide some use to others. If you can improve upon this or know of a better way to go about this kind of mapping please reach out and let me know. Cheers!

