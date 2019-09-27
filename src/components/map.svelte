<script>
   import { onMount, setContext } from "svelte";
   import { key } from '../context/mapbox';

   export let location;
   export let zoom;

   let map;

   $: if(map && location && zoom){
      map.setZoom(zoom);
      map.setCenter([location[1], location[0]]);
   }

   setContext(key, {
      getMap: () => map
   });

   onMount(() => {
      mapboxgl.accessToken = process.env.MAPBOX_ACCESS_TOKEN;
         
      map = new mapboxgl.Map({
         container: "map",
         style: "mapbox://styles/mapbox/streets-v11",
         zoom
      })
   });
</script>

<style>

   .map-container {
      position: absolute;
      top: 0;
      width: 100%;
      height: 100%;
      padding-top: 50px;
   }

   #map {
      width: 100%;
      height: 100%;
   }
</style>

<div class="map-container">
   <div id="map">
      <slot></slot>
   </div>
</div>
