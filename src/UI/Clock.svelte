
<script>
	import { onMount } from 'svelte';
	export let type;

	let time = new Date();

	$: hours = time.getHours();
	$: minutes = time.getMinutes();
	$: seconds = time.getSeconds();

  let minutesInterval = [0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55];
  let hoursInterval = [1, 2, 3, 4];

	onMount(() => {
		const interval = setInterval(() => {
			time = new Date();
		}, 1000);

		return () => {
			clearInterval(interval);
		};
	});




</script>


<svg viewBox='-50 -50 100 100' id="size">
	<circle class='rounded color-{type}' r='48' />

	{#each minutesInterval as minute}
		<line
			class='major'
			y1='35'
			y2='45'
			transform='rotate({30 * minute})'
		/>

		{#each hoursInterval as offset}
			<line
				class='minor'
				y1='42'
				y2='45'
				transform='rotate({6 * (minute + offset)})'
			/>
		{/each}
	{/each}

	<line
		class='hour'
		y1='2'
		y2='-20'
		transform='rotate({30 * hours + minutes / 2})'
	/>

	<line
		class='minute'
		y1='4'
		y2='-30'
		transform='rotate({6 * minutes + seconds / 10})'
	/>


	<g transform='rotate({6 * seconds})'>
		<line class='second' y1='10' y2='-38'/>
		<line class='second-counterweight' y1='10' y2='2'/>
	</g>
  <circle class="rounded-middle" r='3'/>
</svg>

<style>

	.color-blue{
		fill: blue;
	}
	.color-green{
		fill: green;
	}
	.color-black{
		fill: black;
	}
	.color-red{
		fill: red;
	}
	.color-salmon{
		fill: salmon;
	}
  #size{
    width: 150px;
    background-color: white;
    color: black;
  }
  #white{
    color: black;
  }
  label{
    display: block;
    color: black;
    font-weight: bold;
    font-size: 1.5em;
  }
	svg {
		width: 100%;
		height: 100%;
	}
  .rounded-middle{
    fill: white;
    z-index: 100;
  }

	.minor {
		stroke: #999;
		stroke-width: 0.5;
	}

	.major {
		stroke: white;
		stroke-width: 1;
	}

	.hour {
		stroke: white;
	}
	.minute {
		stroke: rgb(255, 255, 255);
	}
  g{
    z-index: 1;
  }
 .second, .second-counterweight {
		stroke: rgb(255, 0, 0);
	}

	.second-counterweight {
		stroke-width: 3;
	}
</style>