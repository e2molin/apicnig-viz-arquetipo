# 🧩️ Capas raster XYZ y TMS

👀 Disponible a partir de API-CNIG 4.0 (Con OL6)
https://mapea-lite-6.desarrollo.guadaltel.es/api-core/

## 🔵Capas raster XYZ

[🔙 Volver](https://github.com/e2molin/viz-arquetipo#readme)

Las capas XYZ son servicios de información geográfica en forma de tiles. Cada tile representa una combinación de tres parámetros. Las capas XYZ presentan la siguiente estructura https://rts.larioja.org/mapa-base/rioja/{z}/{x}/{y}.png . {z} especifica el nivel de zoom, {x} el número de columna y {y} el número de fila

Se pueden construir de varias maneras:

```javascript
const mapa = M.map({
  container: 'map',
  getfeatureinfo: 'plain',
  projection: 'EPSG:3857*m',
  layers: ["XYZ*XYZLaRioja*https://rts.larioja.org/mapa-base/rioja/{z}/{x}/{y}.png*true*true"],
  zoom: 7,
  center: [-491123.5838198825, 4868765.072772329],
});
```

```javascript
const xyz = new M.layer.XYZ({
  url: 'https://rts.larioja.org/mapa-base/rioja/{z}/{x}/{y}.png',
  name: 'XYZLaRioja',
  projection: 'EPSG:3857',
  visibility: true,
});
mapa.addXYZ(xyz);
```

Donde:

* **url**: Url del servicio XYZ.
* **name**: Identificador de la capa.
* **projection**: La proyección destino de la capa.
* **visibility**: Indica si la capa estará por defecto visible o no.


## 🔵 Capas raster TMS

[🔙 Volver](https://github.com/e2molin/viz-arquetipo#readme)

Las capas TMS (Tile Map Service) son servicios de información geográfica en forma de tiles muy similares a las capas XYZ. El protocolo TMS de OSGeo permite que los tiles usen índices numéricos y aporten metadatos para la configuración e investigación. Las capas TMS presentan la siguiente estructura:

```html
https://www.ign.es/web/catalogo-cartoteca/resources/webmaps/data/cresques/{z}/{x}/{y}.jpg
```
* {z} especifica el nivel de zoom.
* {x} el número de columna.
* {y} el número de fila.

Se pueden construir de varias maneras.

Añadiéndolas en el constructor del mapa:

```javascript
const mapa = M.map({
  container: 'map',
  getfeatureinfo: 'plain',
  projection: 'EPSG:3857*m',
  layers: ["TMS*TMSCresques*https://www.ign.es/web/catalogo-cartoteca/resources/webmaps/data/cresques/{z}/{x}/{y}.jpg*true*true"],
  zoom: 7,
  center: [-491123.5838198825, 4868765.072772329],
});
```

Con el método correspondiente:

```javascript
const tms = new M.layer.TMS({
  url: 'https://www.ign.es/web/catalogo-cartoteca/resources/webmaps/data/cresques/{z}/{x}/{y}.jpg',
  name: 'TMSCresques',
  projection: 'EPSG:3857',
  visibility: true,
});
mapa.addTMS(tms);
```

Donde:

* **url**: Url del servicio TMS.
* **name**: Identificador de la capa.
* **projection**: La proyección destino de la capa.
* **visibility**: Indica si la capa estará por defecto visible o no.



---

[🔙 Volver](https://github.com/e2molin/viz-arquetipo#readme)