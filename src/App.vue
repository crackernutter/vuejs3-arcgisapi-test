<template>
  <div id="esri-map" ref="esriMap"></div>
</template>

<script>
import Map from "@arcgis/core/Map";
import MapView from "@arcgis/core/views/MapView";
import FeatureLayer from "@arcgis/core/layers/FeatureLayer";
import { defineComponent, nextTick } from "vue";


export default defineComponent({
  
  setup() {
    /**
     * do we really want vue to make these reactive? Are they really going to change?
     * this will add extra overhead. If we need to handle reactive changes on esri stuff,
     * we can take advantage by using "esri/core/watchUtils" or by using the Accessor.watch()
     */
    // let layer = ref(null);
    // let view = ref(null);

    //same issues with reactive object as well
    ///let app = reactive({ zones: null, view:null });
    
    // instead declare them as static data properties
    const map = new Map({
      basemap: "topo-vector",
    });

    const view = new MapView({
      container: "esri-map", // just pass this here to set required property
      map,
      zoom: 5,
      center: [-95, 39],
      popup: {
        autoOpenEnabled: false,
      },
    });

    const layer = new FeatureLayer({
      portalItem: {
        id: "9e2f2b544c954fda9cd13b7f3e6eebce",
      },
      outFields: ["*"],
      title: "Recent Earthquakes",
    });

    map.add(layer)

    return {
      view,
      map,
      layer
    }

  },

  created(){
    // verify we have access to view, layer
    console.log('view: ', this.view)
    console.log('map: ', this.map)
    
    /**
     * the map actually won't render from our setup() because the
     * "esri-map" div does not exist yet, so we must re-set it here 
     */
    nextTick(()=> this.view.container = this.$refs.esriMap)

    // here is where we can actually test things out
    this.view.whenLayerView(this.layer).then((layerView) => {
      console.log("layerview generated");
      console.log(layerView);
    });
  }
});
</script>

<style scoped>
#esri-map{
  padding:0;
  margin:0;
  height:100%;
}
</style>