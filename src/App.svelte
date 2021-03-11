<script>
	import EsriMap from './esrimap.svelte'
	import OpenlayersMap from './olmap.svelte'
	const astoria = [-123.8,46.2];
	const zoom = 12;
</script>

<main>
	<div class="mapcontainer">
		<OpenlayersMap center={astoria} zoom={zoom}/>
		<EsriMap center={astoria} zoom={zoom} /> 
		<br/>
	</div>

	<p>This is a sample app built with the Svelte framework 
		to experiment with using OpenLayers and 
		Esri Javascript API to create similar maps. 
	</p>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a>
		 to learn how to build Svelte apps.
	</p>
</main>

<style>
	main {
		padding: 1em;
		margin: 0 auto;
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