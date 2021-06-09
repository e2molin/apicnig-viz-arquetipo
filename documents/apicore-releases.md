# API-CORE Releases

## 🚀 20200525 **APICNIG v3.3.17**

### ⚙️ API-CORE

* Se cambia configuración en entidades de búsqueda permitidas.
* Se crea test para **queryattributes**.

### 🔌 Plugins

* **fulltoc**: Se corrige bug al cargar capa de catastro en https.
* **infocoordinates**: Se corrige número de decimales mostrados en la altura de los puntos al navegar entre ellos.
* **printermap**: Se controlan estilos con patrón para rellenarlos con color uniforme pero con cierta opacidad. Se actualizan las configuraciones para la integración del nuevo servicio de fotogramas.
* **queryattributes**: Se crea primera versión de plugin de tabla de atributos.

## 🚀 20200507 **APICNIG v3.3.16**

### ⚙️ API-CORE

* Se cambia configuración en entidades de búsqueda permitidas.
### 🎮 Controles

* **backgroundlayers**: Se corrige bug que afectaba a la versión móvil y no mostraba las capas base en el orden correcto.

### 🔌 Plugins

* **fulltoc**: Se cambia forma de representar capas de un servicio para mostrar los distintos nodos padre en su título. Ignorar parámetros a la hora de comprobar la url para realizar la petición Capabilities. Sólo aplicar filtros de lista blanca cuando el servicio sea usado desde las capas precargadas. Se corrige bug provocado al realizar búsquedas con caracteres especiales en el catálogo CODSI. Se añade control de orden para añadir las capas al mapa según el orden que tengan en el popup de selección.
* **ignsearch**: Se cambia forma de mostrar los candidates, mostrando más tipos en el caso de que vengan del nomenclator y todos los tipos en el caso de resultados provenientes del CPS.
* **ignsearchlocator**: Se cambia forma de mostrar los candidates, mostrando más tipos en el caso de que vengan del nomenclator y todos los tipos en el caso de resultados provenientes del CPS.
* **information**: Se añade la opción de que el usuario pueda modificar el ancho del popup de información.
vectors: Se añade control para capas KML multigeométricas para que cargue cada tipo de geometrías es una capa distinta.

### ☑️ Tarea [#189141](https://www.guadaltel.es/redmine/issues/189141)

En estos momentos si un usuario introduce de forma manual la URL de un servicio y este ya estaba configurado con las capas precargadas le afecta al white_list. Haced que cuando el usuario introduzca directamente la URL pueda visualizar todas las capas.

### ☑️ Tarea [#189026](https://www.guadaltel.es/redmine/issues/189026)

Si un usuario carga el servicio con la siguiente cadena:

https://servicios.idee.es/wms-inspire/riesgos-naturales/inundaciones?request=GetCapabilities&service=WMS

en lugar de:

https://servicios.idee.es/wms-inspire/riesgos-naturales/inundaciones?

se carga el servicio, muestra las capas disponibles y las carga en el TOC pero luego no se visualiza. Permitir que un usuario cargue el servicio con la petición 

https://servicios.idee.es/wms-inspire/riesgos-naturales/inundaciones?request=GetCapabilities&service=WMS 

pero que llegue a mostrar las capas

### ☑️ Tarea [#188918](https://www.guadaltel.es/redmine/issues/188918)
  
Al cargar un servicio como por ejemplo 

ttps://www.ign.es/wms/pnoa-historico?SERVICE=WMS&&request=getcapabilities 

que se muestre la estructura de capas en forma de árbol según la jerarquía de capas del capabilities.  Cuando en un servicio haya varios grupos de Layer, que en el TOC se visualice los nombres de los padres. Por ejemplo, sea:

* Layer.nombre = 'PNOA10'
  * Layer.nombre = "2010"
    * Layer.nombre = "Madrid"

Que el nombre que se muestre en el TOC sea: **PNOA10.2010.Madrid**

Al cargar un servicios en el que haya Layes padres e hijos, al presentarse en la ventana de carga, debe ser visible la estructura de árbol del servicio manteniendo el orden que tiene.

### ☑️ Tarea [#189416](https://www.guadaltel.es/redmine/issues/189416)

Mostrar en los candidatos del "type" para las peticiones que llegan del CPS

### ☑️ Tarea [#189707](https://www.guadaltel.es/redmine/issues/189707)

Si se busca en el CODSI del fullTOC "hidrografía" da un error en el servidor. No sucede si se busca en 
https://www.idee.es/csw-codsi-idee/srv/spa/catalog.search#/search?any=hidrograf%C3%ADa

Ver por qué no se muestra y en cualquier caso controlar la excepción de forma que le aparezca un mensaje al usuario: "No hemos podido procesar su petición. Sentimos las molestias"

