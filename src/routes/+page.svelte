<script>
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { TextPlugin } from 'gsap/TextPlugin';
	import missionData from '$lib/mission-data.js';
	const { randomValues, ...missions } = missionData;

	gsap.registerPlugin(TextPlugin);
	let selectedMission = 'Mission 1',
		xPos = 0,
		yPos = 0,
		rotation = 0,
		ready = false,
		{ isPlanet } = missionData[selectedMission],
		missionNumber = parseInt(selectedMission.split(' ')[1]),
		planetImage = `./${isPlanet ? 'planets' : 'locations'}/mission-${missionNumber}.png`;

	const timeline = gsap.timeline();
	onMount(() => {
		const randArray = randomValues[missionNumber - 1];
		randArray[2] *= 3.6;
		[xPos, yPos, rotation] = randArray;
		document.fonts.ready.then(() => (ready = true));
	});
	$: if (ready) {
		timeline.to('#scan', {
			clipPath: 'inset(0 0% 0 0)',
			duration: 0.75,
			ease: 'linear'
		});
		timeline.to('#scan', {
			opacity: 0,
			repeat: 4,
			duration: 0.5,
			ease: 'linear',
			yoyo: true
		});
		timeline.to(
			'#visual',
			{
				duration: 0.5,
				opacity: 1
			},
			'>-.75'
		);
		timeline.to('#header', {
			duration: 2,
			text: {
				value: 'MISSION BRIEFING'
			},
			ease: 'linear'
		});
		timeline.fromTo(
			'#briefing',
			{
				gridTemplateColumns: '1fr 0'
			},
			{
				gridTemplateColumns: '1fr 30rem'
			},
			'>+.5'
		);
		timeline.to('#briefing-text', {
			opacity: 1
		});
	}
</script>

<main class:visible={ready}>
	<select bind:value={selectedMission}>
		<option value="Mission 1">Mission 1</option>
	</select>
	<!-- svelte-ignore a11y_missing_content -->
	<h1 id="header">&nbsp;</h1>
	<section id="briefing">
		<div id="viewscreen" style="--xPos: {xPos}%; --yPos: {yPos}%; --rotation: {rotation}deg;">
			<div id="visual"><img src={planetImage} alt="" width="512" height="512" /></div>
			<div id="scan"></div>
		</div>
		<div id="briefing-text">
			<h2>LOCATION: PLANET ERIA, BRAGA SYSTEM</h2>
			<p>
				Eria is a lush and temperate world, settled some 1500 years ago. It is one of two inhabited
				planets in this system - its sister world, Ralos, is primarily arid and rocky. Eria and
				Ralos have a complex, intertwined history defined by periods of intense conflict followed by
				uneasy peace agreements. Shortly after the nearby Laos blinkgate finished construction, Eria
				petitioned Union for Core status, a process which can take years.
			</p>
			<p>
				Now that the approval for Eria's inclusion in the Core seems imminent, Ralos has made a
				move. Under the leadership of Imperador Zarat, who has swiftly unified the planet under
				military rule, Ralos launched a massive assault on the major population centers of Eria.
				Zarat's aim seems to be to seize power before Union can establish a significant presence in
				the system.
			</p>
			<p>
				While the situation is fraught, Union did foresee this possibility, and a tactical strike
				force was dispatched to the Braga system weeks ago. As the spearhead of this operation, your
				squad must make contact with Zarat's largest force on Eria and eliminate their long-range
				communications. The resulting chaos will allow our strike force to divide and conquer so as
				to minimize further civilian casualties.
			</p>
		</div>
	</section>
</main>
<div class="loader"></div>

<style>
	.loader {
		position: absolute;
		inset: 0;
		margin: auto;
		border-radius: 100%;
		width: 150px;
		height: 150px;
		border: 10px solid silver;
		border-top-color: #55f9;
		border-bottom-color: #55f9;
		animation: spin 1.5s linear infinite;
		z-index: -50;
	}
	@keyframes spin {
		to {
			rotate: 359.9deg;
		}
	}
	h1 {
		text-align: center;
		color: transparent;
		color: white;
		min-height: 1.5em;
		margin-top: 0;
	}

	main {
		visibility: hidden;
	}
	main.visible {
		visibility: visible;
	}
	main.visible ~ .loader {
		animation: none;
		display: none;
	}
	#briefing {
		display: grid;
		gap: 10px;
		grid-template-columns: 1fr 0rem;
		align-items: start;
		margin: 0 0.5em;
		overflow-x: clip;
		overflow-y: auto;
	}

	#briefing-text {
		padding: 0.5em;
		border: 2px solid white;
		overflow: auto;
		width: 30rem;
		opacity: 0;
		max-height: 100%;
		overflow: auto;
	}
	#briefing-text h2 {
		margin-top: 0;
	}
	#viewscreen {
		border: 2px solid white;
		margin: 0 auto;
		width: 100%;
		max-width: 800px;
		aspect-ratio: 1.33;
		position: relative;
		overflow: hidden;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	#visual {
		opacity: 0;
		width: 64%;
		max-width: 512px;
		min-width: 128px;
		max-height: 512px;
	}
	#visual img {
		width: 100%;
		height: 100%;
		min-width: 0;
	}
	#visual::before {
		content: '';
		position: absolute;
		top: 50%;
		left: 50%;
		translate: -50% -50%;
		margin: auto;
		width: 145%;
		height: 0;
		padding-bottom: 145%;
		background-image: url('/space-bg-2.jpg');
		background-size: 235% 211%;
		background-position: var(--xPos) var(--yPos);
		z-index: -5;
		transform: rotate(var(--rotation));
	}
	#scan {
		content: '';
		position: absolute;
		width: 100%;
		height: 100%;
		inset: 0;
		background-image: repeating-linear-gradient(
				transparent,
				transparent 48px,
				#16f529 48px,
				#16f529 50px
			),
			repeating-linear-gradient(to right, transparent, transparent 48px, #16f529 48px, #16f529 50px);
		z-index: 10;
		clip-path: inset(0 100% 0 0);
	}
	@media (max-width: 1000px) {
		#briefing {
			display: block;
		}
		#briefing-text {
			width: 90%;
			margin: 1em auto 0 auto;
		}
	}
</style>
