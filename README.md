# Ensayo-pagina

Link del sitio 
https://smlopeza.github.io/Ensayo-pagina/

Ensayo para insertar mapas a paginas web



{% load staticfiles %}
{% block content %}
<div class="spacer2"></div>
<div class="container_special">
<div class="jumbotron specialjum">
<script src="http://code.jquery.com/jquery-1.11.0.min.js"></script>
<link href="http://cdn.leafletjs.com/leaflet-0.7.3/leaflet.css" media="screen, print" rel="stylesheet">
<script src="http://cdn.leafletjs.com/leaflet-0.7.3/leaflet.js"></script>
<body>
<!--This is the open street map that's being used from Leaflet-->
var modern = L.tileLayer('http://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>',
    noWrap: true,
});

<!--Create the map with the tilesets-->
var map = L.map('map', {
    layers: [modern]
});

<!--This fits the map to the world view. Otherwise you might see continents repeating multiple times-->
map.fitWorld().zoomIn();

<!--This is calling the points for the city and the data for each-->
var geo_json = 
    '{"type":"FeatureCollection","features":[{% for city in cities %}{"type": "Feature","properties":{"name" : "{{city.cityName}}","url" : "{% url "city" city.url %}"},"geometry":{"type":"Point","coordinates":[{{city.longitude}},{{city.latitude}}]}}{% if not forloop.last %},{% endif %}{% endfor %}]}'


var geodata = JSON.parse(geo_json);


var geolayer = L.geoJson(geodata, {
    onEachFeature: showPopup
});

<!--Add the points to the map-->
geolayer.addTo(map);

<!--This allows you to click the point-->
function showPopup(feature, layer) {
    var key, val;
    var content = [];
    for (key in feature.properties) {
        val = feature.properties[key];
    
        if (key == "url") {
            val = '<a href="' + val + '" />View City</a>';
            key = "";
        }
        content.push("<strong>" + val + "</strong>");
    }
    layer.bindPopup(content.join("<br />"));
}
</script>
</div>
</div>
{% endblock %}
