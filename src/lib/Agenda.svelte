<script>
  import Clock from './Clock.svelte'

  export let address

  const increaseRepeater = createRepeater(increase, 100)
  const decreaseRepeater = createRepeater(decrease, 100)

  let minutes = 0
  let hours = 0
  let place

  function createRepeater(fn, delay) {
    let interval
    const start = () => {
      fn()
      interval = setInterval(fn, delay)
    }
    const stop = () => clearInterval(interval)
    return { start, stop }
  }

  function stopRepeaters() {
    increaseRepeater.stop()
    decreaseRepeater.stop()
  }

  function increase() {
    minutes += 5
    if (minutes >= 60) {
      hours += 1
      minutes = 0
    }
    if (hours >= 12) {
      hours = 0
    }
    selectPlace()
  }

  function decrease() {
    minutes -= 5
    if (minutes < 0) {
      hours -= 1
      minutes = 55
    }
    if (hours < 0) {
      hours = 11
    }
    selectPlace()
  }

  function selectPlace() {
    const morningTime = [
      String(hours).padStart(2, '0'),
      String(minutes).padStart(2, '0'),
    ].join(':')
    const afternoonTime = [
      String(hours + 12).padStart(2, '0'),
      String(minutes).padStart(2, '0'),
    ].join(':')
    place = address.schedule.find(({ time }) => {
      const [start, end] = time
      return (
        (morningTime >= start && morningTime <= end) ||
        (afternoonTime >= start && afternoonTime <= end)
      )
    })
  }

  function onKeyup(event) {
    const actions = {
      ArrowRight: increase,
      ArrowLeft: decrease,
      ArrowUp: increase,
      ArrowDown: decrease,
    }
    const { key } = event
    if (key in actions) {
      event.preventDefault()
      actions[key]()
    }
  }

</script>

<svelte:window
  on:keydown|nonpassive={onKeyup}
  on:mouseup={stopRepeaters}
  />

<div class="app">
  <div class="name">Welcome home {address.person}</div>
  <div class="instructions">Set the time to see where you will be</div>
  <div class="place">
    {#if place}
      {place.placeName}
    {/if}
  </div>
  <div class="clock">
    <Clock {minutes} {hours} />
  </div>
  <div>
    <button
      type="button"
      on:mousedown={decreaseRepeater.start}
      >-</button>
    <button
      type="button"
      on:mousedown={increaseRepeater.start}
      >+</button>
  </div>
</div>

<style>

  .app {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 2rem;
    height: 100vh;
    background-color: #4e3b3b;
    color: #fff;
  }

  .name {
    font-size: 2rem;
  }
  
  .place {
    font-size: 2rem;
    height: 4rem;
    font-weight: bold;
    color: #5dc54e;
  }

  .clock {
    width: 100%;
    max-height: 50vh;
    flex-grow: 1;
    display: flex;
    justify-content: center;
  }

  button {
    font-size: 5rem;
    padding: 0;
    width: 8rem;
    border-radius: 0.5rem;
    border: none;
    background-color: #fff;
    color: #333;
    cursor: pointer;
  }

  button:hover {
    background-color: #ccc;
  }

</style>
