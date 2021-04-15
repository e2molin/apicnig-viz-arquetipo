# Code snippets

[🔙 Volver](https://github.com/e2molin/viz-arquetipo#readme)
##  ⚙ Creación del mapa

El Objeto mapa es de la clase M.map y nos permite configurar los controles que figuran de inicio en el mapa, niveles de zoom y posición y centrado del mapa en el arranque.


```javascript
const map = M.map({
    container: 'mapjs',
    controls: ['panzoom', 'scale*true', 'scaleline', 'rotate', 'location',  'getfeatureinfo'],
    // controls: ['panzoom','panzoombar','scale*true','scaleline','rotate','location','backgroundlayers','getfeatureinfo'],
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

* panzoombar: Añade una barra de desplazamiento para acercarse/alejarse del mapa.
* panzoom: Añade botones de '+' y '-' para acercarse y alejarse del mapa.
* scale: añade escala numérica
* scaleline: añade escala gráfica
* location: Añade un botón de centrado en la posición del usuario. Se le puede indicar si se desea posicionamiento continuo (tracking, por defecto a true) y alta precisión (highAccuracy, por defecto a false)
* rotate: Añade la funcionalidad girar el mapa para que el Norte esté arriba.a
* backgroundlayers: Añade selector de capas base. Ver sección 👇 cómo configurar el control **BackImageLayer**.
* getfeatureinfo: Añade la herramienta de consulta de información sobre capas WMS y WMST a través de su servicio getFeatureInfo. Por defecto, espera formato HTML como formato de respuesta. Otros formatos soportados son *gml* y *plain*. Admite también un buffer en pixeles opcional. Podemos configurarlo así:

```javascript
mapajs.addControls(new M.control.GetFeatureInfo(
                    'gml', 
                    {buffer: 1000}));
```

Los controles también pueden activarse o desactivarse por código:

```javascript
const ctrlLocation = mapajs.getControls({name:'location'})[0];
ctrlLocation.activate(); //para activarlo
ctrlLocation.deactivate(); //para desactivarlo
```

##  ⚙ Configuración inicial

Además de los ficheros Javascript y CSS con las especificaciones de la APICNIG, también se carga un fichero con una configuración inicial, entre las que se encuentrran el mapa fondo con el que se arranca o los mapas que se activan con el control **BackImageLayer**. Esta configuración puede customizarse antes de crear el mapa, de la siguiente manera

```javascript

// Botón 1 del control BackImageLayer
M.config.backgroundlayers[0].id = 'mapa';       //identificador: en minúsculas, sin caracteres especiales.
M.config.backgroundlayers[0].title = 'Vector';  //título: Cualquier carácter
M.config.backgroundlayers[0].layers = ['WMTS*https://www.ign.es/wmts/ign-base?*IGNBaseTodo*GoogleMapsCompatible*base*false*image/jpeg*false*false*true'];
// Otras opciones compatibles
//M.config.backgroundlayers[0].layers = ['WMTS*https://www.ign.es/wmts/ign-base?*IGNBaseTodo*GoogleMapsCompatible*base*false*image/jpeg*false*false*true'];
//M.config.backgroundlayers[0].layers = ['WMTS*https://www.ign.es/wmts/ign-base?*IGNBaseTodo-nofondo*GoogleMapsCompatible*base*false*image/png*false*false*true'];

//Botón 2 del control BackImageLayer
M.config.backgroundlayers[1].id = 'imagen';
M.config.backgroundlayers[1].title = 'Aérea';
//M.config.backgroundlayers[1].layers = ['WMTS*https://www.ign.es/wmts/pnoa-ma?*OI.OrthoimageCoverage*EPSG:4326*imagen*false*image/jpeg*false*false*true'];
M.config.backgroundlayers[1].layers = ['WMTS*https://www.ign.es/wmts/pnoa-ma?*OI.OrthoimageCoverage*GoogleMapsCompatible*imagen*false*image/jpeg*false*false*true'];

//Botón 3 del control BackImageLayer con la peculiaridad que una de las capas es una mezcla de dos
M.config.backgroundlayers[2].id = 'hibrido';
M.config.backgroundlayers[2].title = 'Mezcla';
M.config.backgroundlayers[2].layers = [
    'WMTS*https://www.ign.es/wmts/pnoa-ma?*OI.OrthoimageCoverage*GoogleMapsCompatible*imagen*true*image/jpeg*false*false*true',
    'WMTS*https://www.ign.es/wmts/ign-base?*IGNBaseOrto*GoogleMapsCompatible*Callejero*true*image/png*false*false*true'
];


//Así se configura el mapa por defecto, con el que arranca la App
M.config('wmts', {
    base: 'WMTS*https://www.ign.es/wmts/ign-base?*IGNBaseTodo*GoogleMapsCompatible**false',
});

// Restantes atribuciones
M.config.attributions.defaultAttribution = 'Instituto Geográfico Nacional';
M.config.attributions.defaultURL = 'https://www.ign.es';
```






## ⚙ Definición del estilo para poner etiquetas en los mapas

```javascript
    label: {
            /**
                * e2m: en este caso, meto una función anónima con el feature y el mapa como parámetro para que veáis cómo se pueden definir los estilos en función del zoom del mapa.
                * Como referencia utilizo el manual del API 👉 http://componentes.ign.es/api-core/doc/module-M_Control-Control.html
                * 👀❗️ Es importante que esta refererencia esté actualizada a la última versión. La que hay ahora es de la versión 1.0.0 según el título de la página.
                * A través del paramétro map accedo a las propiedades del objeto mapa. Una de ellas es el método getZoom que me informa del zoom que hay en pantalla
                * Lo que hago es no etiquetar si el zoom es menor que 8 para no emplastar la información
                */
            text: function(feature,map) {
                        if (map.getZoom()>=8){
                            return feature.getAttribute('identificador').trim()
                        }
                    },
            color: '#000000',
            offset: [0, -20],
            font: 'bold 10px Arial',
    }
```

## ⚙ Definiciones de estilo: puntos rojos y verdes

```javascript
//e2m: punto de tamaño 5 con relleno verde semitransparente y borde rojo
let estiloVerde = new M.style.Point({
                        radius: 5, 
                        fill: {  
                            color: 'green',
                            opacity: 0.5
                        },
                        stroke: {
                            color: '#FF0000'
                        }
                });

//e2m: punto de tamaño 5 con relleno verde semitransparente y borde rojo        
        let estiloRojo = new M.style.Point({
        radius: 5, 
        fill: {  
            color: 'green',
            opacity: 0.5
        },
        stroke: {
            color: '#FF0000'
        }
        });
```

## ⚙ Configuración de vistas rápidas

La configuración por defecto de las vistas básicas incluye Península, Baleares, Canarias, Ceuta y Melilla

```javascript
const mp12 = new M.plugin.SelectionZoom({
  position: 'TL',
  collapsible:  true,
  collapsed:  true,
  ids: 'peninsula,canarias,baleares,ceuta,melilla',
  titles: 'Peninsula,Islas Canarias,Illes Balears,Ceuta,Melilla',
  previews: 'img/espana.png,img/canarias.png,img/baleares.png,img/ceuta.png,img/melilla.png',
  bboxs: '-1200091.444315327, 365338.89496508264, 4348955.797933925, 5441088.058207252, -2170190.6639824593, -1387475.4943422542, 3091778.038884449, 3637844.1689537475 , 115720.89020469127, 507078.4750247937, 4658411.436032817, 4931444.501067467,-599755.2558583047, -587525.3313326766, 4281734.817081453, 4290267.100363785, -334717.4178261766, -322487.4933005484, 4199504.016876071, 4208036.300158403',
  zooms: '7,8,9,14,14',
});
```

---
[🔙 Volver](https://github.com/e2molin/viz-arquetipo#readme)
