# 🔌 [BackImgLayer]

## Definición de un control **BackImgLayer**

```javascript
const mp9 = new M.plugin.BackImgLayer({
    position: 'TR',
    collapsible: true,
    collapsed: true,
    layerId: 0,
    layerVisibility: true,
    columnsNumber: 4,
    layerOpts: [{
            id: 'mapa',
            preview: 'https://componentes.ign.es/api-core/plugins/backimglayer/images/svqmapa.png',
            title: 'Mapa',
            layers: [new M.layer.WMTS({
                url: 'http://www.ign.es/wmts/ign-base?',
                name: 'IGNBaseTodo',
                legend: 'Mapa IGN',
                matrixSet: 'EPSG:4326',
                transparent: false,
                displayInLayerSwitcher: false,
                queryable: false,
                visible: true,
                format: 'image/jpeg',
            })],
        },
        {
            id: 'imagen',
            title: 'Imagen',
            preview: 'https://componentes.ign.es/api-core/plugins/backimglayer/images/svqimagen.png',
            layers: [new M.layer.WMTS({
                url: 'http://www.ign.es/wmts/pnoa-ma?',
                name: 'OI.OrthoimageCoverage',
                legend: 'Imagen (PNOA)',
                matrixSet: 'EPSG:4326',
                transparent: false,
                displayInLayerSwitcher: false,
                queryable: false,
                visible: true,
                format: 'image/jpeg',
            })],
        },
        {
            id: 'hibrido',
            title: 'Híbrido',
            preview: 'https://componentes.ign.es/api-core/plugins/backimglayer/images/svqhibrid.png',
            layers: [new M.layer.WMTS({
                    url: 'http://www.ign.es/wmts/pnoa-ma?',
                    name: 'OI.OrthoimageCoverage',
                    legend: 'Imagen (PNOA)',
                    matrixSet: 'EPSG:4326',
                    transparent: true,
                    displayInLayerSwitcher: false,
                    queryable: false,
                    visible: true,
                    format: 'image/jpeg',
                }),
                new M.layer.WMTS({
                    url: 'http://www.ign.es/wmts/ign-base?',
                    name: 'IGNBaseOrto',
                    matrixSet: 'EPSG:4326',
                    legend: 'Mapa IGN',
                    transparent: false,
                    displayInLayerSwitcher: false,
                    queryable: false,
                    visible: true,
                    format: 'image/png',
                })
            ],
        },
        {
            id: 'lidar',
            preview: 'https://componentes.ign.es/api-core/plugins/backimglayer/images/svqlidar.png',
            title: 'LIDAR',
            layers: [new M.layer.WMTS({
                url: 'https://wmts-mapa-lidar.idee.es/lidar?',
                name: 'EL.GridCoverageDSM',
                legend: 'Modelo Digital de Superficies LiDAR',
                matrixSet: 'EPSG:4326',
                transparent: false,
                displayInLayerSwitcher: false,
                queryable: false,
                visible: true,
                format: 'image/png',
            })],
        },
        {
            id: 'mtnActual',
            preview: 'img/mtnactual.jpg',
            title: 'MTN Actual',
            layers: [wmtsMTNActual],
        },
        {
            id: 'mtn25',
            preview: 'img/mtn251Edi.jpg',
            title: 'MTN25 1Edi',
            layers: [wmtsMTN251edi],
        },
        {
            id: 'mtn50',
            preview: 'img/mtn501Edi.jpg',
            title: 'MTN50 1Edi',
            layers: [wmtsMTN501edi],
        },
        {
            id: 'SIOSE',
            preview: 'img/siose.jpg',
            title: 'CORINE / SIOSE',
            layers: [wmtssiose],
        },                
    ],
}
);
```