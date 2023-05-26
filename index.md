<!doctype html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="initial-scale=1,user-scalable=no,maximum-scale=1,width=device-width">
        <meta name="mobile-web-app-capable" content="yes">
        <meta name="apple-mobile-web-app-capable" content="yes">
        <link rel="stylesheet" href="css/leaflet.css"><link rel="stylesheet" href="css/L.Control.Locate.min.css">
        <link rel="stylesheet" href="css/qgis2web.css"><link rel="stylesheet" href="css/fontawesome-all.min.css">
        <link rel="stylesheet" href="css/leaflet-search.css">
        <link rel="stylesheet" href="css/leaflet-control-geocoder.Geocoder.css">
        <style>
        html, body, #map {
            width: 100%;
            height: 100%;
            padding: 0;
            margin: 0;
        }
        </style>
        <title></title>
    </head>
    <body>
        <div id="map">
        </div>
        <script src="js/qgis2web_expressions.js"></script>
        <script src="js/leaflet.js"></script><script src="js/L.Control.Locate.min.js"></script>
        <script src="js/leaflet.rotatedMarker.js"></script>
        <script src="js/leaflet.pattern.js"></script>
        <script src="js/leaflet-hash.js"></script>
        <script src="js/Autolinker.min.js"></script>
        <script src="js/rbush.min.js"></script>
        <script src="js/labelgun.min.js"></script>
        <script src="js/labels.js"></script>
        <script src="js/leaflet-control-geocoder.Geocoder.js"></script>
        <script src="js/leaflet-search.js"></script>
        <script src="data/WESTERN_SCH_TOTAL_HEALTH_T_1.js"></script>
        <script>
        var highlightLayer;
        function highlightFeature(e) {
            highlightLayer = e.target;

            if (e.target.feature.geometry.type === 'LineString') {
              highlightLayer.setStyle({
                color: '#ffff00',
              });
            } else {
              highlightLayer.setStyle({
                fillColor: '#ffff00',
                fillOpacity: 1
              });
            }
            highlightLayer.openPopup();
        }
        var map = L.map('map', {
            zoomControl:true, maxZoom:28, minZoom:8
        })
        var hash = new L.Hash(map);
        map.attributionControl.setPrefix('<a href="https://github.com/tomchadwin/qgis2web" target="_blank">qgis2web</a> &middot; <a href="https://leafletjs.com" title="A JS library for interactive maps">Leaflet</a> &middot; <a href="https://qgis.org">QGIS</a>');
        var autolinker = new Autolinker({truncate: {length: 30, location: 'smart'}});
        L.control.locate({locateOptions: {maxZoom: 19}}).addTo(map);
        var bounds_group = new L.featureGroup([]);
        function setBounds() {
            if (bounds_group.getLayers().length) {
                map.fitBounds(bounds_group.getBounds());
            }
        }
        map.createPane('pane_GoogleMaps_0');
        map.getPane('pane_GoogleMaps_0').style.zIndex = 400;
        var layer_GoogleMaps_0 = L.tileLayer('https://mt1.google.com/vt/lyrs=m&x={x}&y={y}&z={z}', {
            pane: 'pane_GoogleMaps_0',
            opacity: 1.0,
            attribution: '',
            minZoom: 8,
            maxZoom: 28,
        });
        layer_GoogleMaps_0;
        map.addLayer(layer_GoogleMaps_0);
        function pop_WESTERN_SCH_TOTAL_HEALTH_T_1(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (i in e.target._eventParents) {
                        e.target._eventParents[i].resetStyle(e.target);
                    }
                    if (typeof layer.closePopup == 'function') {
                        layer.closePopup();
                    } else {
                        layer.eachLayer(function(feature){
                            feature.closePopup()
                        });
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2"><strong>Constituency Name</strong>: ' + (feature.properties['CONST_NAME'] !== null ? autolinker.link(feature.properties['CONST_NAME'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2"><strong>Population Total</strong>: ' + (feature.properties['Total'] !== null ? autolinker.link(feature.properties['Total'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="3"><strong>MALE</strong>: ' + (feature.properties['Male'] !== null ? autolinker.link(feature.properties['Male'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="3"><strong>FEMALE</strong>: ' + (feature.properties['Female'] !== null ? autolinker.link(feature.properties['Female'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2"><strong>Total Number of Community Schools</strong>: ' + (feature.properties['Community'] !== null ? autolinker.link(feature.properties['Community'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="3"><strong>Total Number Of Primary Schools</strong>: ' + (feature.properties['Primary'] !== null ? autolinker.link(feature.properties['Primary'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2"><strong>Total Number of Secondary Schools</strong>: ' + (feature.properties['Secondary'] !== null ? autolinker.link(feature.properties['Secondary'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2"><strong>School Grand Total</strong>: ' + (feature.properties['SCH_TOTAL'] !== null ? autolinker.link(feature.properties['SCH_TOTAL'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2"><strong>Total Number of Level 2 Health Facilities</strong>: ' + (feature.properties['2nd_Level_'] !== null ? autolinker.link(feature.properties['2nd_Level_'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2"><strong>Total Number of Level 1 Health Facilities</strong>: ' + (feature.properties['1st_Level_'] !== null ? autolinker.link(feature.properties['1st_Level_'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2"><strong>Total Number of Health Centers</strong>: ' + (feature.properties['Health_Cen'] !== null ? autolinker.link(feature.properties['Health_Cen'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2"><strong>Total Number OF Health Posts</strong>: ' + (feature.properties['Health_Pos'] !== null ? autolinker.link(feature.properties['Health_Pos'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2"><strong>Total Number Of Min Hospitals</strong>: ' + (feature.properties['Mini_Hospi'] !== null ? autolinker.link(feature.properties['Mini_Hospi'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2"><strong>Health Facilities Grand Total</strong>: ' + (feature.properties['Grand_Tota'] !== null ? autolinker.link(feature.properties['Grand_Tota'].toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            layer.bindPopup(popupContent, {maxHeight: 400});
        }

        function style_WESTERN_SCH_TOTAL_HEALTH_T_1_0() {
            return {
                pane: 'pane_WESTERN_SCH_TOTAL_HEALTH_T_1',
                opacity: 1,
                color: 'rgba(0,0,0,1.0)',
                dashArray: '',
                lineCap: 'square',
                lineJoin: 'bevel',
                weight: 4.0,
                fillOpacity: 0,
                interactive: true,
            }
        }
        map.createPane('pane_WESTERN_SCH_TOTAL_HEALTH_T_1');
        map.getPane('pane_WESTERN_SCH_TOTAL_HEALTH_T_1').style.zIndex = 401;
        map.getPane('pane_WESTERN_SCH_TOTAL_HEALTH_T_1').style['mix-blend-mode'] = 'normal';
        var layer_WESTERN_SCH_TOTAL_HEALTH_T_1 = new L.geoJson(json_WESTERN_SCH_TOTAL_HEALTH_T_1, {
            attribution: '',
            interactive: true,
            dataVar: 'json_WESTERN_SCH_TOTAL_HEALTH_T_1',
            layerName: 'layer_WESTERN_SCH_TOTAL_HEALTH_T_1',
            pane: 'pane_WESTERN_SCH_TOTAL_HEALTH_T_1',
            onEachFeature: pop_WESTERN_SCH_TOTAL_HEALTH_T_1,
            style: style_WESTERN_SCH_TOTAL_HEALTH_T_1_0,
        });
        bounds_group.addLayer(layer_WESTERN_SCH_TOTAL_HEALTH_T_1);
        map.addLayer(layer_WESTERN_SCH_TOTAL_HEALTH_T_1);
        var osmGeocoder = new L.Control.Geocoder({
            collapsed: true,
            position: 'topleft',
            text: 'Search',
            title: 'Testing'
        }).addTo(map);
        document.getElementsByClassName('leaflet-control-geocoder-icon')[0]
        .className += ' fa fa-search';
        document.getElementsByClassName('leaflet-control-geocoder-icon')[0]
        .title += 'Search for a place';
        var baseMaps = {};
        L.control.layers(baseMaps,{'<img src="legend/WESTERN_SCH_TOTAL_HEALTH_T_1.png" /> WESTERN_SCH_TOTAL_HEALTH_T': layer_WESTERN_SCH_TOTAL_HEALTH_T_1,"Google Maps": layer_GoogleMaps_0,},{collapsed:false}).addTo(map);
        setBounds();
        map.addControl(new L.Control.Search({
            layer: layer_WESTERN_SCH_TOTAL_HEALTH_T_1,
            initial: false,
            hideMarkerOnCollapse: true,
            propertyName: 'CONST_NAME'}));
        document.getElementsByClassName('search-button')[0].className +=
         ' fa fa-binoculars';
        </script>
    </body>
</html>
