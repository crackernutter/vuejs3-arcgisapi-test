<<<<<<< HEAD
# vuejs3-arcgisapi-test
 
 ```
 Demo app showing how ArcGIS JS API seems to not play well with VueJS 3.x when JS API objects (e.g. FeatureLayers, MapViews) are set to reactive objects in the VueJS ecosystem.  
 I'm unsure why exactly this is happening but assume it has to do with Esri's Accessor not playingwell with JavaScript Proxy objects, on which VueJS 3.0 has based all reactive objects.
 
 Lines 42-54 in App.vue show how Esri's examples of adding feature layers to a map and getting access to a feature layer's LayerView do not work when the feature layer and the map view are set to reactive objets in Vue 3.0.
 ```

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
=======
# vuejs3-arcgisapi-test
Repo with demo app showing Esri ArcGIS API v 4.18 with ES Modules and VueJS 3.x
>>>>>>> 815dd9f8c3d53eebfdcf7e26499cd487b9d9b490
