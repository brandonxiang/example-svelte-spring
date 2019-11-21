<script>
	import { spring } from 'svelte/motion';

	const calc = (x, y) => ({
		x: -(y - window.innerHeight / 2) / 20,
		y: (x - window.innerWidth / 2) / 20,
		s: 1.1
	})

	let coords = spring({ x: 0, y: 0, s: 1 }, {
		stiffness: 0.1,
		damping: 0.9,
		precision: 0.1
	});

	console.log($coords.x)
</script>

<div id="root">
  <div 
	  class="card"
		on:mousemove="{e => coords.set(calc(e.clientX, e.clientY))}"
		on:mouseout="{() => coords.set({x: 0, y:0, s: 1})}"
	  style="transform: perspective(600px) rotateX({$coords.x}deg) rotateY({$coords.y}deg) scale({$coords.s});"
	></div>

</div>

<style>
:global(body) {
	font-family: -apple-system, BlinkMacSystemFont, avenir next, avenir, helvetica neue, helvetica, ubuntu,
		roboto, noto, segoe ui, arial, sans-serif;
	background: transparent;
	-webkit-touch-callout: none;
	-webkit-user-select: none;
	-khtml-user-select: none;
	-moz-user-select: none;
	-ms-user-select: none;
	user-select: none;
	cursor: default;
}

:global(html,body) {
	width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
  background-color: white;
}


#root {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
  background-color: white;
}



#root {
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  background: #f0f0f0;
}

.card {
  width: 45ch;
  height: 45ch;
  background: grey;
  border-radius: 5px;
  background-image: url(https://drscdn.500px.org/photo/435236/q%3D80_m%3D1500/v2?webp=true&sig=67031bdff6f582f3e027311e2074be452203ab637c0bd21d89128844becf8e40);
  background-size: cover;
  background-position: center center;
  box-shadow: 0px 10px 30px -5px rgba(0, 0, 0, 0.3);
  transition: box-shadow 0.5s;
  will-change: transform;
  border: 15px solid white;
}

.card:hover {
  box-shadow: 0px 30px 100px -10px rgba(0, 0, 0, 0.4);
}

</style>