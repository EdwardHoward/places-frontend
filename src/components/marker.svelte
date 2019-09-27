<script>
   import { onMount, onDestroy, getContext } from 'svelte';
   import { key } from '../context/mapbox';

   export let marker;

   const { getMap } = getContext(key);
   const map = getMap();

   let mbMarker;

   onMount(() => {
      mbMarker = new mapboxgl.Marker();

      mbMarker.setLngLat([
         marker.location.y,
         marker.location.x
      ])

      mbMarker.addTo(map);
   });

   onDestroy(() => {
      mbMarker.remove();
   });
</script>