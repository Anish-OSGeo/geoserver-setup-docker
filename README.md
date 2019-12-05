<p align="center"><img src="https://upload.wikimedia.org/wikipedia/de/3/38/GeoServer_Logo.svg" /></p>
<h4 align="center">Task: Setup a Geoserver with Docker</h4>
<p align="center">The following README covers the submission requirements for the Google Code-in task: Setup a Geoserver with Docker.</p>

## Basic descriptive works

### Why is GeoServer an important factor in a GIS stack?

### What is Docker and why should it be used to containerize GeoServer?

## Process (documentation)
1. To begin, I built GeoServer + Docker myself via the build script (according to the [kartoza docker-geoserver dockerfile](git://github.com/kartoza/docker-geoserver))

```
# Build script
git clone git://github.com/kartoza/docker-geoserver
cd docker-geoserver
./build.sh

# Docker process startup
docker-compose up
```

2. Next, I travelled to `http://localhost:8600/geoserver` and signed in as an Administrator.

<img src="https://i.imgur.com/J4LBnk1.png" align="center">

3. I created a new testing GeoServer workspace (so that I could create a store and begin uploading layers).

<img src='https://i.imgur.com/L3GZnf6.png' align="center">
<img src="https://i.imgur.com/Z1Ukggq.png" align="center">

4. I created a new testing GeoServer data store.

<img src="https://i.imgur.com/iAoz4my.png" align="center">

5. I copied a testing .tiff file I had downloaded locally to the container. Containerization is fantastic, but, in order to upload the layer in the next step, it needed to be located in the container storage first.
```
# Moving geoTIFF file to the docker container.
docker cp wc2.0_10m_tavg_05.tif a3babc6f02a4:/wc.tif

# Note, a2babc6f02a4 is the container id. You can find it by doing:
docker container ls

## and selecting the container named: kartoza/geoserver:2.15.2
```
6. I added the new Layer (geoTIFF downloaded from the WorldClimate project for the month of May) to GeoServer via `Layers > Add a new layer`.

<img src="https://i.imgur.com/94B5yE6.png" align="center">

7. Finally, once the layer had been uploaded and all was well, I used the Layer Preview via OpenLayers to render and view the layer via the browser. See the first image for the layer open in GeoServer via OpenLayers, and the second to see the same layer open in QGIS.

<img src="https://i.imgur.com/XDasxfE.png" align="center">
<img src="https://i.imgur.com/bzsVcYI.png" align="center">
