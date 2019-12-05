<p align="center"><img src="https://upload.wikimedia.org/wikipedia/de/3/38/GeoServer_Logo.svg" /></p>
<h4 align="center">Task: Setup a Geoserver with Docker</h4>
<p align="center">The following README covers the submission requirements for the Google Code-in task: Setup a Geoserver with Docker.</p>

## Basic descriptive works

### Why is GeoServer an important factor in a GIS stack?
GeoServer is an essential factor to a GIS stack. From my understanding (after running a local environment, and working on a few tasks) is that it is an open-source server for geospatial data. I think it's best put by the WikiPedia entry for GeoServer:

```
Just as the Apache HTTP Server has offered a free and open web server to publish HTML, GeoServer aims to do the same for geospatial data.
```

Open-source platforms are important because they allow for developers around the globe to build powerful software that we depend on, without even knowing it.

In a GIS (Geographic Information System) stack, GeoServer facilitates the hosted storage, sharing, processing, and editing of geospatial data. It's like a backbone for the complete stack, as a means of connecting together information and tools to operate in unison.

### What is Docker and why should it be used to containerize GeoServer?
Docker is a tool that allows for operating system level virtualization via containers. Containers let developers ship complete applications in single, simply installable packages. It's fantastic not only for ease of development, but also for scaling, security, and a host of other benefits.

Docker is fantastic to containerize GeoServer, since it allows for:
* Ease in setup so anyone, anywhere can quickly spin up their own development environment via a basic DOCKERFILE.
* Isolation so that existing processes running on a machine/server are not hindered by GeoServer (except I/O of course).
* Ease of development, so that any open-source developer can get setup with a uniform development environment that is the same across Operating Systems and devices.
* Security, scaleability via swarm, and more.

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
