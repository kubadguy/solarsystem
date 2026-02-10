<script>
	const sections = ["id-overview", "id-atmosphere", "id-storms", "id-moons", "id-rings", "id-quiz"];
	const factsBySection = {"id-overview": [{"title": "Core Idea", "text": "What it is and where it belongs."}, {"title": "Key Detail", "text": "Key identity facts to remember."}, {"title": "Quick Clue", "text": "Gas giant famous for bright rings."}, {"title": "Remember", "text": "Rings of ice and rock."}, {"title": "Extra", "text": "Remember this point."}], "id-atmosphere": [{"title": "Core Idea", "text": "Air, clouds, and pressure."}, {"title": "Key Detail", "text": "How the atmosphere changes heat and weather."}, {"title": "Quick Clue", "text": "Gas giant famous for bright rings."}, {"title": "Remember", "text": "Rings of ice and rock."}, {"title": "Extra", "text": "Remember this point."}], "id-storms": [{"title": "Core Idea", "text": "Big storms and fast winds."}, {"title": "Key Detail", "text": "Weather that can last for years."}, {"title": "Quick Clue", "text": "Gas giant famous for bright rings."}, {"title": "Remember", "text": "Rings of ice and rock."}, {"title": "Extra", "text": "Remember this point."}], "id-moons": [{"title": "Core Idea", "text": "Major moons and their traits."}, {"title": "Key Detail", "text": "Some are icy, some are volcanic."}, {"title": "Quick Clue", "text": "Gas giant famous for bright rings."}, {"title": "Remember", "text": "Rings of ice and rock."}, {"title": "Extra", "text": "Remember this point."}], "id-rings": [{"title": "Core Idea", "text": "Rings are icy and thin."}, {"title": "Key Detail", "text": "Gaps and divisions shape the system."}, {"title": "Quick Clue", "text": "Gas giant famous for bright rings."}, {"title": "Remember", "text": "Rings of ice and rock."}, {"title": "Extra", "text": "Remember this point."}], "id-quiz": [{"title": "Core Idea", "text": "Test yourself with harder questions."}, {"title": "Key Detail", "text": "Try to answer without guessing."}, {"title": "Quick Clue", "text": "Gas giant famous for bright rings."}, {"title": "Remember", "text": "Rings of ice and rock."}, {"title": "Extra", "text": "Remember this point."}]};
	let activeSection = 'id-overview';
	let activeFacts = factsBySection[activeSection];
	let quizAnswers = { q1: '', q2: [], q3: '', q4: '', q5: '' };
	let score = null;
	function setSection(id) { activeSection = id; }
	function submitQuiz() {
		const answerKey = { q1: 'gas', q2: ["storms", "rings"], q3: 'moons', q4: 'b', q5: 'true' };
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

<main class="saturn-page">
	<section class="top">
		<div class="title">
			<p class="tag">Ring Master</p>
			<h1>Saturn</h1>
			<p class="subtitle">Gas giant famous for bright rings.</p>
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
						class:active={activeSection === 'id-atmosphere'}
						on:click={() => setSection('id-atmosphere')}
					>
						Atmosphere
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

	<section class="saturn-layout">
		<div class="saturn-core" aria-hidden="true">
			<div class="saturn-sphere"></div>
			<div class="saturn-halo"></div>
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
		<article class="panel" data-active={activeSection === 'id-atmosphere'} id="id-atmosphere">
			<h2>Atmosphere</h2>
			<p>Air, clouds, and pressure.</p>
			<p>How the atmosphere changes heat and weather.</p>
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
					<p>1. This world is a ______ giant.</p>
					<input type="text" placeholder="One word" bind:value={quizAnswers.q1} />
				</div>
				<div class="question">
					<p>2. Multi-select:</p>
					<label><input type="checkbox" value="storms" bind:group={quizAnswers.q2} /> Has storms</label>
					<label><input type="checkbox" value="rings" bind:group={quizAnswers.q2} /> Has rings</label>
					<label><input type="checkbox" value="rocky" bind:group={quizAnswers.q2} /> Mostly rock</label>
				</div>
				<div class="question">
					<p>3. Short answer: Name a feature of this planet.</p>
					<input type="text" placeholder="Answer" bind:value={quizAnswers.q3} />
				</div>
				<div class="question">
					<p>4. Which statement is most accurate?</p>
					<label><input type="radio" name="q4" value="a" bind:group={quizAnswers.q4} /> It has a solid surface</label>
					<label><input type="radio" name="q4" value="b" bind:group={quizAnswers.q4} /> It is mostly gas</label>
					<label><input type="radio" name="q4" value="c" bind:group={quizAnswers.q4} /> It is a comet</label>
				</div>
				<div class="question">
					<p>5. True or False: It has many moons.</p>
					<label><input type="radio" name="q5" value="true" bind:group={{quizAnswers.q5}} /> True</label>
					<label><input type="radio" name="q5" value="false" bind:group={{quizAnswers.q5}} /> False</label>
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
			radial-gradient(circle at 20% 12%, rgba(255, 190, 140, 0.25), transparent 45%),
			radial-gradient(circle at 80% 18%, rgba(255, 150, 100, 0.22), transparent 45%),
			radial-gradient(circle at 45% 90%, rgba(210, 120, 90, 0.2), transparent 45%),
			linear-gradient(160deg, #120a08 15%, #1a120f 55%, #10090c 100%);
		min-height: 100svh;
	}
	.saturn-page { min-height: 100svh; padding: clamp(1.5rem, 4vw, 3rem); display: grid; gap: clamp(1.2rem, 2.4vw, 2.2rem); }
	.top { display: grid; grid-template-columns: minmax(0, 1fr) minmax(0, 320px); gap: 1.5rem; align-items: center; }
	.title h1 { margin: 0 0 0.6rem; font-family: "Unbounded", "Space Grotesk", system-ui, sans-serif; font-size: clamp(2.4rem, 4.5vw, 3.8rem); }
	.tag { margin: 0 0 0.6rem; letter-spacing: 0.28em; text-transform: uppercase; font-size: 0.8rem; color: rgba(255, 215, 180, 0.85); }
	.subtitle { margin: 0; color: rgba(246, 247, 255, 0.8); line-height: 1.5; }
	.jump { display: grid; gap: 0.5rem; }
	.jump button { border: 1px solid rgba(255, 255, 255, 0.12); background: rgba(255, 255, 255, 0.05); color: inherit; padding: 0.55rem 0.9rem; border-radius: 999px; font-size: 0.85rem; cursor: pointer; transition: transform 0.2s ease, box-shadow 0.2s ease; }
	.jump button.active { background: linear-gradient(120deg, #ffc07a, #ff8d5a); color: #0b0c18; border-color: transparent; box-shadow: 0 15px 30px rgba(255, 170, 120, 0.35); transform: translateY(-1px); }
	.saturn-layout { position: relative; min-height: 320px; display: grid; place-items: center; }
	.saturn-core { position: relative; width: min(240px, 40vw); aspect-ratio: 1; border-radius: 50%; display: grid; place-items: center; filter: drop-shadow(0 20px 50px rgba(255, 170, 120, 0.35)); }
	.saturn-sphere { position: absolute; inset: 0; border-radius: 50%; background: radial-gradient(circle at 30% 30%, rgba(255, 230, 210, 0.9), transparent 40%), radial-gradient(circle at 70% 60%, rgba(255, 170, 120, 0.6), transparent 50%), radial-gradient(circle at 50% 50%, #f4c7a2, #e0895c 60%, #a05435 100%); animation: slowspin 22s linear infinite; }
	.saturn-halo { position: absolute; inset: -8%; border-radius: 50%; background: radial-gradient(circle, rgba(255, 170, 120, 0.35), transparent 70%); filter: blur(6px); animation: pulse 4s ease-in-out infinite; }
	.fact { position: absolute; width: min(220px, 40vw); background: rgba(20, 15, 12, 0.78); border: 1px solid rgba(255, 255, 255, 0.1); border-radius: 16px; padding: 0.8rem 1rem; box-shadow: 0 20px 40px rgba(0, 0, 0, 0.45); animation: float 4s ease-in-out infinite; }
	.fact h3 { margin: 0 0 0.3rem; font-size: 1rem; }
	.fact p { margin: 0; font-size: 0.9rem; color: rgba(246, 247, 255, 0.8); }
	.orbit-1 { top: 0; left: 4%; animation-delay: 0s; }
	.orbit-2 { top: 10%; right: 6%; animation-delay: 0.6s; }
	.orbit-3 { bottom: 10%; right: 4%; animation-delay: 1.2s; }
	.orbit-4 { bottom: 0; left: 10%; animation-delay: 1.8s; }
	.orbit-5 { top: 42%; left: -2%; animation-delay: 2.4s; }
	.panels { display: grid; grid-template-columns: minmax(0, 1fr); }
	.panel { display: none; background: rgba(20, 15, 12, 0.78); border-radius: 18px; padding: 1.3rem 1.6rem; border: 1px solid rgba(255, 255, 255, 0.1); box-shadow: 0 25px 50px rgba(0, 0, 0, 0.45); animation: fadeIn 0.35s ease; }
	.panel[data-active='true'] { display: block; }
	.panel h2 { margin: 0 0 0.6rem; }
	.panel p { color: rgba(246, 247, 255, 0.8); line-height: 1.6; }
	.quiz { display: grid; gap: 0.8rem; }
	.question { display: grid; gap: 0.35rem; font-size: 0.95rem; }
	.question label { display: flex; align-items: center; gap: 0.4rem; }
	.question input[type='text'] { border-radius: 10px; border: 1px solid rgba(255, 255, 255, 0.15); background: rgba(255, 255, 255, 0.06); color: inherit; padding: 0.35rem 0.6rem; }
	.submit { border: none; background: linear-gradient(120deg, #ffc07a, #ff8d5a); color: #0b0c18; padding: 0.6rem 1.2rem; border-radius: 999px; font-weight: 600; cursor: pointer; width: fit-content; }
	.score { margin: 0; font-weight: 600; color: rgba(200, 220, 255, 0.9); }
	@keyframes slowspin { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
	@keyframes pulse { 0%, 100% { transform: scale(1); opacity: 0.6; } 50% { transform: scale(1.08); opacity: 0.9; } }
	@keyframes float { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-8px); } }
	@keyframes fadeIn { from { opacity: 0; transform: translateY(6px); } to { opacity: 1; transform: translateY(0); } }
	@media (max-width: 900px) { .top { grid-template-columns: 1fr; } .jump { grid-template-columns: repeat(3, minmax(0, 1fr)); } .fact { display: none; } .saturn-layout { min-height: 240px; } }
+</style>
