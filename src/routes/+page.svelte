<script>
	import { base } from '$app/paths';
</script>

<main class="hero">
	<div class="backdrop"></div>
	<div class="grid"></div>

	<section class="card">
		<p class="eyebrow">Presentation by roll no. 19 to 27</p>
		<h1>Solar System</h1>
		<p class="lede">
			Lets look at our neighbourhood in Space from Earth
			to the sun.
		</p>
		<a class="cta" href={`${base}/start`}>Start</a>
	</section>

	<section class="scene" aria-hidden="true">
		<div class="particles"></div>
		<svg class="orbit" viewBox="0 0 420 420" role="presentation">
			<defs>
				<radialGradient id="sunGlow" cx="50%" cy="50%" r="50%">
					<stop offset="0%" stop-color="#fff3b0" />
					<stop offset="55%" stop-color="#ffb347" />
					<stop offset="100%" stop-color="rgba(255, 179, 71, 0)" />
				</radialGradient>
				<linearGradient id="planetGlow" x1="0%" y1="0%" x2="100%" y2="100%">
					<stop offset="0%" stop-color="#6b5bff" />
					<stop offset="100%" stop-color="#00d6ff" />
				</linearGradient>
			</defs>
			<circle class="ring ring-a" cx="210" cy="210" r="80" />
			<circle class="ring ring-b" cx="210" cy="210" r="120" />
			<circle class="ring ring-c" cx="210" cy="210" r="160" />
			<circle class="ring ring-d" cx="210" cy="210" r="200" />
			<circle class="sun" cx="210" cy="210" r="36" fill="url(#sunGlow)" />
			<circle class="sun-core" cx="210" cy="210" r="18" />
			<g class="planet orbit-a">
				<circle cx="210" cy="130" r="8" fill="url(#planetGlow)" />
			</g>
			<g class="planet orbit-b">
				<circle cx="210" cy="90" r="5" fill="#9bdcff" />
			</g>
			<g class="planet orbit-c">
				<circle cx="210" cy="50" r="6" fill="#ffc86b" />
			</g>
			<g class="planet orbit-d">
				<circle cx="210" cy="20" r="4" fill="#a7b7ff" />
			</g>
		</svg>
	</section>
</main>

