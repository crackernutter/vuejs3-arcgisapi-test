<template>
  <div id="esri-map"></div>
</template>

<script>
import Map from "@arcgis/core/Map";
import MapView from "@arcgis/core/views/MapView";
import FeatureLayer from "@arcgis/core/layers/FeatureLayer";
import { ref, onMounted } from "vue";

export default {
  setup() {
    let layer = ref(null);
    let view = ref(null);

    //same issues with reactive object as well
    ///let app = reactive({ zones: null, view:null });

    const setupMap = () => {
      const map = new Map({
        basemap: "topo-vector",
      });

      view.value = new MapView({
        container: "esri-map",
        map,
        zoom: 5,
        center: [-95, 39],
        popup: {
          autoOpenEnabled: false,
        },
      });

      layer.value = new FeatureLayer({
        portalItem: {
          id: "9e2f2b544c954fda9cd13b7f3e6eebce",
        },
        outFields: ["*"],
        title: "Recent Earthquakes",
      });

      try {
        //this will generate an error
        map.add(layer.value);
      } catch (e) {
        console.log("error with map.add(layer)");
        console.log(e);
        map.add(layer.value.load());
      }

      //this will also throw an error
      view.value.whenLayerView(layer.value).then((layerView) => {
        console.log("layerview generated");
        console.log(layerView);
      });
    };
    onMounted(setupMap);
    return { setupMap, view, layer };
  },
};
</script>

<style scoped>
#esri-map{
  padding:0;
  margin:0;
  height:100%;
}
</style>
