<script>
	const sections = [
		'id-overview',
		'id-size',
		'id-orbit',
		'id-surface',
		'id-discovery',
		'id-quiz'
	];

	const factsBySection = {
		'id-overview': [
			{ title: 'Dwarf Planet', text: 'Eris is a dwarf planet in the outer solar system.' },
			{ title: 'Very Distant', text: 'It travels far beyond Neptune.' },
			{ title: 'Icy World', text: 'Its surface is cold and frozen.' },
			{ title: 'Pluto Rival', text: 'Its discovery changed how we define planets.' },
			{ title: 'Slow Year', text: 'One orbit takes many centuries.' }
		],
		'id-size': [
			{ title: 'Big for a Dwarf', text: 'Eris is similar in size to Pluto.' },
			{ title: 'Heavy', text: 'It is one of the most massive dwarf planets.' },
			{ title: 'Small Moon', text: 'Eris has a moon called Dysnomia.' },
			{ title: 'Round Shape', text: 'Gravity makes it nearly spherical.' },
			{ title: 'Tiny in the Sky', text: 'It appears as a faint dot in telescopes.' }
		],
		'id-orbit': [
			{ title: 'Very Oval', text: 'Its orbit is highly elliptical.' },
			{ title: 'Tilted Path', text: 'It is tilted compared to the planets.' },
			{ title: 'Long Trip', text: 'It takes over 500 years to orbit the Sun.' },
			{ title: 'Far Stretch', text: 'It goes far beyond Pluto at its farthest.' },
			{ title: 'Slow Motion', text: 'It moves very slowly across the sky.' }
		],
		'id-surface': [
			{ title: 'Frozen Gases', text: 'Surface ice includes frozen methane.' },
			{ title: 'Bright', text: 'It reflects a lot of sunlight.' },
			{ title: 'Deep Cold', text: 'Temperatures are extremely low.' },
			{ title: 'Thin Air', text: 'Any atmosphere is very weak and frozen.' },
			{ title: 'Season Changes', text: 'Changes happen over long periods.' }
		],
		'id-discovery': [
			{ title: 'Found in 2005', text: 'Discovered by a team led by Mike Brown.' },
			{ title: 'Planet Debate', text: 'Helped create the dwarf planet category.' },
			{ title: 'Named Eris', text: 'Named after the Greek goddess of discord.' },
			{ title: 'New Horizons Era', text: 'Discovery pushed new interest in outer worlds.' },
			{ title: 'Still Mysterious', text: 'We have not visited it yet.' }
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
			q2: ['oval', 'tilted'],
			q3: 'dysnomia',
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

<main class="eris-page">
	<section class="top">
		<div class="title">
			<p class="tag">Far Frontier</p>
			<h1>Eris</h1>
			<p class="subtitle">
				A distant dwarf planet that helped change how we define planets. Jump through the sections
				to explore.
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
					{#if id === 'id-size'}Size{/if}
					{#if id === 'id-orbit'}Orbit{/if}
					{#if id === 'id-surface'}Surface{/if}
					{#if id === 'id-discovery'}Discovery{/if}
					{#if id === 'id-quiz'}Mini Test{/if}
				</button>
			{/each}
		</nav>
	</section>

	<section class="eris-layout">
		<div class="eris-core" aria-hidden="true">
			<div class="eris-sphere"></div>
			<div class="eris-halo"></div>
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
				Eris is a dwarf planet far beyond Neptune. Its discovery helped scientists decide that Pluto
				and similar objects should be called dwarf planets instead of full planets.
			</p>
			<p>
				It is one of the largest and most massive dwarf planets we know.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-size'} id="id-size">
			<h2>Size and Moon</h2>
			<p>
				Eris is similar in size to Pluto. It has a small moon named Dysnomia.
			</p>
			<p>
				Together they form a tiny system far from the Sun.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-orbit'} id="id-orbit">
			<h2>Orbit</h2>
			<p>
				Eris travels in a very stretched, tilted orbit. One trip around the Sun takes more than 500
				years.
			</p>
			<p>
				At its farthest point, it goes even farther out than Pluto.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-surface'} id="id-surface">
			<h2>Surface</h2>
			<p>
				Its surface is extremely cold and covered in frozen gases like methane. The surface looks
				bright because it reflects a lot of sunlight.
			</p>
			<p>
				Any atmosphere is very thin and likely freezes out most of the time.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-discovery'} id="id-discovery">
			<h2>Discovery</h2>
			<p>
				Eris was discovered in 2005 by a team led by Mike Brown. Its discovery pushed scientists to
				define the term planet more carefully.
			</p>
			<p>
				It was named after the Greek goddess of discord.
			</p>
		</article>

		<article class="panel" data-active={activeSection === 'id-quiz'} id="id-quiz">
			<h2>Mini Test</h2>
			<div class="quiz">
				<div class="question">
					<p>1. Short answer: Eris is a ______ planet.</p>
					<input type="text" placeholder="One word" bind:value={quizAnswers.q1} />
				</div>
				<div class="question">
					<p>2. Multi-select: Which two describe Eris orbit?</p>
					<label>
						<input type="checkbox" value="oval" bind:group={quizAnswers.q2} />
						Oval
					</label>
					<label>
						<input type="checkbox" value="tilted" bind:group={quizAnswers.q2} />
						Tilted
					</label>
					<label>
						<input type="checkbox" value="perfect" bind:group={quizAnswers.q2} />
						Perfect circle
					</label>
				</div>
				<div class="question">
					<p>3. Short answer: What is the name of Eris moon?</p>
					<input type="text" placeholder="One word" bind:value={quizAnswers.q3} />
				</div>
				<div class="question">
					<p>4. Which statement is most accurate?</p>
					<label>
						<input type="radio" name="q4" value="a" bind:group={quizAnswers.q4} />
						Eris orbits closer than Mars
					</label>
					<label>
						<input type="radio" name="q4" value="b" bind:group={quizAnswers.q4} />
						Eris orbits far beyond Neptune
					</label>
					<label>
						<input type="radio" name="q4" value="c" bind:group={quizAnswers.q4} />
						Eris is a comet
					</label>
				</div>
				<div class="question">
					<p>5. True or False: Eris discovery helped change the planet definition.</p>
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
		color: #eef2ff;
		background:
			radial-gradient(circle at 20% 15%, rgba(140, 160, 255, 0.3), transparent 45%),
			radial-gradient(circle at 85% 25%, rgba(120, 110, 255, 0.25), transparent 45%),
			radial-gradient(circle at 40% 90%, rgba(90, 120, 200, 0.25), transparent 45%),
			linear-gradient(160deg, #0a0c1a 15%, #101225 55%, #0a0b18 100%);
		min-height: 100svh;
	}

	.eris-page {
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
		color: rgba(190, 200, 255, 0.8);
	}

	.subtitle {
		margin: 0;
		color: rgba(238, 242, 255, 0.8);
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
		background: linear-gradient(120deg, #9aa7ff, #6c7bff);
		color: #0c0d18;
		border-color: transparent;
		box-shadow: 0 15px 30px rgba(120, 130, 255, 0.35);
		transform: translateY(-1px);
	}

	.eris-layout {
		position: relative;
		min-height: 320px;
		display: grid;
		place-items: center;
	}

	.eris-core {
		position: relative;
		width: min(240px, 40vw);
		aspect-ratio: 1;
		border-radius: 50%;
		display: grid;
		place-items: center;
		filter: drop-shadow(0 20px 50px rgba(120, 130, 255, 0.35));
	}

	.eris-sphere {
		position: absolute;
		inset: 0;
		border-radius: 50%;
		background:
			radial-gradient(circle at 30% 30%, rgba(230, 235, 255, 0.9), transparent 40%),
			radial-gradient(circle at 70% 60%, rgba(120, 140, 255, 0.6), transparent 50%),
			radial-gradient(circle at 50% 50%, #cfd6ff, #8a97ff 60%, #4c56a8 100%);
		animation: slowspin 22s linear infinite;
	}

	.eris-halo {
		position: absolute;
		inset: -8%;
		border-radius: 50%;
		background: radial-gradient(circle, rgba(140, 160, 255, 0.3), transparent 70%);
		filter: blur(6px);
		animation: pulse 4s ease-in-out infinite;
	}

	.fact {
		position: absolute;
		width: min(220px, 40vw);
		background: rgba(12, 14, 28, 0.78);
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
		color: rgba(238, 242, 255, 0.8);
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
		background: rgba(12, 14, 28, 0.8);
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
		background: linear-gradient(120deg, #9aa7ff, #6c7bff);
		color: #0c0d18;
		padding: 0.6rem 1.2rem;
		border-radius: 999px;
		font-weight: 600;
		cursor: pointer;
		width: fit-content;
	}

	.score {
		margin: 0;
		font-weight: 600;
		color: rgba(200, 210, 255, 0.9);
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

		.eris-layout {
			min-height: 240px;
		}
	}
</style>
