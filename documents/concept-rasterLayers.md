# Capas raster WMS y WMTS

[🔙 Volver al inicio](readme.md)

## Consulta de las capas de un mapa

Existen varios métodos que permiten gestionar las capas de un mapa.

```javascript
// Acceder y eliminar las capas del mapa
const capas = mapajs.getLayers();
mapajs.removeLayers(layer1); // eliminar una capa 
mapajs.removeLayers([layer1, layer2, layer3]); // o varias capas

// Capas específicas por atributo: WMS, WFS, KML, WMTS
const layersWMS = mapajs.getWMS({name:'batimetría'}); // capas WMS que cumplen la condicion

// Buscar las capas base, si hay alguna
const capasBase = mapajs.getBaseLayers(); // capas WMS o WMTS que sean base
```

## Definición de capas WMS

### Mediante definición de objeto M.layer.WMS

```javascript
let wmsAdminBoundaries = new M.layer.WMS({
                    url: 'https://www.ign.es/wms-inspire/unidades-administrativas?',
                    name: 'AU.AdministrativeBoundary',
                    legend: 'Limite administrativo',
                    transparent: 'false',
                    tiled: false,
                }, {
                  //Pueden especificarse las resoluciones mínima y máxima de dibujado de las capas
                  //Son los niveles de zoom en los que sería visible. Omitir para dibujar en todos
                  maxResolution: 3270.877524508511,
                  minResolution: 1635.4387622542556
                })
```

### Mediante Template Literals

```javascript
'WMS*Limite Administrativo*https:/www.ign.es/wms-inspire/unidades-administrativas?*AU.AdministrativeBoundary*false*true'
```


## Definición de capas WMTS

### Mediante definición de objeto M.layer.WMTS

Aquí tenemos algunas capas de ejemplo

```javascript
/**
 * Definimos capas notación standard
 * 
 */
let wmtsMTN251edi = new M.layer.WMTS({
  url: "https://www.ign.es/wmts/primera-edicion-mtn",
  name: "mtn25-edicion1",
  matrixSet: "GoogleMapsCompatible",
  legend: "Primera edición MTN25"
}, {
  format: 'image/jpeg'
});

let wmtsMTN501edi = new M.layer.WMTS({
  url: "https//www.ign.es/wmts/primera-edicion-mtn",
  name: "mtn50-edicion1",
  matrixSet: "GoogleMapsCompatible",
  legend: "Primera edición MTN50"
}, {
  format: 'image/jpeg'
});

let wmtsMTNActual = new M.layer.WMTS({
  url: "https://www.ign.es/wmts/mapa-raster",
  name: "MTN",
  matrixSet: "GoogleMapsCompatible",
  legend: "Cartografía Ráster Actual"
}, {
  format: 'image/jpeg'
});

let wmtssiose = new M.layer.WMTS({
  url: "https://servicios.idee.es/wmts/ocupacion-suelo",
  name: "LC.LandCoverSurfaces",
  matrixSet: "GoogleMapsCompatible",
  legend: "CORINE / SIOSE"
}, {
  format: 'image/jpeg'
});

let wmtsmdt = new M.layer.WMTS({
  url: "https://servicios.idee.es/wmts/mdt",
  name: "Relieve",
  matrixSet: "GoogleMapsCompatible",
  legend: "MDT"
}, {
  format: 'image/jpeg'
});
```

### Mediante Template Literals

Podemos definir también una capa WMTS de la siguiente manera:

```javascript
'WMTS*https://www.ign.es/wmts/ign-base?*IGNBaseTodo*EPSG:4326*base*false*image/jpeg*false*false*true'
```

en donde:

* WMTS 👉 Tipo de servicio https://www.ign.es/wmts/ign-base? -> URL del servicio
* IGNBaseTodo 👉 Nombre de la capa especificada en el *capabilities*
* GoogleMapsCompatible 👉 Nombre de TileMatrix: EPSG:4326, GoogleMapsCompatible, InspireCRS84Quad, EPSG:4258, EPSG:25830
* base 👉 Título de la capa (legend), que sería la que aparecería en los plugins de TOC.
* false 👉 *transparent*, controla que la capa se cargue como base o como servicio superpuesto encima de otra capa
* image/jpeg 👉 Formato de imagen
* false 👉 *displayInLayerSwitcher*, controla que la capa aparezca o no en los plugins de TOC
* false 👉 *queryable*, controla que la capa pueda ser consultable mediante peticiones **GetFeatureInfo**.
* true 👉 *visible*, controla que la capa se carge visible u oculta

