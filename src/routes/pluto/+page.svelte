<script>
	const sections = ['id-overview', 'id-orbit', 'id-surface', 'id-moons', 'id-discovery', 'id-quiz'];
	const factsBySection = {'id-overview': [{'title': 'Overview', 'text': 'Basic facts and identity.'}, {'title': 'Overview', 'text': 'Where it is and what it is made of.'}, {'title': 'Overview', 'text': 'Key traits you can remember.'}, {'title': 'Overview', 'text': 'Why it matters.'}, {'title': 'Overview', 'text': 'Large moon: Charon.'}], 'id-orbit': [{'title': 'Orbit', 'text': 'Oval path around the Sun.'}, {'title': 'Orbit', 'text': 'Year length and distance.'}, {'title': 'Orbit', 'text': 'Tilt and seasons.'}, {'title': 'Orbit', 'text': 'Speed changes.'}, {'title': 'Orbit', 'text': 'Special orbit facts.'}], 'id-surface': [{'title': 'Surface', 'text': 'Craters, plains, and mountains.'}, {'title': 'Surface', 'text': 'Signs of impacts and change.'}, {'title': 'Surface', 'text': 'Older and newer regions.'}, {'title': 'Surface', 'text': 'Textures and colors.'}, {'title': 'Surface', 'text': 'Interesting landmarks.'}], 'id-moons': [{'title': 'Moons', 'text': 'Major moons to know.'}, {'title': 'Moons', 'text': 'Icy and rocky types.'}, {'title': 'Moons', 'text': 'Interesting features.'}, {'title': 'Moons', 'text': 'Possible oceans.'}, {'title': 'Moons', 'text': 'Moon systems.'}], 'id-discovery': [{'title': 'Discovery', 'text': 'Discovery year and team.'}, {'title': 'Discovery', 'text': 'Name meaning.'}, {'title': 'Discovery', 'text': 'Why it is special.'}, {'title': 'Discovery', 'text': 'Planet debate.'}, {'title': 'Discovery', 'text': 'Still mysterious.'}], 'id-quiz': [{'title': 'Mini Test', 'text': 'Think deep.'}, {'title': 'Mini Test', 'text': 'Short answers and multi-select.'}, {'title': 'Mini Test', 'text': 'Be precise.'}, {'title': 'Mini Test', 'text': 'Reason it out.'}, {'title': 'Mini Test', 'text': 'Challenge mode.'}]};
	let activeSection = 'id-overview';
	let activeFacts = factsBySection[activeSection];
	let quizAnswers = { q1: '', q2: [], q3: '', q4: '', q5: '' };
	let score = null;
	function setSection(id) { activeSection = id; }
	function submitQuiz() {
		const answerKey = { q1: 'dwarf', q2: ['a','b'], q3: 'orbit', q4: 'b', q5: 'true' };
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

<main class="pluto-page">
	<section class="top">
		<div class="title">
			<p class="tag">Distant Dwarf</p>
			<h1>Pluto</h1>
			<p class="subtitle">Small icy world far beyond Neptune.</p>
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
						class:active={activeSection === 'id-orbit'}
						on:click={() => setSection('id-orbit')}
					>
						Orbit
					</button>
					<button
						type="button"
						class:active={activeSection === 'id-surface'}
						on:click={() => setSection('id-surface')}
					>
						Surface
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
						class:active={activeSection === 'id-discovery'}
						on:click={() => setSection('id-discovery')}
					>
						Discovery
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

	<section class="pluto-layout">
		<div class="pluto-core" aria-hidden="true">
			<div class="pluto-sphere"></div>
			<div class="pluto-halo"></div>
		</div>

		{#each activeFacts as fact, index (fact.title)}
			<div class="fact orbit-{index + 1}">
				<h3>{fact.title}</h3>
				<p>{fact.text}</p>
			</div>
		{/each}
	</section>

	<section class="panels">
		<article class="panel" data-active={activeSection === 'id-overview'} id="id-overview">
			<h2>Overview</h2>
			<p>Small icy world far beyond Neptune.</p>
			<p>Large moon: Charon.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-orbit'} id="id-orbit">
			<h2>Orbit</h2>
			<p>Small icy world far beyond Neptune.</p>
			<p>Large moon: Charon.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-surface'} id="id-surface">
			<h2>Surface</h2>
			<p>Small icy world far beyond Neptune.</p>
			<p>Large moon: Charon.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-moons'} id="id-moons">
			<h2>Moons</h2>
			<p>Small icy world far beyond Neptune.</p>
			<p>Large moon: Charon.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-discovery'} id="id-discovery">
			<h2>Discovery</h2>
			<p>Small icy world far beyond Neptune.</p>
			<p>Large moon: Charon.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-quiz'} id="id-quiz">
			<h2>Mini Test</h2>
			<div class="quiz">
				<div class="question">
					<p>1. Short answer:</p>
					<input type="text" placeholder="One word" bind:value={quizAnswers.q1} />
				</div>
				<div class="question">
					<p>2. Multi-select:</p>
					<label><input type="checkbox" value="a" bind:group={quizAnswers.q2} /> Option A</label>
					<label><input type="checkbox" value="b" bind:group={quizAnswers.q2} /> Option B</label>
					<label><input type="checkbox" value="c" bind:group={quizAnswers.q2} /> Option C</label>
				</div>
				<div class="question">
					<p>3. Short answer:</p>
					<input type="text" placeholder="Answer" bind:value={quizAnswers.q3} />
				</div>
				<div class="question">
					<p>4. Choose one:</p>
					<label><input type="radio" name="q4" value="a" bind:group={quizAnswers.q4} /> A</label>
					<label><input type="radio" name="q4" value="b" bind:group={quizAnswers.q4} /> B</label>
					<label><input type="radio" name="q4" value="c" bind:group={quizAnswers.q4} /> C</label>
				</div>
				<div class="question">
					<p>5. True or False:</p>
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
			radial-gradient(circle at 20% 12%, rgba(150, 190, 255, 0.28), transparent 45%),
			radial-gradient(circle at 80% 18%, rgba(120, 160, 230, 0.24), transparent 45%),
			radial-gradient(circle at 45% 90%, rgba(120, 140, 200, 0.2), transparent 45%),
			linear-gradient(160deg, #0b0f1a 15%, #111a2a 55%, #0a0f18 100%);
		min-height: 100svh;
	}
	.pluto-page { min-height: 100svh; padding: clamp(1.5rem, 4vw, 3rem); display: grid; gap: clamp(1.2rem, 2.4vw, 2.2rem); }
	.top { display: grid; grid-template-columns: minmax(0, 1fr) minmax(0, 320px); gap: 1.5rem; align-items: center; }
	.title h1 { margin: 0 0 0.6rem; font-family: "Unbounded", "Space Grotesk", system-ui, sans-serif; font-size: clamp(2.4rem, 4.5vw, 3.8rem); }
	.tag { margin: 0 0 0.6rem; letter-spacing: 0.28em; text-transform: uppercase; font-size: 0.8rem; color: rgba(190, 210, 255, 0.85); }
	.subtitle { margin: 0; color: rgba(246, 247, 255, 0.8); line-height: 1.5; }
	.jump { display: grid; gap: 0.5rem; }
	.jump button { border: 1px solid rgba(255, 255, 255, 0.12); background: rgba(255, 255, 255, 0.05); color: inherit; padding: 0.55rem 0.9rem; border-radius: 999px; font-size: 0.85rem; cursor: pointer; transition: transform 0.2s ease, box-shadow 0.2s ease; }
	.jump button.active { background: linear-gradient(120deg, #9ab8ff, #6a8dff); color: #0b0c18; border-color: transparent; box-shadow: 0 15px 30px rgba(150, 180, 255, 0.35); transform: translateY(-1px); }
	.pluto-layout { position: relative; min-height: 320px; display: grid; place-items: center; }
	.pluto-core { position: relative; width: min(240px, 40vw); aspect-ratio: 1; border-radius: 50%; display: grid; place-items: center; filter: drop-shadow(0 20px 50px rgba(150, 180, 255, 0.35)); }
	.pluto-sphere { position: absolute; inset: 0; border-radius: 50%; background: radial-gradient(circle at 30% 30%, rgba(220, 235, 255, 0.9), transparent 40%), radial-gradient(circle at 70% 60%, rgba(140, 170, 230, 0.6), transparent 50%), radial-gradient(circle at 50% 50%, #cbd8f2, #7aa0d6 60%, #3c5e9c 100%); animation: slowspin 22s linear infinite; }
	.pluto-halo { position: absolute; inset: -8%; border-radius: 50%; background: radial-gradient(circle, rgba(150, 180, 255, 0.35), transparent 70%); filter: blur(6px); animation: pulse 4s ease-in-out infinite; }
	.fact { position: absolute; width: min(220px, 40vw); background: rgba(12, 16, 28, 0.78); border: 1px solid rgba(255, 255, 255, 0.1); border-radius: 16px; padding: 0.8rem 1rem; box-shadow: 0 20px 40px rgba(0, 0, 0, 0.45); animation: float 4s ease-in-out infinite; }
	.fact h3 { margin: 0 0 0.3rem; font-size: 1rem; }
	.fact p { margin: 0; font-size: 0.9rem; color: rgba(246, 247, 255, 0.8); }
	.orbit-1 { top: 0; left: 4%; animation-delay: 0s; }
	.orbit-2 { top: 10%; right: 6%; animation-delay: 0.6s; }
	.orbit-3 { bottom: 10%; right: 4%; animation-delay: 1.2s; }
	.orbit-4 { bottom: 0; left: 10%; animation-delay: 1.8s; }
	.orbit-5 { top: 42%; left: -2%; animation-delay: 2.4s; }
	.panels { display: grid; grid-template-columns: minmax(0, 1fr); }
	.panel { display: none; background: rgba(12, 16, 28, 0.78); border-radius: 18px; padding: 1.3rem 1.6rem; border: 1px solid rgba(255, 255, 255, 0.1); box-shadow: 0 25px 50px rgba(0, 0, 0, 0.45); animation: fadeIn 0.35s ease; }
	.panel[data-active='true'] { display: block; }
	.panel h2 { margin: 0 0 0.6rem; }
	.panel p,
	.panel li { color: rgba(246, 247, 255, 0.8); line-height: 1.6; }
	.quiz { display: grid; gap: 0.8rem; }
	.question { display: grid; gap: 0.35rem; font-size: 0.95rem; }
	.question label { display: flex; align-items: center; gap: 0.4rem; }
	.question input[type='text'] { border-radius: 10px; border: 1px solid rgba(255, 255, 255, 0.15); background: rgba(255, 255, 255, 0.06); color: inherit; padding: 0.35rem 0.6rem; }
	.submit { border: none; background: linear-gradient(120deg, #9ab8ff, #6a8dff); color: #0b0c18; padding: 0.6rem 1.2rem; border-radius: 999px; font-weight: 600; cursor: pointer; width: fit-content; }
	.score { margin: 0; font-weight: 600; color: rgba(200, 220, 255, 0.9); }
	@keyframes slowspin { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
	@keyframes pulse { 0%, 100% { transform: scale(1); opacity: 0.6; } 50% { transform: scale(1.08); opacity: 0.9; } }
	@keyframes float { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-8px); } }
	@keyframes fadeIn { from { opacity: 0; transform: translateY(6px); } to { opacity: 1; transform: translateY(0); } }
	@media (max-width: 900px) { .top { grid-template-columns: 1fr; } .jump { grid-template-columns: repeat(3, minmax(0, 1fr)); } .fact { display: none; } .pluto-layout { min-height: 240px; } }
+</style>
