<script>
  import { createEventDispatcher } from 'svelte'
  import addresses from './addresses'
  import { addressTitle } from './func'

  const dispatch = createEventDispatcher()

  function onChange({ target }) {
    const address = addresses.find(address => addressTitle(address) === target.value)
    if (address) {
      dispatch('select', address)
    }
  }

</script>

<div>
  <select on:change={onChange}>
    <option value="">Select an address</option>
    {#each addresses as address}
      {@const title = addressTitle(address)}
      <option value={title}>{title}{address.person ? ` (${address.person})` : ''}</option>
    {/each}
  </select>
</div>
