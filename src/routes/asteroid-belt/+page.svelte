<script>
	const sections = [
		'id-overview',
		'id-location',
		'id-composition',
		'id-orbits',
		'id-missions',
		'id-quiz'
	];

	const factsBySection = {
		'id-overview': [
			{ title: 'Rocky Zone', text: 'A wide region filled with many small rocky bodies.' },
			{ title: 'Not a Ring', text: 'Asteroids are far apart, not packed together.' },
			{ title: 'Leftovers', text: 'Material that never became a planet.' },
			{ title: 'Mostly Small', text: 'Most are tiny, some are the size of mountains.' },
			{ title: 'Big Ones', text: 'Ceres, Vesta, Pallas are among the largest.' }
		],
		'id-location': [
			{ title: 'Between Planets', text: 'It sits between Mars and Jupiter.' },
			{ title: 'Huge Space', text: 'The belt stretches across a wide region.' },
			{ title: 'Safe Travel', text: 'Spacecraft can pass through safely.' },
			{ title: 'Gravitational Pull', text: 'Jupiter helped shape the belt.' },
			{ title: 'Two Neighborhoods', text: 'Inner and outer parts have different types.' }
		],
		'id-composition': [
			{ title: 'Rock and Metal', text: 'Many asteroids are rocky or metallic.' },
			{ title: 'Some Icy', text: 'Farther out, there can be more ice.' },
			{ title: 'Dust', text: 'Tiny particles fill the space too.' },
			{ title: 'Color Clues', text: 'Different colors show different materials.' },
			{ title: 'Fragments', text: 'Collisions break asteroids into pieces.' }
		],
		'id-orbits': [
			{ title: 'Ellipses', text: 'Asteroids orbit the Sun in oval paths.' },
			{ title: 'Different Speeds', text: 'Closer ones move faster than farther ones.' },
			{ title: 'Gaps', text: 'Some areas are emptier because of gravity.' },
			{ title: 'Families', text: 'Groups share similar orbits from old collisions.' },
			{ title: 'Near Earth', text: 'A few cross paths near Earth.' }
		],
		'id-missions': [
			{ title: 'Dawn', text: 'Visited Vesta and Ceres to study them up close.' },
			{ title: 'Pictures', text: 'Spacecraft images show craters and ridges.' },
			{ title: 'Samples', text: 'Meteorites on Earth are asteroid pieces.' },
			{ title: 'Mapping', text: 'Scientists map sizes, shapes, and paths.' },
			{ title: 'Learning', text: 'Asteroids tell the story of early planets.' }
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
			q1: 'mars and jupiter',
			q2: ['leftovers', 'collisions'],
			q3: 'ceres',
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

<main class="belt-page">
	<section class="top">
		<div class="title">
			<p class="tag">Rocky Highway</p>
			<h1>Asteroid Belt</h1>
			<p class="subtitle">
				A wide zone of rocky leftovers between the inner and outer planets. Jump through the
				sections to explore.
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
					{#if id === 'id-composition'}Composition{/if}
					{#if id === 'id-orbits'}Orbits{/if}
					{#if id === 'id-missions'}Missions{/if}
					{#if id === 'id-quiz'}Mini Test{/if}
				</button>
			{/each}
		</nav>
	</section>

	<section class="belt-layout">
		<div class="belt-core" aria-hidden="true">
			<div class="belt-ring"></div>
			<div class="belt-glow"></div>
		</div>

		{#each activeFacts as fact, index (index)}
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
				The asteroid belt is a huge region of space filled with rocky objects called asteroids.
				It is not a solid ring. The rocks are far apart and there is lots of empty space.
			</p>
			<p>
				These objects are leftovers from the early solar system that never formed into a planet.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-location'} id="id-location">
			<h2>Location</h2>
			<p>
				The belt sits between Mars and Jupiter. Jupiter is so massive that its gravity kept
				the material here from clumping into one planet.
			</p>
			<p>
				Even though it looks like a thick band in pictures, spacecraft can fly through it safely.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-composition'} id="id-composition">
			<h2>Composition</h2>
			<p>
				Many asteroids are made of rock and metal. Some in the outer parts contain more ice.
			</p>
			<p>
				Collisions break asteroids into smaller pieces, creating families with similar materials.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-orbits'} id="id-orbits">
			<h2>Orbits and Motion</h2>
			<p>
				Asteroids orbit the Sun in oval paths. Those closer to the Sun move faster, while farther
				ones move more slowly.
			</p>
			<p>
				Some paths line up into groups called families, often created by old collisions.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-missions'} id="id-missions">
			<h2>Missions and Discoveries</h2>
			<p>
				The Dawn spacecraft visited two large objects in the belt: Vesta and the dwarf planet Ceres.
			</p>
			<p>
				Meteorites found on Earth are often broken pieces of asteroids, giving scientists real samples.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-quiz'} id="id-quiz">
			<h2>Mini Test</h2>
			<div class="quiz">
				<div class="question">
					<p>1. Short answer: The asteroid belt lies between which two planets?</p>
					<input type="text" placeholder="Answer in words" bind:value={quizAnswers.q1} />
				</div>
				<div class="question">
					<p>2. Multi-select: Why are there many small asteroids instead of one planet?</p>
					<label>
						<input type="checkbox" value="leftovers" bind:group={quizAnswers.q2} />
						Leftover material from early formation
					</label>
					<label>
						<input type="checkbox" value="collisions" bind:group={quizAnswers.q2} />
						Collisions broke objects apart
					</label>
					<label>
						<input type="checkbox" value="oceans" bind:group={quizAnswers.q2} />
						Oceans pulled them apart
					</label>
				</div>
				<div class="question">
					<p>3. Short answer: Name the dwarf planet in the asteroid belt.</p>
					<input type="text" placeholder="One word" bind:value={quizAnswers.q3} />
				</div>
				<div class="question">
					<p>4. Which statement is most accurate?</p>
					<label>
						<input type="radio" name="q4" value="a" bind:group={quizAnswers.q4} />
						The belt is a solid ring of rocks
					</label>
					<label>
						<input type="radio" name="q4" value="b" bind:group={quizAnswers.q4} />
						The belt has lots of empty space between rocks
					</label>
					<label>
						<input type="radio" name="q4" value="c" bind:group={quizAnswers.q4} />
						The belt is a single giant planet
					</label>
				</div>
				<div class="question">
					<p>5. True or False: Some asteroid pieces land on Earth as meteorites.</p>
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
		color: #f5f3ff;
		background:
			radial-gradient(circle at 20% 10%, rgba(110, 180, 255, 0.3), transparent 45%),
			radial-gradient(circle at 80% 20%, rgba(160, 120, 255, 0.25), transparent 45%),
			radial-gradient(circle at 40% 90%, rgba(80, 120, 200, 0.25), transparent 45%),
			linear-gradient(160deg, #080913 15%, #0d1020 55%, #0a0b15 100%);
		min-height: 100svh;
	}

	.belt-page {
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
		color: rgba(190, 210, 255, 0.8);
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
		background: linear-gradient(120deg, #7ab2ff, #b48dff);
		color: #0b0c18;
		border-color: transparent;
		box-shadow: 0 15px 30px rgba(122, 178, 255, 0.35);
		transform: translateY(-1px);
	}

	.belt-layout {
		position: relative;
		min-height: 320px;
		display: grid;
		place-items: center;
	}

	.belt-core {
		position: relative;
		width: min(260px, 42vw);
		aspect-ratio: 1;
		border-radius: 50%;
		display: grid;
		place-items: center;
		filter: drop-shadow(0 20px 50px rgba(120, 160, 255, 0.45));
	}

	.belt-ring {
		position: absolute;
		inset: 12%;
		border-radius: 50%;
		border: 3px dashed rgba(220, 230, 255, 0.4);
		box-shadow: inset 0 0 20px rgba(120, 160, 255, 0.35);
		animation: slowspin 18s linear infinite;
	}

	.belt-glow {
		position: absolute;
		inset: -10%;
		border-radius: 50%;
		background: radial-gradient(circle, rgba(120, 160, 255, 0.25), transparent 70%);
		filter: blur(6px);
		animation: pulse 4s ease-in-out infinite;
	}

	.fact {
		position: absolute;
		width: min(220px, 40vw);
		background: rgba(15, 18, 28, 0.78);
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
		background: rgba(15, 18, 28, 0.8);
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

	.panel p {
		color: rgba(246, 243, 255, 0.8);
		line-height: 1.6;
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
		background: linear-gradient(120deg, #7ab2ff, #b48dff);
		color: #0b0c18;
		padding: 0.6rem 1.2rem;
		border-radius: 999px;
		font-weight: 600;
		cursor: pointer;
		width: fit-content;
	}

	.score {
		margin: 0;
		font-weight: 600;
		color: rgba(200, 220, 255, 0.9);
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

		.belt-layout {
			min-height: 240px;
		}
	}
</style>
