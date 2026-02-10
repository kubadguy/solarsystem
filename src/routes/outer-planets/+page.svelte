<script>
	const sections = ["id-overview", "id-members", "id-features", "id-distance", "id-compare", "id-quiz"];
	const factsBySection = {"id-overview": [{"title": "Core Idea", "text": "What it is and where it belongs."}, {"title": "Key Detail", "text": "Key identity facts to remember."}, {"title": "Quick Clue", "text": "Jupiter, Saturn, Uranus, Neptune."}, {"title": "Remember", "text": "Large and far from the Sun."}, {"title": "Extra", "text": "Remember this point."}], "id-members": [{"title": "Core Idea", "text": "Group members."}, {"title": "Key Detail", "text": "Order and key traits."}, {"title": "Quick Clue", "text": "Jupiter, Saturn, Uranus, Neptune."}, {"title": "Remember", "text": "Large and far from the Sun."}, {"title": "Extra", "text": "Remember this point."}], "id-features": [{"title": "Core Idea", "text": "Shared features."}, {"title": "Key Detail", "text": "Rings, storms, and size."}, {"title": "Quick Clue", "text": "Jupiter, Saturn, Uranus, Neptune."}, {"title": "Remember", "text": "Large and far from the Sun."}, {"title": "Extra", "text": "Remember this point."}], "id-distance": [{"title": "Core Idea", "text": "Distance from the Sun."}, {"title": "Key Detail", "text": "Longer years and colder temps."}, {"title": "Quick Clue", "text": "Jupiter, Saturn, Uranus, Neptune."}, {"title": "Remember", "text": "Large and far from the Sun."}, {"title": "Extra", "text": "Remember this point."}], "id-compare": [{"title": "Core Idea", "text": "Compare size and atmosphere."}, {"title": "Key Detail", "text": "What makes each unique."}, {"title": "Quick Clue", "text": "Jupiter, Saturn, Uranus, Neptune."}, {"title": "Remember", "text": "Large and far from the Sun."}, {"title": "Extra", "text": "Remember this point."}], "id-quiz": [{"title": "Core Idea", "text": "Test yourself with harder questions."}, {"title": "Key Detail", "text": "Try to answer without guessing."}, {"title": "Quick Clue", "text": "Jupiter, Saturn, Uranus, Neptune."}, {"title": "Remember", "text": "Large and far from the Sun."}, {"title": "Extra", "text": "Remember this point."}]};
	let activeSection = 'id-overview';
	let activeFacts = factsBySection[activeSection];
	let quizAnswers = { q1: '', q2: [], q3: '', q4: '', q5: '' };
	let score = null;
	function setSection(id) { activeSection = id; }
	function submitQuiz() {
		const answerKey = { q1: 'four', q2: ["planets", "group"], q3: 'order', q4: 'b', q5: 'true' };
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

<main class="outer-planets-page">
	<section class="top">
		<div class="title">
			<p class="tag">Giant Worlds</p>
			<h1>Outer Planets</h1>
			<p class="subtitle">Jupiter, Saturn, Uranus, Neptune.</p>
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
						class:active={activeSection === 'id-members'}
						on:click={() => setSection('id-members')}
					>
						Members
					</button>
					<button
						type="button"
						class:active={activeSection === 'id-features'}
						on:click={() => setSection('id-features')}
					>
						Features
					</button>
					<button
						type="button"
						class:active={activeSection === 'id-distance'}
						on:click={() => setSection('id-distance')}
					>
						Distance
					</button>
					<button
						type="button"
						class:active={activeSection === 'id-compare'}
						on:click={() => setSection('id-compare')}
					>
						Compare
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

	<section class="outer-planets-layout">
		<div class="outer-planets-core" aria-hidden="true">
			<div class="outer-planets-sphere"></div>
			<div class="outer-planets-halo"></div>
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
		<article class="panel" data-active={activeSection === 'id-members'} id="id-members">
			<h2>Members</h2>
			<p>Group members.</p>
			<p>Order and key traits.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-features'} id="id-features">
			<h2>Features</h2>
			<p>Shared features.</p>
			<p>Rings, storms, and size.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-distance'} id="id-distance">
			<h2>Distance</h2>
			<p>Distance from the Sun.</p>
			<p>Longer years and colder temps.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-compare'} id="id-compare">
			<h2>Compare</h2>
			<p>Compare size and atmosphere.</p>
			<p>What makes each unique.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-quiz'} id="id-quiz">
			<h2>Mini Test</h2>
			<div class="quiz">
				<div class="question">
					<p>1. There are ______ worlds in this group.</p>
					<input type="text" placeholder="One word" bind:value={quizAnswers.q1} />
				</div>
				<div class="question">
					<p>2. Multi-select:</p>
					<label><input type="checkbox" value="planets" bind:group={quizAnswers.q2} /> They are planets</label>
					<label><input type="checkbox" value="group" bind:group={quizAnswers.q2} /> They share traits</label>
					<label><input type="checkbox" value="rings" bind:group={quizAnswers.q2} /> They all have rings</label>
				</div>
				<div class="question">
					<p>3. Short answer: Name one member.</p>
					<input type="text" placeholder="Answer" bind:value={quizAnswers.q3} />
				</div>
				<div class="question">
					<p>4. Which statement is most accurate?</p>
					<label><input type="radio" name="q4" value="a" bind:group={quizAnswers.q4} /> They are all the same</label>
					<label><input type="radio" name="q4" value="b" bind:group={quizAnswers.q4} /> They share key features</label>
					<label><input type="radio" name="q4" value="c" bind:group={quizAnswers.q4} /> They are all comets</label>
				</div>
				<div class="question">
					<p>5. True or False: This group orbits the Sun.</p>
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
			radial-gradient(circle at 20% 12%, rgba(140, 190, 255, 0.25), transparent 45%),
			radial-gradient(circle at 80% 18%, rgba(120, 160, 220, 0.22), transparent 45%),
			radial-gradient(circle at 45% 90%, rgba(110, 140, 200, 0.2), transparent 45%),
			linear-gradient(160deg, #0a0f1a 15%, #101a26 55%, #0a0f18 100%);
		min-height: 100svh;
	}
	.outer-planets-page { min-height: 100svh; padding: clamp(1.5rem, 4vw, 3rem); display: grid; gap: clamp(1.2rem, 2.4vw, 2.2rem); }
	.top { display: grid; grid-template-columns: minmax(0, 1fr) minmax(0, 320px); gap: 1.5rem; align-items: center; }
	.title h1 { margin: 0 0 0.6rem; font-family: "Unbounded", "Space Grotesk", system-ui, sans-serif; font-size: clamp(2.4rem, 4.5vw, 3.8rem); }
	.tag { margin: 0 0 0.6rem; letter-spacing: 0.28em; text-transform: uppercase; font-size: 0.8rem; color: rgba(190, 210, 255, 0.85); }
	.subtitle { margin: 0; color: rgba(246, 247, 255, 0.8); line-height: 1.5; }
	.jump { display: grid; gap: 0.5rem; }
	.jump button { border: 1px solid rgba(255, 255, 255, 0.12); background: rgba(255, 255, 255, 0.05); color: inherit; padding: 0.55rem 0.9rem; border-radius: 999px; font-size: 0.85rem; cursor: pointer; transition: transform 0.2s ease, box-shadow 0.2s ease; }
	.jump button.active { background: linear-gradient(120deg, #9ab8ff, #6a8dff); color: #0b0c18; border-color: transparent; box-shadow: 0 15px 30px rgba(150, 180, 255, 0.35); transform: translateY(-1px); }
	.outer-planets-layout { position: relative; min-height: 320px; display: grid; place-items: center; }
	.outer-planets-core { position: relative; width: min(240px, 40vw); aspect-ratio: 1; border-radius: 50%; display: grid; place-items: center; filter: drop-shadow(0 20px 50px rgba(150, 180, 255, 0.35)); }
	.outer-planets-sphere { position: absolute; inset: 0; border-radius: 50%; background: radial-gradient(circle at 30% 30%, rgba(220, 235, 255, 0.9), transparent 40%), radial-gradient(circle at 70% 60%, rgba(140, 170, 230, 0.6), transparent 50%), radial-gradient(circle at 50% 50%, #cbd8f2, #7aa0d6 60%, #3c5e9c 100%); animation: slowspin 22s linear infinite; }
	.outer-planets-halo { position: absolute; inset: -8%; border-radius: 50%; background: radial-gradient(circle, rgba(150, 180, 255, 0.35), transparent 70%); filter: blur(6px); animation: pulse 4s ease-in-out infinite; }
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
	.panel p { color: rgba(246, 247, 255, 0.8); line-height: 1.6; }
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
	@media (max-width: 900px) { .top { grid-template-columns: 1fr; } .jump { grid-template-columns: repeat(3, minmax(0, 1fr)); } .fact { display: none; } .outer-planets-layout { min-height: 240px; } }
+</style>
