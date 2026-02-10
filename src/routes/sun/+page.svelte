<script>
	const sections = [
		'id-overview',
		'id-structure',
		'id-energy',
		'id-weather',
		'id-quiz',
		'id-safety'
	];

	const factsBySection = {
		'id-overview': [
			{ title: 'Giant Star', text: 'A massive star made of super-hot gas, not a planet.' },
			{ title: 'Center Boss', text: 'Its gravity keeps the solar system in motion.' },
			{ title: 'Day Maker', text: 'Sunlight creates daytime and keeps Earth warm.' },
			{ title: 'Far but Fast', text: 'Light still takes minutes to reach Earth.' },
			{ title: 'Not Solid', text: 'It spins differently at the equator and poles.' }
		],
		'id-structure': [
			{ title: 'Core', text: 'Where energy is made under huge pressure.' },
			{ title: 'Radiative Zone', text: 'Energy moves slowly outward here.' },
			{ title: 'Convection Zone', text: 'Hot gas rises, cool gas sinks.' },
			{ title: 'Photosphere', text: 'The bright surface we see.' },
			{ title: 'Corona', text: 'Outer glow visible during eclipses.' }
		],
		'id-energy': [
			{ title: 'Fusion', text: 'Tiny particles join and release energy.' },
			{ title: 'Light + Heat', text: 'Energy escapes as sunlight and warmth.' },
			{ title: 'Earth Engine', text: 'Powers weather, winds, and ocean currents.' },
			{ title: 'Plant Power', text: 'Drives photosynthesis in plants.' },
			{ title: 'Energy Journey', text: 'It takes a long trip from core to surface.' }
		],
		'id-weather': [
			{ title: 'Sunspots', text: 'Cooler, darker regions with strong magnetic fields.' },
			{ title: 'Flares', text: 'Sudden bursts of energy and light.' },
			{ title: 'Solar Wind', text: 'A steady stream of particles from the Sun.' },
			{ title: 'Auroras', text: 'Storms can light up Earths polar skies.' },
			{ title: 'Active Star', text: 'The Sun changes day to day.' }
		],
		'id-quiz': [
			{ title: 'Think Deep', text: 'Use clues from the panels to answer.' },
			{ title: 'More Than MCQ', text: 'Try short answers and multi-select.' },
			{ title: 'Be Precise', text: 'Close answers still need accuracy.' },
			{ title: 'Reason It Out', text: 'Explain it in your head first.' },
			{ title: 'Challenge Mode', text: 'These are not the easy ones.' }
		],
		'id-safety': [
			{ title: 'Eye Safety', text: 'Never stare at the Sun with bare eyes.' },
			{ title: 'Safe Tools', text: 'Use proper solar glasses or projection.' },
			{ title: 'Filters Matter', text: 'Regular sunglasses are not enough.' },
			{ title: 'Camera Caution', text: 'Lenses can be damaged by sunlight.' },
			{ title: 'Be Smart', text: 'Ask an adult for safe viewing setups.' }
		]
	};

	let activeSection = 'id-overview';
	let activeFacts = factsBySection[activeSection];
	let quizAnswers = { q1: '', q2: [], q3: '', q4: '', q5: '' };
	let score = null;

	function setSection(id) {
		activeSection = id;
	}

	function submitQuiz() {
		const answerKey = {
			q1: 'fusion',
			q2: ['sunspots', 'solar flares'],
			q3: '8',
			q4: 'b',
			q5: 'false'
		};
		let tally = 0;
		if (quizAnswers.q1.trim().toLowerCase().includes(answerKey.q1)) tally += 1;
		if (
			quizAnswers.q2.length === answerKey.q2.length &&
			answerKey.q2.every((item) => quizAnswers.q2.includes(item))
		)
			tally += 1;
		if (quizAnswers.q3.trim() === answerKey.q3) tally += 1;
		if (quizAnswers.q4 === answerKey.q4) tally += 1;
		if (quizAnswers.q5 === answerKey.q5) tally += 1;
		score = `${tally} / 5`;
	}

	$: activeFacts = factsBySection[activeSection];
