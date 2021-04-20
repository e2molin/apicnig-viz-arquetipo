# APIcore Releases


## 🚀 20200419 APICNIG v3.3.15

### Tarea [#188176](https://www.guadaltel.es/redmine/issues/188176)

Realizar los siguientes cambios en el listado de candidatos:
* No mostrar los resultados en Mayúsculas. Hacerlo tal y como vienen del Geocoder o del CPS
* Sólo añadir el atributo "Type" al resultado cuando se trate de Municipio, provincia o Comunidad Autónoma

Resultados de la Geometría:
* Quitar el relleno en los superficiales. Dejar únicamente el perímetro en azul.

### Tareas [#188463](https://www.guadaltel.es/redmine/issues/188463) y [#188696](https://www.guadaltel.es/redmine/issues/188696)

* En ocasiones el servicio WMS devuelve un 404 ó un 500 directamente. En ese caso o en el de cualquier otro error, mostrar un mensaje indicando que "no ha podido realizarse la descarga en este momento. Por favor, inténtelo más tarde"
* Poner un timeout de 60s . Si no responde el servidor en ese tiempo, poner el mismo mensaje indicado anteriormente.
* Cuando está generando la imagen sale una ventana informando. Poner un botón "Cancelar" que permita volver a utilizar el visualizador y cancele la operación.

### Otras tareas

* Se disminuye el nivel máximo de zoom
* Se genera nueva versión 

---

## 🚀 20200408 APICNIG v3.3.14

### Tarea [#187342](https://www.guadaltel.es/redmine/issues/187342)

Añadir las entidades comentadas también a la lista de configuración de las entidades de búsqueda, para el uso del IGNSearch


### Tarea [#187497](https://www.guadaltel.es/redmine/issues/187497)

🐛 Problema: En el visualizador [http://componentes.cnig.es/idee/visor](http://componentes.cnig.es/idee/visor) (IDEE) y para el servicio [http://wms.mapama.es/sig/Biodiversidad/MFE/wms.aspx](http://wms.mapama.es/sig/Biodiversidad/MFE/wms.aspx) la operación *GetFeatureInfo* no se maqueta bien.

🔧 Los problemas venían dados por una mala integración entre la maquetación propia de la respuesta a la petición *GetFeatureInfo* y la forma en la que se incluía en el popup. Se han establecido algunas reglas CSS para corregir y mostrar lo mejor posible el html.

Se puede probar en: [http://visores-cnig-gestion-publico.desarrollo.guadaltel.es/idee/](http://visores-cnig-gestion-publico.desarrollo.guadaltel.es/idee/)

---

## 🚀 20200329 APICNIG v3.3.13

### CORE

* Se rediseña página de galería de test de plugins.
* Se añade configuración de entidades a mostrar en las búsquedas del CPS en el fichero configurations.js.

### PLUGINS

* **ignsearch**: Se externaliza la configuración entidades a mostrar en las búsquedas del CPS. Se corrige bug al realizar búsquedas. Se iguala la plantilla de resultados a la mostrada en plugin ignsearchlocator.
* **ignsearchlocator**: Se externaliza la configuración entidades a mostrar en las búsquedas del CPS. Se corrige bug al realizar búsquedas. Se activa proxy para petición de geolocalización de un resultado.
* **georefimage2**: Se replica el funcionamiento del anterior visor Iberpix para realizar la petición GetMap de forma directa.
* **vectors**: Se controlan las peticiones de altura para evitar usar las que devuelvan 0.
* **backimglayer**: Se añade configuración para mostrar la opción de "Ninguna capa".

---

## 🚀 20200315 APICNIG v3.3.12

### PLUGINS

* **georefimage2**: Se crea nuevo plugin de descarga de imagen georreferenciada.
* **ignsearch**: Se cambian etiquetas del plugin. Cuando se localiza geometría lineal realizar zoom a la extensión de la geometría. Se separan las consultas a idee y cartociudad para que no condicionen la una a la otra y se muestren según van respondiendo los servicios.
* **ignsearchlocator**: Se cambian etiquetas del plugin. Cuando se localiza geometría lineal realizar zoom a la extensión de la geometría. Se separan las consultas a idee y cartociudad para que no condicionen la una a la otra y se muestren según van respondiendo los servicios.
* **vectors**: Se realiza un cambio de diseño. Se integra nueva funcionalidad de cálculo de distancia 3D. Se ha configurado una mayor tolerancia a los click muy juntos para que no se detecte como doble click y no se den inconvenientes a la hora de trazar rutas.
* **beautytoc**: Se desactiva proxy para petición de imagen de comprobación de cobertura de capa de vuelo.
* **fulltoc**: Se controla el scroll al realizar operaciones con las capas para que no se ignore. Se añade configuración de capas precargadas por defecto para cuando se invoque el plugin sin parametrizar.
* **mousesrs**: Se vuelve a habilitar la consulta de alturas para mostrarlas con el movimiento del ratón.
printermap: Se añade gestión para poder imprimir los resultados de dibujar puntos con la herramienta infocoordinates.

---

## 🚀 20200222 APICNIG v3.3.11

### API-CORE

Se elimina parámetro TILED en capas WMS con versión 1.3.0.
Se corrigen asignaciones de niveles de zoom obsoletas.

### PLUGINS

* **fulltoc**: Se añade filtro por nombre de grupo al comprobar el parámetro white_list para poder filtrar dentro de un mismo servicio.
* **iberpixcompare**: Se mejora la usabilidad.
* **infocoordinates**: Se exporta elevación en fichero .txt.
* **comparepanel**: Se mejora la usabilidad.
* **mousesrs**: Se quita consulta de alturas a servicio WCS.