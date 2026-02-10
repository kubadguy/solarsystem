<script>
	const sections = [
		'id-overview',
		'id-location',
		'id-objects',
		'id-orbits',
		'id-importance',
		'id-quiz'
	];

	const factsBySection = {
		'id-overview': [
			{ title: 'Icy Zone', text: 'A cold region filled with icy objects and dwarf planets.' },
			{ title: 'Outer Belt', text: 'It lies beyond Neptune, far from the Sun.' },
			{ title: 'Leftovers', text: 'Material left from early solar system days.' },
			{ title: 'Huge Space', text: 'Objects are far apart, not crowded.' },
			{ title: 'Many Worlds', text: 'There are thousands of known objects.' }
		],
		'id-location': [
			{ title: 'Beyond Neptune', text: 'Starts just past Neptune and stretches outward.' },
			{ title: 'Dark and Cold', text: 'Very little sunlight reaches this region.' },
			{ title: 'Wide Band', text: 'It is a broad, thick region, not a thin ring.' },
			{ title: 'Slow Orbits', text: 'Objects take a long time to go around the Sun.' },
			{ title: 'Far Frontier', text: 'A boundary zone of the planetary system.' }
		],
		'id-objects': [
			{ title: 'Dwarf Planets', text: 'Pluto, Eris, Haumea, Makemake and more.' },
			{ title: 'Comet Seeds', text: 'Many short-period comets come from here.' },
			{ title: 'Rock + Ice', text: 'Mix of frozen gases, ice, and rock.' },
			{ title: 'Different Sizes', text: 'From tiny chunks to large worlds.' },
			{ title: 'Odd Shapes', text: 'Some are round, some are lumpy.' }
		],
		'id-orbits': [
			{ title: 'Ellipses', text: 'Many have oval, tilted orbits.' },
			{ title: 'Resonance', text: 'Some orbit in patterns linked to Neptune.' },
			{ title: 'Slow Years', text: 'Orbits can take hundreds of Earth years.' },
			{ title: 'Scattered', text: 'Some are pushed into distant paths.' },
			{ title: 'Long Journeys', text: 'They move slowly across the sky.' }
		],
		'id-importance': [
			{ title: 'Solar History', text: 'Shows how the planets formed.' },
			{ title: 'Comet Clues', text: 'Explains where many comets begin.' },
			{ title: 'New Worlds', text: 'We keep discovering new objects.' },
			{ title: 'Exploration', text: 'Missions like New Horizons visited Pluto.' },
			{ title: 'Big Frontier', text: 'A huge region still mostly unexplored.' }
		],
		'id-quiz': [
			{ title: 'Think Deep', text: 'Use clues from the panels to answer.' },
			{ title: 'More Than MCQ', text: 'Short answers and multi-select.' },
			{ title: 'Be Precise', text: 'Close answers still need accuracy.' },
			{ title: 'Reason It Out', text: 'Explain it in your head first.' },
			{ title: 'Challenge Mode', text: 'These are not the easy ones.' }
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
			q1: 'neptune',
			q2: ['icy', 'far'],
			q3: 'pluto',
			q4: 'b',
			q5: 'true'
		};
		let tally = 0;
		if (quizAnswers.q1.trim().toLowerCase().includes(answerKey.q1)) tally += 1;
		if (
			quizAnswers.q2.length === answerKey.q2.length &&
			answerKey.q2.every((item) => quizAnswers.q2.includes(item))
		)
			tally += 1;
		if (quizAnswers.q3.trim().toLowerCase().includes(answerKey.q3)) tally += 1;
		if (quizAnswers.q4 === answerKey.q4) tally += 1;
		if (quizAnswers.q5 === answerKey.q5) tally += 1;
		score = `${tally} / 5`;
	}

	$: activeFacts = factsBySection[activeSection];
</script>

