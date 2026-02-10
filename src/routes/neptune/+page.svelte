<script>
	const sections = ["id-overview", "id-color", "id-storms", "id-moons", "id-rings", "id-quiz"];
	const factsBySection = {"id-overview": [{"title": "Core Idea", "text": "What it is and where it belongs."}, {"title": "Key Detail", "text": "Key identity facts to remember."}, {"title": "Quick Clue", "text": "Deep blue planet with the fastest winds."}, {"title": "Remember", "text": "Very fast storms."}, {"title": "Extra", "text": "Remember this point."}], "id-color": [{"title": "Core Idea", "text": "Why it looks blue or green."}, {"title": "Key Detail", "text": "Gases and hazes change its color."}, {"title": "Quick Clue", "text": "Deep blue planet with the fastest winds."}, {"title": "Remember", "text": "Very fast storms."}, {"title": "Extra", "text": "Remember this point."}], "id-storms": [{"title": "Core Idea", "text": "Big storms and fast winds."}, {"title": "Key Detail", "text": "Weather that can last for years."}, {"title": "Quick Clue", "text": "Deep blue planet with the fastest winds."}, {"title": "Remember", "text": "Very fast storms."}, {"title": "Extra", "text": "Remember this point."}], "id-moons": [{"title": "Core Idea", "text": "Major moons and their traits."}, {"title": "Key Detail", "text": "Some are icy, some are volcanic."}, {"title": "Quick Clue", "text": "Deep blue planet with the fastest winds."}, {"title": "Remember", "text": "Very fast storms."}, {"title": "Extra", "text": "Remember this point."}], "id-rings": [{"title": "Core Idea", "text": "Rings are icy and thin."}, {"title": "Key Detail", "text": "Gaps and divisions shape the system."}, {"title": "Quick Clue", "text": "Deep blue planet with the fastest winds."}, {"title": "Remember", "text": "Very fast storms."}, {"title": "Extra", "text": "Remember this point."}], "id-quiz": [{"title": "Core Idea", "text": "Test yourself with harder questions."}, {"title": "Key Detail", "text": "Try to answer without guessing."}, {"title": "Quick Clue", "text": "Deep blue planet with the fastest winds."}, {"title": "Remember", "text": "Very fast storms."}, {"title": "Extra", "text": "Remember this point."}]};
	let activeSection = 'id-overview';
	let activeFacts = factsBySection[activeSection];
	let quizAnswers = { q1: '', q2: [], q3: '', q4: '', q5: '' };
	let score = null;
	function setSection(id) { activeSection = id; }
	function submitQuiz() {
		const answerKey = { q1: 'ice', q2: ["blue", "winds"], q3: 'rings', q4: 'b', q5: 'true' };
		let tally = 0;
		if (quizAnswers.q1.trim().toLowerCase().includes(answerKey.q1)) tally += 1;
		if (quizAnswers.q2.length === answerKey.q2.length && answerKey.q2.every((item) => quizAnswers.q2.includes(item))) tally += 1;
		if (quizAnswers.q3.trim().toLowerCase().includes(answerKey.q3)) tally += 1;
		if (quizAnswers.q4 === answerKey.q4) tally += 1;
		if (quizAnswers.q5 === answerKey.q5) tally += 1;
		score = `${tally} / 5`;
	}
	$: activeFacts = factsBySection[activeSection];
</script>

