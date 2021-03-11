<script>
    import {onMount} from "svelte";
    import {loadModules} from "esri-loader";

    // props
    export let center;
    export let zoom;

    let viewDiv;

    // wait until the esri component has loaded
    // see https://svelte.dev/tutorial/onmount
    onMount(async() => {
        const esriLoaderOptions = {
            css: true
        };
        const [
            EsriMap, 
            MapView
        ] = await loadModules([
                'esri/Map', 
                'esri/views/MapView'
            ],
            esriLoaderOptions
        );
        const map = new EsriMap({
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
<h1>esri javascript api 4</h1>
<div id="map" class="map" bind:this={viewDiv}></div>
</div>

<style>
</style>


