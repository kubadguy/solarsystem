<script>
	import { base } from '$app/paths';
</script>

<main class="system">
	<header class="title">
		<h1>Solar System Map</h1>
		<p>Click any body or region to open its page.</p>
	</header>

	<div class="canvas">
		<svg class="map" viewBox="0 0 1600 420" role="img" aria-label="Solar system diagram">
			<defs>
				<radialGradient id="sunGlow" cx="50%" cy="50%" r="50%">
					<stop offset="0%" stop-color="#fff2b4" />
					<stop offset="55%" stop-color="#ffb347" />
					<stop offset="100%" stop-color="rgba(255, 179, 71, 0)" />
				</radialGradient>
				<linearGradient id="earthGlow" x1="0%" y1="0%" x2="100%" y2="100%">
					<stop offset="0%" stop-color="#3bd8ff" />
					<stop offset="100%" stop-color="#3b7bff" />
				</linearGradient>
				<linearGradient id="jupiterGlow" x1="0%" y1="0%" x2="100%" y2="100%">
					<stop offset="0%" stop-color="#f4c086" />
					<stop offset="100%" stop-color="#ff8f5a" />
				</linearGradient>
			</defs>

			<line class="path" x1="120" y1="210" x2="1540" y2="210" />

			<a href={`${base}/sun`} class="planet-link">
				<circle class="sun" cx="140" cy="210" r="70" fill="url(#sunGlow)" />
				<circle class="sun-core" cx="140" cy="210" r="30" />
				<text class="label" x="140" y="320">Sun</text>
			</a>

			<a href={`${base}/inner-planets`} class="group-link">
				<text class="group" x="370" y="90">Inner Planets</text>
			</a>

			<a href={`${base}/mercury`} class="planet-link">
				<circle class="planet mercury" cx="320" cy="210" r="8" />
				<text class="label" x="320" y="300">Mercury</text>
			</a>
			<a href={`${base}/venus`} class="planet-link">
				<circle class="planet venus" cx="390" cy="210" r="12" />
				<text class="label" x="390" y="300">Venus</text>
			</a>
			<a href={`${base}/earth`} class="planet-link">
				<circle class="planet earth" cx="470" cy="210" r="13" fill="url(#earthGlow)" />
				<text class="label" x="470" y="300">Earth</text>
			</a>
			<a href={`${base}/moon`} class="planet-link">
				<circle class="moon" cx="500" cy="184" r="5" />
				<text class="label small" x="510" y="170">Moon</text>
			</a>
			<a href={`${base}/mars`} class="planet-link">
				<circle class="planet mars" cx="560" cy="210" r="10" />
				<text class="label" x="560" y="300">Mars</text>
			</a>

			<a href={`${base}/asteroid-belt`} class="planet-link">
				<g class="belt">
					<circle cx="640" cy="200" r="2" />
					<circle cx="650" cy="220" r="3" />
					<circle cx="670" cy="210" r="2" />
					<circle cx="690" cy="195" r="2" />
					<circle cx="705" cy="225" r="3" />
					<circle cx="720" cy="205" r="2" />
				</g>
				<text class="label" x="680" y="300">Asteroid Belt</text>
			</a>

			<a href={`${base}/outer-planets`} class="group-link">
				<text class="group" x="920" y="90">Outer Planets</text>
			</a>

			<a href={`${base}/jupiter`} class="planet-link">
				<circle class="planet jupiter" cx="820" cy="210" r="26" fill="url(#jupiterGlow)" />
				<text class="label" x="820" y="300">Jupiter</text>
			</a>
			<a href={`${base}/saturn`} class="planet-link">
				<g class="saturn">
					<ellipse cx="950" cy="210" rx="32" ry="14" />
					<circle class="planet saturn-core" cx="950" cy="210" r="18" />
				</g>
				<text class="label" x="950" y="300">Saturn</text>
			</a>
			<a href={`${base}/uranus`} class="planet-link">
				<circle class="planet uranus" cx="1080" cy="210" r="16" />
				<text class="label" x="1080" y="300">Uranus</text>
			</a>
			<a href={`${base}/neptune`} class="planet-link">
				<circle class="planet neptune" cx="1180" cy="210" r="16" />
				<text class="label" x="1180" y="300">Neptune</text>
			</a>

			<a href={`${base}/comets`} class="planet-link">
				<path class="comet" d="M1340 170 l30 10 -30 10 z" />
				<circle class="comet-core" cx="1340" cy="180" r="6" />
				<text class="label" x="1340" y="300">Comets</text>
			</a>
			<a href={`${base}/asteroids`} class="planet-link">
				<g class="rock">
					<circle cx="1420" cy="210" r="8" />
					<circle cx="1436" cy="200" r="5" />
				</g>
				<text class="label" x="1430" y="300">Asteroids</text>
			</a>
			<a href={`${base}/satellites`} class="planet-link">
				<g class="sat">
					<rect x="1500" y="190" width="18" height="18" rx="3" />
					<rect x="1482" y="196" width="12" height="6" rx="2" />
					<rect x="1524" y="196" width="12" height="6" rx="2" />
				</g>
				<text class="label" x="1510" y="300">Satellites</text>
			</a>
		</svg>
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

	.map {
		width: min(1600px, 100%);
		height: auto;
	}

	.path {
		stroke: rgba(255, 255, 255, 0.1);
		stroke-width: 2;
	}

	.planet-link {
		cursor: pointer;
	}

	.planet-link:hover .label,
	.group-link:hover .group {
		fill: #ffffff;
	}

	.label {
		fill: rgba(233, 236, 255, 0.8);
		font-size: 14px;
		text-anchor: middle;
		letter-spacing: 0.08em;
		text-transform: uppercase;
	}

	.label.small {
		font-size: 11px;
		letter-spacing: 0.06em;
	}

	.group {
		fill: rgba(155, 220, 255, 0.8);
		font-size: 16px;
		text-anchor: middle;
		letter-spacing: 0.12em;
		text-transform: uppercase;
	}

	.sun-core {
		fill: #fff0b3;
		filter: drop-shadow(0 0 18px rgba(255, 200, 107, 0.65));
	}

	.planet {
		fill: #ff9a7a;
	}

	.planet.venus {
		fill: #ffc86b;
	}

	.planet.mars {
		fill: #ff7a6b;
	}

	.planet.jupiter {
		filter: drop-shadow(0 0 16px rgba(244, 192, 134, 0.45));
	}

	.planet.uranus {
		fill: #8cf0ff;
	}

	.planet.neptune {
		fill: #6b8bff;
	}

	.moon {
		fill: #d9e1ff;
	}

	.belt circle,
	.rock circle {
		fill: #c8b7ff;
	}

	.saturn ellipse {
		fill: rgba(255, 214, 138, 0.4);
		stroke: rgba(255, 214, 138, 0.7);
		stroke-width: 2;
	}

	.saturn-core {
		fill: #ffd6a1;
	}

	.comet {
		fill: rgba(159, 240, 255, 0.6);
	}

	.comet-core {
		fill: #c6f6ff;
	}

	.sat rect {
		fill: #8bf7c7;
	}

	@media (max-width: 900px) {
		.map {
			width: 1200px;
		}
	}
</style>
