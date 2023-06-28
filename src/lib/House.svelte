<script>
  import Agenda from './Agenda.svelte'
  import Door from './Door.svelte'

  export let address

  let isOpen = false

</script>

{#if !isOpen}
  <Door
    {address}
    on:open={() => isOpen = true}
    />
{:else}
  <Agenda
    {address}
    />
{/if}
