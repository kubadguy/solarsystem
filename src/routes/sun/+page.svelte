<script>
	const sections = [
		'id-overview',
		'id-structure',
		'id-energy',
		'id-weather',
		'id-quiz',
		'id-safety'
	];

	let activeSection = 'id-overview';
	let quizAnswers = { q1: '', q2: '', q3: '' };
	let score = null;

	function setSection(id) {
		activeSection = id;
	}

	function submitQuiz() {
		const answerKey = { q1: 'b', q2: 'c', q3: 'a' };
		let tally = 0;
		for (const key of Object.keys(answerKey)) {
			if (quizAnswers[key] === answerKey[key]) tally += 1;
		}
		score = `${tally} / 3`;
	}
</script>

<main class="sun-page">
	<section class="top">
		<div class="title">
			<p class="tag">Star at the Center</p>
			<h1>The Sun</h1>
			<p class="subtitle">
				A blazing star that powers every day on Earth. Explore the facts by jumping through the
				sections below.
			</p>
		</div>
		<nav class="jump">
			{#each sections as id}
				<button
					type="button"
					class:active={activeSection === id}
					on:click={() => setSection(id)}
				>
					{#if id === 'id-overview'}Overview{/if}
					{#if id === 'id-structure'}Layers{/if}
					{#if id === 'id-energy'}Energy{/if}
					{#if id === 'id-weather'}Sun Weather{/if}
					{#if id === 'id-quiz'}Mini Test{/if}
					{#if id === 'id-safety'}Safety{/if}
				</button>
			{/each}
		</nav>
	</section>

	<section class="solar-layout">
		<div class="sun-core">
			<img
				src="https://upload.wikimedia.org/wikipedia/commons/4/4c/Sun_poster.svg"
				alt="Stylized view of the Sun"
			/>
			<div class="pulse"></div>
		</div>

		<div class="fact orbit-a">
			<h3>Giant Star</h3>
			<p>It is a star made of super‑hot gas, not a planet.</p>
		</div>
		<div class="fact orbit-b">
			<h3>Life Power</h3>
			<p>Its light powers plants, weather, and energy on Earth.</p>
		</div>
		<div class="fact orbit-c">
			<h3>Fast Light</h3>
			<p>Sunlight reaches Earth in a little over 8 minutes.</p>
		</div>
		<div class="fact orbit-d">
			<h3>Spinning Star</h3>
			<p>The middle spins faster than the edges.</p>
		</div>
		<div class="fact orbit-e">
			<h3>Solar Wind</h3>
			<p>A stream of particles flows out and fills space.</p>
		</div>
	</section>

	<section class="panels">
		<article class="panel" data-active={activeSection === 'id-overview'} id="id-overview">
			<h2>Overview</h2>
			<p>
				The Sun is the closest star to Earth and the center of our solar system. All the planets,
				moons, and smaller objects travel around it because of its strong gravity.
			</p>
			<p>
				It looks small in the sky, but it is enormous. Imagine lining up many Earths across its
				width — the Sun would still be far wider.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-structure'} id="id-structure">
			<h2>Layers of the Sun</h2>
			<ul>
				<li><strong>Core:</strong> the center where energy is made.</li>
				<li><strong>Radiative zone:</strong> energy moves outward slowly.</li>
				<li><strong>Convection zone:</strong> hot gas rises and cool gas sinks.</li>
				<li><strong>Photosphere:</strong> the bright surface we see.</li>
				<li><strong>Corona:</strong> a thin, hot outer glow.</li>
			</ul>
			<p>
				During a total solar eclipse, the corona can look like a shining crown around the Sun.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-energy'} id="id-energy">
			<h2>Where the Energy Comes From</h2>
			<p>
				Inside the core, tiny particles fuse together and release huge amounts of energy. That energy
				moves outward and finally escapes as light and heat.
			</p>
			<p>
				When sunlight reaches Earth, it warms the air and oceans and gives plants the energy to grow.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-weather'} id="id-weather">
			<h2>Sun Weather</h2>
			<p>
				The Sun is active. Dark spots called sunspots appear when magnetic fields twist and tangle.
			</p>
			<p>
				Sometimes the Sun releases bursts of energy called solar storms. When those reach Earth,
				they can create bright auroras near the poles.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-quiz'} id="id-quiz">
			<h2>Mini Test</h2>
			<div class="quiz">
				<div class="question">
					<p>1. The Sun is a…</p>
					<label><input type="radio" name="q1" value="a" bind:group={quizAnswers.q1} /> Planet</label>
					<label><input type="radio" name="q1" value="b" bind:group={quizAnswers.q1} /> Star</label>
					<label><input type="radio" name="q1" value="c" bind:group={quizAnswers.q1} /> Comet</label>
				</div>
				<div class="question">
					<p>2. Sunlight reaches Earth in about…</p>
					<label><input type="radio" name="q2" value="a" bind:group={quizAnswers.q2} /> 8 seconds</label>
					<label><input type="radio" name="q2" value="b" bind:group={quizAnswers.q2} /> 8 hours</label>
					<label><input type="radio" name="q2" value="c" bind:group={quizAnswers.q2} /> 8 minutes</label>
				</div>
				<div class="question">
					<p>3. Sunspots are…</p>
					<label><input type="radio" name="q3" value="a" bind:group={quizAnswers.q3} /> Cooler areas</label>
					<label><input type="radio" name="q3" value="b" bind:group={quizAnswers.q3} /> Oceans</label>
					<label><input type="radio" name="q3" value="c" bind:group={quizAnswers.q3} /> Rings</label>
				</div>
				<button class="submit" type="button" on:click={submitQuiz}>Check score</button>
				{#if score}
					<p class="score">Score: {score}</p>
				{/if}
			</div>
		</article>

		<article class="panel" data-active={activeSection === 'id-safety'} id="id-safety">
			<h2>Safety First</h2>
			<p>
				Never look directly at the Sun with your eyes. It can damage your vision. Use safe solar
				glasses or view it with a proper projection method.
			</p>
		</article>
	</section>
</main>

<style>
	:global(body) {
		margin: 0;
		font-family: "Space Grotesk", system-ui, sans-serif;
		color: #f6f3ff;
		background:
			radial-gradient(circle at 20% 10%, rgba(255, 190, 80, 0.4), transparent 45%),
			radial-gradient(circle at 85% 25%, rgba(255, 90, 30, 0.35), transparent 45%),
			radial-gradient(circle at 40% 90%, rgba(255, 120, 40, 0.3), transparent 45%),
			linear-gradient(160deg, #06060b 15%, #150a08 55%, #0b0814 100%);
		min-height: 100svh;
	}

	.sun-page {
		min-height: 100svh;
		padding: clamp(1.5rem, 4vw, 3rem);
		display: grid;
		gap: clamp(1.2rem, 2.4vw, 2.2rem);
	}

	.top {
		display: grid;
		grid-template-columns: minmax(0, 1fr) minmax(0, 320px);
		gap: 1.5rem;
		align-items: center;
	}

	.title h1 {
		margin: 0 0 0.6rem;
		font-family: "Unbounded", "Space Grotesk", system-ui, sans-serif;
		font-size: clamp(2.4rem, 4.5vw, 3.8rem);
	}

	.tag {
		margin: 0 0 0.6rem;
		letter-spacing: 0.28em;
		text-transform: uppercase;
		font-size: 0.8rem;
		color: rgba(255, 220, 170, 0.8);
	}

	.subtitle {
		margin: 0;
		color: rgba(246, 243, 255, 0.8);
		line-height: 1.5;
	}

	.jump {
		display: grid;
		gap: 0.5rem;
	}

	.jump button {
		border: 1px solid rgba(255, 255, 255, 0.12);
		background: rgba(255, 255, 255, 0.05);
		color: inherit;
		padding: 0.55rem 0.9rem;
		border-radius: 999px;
		font-size: 0.85rem;
		cursor: pointer;
		transition: transform 0.2s ease, box-shadow 0.2s ease;
	}

	.jump button.active {
		background: linear-gradient(120deg, #ffb347, #ff5f2e);
		color: #1b0c08;
		border-color: transparent;
		box-shadow: 0 15px 30px rgba(255, 95, 46, 0.35);
		transform: translateY(-1px);
	}

	.solar-layout {
		position: relative;
		min-height: 320px;
		display: grid;
		place-items: center;
	}

	.sun-core {
		position: relative;
		width: min(260px, 40vw);
		aspect-ratio: 1;
		border-radius: 50%;
		display: grid;
		place-items: center;
		filter: drop-shadow(0 20px 50px rgba(255, 120, 40, 0.55));
	}

	.sun-core img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		border-radius: 50%;
		animation: slowspin 18s linear infinite;
	}

	.pulse {
		position: absolute;
		inset: -12%;
		border-radius: 50%;
		background: radial-gradient(circle, rgba(255, 200, 90, 0.35), transparent 70%);
		animation: pulse 3.5s ease-in-out infinite;
	}

	.fact {
		position: absolute;
		width: min(220px, 40vw);
		background: rgba(20, 14, 18, 0.78);
		border: 1px solid rgba(255, 255, 255, 0.1);
		border-radius: 16px;
		padding: 0.8rem 1rem;
		box-shadow: 0 20px 40px rgba(0, 0, 0, 0.45);
		animation: float 4s ease-in-out infinite;
	}

	.fact h3 {
		margin: 0 0 0.3rem;
		font-size: 1rem;
	}

	.fact p {
		margin: 0;
		font-size: 0.9rem;
		color: rgba(246, 243, 255, 0.8);
	}

	.orbit-a {
		top: 0;
		left: 4%;
		animation-delay: 0s;
	}

	.orbit-b {
		top: 10%;
		right: 6%;
		animation-delay: 0.6s;
	}

	.orbit-c {
		bottom: 10%;
		right: 4%;
		animation-delay: 1.2s;
	}

	.orbit-d {
		bottom: 0;
		left: 10%;
		animation-delay: 1.8s;
	}

	.orbit-e {
		top: 42%;
		left: -2%;
		animation-delay: 2.4s;
	}

	.panels {
		display: grid;
		grid-template-columns: minmax(0, 1fr);
	}

	.panel {
		display: none;
		background: rgba(15, 12, 20, 0.8);
		border-radius: 18px;
		padding: 1.3rem 1.6rem;
		border: 1px solid rgba(255, 255, 255, 0.1);
		box-shadow: 0 25px 50px rgba(0, 0, 0, 0.45);
		animation: fadeIn 0.35s ease;
	}

	.panel[data-active='true'] {
		display: block;
	}

	.panel h2 {
		margin: 0 0 0.6rem;
	}

	.panel p,
	.panel li {
		color: rgba(246, 243, 255, 0.8);
		line-height: 1.6;
	}

	.panel ul {
		margin: 0 0 0.6rem;
		padding-left: 1.1rem;
	}

	.quiz {
		display: grid;
		gap: 0.8rem;
	}

	.question {
		display: grid;
		gap: 0.35rem;
		font-size: 0.95rem;
	}

	.question label {
		display: flex;
		align-items: center;
		gap: 0.4rem;
	}

	.submit {
		border: none;
		background: linear-gradient(120deg, #ffb347, #ff5f2e);
		color: #1b0c08;
		padding: 0.6rem 1.2rem;
		border-radius: 999px;
		font-weight: 600;
		cursor: pointer;
		width: fit-content;
	}

	.score {
		margin: 0;
		font-weight: 600;
		color: rgba(255, 220, 170, 0.9);
	}

	@keyframes slowspin {
		from {
			transform: rotate(0deg);
		}
		to {
			transform: rotate(360deg);
		}
	}

	@keyframes pulse {
		0%,
		100% {
			transform: scale(1);
			opacity: 0.6;
		}
		50% {
			transform: scale(1.08);
			opacity: 0.9;
		}
	}

	@keyframes float {
		0%,
		100% {
			transform: translateY(0);
		}
		50% {
			transform: translateY(-8px);
		}
	}

	@keyframes fadeIn {
		from {
			opacity: 0;
			transform: translateY(6px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}

	@media (max-width: 900px) {
		.top {
			grid-template-columns: 1fr;
		}

		.jump {
			grid-template-columns: repeat(3, minmax(0, 1fr));
		}

		.fact {
			display: none;
		}

		.solar-layout {
			min-height: 240px;
		}
	}
</style>
