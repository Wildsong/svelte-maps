<script>
    import Map from 'ol/Map'
    import View from 'ol/View'
    import OSM from 'ol/source/OSM'
    import TileLayer from 'ol/layer/Tile'
    import { fromLonLat, transform } from 'ol/proj'

    //props 
    export let center;
    export let zoom;
    export let options = {};

    const projection = options.projection || 'EPSG:3857';

    let viewDiv = "openlayersmap";
    let map = null;

    const setupMap = (node, _id) => {
        const osmLayer = new TileLayer({
            source: new OSM({
                // hide attributions from showing up in the middle of the map
                attributions: ''
            })
        })
        map = new Map({
            target: _id,
            layers: [osmLayer],
            view: new View({ 
                // if projection is not latlon we must convert
                center: projection === 'EPSG:4326' ? center : fromLonLat(center),
                zoom
            })
        });
        return {
            destroy() {
                if (map) {
                    map.setTarget(null);
                    map = null;
                }
            }
        }
    }
</script>

<div>
<h1>openlayers and mapbox</h1>
<div id={viewDiv} class="map" use:setupMap={viewDiv}/>
</div>

<style>
</style>


