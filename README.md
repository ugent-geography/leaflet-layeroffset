#Leaflet.layershift
An extension to Leaflet that allows you to drag a single tile layer around and measure the offset from the other layers. Admittedly, the use cases for this are rather limited. The Department of Geography at UGent is using it to interpret 18th century maps that aren't easily georeferenced, and as such are impossible to overlay perfectly on a modern map.

##Unfortunately...
... it currently only works on tile layers; this doesn't even include WMS or other L.TileLayer descendants.

##Using the plugin
If you want to be able to drag a layer around, you'll have to use L.ShiftableTileLayer instead of L.TileLayer. 
```javascript
var map = L.map('map').setView([51.02435, 3.71018], 17);

var osm = L.shiftableTileLayer('http://{s}.tile.osm.org/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors'
}).addTo(map);
```

By default, the layer will behave exactly like a normal `L.TileLayer`. Before you can drag a layer around, you have to enable the shifting handler:
```javascript
osm.shifting.enable();
```

##Events
The following events will be triggered on the layer:
###shiftstart
Fired the moment you enable shifting. There are no additional event properties.
###shiftend
Fired the moment you disable shifting by calling 
```javascript
layer.shifting.disable();
```
There are no additional event properties.
###shift
Fired whenever the layer is dragged.
|Property|Type|Description|
|--------|----|-----------|
|distance|Number|The distance the layer was shifted from its initial position in meters|
|pixelShift|Point|The vector by which the layer was shifted in layer container pixels|
|angle|Number|The angle of the pixelShift vector in radians - 0 is north|