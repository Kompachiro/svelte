<script>

	let videoElement
	let videoVolume
	let videoSpeed = 1
	let isMuted
	let isPaused = true
	let videoTimeLine
	let isLoaded
	let hideVideoControls

	export let color = "#000"
	export let src = ''

	const playRates = [ 0.5, 1, 1.5, 2 ]

	const cssVariables = (node, variables) => {
		setCssVariables(node, variables);
		
		return {
			update(variables) {
				setCssVariables(node, variables);
			}
		}
	}

	const setCssVariables = (node, variables) => {
		for (const name in variables) {
			node.style.setProperty(`--${name}`, variables[name]);
		}
	}

	const toggleVideoStatus = () => {
		if ( videoElement.paused ) {
			videoElement.play()
			isPaused = false
		}
		else {
			videoElement.pause()
			isPaused = true
		}
	}

	const unmuteVideo = () => {
		isMuted = false
		videoVolume = .5
		setVolume()
	}

	const muteVideo = () => {
		isMuted = true
		videoElement.volume = 0
	}

	const setVolume = () => {
		videoElement.volume = videoVolume
		if ( videoVolume === 0 ) muteVideo()
	}

	const handleSpeedChange = (index) => {
		if (index === (playRates.length - 1)) {
			setSpeed(playRates[0])
			return
		}
		setSpeed(playRates[index + 1])
	}

	const setSpeed = (speed) => {
		videoSpeed = speed
		videoElement.playbackRate = videoSpeed
	}

	const updateTimeLine = () => {
		videoElement = videoElement
		videoTimeLine.style.transform = `translateX(${videoElement.currentTime / videoElement.duration * 100}%)`
	}

	const formatTime = (timeInSeconds) => {
		return `${fromSecondsToMinutes(timeInSeconds)}:${fromSecondstoCleanedSeconds(timeInSeconds)}`
	}

	const fromSecondstoCleanedSeconds = (timeInSeconds) => {
		if ( Math.trunc(timeInSeconds % 60) < 10 ) return `0${Math.trunc(timeInSeconds % 60)}`
		return Math.trunc(timeInSeconds % 60)
	}

	const fromSecondsToMinutes = (timeInSeconds) => {
		return Math.trunc(timeInSeconds / 60)
	}

</script>

