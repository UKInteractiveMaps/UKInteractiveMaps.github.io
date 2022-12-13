---
title: Home
permalink: /test123.html
layout: none
---
<html lang="en">
<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css" />
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>

<base target="_top">
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">

<title>Choropleth Tutorial - Leaflet</title>

<link rel="shortcut icon" type="image/x-icon" href="docs/images/favicon.ico" />

<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.3/dist/leaflet.css" integrity="sha256-kLaT2GOSpHechhsozzB+flnD+zUyjE2LlfWPgU04xyI=" crossorigin=""/>
<script src="/js/leaflet.js" integrity="sha256-WBkoXOwTeyKclOHuWtc+i2uENFpDZ9YPdf5Hf+D7ewM=" crossorigin=""></script>

<style>
html, body {
height: 100%;
margin: 0;
}
.leaflet-container {
height: 400px;
width: 600px;
max-width: 100%;
max-height: 100%;
}
#result {
position: absolute;
width: 100%;
max-width:870px;
cursor: pointer;
overflow-y: auto;
max-height: 400px;
box-sizing: border-box;
z-index: 1001;
}
.link-class:hover{
background-color:#f1f1f1;
}
#map { width: 800px; height: 500px; }
.info { padding: 6px 8px; font: 14px/16px Arial, Helvetica, sans-serif; background: white; background: rgba(255,255,255,0.8); box-shadow: 0 0 15px rgba(0,0,0,0.2); border-radius: 5px; } .info h4 { margin: 0 0 5px; color: #777; }
.legend { text-align: left; line-height: 18px; color: #555; } .legend i { width: 18px; height: 18px; float: left; margin-right: 8px; opacity: 0.7; }
</style>
</head>
<body>

<div class="container" style="padding:50px 250px;">
<div id="findbox"></div>
<div id='map'></div>

<form role="form">
<div class="form-group">
<input type="input" class="form-control input-lg" id="txt-search" placeholder="Type your search character">
</div>
</form>
<div id="filter-records"></div>
</div>
</body>
</html>
<script type="text/javascript" src="/js/leaflet-search.js"></script>
<script type="text/javascript" src="/js/us-states.js"></script>
<script type="text/javascript">
const map = L.map('map').setView([56, 0], 5);
const tiles = L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
maxZoom: 19,
//attribution: '<!--&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>-->'
}).addTo(map);
// control that shows state info on hover
const info = L.control();
info.onAdd = function (map) {
this._div = L.DomUtil.create('div', 'info');
this.update();
return this._div;
};
info.update = function (props) {
const contents = props ? `<b>${props.name}</b><br />${props.density} people / mi<sup>2</sup>` : 'Hover over a state';
this._div.innerHTML = `<h4>US Population Density</h4>${contents}`;
};
info.addTo(map);
// get color depending on population density value
function getColor(d) {
return d > 1000 ? '#800026' :
d > 500  ? '#BD0026' :
d > 200  ? '#E31A1C' :
d > 100  ? '#FC4E2A' :
d > 50   ? '#FD8D3C' :
d > 20   ? '#FEB24C' :
d > 10   ? '#FED976' : '#FFEDA0';
}
function style(feature) {
return {
weight: 0.2,
opacity: 1,
color: 'white',
dashArray: '1',
fillOpacity: 0.7,
fillColor: getColor(feature.properties.density)
};
}
function highlightFeature(e) {
const layer = e.target;
layer.setStyle({
weight: 5,
color: '#666',
dashArray: '',
fillOpacity: 0.7
});
layer.bringToFront();
info.update(layer.feature.properties);
}
/* global statesData */
const geojson = L.geoJson(statesData, {
style,
onEachFeature
}).addTo(map);
function resetHighlight(e) {
geojson.resetStyle(e.target);
info.update();
}
function zoomToFeature(e) {
map.fitBounds(e.target.getBounds());
}
function onEachFeature(feature, layer) {
layer.on({
mouseover: highlightFeature,
mouseout: resetHighlight,
click: zoomToFeature
});
}
map.attributionControl.addAttribution('Population data &copy; <a href="http://census.gov/">US Census Bureau</a>');
const legend = L.control({position: 'bottomright'});
legend.onAdd = function (map) {
const div = L.DomUtil.create('div', 'info legend');
const grades = [0, 10, 20, 50, 100, 200, 500, 1000];
const labels = [];
let from, to;
for (let i = 0; i < grades.length; i++) {
from = grades[i];
to = grades[i + 1];
labels.push(`<i style="background:${getColor(from + 1)}"></i> ${from}${to ? `&ndash;${to}` : '+'}`);
}
div.innerHTML = labels.join('<br>');
return div;
};
var markersLayer = new L.LayerGroup();//layer contain searched elements
map.addLayer(markersLayer);
map.addControl( new L.Control.Search({
container: 'findbox',
layer: markersLayer,
propertyName: 'name',
initial: false,
collapsed: false
}) );
	var featuresLayer = new L.GeoJSON(data, {
			style: function(feature) {
				return {color: feature.properties.color };
			},
			onEachFeature: function(feature, marker) {
				marker.bindPopup('<h4 style="color:'+feature.properties.color+'">'+ feature.properties.name +'</h4>');
			}
		});
	map.addLayer(featuresLayer);
	var searchControl = new L.Control.Search({
		layer: featuresLayer,
		propertyName: 'name',
		marker: false,
		moveToLocation: function(latlng, title, map) {
			//map.fitBounds( latlng.layer.getBounds() );
			var zoom = map.getBoundsZoom(latlng.layer.getBounds());
  			map.setView(latlng, zoom); // access the zoom
		}
	});
	searchControl.on('search:locationfound', function(e) {
		//console.log('search:locationfound', );
		//map.removeLayer(this._markerSearch)
		e.layer.setStyle({fillColor: '#3f0', color: '#0f0'});
		if(e.layer._popup)
			e.layer.openPopup();
	}).on('search:collapsed', function(e) {
		featuresLayer.eachLayer(function(layer) {	//restore feature color
			featuresLayer.resetStyle(layer);
		});	
	});
	map.addControl( searchControl );  //inizialize search control
