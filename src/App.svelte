<script>
  import AdressSelector from './lib/AdressSelector.svelte'
  import House from './lib/House.svelte'

  let address

  function onAddressSelect({ detail }) {
    address = detail
  }

</script>

<div class="app">
  {#if !address}
    <AdressSelector on:select={onAddressSelect} />
  {:else}
    <House {address} />
  {/if}
</div>

<style>

  .app {
    width: 100vw;
    height: 100vh;
  }

</style>

