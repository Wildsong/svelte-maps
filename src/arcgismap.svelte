<script>
    import {onMount} from "svelte";
    import {loadModules} from "esri-loader";

    // props
    export let center;
    export let zoom;

    let viewDiv = "arcmap";

    // wait until the esri component has loaded
    // see https://svelte.dev/tutorial/onmount
    onMount(async() => {
        const esriLoaderOptions = {
            css: true
        };
        const [
            ArcGISMap, 
            MapView
        ] = await loadModules([
                'esri/Map', 
                'esri/views/MapView'
            ],
            esriLoaderOptions
        );
        const map = new ArcGISMap({
            basemap: 'streets',
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
    <h1>ArcGIS API 4</h1>
    <div id={viewDiv} class="map" bind:this={viewDiv}></div>
</div>