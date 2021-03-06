![MapmyIndia APIs](https://www.mapmyindia.com/api/img/mapmyindia-api.png)
# MapmyIndia Geo-Analytics APIs
## (With MapmyIndia Interactive Map JS Library)

## Version History

| Version | Last Updated | Author |
| ---- | ---- | ---- |
| 3.2 | 24 February 2020 | MapmyIndia API Team ([NS]())
| 3.1 | 20 May 2019 | MapmyIndia API Team ([NS]())
| 3.0 | 02 April 2019 | MapmyIndia API Team ([NS]())
| 1.0 | 14 Jan 2019 | MapmyIndia API Team ([NS]()) |
| 1.0 | 03 August 2018 | MapmyIndia API Team ([NS]())

## Live Demo

### [GeoAnalytics Sample Web App](https://www.mapmyindia.com/api/advanced-maps/doc/sample/mapmyindia-maps-geoanalytics-apis)

## Getting Started

### Compatible Web Browsers
1. Google Chrome (Version 67 and above)
2. Mozilla Firefox (Version 60 and above)

### URL for the MapmyIndia Interactive Map JS

`https://apis.mapmyindia.com/advancedmaps/v1/your_map_key_here/map_load?v=1.3&plugin=geoanalytics`

**where**: 
`plugins` available are: 

1. `kml`: to display kml overlays over MapmyIndia Maps.
2. `geoanalytics`: to use MapmyIndia Geo-Analytics Core APIs with MapmyIndia as basemap layer.
3. `cluster`: to use a simple clustering with MapmyIndia Maps.
4. `prunecluster`: to use advanced clustering with MapmyIndia Maps.
5. `path.drag`: to enable drag-able polyline based objects with MapmyIndia Maps.
6. `editable`: to draw editable polygon overlays on MapmyIndia Maps.

## Fetching & Displaying overlays using GeoAnalytics APIs

### Getting Layers
This method gets the layer specified which is stored in MapmyIndia’s Database and gives a WMS layer as an output with any filters or styles specified by the user. 
Example: `geoAnalytics.getState`, `geoAnalytics.getCity`, `geoAnalytics.getPincode`, etc.


#### Method name
`geoAnalytics.get<LayerName>`

where: 
- LayerName is the [list of layers(APIs) available](#layers).

#### Parameters
Parameters are sent to the APIs as **`geoparams`**
1. `AccessToken` (Mandatory; string): These APIs follow OAuth2 based security. To know more how to create your authorization tokens, please use our authorization URL. More details are available [here](https://www.mapmyindia.com/api/advanced-maps/doc/authentication-api.php)
2. `GeoBoundType` (String; Mandatory): The type of geographical extents on which data would be bound, i.e. the parent layer types (India, State, District, Sub District, etc.)
**Note**: To get the list of available parent layer types, contact [apisupport@mapmyindia.com](mailto:apisupport@mapmyindia.com)
3. `GeoBound` (Array of Strings; Mandatory): The values of the extent depending on the GeoBoundType. (Array of Names)
**Note**: To fetch the list of available types, see the Listing API [here](https://github.com/MapmyIndia/mapmyindia-geoanalytics-api-web/blob/master/listingAPI.md).
4. `Attribute` (String; Optional): The name of Attribute to filter the output, such as population or number of households.
**Note**: To see the list of available parent layer types, contact [apisupport@mapmyindia.com](mailto:apisupport@mapmyindia.com)
5. `Query` (String; Optional*):  A string containing an operator and a value which would be applied to the attribute filter. Applicable queries include < (Less than) OR > (Greater then) OR <> (Between). 
Example 1: ‘> 10000’
Example 2: BETWEEN `value1` AND `value2`
***Note**: `Query` is mandatory if `Attribute` is given.
6. `Style` (Object; Optional): 
	- `Label` (Boolean; Optional*): Value to display labels. Set as true OR false.
	- `LabelColor`(Hex Value; Optional*): Value of the color of label. 
	- `LabelSize`(Number; Optional*): Size of labels to be displayed. 
	- `FillColor`(Hex Value; Optional*): Value of the polygon/point color. 
	- `PointSize`(Number; Optional*): Size of point data.  (Applicable for Point geometry only)
	- `BorderColor`(Hex Value; Optional*): Value of the color of the label. 
	- `BorderWidth`(Number; Optional*): Width of the polygon border. 
	- `Opacity`(Float; Optional*): Opacity value of whole layer. (Any range between 0 & 1)
		***Note**: All starred parameters are mandatory if `Style` is given.

#### Example
```js
var geoParams = 
{
	AccessToken		:	'xxxx-xxxxx-xxxxxxxx-xxxxxx-xxxx',
	GeoBoundType	:	'stt_nme',
	GeoBound		:	['haryana'],
	Attribute		:	't_p',
	Query			:	'>10000',
    Style: 
		{
			Label		:	true,
			LabelColor	:	'13592e',
			LabelSize	:	10,
			FillColor	:	'ffe0aa',			  
			BorderColor	:	'13592e',
			BorderWidth	:	2,
			Opacity		:	0.5
        }
};
var GeoDataLayer = geoAnalytics.getPanchayat(geoParams);
map.addLayer(GeoDataLayer);
```

#### <a name="layers"></a>APIs: List of Available Layers
1. getState
2. getDistrict
3. getSubdistrict
4. getTown
5. getCity
6. getPincode
7. getWard
8. getLocality
9. getPanchayat
10. getBlock
11. getVillage
12. getSubLocality
13. getSubSubLocality

## Layers and Attributes
To get the list of available layer's and attribute's names, please use the Listing API [available here](https://github.com/MapmyIndia/mapmyindia-geoanalytics-api-web/blob/master/listingAPI.md).

## Getting Started

Now that you’re all caught up with the features, let's get down right to them and look at how you can  integrate our Interactive Map JS API in conjunction with the above geoAnalytics methods to add data on that map to your Website from scratch.

### Initializing The Map
Follow the documentation of [Interactive Map API](https://www.mapmyindia.com/api/advanced-maps/doc/interactive-map-api) to integrate MapmyIndia Interactive Maps into your existing code base.

### Adding Your First DataLayer
To add a `DataLayer` to the map, go through the following steps after declaring the map object:

- First, declare the `DataLayer` object

```js
var geoParams =
{
	AccessToken		:	'xxxx-xxxxx-xxxxxxxx-xxxxxx-xxxx',
	GeoBoundType	: 	'stt_nme',
	GeoBound	: 	['haryana'],
	Attribute		:	't_p',
	Query		:	'>10000',
	Style		:	
		{
	        Label	:	 true,
	        LabelColor	: 	'13592e',
	        LabelSize	: 	10,
	        FillColor	: 	'ffe0aa',
			BorderColor	 :	 '13592e',
			BorderWidth  :	 2,
			Opacity	: 	0.5
		}
};
```
- Second, declare the `GeoDataLayer` object by calling new `geoAnalytics.get<layerName>` method in the JavaScript and passing the above created `geoParams` object in it.
```js
var GeoDataLayer = geoAnalytics.getPanchayat(geoParams); // for panchayat layer
```
- Third, Add the `GeoDataLayer` object on the map on the map object created above:
```js
map.addLayer(GeoDataLayer);
```
- Finally, call the MapmyIndia’s Listing APIs to get the bounding box of the `DataLayer` to set the bounds of the map with respect to the `DataLayer` . Refer to the Listing API documentation for more information  (Alternatively call the new `geoAnalytics.setBounds` method in the JavaScript and pass it layer name, `geoParams` and map objects in it to set the bounds of map to the bounding box of `GeoDataLayer`. 
```js
geoAnalytics.setBounds('pincode',geoParams,map); // for pincode layer
```
### Info Windows
Info Windows are a convenient way of showing data about a point in the `DataLayer`. The expected behaviour of a user to know about any point in the `DataLayer` is to try and click on it to know what it is all about. The mechanism to accomplish this is by showing an info window.
The info window for a `DataLayer`(created previously) can be obtained through following steps:
- Create a click event on the map.
```js
map.on('click', function(e) 
{
// e stands for the event in which the click happens
});
```
- Declare the attribute names in propertyName  that you want to see in the info  window.
```js
map.on('click', function(e) 
{
var propertyName = 'stt_nme,stt_id,t_p,t_m,t_f,label';
});
```
- Call a new `geoAnalytics.getFeatureInfo` method in the JavaScript and pass the `event`, `propertyName` and `GeoDataLayer` in it. This will give json response in which all the information for the requested attribute will be available.
```js
map.on('click', function(e) 
{
var propertyName = 'stt_nme,stt_id,t_p,t_m,t_f,label';
var Infodata = geoAnalytics.getFeatureInfo(e,propertyName,GeoDataLayer);
});.
```
- Create a variable html and add the data into it.
```js
map.on('click', function(e) 
{
var propertyName = 'stt_nme,stt_id,t_p,t_m,t_f,label';
var Infodata = geoAnalytics.getFeatureInfo(e,propertyName,GeoDataLayer);
var html = "";
if(Infodata.features[0])
	{
	html += "<div class='mainlabel_details'><label class='label_name'>Town Name:</label> " + Infodata.features[0].properties["twn_nme"] + "</div> ";
	html += "<div class='mainlabel_details'><label class='label_name'>State ID:</label> " + Infodata.features[0].properties["stt_id"] + "</div>";
	html += "<div class='mainlabel_details'><label class='label_name'>State Name:</label> " + Infodata.features[0].properties["stt_nme"] + "</div> ";
    html += "<div class='mainlabel_details'><label class='label_name'>Total Population:</label> " + Infodata.features[0].properties["t_p"] + "</div> ";
    
          	  }
	  else if(Infodata.features[0] == undefined)
	  console.log("Not Exists");
	}
);
```
- Finally, add the info window to the map by creating a leaflet popup.
```js
map.on('click', function(e) 
{
var propertyName = 'stt_nme,stt_id,t_p,t_m,t_f,label';
var Infodata = geoAnalytics.getFeatureInfo(e,propertyName,GeoDataLayer);
var html = "";
if(Infodata.features[0])
	{
	html += "<div class='mainlabel_details'><label class='label_name'>Town Name:</label> " + Infodata.features[0].properties["twn_nme"] + "</div> ";
	html += "<div class='mainlabel_details'><label class='label_name'>State ID:</label> " + Infodata.features[0].properties["stt_id"] + "</div>";
	html += "<div class='mainlabel_details'><label class='label_name'>State Name:</label> " + Infodata.features[0].properties["stt_nme"] + "</div> ";
    html += "<div class='mainlabel_details'><label class='label_name'>Total Population:</label> " + Infodata.features[0].properties["t_p"] + "</div> ";

    L.popup({ maxWidth: 800})
      .setLatLng(e.latlng)
      .setContent(html)
      .addTo(map);
          	  }
	  else if(Infodata.features[0] == undefined)
	  console.log("Not Exists");
	}
);
```

## Examples

### getState (some states with default style)
![getState](https://mmi-api-team.s3.ap-south-1.amazonaws.com/geoAnalyticsApiImages/someStateswithDefaultstyling.png)

### getState (all states with default style)
![getState](https://mmi-api-team.s3.ap-south-1.amazonaws.com/geoAnalyticsApiImages/allstate.PNG)

### getCity(city with default style)

![getCity](https://mmi-api-team.s3.amazonaws.com/geoAnalyticsApiImages/getCity.png)

### getDistrict (all districts of one state with default style)
![getDistrict](https://mmi-api-team.s3.amazonaws.com/geoAnalyticsApiImages/districtswithCustomstyling.png)



For any queries and support, please contact: 

![Email](https://www.google.com/a/cpanel/mapmyindia.co.in/images/logo.gif?service=google_gsuite) 
Email us at [apisupport@mapmyindia.com](mailto:apisupport@mapmyindia.com)

![](https://www.mapmyindia.com/api/img/icons/stack-overflow.png)
[Stack Overflow](https://stackoverflow.com/questions/tagged/mapmyindia-api)
Ask a question under the mapmyindia-api

![](https://www.mapmyindia.com/api/img/icons/support.png)
[Support](https://www.mapmyindia.com/api/index.php#f_cont)
Need support? contact us!

![](https://www.mapmyindia.com/api/img/icons/blog.png)
[Blog](http://www.mapmyindia.com/blog/)
Read about the latest updates & customer stories


> © Copyright 2019. CE Info Systems Pvt. Ltd. All Rights Reserved. | [Terms & Conditions](http://www.mapmyindia.com/api/terms-&-conditions)
>  Written with [StackEdit](https://stackedit.io/) by MapmyIndia.