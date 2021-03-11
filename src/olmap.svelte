<script>
    import Map from 'ol/Map'
    import View from 'ol/View'
    import TileLayer from 'ol/layer/Tile'
    import XYZ from 'ol/source/XYZ'
    import { fromLonLat } from 'ol/proj'

    const url = 'https://services.arcgisonline.com/ArcGIS/rest/services/World_Street_Map/MapServer/tile/{z}/{y}/{x}'

    //props 
    export let center;
    export let zoom;
    
    let viewDiv = "openlayersmap";
    let map = null;

    const setupMap = (node, _id) => {
        const arcgisLayer = new TileLayer({
            source: new XYZ({ url: url })
        })
        map = new Map({
            target: _id,
            layers: [arcgisLayer],
            view: new View({ 
                center: fromLonLat(center),
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
    <h1>OpenLayers</h1>
    <div id={viewDiv} class="map" use:setupMap={viewDiv}/>
</div>