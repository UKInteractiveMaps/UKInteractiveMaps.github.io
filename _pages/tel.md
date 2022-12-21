---
title: Home
permalink: /maps/
layout: none
---
<html lang="en" >

<head>

  <meta charset="UTF-8">
  
<link rel="apple-touch-icon" type="image/png" href="https://cpwebassets.codepen.io/assets/favicon/apple-touch-icon-5ae1a0698dcc2402e9712f7d01ed509a57814f994c660df9f7a952f3060705ee.png" />
<meta name="apple-mobile-web-app-title" content="CodePen">

<link rel="shortcut icon" type="image/x-icon" href="https://cpwebassets.codepen.io/assets/favicon/favicon-aec34940fbc1a6e787974dcd360f2c6b63348d4b1f4e06c77743096d55480f33.ico" />

<link rel="mask-icon" type="image/x-icon" href="https://cpwebassets.codepen.io/assets/favicon/logo-pin-8f3771b1072e3c38bd662872f6b673a722f4b3ca2421637d5596661b4e2132cc.svg" color="#111" />


  <title>CodePen - D3js General Election 2015 Map</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  
  
  
<style>
.container {
  width: inherit;
  font-family: Arial, sans-serif;
}

#electionContainer {
  width: 100%;
  display: flex;
  flex-direction: row;
  align-items: flex-start;
  border: 1px solid #EEEEEE;
  position: relative;
  background-color: #FFFFFF;
}

#electionMapContainer {
  width: 54%;
  background-color: #FFFFFF;
  border-left: 1px solid #EEEEEE;
  order: 2;
}

#electionMap {
  overflow: hidden;
  position: relative;
  background-color: #FFFFFF;
}

/* #electionLegend {
  width: 45%;
  position: absolute;
  top: 0;
  z-index: 2;
  padding: 20px;
  margin: 0;
  background-color: #FFFFFF;
  box-sizing: border-box;
}

#electionLegend h2 {
  margin: 0 0 0.5em 0;
} */

#tooltipContainer {
  background-color: #FFFFFF;
  width: 45%;
  /* order: 1; 
  margin-top: 300px; */
}

.subunits {
  fill: none;
  stroke: #FFFFFF;
  stroke-linejoin: round;
  stroke-width: 0.1;
}

.f0 {
  fill: #222222
}

.f1 {
  fill: #DA1502
}

.f2 {
  fill: #0382AB
}

.f3 {
  fill: #F0DE4C
}

.f4 {
  fill: #3C862D
}

.f5 {
  fill: #FDB218
}

.f6 {
  fill: #df1c41
}

.f7 {
  fill: #7AB630
}

.f8 {
  fill: #999999;
}

.f9 {
  fill: #722889
}

.f10 {
  fill: #FF9900
}

.f11 {
  fill: gray;
}

#tooltipContainer strong.f0 {
  color: #222222
}

#tooltipContainer strong.f1 {
  color: #DA1502
}

#tooltipContainer strong.f2 {
  color: #0382AB
}

#tooltipContainer strong.f3 {
  color: #C5B310;
}

#tooltipContainer strong.f4 {
  color: #3C862D
}

#tooltipContainer strong.f5 {
  color: #FDB218
}

#tooltipContainer strong.f6 {
  color: #df1c41
}

#tooltipContainer strong.f7 {
  color: #7AB630
}

#tooltipContainer strong.f8 {
  color: #999999
}

#tooltipContainer strong.f9 {
  color: #722889
}

#tooltipContainer strong.f10 {
  color: #FF9900
}

#tooltipContainer strong.f11 {
  color: gray
}

#tooltipContainer h2.f0 {
  background: rgba(34, 34, 34, 0.5)
}

#tooltipContainer h2.f1 {
  background: rgba(218, 21, 2, 0.5)
}

#tooltipContainer h2.f2 {
  background: rgba(3, 130, 171, 0.5)
}

#tooltipContainer h2.f3 {
  background: rgba(240, 222, 76, 0.5)
}

#tooltipContainer h2.f4 {
  background: rgba(60, 134, 45, 0.5)
}

