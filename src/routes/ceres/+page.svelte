<script>
	const sections = [
		'id-overview',
		'id-location',
		'id-surface',
		'id-water',
		'id-mission',
		'id-quiz'
	];

	const factsBySection = {
		'id-overview': [
			{ title: 'Dwarf Planet', text: 'Ceres is the only dwarf planet in the asteroid belt.' },
			{ title: 'Largest Asteroid', text: 'It is the biggest object in the belt.' },
			{ title: 'Round World', text: 'It is large enough to be nearly spherical.' },
			{ title: 'Rock + Ice', text: 'A mix of rocky material and ice.' },
			{ title: 'Mini Planet', text: 'Acts like a small planet among asteroids.' }
		],
		'id-location': [
			{ title: 'Asteroid Belt', text: 'Ceres orbits between Mars and Jupiter.' },
			{ title: 'Wide Path', text: 'Its orbit is inside the main belt region.' },
			{ title: 'Fastest Here', text: 'It moves faster than outer belt objects.' },
			{ title: 'Not Near Earth', text: 'It stays far from Earths orbit.' },
			{ title: 'Stable Orbit', text: 'Its path is steady and long-term.' }
		],
		'id-surface': [
			{ title: 'Bright Spots', text: 'Some craters have bright, salty deposits.' },
			{ title: 'Craters', text: 'Impacts left many round craters.' },
			{ title: 'Dark Plains', text: 'Some areas are darker, with older rock.' },
			{ title: 'Mountains', text: 'Ceres has a tall mountain called Ahuna Mons.' },
			{ title: 'Patches of Ice', text: 'Ice can be found in shadowed places.' }
		],
		'id-water': [
			{ title: 'Hidden Water', text: 'There may be water ice under the surface.' },
			{ title: 'Ice + Salt', text: 'Salty deposits suggest liquid once moved.' },
			{ title: 'Possible Brine', text: 'Some areas show signs of salty water.' },
			{ title: 'Cold Storage', text: 'Ice can last a long time in deep craters.' },
			{ title: 'Science Clues', text: 'Water hints at activity long ago.' }
		],
		'id-mission': [
			{ title: 'Dawn Mission', text: 'NASA Dawn studied Ceres up close.' },
			{ title: 'Mapped Surface', text: 'Detailed maps showed craters and spots.' },
			{ title: 'Gravity Data', text: 'Helped reveal its interior structure.' },
			{ title: 'Geology', text: 'Showed Ceres has a complex history.' },
			{ title: 'Big Discovery', text: 'Bright spots were a major surprise.' }
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
			q1: 'dwarf',
			q2: ['asteroid belt', 'mars and jupiter'],
			q3: 'dawn',
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

<main class="ceres-page">
	<section class="top">
		<div class="title">
			<p class="tag">Belt Giant</p>
			<h1>Ceres</h1>
			<p class="subtitle">
				The largest object in the asteroid belt and a dwarf planet with icy secrets. Jump through the
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
					{#if id === 'id-surface'}Surface{/if}
					{#if id === 'id-water'}Water{/if}
					{#if id === 'id-mission'}Mission{/if}
					{#if id === 'id-quiz'}Mini Test{/if}
				</button>
			{/each}
		</nav>
	</section>

	<section class="ceres-layout">
		<div class="ceres-core" aria-hidden="true">
			<div class="ceres-sphere"></div>
			<div class="ceres-halo"></div>
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
				Ceres is the only dwarf planet in the asteroid belt. It is the largest object there and is
				round like a small planet.
			</p>
			<p>
				It is made of rock and ice, with features that hint at a complex history.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-location'} id="id-location">
			<h2>Location</h2>
			<p>
				Ceres orbits between Mars and Jupiter, right inside the main asteroid belt. It has a stable
				path around the Sun.
			</p>
			<p>
				It never comes close to Earth and stays in the belt region.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-surface'} id="id-surface">
			<h2>Surface</h2>
			<p>
				Ceres has many craters, bright spots, and a tall mountain called Ahuna Mons. Some of the
				bright areas are made of salty deposits.
			</p>
			<p>
				Dark plains and lighter regions show that its surface has changed over time.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-water'} id="id-water">
			<h2>Water and Ice</h2>
			<p>
				Scientists think there is water ice under the surface. Bright salty spots hint that liquid
				water or brine once moved upward.
			</p>
			<p>
				Ice can also survive in shadowed craters that never see sunlight.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-mission'} id="id-mission">
			<h2>Dawn Mission</h2>
			<p>
				NASA Dawn spacecraft studied Ceres in detail, mapping its surface and measuring its gravity.
			</p>
			<p>
				The mission revealed unexpected bright spots and signs of past activity.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-quiz'} id="id-quiz">
			<h2>Mini Test</h2>
			<div class="quiz">
				<div class="question">
					<p>1. Short answer: Ceres is a ______ planet.</p>
					<input type="text" placeholder="One word" bind:value={quizAnswers.q1} />
				</div>
				<div class="question">
					<p>2. Multi-select: Which two describe where Ceres is found?</p>
					<label>
						<input type="checkbox" value="asteroid belt" bind:group={quizAnswers.q2} />
						In the asteroid belt
					</label>
					<label>
						<input type="checkbox" value="mars and jupiter" bind:group={quizAnswers.q2} />
						Between Mars and Jupiter
					</label>
					<label>
						<input type="checkbox" value="inside mercury" bind:group={quizAnswers.q2} />
						Inside Mercury orbit
					</label>
				</div>
				<div class="question">
					<p>3. Short answer: Which mission studied Ceres up close?</p>
					<input type="text" placeholder="One word" bind:value={quizAnswers.q3} />
				</div>
				<div class="question">
					<p>4. Which statement is most accurate?</p>
					<label>
						<input type="radio" name="q4" value="a" bind:group={quizAnswers.q4} />
						Ceres is a gas giant
					</label>
					<label>
						<input type="radio" name="q4" value="b" bind:group={quizAnswers.q4} />
						Ceres is a dwarf planet in the asteroid belt
					</label>
					<label>
						<input type="radio" name="q4" value="c" bind:group={quizAnswers.q4} />
						Ceres is a comet
					</label>
				</div>
				<div class="question">
					<p>5. True or False: Bright spots on Ceres suggest salty material.</p>
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
		color: #f6f4ff;
		background:
			radial-gradient(circle at 20% 12%, rgba(255, 190, 140, 0.28), transparent 45%),
			radial-gradient(circle at 80% 18%, rgba(255, 160, 120, 0.25), transparent 45%),
			radial-gradient(circle at 45% 90%, rgba(200, 150, 120, 0.22), transparent 45%),
			linear-gradient(160deg, #100b08 15%, #151015 55%, #0e0b10 100%);
		min-height: 100svh;
	}

	.ceres-page {
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
		color: rgba(255, 210, 170, 0.8);
	}

	.subtitle {
		margin: 0;
		color: rgba(246, 244, 255, 0.8);
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
		background: linear-gradient(120deg, #ffb47a, #ff8d6a);
		color: #1a0f0a;
		border-color: transparent;
		box-shadow: 0 15px 30px rgba(255, 160, 120, 0.35);
		transform: translateY(-1px);
	}

	.ceres-layout {
		position: relative;
		min-height: 320px;
		display: grid;
		place-items: center;
	}

	.ceres-core {
		position: relative;
		width: min(240px, 40vw);
		aspect-ratio: 1;
		border-radius: 50%;
		display: grid;
		place-items: center;
		filter: drop-shadow(0 20px 50px rgba(255, 160, 120, 0.35));
	}

	.ceres-sphere {
		position: absolute;
		inset: 0;
		border-radius: 50%;
		background:
			radial-gradient(circle at 30% 30%, rgba(255, 235, 220, 0.9), transparent 40%),
			radial-gradient(circle at 70% 60%, rgba(255, 170, 120, 0.6), transparent 50%),
			radial-gradient(circle at 50% 50%, #f2c9a8, #d99062 60%, #9c5a3a 100%);
		animation: slowspin 22s linear infinite;
	}

	.ceres-halo {
		position: absolute;
		inset: -8%;
		border-radius: 50%;
		background: radial-gradient(circle, rgba(255, 170, 120, 0.3), transparent 70%);
		filter: blur(6px);
		animation: pulse 4s ease-in-out infinite;
	}

	.fact {
		position: absolute;
		width: min(220px, 40vw);
		background: rgba(20, 16, 14, 0.78);
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
		color: rgba(246, 244, 255, 0.8);
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
		background: rgba(20, 16, 14, 0.8);
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
		color: rgba(246, 244, 255, 0.8);
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
		background: linear-gradient(120deg, #ffb47a, #ff8d6a);
		color: #1a0f0a;
		padding: 0.6rem 1.2rem;
		border-radius: 999px;
		font-weight: 600;
		cursor: pointer;
		width: fit-content;
	}

	.score {
		margin: 0;
		font-weight: 600;
		color: rgba(255, 220, 200, 0.9);
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

		.ceres-layout {
			min-height: 240px;
		}
	}
</style>
