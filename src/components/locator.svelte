<script>
   import Search from './search';
   import Marker from './marker';
   import Map from './map';

   let query = "Salt Lake";
   let markers = [];
   let location = [0, 0];
   let zoom = 0;

   $: if (query) {
      search(query).then(data => {
         markers = data.markers;
         location = data.location;
         zoom = 12;
      });
   }

   function handleSearch(e){
      query = e.detail.query;
   }

   async function search(query) {
      return await fetch(`${process.env.API_URL}/distance.json?q=${query}`).then(data => data.json());
   }
</script>

<Search on:search={handleSearch} query={query} />
<Map location={location} zoom={zoom}>
   {#each markers as marker (marker.id)}
      <Marker marker={marker}></Marker>
   {/each}
</Map>
