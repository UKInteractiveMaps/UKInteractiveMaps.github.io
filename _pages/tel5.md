---
title: Home
permalink: /index.html
layout: none
---
<html xmlns="http://www.w3.org/1999/xhtml"> 
<head> 
<title></title> 
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" /> 
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.3.0/dist/leaflet.css" />
<link rel="stylesheet" href="/css/leaflet-search.css" />
<link rel="stylesheet" href="/css/style.css" />
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>
<style>
#findbox {
background: #eee;
border-radius:.125em;
border:2px solid #1978cf;
box-shadow: 0 0 8px #999;
margin-bottom: 10px;
padding: 2px 0;
width: 600px;
height: 26px;
}
.search-tooltip {
width: 200px;
}
.leaflet-control-search .search-cancel {
position: static;
float: left;
margin-left: -22px;
}
</style>
</head>
<body onload="getStreams()">
<table style="width:100%">
<tr>
<td><div id="findbox"></div>
<div id="map"></div></td>
<td id="info"></td>
</tr>
</table>
<div style="display:none" id="list"></div>
<div id="list2"></div>
<script src="https://unpkg.com/leaflet@1.3.0/dist/leaflet.js"></script>
<script src="/js/leaflet-search.js"></script>
<script src="/js/us-states.js"></script>
<script>
//sample data values define in us-states.js
var map = new L.Map('map', {zoom: 5, center: new L.latLng([55, -2]) });
map.addLayer(new L.TileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png'));//base layer
var dude77 = [];
var dude78 = [];
var uktownstate = {"type":"FeatureCollection","features":[dude77]};
var data = statesData;
var data2 = uktownstate;
let text = "";
let text2 = "";
document.getElementById("list2").innerHTML = text2;
myfruit = {};
let xx = 0;
function getStreams() {
  //let httpRequest;
  let url = [0, 20, 40, 60, 80, 100, 120, 140, 160, 180, 200, 220, 240, 260, 280, 300, 320, 340, 360, 380, 400, 420, 440, 460, 480, 500, 520, 540, 560, 580, 600, 620, 640];
  function makeRequest() {
    url.forEach(async function(e) {
      let httpRequest = new XMLHttpRequest();
      if (!httpRequest) {
        alert("can not create http instance!");
        return false;
      }
      httpRequest.onreadystatechange = streams;
      httpRequest.open('GET', 'https://members-api.parliament.uk/api/Location/Constituency/Search?skip='+e+'&take=20');
      httpRequest.send();
    });
  }
  function streams() {
    if (this.readyState === this.DONE) {
        let data = JSON.parse(this.response);
		let e = 0;
		const f = e++;
		var data2 = data.items;
		var data55 = data2.value;
		let a = -1;
		document.getElementById("list2").innerHTML = text2;
		data2.forEach((data2, index) => {
		if(data2.value.currentRepresentation == undefined){var data66 = 'Undefined'}else{var data66 = data2.value.currentRepresentation.member.value.latestParty.name};
		if(data66 == 'Undefined'){var color = '#86848A'};
		if(data66 == 'Labour'){var color = '#Ff0000'};
		if(data66 == 'Scottish National Party'){var color = '#Fff800'};
		if(data66 == 'Conservative'){var color = '#0038FF'};
		if(data66 == 'Democratic Unionist Party'){var color = '#50A9D4'};
		if(data66 == 'Plaid Cymru'){var color = '#EF00FF'};
		if(data66 == 'Liberal Democrat'){var color = '#67A81B'};
		if(data66 == 'Sinn Féin'){var color = '#6900FF'};
		if(data66 == 'Independent'){var color = '#FFFFFF'};
		if(data66 == 'Social Democratic & Labour Party'){var color = '#FF9E00'};
		if(data66 == 'Alba Party'){var color = '#56A1A4'};
		if(data66 == 'Green Party'){var color = '#38FF00'};
		if(data66 == 'Labour (Co-op)'){var color = '#F7005A'};
		if(data66 == 'Speaker'){var color = '#000000'};
		if(data66 == 'Alliance'){var color = '#00FDFF'};
		let httpRequest1 = new XMLHttpRequest();
		httpRequest1.onreadystatechange = function(){
    	if(this.readyState == 4 && this.status == 200){
		var str2 = this.responseText;
		const after_ = str2.split('coordinates')[1];
		const after66_ = str2.split('type')[1];
		const after66a_ = after66_.substring(5);
      	const after1_ = after_.substring(3);
	  	const before_ = after1_.split('}')[0];
		const before66a_ = after66a_.split(',')[0];
		const before66b_ = before66a_.replace('"', '');
		const before66c_ = before66b_.split('n')[0]+'n';
		//const before66d_ = before66c_+'n';
		//console.log(before66c_);
    	//2
		++a;
		console.log(a);  
	   	console.log(data2.value.id +' - '+data66+' - '+data2.value.name+' - '+color+' - '+before66c_+' - '+before_);
		dude78.push({"type":"Feature","id":"3298","properties":{"name":"Ashton-under-Lyne","density":63.50},"geometry":{"type":"Polygon","coordinates":[[[-2.150474,53.472571],[-2.161498,53.474875],[-2.16965,53.486775],[-2.163386,53.496724],[-2.178685,53.505833],[-2.173218,53.51212],[-2.156231,53.5158],[-2.146436,53.521038],[-2.137239,53.515123],[-2.133415,53.508903],[-2.118281,53.505729],[-2.103361,53.509626],[-2.092124,53.520599],[-2.061846,53.522365],[-2.056528,53.513399],[-2.056494,53.505455],[-2.068884,53.496795],[-2.068265,53.492058],[-2.074903,53.480737],[-2.075835,53.482685],[-2.100914,53.481646],[-2.111759,53.46762],[-2.122242,53.482833],[-2.128188,53.485759],[-2.150474,53.472571]]]}});
		dude77.push({"type":"Feature","id":""+data2.value.id+ "","properties":{"name":""+data2.value.name+"","color":""+color+"","party":""+data66+""},"geometry":{"type":""+before66c_+"","coordinates":""+before_}});
    	}	
  	};
	httpRequest1.open('GET', 'https://members-api.parliament.uk/api/Location/Constituency/'+data2.value.id+'/Geometry');
      httpRequest1.send();
	  text2 += data2.value.id+" - "+data2.value.name+" - "+data66+"<br>";
});
}
  }
  makeRequest();
}
//const myArr = JSON.parse(dude77);
//	console.log(myArr[0]);
const fruits = data.features;
fruits.forEach(myFunction);
document.getElementById("list").innerHTML = text;
const fruits2 = data2.features;
console.log(dude78);
console.log(fruits[1].id);
fruits2.forEach(pleasework);
function pleasework(item, index) {
	console.log(item.properties);
	console.log(Object.keys(item));
	console.log(item.length);
}
function myFunction(item, index, emp1) {
text += index + ": " + item.properties.name + "<br>";
$.ajax({
/*
url: 'http://members-api.parliament.uk/api/Location/Constituency/'+item.id,
success: function(response) {
document.getElementById("list2").innerHTML = text2;
//console.log(response.value.currentRepresentation);
var dude6= response.value.currentRepresentation.member.value.latestParty.name;
text2 += index + ": " + dude6 + " - " + item.id + " - " + item.properties.name + "<br>";
},
error: function(error) {
//Do Something to handle error
console.log(error);
}
*/
});
/*
$.getJSON('http://members-api.parliament.uk/api/Location/Constituency/'+item.id, function(emp1) {
var dude5 = emp1.value.currentRepresentation.member.value.latestParty.name;
if (dude5 === undefined || dude5.value === null) {
console.log("bullshit");
}else {
	//text2 += index + ": " + dude5 + "- " + item.id + " - " + item.properties.name + "<br>";
	console.log(dude5, item.properties.name);
	}
});
*/
}
function mapcolor() {
 // alert("Page is loaded");
}
var featuresLayer = new L.GeoJSON(data, {
style: function(feature) {
return {color: feature.properties.color };
},
onEachFeature: function(feature, marker,) {
marker.bindPopup('<h4 style="color:'+feature.properties.color+'">'+ feature.properties.name +'<br /><button onclick="stateinfo(this, \''+ feature.id +'\')">'+''+'Click Here For more info</button></h4>');
}
});
map.addLayer(featuresLayer);
var searchControl = new L.Control.Search({
container: 'findbox',
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
featuresLayer.eachLayer(function(layer) {//restore feature color
featuresLayer.resetStyle(layer);
});
});	
map.addControl(searchControl);//inizialize search control
function stateinfo(element, color) {
//console.log(color);
let country = data.features.find(el => el.id === color);
//console.log(country.properties["name"]);
const info = document.getElementById("info");
info.innerHTML = country.properties["name"];
const para = document.createElement("div");
para.setAttribute("id", "info1");
para.setAttribute("class", "header");
const para2 = document.createElement("div");
para2.setAttribute("id", "info2");
para2.setAttribute("class", "header");
const para3 = document.createElement("div");
para3.setAttribute("id", "info3");
para3.setAttribute("class", "header");
para.innerHTML = color;
para2.innerHTML = color;
para3.innerHTML = color;
info.appendChild(para);
info.appendChild(para2);
info.appendChild(para3);
$.getJSON('https://members-api.parliament.uk/api/Location/Constituency/'+color, function(emp) {
$('#info1').html('<p>Constituency Name: ' + emp.value.name + '</p>');
$('#info1').append('<p>MP Name : ' + emp.value.currentRepresentation.member.value.nameFullTitle + '</p>');
$('#info1').append('<img src="' + emp.value.currentRepresentation.member.value.thumbnailUrl + '" alt="' + emp.value.currentRepresentation.member.value.nameFullTitle + '" width="100">');
$('#info1').append('<p>Party: '
+ emp.value.currentRepresentation.member.value.latestParty.name
+ '</p>');
});
$.getJSON('https://members-api.parliament.uk/api/Location/Constituency/'+color+'/Synopsis', function(emp1) {
$('#info2').html('<p>Member Info: ' + emp1.value + '</p>');
});
$.getJSON('https://members-api.parliament.uk/api/Location/Constituency/'+color+'/ElectionResults', function(emp3) {
	var dude5 = emp3.value;
$('#info3').html('<p>Electorate Info: ' + dude5[0].electorate + '</p>');
$('#info3').append('<p>Majority : ' + dude5[0].majority + '</p>');
$('#info3').append('<p>Turnout : ' + dude5[0].turnout + '</p>');
});
}
</script>
</body>
</html>
