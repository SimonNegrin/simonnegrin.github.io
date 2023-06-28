<script>
  import { createEventDispatcher } from 'svelte'
  import { addressTitle } from './func'

  export let address

  const dispatch = createEventDispatcher()

  let password = ''

  function onSubmit() {
    if (address.password && address.password.toLowerCase() === password.toLowerCase()) {
      dispatch('open')
    }
  }

</script>

<div class="wall">
  <div class="up">
    <div class="title">{addressTitle(address)}</div>
  </div>
  <div class="down">
    <div class="door">
      <div class="handle"></div>
      <form on:submit|preventDefault={onSubmit}>
        <input
          type="text"
          class="password"
          placeholder="Password"
          bind:value={password}
          >
      </form>
    </div>
  </div>
</div>

<style>

  .wall {
    --units: 1.5vmax;
    --brick1: #4e3b3b;
    --brick2: #483434;
    --lines: #565656;
    --gp-ln: 50%/calc(var(--units) * 10) calc(var(--units) * 5);
    --gp-cn: 50%/calc(var(--units) * 5) calc(var(--units) * 5);
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    background: 
      repeating-conic-gradient(from 90deg at 95% 55%, var(--lines) 0% 25%, #fff0 0% 100%) var(--gp-cn), 
      repeating-linear-gradient(180deg, var(--lines) 0 5%, #fff0 0 50%, var(--lines) 0 55%, var(--brick2) 0 100% ) var(--gp-ln), 
      repeating-linear-gradient(90deg, var(--brick1) 0 47.5%, var(--lines) 0 50%, var(--brick1) 0 97.5%, var(--lines) 0 100% ) var(--gp-ln);
  }

  .up {
    height: 25%;
    font-size: 2rem;
    flex-grow: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .down {
    height: 75%;
    display: flex;
    justify-content: center;
    align-items: end;
  }

  .title {
    padding: 0.5rem;
    background-color: #222;
    color: bisque;
    border: 0.2rem solid bisque
  }

  .door {
    position: relative;
    height: 100%;
    aspect-ratio: 0.6;
    background-color: #222;
    border: 0.2rem solid bisque;
    border-bottom: none;
    border-top-left-radius: 5000rem;
    border-top-right-radius: 5000rem;
  }

  .handle {
    position: absolute;
    left: 1rem;
    top: calc(50% - 1rem);
    width: 2rem;
    height: 2rem;
    border-radius: 50%;
    background-color: bisque;
  }

  .password {
    position: absolute;
    left: 50%;
    top: 30%;
    transform: translate(-50%, -50%);
    width: 80%;
    height: 4rem;
    border-radius: 0.5rem;
    border: none;
    outline: none;
    background-color: #fff;
    color: #222;
    font-size: 2rem;
    text-align: center;
  }

</style>
