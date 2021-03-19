<script>
    import Map from 'ol/Map'
    import View from 'ol/View'
    import TileLayer from 'ol/layer/Tile'
    import XYZ from 'ol/source/XYZ'
    import { fromLonLat } from 'ol/proj'

    const esri_basemap_url = 'https://services.arcgisonline.com/ArcGIS/rest/services/Canvas/World_Light_Gray_Base/MapServer/tile/{z}/{y}/{x}'
    const rumsey_xyz_url = "http://maps.georeferencer.com/georeferences/e8148ea0-340f-553a-8a5d-fb35b9f7bef6/2019-09-14T06:05:24.397134Z/map/{z}/{x}/{y}.png?key=mpLuNUCkgUrSGkCrPyoT";
    
    //props 
    export let center;
    export let zoom;
    
    let viewDiv = "openlayersmap";
    let map = null;

    const setupMap = (node, _id) => {
        const arcgisLayer = new TileLayer({
            source: new XYZ({ url: esri_basemap_url })
        })
        const rumseyLayer = new TileLayer({
            source: new XYZ({ url: rumsey_xyz_url }),
            opacity: .70,
        })
        map = new Map({
            target: _id,
            layers: [
                arcgisLayer,
                rumseyLayer, 
            ],
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
    <h1>OpenLayers 6</h1>
    <div id={viewDiv} class="map" use:setupMap={viewDiv}/>
</div>