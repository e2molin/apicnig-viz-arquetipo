# Fichero de configuración

Uno de los enlaces que añadimos a nuestro visualizador , además de la librería javascript de APICNIG, y el fichero de estilos, es un fichero de configuración.

```javascript
<script type="text/javascript" src="https://componentes.ign.es/api-core/js/configuration.js"></script>
```

Aquí se definen parámetros por defecto que configurean la apariencia del mapa cuando creamos una instancia lo más simple posible.


```javascript
const map = M.map({
    container: 'mapjs',
    controls: ['backgroundlayers', 'scale*true', 'scaleline', 'rotate', 'location',  'getfeatureinfo'],
    zoom: 6,
    maxZoom: 20,
    minZoom: 4,
    projection: "EPSG:3857*m",
    center: {
        x: -712300,
        y: 4310700,
        draw: false  //Dibuja un punto en el lugar de la coordenada
    },
});
```

Si usamos el fichero tal cual se sirve desde la API, veremos por ejemplo un mapa base con el WMTS del IGNBASE de fondo, y un control con tres botones que permiten cambiar la capa base con tres opciones. Pero podemos descargarlo y guardarlo en nuestra aplicación, y quitar el enlace a la API. Esto nos permitirá customizar algunas cosas a nuestro gusto.

```javascript
<script type="text/javascript" src="js/mapconfig.js"></script>
```

Podemos cambiar el mapa base de inicio

```javascript
M.config('wmts', {
    base: 'WMTS*https://www.ign.es/wmts/ign-base?*IGNBaseTodo*GoogleMapsCompatible*base*false*image/jpeg*false*false*true',
});
```

El comportamiento de las atribuciones por defecto.

```javascript
M.config.attributions.defaultAttribution = 'Instituto Geográfico Nacional';
M.config.attributions.defaultURL = 'https://www.ign.es';
```

Las capas y el número de botones de cambios de mapa base (Hasta un número máximo de cinco).

```Javascript
const backgroundlayersIds = 'mapa,imagen,hibrido,mtn50,mtn25'.split(',');
const backgroundlayersTitles = 'Mapa,Imagen,H&iacute;brido,MTN50,MTN25'.split(',');
const backgroundlayersLayers = 'WMTS*https://www.ign.es/wmts/ign-base?*IGNBaseTodo*GoogleMapsCompatible*base*false*image/jpeg*false*false*true,WMTS*https://www.ign.es/wmts/pnoa-ma?*OI.OrthoimageCoverage*GoogleMapsCompatible*imagen*false*image/jpeg*false*false*true,WMTS*https://www.ign.es/wmts/pnoa-ma?*OI.OrthoimageCoverage*GoogleMapsCompatible*imagen*true*image/jpeg*false*false*true+WMTS*https://www.ign.es/wmts/ign-base?*IGNBaseOrto*GoogleMapsCompatible*Callejero*true*image/png*false*false*true,WMTS*http://www.ign.es/wmts/primera-edicion-mtn?*mtn50-edicion1*GoogleMapsCompatible*MTN50 Primera edición*false*image/jpeg*false*false*true,WMTS*http://www.ign.es/wmts/primera-edicion-mtn?*mtn25-edicion1*GoogleMapsCompatible*MTN25 Primera edición*false*image/jpeg*false*false*true'.split(',');
const backgroundlayersOpts = backgroundlayersIds.map((id, index) => {
  return {
    id,
    title: backgroundlayersTitles[index],
    layers: backgroundlayersLayers[index].split('+'),
  };
});
```

La anchura a partir de la API se comporta en versión móvil

```Javascript
M.config('MOBILE_WIDTH', '768');
```

Sistema de referencia por defecto

```Javascript
M.config('DEFAULT_PROJ', 'EPSG:3857*m');
```

> 💡 La mejor opción no es configurar un nuestro script, sino descargarnos el de la API, modificarlo a nuestro gusto, y apuntar a este desde nuestro código.

Este es un ejemplo completo 

