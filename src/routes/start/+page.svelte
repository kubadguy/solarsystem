<script>
	import { base } from '$app/paths';
	const imageUrl =
		'https://upload.wikimedia.org/wikipedia/commons/6/6d/490_Our_Solar_System.jpg';

	const hotspots = [
		{ id: 'sun', label: 'Sun', x: 6, y: 52, size: 70 },
		{ id: 'inner-planets', label: 'Inner Planets', x: 26, y: 18, size: 90 },
		{ id: 'mercury', label: 'Mercury', x: 21, y: 52, size: 24 },
		{ id: 'venus', label: 'Venus', x: 26, y: 52, size: 28 },
		{ id: 'earth', label: 'Earth', x: 31, y: 52, size: 30 },
		{ id: 'moon', label: 'Moon', x: 33, y: 44, size: 18 },
		{ id: 'mars', label: 'Mars', x: 37, y: 52, size: 24 },
		{ id: 'asteroid-belt', label: 'Asteroid Belt', x: 45, y: 72, size: 60 },
		{ id: 'outer-planets', label: 'Outer Planets', x: 58, y: 18, size: 100 },
		{ id: 'jupiter', label: 'Jupiter', x: 56, y: 52, size: 50 },
		{ id: 'saturn', label: 'Saturn', x: 66, y: 52, size: 50 },
		{ id: 'uranus', label: 'Uranus', x: 74, y: 52, size: 38 },
		{ id: 'neptune', label: 'Neptune', x: 82, y: 52, size: 38 },
		{ id: 'comets', label: 'Comets', x: 90, y: 28, size: 34 },
		{ id: 'asteroids', label: 'Asteroids', x: 92, y: 70, size: 34 },
		{ id: 'satellites', label: 'Satellites', x: 96, y: 50, size: 34 }
	];
</script>

<main class="system">
	<header class="title">
		<h1>Solar System Map</h1>
		<p>Click any body or region to open its page.</p>
	</header>

	<div class="canvas">
		<div class="image-frame">
			<img src={imageUrl} alt="Solar system with the sun and planets" />
			<div class="hotspots">
				{#each hotspots as spot}
					<a
						class="hotspot"
						href={`${base}/${spot.id}`}
						style={`--x:${spot.x}%; --y:${spot.y}%; --size:${spot.size}px;`}
					>
						<span class="dot" aria-hidden="true"></span>
						<span class="label">{spot.label}</span>
					</a>
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
		text-decoration: none;
		color: #e9ecff;
		display: grid;
		justify-items: center;
		gap: 0.35rem;
		min-width: 90px;
	}

	.hotspot::before {
		content: "";
		position: absolute;
		width: var(--size);
		height: var(--size);
		border-radius: 999px;
		background: radial-gradient(circle, rgba(255, 255, 255, 0.22), transparent 70%);
		opacity: 0;
		transition: opacity 0.2s ease;
	}

	.hotspot:hover::before {
		opacity: 1;
	}

	.dot {
		width: clamp(10px, 1.2vw, 16px);
		height: clamp(10px, 1.2vw, 16px);
		border-radius: 50%;
		background: #ffffff;
		box-shadow: 0 0 14px rgba(255, 255, 255, 0.7);
	}

	.label {
		font-size: clamp(0.6rem, 1vw, 0.85rem);
		text-transform: uppercase;
		letter-spacing: 0.14em;
		background: rgba(5, 6, 10, 0.7);
		padding: 0.25rem 0.5rem;
		border-radius: 999px;
		border: 1px solid rgba(255, 255, 255, 0.12);
		white-space: nowrap;
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
