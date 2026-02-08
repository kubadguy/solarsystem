<script>
	import { base } from '$app/paths';
	import { goto } from '$app/navigation';

	const imageUrl =
		'https://upload.wikimedia.org/wikipedia/commons/d/d9/Solar_System_graphic_by_NASA.png';

	const hotspots = [
		{ id: 'sun', label: 'Sun', x: 5, y: 68, size: 140 },
		{ id: 'mercury', label: 'Mercury', x: 15.5, y: 68, size: 28 },
		{ id: 'venus', label: 'Venus', x: 18.2, y: 66.5, size: 34 },
		{ id: 'earth', label: 'Earth', x: 20.5, y: 64.5, size: 36 },
		{ id: 'moon', label: 'Moon', x: 22.4, y: 61, size: 22 },
		{ id: 'mars', label: 'Mars', x: 24.8, y: 63.5, size: 30 },
		{ id: 'asteroid-belt', label: 'Asteroid Belt', x: 33.5, y: 58, size: 70 },
		{ id: 'ceres', label: 'Ceres', x: 31, y: 70, size: 26 },
		{ id: 'jupiter', label: 'Jupiter', x: 45.5, y: 62.5, size: 80 },
		{ id: 'saturn', label: 'Saturn', x: 54, y: 52, size: 80 },
		{ id: 'comets', label: 'Comets', x: 63.5, y: 75, size: 44 },
		{ id: 'uranus', label: 'Uranus', x: 71.5, y: 40, size: 52 },
		{ id: 'neptune', label: 'Neptune', x: 76.5, y: 36, size: 52 },
		{ id: 'pluto', label: 'Pluto', x: 86, y: 66, size: 36 },
		{ id: 'makemake', label: 'Makemake', x: 90, y: 80, size: 32 },
		{ id: 'kuiper-belt-objects', label: 'Kuiper Belt Objects', x: 93, y: 46, size: 70 },
		{ id: 'eris', label: 'Eris', x: 90, y: 20, size: 34 }
	];

	function onClick(event) {
		const target = event.currentTarget;
		const rect = target.getBoundingClientRect();
		const x = ((event.clientX - rect.left) / rect.width) * 100;
		const y = ((event.clientY - rect.top) / rect.height) * 100;

		let closest = hotspots[0];
		let closestScore = Infinity;

		for (const spot of hotspots) {
			const dx = x - spot.x;
			const dy = y - spot.y;
			const weight = Math.max(spot.size, 24) / 60;
			const score = (dx * dx + dy * dy) / weight;
			if (score < closestScore) {
				closestScore = score;
				closest = spot;
			}
		}

		goto(`${base}/${closest.id}`);
	}
</script>

<main class="system">
	<header class="title">
		<h1>Solar System Map</h1>
		<p>Click any body or region to open its page.</p>
	</header>

	<div class="canvas">
		<div class="image-frame" on:click={onClick} role="button" tabindex="0">
			<img src={imageUrl} alt="Solar system with the sun and planets" />
			<div class="hotspots">
				{#each hotspots as spot}
					<span class="hotspot" style={`--x:${spot.x}%; --y:${spot.y}%; --size:${spot.size}px;`}>
						<span class="sr-only">{spot.label}</span>
					</span>
				{/each}
			</div>
		</div>
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

	.canvas {
		width: 100%;
		overflow-x: auto;
		padding-bottom: 1rem;
	}

	.image-frame {
		position: relative;
		width: min(1200px, 100%);
		aspect-ratio: 16 / 9;
		border-radius: 24px;
		overflow: hidden;
		box-shadow: 0 30px 70px rgba(0, 0, 0, 0.55);
		border: 1px solid rgba(255, 255, 255, 0.08);
		cursor: pointer;
	}

	.image-frame img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		display: block;
		filter: saturate(1.05) contrast(1.05);
	}

	.hotspots {
		position: absolute;
		inset: 0;
	}

	.hotspot {
		position: absolute;
		left: var(--x);
		top: var(--y);
		transform: translate(-50%, -50%);
		width: var(--size);
		height: var(--size);
	}

	.hotspot::before {
		content: "";
		position: absolute;
		inset: 0;
		border-radius: 999px;
		background: radial-gradient(circle, rgba(255, 255, 255, 0.22), transparent 70%);
		opacity: 0.12;
		pointer-events: none;
	}

	.sr-only {
		position: absolute;
		width: 1px;
		height: 1px;
		padding: 0;
		margin: -1px;
		overflow: hidden;
		clip: rect(0, 0, 0, 0);
		white-space: nowrap;
		border: 0;
	}

	@media (max-width: 900px) {
		.image-frame {
			width: 1100px;
		}

		.label {
			letter-spacing: 0.1em;
		}
	}
</style>