### ☑️ Tarea [#187693](https://www.guadaltel.es/redmine/issues/187693)

Hacer que el popup aumentase de tamaño por acción del usuario.

### ☑️ Tarea [#189838](https://www.guadaltel.es/redmine/issues/189838)

Al cargar un KML adopta el símbolo de puntos en lugar del de líneas. Lo que sucedía era que estaba cargando geometrías de varios tipos, ahora se separan y las carga en dos capas distintas.

---
## 🚀 20200419 APICNIG v3.3.15

### ☑️ Tarea [#188176](https://www.guadaltel.es/redmine/issues/188176)

Realizar los siguientes cambios en el listado de candidatos:
* No mostrar los resultados en Mayúsculas. Hacerlo tal y como vienen del Geocoder o del CPS
* Sólo añadir el atributo "Type" al resultado cuando se trate de Municipio, provincia o Comunidad Autónoma

Resultados de la Geometría:
* Quitar el relleno en los superficiales. Dejar únicamente el perímetro en azul.

### ☑️ Tareas [#188463](https://www.guadaltel.es/redmine/issues/188463) y [#188696](https://www.guadaltel.es/redmine/issues/188696)

* En ocasiones el servicio WMS devuelve un 404 ó un 500 directamente. En ese caso o en el de cualquier otro error, mostrar un mensaje indicando que "no ha podido realizarse la descarga en este momento. Por favor, inténtelo más tarde"
* Poner un timeout de 60s . Si no responde el servidor en ese tiempo, poner el mismo mensaje indicado anteriormente.
* Cuando está generando la imagen sale una ventana informando. Poner un botón "Cancelar" que permita volver a utilizar el visualizador y cancele la operación.

### ☑️ Otras tareas

* Se disminuye el nivel máximo de zoom
* Se genera nueva versión 

---

## 🚀 20200408 APICNIG v3.3.14

### ☑️ Tarea [#187342](https://www.guadaltel.es/redmine/issues/187342)

Añadir las entidades comentadas también a la lista de configuración de las entidades de búsqueda, para el uso del IGNSearch


### ☑️ Tarea [#187497](https://www.guadaltel.es/redmine/issues/187497)

🐛 Problema: En el visualizador [http://componentes.cnig.es/idee/visor](http://componentes.cnig.es/idee/visor) (IDEE) y para el servicio [http://wms.mapama.es/sig/Biodiversidad/MFE/wms.aspx](http://wms.mapama.es/sig/Biodiversidad/MFE/wms.aspx) la operación *GetFeatureInfo* no se maqueta bien.

🔧 Los problemas venían dados por una mala integración entre la maquetación propia de la respuesta a la petición *GetFeatureInfo* y la forma en la que se incluía en el popup. Se han establecido algunas reglas CSS para corregir y mostrar lo mejor posible el html.

Se puede probar en: [http://visores-cnig-gestion-publico.desarrollo.guadaltel.es/idee/](http://visores-cnig-gestion-publico.desarrollo.guadaltel.es/idee/)

---

## 🚀 20200329 APICNIG v3.3.13

### ⚙️ API-CORE

* Se rediseña página de galería de test de plugins.
* Se añade configuración de entidades a mostrar en las búsquedas del CPS en el fichero configurations.js.

### 🔌 PLUGINS

* **ignsearch**: Se externaliza la configuración entidades a mostrar en las búsquedas del CPS. Se corrige bug al realizar búsquedas. Se iguala la plantilla de resultados a la mostrada en plugin ignsearchlocator.
* **ignsearchlocator**: Se externaliza la configuración entidades a mostrar en las búsquedas del CPS. Se corrige bug al realizar búsquedas. Se activa proxy para petición de geolocalización de un resultado.
* **georefimage2**: Se replica el funcionamiento del anterior visor Iberpix para realizar la petición GetMap de forma directa.
* **vectors**: Se controlan las peticiones de altura para evitar usar las que devuelvan 0.
* **backimglayer**: Se añade configuración para mostrar la opción de "Ninguna capa".

---

## 🚀 20200315 APICNIG v3.3.12

### 🔌 Plugins

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

### ⚙️ API-CORE

Se elimina parámetro TILED en capas WMS con versión 1.3.0.
Se corrigen asignaciones de niveles de zoom obsoletas.

### 🔌 Plugins

* **fulltoc**: Se añade filtro por nombre de grupo al comprobar el parámetro white_list para poder filtrar dentro de un mismo servicio.
* **iberpixcompare**: Se mejora la usabilidad.
* **infocoordinates**: Se exporta elevación en fichero .txt.
* **comparepanel**: Se mejora la usabilidad.
* **mousesrs**: Se quita consulta de alturas a servicio WCS.