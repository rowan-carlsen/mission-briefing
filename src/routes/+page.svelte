<script>
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { TextPlugin } from 'gsap/TextPlugin';

	gsap.registerPlugin(TextPlugin);

	const planetImage = './planets/mission-1.png';
	let xPos = 0,
		yPos = 0,
		rotation = 0,
		ready = false,
		header,
		scan;
	onMount(() => {
		xPos = Math.random() * 100;
		yPos = Math.random() * 100;
		rotation = Math.random() * 360;
		document.fonts.ready.then(() => (ready = true));
	});
	$: if (ready) {
		gsap.to(header, {
			duration: 2,
			text: {
				value: 'MISSION BRIEFING',
				newClass: 'visible'
			}
		});
	}
</script>

<main class:visible={ready}>
	<h1 bind:this={header}>MISSION BRIEFING</h1>
	<section id="briefing">
		<div id="viewscreen" style="--xPos: {xPos}%; --yPos: {yPos}%; --rotation: {rotation}deg;">
			<img src={planetImage} alt="" id="planet" />
			<div bind:this={scan} id="scan"></div>
		</div>
		<div id="briefing-text">
			<p>
				Lorem ipsum dolor sit amet consectetur adipisicing elit. Et autem, fugiat, aliquam impedit
				nemo dolore quae optio ipsum culpa dignissimos, veritatis soluta corporis totam ea eveniet.
				Amet esse inventore vel? Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptates
				nesciunt reprehenderit, esse expedita distinctio, aut animi dolorem officiis enim, maxime
				eos corporis quas quasi neque delectus ea dignissimos natus. Velit!
			</p>
			<p>
				Lorem ipsum dolor sit amet consectetur adipisicing elit. Ducimus maiores quod, in
				dignissimos laboriosam voluptas praesentium molestias ratione non voluptatum repellat ad ab
				nobis illum harum doloribus debitis quidem tenetur! Lorem ipsum dolor sit amet, consectetur
				adipisicing elit. Distinctio eos dolores delectus nostrum sequi maiores corporis animi,
				atque aperiam praesentium aliquam facilis itaque dolorum fuga, quas cumque? Libero,
				perferendis quae.
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
	}
	:global(h1 .visible) {
		color: white;
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
		grid-template-columns: 1fr 0rem;
		margin: 0 0.5em;
		animation: slide-text 1s 0.5s forwards;
		overflow: hidden;
	}
	@keyframes slide-text {
		to {
			grid-template-columns: 1fr 20rem;
		}
	}
	#briefing-text {
		padding: 0.5em;
		border: 2px solid white;
		overflow: auto;
		width: 20rem;
		animation: fade-in 0.75s 1.5s forwards;
		opacity: 0;
	}
	@keyframes fade-in {
		to {
			opacity: 1;
		}
	}
	#briefing-text p:first-child {
		margin-top: 0;
	}
	#viewscreen {
		border: 2px solid white;
		margin: 0 auto;
		width: 800px;
		height: 600px;
		position: relative;
		overflow: hidden;
	}
	#viewscreen::before {
		content: '';
		position: absolute;
		top: 50%;
		left: 50%;
		translate: -50% -50%;
		margin: auto;
		width: 145%;
		height: 0;
		padding-bottom: 145%;
		background-image: url('space-bg-2.jpg');
		background-size: 2736px 1824px;
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
	}
	#planet {
		position: absolute;
		inset: 0;
		margin: auto;
	}
</style>
