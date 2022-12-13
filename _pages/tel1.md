---
title: Home
permalink: /maps1/
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

<div id='map'></div>
<div id="findbox"></div>
<br /><br />
  <div class="container" style="width:900px;">
   <h2 align="center">JSON Live Data Search using Ajax JQuery</h2>
   <h3 align="center">Employee Data</h3>   
   <br /><br />
   <div align="center">
    <input type="text" name="search" id="search" placeholder="Search Employee Details" class="form-control" />
   </div>
   <ul class="list-group" id="result"></ul>
   <br />
  </div>
<script type="text/javascript" src="/js/us-states.js"></script>
<script src="/js/leaflet-search.js"></script>

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

legend.addTo(map);

$(document).ready(function(){
$.ajaxSetup({ cache: false });
$('#search').keyup(function(){
$('#result').html('');
$('#state').val('');
var searchField = $('#search').val();
var expression = new RegExp(searchField, "i");
$.getJSON('/data.json', function(data) {
$.each(data, function(key, value){
if (value.name.search(expression) != -1 || value.location.search(expression) != -1)
{
$('#result').append('<li class="list-group-item link-class"><img src="'+value.image+'" height="40" width="40" class="img-thumbnail" /> '+value.name+' | <span class="text-muted">'+value.location+'</span></li>');
}
});
});
});
$('#result').on('click', 'li', function() {
var click_text = $(this).text().split('|');
$('#search').val($.trim(click_text[0]));
$("#result").html('');
});
});
</script>
</body>
</html>