<style>
	:global(body) {
		margin: 0;
		background:
			radial-gradient(circle at 15% 20%, rgba(35, 40, 90, 0.95), transparent 45%),
			radial-gradient(circle at 85% 10%, rgba(0, 150, 255, 0.35), transparent 40%),
			radial-gradient(circle at 20% 80%, rgba(130, 90, 255, 0.3), transparent 45%),
			radial-gradient(circle at 80% 85%, rgba(0, 214, 255, 0.28), transparent 40%),
			radial-gradient(circle at 50% 50%, #0a0b12 0%, #05060a 60%);
		background-size: 160% 160%;
		animation: glowshift 18s ease-in-out infinite;
		color: #e9ecff;
		font-family: "Space Grotesk", system-ui, sans-serif;
		min-height: 100svh;
	}

	:global(a) {
		color: inherit;
		text-decoration: none;
	}

	.hero {
		position: relative;
		min-height: 100svh;
		display: grid;
		place-items: center;
		gap: 3.5rem;
		overflow: hidden;
		padding: 4rem 1.5rem;
	}

	.backdrop {
		position: absolute;
		inset: -20%;
		background:
			radial-gradient(circle at 70% 30%, rgba(102, 90, 255, 0.35), transparent 45%),
			radial-gradient(circle at 20% 75%, rgba(0, 214, 255, 0.28), transparent 40%),
			radial-gradient(circle at 50% 50%, rgba(255, 255, 255, 0.05), transparent 50%);
		filter: blur(2px);
		z-index: 0;
	}

	.grid {
		position: absolute;
		inset: 0;
		background-image:
			linear-gradient(rgba(255, 255, 255, 0.06) 1px, transparent 1px),
			linear-gradient(90deg, rgba(255, 255, 255, 0.06) 1px, transparent 1px);
		background-size: 80px 80px;
		mask-image: radial-gradient(circle at 50% 40%, black 0%, transparent 70%);
		opacity: 0.35;
		z-index: 1;
	}

	.card {
		position: relative;
		z-index: 2;
		max-width: 680px;
		padding: 3.25rem 3rem;
		border-radius: 28px;
		background: linear-gradient(150deg, rgba(18, 20, 40, 0.9), rgba(8, 10, 20, 0.9));
		box-shadow:
			0 25px 60px rgba(0, 0, 0, 0.55),
			inset 0 0 0 1px rgba(255, 255, 255, 0.08);
		backdrop-filter: blur(12px);
	}

	.scene {
		position: relative;
		z-index: 1;
		width: min(460px, 85vw);
		aspect-ratio: 1;
		display: grid;
		place-items: center;
	}

	.orbit {
		width: 100%;
		height: 100%;
		filter: drop-shadow(0 12px 30px rgba(0, 0, 0, 0.45));
		animation: float 6s ease-in-out infinite;
	}

	.ring {
		fill: none;
		stroke: rgba(255, 255, 255, 0.18);
		stroke-width: 1;
		stroke-dasharray: 4 10;
	}

	.ring-a {
		animation: spin 18s linear infinite;
		transform-origin: 210px 210px;
	}

	.ring-b {
		animation: spin 26s linear infinite reverse;
		transform-origin: 210px 210px;
	}

	.ring-c {
		animation: spin 34s linear infinite;
		transform-origin: 210px 210px;
	}

	.ring-d {
		animation: spin 46s linear infinite reverse;
		transform-origin: 210px 210px;
	}

	.sun {
		opacity: 0.85;
	}

	.sun-core {
		fill: #fff0b3;
		filter: drop-shadow(0 0 18px rgba(255, 200, 107, 0.65));
	}

	.planet {
		transform-origin: 210px 210px;
	}

	.orbit-a {
		animation: spin 10s linear infinite;
	}

	.orbit-b {
		animation: spin 16s linear infinite reverse;
	}

	.orbit-c {
		animation: spin 22s linear infinite;
	}

	.orbit-d {
		animation: spin 28s linear infinite reverse;
	}

	.particles {
		position: absolute;
		inset: -10%;
		background-image:
			radial-gradient(circle at 10% 20%, rgba(255, 255, 255, 0.25) 0 1px, transparent 2px),
			radial-gradient(circle at 80% 30%, rgba(0, 214, 255, 0.3) 0 1px, transparent 2px),
			radial-gradient(circle at 20% 80%, rgba(255, 180, 92, 0.25) 0 1px, transparent 2px),
			radial-gradient(circle at 60% 70%, rgba(255, 255, 255, 0.2) 0 1px, transparent 2px),
			radial-gradient(circle at 45% 45%, rgba(123, 97, 255, 0.3) 0 1px, transparent 2px);
		background-size: 220px 220px;
		opacity: 0.6;
		animation: drift 18s linear infinite;
	}

	.card::before {
		content: "";
		position: absolute;
		inset: 0;
		border-radius: inherit;
		padding: 1px;
		background: linear-gradient(120deg, rgba(123, 97, 255, 0.7), rgba(0, 214, 255, 0.1));
		-webkit-mask: linear-gradient(#000 0 0) content-box, linear-gradient(#000 0 0);
		-webkit-mask-composite: xor;
		mask-composite: exclude;
		opacity: 0.6;
		pointer-events: none;
	}

	.eyebrow {
		font-size: 0.95rem;
		letter-spacing: 0.22em;
		text-transform: uppercase;
		color: rgba(233, 236, 255, 0.75);
		margin: 0 0 1.2rem;
	}

	h1 {
		font-family: "Unbounded", "Space Grotesk", system-ui, sans-serif;
		font-size: clamp(2.6rem, 5vw, 4rem);
		margin: 0 0 1rem;
		letter-spacing: 0.04em;
	}

	.lede {
		font-size: 1.1rem;
		line-height: 1.7;
		color: rgba(233, 236, 255, 0.82);
		margin: 0 0 2.5rem;
	}

	.cta {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		padding: 0.85rem 2.6rem;
		border-radius: 999px;
		background: linear-gradient(120deg, #6b5bff, #00d6ff);
		color: #0b0c14;
		font-weight: 600;
		letter-spacing: 0.12em;
		text-transform: uppercase;
		box-shadow: 0 16px 30px rgba(0, 214, 255, 0.25);
		transition: transform 0.2s ease, box-shadow 0.2s ease;
	}

	.cta:hover {
		transform: translateY(-2px);
		box-shadow: 0 18px 36px rgba(0, 214, 255, 0.35);
	}

	@keyframes spin {
		from {
			transform: rotate(0deg);
		}
		to {
			transform: rotate(360deg);
		}
	}

	@keyframes float {
		0%,
		100% {
			transform: translateY(0);
		}
		50% {
			transform: translateY(-10px);
		}
	}

	@keyframes drift {
		from {
			transform: translateY(0);
		}
		to {
			transform: translateY(-30px);
		}
	}

	@keyframes glowshift {
		0%,
		100% {
			background-position: 0% 0%;
		}
		50% {
			background-position: 100% 50%;
		}
	}

	@media (max-width: 600px) {
		.card {
			padding: 2.5rem 2rem;
		}

		.eyebrow {
			letter-spacing: 0.14em;
		}
	}
</style>
