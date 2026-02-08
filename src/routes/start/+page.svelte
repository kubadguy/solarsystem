<script>
	import { base } from '$app/paths';

	const nodes = [
		{ id: 'sun', label: 'Sun', tone: 'sun' },
		{ id: 'inner-planets', label: 'Inner Planets', tone: 'group' },
		{ id: 'mercury', label: 'Mercury', tone: 'inner' },
		{ id: 'venus', label: 'Venus', tone: 'inner' },
		{ id: 'earth', label: 'Earth', tone: 'earth' },
		{ id: 'moon', label: 'Moon', tone: 'moon' },
		{ id: 'mars', label: 'Mars', tone: 'inner' },
		{ id: 'asteroid-belt', label: 'Asteroid Belt', tone: 'belt' },
		{ id: 'outer-planets', label: 'Outer Planets', tone: 'group' },
		{ id: 'jupiter', label: 'Jupiter', tone: 'outer' },
		{ id: 'saturn', label: 'Saturn', tone: 'outer' },
		{ id: 'uranus', label: 'Uranus', tone: 'outer' },
		{ id: 'neptune', label: 'Neptune', tone: 'outer' },
		{ id: 'comets', label: 'Comets', tone: 'comet' },
		{ id: 'asteroids', label: 'Asteroids', tone: 'asteroid' },
		{ id: 'satellites', label: 'Satellites', tone: 'sat' }
	];
</script>

<main class="system">
	<header class="title">
		<h1>Solar System Map</h1>
		<p>Tap a body or region to open its page.</p>
	</header>

	<div class="track">
		{#each nodes as node}
			<a class={`node ${node.tone}`} href={`${base}/${node.id}`}>
				<span class="dot"></span>
				<span class="label">{node.label}</span>
			</a>
		{/each}
	</div>
</main>

<style>
	:global(body) {
		margin: 0;
		color: #e9ecff;
		font-family: "Space Grotesk", system-ui, sans-serif;
		background: #05060a;
	}

	.system {
		min-height: 100svh;
		padding: clamp(2rem, 5vw, 4rem);
		display: grid;
		gap: clamp(1.5rem, 3vw, 2.5rem);
	}

	.title h1 {
		margin: 0 0 0.4rem;
		font-family: "Unbounded", "Space Grotesk", system-ui, sans-serif;
		font-size: clamp(2rem, 4vw, 3rem);
	}

	.title p {
		margin: 0;
		color: rgba(233, 236, 255, 0.7);
	}

	.track {
		display: grid;
		gap: 0.9rem;
		align-items: center;
	}

	.node {
		display: grid;
		grid-auto-flow: column;
		align-items: center;
		justify-content: start;
		gap: 0.8rem;
		padding: 0.75rem 1rem;
		border-radius: 999px;
		border: 1px solid rgba(255, 255, 255, 0.08);
		background: rgba(10, 12, 20, 0.75);
		box-shadow: 0 12px 30px rgba(0, 0, 0, 0.4);
		text-decoration: none;
		color: inherit;
		transition: transform 0.2s ease, box-shadow 0.2s ease;
	}

	.node:hover {
		transform: translateY(-2px);
		box-shadow: 0 16px 36px rgba(0, 0, 0, 0.55);
	}

	.dot {
		width: 16px;
		height: 16px;
		border-radius: 50%;
		background: currentColor;
		box-shadow: 0 0 14px currentColor;
	}

	.label {
		font-size: 1rem;
		letter-spacing: 0.06em;
		text-transform: uppercase;
	}

	.node.sun {
		color: #ffd36b;
	}

	.node.group {
		color: #9bdcff;
	}

	.node.inner {
		color: #ff9a7a;
	}

	.node.earth {
		color: #5ce1ff;
	}

	.node.moon {
		color: #d9e1ff;
	}

	.node.belt {
		color: #c8b7ff;
	}

	.node.outer {
		color: #6b8bff;
	}

	.node.comet {
		color: #9ff0ff;
	}

	.node.asteroid {
		color: #ffb07b;
	}

	.node.sat {
		color: #8bf7c7;
	}

	@media (min-width: 900px) {
		.track {
			grid-auto-flow: column;
			grid-auto-columns: minmax(160px, 1fr);
			gap: 1rem;
			overflow-x: auto;
			padding-bottom: 0.5rem;
		}

		.node {
			justify-content: center;
		}
	}
</style>