<main class="kuiper-page">
	<section class="top">
		<div class="title">
			<p class="tag">Frozen Frontier</p>
			<h1>Kuiper Belt Objects</h1>
			<p class="subtitle">
				A distant, icy region beyond Neptune filled with small worlds. Jump through the sections to
				explore.
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
					{#if id === 'id-location'}Location{/if}
					{#if id === 'id-objects'}Objects{/if}
					{#if id === 'id-orbits'}Orbits{/if}
					{#if id === 'id-importance'}Why It Matters{/if}
					{#if id === 'id-quiz'}Mini Test{/if}
				</button>
			{/each}
		</nav>
	</section>

	<section class="kuiper-layout">
		<div class="kuiper-core" aria-hidden="true">
			<div class="kuiper-ring"></div>
			<div class="kuiper-glow"></div>
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
				The Kuiper Belt is a wide region beyond Neptune filled with icy objects. It is a leftover
				storehouse from the early solar system.
			</p>
			<p>
				Objects here are very far apart, so the belt is mostly empty space.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-location'} id="id-location">
			<h2>Location</h2>
			<p>
				The belt begins just past Neptune and stretches far outward. Sunlight is weak and the region
				is extremely cold.
			</p>
			<p>
				Because it is so far, objects move slowly and take long years to orbit the Sun.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-objects'} id="id-objects">
			<h2>Objects</h2>
			<p>
				Many dwarf planets live here, including Pluto, Eris, Makemake, and Haumea. There are also
				thousands of smaller icy bodies.
			</p>
			<p>
				Some of these objects can become comets that visit the inner solar system.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-orbits'} id="id-orbits">
			<h2>Orbits</h2>
			<p>
				Kuiper Belt objects travel in oval, tilted paths. Some are in orbital patterns linked to
				Neptune, while others are scattered into distant orbits.
			</p>
			<p>
				Many take hundreds of Earth years to complete one orbit.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-importance'} id="id-importance">
			<h2>Why It Matters</h2>
			<p>
				The Kuiper Belt preserves clues about how planets formed. By studying these objects,
				scientists learn how the early solar system looked and evolved.
			</p>
			<p>
				New missions and discoveries keep revealing surprising new worlds.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-quiz'} id="id-quiz">
			<h2>Mini Test</h2>
			<div class="quiz">
				<div class="question">
					<p>1. Short answer: The Kuiper Belt lies beyond which planet?</p>
					<input type="text" placeholder="One word" bind:value={quizAnswers.q1} />
				</div>
				<div class="question">
					<p>2. Multi-select: Which two describe the Kuiper Belt?</p>
					<label>
						<input type="checkbox" value="icy" bind:group={quizAnswers.q2} />
						Icy
					</label>
					<label>
						<input type="checkbox" value="far" bind:group={quizAnswers.q2} />
						Far from the Sun
					</label>
					<label>
						<input type="checkbox" value="hot" bind:group={quizAnswers.q2} />
						Very hot
					</label>
				</div>
				<div class="question">
					<p>3. Short answer: Name one dwarf planet in the Kuiper Belt.</p>
					<input type="text" placeholder="One name" bind:value={quizAnswers.q3} />
				</div>
				<div class="question">
					<p>4. Which statement is most accurate?</p>
					<label>
						<input type="radio" name="q4" value="a" bind:group={quizAnswers.q4} />
						The Kuiper Belt is a tight ring of rocks
					</label>
					<label>
						<input type="radio" name="q4" value="b" bind:group={quizAnswers.q4} />
						Objects are spread far apart with lots of empty space
					</label>
					<label>
						<input type="radio" name="q4" value="c" bind:group={quizAnswers.q4} />
						The Kuiper Belt is inside Mars
					</label>
				</div>
				<div class="question">
					<p>5. True or False: Some short-period comets come from the Kuiper Belt.</p>
					<label><input type="radio" name="q5" value="true" bind:group={quizAnswers.q5} /> True</label>
					<label><input type="radio" name="q5" value="false" bind:group={quizAnswers.q5} /> False</label>
				</div>
				<button class="submit" type="button" on:click={submitQuiz}>Check score</button>
				{#if score}
					<p class="score">Score: {score}</p>
				{/if}
			</div>
		</article>
	</section>
</main>

<style>
	:global(body) {
		margin: 0;
		font-family: "Space Grotesk", system-ui, sans-serif;
		color: #f5f6ff;
		background:
			radial-gradient(circle at 15% 15%, rgba(120, 210, 255, 0.3), transparent 45%),
			radial-gradient(circle at 85% 25%, rgba(80, 140, 255, 0.25), transparent 45%),
			radial-gradient(circle at 40% 90%, rgba(90, 180, 220, 0.25), transparent 45%),
			linear-gradient(160deg, #071018 15%, #0a1622 55%, #0a0f1a 100%);
		min-height: 100svh;
	}

	.kuiper-page {
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
		color: rgba(170, 220, 255, 0.8);
	}

	.subtitle {
		margin: 0;
		color: rgba(246, 247, 255, 0.8);
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
		background: linear-gradient(120deg, #7ad7ff, #6a9dff);
		color: #04121c;
		border-color: transparent;
		box-shadow: 0 15px 30px rgba(122, 215, 255, 0.35);
		transform: translateY(-1px);
	}

	.kuiper-layout {
		position: relative;
		min-height: 320px;
		display: grid;
		place-items: center;
	}

	.kuiper-core {
		position: relative;
		width: min(260px, 42vw);
		aspect-ratio: 1;
		border-radius: 50%;
		display: grid;
		place-items: center;
		filter: drop-shadow(0 20px 50px rgba(90, 170, 255, 0.45));
	}

	.kuiper-ring {
		position: absolute;
		inset: 12%;
		border-radius: 50%;
		border: 3px dashed rgba(200, 235, 255, 0.45);
		box-shadow: inset 0 0 20px rgba(90, 170, 255, 0.35);
		animation: slowspin 18s linear infinite;
	}

	.kuiper-glow {
		position: absolute;
		inset: -10%;
		border-radius: 50%;
		background: radial-gradient(circle, rgba(90, 170, 255, 0.25), transparent 70%);
		filter: blur(6px);
		animation: pulse 4s ease-in-out infinite;
	}

	.fact {
		position: absolute;
		width: min(220px, 40vw);
		background: rgba(12, 18, 26, 0.78);
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
		color: rgba(246, 247, 255, 0.8);
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
		background: rgba(12, 18, 26, 0.8);
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
		background: linear-gradient(120deg, #7ad7ff, #6a9dff);
		color: #04121c;
		padding: 0.6rem 1.2rem;
		border-radius: 999px;
		font-weight: 600;
		cursor: pointer;
		width: fit-content;
	}

	.score {
		margin: 0;
		font-weight: 600;
		color: rgba(190, 220, 255, 0.9);
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

		.kuiper-layout {
			min-height: 240px;
		}
	}
</style>
