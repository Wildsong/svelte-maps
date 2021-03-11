# svelte-maps

I followed along with a presentation from the Esri Dev Summit
and built this Esri JSAPI example map app. Then I added OpenLayers for good measure.

It does nothing fancy. I want to link the extent together but that's not done yet.

The original presentation is on YouTube, <https://www.youtube.com/watch?v=Y_EVrWtBnow>

The project was created from the standard svelte project template at <https://github.com/sveltejs/template>.

## Additional help

* <https://esri-svelte-basemaps-example.now.sh/>
* <https://github.com/jwasilgeo/esri-svelte-basemaps-example>

## Get started

Install the dependencies.

```bash
cd svelte-app
npm install
```

Then start [Rollup](https://rollupjs.org):

```bash
npm run dev
```

Navigate to [localhost:5000](http://localhost:5000). You should see a street map. Edit a component file in `src`, save it, and in dev mode your page should update.


## Deploying to the web

The Svelte people suggest using Vercel.com or Surge.sh;
probably both fine ideas but I want to keep the content in my own servers.
To me the bundler is to make deployment simple, so "copy" is a good way to deploy too.

I think for me it's simpler, like perhaps

```bash
npm run build
rsync -av public/* cc-testmaps:docker/nginx/html
```

I have that automated with

```bash
npm run deploy
```
