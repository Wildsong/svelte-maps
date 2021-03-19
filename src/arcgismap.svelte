<script>
    import {onMount} from "svelte";
    import {loadModules} from "esri-loader";

    // props
    export let center;
    export let zoom;

    // note that Esri requires changing {z}/{x}/{y} to {level}/{col}/{row}
    const rumsey_xyz_url = "http://maps.georeferencer.com/georeferences/e8148ea0-340f-553a-8a5d-fb35b9f7bef6/2019-09-14T06:05:24.397134Z/map/{z}/{x}/{y}.png?key=mpLuNUCkgUrSGkCrPyoT";

    let viewDiv = "arcmap";

    // wait until the esri component has loaded
    // see https://svelte.dev/tutorial/onmount
    onMount(async() => {
        const esriLoaderOptions = {
            css: true
        };

        // In a "normal" world these would be "imports"
        const [
            ArcGISMap, 
            MapView,
            WebTileLayer,
            esriConfig,
        ] = await loadModules([
                'esri/Map', 
                'esri/views/MapView',
                'esri/layers/WebTileLayer',
                'esri/config', 
            ],
            esriLoaderOptions
        );

        // THIS SIMPLY DOES NOT WORK. THE WORLD IS FULL OF STUPID CORS ERRORS AND THIS IS ONE
        // Using the XYZ tiles instead of the WMTS works around it.
        //esriConfig.request.trustedServers.push("https://maps.georeferencer.com");

        // see https://developers.arcgis.com/javascript/latest/api-reference/esri-layers-WMTSLayer.html
        const rumseyLayer = new WebTileLayer({
            // Tip, go to this URL and read the capabilities doc to find the correct id.
            urlTemplate: rumsey_xyz_url,
            opacity: .7,
        })

        const map = new ArcGISMap({
            layers: [ rumseyLayer ],
            basemap: 'gray',
        });

        const mapView = new MapView({
            container: viewDiv,
            map,
            center,
            zoom,
            ui: { components: ['zoom'] }
        })
    })
</script>

<div>
    <h1>ArcGIS JSAPI 4</h1>
    <div id={viewDiv} class="map" bind:this={viewDiv}></div>
</div>