</script>

<main class="sun-page">
	<section class="top">
		<div class="title">
			<p class="tag">Star at the Center</p>
			<h1>The Sun</h1>
			<p class="subtitle">
				A blazing star that powers every day on Earth. Jump through the sections to explore.
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
		<div class="sun-core" aria-hidden="true">
			<div class="sun-surface"></div>
			<div class="sun-flare"></div>
			<div class="pulse"></div>
		</div>

		{#each activeFacts as fact, index (fact.title)}
			<div class={`fact orbit-${index + 1}`}>
				<h3>{fact.title}</h3>
				<p>{fact.text}</p>
			</div>
		{/each}
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
				width - the Sun would still be far wider.
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
					<p>1. Short answer: What process powers the Sun?</p>
					<input type="text" placeholder="One word" bind:value={quizAnswers.q1} />
				</div>
				<div class="question">
					<p>2. Multi-select: Which two are solar activity events?</p>
					<label>
						<input type="checkbox" value="sunspots" bind:group={quizAnswers.q2} />
						Sunspots
					</label>
					<label>
						<input type="checkbox" value="solar flares" bind:group={quizAnswers.q2} />
						Solar flares
					</label>
					<label>
						<input type="checkbox" value="rings" bind:group={quizAnswers.q2} />
						Rings
					</label>
				</div>
				<div class="question">
					<p>3. Number: About how many minutes does sunlight take to reach Earth?</p>
					<input type="text" placeholder="Just the number" bind:value={quizAnswers.q3} />
				</div>
				<div class="question">
					<p>4. Which layer is the bright surface we see?</p>
					<label><input type="radio" name="q4" value="a" bind:group={quizAnswers.q4} /> Core</label>
					<label>
						<input type="radio" name="q4" value="b" bind:group={quizAnswers.q4} />
						Photosphere
					</label>
					<label><input type="radio" name="q4" value="c" bind:group={quizAnswers.q4} /> Corona</label>
				</div>
				<div class="question">
					<p>5. True or False: The corona is cooler than the photosphere.</p>
					<label><input type="radio" name="q5" value="true" bind:group={quizAnswers.q5} /> True</label>
					<label>
						<input type="radio" name="q5" value="false" bind:group={quizAnswers.q5} />
						False
					</label>
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
		width: min(260px, 42vw);
		aspect-ratio: 1;
		border-radius: 50%;
		display: grid;
		place-items: center;
		filter: drop-shadow(0 20px 50px rgba(255, 120, 40, 0.55));
	}

	.sun-surface {
		position: absolute;
		inset: 0;
		border-radius: 50%;
		background:
			radial-gradient(circle at 30% 30%, rgba(255, 240, 200, 0.9), transparent 35%),
			radial-gradient(circle at 70% 60%, rgba(255, 120, 30, 0.75), transparent 45%),
			radial-gradient(circle at 50% 50%, #ffd36a, #ff7b2e 60%, #d94b1a 100%);
		animation: slowspin 22s linear infinite;
	}

	.sun-flare {
		position: absolute;
		inset: -8%;
		border-radius: 50%;
		background: radial-gradient(circle, rgba(255, 170, 60, 0.35), transparent 70%);
		filter: blur(6px);
		animation: pulse 4.5s ease-in-out infinite;
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

	.orbit-1 {
		top: 0;
		left: 4%;
		animation-delay: 0s;
	}

	.orbit-2 {
		top: 10%;
		right: 6%;
		animation-delay: 0.6s;
	}

	.orbit-3 {
		bottom: 10%;
		right: 4%;
		animation-delay: 1.2s;
	}

	.orbit-4 {
		bottom: 0;
		left: 10%;
		animation-delay: 1.8s;
	}

	.orbit-5 {
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

	.question input[type='text'] {
		border-radius: 10px;
		border: 1px solid rgba(255, 255, 255, 0.15);
		background: rgba(255, 255, 255, 0.06);
		color: inherit;
		padding: 0.35rem 0.6rem;
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
