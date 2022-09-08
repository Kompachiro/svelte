<script>
	export let color = '#ff3e00';
	export let currentsize = '30';
</script>

<div>
	<h1>
		Choisis la couleur:
	</h1>
</div>

<input type="color" bind:value={color} style = { 'height: ' + currentsize + 'px; width: ' + currentsize + 'px' }> <br>
<input type="range" min="30" max="100" bind:value= {currentsize}>
{currentsize}

<style>
	h1{
		font-family: Arial;
	}
</style>
