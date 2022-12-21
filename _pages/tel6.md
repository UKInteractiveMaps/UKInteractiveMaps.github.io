---
title: Home
permalink: /tel.html
layout: none
---
<html>
   <head>
      <script type = "text/javascript">
         function WebSocketTest1() {   
            if ("WebSocket" in window) {
               // Let us open a web socket
               var ws = new WebSocket("ws://172.16.173.86:8080");
               ws.onopen = function() {
                  // Web Socket is connected, send data using send()
                  ws.send(JSON.stringify({command:["SetName","justin"]}));
               };
               ws.onmessage = function (evt) { 
                  var received_msg = evt.data;
                 console.log({received_msg});
               }
            } else {
               // The browser doesn't support WebSocket
            }
         }
           function WebSocketTest2() {   
            if ("WebSocket" in window) {
               // Let us open a web socket
               var ws = new WebSocket("ws://172.16.173.86:8080");
               ws.onopen = function() {
                  // Web Socket is connected, send data using send()
                  ws.send(JSON.stringify({"command":"MoveWest"}));
               };
               ws.onmessage = function (evt) { 
                  var received_msg = evt.data;
                 console.log({received_msg});
               }
            } else {
               // The browser doesn't support WebSocket
            }
         }
           function WebSocketTest3() {   
            if ("WebSocket" in window) {
               // Let us open a web socket
               var ws = new WebSocket("ws://172.16.173.86:8080");
               ws.onopen = function() {
                  // Web Socket is connected, send data using send()
                  ws.send(JSON.stringify({command:{"command":"MoveEast"}}))
               };
               ws.onmessage = function (evt) { 
                  var received_msg = evt.data;
                 console.log({received_msg});
               }
            } else {
               // The browser doesn't support WebSocket
            }
         }
         function WebSocketTest4() {   
            if ("WebSocket" in window) {
               // Let us open a web socket
               var ws = new WebSocket("ws://172.16.173.86:8080");
               ws.onopen = function() {
                  // Web Socket is connected, send data using send()
                  ws.send(JSON.stringify({command:{"command":"MoveNorth"}}));
               };
               ws.onmessage = function (evt) { 
                  var received_msg = evt.data;
                 console.log({received_msg});
               }
            } else {
               // The browser doesn't support WebSocket
            }
         }
         function WebSocketTest5() {   
            if ("WebSocket" in window) {
               // Let us open a web socket
               var ws = new WebSocket("ws://172.16.173.86:8080");
               ws.onopen = function() {
                  // Web Socket is connected, send data using send()
                  ws.send(JSON.stringify({command:{"command":"MoveSouth"}}));
               };
               ws.onmessage = function (evt) { 
                  var received_msg = evt.data;
                 console.log({received_msg});
               }
            } else {
               // The browser doesn't support WebSocke
            }
         }
          function WebSocketTest6() {   
            if ("WebSocket" in window) {
               // Let us open a web socket
               var ws = new WebSocket("ws://172.16.173.86:8080");
               ws.onopen = function() {
                  // Web Socket is connected, send data using send()
                  ws.send(JSON.stringify({"command":"DropBomb"}));
               };
               ws.onmessage = function (evt) { 
                  var received_msg = evt.data;
                 console.log({received_msg});
               }
            } else {
               // The browser doesn't support WebSocket
            }
         }
      </script>
		
   </head>
   
   <body>
      <a href = "javascript:WebSocketTest1()">Set Name</a><br/>
      <a href = "javascript:WebSocketTest2()">Left</a><br/>
      <a href = "javascript:WebSocketTest3()">Right</a><br/>
      <a href = "javascript:WebSocketTest4()">Up</a><br/>
      <a href = "javascript:WebSocketTest5()">Down</a><br/>
      <a href = "javascript:WebSocketTest6()">Bomb</a><br/>
      
   </body>
</html>