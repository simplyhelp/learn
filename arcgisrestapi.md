# ArcGIS REST api introduction

This site introduces the ArcGIS REST API to those learning about web GIS. In particular, it will focus on navigating and using this documentation: https://developers.arcgis.com/rest/services-reference/enterprise/get-started-with-the-services-directory.htm

# What is REST anyway?

Representational State Transfer (https://en.wikipedia.org/wiki/Representational_state_transfer) is a common web architecture for middle-ware that uses URLs to retrieve data from internal data systems. Each URL request to a REST endpoint (as they are called) is independent of any other request (stateless). This means the server providing the results to a REST endpoint request is not concerned with what it did before, or after; it just needs to work on the current request. It is the job of an application to maintain its state (for example, remember where you are looking when panning on a map). 

Refresher: What is a URL? https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL

The modern development pattern for web solutions is a web-tier, which is only the user interface, a data-tier that powers the information usually required for applications, and some middle stuff that bridges the gap between the user and data. REST is ideal for this, especially compared to other technologies like SOAP and XML which are hard to navigate interpret as a programmer. This is where most REST endpoints shine: They have a "human" navigable GUI. 

Most REST endpoints have two versions, one focused on the developers (humans), and another focused on the computer (particularly but not limited to JavaScript). If you open the "human" version you get a common website interface with links and lists. It is well organized, but isn't a fancy website like a marketing page. It is utilitarian and functional to server its purpose: it provides a clickable way you can interact with the interface, test, design new URLs that do specific use cases, and then possible program something to generate the same URLs and automate a process or task. 

# ArcGIS Enterprise

ArcGIS Enterprise is a software suite and web-GIS platform. The two main components, ArcGIS Server and Portal, both have REST endpoints to manage its configuration. ArcGIS Server is the main spatial engine for ArcGIS Enterprise, and all data published through Portal or directly against ArcGIS Server are made available in a rich and well-documented REST endpoint called the ArcGIS REST API.

# ArcGIS Server

Learning to navigate ArcGIS Server's REST API gives data administrators a powerful tool in discovering what capabilities are available, debugging problems with solutions, and ensuring data shared are secured, appropriate and valid. Without understanding how to navigate the REST API, an administer is effectively working blind and only can use the GUI within ArcGIS Server or Portal to see what is happening with their environment.

# The REST Services Directory

The ArcGIS REST services directory is a website (HTML version) and programming interface (JSON Version) to published services. This is often called an endpoint. The default location for this rest endpoint is in a path of `/arcgis/rest/services`. The "arcgis" portion can be configured and sometimes there are more folders placed in the path, but for ESRI it always has `/rest/services` when dealing with Data and Map Services, which this learning tool focuses on. 

1. Use Google to search for a place and `/arcgis/rest/services` and see the various public services

Search "ontario arcgis/rest/services": https://www.google.com/search?q=ontario+%2Farcgis%2Frest%2Fservices

Many of the returned searches are for government ArcGIS REST endpoints that power much of the public websites! All of these can be read by a program or person. How? Each is available both as a JSON and HTML version:

- Example HTML Version (default): https://sampleserver6.arcgisonline.com/arcgis/rest/services?f=html
- Example 'pretty' JSON Version: https://sampleserver6.arcgisonline.com/arcgis/rest/services?f=pjson

What is different between the results from the two above URLS? 

<details><summary>Click for Answer</summary>

> - There is no URL parameter on the first one, but the second one specifically asks for the returned results in "Pretty" JSON. The JSON version is meant to be serializable by a program, usually JavaScript. That is just a fancy way of saying a programmer can code something to read and navigate the information shown on the REST endpoint easily. 
> - Why the P in front of JSON? "Pretty" JSON. Pretty? It is formatted nicely to be read by a human and program.

</details>

2. Open the less "pretty" version of the interface by changing the f=pjson to be f=json in the URL. 

Now the JSON bunches up (all spaces are removed) and is arguably less easily read by us people? This is an optimum format for a program to read, but not very easily read as a person. The PJSON version is easier for people, but without question the HTML version is easiest for us to read since it even has links that can be clicked. 

3. Open the HTML version by changing the f=json in the URL to be f=html

The f=html option is the default, so if the "f" URL parameter is missing it will show the html version. There are other output formats, but for the purposes here we will be focusing on the HTML version. The full documentation for this URL parameter is at https://developers.arcgis.com/rest/services-reference/enterprise/output-formats.htm.

4. Return your focus to and open just the HTML version at https://sampleserver6.arcgisonline.com/arcgis/rest/services. The remaining parts of the exercise will always use the HTML version, but remember you can always change the format to `f=json` or `f=pjson` in the URL parameters to return JSON or PJSON. 

Now, using the HTML version of sampleserver6 (PS: there is a sampleserver5 as well, with the same content) let us explore some functionality with existing published map services.

# Navigating the MapServer REST Endpoint

Full API Documentation: https://developers.arcgis.com/rest/services-reference/enterprise/map-service.htm

A MapServer is available on ArcGIS Enterprise and ArcGIS Server environments, but not ArcGIS Online. This contains data (layers) combined together into a single "map" with default applied cartography. Think of it as a pre-created map that you can easily request as an image. This is called a Dynamic Map, meaning that the image provided is generated using the live data on the server. 

Example: https://sampleserver6.arcgisonline.com/arcgis/rest/services/USA/MapServer/export?bbox=-89.25%2C35.48%2C-72.61%2C46.01&size=713%2C451&format=png32&f=image

Generates this image:

![map example](https://sampleserver6.arcgisonline.com/arcgis/rest/services/USA/MapServer/export?bbox=-89.25%2C35.48%2C-72.61%2C46.01&size=450%2C200&format=png32&f=image)

Lets break this down into its method and parameters, section by section (remember, URL parameter order does not matter when submitting a URL for a REST request and `%2C` is an encoded `,` (comma)):

- Each parameter below is detailed in the documentation, and is recommended you read each listed below from here: https://developers.arcgis.com/rest/services-reference/enterprise/export-map.htm

## EXPORT method

The Export is a method (method, as in it does something) that generates an image on the server using all layers in the map service, then returns the image file as link in the format requested. 

## Bounding Box `bbox=-89.25,35.48,-72.61,46.01`  

Documentation: https://developers.arcgis.com/rest/services-reference/enterprise/export-map.htm#GUID-615E87E9-D0A9-4211-A872-06FFF95A6244

This is the bounding box for the request. The image will be generated using the geographical box indicated. The syntax is `<xmin>, <ymin>, <xmax>, <ymax>` using the spatial reference of the map (or converted, if a different spatial reference is used by including the URL parameter `bbSR`). 

## Image Size `size=450,200` 

Documentation: https://developers.arcgis.com/rest/services-reference/enterprise/export-map.htm#GUID-E79E5960-E5D7-42B5-BB1A-CE1D345396C9

Given the bounding box, this image size request will be the size of the actual image returned in pixels `<width>,<height>`.

## Image Format `format=png32` 

Documentation: https://developers.arcgis.com/rest/services-reference/enterprise/export-map.htm#GUID-6B8563EA-E9BC-4A1F-8FB7-BC8FD3B83FA2

The image format to be returned can be specified using this parameter. In this case, it is a 32-bit PNG that is created and returned. There are a lot of options for this, including any one of: 

`png | png8 | png24 | jpg | pdf | bmp | gif | svg | svgz | emf | ps | png32`

## Return the image `format=image` 

Documentation: https://developers.arcgis.com/rest/services-reference/enterprise/export-map.htm#GUID-6B8563EA-E9BC-4A1F-8FB7-BC8FD3B83FA2

This option just returns the image directly from the request. It can be used in an `<img src="image">` tag directly, where the image is the entire URL that generates that static image. There is no user interface around this image being displayed, so you cannot interact with the map. Note you can also shortform this to just "f=". 

## What else can a MapServer do?

The URL example for export just returns an image. You cannot use the image to do anything, other than look! So there are other methods on the MapServer that allow you to interact with the data, including identify. Here is an identify example all pre-populated asking for a point on a map of the USA right on the state line between Nevada and California (note some characters are not URL encoded for easier readability, but they should be if using this in a production environment!):

https://sampleserver6.arcgisonline.com/arcgis/rest/services/USA/MapServer/identify?geometryType=esriGeometryPoint&geometry=-120,40&tolerance=10&mapExtent=-119,38,-121,41&imageDisplay=400,300,96

You can actively change any of the values and re-run the query with results returning back below the form. It is a nice way to play and test out what is happening, as well to learn what the capabilities are. Refer to the API documentation (https://developers.arcgis.com/rest/services-reference/enterprise/identify-map-service-.htm) if you want to learn what each parameter expects, which are required, and what format should they be written in. 

Identify and Export are just two methods available on the MapServer REST endpoint. Click on the `USA (MapServer)` at the top of the REST Endpoint HTML window to return to the main MapServer interface. Scroll to the bottom where it has Supported Operations shown. This is a clickable list of all the methods available for this service! You can learn about each by clicking and looking at the form to drive the interface.

Another way you can interact with a MapServer is layer by layer. At the main interface, look at the list of layers included in this service:

- Layers:
  - Cities (0)
  - Highways (1)
  - States (2)
  - Counties (3)

Each is clickable and has their own interface. Read on how to interact with these and use the `Query` method to return attribute data and specific geometries next. 

# Layers in ArcGIS REST Endpoints

Map Services (actually both Feature Services and Map Services, but more on Feature Services later) have one or more layers of geographic data included within them. Return to the root of the USA MapServer: 

https://sampleserver6.arcgisonline.com/arcgis/rest/services/USA/MapServer

## MapServer (and FeatureServer) Layer List

The list of layers is numbered, usually starting with 0 and going up to the number of Layers -1 (called 0 based numbering). Click on the States layer notice how the URL is modified. A number is added to the end that corresponds to that layer's listed number (it is called a layer ID). 

Knowing this, can you modify your REST Endpoint URL on the USA MapServer to open the first layer Cities?

<details><summary>Click for URL Answer</summary>
 
- https://sampleserver6.arcgisonline.com/arcgis/rest/services/USA/MapServer/0
- Remember, the numbering is 0 based so the first one is 0, not 1! If you put in 1 you would get the highways layer.

</details>

## Dynamic Layers and Tables

https://developers.arcgis.com/rest/services-reference/enterprise/dynamic-layer-table.htm

The two most common layer types publish are dynamic layers and tiled/cached layers. Dynamic layers are typically operational layers, in that the application that will be using this map service interacts with the data, modifies the data, or queries the data directly (hence operational). Contrast that with tiled or cached layers where they are there for visual aesthetics or cartographic reasons only--the application does nothing other than display the data, usually in the background with the operational data on top. For the purposes of exploring the REST endpoint we will focus on operational layers, which again the documentation calls these dynamic layers because the data can change at any time (if the underlying data were updated in some way) and those changes will be displayed on the next request. 

Where a layer that is selected is stored as vector data (X and Y coordinates to make up a point, line or polygon and combined with an attribute record), there are a series of operations possible that work similar to a SQL SELECT statement. This is called a query operation or method. 

## Query Method

API Documentation: https://developers.arcgis.com/rest/services-reference/enterprise/query-map-service-dynamic-layer-.htm

The Query method is used to retrieve records from the data that is in the map service. Combined with the Export option above, this is one of the most used methods to display information in web applications from the ArcGIS ecosystem. You can think of this method as the equivalent of a "SELECT" statement in SQL, but uses a REST interface. 

Start by opening and looking at this example query:

https://sampleserver6.arcgisonline.com/arcgis/rest/services/USA/MapServer/0/query?where=capital%3D%27Y%27&outFields=objectid%2Careaname%2Cst&orderByFields=areaname&f=html


### Query Results

```
# records: 51

objectid: 2346
areaname: Albany
st: NY

objectid: 1593
areaname: Annapolis
st: MD

objectid: 974
areaname: Atlanta
st: GA

--- and 47 more ---
```

Observing each of the parameters in the URL helps explain what this is asking to be returned (note the above URL is  encoded and below are decoded to explain easier, see https://developers.google.com/maps/url-encoding for info on encoding):

- `where=captial='Y'` This required item looks and acts like the where clause in a standard SELECT statement. For this example, only data that have a `Y` character in the field `capitals` will be returned. The where clause is arguably the most important part of the query in that it limits what will be returned where the boolean clause is true for each record searched. Sometimes, particularly to debug, you want to return all data so you can include a WHERE of `1=1` to force it to return everything, since 1 is always equal to 1 (evalutes to TRUE), every record is returned!
- `outFields=objectid,areaname,st` This is another required item and specifies which fields will be returned by the query. If you wish to return all fields, place a `*` as the value in this field. 
- `orderByFields=areaname` The query will return records in whatever order they are found unless you specify a field to order the data. In this case, it will be ordered (sorted) by the contents of the field `areaname` in the returned data. 
- `f=html` This was already discussed and returns the data in the HTML (person) view with links etc. 

There are also ways to query using a geographic extent, and only return data that fall within that area. 

https://sampleserver6.arcgisonline.com/arcgis/rest/services/USA/MapServer/0/query?where=capital%3D%27Y%27&geometry=%7Bxmin%3A+-104%2C+ymin%3A+35.6%2C+xmax%3A+-94.32%2C+ymax%3A+41%7D&geometryType=esriGeometryEnvelope&spatialRel=esriSpatialRelIntersects&outFields=objectid%2Careaname%2Cst&returnGeometry=true&orderByFields=areaname&f=html

### Query Results:
```
# records: 2

objectid: 2118
areaname: Lincoln
st: NE
Point:
X: -96.67534491599997
Y: 40.80986809400008

objectid: 1406
areaname: Topeka
st: KS
Point:
X: -95.68950812299994
Y: 39.03919994000006
```

This URL builds on the previous URL parameters and adds the following:

- `geometry={xmin: -104, ymin: 35.6, xmax: -94.32, ymax: 41}` This is the heart of the additional query. It creates an additional limiter to evaluate all of the data where only those records that fall within these coordinates will be returned
- `spatialRel=esriSpatialRelIntersects` This couples with the geometry to determine how the spatial limiting will occur, and in this case any feature in the layer that intersects with the extent provided in the `geometry` parameter will be returned. 
- `returnGeometry=true` This parameter makes the data returned include the geometry associated with each record. Because this is point data, a point will be returned. But note, it doesn't return a map--it returns the actual vectors that make up the geometry and it would be the job of the application to display that! 

There are many more options in the Query tool, but this gives you a start. Now, dive into trying to build some queries yourself. 

## ***Try it***: Cities layer query

Using the Cities layer (https://sampleserver6.arcgisonline.com/arcgis/rest/services/USA/MapServer/0) query and return all records, and the geometry and fields for each within the state (field name `st`) of Georgia (which the data uses just the 2 character short form, `GA` for this). Order the results by population in 2000 in descending order (field `pop2000 desc`). Some notes to help you get started:

- Use the previous example as a starting point, but be sure to remove the Input Geometry, since we do not want to limit our search area to that geography.
- String values must be put into single quotes. So in this case, `'GA'` would be the proper way to provide the string in the where clause. 
- The operator to use in the where clause is `=` (equals). 
- We are going to be returning all fields, so change the out fields to be just a single star `*` character. 
- Ordering your results in descending order requires you to specify the field `pop2000` followed by the notation to make it reverse order from biggest to smallest using `desc'. 

<details><summary>Click for Answer</summary>

### Answer
```
# records: 82

objectid: 974
areaname: Atlanta
class: city
st: GA
capital: Y
pop2000: 416474
Point:
X: -84.40317593599997
Y: 33.75950604800005

objectid: 975
areaname: Augusta-Richmond County
class: city (consolidated, balance)
st: GA
capital: N
pop2000: 195182
Point:
X: -82.02204799199995
Y: 33.43327105000003

--- truncated, total 82 records returned ---
```

> Note: If using the HTML form all fields in the form will appear in the parameters, even if no value is provided and the parameter is equal to nothing. The answer below shows ONLY the fields required to make the query work, but if your answer has all parameter values included and gets the same results then it is correct!
> 
> -  https://sampleserver6.arcgisonline.com/arcgis/rest/services/USA/MapServer/0/query?where=st+%3D+%27GA%27&outFields=*&returnGeometry=true&orderByFields=pop2000+desc&f=html
> 

</details>

## ***Try it***: What earthquake damaged the most houses?

In the same server, return to the root of the ArcGIS Rest Endpoint (https://sampleserver6.arcgisonline.com/arcgis/rest/services) and look for the Earthquakes since 1970's MapServer and use the Query method to answer this question:

How many earthquakes occurred that were at least 8.3 magnitude?

Tips: 

- On the layer in the map service, you can review the fields to understand their data types. https://sampleserver6.arcgisonline.com/arcgis/rest/services/Earthquakes_Since1970/MapServer/0
- 8.3 is a number, so you want to use an appropriate operator to evaluate the statement to match the requirements. Take a look at the documentation to learn what operators are possible on the query where parameter (https://developers.arcgis.com/rest/services-reference/enterprise/query-feature-service-layer-.htm)

<details><summary>Click for Answer</summary>

### Answer
 
 ```
 # records: 7
 
 objectid: 763
 year_: 1994.0
 
 --- TRUNCATED TO SAVE SPACE ---
 ```
> 
> https://sampleserver6.arcgisonline.com/arcgis/rest/services/Earthquakes_Since1970/MapServer/0/query?where=magnitude+%3E%3D+8.3&outFields=*&returnGeometry=false&f=html
> 
> Did you only get 3? The question asked for AT LEAST 8.3, so you must include 8.3 by using the operator `>=` (greater than or equal) and not just `>` (greater than)
> 
> ### Bonus:
> 
> The question was for the number of earthquakes, and there is a parameter called `returnCountOnly=true` that would do this and be quicker to respond with only a count of the number of records. Can you just return the count?
> 
 
</details>

## ***Try it***: What were the Atlantic hurricane's names in 2000?

Using the MapServer at https://sampleserver6.arcgisonline.com/arcgis/rest/services/AGP/Hurricanes/MapServer, can you find the distinct names for the 14 hurricanes?

Tips:

- There is a parameter to return distinct values (each only once). 
- You must return only the field that contains the name. Not sure which field that is? Try looking at the data by creating a 1=1 WHERE query to look through all data returned.

<details><summary>Click for Answer</summary>

### Answer

> https://sampleserver6.arcgisonline.com/arcgis/rest/services/AGP/Hurricanes/MapServer/0/query?where=1%3D1&outFields=EVENTID+&returnGeometry=false&returnDistinctValues=true&f=html
>
</details>

# ArcGIS REST Feature Services

The Feature Service allows you to interact with the actual vector geometries and is much more capable than the Map Service. A MapServer has cartography pre-defined, so you can just request a map and it will be displayed using that. A FeatureServer typically does not have information on how to display the layers contained in the service. But the same QUERY method exists for FeatureServer services as does MapServer services! 

Sometimes it even makes sense to have both a MapServer and FeatureServer published together, since the FeatureServer allows for editing rights and can be secured to be accessed only with a username and password, while the MapServer can share that same data live with edits! Take a look at these two services, one is a MapServer and the second is a MapServer. They are the same data shared and point to the same layer in the Enterprise geodatabase on the server (a requirement for web editing capabilities), but each has slightly different capabilities in the REST endpoint. 

https://sampleserver6.arcgisonline.com/arcgis/rest/services/Recreation/MapServer/0
https://sampleserver6.arcgisonline.com/arcgis/rest/services/Recreation/FeatureServer/0/


The FeatureServer actually has editing enabled and is public so anyone can edit the data! You can see this by the provided supported operations:

**Supported Operations:**   Query   Query Attachments   Query Analytic   Apply Edits   Add Features   Update Features   Delete Features   Calculate   Validate SQL   Generate Renderer   Return Updates   Iteminfo   Thumbnail   Metadata

Not a good idea for some purposes, but if you want the public to be able to submit data this is what is required. Just recognize that anyone understanding these tools could go through and "delete" the data at any time if they know how to use this rest endpoint interface. 

# Conclusion

Now you know the basics of how to navigate the REST API used in ArcGIS Online and ArcGIS Server (which is part of ArcGIS Enterprise). Using the documentation provided at https://developers.arcgis.com/rest/services-reference/enterprise/what-s-new.htm you can explore and use the interface to directly query services without an application!
