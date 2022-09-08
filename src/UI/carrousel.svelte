<script>
	import {fade} from 'svelte/transition'
	export let carouselIMg =[
		'https://www.ecranlarge.com/media/cache/1600x1200/uploads/image/001/418/demon-slayer-photo-1418343.png',
		'https://www.newsmangas.fr/wp-content/uploads/2022/01/kid_law_vs_big_mom_by_melonciutus_deu79sf-fullview.jpeg',
        'https://static.actugaming.net/media/2018/10/180831_Endeavor_24_1538995558.jpg',
	];
	let index = 0;
	export let msecond = '1500';
	function autoPlay() {
		setInterval(() => {
			nextimg();
		}, msecond);
	}
	//function StopPlay() {
	//	clearInterval(() => {
	//		nextimg();
	//	}, 0);
	//}
	const nextimg = () => {
		index = (index + 1) % carouselIMg.length
	}
</script>

<style>
    img {
        width: 40%;
    }
</style>
{#key carouselIMg[index]}
	<img transition:fade src={carouselIMg[index]} alt="nextimg" />
{/key}
<br>
<button on:click={nextimg}>Next</button>
<button on:click={autoPlay}>Play</button>