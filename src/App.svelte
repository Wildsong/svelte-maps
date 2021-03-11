<script>
	import ArcGISMap from './arcgismap.svelte'
	import OpenlayersMap from './olmap.svelte'
	const astoria = [-123.8,46.2];
	const zoom = 12;
</script>

<main>
	<div class="mapcontainer">
		<OpenlayersMap center={astoria} zoom={zoom}/>
		<ArcGISMap center={astoria} zoom={zoom} /> 
	</div>

	<div class="footer">
		<p>This demo was built with the <a href="https://svelte.dev">Svelte framework</a> 
			to experiment with <a href="https:openlayers.org">OpenLayers</a> and 
			<a href="https://developers.arcgis.com/javascript/latest/">Esri ArcGIS API</a>
			to create similar maps, side-by-side.
			<i>I want to tie the extent of the two maps together
			but that's not what I am working on today.</i> 
		</p>
		<p>Total lines of code in this project: 131, ol map: 43, esri map: 41</p>
	</div>
</main>

<style>
	main {
		padding: 1em;
		margin: 0 auto;
	}
	.footer {
		width: 800px;
	}
	.mapcontainer {
		display: flex;
	}
	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>