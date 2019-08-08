# Ensayo-pagina

Link del sitio 
https://smlopeza.github.io/Ensayo-pagina/

Ensayo para insertar mapas a paginas web

<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~chris/1638.embed" height="525" width="100%"></iframe>

var map = L.map('map').setView([51.505, -0.09], 13);

L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
}).addTo(map);

L.marker([51.5, -0.09]).addTo(map)
    .bindPopup('A pretty CSS3 popup.<br> Easily customizable.')
    .openPopup();
