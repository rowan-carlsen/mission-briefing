<script>
	//content
</script>

<main>
	<ul class="outer">
		<li>
			<div
				style="width:100%; aspect-ratio:1; color:white; display:flex;
            align-items:center; text-align:center; justify-content:center;font-size:min(4vw, 2em);"
			>
				NO VISUAL DATA
			</div>
			<!-- <img width="200" height="200" src="/players/guy.png" alt="NO VISUAL DATA" /> -->
			<ul class="inner">
				<li>Shrimp Kaiju</li>
				<li>CALLSIGN: CHUM</li>
				<li>MECH: Crawdaddy</li>
			</ul>
		</li>
		<li>
			<img width="200" height="200" src="/players/NoiseIsFolk.png" alt="" />
			<ul class="inner">
				<li>Ysaj Oxameter</li>
				<li>CALLSIGN: GEODE</li>
				<li>MECH: The Least of Your Problems</li>
			</ul>
		</li>
		<li>
			<img width="200" height="200" src="/players/Bocchi_the_sniper.png" alt="" />
			<ul class="inner">
				<li>Marissa Galanche</li>
				<li>CALLSIGN: BOCCHI</li>
				<li>MECH: Paranoia</li>
			</ul>
		</li>
		<li>
			<img width="200" height="200" src="/players/q-v2.png" alt="" />
			<ul class="inner">
				<li>Kaliya Azad</li>
				<li>CALLSIGN: MIST</li>
				<li>MECH: Lucky You</li>
			</ul>
		</li>
	</ul>
</main>

<style>
	.outer {
		display: flex;
		justify-content: space-between;
		gap: 5%;
		list-style-type: none;
	}
	.outer > li {
		width: 25%;
		display: flex;
		flex-flow: column;
		gap: 2em;
	}
	.inner {
		padding: 0 1em;
		text-align: left;
		line-height: 1.5;
		font-size: 1.2em;
		list-style-type: none;
	}
	.inner li {
		width: 100%;
	}
	.inner li:first-child {
		text-align: center;
		margin-bottom: 1em;
		font-size: 1.1em;
		font-weight: bold;
	}
	img {
		width: 100%;
		height: auto;
		color: white;
	}
</style>
