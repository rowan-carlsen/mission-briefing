<script>
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	const players = [
		{
			name: 'Ysaj Oxameter',
			callsign: 'GEODE',
			mech: 'The Least of Your Problems',
			image: '/players/NoiseIsFolk.png'
		},
		{
			name: 'Marissa Galanche',
			callsign: 'BOCCHI',
			mech: 'Paranoia',
			image: '/players/Bocchi_the_sniper.png'
		},
		{
			name: 'Kaliya Azad',
			callsign: 'MIST',
			mech: 'Lucky You',
			image: '/players/q-v2.png'
		},
		{
			name: 'Shrimp Kaiju',
			callsign: 'CHUM',
			mech: 'Crawdaddy',
			image: ''
		}
	];
	onMount(() => {
		gsap.from('img', { y: -200, delay: 0.6, stagger: 0.4, opacity: 0, ease: 'power3' });
		gsap.from('.placeholder', { opacity: 0, ease: 'power3', delay: 1.8 });
	});
</script>

<main>
	<ul class="outer">
		{#each players as { name, callsign, mech, image }, i}
			<li>
				{#if image.length}
					<img width="200" height="200" src={image} alt="" />
				{:else}
					<div class="placeholder">NO VISUAL DATA</div>
				{/if}
				<ul class="inner">
					<li>{name}</li>
					<li>CALLSIGN: {callsign}</li>
					<li>MECH: {mech}</li>
				</ul>
			</li>
		{/each}
	</ul>
</main>

<style>
	.outer {
		display: grid;
		gap: 1em 5%;
		grid-template-rows: repeat(4, auto);
		grid-auto-columns: 1fr;
		grid-auto-flow: column;
		list-style-type: none;
	}
	.outer > li {
		display: contents;
		list-style-type: none;
	}
	.inner {
		display: contents;
	}
	.inner li {
		width: 100%;
		list-style-type: none;
		font-size: 1.2em;
	}
	.inner li ~ li {
		font-family: 'Courier New', Courier, monospace;
		font-weight: bold;
	}
	.inner li:first-child {
		text-align: center;
		margin-bottom: 1em;
		font-size: 1.4em;
		font-weight: bold;
	}
	img {
		width: 100%;
		height: auto;
	}
	.placeholder {
		color: white;
		font-size: min(4vw, 2em);
		display: flex;
		justify-content: center;
		align-items: center;
		aspect-ratio: 1;
		font-weight: bold;
	}
	@media (max-width: 800px) {
		:global(html) {
			font-size: 0.8rem;
		}
	}
</style>
