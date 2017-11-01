*** To run locally, make sure to change the line 112 to: d3.csv('/crimeLog.csv', function(error, crime_log_data) {

# Georgia Tech Crime Map - Tutorial Guide

## Goal
We will be using the D3 and Leaflet libraries and basic HTML and CSS to create a map visualization of the crimes that have occurred in Georgia Tech's campus in 2016. The goal of this workshop/tutorial guide is to provide the basic concepts of data visualization with D3 and encourage campus-wide interest in data visualization. No prior programming experience is required.

## References
1. HTML & CSS for Beginners https://www.codecademy.com/en/tracks/htmlcss
2. Leaflet API http://leafletjs.com/reference-1.2.0.html 
3. D3 API https://github.com/d3/d3/blob/master/API.md
4. D3: Thinking with Data Joins: https://bost.ocks.org/mike/join/
5. D3: General Update Pattern (Part 1 of 3): https://bl.ocks.org/mbostock/3808218

## Tutorial Outline
1. HTML Basics: Setting up the webpage structure
2. CSS Basics: Styling up the webpage
3. Incorporating Leaflet: Making the map
4. Incorporating D3: Importing Data + Making the listview and map interactive

## Tutorial 

### 1. HTML Basics: Setting up our webpage structure
HTML stands for **HyperText Markup Language** and gives webpages its structure. The “HyperText” part means “text with links” and a “Markup Language” is used to code and format layouts and styles. 

First, create a file titled **index.html**. This file will hold the code for the home webpage. To see what our webpage looks like, we open the HTML file using our browser. The browser will render the HTML and other files, and it will allow us to view the page.

Things inside **<>** are called **tags**. Tags usually come in pairs with an opening tag and a closing tag, but there are some tags that do not need a closing tag like &lt;img/&gt; for images and &lt;link/&gt; (which we will look into soon). Tags also have **attributes**, which provide additional information about the element. Attributes are specified in the starting tag, and they come in **name/value pairs (for example, name=”value”)**. 

In HTML, we can make comments by surrounding the content with “&lt;!--” in the beginning and “--&gt;” in the end. So for example if we wanted to comment some content, we type:  
```
<!-- [content that is commented out] -->
```

You can place one HTML tag inside of another. This is called **nesting**.

In the beginning of your index.html file and every HTML file that you write, put **&lt;!DOCTYPE html&gt;** on the first line. This tag will let the browser know what language it's reading (in this case, HTML).

In the next line, type **&lt;html&gt;**. This opening tag will start the HTML document. Then in the next line, type **&lt;/html&gt;**. This closing tag will end the HTML document. All of the HTML that you will write in this document will be inside the <html> tag.

There are always two parts to an HTML file, a **&lt;head&gt;** tag and a **&lt;body&gt;** tag. 

The **&lt;head&gt;** tag contains information about the HTML file, such as the title and links to other files and libraries. 

We will now add tags inside of the **&lt;head&gt;** tag.
To display a title on the browser’s page tab: type 
```
<title>Georgia Tech 2016 Crime Map</title> 
```

We can add a comment to specify that we are going to import D3 and Leaflet and our stylesheet into our webpage. To do so, type:
```
<!-- import D3 and Leaflet and our stylesheet-->
```

To link our webpage to the D3 library, type:	
```
<script src="https://d3js.org/d3.v4.min.js"></script>
```

To link our webpage to the leaflet library, type:
```
<script src="https://unpkg.com/leaflet@1.0.3/dist/leaflet.js"></script>
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.3/dist/leaflet.css" />
```
  
To link our webpage to our styles sheet (which we will create in the next section and use to style our webpage), type:
```
<link rel="stylesheet" type="text/css" href="stylesheet.css" /> 
```

After all those steps, the **&lt;head&gt;** tag should look like this:
```
<head>
	<title>Georgia Tech 2016 Crime Map</title>
	<!-- import D3 and Leaflet and our stylesheet-->
	<script src="https://d3js.org/d3.v4.min.js"></script>
	<script src="https://unpkg.com/leaflet@1.0.3/dist/leaflet.js"></script>
	<link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.3/dist/leaflet.css" />
	<link rel="stylesheet" type="text/css" href="stylesheet.css" />
</head>
```

The **&lt;body&gt;** tag contains all the content that will be visible on your web page, such as text and images. 
In the **&lt;body&gt;** tag, we are going to be using **&lt;div&gt;** tags to structure our webpage. The **&lt;div&gt;** **&lt;/div&gt;** tags allows you to divide your page into different containers and pieces. It is short for “division”.

We will have a **&lt;div&gt;** to be the container that will hold all of our content. We set the id attribute of this div to “container”.
Inside of **&lt;div id="container"&gt;** **&lt;/div&gt;**, we will add and nest another **&lt;div&gt;** **&lt;/div&gt;** tag for our header. We set the id attribute of this div to “header”.

Likewise, inside of **&lt;div id="container"&gt;** **&lt;/div&gt;** we will do the same for creating a **&lt;div&gt;** **&lt;/div&gt;** for “content_area” and another **&lt;div&gt;** **&lt;/div&gt;** for “footer”.

Inside of the **&lt;div id="content_area"&gt;**, we will create more **&lt;div&gt;** **&lt;/div&gt;** tags to structure the webpage. Create a **&lt;div&gt;** **&lt;/div&gt;** with id attribute set to “left_col”. Create a **&lt;div&gt;** **&lt;/div&gt;** with id attribute set to “right_col”.

Inside of **&lt;div id="right_col"&gt;**, add another **&lt;div&gt;** **&lt;/div&gt;** with id attribute “mapid”. 
**&lt;div id="mapid"&gt;** **&lt;/div&gt;** will contain our map visualization.

We will specify the sizes of these **&lt;div&gt;** **&lt;/div&gt;** in the css file.

Your HTML code should now look like this:
```
<!DOCTYPE html>
<html>
<head>
	<title>Georgia Tech 2016 Crime Map</title>
	<!-- import D3 and Leaflet -->
	<script src="https://d3js.org/d3.v4.min.js"></script>
	<link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.3/dist/leaflet.css" />
	<link rel="stylesheet" type="text/css" href="stylesheet.css" />
	<script src="https://unpkg.com/leaflet@1.0.3/dist/leaflet.js"> </script>
</head>
<body>
	<div id="container">
	 <div id="header">
	 </div>
	 <div id="content_area">
		<div id="left_col"></div>
		<div id="right_col">
		 <div id="mapid"></div>
	 	</div>
	 </div>
		<div id="footer"></div>
	</div>
</body>
</html>
```

### 2. CSS Basics: Styling up our webpage
CSS stands for **Cascading Style Sheets** and is used to define styles for a webpage’s layout and appearance. Style sheets are files that describe the style for how an HMTL file should look like. The “Cascading” part is to resolve conflicts between style sheets by styling a webpage based on the most specific rule. We will look more into the cascading part of CSS soon.

Now, create a file called **“stylesheet.css”**. This file will contain all the CSS styling information.

Talk about CSS syntax like selectors, cascading selectors, class and id selectors, properties and values.

Adjust the size of the map

Style a header color, size, and alignment to show CSS styling

### 3. Incorporating Leaflet: Making the map
Leaflet is an open-source JavaScript library that allows us to build interactive maps that are web-friendly and mobile-friendly. 

We already linked the Leaflet library to our webpage from chapter 1. To start using Leaflet, let’s initialize the map with coordinates to Tech’s student center. First, we will use JavaScript to create a variable

```
var atl = new L.LatLng(33.77438, -84.39879);
//create map object with GT's student center at the center of map
var mymap = L.map('mapid').setView(atl, 16);
L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token={accessToken}', {
  attribution: 'Map data &copy; <a href="http://openstreetmap.org">OpenStreetMap</a> contributors, <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="http://mapbox.com">Mapbox</a>',
  maxZoom: 20,
  minZoom: 15,
  id: 'mapbox.light',
  accessToken: 'pk.eyJ1IjoiamFnb2R3aW4iLCJhIjoiY2lnOGQxaDhiMDZzMXZkbHYzZmN4ZzdsYiJ9.Uwh_L37P-qUoeC-MBSDteA'
}).addTo(mymap);
```

We will use Leaflet’s feature of building markers to mark important landmarks on Georgia Tech’s campus. 
```
var studentCenterMarker = L.marker([33.77438, -84.39879]).bindPopup('Student Center').addTo(mymap);
```

We will follow a similar pattern for the other markers that we have created. 
```
var northAvenueMarker = L.marker([33.76941, -84.39136]).bindPopup('North Avenue Apartments').addTo(mymap);
var cloughMarker = L.marker([33.77456, -84.39608]).bindPopup('Clough Commons/Library').addTo(mymap);
var bobbyDoddMarker = L.marker([33.77251, -84.39281]).bindPopup('Bobby Dodd Stadium').addTo(mymap);
var crcMarker = L.marker([33.77567, -84.40325]).bindPopup('Campus Recreation Center').addTo(mymap);
var gtpdMarker = L.marker([33.77906, -84.40143]).bindPopup('GT Police Department').addTo(mymap);
var techSquareMarker = L.marker([33.77698, -84.38924]).bindPopup('Tech Square').addTo(mymap);
var biotechQuadMarker = L.marker([33.77897, -84.39653]).bindPopup('Biotech Quad').addTo(mymap);
var greekHousesMarker = L.marker([33.77648, -84.39246]).bindPopup('Small portion of Greek houses').addTo(mymap);
var howeyPhysicsMarker = L.marker([33.77745, -84.39882]).bindPopup('Howey Physics Building').addTo(mymap);
var mccamishPavilionMarker = L.marker([33.7809, -84.39274]).bindPopup('McCamish Pavilion').addTo(mymap);
var westVillageMarker = L.marker([33.77932, -84.40462]).bindPopup('West Village Dining Commons').addTo(mymap);
var graduateLivingCenterMarker = L.marker([33.78254, -84.39646]).bindPopup('Graduate Living Center').addTo(mymap);
var woodruffMarker = L.marker([33.77913, -84.40698]).bindPopup('Woodruff Housing').addTo(mymap);
```

We will draw a boundary to show where Georgia Tech’s campus is encapsulated. Leaflet allows us to create this boundary with the polyline feature. 
First we define the longidude and latitude for Georgia Tech’s campus. We already calculated the points, so feel free to use them
```
var techBoundaryLatLngs = [
  [33.76816, -84.39059], //starting point in the bottom right at north avenue apartments
  [33.76816, -84.39213],
  [33.7703, -84.39213],
  [33.77048, -84.39599],
  [33.77269, -84.39767],
  [33.7738, -84.40221],
  [33.7754, -84.4047],
  [33.77683, -84.4063],
  [33.77904, -84.4071],
  [33.77961, -84.40714],
  [33.7820, -84.40789], //top left corner of the map
  [33.78204, -84.39076],
  [33.7783, -84.3908],
  [33.77808, -84.38677],
  [33.77458, -84.38677],
  [33.77462, -84.39059],
  [33.76816, -84.39059]
];
```

Then we will add our polyline for Georgia Tech's boundary and add it to the map.

```
var polyline = L.polyline(techBoundaryLatLngs, {
  color: 'gold'
}).addTo(mymap);
// zoom the map to the polyline
mymap.fitBounds(polyline.getBounds());
```
We will add an svg later on top of our map object so that we may write data points on the map, which we will do in a future section soon

```
var svgLayer = L.svg();
svgLayer.addTo(mymap)
```

Look at the data and point out the significant fields such as the longitude/latitude

### 4. Incorporating D3: Making the listview and map interactive

