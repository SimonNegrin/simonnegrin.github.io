<script>
  
  export let hours = 0
  export let minutes = 0

  let minutesAngle = 0
  let hoursAngle = 0

  $: updateClock(hours, minutes)

  function updateClock(hours, minutes) {
    hours = Math.abs(hours % 12)
    minutes = Math.abs(minutes % 60)
    const minFr = minutes / 60
    minutesAngle = 180 + 360 * minFr
    hoursAngle = 180 + 360 * ((hours + minFr) / 12)
  }

</script>

<div class="clock">
  <div class="center"></div>
  <div class="minutes" style="--minutesAngle: {minutesAngle}deg;"></div>
  <div class="hours" style="--hoursAngle: {hoursAngle}deg;"></div>
</div>

<style>

.clock {
  position: relative;
  aspect-ratio: 1;
  border-radius: 50%;
  background-color: #fff;
  box-sizing: border-box;
  min-height: 0;
  height: 100%;
  background-image: url('/clock.svg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
}

.center {
  --size: 8%;
  width: var(--size);
  height: var(--size);
  border-radius: 50%;
  background-color: #000;
  position: absolute;
  z-index: 2;
  top: calc(50% - var(--size) * 0.5);
  left: calc(50% - var(--size) * 0.5);
}

.minutes {
  --width: 2.5%;
  --height: 35%;
  width: var(--width);
  height: var(--height);
  border-radius: 5000rem;
  background-color: #5dc54e;
  position: absolute;
  top: 50%;
  left: calc(50% - var(--width) * 0.5);
  transform-origin: center top;
  transform: rotate(var(--minutesAngle));
}

.hours {
  --width: 4%;
  --height: 25%;
  width: var(--width);
  height: var(--height);
  border-radius: 5000rem;
  background-color: #ff63e0;
  position: absolute;
  top: 50%;
  left: calc(50% - var(--width) * 0.5);
  transform-origin: center top;
  transform: rotate(var(--hoursAngle));
}

</style>
