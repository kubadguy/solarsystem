<main class="hero">
	<div class="backdrop"></div>
	<div class="grid"></div>

	<section class="card">
		<p class="eyebrow">Presentation by roll no. 19 to 27</p>
		<h1>Solar System</h1>
		<p class="lede">
			A dark, focused journey through our neighborhood in space. A cinematic opening with a clean path
			forward.
		</p>
		<a class="cta" href="/start">Start</a>
	</section>
</main>

<style>
	:global(body) {
		margin: 0;
		background: radial-gradient(circle at 20% 20%, #1b1e3f, #0a0b12 55%, #05060a);
		color: #e9ecff;
		font-family: "Space Grotesk", system-ui, sans-serif;
		min-height: 100vh;
	}

	:global(a) {
		color: inherit;
		text-decoration: none;
	}

	.hero {
		position: relative;
		min-height: 100vh;
		display: grid;
		place-items: center;
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

	@media (max-width: 600px) {
		.card {
			padding: 2.5rem 2rem;
		}

		.eyebrow {
			letter-spacing: 0.14em;
		}
	}
</style>
