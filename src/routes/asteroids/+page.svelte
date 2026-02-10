<script>
	const sections = ["id-overview", "id-structure", "id-orbits", "id-types", "id-famous", "id-quiz"];
	const factsBySection = {"id-overview": [{"title": "Small Bodies", "text": "Asteroids are small rocky objects."}, {"title": "Many", "text": "Millions orbit the Sun."}, {"title": "Main Belt", "text": "Most live between Mars and Jupiter."}, {"title": "Near Earth", "text": "Some pass near Earth."}, {"title": "Leftovers", "text": "They are leftover building blocks."}], "id-structure": [{"title": "Rocky", "text": "Most are made of rock and metal."}, {"title": "Rubble Piles", "text": "Some are piles of loose rocks."}, {"title": "Odd Shapes", "text": "Many are lumpy, not round."}, {"title": "Craters", "text": "Impacts leave craters and scars."}, {"title": "Spinning", "text": "They rotate at different speeds."}], "id-orbits": [{"title": "Elliptical", "text": "Orbits are often oval."}, {"title": "Families", "text": "Groups share similar orbits."}, {"title": "Resonance", "text": "Jupiter creates gaps in the belt."}, {"title": "Crossers", "text": "Some cross Earths orbit."}, {"title": "Long Paths", "text": "Farther ones move more slowly."}], "id-types": [{"title": "C Type", "text": "Carbon-rich and dark."}, {"title": "S Type", "text": "Stony and brighter."}, {"title": "M Type", "text": "Metal-rich."}, {"title": "Colors", "text": "Color hints at material."}, {"title": "Meteorites", "text": "Some pieces land on Earth."}], "id-famous": [{"title": "Vesta", "text": "A large asteroid visited by Dawn."}, {"title": "Ceres", "text": "The largest object in the belt."}, {"title": "Bennu", "text": "Sampled by OSIRIS-REx."}, {"title": "Ryugu", "text": "Sampled by Hayabusa2."}, {"title": "Chelyabinsk", "text": "A small impact event in 2013."}], "id-quiz": [{"title": "Quick Recall", "text": "Use the facts from each section."}, {"title": "Be Precise", "text": "Short answers should be clear."}, {"title": "Think First", "text": "Try to answer before guessing."}, {"title": "Challenge", "text": "Some answers need details."}, {"title": "You Got This", "text": "Check your score at the end."}]};
	let activeSection = 'id-overview';
	let activeFacts = factsBySection[activeSection];
	let quizAnswers = { q1: '', q2: [], q3: '', q4: '', q5: '' };
	let score = null;
	function setSection(id) { activeSection = id; }
	function submitQuiz() {
		const answerKey = { q1: 'rocky', q2: ["belt", "near"], q3: 'ceres', q4: 'b', q5: 'true' };
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

<main class="asteroids-page">
	<section class="top">
		<div class="title">
			<p class="tag">Rocky Travelers</p>
			<h1>Asteroids</h1>
			<p class="subtitle">Small rocky bodies orbiting the Sun.</p>
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
						class:active={activeSection === 'id-structure'}
						on:click={() => setSection('id-structure')}
					>
						Structure
					</button>
					<button
						type="button"
						class:active={activeSection === 'id-orbits'}
						on:click={() => setSection('id-orbits')}
					>
						Orbits
					</button>
					<button
						type="button"
						class:active={activeSection === 'id-types'}
						on:click={() => setSection('id-types')}
					>
						Types
					</button>
					<button
						type="button"
						class:active={activeSection === 'id-famous'}
						on:click={() => setSection('id-famous')}
					>
						Famous
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

	<section class="asteroids-layout">
		<div class="asteroids-core" aria-hidden="true">
			<div class="asteroids-sphere"></div>
			<div class="asteroids-halo"></div>
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
			<p>Asteroids are small rocky bodies that orbit the Sun.</p>
			<p>Most are in the asteroid belt, but some pass near Earth.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-structure'} id="id-structure">
			<h2>Structure</h2>
			<p>Asteroids are rocky or metallic and often irregular.</p>
			<p>Some are rubble piles held together by gravity.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-orbits'} id="id-orbits">
			<h2>Orbits</h2>
			<p>Asteroids orbit the Sun in oval paths.</p>
			<p>Some cross Earths orbit and are tracked closely.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-types'} id="id-types">
			<h2>Types</h2>
			<p>C-type, S-type, and M-type show different materials.</p>
			<p>Color and brightness give clues about composition.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-famous'} id="id-famous">
			<h2>Famous</h2>
			<p>Vesta and Ceres are large belt objects.</p>
			<p>Bennu and Ryugu were visited and sampled by missions.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-quiz'} id="id-quiz">
			<h2>Mini Test</h2>
			<div class="quiz">
				<div class="question">
					<p>1. Asteroids are mostly ______ bodies.</p>
					<input type="text" placeholder="One word" bind:value={quizAnswers.q1} />
				</div>
				<div class="question">
					<p>2. Multi-select: Which two are true?</p>
					<label><input type="checkbox" value="belt" bind:group={quizAnswers.q2} /> Many are in a belt</label>
					<label><input type="checkbox" value="near" bind:group={quizAnswers.q2} /> Some pass near Earth</label>
					<label><input type="checkbox" value="rings" bind:group={quizAnswers.q2} /> They have rings</label>
				</div>
				<div class="question">
					<p>3. Short answer: Name the largest object in the asteroid belt.</p>
					<input type="text" placeholder="Answer" bind:value={quizAnswers.q3} />
				</div>
				<div class="question">
					<p>4. Which statement is most accurate?</p>
					<label><input type="radio" name="q4" value="a" bind:group={quizAnswers.q4} /> All asteroids are round</label>
					<label><input type="radio" name="q4" value="b" bind:group={quizAnswers.q4} /> Many are irregular shapes</label>
					<label><input type="radio" name="q4" value="c" bind:group={quizAnswers.q4} /> They are gas giants</label>
				</div>
				<div class="question">
					<p>5. True or False: Some meteorites are asteroid pieces.</p>
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
			radial-gradient(circle at 20% 12%, rgba(170, 190, 210, 0.25), transparent 45%),
			radial-gradient(circle at 80% 18%, rgba(130, 150, 180, 0.22), transparent 45%),
			radial-gradient(circle at 45% 90%, rgba(100, 120, 150, 0.2), transparent 45%),
			linear-gradient(160deg, #0a0e14 15%, #111723 55%, #0a0d16 100%);
		min-height: 100svh;
	}
	.asteroids-page { min-height: 100svh; padding: clamp(1.5rem, 4vw, 3rem); display: grid; gap: clamp(1.2rem, 2.4vw, 2.2rem); }
	.top { display: grid; grid-template-columns: minmax(0, 1fr) minmax(0, 320px); gap: 1.5rem; align-items: center; }
	.title h1 { margin: 0 0 0.6rem; font-family: "Unbounded", "Space Grotesk", system-ui, sans-serif; font-size: clamp(2.4rem, 4.5vw, 3.8rem); }
	.tag { margin: 0 0 0.6rem; letter-spacing: 0.28em; text-transform: uppercase; font-size: 0.8rem; color: rgba(200, 210, 230, 0.85); }
	.subtitle { margin: 0; color: rgba(246, 247, 255, 0.8); line-height: 1.5; }
	.jump { display: grid; gap: 0.5rem; }
	.jump button { border: 1px solid rgba(255, 255, 255, 0.12); background: rgba(255, 255, 255, 0.05); color: inherit; padding: 0.55rem 0.9rem; border-radius: 999px; font-size: 0.85rem; cursor: pointer; transition: transform 0.2s ease, box-shadow 0.2s ease; }
	.jump button.active { background: linear-gradient(120deg, #b1c3d8, #8ea3c2); color: #0b0c18; border-color: transparent; box-shadow: 0 15px 30px rgba(170, 190, 210, 0.35); transform: translateY(-1px); }
	.asteroids-layout { position: relative; min-height: 320px; display: grid; place-items: center; }
	.asteroids-core { position: relative; width: min(240px, 40vw); aspect-ratio: 1; border-radius: 50%; display: grid; place-items: center; filter: drop-shadow(0 20px 50px rgba(170, 190, 210, 0.35)); }
	.asteroids-sphere { position: absolute; inset: 0; border-radius: 50%; background: radial-gradient(circle at 30% 30%, rgba(230, 235, 245, 0.9), transparent 40%), radial-gradient(circle at 70% 60%, rgba(150, 170, 200, 0.6), transparent 50%), radial-gradient(circle at 50% 50%, #d4dbe6, #9aa9bf 60%, #5b6a80 100%); animation: slowspin 22s linear infinite; }
	.asteroids-halo { position: absolute; inset: -8%; border-radius: 50%; background: radial-gradient(circle, rgba(170, 190, 210, 0.35), transparent 70%); filter: blur(6px); animation: pulse 4s ease-in-out infinite; }
	.fact { position: absolute; width: min(220px, 40vw); background: rgba(12, 16, 22, 0.78); border: 1px solid rgba(255, 255, 255, 0.1); border-radius: 16px; padding: 0.8rem 1rem; box-shadow: 0 20px 40px rgba(0, 0, 0, 0.45); animation: float 4s ease-in-out infinite; }
	.fact h3 { margin: 0 0 0.3rem; font-size: 1rem; }
	.fact p { margin: 0; font-size: 0.9rem; color: rgba(246, 247, 255, 0.8); }
	.orbit-1 { top: 0; left: 4%; animation-delay: 0s; }
	.orbit-2 { top: 10%; right: 6%; animation-delay: 0.6s; }
	.orbit-3 { bottom: 10%; right: 4%; animation-delay: 1.2s; }
	.orbit-4 { bottom: 0; left: 10%; animation-delay: 1.8s; }
	.orbit-5 { top: 42%; left: -2%; animation-delay: 2.4s; }
	.panels { display: grid; grid-template-columns: minmax(0, 1fr); }
	.panel { display: none; background: rgba(12, 16, 22, 0.78); border-radius: 18px; padding: 1.3rem 1.6rem; border: 1px solid rgba(255, 255, 255, 0.1); box-shadow: 0 25px 50px rgba(0, 0, 0, 0.45); animation: fadeIn 0.35s ease; }
	.panel[data-active='true'] { display: block; }
	.panel h2 { margin: 0 0 0.6rem; }
	.panel p { color: rgba(246, 247, 255, 0.8); line-height: 1.6; }
	.quiz { display: grid; gap: 0.8rem; }
	.question { display: grid; gap: 0.35rem; font-size: 0.95rem; }
	.question label { display: flex; align-items: center; gap: 0.4rem; }
	.question input[type='text'] { border-radius: 10px; border: 1px solid rgba(255, 255, 255, 0.15); background: rgba(255, 255, 255, 0.06); color: inherit; padding: 0.35rem 0.6rem; }
	.submit { border: none; background: linear-gradient(120deg, #b1c3d8, #8ea3c2); color: #0b0c18; padding: 0.6rem 1.2rem; border-radius: 999px; font-weight: 600; cursor: pointer; width: fit-content; }
	.score { margin: 0; font-weight: 600; color: rgba(200, 220, 255, 0.9); }
	@keyframes slowspin { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
	@keyframes pulse { 0%, 100% { transform: scale(1); opacity: 0.6; } 50% { transform: scale(1.08); opacity: 0.9; } }
	@keyframes float { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-8px); } }
	@keyframes fadeIn { from { opacity: 0; transform: translateY(6px); } to { opacity: 1; transform: translateY(0); } }
	@media (max-width: 900px) { .top { grid-template-columns: 1fr; } .jump { grid-template-columns: repeat(3, minmax(0, 1fr)); } .fact { display: none; } .asteroids-layout { min-height: 240px; } }
</style>