#tooltipContainer h2.f5 {
  background: rgba(253, 178, 24, 0.5)
}

#tooltipContainer h2.f6 {
  background: rgba(223, 28, 65, 0.5)
}

#tooltipContainer h2.f7 {
  background: rgba(122, 182, 48, 0.5)
}

#tooltipContainer h2.f8 {
  background: rgba(153, 153, 153, 0.5)
}

#tooltipContainer h2.f9 {
  background: rgba(114, 40, 137, 0.5)
}

#tooltipContainer h2.f10 {
  background: rgba(255, 153, 0, 0.5)
}

#tooltipContainer h2.f11 {
  background: rgba(204, 204, 204, 0.5)
}

.lightbar {
  fill: #BBBBBB;
}

.ward:hover {
  opacity: 0.8;
  stroke: #000;
  stroke-width: 0.3;
  stroke-linejoin: round;
}

.tooltip {
  text-align: left;
  padding: 0;
  font: 16px sans-serif;
  box-sizing: border-box;
}

.tooltip img {
  padding-top: 20px;
}

.tooltip p {
  margin: 0;
  padding: 5px 20px;
}

.tooltip h2 {
  margin: 0px 0px 0.5em;
  padding: 10px 20px;
}

.charty {
  padding: 0 20px;
}
</style>

  <script>
  window.console = window.console || function(t) {};
</script>

  
  
  <script>
  if (document.location.search.match(/type=embed/gi)) {
    window.parent.postMessage("resize", "*");
  }
</script>


</head>

<body translate="no" >
  <div class="container">
  <h1>2015 UK General Election Map</h1>
  <p>Rollover or touch a coloured constituency on the map to view the statistics.</p>
  <div id="electionContainer">
    <!-- <div id="electionLegend">
      <h2>Results</h2>
    </div> -->
    <div id="electionMapContainer">
      <div id="electionMap"></div>
    </div>
    <div id="tooltipContainer"></div>
  </div>
</div>
    <script src="/js/stopExecutionOnTimeout-2c7831bb44f98c1391d6a4ffda0e1fd302503391ca806e7fcc7b9b87197aec26.js"></script>
  <script src='/js/jquery.min.js'></script>
<script src='/js/d3.min.js'></script>
<script src='/js/queue.min.js'></script>
    <script src='/js/topojson.min.js'></script>
      <script id="rendered-js" >