legend.addTo(map);
var data = [
{"id":"1","employee_name":"Tiger Nixon","employee_salary":"320800","employee_age":"61","profile_image":"default_profile.png"},
{"id":"2","employee_name":"Garrett Winters","employee_salary":"434343","employee_age":"63","profile_image":"default_profile.png"},
{"id":"3","employee_name":"Ashton Cox","employee_salary":"86000","employee_age":"66","profile_image":"default_profile.png"},
{"id":"4","employee_name":"Cedric Kelly","employee_salary":"433060","employee_age":"22","profile_image":"default_profile.png"},
{"id":"5","employee_name":"Airi Satou","employee_salary":"162700","employee_age":"33","profile_image":"default_profile.png"},
{"id":"6","employee_name":"Brielle Williamson","employee_salary":"372000","employee_age":"61","profile_image":"default_profile.png"},
{"id":"7","employee_name":"Herrod Chandler","employee_salary":"137500","employee_age":"59","profile_image":"default_profile.png"},
{"id":"8","employee_name":"Rhona Davidson","employee_salary":"327900","employee_age":"55","profile_image":"default_profile.png"},
{"id":"9","employee_name":"Colleen Hurst","employee_salary":"205500","employee_age":"39","profile_image":"default_profile.png"},
{"id":"10","employee_name":"Sonya Frost","employee_salary":"103600","employee_age":"23","profile_image":"default_profile.png"},
{"id":"11","employee_name":"Justin Grierson","employee_salary":"103600","employee_age":"23","profile_image":"default_profile.png"}
];
var dude = statesData.features
//document.write(JSON.stringify(dude));
$(document).ready(function(){
$('#txt-search').keyup(function(){
var searchField = $(this).val();
if(searchField === '')  {
$('#filter-records').html('');
return;
}
var regex = new RegExp(searchField, "i");
var output = '<div class="row">';
var count = 1;
$.each(dude, function(key, val){
if ((val.id.search(regex) != -1) || (val.properties.name.search(regex) != -1) || (val.type.search(regex) != -1)) {
output += '<div class="col-md-6 well">';
output += '<div class="col-md-3"><!--<img class="img-responsive" src="'+val.profile_image+'" alt="'+ val.employee_name +'" />--></div>';
output += '<div class="col-md-7">';
output += '<h5>' + val.id + '</h5>';
output += '<p>' + val.properties.name + '</p>'
output += '</div>';
output += '</div>';
if(count%2 == 0){
output += '</div><div class="row">'
}
count++;
}
});
output += '</div>';
$('#filter-records').html(output);
});
});
</script>