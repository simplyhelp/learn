# SOLRIS 3.0

Southern Ontario Land Resource Information System (SOLRIS) is created by the Province of Ontario as their primary data layer providing a comprehensive, 
standardized, landscape level inventory of natural, rural and urban lands in Ecoregions 7E, 6E and 5E, 2000 to 2015. The data covers the date ranges from 
2000-2015 in Ecoregions 7E, 6E and 5E (Growth Plan for the Greater Golden Horseshoe Study Area and an Eastern Ontario extension to the Forest Resources 
Inventory boundary).

- SOLRIS LIO Metadata Link [https://geohub.lio.gov.on.ca/documents/0279f65b82314121b5b5ec93d76bc6ba](https://geohub.lio.gov.on.ca/documents/0279f65b82314121b5b5ec93d76bc6ba)
- SOLRIS Download Link [https://www.arcgis.com/home/item.html?id=0279f65b82314121b5b5ec93d76bc6ba](https://www.arcgis.com/home/item.html?id=0279f65b82314121b5b5ec93d76bc6ba)

The downloaded ZIP file contains the following:

- SOLRIS_Version_3_0_LAMBERT.gdb - Esri File Geodatabase containing:
  - project_area_lambert (Polygon)
  - SOLRIS_Version_3_0_Changes_2000to2015_Lambert (Polygon)
  - SOLRIS_Version_3_0_Class_Corrections_2000to2015_LAMBERT (Polygon)
  - SOLRIS_Version_3_0_LAMBERT (Raster)
- SOLRIS_Version_3_0_LAMBERT.tif (Raster, same as in Esri File Geodatabase)
- SOLRIS_Version_3_0.lyr (ArcGIS Style file)
- Southern Ontario Land Resource Information System Version 3.0 Data Specifications.pdf
- Southern Ontario Land Resource Information System Version 3.0 FAQs.pdf

All data are in Spatial Reference NAD 1983 CSRS Ontario MNR Lambert Conformal Conic (EPSG 3162). 

# Using in QGIS

The lyr file is binary and cannot be read by QGIS. To facilitate ease of use, SimplyHelp has created the following CLR 
file which is a conversion of the LYR file provided in the above package. Copy this text and save it as "SOLRIS.clr" which can be used in QGIS. 

```
11 255 255 0 255 Open Beach/Bar
21 255 170 0 255 Open Sand Dune
23 168 112 0 255 Treed Sand Dune
41 104 104 104 255 Open Cliff and Talus
43 52 52 52 255 Treed Cliff and Talus
51 232 190 255 255 Open Alvar
52 223 115 255 255 Shrub Alvar
53 197 0 255 255 Treed Alvar
64 255 190 232 255 Open Bedrock
65 211 255 191 255 Sparse Treed
81 205 205 102 255 Open Tallgrass Prairie
82 137 137 68 255 Tallgrass Savannah
83 112 112 43 255 Tallgrass Woodland
90 117 191 48 255 Forest
91 59 179 0 255 Coniferous Forest
92 170 255 0 255 Mixed Forest
93 0 255 42 255 Deciduous Forest
131 0 140 94 255 Treed Swamp
135 163 255 115 255 Thicket swamp
140 152 214 190 255 Fen
150 255 182 122 255 Bog
160 191 233 255 255 Marsh
170 0 38 115 255 Open Water
191 80 176 98 255 Plantation
192 69 186 34 255 Hedge Rows
193 255 255 190 255 Tilled
```

Above is free to distribute or modify, but must contain a reference as SimplyHelp.ca for the source
201 255 0 0 255 Transportation
202 170 207 60 255 Built Up Area-Pervious
203 195 193 199 255 Build Up Area-Impervious
204 230 126 140 255 Extraction-Aggregate
205 255 167 127 255 Extraction-Peat/Topsoil
250 199 215 158 255 Undifferentiated
```