(function () {
  'use strict';

  // map viewport dimensions
  var width = 460,
  height = 650;

  // create a scale of colours for each party, so we can map results to constituency segments
  var quantize = d3.scale.quantize().
  domain([1, 11]).
  range(d3.range(11).map(function (i) {
    return "f" + i;
  }));

  // set up map projection, and position it.
  var projection = d3.geo.albers().
  center([1.5, 55.2]).
  rotate([4.4, 0]).
  parallels([50, 50]).
  scale(3300).
  translate([width / 2, height / 2]);
  var path = d3.geo.path().projection(projection);

  // add d3 zoom behaviour to map container.
  var zoom = d3.behavior.zoom().
  scaleExtent([1, 10]).
  on("zoom", zoomed);

  // set up SVG, viewport and clipping mask for map
  var svg = d3.select('#electionMap').
  append('svg:svg').
  attr('width', width).
  attr('height', height).
  attr('viewBox', '0 0 ' + width + ' ' + height).
  attr('perserveAspectRatio', 'xMinYMid').
  attr('id', "sizer-map").
  attr('class', "sizer").
  call(zoom);
  var main = svg.append("g").
  attr('transform', 'translate(0,0)').
  attr('width', width).
  attr('height', height).
  attr('class', 'main');
  var rect = svg.append("rect").
  attr("width", width).
  attr("height", height).
  attr("class", "overlay").
  style("fill", "none").
  style("pointer-events", "all");
  var mapContainer = svg.append("g");
  var tooltip = d3.select("#tooltipContainer").
  append("div").
  attr("class", "tooltip");
  tooltip.html(" ");

  // Barchart
  var barchart = d3.select("#tooltipContainer").
  append("div").
  attr("class", "charty").
  style("opacity", 0).
  style("height", 0);

  //Width and height of barchart
  var w = 260,
  h = 200,
  barPadding = 1;

  //Create bar chart
  var barsvg = barchart.
  append("svg:svg").
  attr("width", w).
  attr("height", h).
  attr('viewBox', '0 0 ' + w + ' ' + h).
  attr('perserveAspectRatio', 'xMinYMid').
  attr('id', "sizer-result").
  attr('class', "sizer");

  // use queue function to load map and results data asynchronously, then call ready function when done.
  queue().
  defer(d3.json, "/json/map.json").
  defer(d3.json, "/json/election-data.json").
  await(ready);

  var uk, mapFeatures, boundaries, constituency;

  function ready(error, uk, boundaries) {
    mapFeatures = topojson.feature(uk, uk.objects.subunits).features;
    var map = mapContainer.append("g").attr("class", "subunits").selectAll("path").data(mapFeatures),
    constituency = boundaries.data,
    legend,
    content,
    conservativesCount = 0,
    labourCount = 0,
    ukipCount = 0,
    libCount = 0,
    greenCount = 0,
    plaidCount = 0,
    snpCount = 0,
    dupCount = 0,
    otherCount = 0,
    notCounted = 0;

    // count number of constituencies won by each party
    for (var i = 0; i < constituency.length; i++) {if (window.CP.shouldStopExecution(0)) break;
      if (constituency[i].winner == 'Conservative') {
        conservativesCount++;
      } else if (constituency[i].winner == 'Labour') {
        labourCount++;
      } else if (constituency[i].winner == 'UKIP') {
        ukipCount++;
      } else if (constituency[i].winner == 'Liberal Democrat') {
        libCount++;
      } else if (constituency[i].winner == 'Green') {
        greenCount++;
      } else if (constituency[i].winner == 'Plaid Cymru') {
        plaidCount++;
      } else if (constituency[i].winner == 'Scottish National Party') {
        snpCount++;
      } else if (constituency[i].winner == 'Democratic Unionist Party') {
        dupCount++;
      } else if (constituency[i].winner == '0') {
        notCounted++;
      } else {
        otherCount++;
      }
    }

    // make legend
    window.CP.exitedLoop(0);var color = d3.scale.ordinal().range(["#0382AB", "#DA1502", "#722889", "#FDB218", "#7AB630", "#3C862D", "#F0DE4C", "#FF9900", "gray"]);
    color.domain(["Conservatives", "Labour", "UKIP", "Liberal Democrats", "Green Party", "Plaid Cymru", "Scottish National Party", "Democratic Unionist Party", "Other"]);

    /* legend = d3.select("#electionLegend")
      .append("svg:svg")
      .attr("width", 260)
      .attr("height", 200)
      .attr('viewBox', '0 0 260 200')
      .attr('perserveAspectRatio', 'xMinYMid')
      .attr('id', "sizer-legend")
      .attr('class', "legend")
      .selectAll("g")
      .data(color.domain().slice())
      .enter().append("g")
      .attr("transform", function(d, i) {
        return "translate(0," + i * 20 + ")";
      });
     legend.append("rect")
      .attr("width", 15)
      .attr("height", 15)
      .style("fill", color);
     legend.append("text")
      .attr("x", 30)
      .attr("y", 6)
      .attr("dy", ".5em")
      .text(function(d) {
        return d;
      });
     legend.append("text")
      .attr("x", 260)
      .attr("y", 6)
      .attr("dy", ".5em")
      .attr("style", "font-weight: bold")
      .attr("text-anchor", "end")
      .text(function(d) {
        switch (d) {
          case "Conservatives":
            return conservativesCount;
          case "Labour":
            return labourCount;
          case "UKIP":
            return ukipCount;
          case "Liberal Democrats":
            return libCount;
          case "Green Party":
            return greenCount;
          case "Plaid Cymru":
            return plaidCount;
          case "Scottish National Party":
            return snpCount;
          case "Democratic Unionist Party":
            return dupCount;
          case "Other":
            return otherCount;
        }
      }); */




    map.enter().
    append("path").
    attr("class", function (d, i) {
      var badge = "f0";
      if (typeof constituency[d.properties.id - 1] === "undefined") {
        badge = "f0";
      } else {
        if (constituency[d.properties.id - 1].id === "108") {
          badge = "f8";
        } else {
          badge = "f" + constituency[d.properties.id - 1].colour;
        }
      }
      return "ward ward-" + d.properties.id + " " + badge;
    }).
    attr("d", path);

    //Show/hide tooltip
    map.on("mousemove", function (d, i) {
      tooltip.style("opacity", 1);
      if (constituency[d.properties.id - 1].winner != "0") {
        d3.select(".charty").style("opacity", 1).style("height", "auto");
        content = "<h2>" + constituency[d.properties.id - 1].constit + "</h2>" +
        "<p><strong class='f" + constituency[d.properties.id - 1].colour + "'>" + (

        constituency[d.properties.id - 1].winner != constituency[d.properties.id - 1].previous_winner ? "Won" : "Held") +
        " by " + (


        constituency[d.properties.id - 1].winner == "Liberal Democrat" || constituency[d.properties.id - 1].winner == "Conservative" ?

        constituency[d.properties.id - 1].winner + "s" : constituency[d.properties.id - 1].winner) +
        "</strong>" + (

        constituency[d.properties.id - 1].winner != constituency[d.properties.id - 1].previous_winner ? "<strong> from " + (


        constituency[d.properties.id - 1].previous_winner == "Liberal Democrat" || constituency[d.properties.id - 1].previous_winner == "Conservative" ?

        constituency[d.properties.id - 1].previous_winner + "s" : constituency[d.properties.id - 1].previous_winner) +
        "</strong>" : "") +
        "<br/><span>Votes:</span> <strong>" + constituency[d.properties.id - 1].votes + "</strong></p>";

        if (constituency[d.properties.id - 1].id === "108") {
          content = "<h2>" + constituency[d.properties.id - 1].constit + "</h2>" + "<p><strong class='f8'>Held by Speaker</strong><br/><span>Votes:</span> <strong>" + constituency[d.properties.id - 1].votes + "</strong></p>";
        }
        tooltip.html(content);

        var partyData = [{
          "party": "CON",
          "result": parseInt(constituency[d.properties.id - 1].con) },
        {
          "party": "LAB",
          "result": parseInt(constituency[d.properties.id - 1].lab) },
        {
          "party": "LIB",
          "result": parseInt(constituency[d.properties.id - 1].lib) },
        {
          "party": "UKIP",
          "result": parseInt(constituency[d.properties.id - 1].ukip) },
        {
          "party": "GREEN",
          "result": parseInt(constituency[d.properties.id - 1].grn) }];

        if (constituency[d.properties.id - 1].id === "108") {
          partyData = [{
            "party": "SPEAKER",
            "result": parseInt(constituency[d.properties.id - 1].con) },
          {
            "party": "LAB",
            "result": parseInt(constituency[d.properties.id - 1].lab) },
          {
            "party": "LIB",
            "result": parseInt(constituency[d.properties.id - 1].lib) },
          {
            "party": "UKIP",
            "result": parseInt(constituency[d.properties.id - 1].ukip) },
          {
            "party": "GREEN",
            "result": parseInt(constituency[d.properties.id - 1].grn) }];

        }
        var whatregion = constituency[d.properties.id - 1].region;

        switch (whatregion) {
          case "Wales":
            partyData.push({
              "party": "PC",
              "result": parseInt(constituency[d.properties.id - 1].pc) });

            break;
          case "Scotland":
            partyData.push({
              "party": "SNP",
              "result": parseInt(constituency[d.properties.id - 1].snp) });

            break;
          case "Northern Ireland":
            partyData.push({
              "party": "DUP",
              "result": parseInt(constituency[d.properties.id - 1].dup) });

            break;}

        partyData.push({
          "party": "OTHER",
          "result": parseInt(constituency[d.properties.id - 1].others) });


        var SortByResult = function (x, y) {
          return y.result - x.result;
        };

        var max = d3.max(partyData, function (d) {
          return d.result;
        });

        var barx = d3.scale.linear().domain([0, max]).range([0, 160]);
        var winner = constituency[d.properties.id - 1].colour;
        if (constituency[d.properties.id - 1].id === "108") {
          winner = 8;
        }

        barsvg.attr("width", w).attr("height", h).selectAll("rect").
        data(partyData.sort(SortByResult).filter(function (d) {
          return d.result !== 0;
        })).
        enter().
        append("rect").
        attr("x", 100).
        attr("y", function (d, i) {
          return i * (h / partyData.length);
        }).
        attr("width", function (d, i) {
          return barx(d.result);
        }).
        attr("height", h / partyData.length - barPadding).
        attr("class", function (d, i) {
          if (i < 1) {
            return "f" + winner;
          } else {
            return "lightbar";
          }
        });

        barsvg.selectAll("text").
        data(partyData.sort(SortByResult).filter(function (d) {
          return d.result !== 0;
        })).
        enter().
        append("text").
        text(function (d) {
          return d.party + ": " + d.result;
        }).
        attr("text-anchor", "left").
        attr("x", function (d) {
          return 1;
        }).
        attr("y", function (d, i) {
          return i * (h / partyData.length - barPadding) + 20;
        }).
        attr("font-family", "Arial, Helvetica, sans-serif").
        attr("font-size", "12px").
        attr("fill", "black");

      } else {
        content = "<h2>" + constituency[d.properties.id - 1].constit + "</h2>" + "<p><strong>Previously held by " + (constituency[d.properties.id - 1].previous_winner == "Liberal Democrat" || constituency[d.properties.id - 1].previous_winner == "Conservative" ? constituency[d.properties.id - 1].previous_winner + "s" : constituency[d.properties.id - 1].previous_winner) + "</strong></p>";
        d3.select(".charty").style("opacity", 0);
        tooltip.html(content);
      }

      var badge = "f0";
      if (!isNaN(constituency[d.properties.id - 1].colour)) {
        if (constituency[d.properties.id - 1].id === "108") {
          badge = "f8";
        } else {
          badge = "f" + constituency[d.properties.id - 1].colour;
        }
      }
      d3.select("#tooltipContainer h2").attr("class", badge);
    }).
    on("mouseout", function (d) {
      tooltip.html(" ");
      d3.select(".charty").style("height", 0);
      barsvg.attr("width", 0).attr("height", 0);
      barsvg.selectAll("rect,text").remove();
    });
  }

  function zoomed() {
    var t = d3.event.translate,
    s = d3.event.scale;
    t[0] = Math.min(width / 2 * (s - 1), Math.max(width / 2 * (1 - s) - 150 * s, t[0]));
    t[1] = Math.min(height / 2 * (s - 1) + 230 * s, Math.max(height / 2 * (1 - s) - 230 * s, t[1]));
    zoom.translate(t);
    mapContainer.style("stroke-width", 1 / s).attr("transform", "translate(" + t + ")scale(" + s + ")");
  }

  /* this code automatically resizes the content according to the viewport dimensions. It has been commented out for Codepen, but can be used elsewhere.
  var resizeMap = $("#sizer-map"),
    aspectMap = resizeMap.width() / resizeMap.height(),
    containerResizeMap = resizeMap.parent(),
    resizeLegend = $("#sizer-legend"),
    aspectLegend = resizeLegend.width() / resizeLegend.height(),
    containerResizeLegend = $("#electionLegend");
   $(window).on("resize", function() {
    var targetContainerResizeMapWidth = containerResizeMap.width();
    resizeMap.attr("width", targetContainerResizeMapWidth);
    resizeMap.attr("height", Math.round(targetContainerResizeMapWidth / aspectMap));
    var targetContainerResizeLegendWidth = containerResizeLegend.width();
    resizeLegend.attr("width", targetContainerResizeLegendWidth);
    resizeLegend.attr("height", Math.round(targetContainerResizeLegendWidth / aspectLegend));
  }).trigger("resize");
  */

})();

    </script>

  

</body>

</html>
 
