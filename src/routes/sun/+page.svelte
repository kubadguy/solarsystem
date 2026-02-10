<main class="sun-page">
	<header class="hero">
		<p class="tag">Star at the Center</p>
		<h1>The Sun</h1>
		<p class="intro">
			The Sun is not a planet. It is a giant star made of super‑hot gas. Everything in our solar system
			goes around it, and its light gives Earth daytime, warmth, and energy for life.
		</p>
	</header>

	<section class="cards">
		<article class="card">
			<h2>Quick Facts</h2>
			<ul>
				<li>It is the closest star to Earth.</li>
				<li>It is huge: you could fit many Earths across its width.</li>
				<li>Its light reaches Earth in a little over 8 minutes.</li>
				<li>It spins, but not like a solid ball — the middle and the edges turn at different speeds.</li>
			</ul>
		</article>

		<article class="card">
			<h2>How It Shines</h2>
			<p>
				Deep inside, the Sun is so hot and squeezed that tiny particles smash together and release
				energy. That energy moves outward and finally leaves the surface as bright light and heat.
			</p>
			<p>
				When sunlight reaches Earth, it powers plants, warms oceans and land, and helps drive weather.
			</p>
		</article>

		<article class="card">
			<h2>Layers You Can Imagine</h2>
			<ol>
				<li>
					<strong>Core</strong> – the deep center where energy is made.
				</li>
				<li>
					<strong>Middle zones</strong> – energy slowly travels outward.
				</li>
				<li>
					<strong>Surface</strong> – the bright part we can see.
				</li>
				<li>
					<strong>Outer glow</strong> – a thin, very hot atmosphere that can look like a crown during
					an eclipse.
				</li>
			</ol>
		</article>
	</section>

	<section class="spotlight">
		<h2>Sunspots & Storms</h2>
		<p>
			Sometimes dark spots appear on the Sun. These are cooler areas with strong magnetic fields.
			The Sun can also blast out bursts of energy called solar storms. On Earth, those storms can
			make beautiful auroras near the poles.
		</p>
	</section>

	<section class="tips">
		<h2>Safety First</h2>
		<p>
			Never look directly at the Sun with your eyes. It can damage your vision. Use special solar
			viewing glasses or watch through a safe projection method.
		</p>
	</section>
</main>

<style>
	:global(body) {
		margin: 0;
		font-family: "Space Grotesk", system-ui, sans-serif;
		color: #f6f3ff;
		background:
			radial-gradient(circle at 15% 15%, rgba(255, 200, 90, 0.4), transparent 45%),
			radial-gradient(circle at 80% 20%, rgba(255, 120, 40, 0.25), transparent 40%),
			radial-gradient(circle at 50% 80%, rgba(255, 90, 0, 0.22), transparent 45%),
			linear-gradient(160deg, #07060a 10%, #140a08 55%, #0b0812 100%);
		min-height: 100svh;
	}

	.sun-page {
		min-height: 100svh;
		padding: clamp(2rem, 5vw, 4rem);
		display: grid;
		gap: clamp(2rem, 4vw, 3.5rem);
	}

	.hero {
		max-width: 720px;
	}

	.tag {
		margin: 0 0 0.75rem;
		letter-spacing: 0.28em;
		text-transform: uppercase;
		font-size: 0.85rem;
		color: rgba(255, 220, 170, 0.8);
	}

	h1 {
		margin: 0 0 1rem;
		font-family: "Unbounded", "Space Grotesk", system-ui, sans-serif;
		font-size: clamp(2.5rem, 5vw, 4rem);
	}

	.intro {
		margin: 0;
		font-size: clamp(1.05rem, 2vw, 1.2rem);
		line-height: 1.7;
		color: rgba(246, 243, 255, 0.85);
	}

	.cards {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(230px, 1fr));
		gap: 1.5rem;
	}

	.card {
		background: rgba(15, 12, 20, 0.75);
		border-radius: 20px;
		padding: 1.5rem;
		border: 1px solid rgba(255, 255, 255, 0.08);
		box-shadow: 0 20px 50px rgba(0, 0, 0, 0.45);
	}

	.card h2 {
		margin: 0 0 0.8rem;
		font-size: 1.2rem;
	}

	.card ul,
	.card ol {
		margin: 0;
		padding-left: 1.1rem;
		color: rgba(246, 243, 255, 0.8);
		line-height: 1.6;
	}

	.card p {
		margin: 0 0 0.8rem;
		color: rgba(246, 243, 255, 0.8);
	}

	.spotlight,
	.tips {
		max-width: 720px;
		padding: 1.5rem;
		border-radius: 18px;
		background: rgba(20, 14, 18, 0.7);
		border: 1px solid rgba(255, 255, 255, 0.08);
	}

	.spotlight h2,
	.tips h2 {
		margin: 0 0 0.6rem;
	}

	.spotlight p,
	.tips p {
		margin: 0;
		color: rgba(246, 243, 255, 0.8);
		line-height: 1.6;
	}
</style>
