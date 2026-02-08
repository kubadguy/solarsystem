<script>
	import { base } from '$app/paths';
	import { goto } from '$app/navigation';

	const imageUrl =
		'https://upload.wikimedia.org/wikipedia/commons/d/d9/Solar_System_graphic_by_NASA.png';

	const ref = { w: 800, h: 500 };
	const rawHotspots = [
		{ id: 'sun', label: 'Sun', x: 80, y: 360 },
		{ id: 'mercury', label: 'Mercury', x: 185, y: 360 },
		{ id: 'venus', label: 'Venus', x: 215, y: 350 },
		{ id: 'earth', label: 'Earth', x: 245, y: 355 },
		{ id: 'moon', label: 'Moon', x: 260, y: 335 },
		{ id: 'mars', label: 'Mars', x: 275, y: 350 },
		{ id: 'asteroid-belt', label: 'Asteroid Belt', x: 330, y: 350 },
		{ id: 'ceres', label: 'Ceres', x: 360, y: 420 },
		{ id: 'jupiter', label: 'Jupiter', x: 430, y: 445 },
		{ id: 'saturn', label: 'Saturn', x: 460, y: 300 },
		{ id: 'uranus', label: 'Uranus', x: 560, y: 285 },
		{ id: 'neptune', label: 'Neptune', x: 610, y: 295 },
		{ id: 'pluto', label: 'Pluto', x: 665, y: 405 },
		{ id: 'makemake', label: 'Makemake', x: 705, y: 450 },
		{ id: 'eris', label: 'Eris', x: 720, y: 210 },
		{ id: 'kuiper-belt-objects', label: 'Kuiper Belt Objects', x: 710, y: 330 },
		{ id: 'comets', label: 'Comets', x: 565, y: 455 }
	];
	const hotspots = rawHotspots.map((spot) => ({
		...spot,
		px: (spot.x / ref.w) * 100,
		py: (spot.y / ref.h) * 100
	}));

	let hoveredId = null;

	function getNearest(x, y) {
		let closest = hotspots[0];
		let closestScore = Infinity;

		for (const spot of hotspots) {
			const dx = x - spot.px;
			const dy = y - spot.py;
			const score = dx * dx + dy * dy;
			if (score < closestScore) {
				closestScore = score;
				closest = spot;
			}
		}

		return closest;
	}

	function onClick(event) {
		const target = event.currentTarget;
		const rect = target.getBoundingClientRect();
		const x = ((event.clientX - rect.left) / rect.width) * 100;
		const y = ((event.clientY - rect.top) / rect.height) * 100;
		const closest = getNearest(x, y);
		goto(`${base}/${closest.id}`);
	}

	function onMove(event) {
		const target = event.currentTarget;
		const rect = target.getBoundingClientRect();
		const x = ((event.clientX - rect.left) / rect.width) * 100;
		const y = ((event.clientY - rect.top) / rect.height) * 100;
		hoveredId = getNearest(x, y)?.id ?? null;
	}

	function onLeave() {
		hoveredId = null;
	}
</script>

<main class="system">
	<header class="title">
		<h1>Solar System Map</h1>
		<p>Click any body or region to open its page.</p>
	</header>

	<div class="canvas">
		<div
			class="image-frame"
			on:click={onClick}
			on:mousemove={onMove}
			on:mouseleave={onLeave}
			role="button"
			tabindex="0"
		>
			<img src={imageUrl} alt="Solar system with the sun and planets" />
			<div class="hotspots">
				{#each hotspots as spot}
					<span
						class={`hotspot ${hoveredId === spot.id ? 'active' : ''}`}
						style={`--x:${spot.px}%; --y:${spot.py}%;`}
					>
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
		width: 52px;
		height: 52px;
	}

	.hotspot::before {
		content: "";
		position: absolute;
		inset: 0;
		border-radius: 999px;
		background: radial-gradient(circle, rgba(255, 255, 255, 0.4), transparent 70%);
		opacity: 0;
		transition: opacity 0.15s ease, transform 0.15s ease;
		pointer-events: none;
	}

	.hotspot.active::before {
		opacity: 0.85;
		transform: scale(1.15);
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