<main class="neptune-page">
	<section class="top">
		<div class="title">
			<p class="tag">Wind King</p>
			<h1>Neptune</h1>
			<p class="subtitle">Deep blue planet with the fastest winds.</p>
		</div>
		<nav class="jump">
					<button
						type="button"
						class:active={activeSection === 'id-overview'}
						on:click={() => setSection('id-overview')}
					>
						Overview
					</button>
					<button
						type="button"
						class:active={activeSection === 'id-color'}
						on:click={() => setSection('id-color')}
					>
						Color
					</button>
					<button
						type="button"
						class:active={activeSection === 'id-storms'}
						on:click={() => setSection('id-storms')}
					>
						Storms
					</button>
					<button
						type="button"
						class:active={activeSection === 'id-moons'}
						on:click={() => setSection('id-moons')}
					>
						Moons
					</button>
					<button
						type="button"
						class:active={activeSection === 'id-rings'}
						on:click={() => setSection('id-rings')}
					>
						Rings
					</button>
					<button
						type="button"
						class:active={activeSection === 'id-quiz'}
						on:click={() => setSection('id-quiz')}
					>
						Mini Test
					</button>
		</nav>
	</section>

	<section class="neptune-layout">
		<div class="neptune-core" aria-hidden="true">
			<div class="neptune-sphere"></div>
			<div class="neptune-halo"></div>
		</div>

		{#each activeFacts as fact, index (index)}
			<div class="fact orbit-{index + 1}">
				<h3>{fact.title}</h3>
				<p>{fact.text}</p>
			</div>
		{/each}
	</section>

	<section class="panels">
		<article class="panel" data-active={activeSection === 'id-overview'} id="id-overview">
			<h2>Overview</h2>
			<p>What it is and where it belongs.</p>
			<p>Key identity facts to remember.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-color'} id="id-color">
			<h2>Color</h2>
			<p>Why it looks blue or green.</p>
			<p>Gases and hazes change its color.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-storms'} id="id-storms">
			<h2>Storms</h2>
			<p>Big storms and fast winds.</p>
			<p>Weather that can last for years.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-moons'} id="id-moons">
			<h2>Moons</h2>
			<p>Major moons and their traits.</p>
			<p>Some are icy, some are volcanic.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-rings'} id="id-rings">
			<h2>Rings</h2>
			<p>Rings are icy and thin.</p>
			<p>Gaps and divisions shape the system.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-quiz'} id="id-quiz">
			<h2>Mini Test</h2>
			<div class="quiz">
				<div class="question">
					<p>1. This world is an ______ giant.</p>
					<input type="text" placeholder="One word" bind:value={quizAnswers.q1} />
				</div>
				<div class="question">
					<p>2. Multi-select:</p>
					<label><input type="checkbox" value="blue" bind:group={quizAnswers.q2} /> Looks blue</label>
					<label><input type="checkbox" value="winds" bind:group={quizAnswers.q2} /> Fast winds</label>
					<label><input type="checkbox" value="hot" bind:group={quizAnswers.q2} /> Very hot</label>
				</div>
				<div class="question">
					<p>3. Short answer: Name a feature of this planet.</p>
					<input type="text" placeholder="Answer" bind:value={quizAnswers.q3} />
				</div>
				<div class="question">
					<p>4. Which statement is most accurate?</p>
					<label><input type="radio" name="q4" value="a" bind:group={quizAnswers.q4} /> It is closest to the Sun</label>
					<label><input type="radio" name="q4" value="b" bind:group={quizAnswers.q4} /> It is cold and distant</label>
					<label><input type="radio" name="q4" value="c" bind:group={quizAnswers.q4} /> It is a star</label>
				</div>
				<div class="question">
					<p>5. True or False: It has rings.</p>
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
			radial-gradient(circle at 20% 12%, rgba(120, 210, 255, 0.25), transparent 45%),
			radial-gradient(circle at 80% 18%, rgba(90, 170, 240, 0.22), transparent 45%),
			radial-gradient(circle at 45% 90%, rgba(90, 200, 200, 0.2), transparent 45%),
			linear-gradient(160deg, #07131a 15%, #0a1a22 55%, #071018 100%);
		min-height: 100svh;
	}
	.neptune-page { min-height: 100svh; padding: clamp(1.5rem, 4vw, 3rem); display: grid; gap: clamp(1.2rem, 2.4vw, 2.2rem); }
	.top { display: grid; grid-template-columns: minmax(0, 1fr) minmax(0, 320px); gap: 1.5rem; align-items: center; }
	.title h1 { margin: 0 0 0.6rem; font-family: "Unbounded", "Space Grotesk", system-ui, sans-serif; font-size: clamp(2.4rem, 4.5vw, 3.8rem); }
	.tag { margin: 0 0 0.6rem; letter-spacing: 0.28em; text-transform: uppercase; font-size: 0.8rem; color: rgba(170, 230, 255, 0.85); }
	.subtitle { margin: 0; color: rgba(246, 247, 255, 0.8); line-height: 1.5; }
	.jump { display: grid; gap: 0.5rem; }
	.jump button { border: 1px solid rgba(255, 255, 255, 0.12); background: rgba(255, 255, 255, 0.05); color: inherit; padding: 0.55rem 0.9rem; border-radius: 999px; font-size: 0.85rem; cursor: pointer; transition: transform 0.2s ease, box-shadow 0.2s ease; }
	.jump button.active { background: linear-gradient(120deg, #7ad6ff, #6aa9ff); color: #0b0c18; border-color: transparent; box-shadow: 0 15px 30px rgba(120, 210, 255, 0.35); transform: translateY(-1px); }
	.neptune-layout { position: relative; min-height: 320px; display: grid; place-items: center; }
	.neptune-core { position: relative; width: min(240px, 40vw); aspect-ratio: 1; border-radius: 50%; display: grid; place-items: center; filter: drop-shadow(0 20px 50px rgba(120, 210, 255, 0.35)); }
	.neptune-sphere { position: absolute; inset: 0; border-radius: 50%; background: radial-gradient(circle at 30% 30%, rgba(220, 250, 255, 0.9), transparent 40%), radial-gradient(circle at 70% 60%, rgba(120, 210, 255, 0.6), transparent 50%), radial-gradient(circle at 50% 50%, #b2e6ff, #6ac7e8 60%, #2f7fa8 100%); animation: slowspin 22s linear infinite; }
	.neptune-halo { position: absolute; inset: -8%; border-radius: 50%; background: radial-gradient(circle, rgba(120, 210, 255, 0.35), transparent 70%); filter: blur(6px); animation: pulse 4s ease-in-out infinite; }
	.fact { position: absolute; width: min(220px, 40vw); background: rgba(10, 18, 26, 0.78); border: 1px solid rgba(255, 255, 255, 0.1); border-radius: 16px; padding: 0.8rem 1rem; box-shadow: 0 20px 40px rgba(0, 0, 0, 0.45); animation: float 4s ease-in-out infinite; }
	.fact h3 { margin: 0 0 0.3rem; font-size: 1rem; }
	.fact p { margin: 0; font-size: 0.9rem; color: rgba(246, 247, 255, 0.8); }
	.orbit-1 { top: 0; left: 4%; animation-delay: 0s; }
	.orbit-2 { top: 10%; right: 6%; animation-delay: 0.6s; }
	.orbit-3 { bottom: 10%; right: 4%; animation-delay: 1.2s; }
	.orbit-4 { bottom: 0; left: 10%; animation-delay: 1.8s; }
	.orbit-5 { top: 42%; left: -2%; animation-delay: 2.4s; }
	.panels { display: grid; grid-template-columns: minmax(0, 1fr); }
	.panel { display: none; background: rgba(10, 18, 26, 0.78); border-radius: 18px; padding: 1.3rem 1.6rem; border: 1px solid rgba(255, 255, 255, 0.1); box-shadow: 0 25px 50px rgba(0, 0, 0, 0.45); animation: fadeIn 0.35s ease; }
	.panel[data-active='true'] { display: block; }
	.panel h2 { margin: 0 0 0.6rem; }
	.panel p { color: rgba(246, 247, 255, 0.8); line-height: 1.6; }
	.quiz { display: grid; gap: 0.8rem; }
	.question { display: grid; gap: 0.35rem; font-size: 0.95rem; }
	.question label { display: flex; align-items: center; gap: 0.4rem; }
	.question input[type='text'] { border-radius: 10px; border: 1px solid rgba(255, 255, 255, 0.15); background: rgba(255, 255, 255, 0.06); color: inherit; padding: 0.35rem 0.6rem; }
	.submit { border: none; background: linear-gradient(120deg, #7ad6ff, #6aa9ff); color: #0b0c18; padding: 0.6rem 1.2rem; border-radius: 999px; font-weight: 600; cursor: pointer; width: fit-content; }
	.score { margin: 0; font-weight: 600; color: rgba(200, 220, 255, 0.9); }
	@keyframes slowspin { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
	@keyframes pulse { 0%, 100% { transform: scale(1); opacity: 0.6; } 50% { transform: scale(1.08); opacity: 0.9; } }
	@keyframes float { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-8px); } }
	@keyframes fadeIn { from { opacity: 0; transform: translateY(6px); } to { opacity: 1; transform: translateY(0); } }
	@media (max-width: 900px) { .top { grid-template-columns: 1fr; } .jump { grid-template-columns: repeat(3, minmax(0, 1fr)); } .fact { display: none; } .neptune-layout { min-height: 240px; } }
+</style>
