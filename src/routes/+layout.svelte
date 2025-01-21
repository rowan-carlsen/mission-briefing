<script>
	import { base } from '$app/paths';
</script>

<nav>
	<ul>
		<li><a href={`${base}/`}>MISSION</a></li>
		<li><a href={`${base}/crew`}>CREW</a></li>
	</ul>
</nav>
<slot />

<style>
	nav ul {
		display: flex;
		list-style-type: none;
		gap: 1em;
		padding: 0.5em 1em;
		margin: 0;
	}
	a {
		text-decoration: none;
		color: white;
	}
</style>