```Javascript
/**
 * IGN API
 * Version 3.3.14
 * Date 08-04-2021
 */

 const backgroundlayersIds = 'mapa,imagen,hibrido,mtn50,mtn25'.split(',');
 const backgroundlayersTitles = 'Mapa,Imagen,H&iacute;brido,MTN50,MTN25'.split(',');
 const backgroundlayersLayers = 'WMTS*https://www.ign.es/wmts/ign-base?*IGNBaseTodo*GoogleMapsCompatible*base*false*image/jpeg*false*false*true,WMTS*https://www.ign.es/wmts/pnoa-ma?*OI.OrthoimageCoverage*GoogleMapsCompatible*imagen*false*image/jpeg*false*false*true,WMTS*https://www.ign.es/wmts/pnoa-ma?*OI.OrthoimageCoverage*GoogleMapsCompatible*imagen*true*image/jpeg*false*false*true+WMTS*https://www.ign.es/wmts/ign-base?*IGNBaseOrto*GoogleMapsCompatible*Callejero*true*image/png*false*false*true,WMTS*http://www.ign.es/wmts/primera-edicion-mtn?*mtn50-edicion1*GoogleMapsCompatible*MTN50 Primera edición*false*image/jpeg*false*false*true,WMTS*http://www.ign.es/wmts/primera-edicion-mtn?*mtn25-edicion1*GoogleMapsCompatible*MTN25 Primera edición*false*image/jpeg*false*false*true'.split(',');
 const backgroundlayersOpts = backgroundlayersIds.map((id, index) => {
   return {
     id,
     title: backgroundlayersTitles[index],
     layers: backgroundlayersLayers[index].split('+'),
   };
 });
 
 (function(M) {
   /**
    * Pixels width for mobile devices
    *
    * @private
    * @type {Number}
    */
   M.config('MOBILE_WIDTH', '768');
 
   /**
    * The Mapea URL
    * @const
    * @type {string}
    * @public
    * @api stable
    */
   M.config('MAPEA_URL', 'https://componentes.cnig.es/api-core/');
 
   /**
    * The path to the Mapea proxy to send
    * jsonp requests
    * @const
    * @type {string}
    * @public
    * @api stable
    */
   M.config('PROXY_URL', location.protocol + '//componentes.cnig.es/api-core/api/proxy');
 
   /**
    * The path to the Mapea proxy to send
    * jsonp requests
    * @const
    * @type {string}
    * @public
    * @api stable
    */
   M.config('PROXY_POST_URL', location.protocol + '//componentes.cnig.es/api-core/proxyPost');
 
   /**
    * The path to the Mapea templates
    * @const
    * @type {string}
    * @public
    * @api stable
    */
   M.config('TEMPLATES_PATH', '/files/templates/');
 
   /**
    * The path to the Mapea theme
    * @const
    * @type {string}
    * @public
    * @api stable
    */
   M.config('THEME_URL', location.protocol + '//componentes.cnig.es/api-core/assets/');
 
   /**
    * The path to the Mapea theme
    * @const
    * @type {string}
    * @public
    * @api stable
    */
 
   /**
    * TODO
    * @type {object}
    * @public
    * @api stable
    */
   M.config('tileMappgins', {
     /**
      * Predefined WMC URLs
      * @const
      * @type {Array<string>}
      * @public
      * @api stable
      */
     'tiledNames': '${tile.mappings.tiledNames}'.split(','),
 
     /**
      * WMC predefined names
      * @const
      * @type {Array<string>}
      * @public
      * @api stable
      */
     'tiledUrls': '${tile.mappings.tiledUrls}'.split(','),
 
     /**
      * WMC context names
      * @const
      * @type {Array<string>}
      * @public
      * @api stable
      */
     'names': '${tile.mappings.names}'.split(','),
 
     /**
      * WMC context names
      * @const
      * @type {Array<string>}
      * @public
      * @api stable
      */
     'urls': '${tile.mappings.urls}'.split(',')
   });
 
   /**
    * Default projection
    * @const
    * @type {string}
    * @public
    * @api stable
    */
   M.config('DEFAULT_PROJ', 'EPSG:3857*m');
 
   /**
    * Default projection
    * @const
    * @type {string}
    * @public
    * @api stable
    */
   M.config('GEOPRINT_URL', 'https://componentes.cnig.es/geoprint');
 
   /**
    * Default projection
    * @const
    * @type {string}
    * @public
    * @api stable
    */
   M.config('GEOREFIMAGE_TEMPLATE', 'https://componentes.cnig.es/geoprint' + '/print/mapexport');
 
   /**
    * Default projection
    * @const
    * @type {string}
    * @public
    * @api stable
    */
   M.config('PRINTERMAP_TEMPLATE', 'https://componentes.cnig.es/geoprint' + '/print/CNIG');
 
   /**
    * Default projection
    * @const
    * @type {string}
    * @public
    * @api stable
    */
   M.config('GEOPRINT_STATUS', 'https://componentes.cnig.es/geoprint' + '/print/status');
 
   /**
    * WMTS configuration
    *
    * @private
    * @type {object}
    */
   M.config('wmts', {
     base: 'WMTS*https://www.ign.es/wmts/ign-base?*IGNBaseTodo*GoogleMapsCompatible*base*false*image/jpeg*false*false*true',
   });
 
   /**
    * Controls configuration
    *
    * @private
    * @type {object}
    */
   M.config('controls', {
     default: '',
   });
 
   /**
    * Attributions configuration
    *
    * @private
    * @type {object}
    */
   M.config('attributions', {
     defaultAttribution: 'Instituto Geogr&aacute;fico Nacional',
     defaultURL: 'https://www.ign.es/',
     url: 'https://componentes.cnig.es/api-core/files/attributions/WMTS_PNOA_20170220/atribucionPNOA_Url.kml',
     type: 'kml',
   });
 
   /**
    * BackgroundLayers Control
    *
    * @private
    * @type {object}
    */
   M.config('backgroundlayers', backgroundlayersOpts);
 
   /**
    * IGNSearch List Control
    *
    * @private
    * @type {object}
    */
    M.config('IGNSEARCH_TYPES_CONFIGURATION', [
      'Estado',
      //'Comunidad aut\u00F3noma',
      //'Ciudad con estatuto de autonom\u00EDa',
      //'Provincia',
      //'Municipio',
      //'EATIM',
      'Isla administrativa',
      'Comarca administrativa',
      'Jurisdicci\u00F3n',
      //'Capital de Estado',
      //'Capital de comunidad aut\u00F3noma y ciudad con estatuto de autonom\u00EDa',
      //'Capital de provincia',
      //'Capital de municipio',
      //'Capital de EATIM',
      //'Entidad colectiva',
      //'Entidad menor de poblaci\u00F3n',
      'Distrito municipal',
      //'Barrio',
      //'Entidad singular',
      'Construcci\u00F3n/instalaci\u00F3n abierta',
      'Edificaci\u00F3n',
      //'V\u00E9rtice Geod\u00E9sico',
      //'Hitos de demarcaci\u00F3n territorial',
      //'Hitos en v\u00EDas de comunicaci\u00F3n',
      'Alineaci\u00F3n monta\u00F1osa',
      'Monta\u00F1a',
      'Paso de monta\u00F1a',
      'Llanura',
      'Depresi\u00F3n',
      'Vertientes',
      'Comarca geogr\u00E1fica',
      'Paraje',
      'Elemento puntual del paisaje',
      'Saliente costero',
      'Playa',
      'Isla',
      'Otro relieve costero',
       //'Parque Nacional y Natural',
      'Espacio protegido restante',
      //'Aeropuerto',
      //'Aer\u00F3dromo',
      //'Pista de aviaci\u00F3n y helipuerto',
      //'Puerto de Estado',
      'Instalaci\u00F3n portuaria',
      //'Carretera',
      'Camino y v\u00EDa pecuaria',
      //'V\u00EDa urbana',
      //'Ferrocarril',
      'Curso natural de agua',
      'Masa de agua',
      'Curso artificial de agua',
      'Embalse',
      'Hidr\u00F3nimo puntual',
      'Glaciares',
      'Mar',
      'Entrante costero y estrecho mar\u00EDtimo',
      'Relieve submarino',
    ]);
 })(window.M);
```