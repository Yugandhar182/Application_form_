<script>
  import { onMount } from "svelte";
  import Grid from "gridjs-svelte";

  let jsonData = [];
  let tableVisible = false;

  onMount(async () => {
    await fetchData();
    tableVisible = true;
  });

  async function fetchData() {
    const response = await fetch("https://api.recruitly.io/api/job?apiKey=TEST64518616D4CF145D4E20BD47169EA7229BA3");
    const responseData = await response.json();
    jsonData = responseData.data;
  }
</script>

<main class="container mt-4">
  {#if tableVisible}
    <Grid
      search
      sort
      pagination={{ enabled: true, limit: 38 }}
      data={jsonData.map(item => ({
        id: item.id,
        title: item.title,
        reference: item.reference,
        status: item.status,
        industry: item.industry,
        
      }))} />
  {/if}
</main>

<style>
  @import "https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css";


  .gridjs-th {
    background-color: yellow;
  }
</style>