<div class="video-player" use:cssVariables={{color}} on:mouseleave={() => { hideVideoControls = true } } on:mouseenter={() => { hideVideoControls = false } }>
	<video src={src} bind:this={videoElement} on:loadedmetadata={() => { isLoaded = true }} on:click={ toggleVideoStatus } on:timeupdate={ updateTimeLine }></video>
	<div class="gradient" class:controls-hidden={ hideVideoControls }></div>
	<div class="video-controls" class:controls-hidden={ hideVideoControls }>
		<button class="video-status-btn btn" on:click={ toggleVideoStatus }>
			<svg class:hide={ !isPaused } class="play" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 499.38 548.18"><g id="Calque_2" data-name="Calque 2"><g id="Calque_1-2" data-name="Calque 1"><path d="M499.37,274.07a91.89,91.89,0,0,1-47,81.43L141,535.24a91.86,91.86,0,0,1-94,0A91.89,91.89,0,0,1,0,453.81V94.33A91.88,91.88,0,0,1,47,12.94a91.86,91.86,0,0,1,94,0L452.36,192.65a91.86,91.86,0,0,1,47,81.42Z"/></g></g></svg>
			<svg class:hide={ isPaused } class="pause" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 394.74 526"><defs><style>.cls-1{fill-rule:evenodd;}</style></defs><g id="Calque_2" data-name="Calque 2"><g id="Calque_1-2" data-name="Calque 1"><path class="cls-1" d="M241.84,449.55V76.45C241.84,34.23,284.06,0,318.29,0a76.45,76.45,0,0,1,76.45,76.45v373.1c0,42.22-42.22,76.45-76.45,76.45a76.45,76.45,0,0,1-76.45-76.45Z"/><path class="cls-1" d="M0,449.55V76.45C0,34.23,42.22,0,76.45,0A76.45,76.45,0,0,1,152.9,76.45v373.1c0,42.22-42.22,76.45-76.45,76.45A76.45,76.45,0,0,1,0,449.55Z"/></g></g></svg>
		</button>
		<div class="side-column">
			<div class="volume-controls">
				<button class="btn">
					<svg on:click={ muteVideo } class:hide={ isMuted } xmlns="http://www.w3.org/2000/svg" viewBox="0 0 513.34 466.77"><g id="Calque_2" data-name="Calque 2"><g id="Calque_1-2" data-name="Calque 1"><path d="M303.34,23.43v420a23.36,23.36,0,0,1-11.67,20.07A21,21,0,0,1,280,466.76a23.22,23.22,0,0,1-11.66-3l-158-90.3h-87A23.35,23.35,0,0,1,0,350.1V116.76A23.34,23.34,0,0,1,23.34,93.43h87l158-90.31a23.35,23.35,0,0,1,35,20.31ZM420,233.43h0a160.75,160.75,0,0,0-48.06-115.5l-32.67,33.13h0a116.68,116.68,0,0,1,0,164.74l32.67,34.3A160.78,160.78,0,0,0,420,233.43Zm93.33,0A254.84,254.84,0,0,0,438.21,51.9L405.07,85a210,210,0,0,1,0,296.8L438.21,415a254.84,254.84,0,0,0,75.13-181.54Z"/></g></g></svg>
					<svg on:click={ unmuteVideo } class:hide={ !isMuted } xmlns="http://www.w3.org/2000/svg" viewBox="0 0 513.39 466.53"><g id="Calque_2" data-name="Calque 2"><g id="Calque_1-2" data-name="Calque 1"><path d="M141.63,390.93l161.7-161.7v214a23.32,23.32,0,0,1-11.67,20.07A21,21,0,0,1,280,466.53a23.29,23.29,0,0,1-11.67-3ZM391.53,141,357.7,174.87a114.39,114.39,0,0,1,15.63,58.33,116.61,116.61,0,0,1-34.06,82.36l32.66,34.31a163.33,163.33,0,0,0,19.6-207.67ZM458.27,74.3l-33.61,33.6a206.17,206.17,0,0,1,42,125.3,208.5,208.5,0,0,1-61.6,148.4l33.14,33.14h0A256.68,256.68,0,0,0,458.27,74.31ZM426.77,6.63,303.34,130.06V23.19a23.34,23.34,0,0,0-35-20.07l-158,90.07h-87A23.35,23.35,0,0,0,0,116.53V349.86a23.34,23.34,0,0,0,23.34,23.33H60.2L6.77,426.62,39.9,459.76l420-420Z"/></g></g></svg>
				</button>
				<input type="range" class="volume-jauge" bind:value={videoVolume} class:hide-jauge={ isMuted } on:change={ setVolume } min="0" max="1" step="0.1">
			</div>
		</div>
		<button class='video-speed-btn btn'>
			{ #each playRates as playRate, i}
				<span class="video-speed" on:click={ () => { handleSpeedChange(i) }} class:hide={videoSpeed != playRate} >x { playRate }</span>
			{ /each }
		</button>
		<a href={src} download class="btn">
			<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 224 302.4" class="download-btn"><g id="Calque_2" data-name="Calque 2"><g id="Calque_1-2" data-name="Calque 1"><path d="M112,0a16.8,16.8,0,0,0-16.8,16.8V190.92l-66.85-63c-6.24-6.66-18.29-6.86-24.5-.17s-4.06,18.43,1.39,24.5l95.21,89.6c7.75,5.74,15.24,6.35,23.1,0l95.2-89.6c5.68-5.83,7.69-17.89,1.4-24.5s-18.76-5.56-24.5.17l-66.85,63V16.8A16.8,16.8,0,0,0,112,0ZM33.57,268.8a16.8,16.8,0,0,0,0,33.6H190.38a16.8,16.8,0,1,0,0-33.6Z"/></g></g></svg>
		</a>
		{ #if isLoaded }
			<p class="video-time-display">{formatTime(videoElement.currentTime)} / {formatTime(videoElement.duration)}</p>
		{ /if }
		<div class="time-line-container">
			<div class="time-line" bind:this={videoTimeLine}></div>
		</div>
		<!-- <button class="video-speed" on:click={ setSpeed } >x{videoSpeed}</button> -->
	</div>
</div>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500&display=swap');

	.video-player {
		position: relative;
		width: 100%;
	}
	.video-time-display{
		color: var(--color);
	}

	.video-controls {
		display: flex;
		align-items: center;
		gap: 25px;
		position: absolute;
		right: 0;
		bottom: 0;
		left: 0;
		padding: 25px;
		transition: all .5s ease;
	}

	.gradient {
		position: absolute;
		left: 0;
		bottom: 0;
		right: 0;
		height: 250px;
		background: rgba(0,0,0,.5);
		background: linear-gradient(rgba(255,255,255,0) 0%, rgba(255,255,255,.08) 100%);
		transition: all .5s ease;
	}

	.video-status-btn {
		width: 30px;
		height: 30px;
	}

	.btn {
		display: block;
		width: 20px;
		height: 20px;
		border: none;
		background: none;
		padding: 0;
	}

	.btn-wrapper {
		display: flex;
		align-items: center;
		justify-content: space-between;
		width: 200px;
	}

	img {
		display: block;
		width: 100%;
		height: 100%;
	}

	.backward {
		transform: scaleX(-1);
	}

	video {
		display: block;
		width: 100%;
	}

	.volume-controls {
		display: flex;
		justify-content: center;
		align-items: center;
		gap: 5px;
	}

	.volume-jauge {
		width: 70px;
		transition: all .5s ease;
		height: 5px;
		background-color: rgba(0, 0, 0, 0.3);
		-webkit-appearance: none;
	}


	input[type=range]::-webkit-slider-thumb {
		height: 15px;
		width: 15px;
		border-radius: 100%;
		background: var(--color);
		cursor: pointer;
		-webkit-appearance: none;
	}

	.hide-jauge {
		width: 0;
		opacity: 0;
	}

	.video-speed-btn {
		border: 2px var(--color) solid;
		color: var(--color);
		font-weight: 500;
		width: auto;
		height: auto;
		border-radius: .3em;
		font-family: Poppins, sans-serif;
		transition: all .1s ease;
	}

	.video-speed-btn:hover {
		background: var(--color);
		color: white;
	}

	.video-speed {
		display: block;
		width: 40px;
		padding: .5em .3em;
		font-size: 1.3em;
	}
	
	.time-line-container {
		position: relative;
		width: 100%;
		height: 5px;
		background-color: rgba(0, 0, 0, 0.3);
		overflow-x: hidden;
	}
	
	.time-line {
		position: absolute;
		top: 0;
		left: -100%;
		width: 100%;
		height: 100%;
		background-color: var(--color);
	}

	.video-time-display {
		white-space: nowrap;
		font-family: Poppins, sans-serif;
		font-size: 1em;
	}

	path {
		fill: var(--color);
	}

	.controls-hidden {
		opacity: 0;
		pointer-events: none;
	}

	.hide {
		display: none;
	}

</style>