<script>
	const sections = ["id-overview", "id-members", "id-features", "id-distance", "id-compare", "id-quiz"];
	const factsBySection = {"id-overview": [{"title": "Core Idea", "text": "Satellites are natural moons that orbit planets."}, {"title": "Gravity Bond", "text": "They are held by a planet’s gravity, not their own."}, {"title": "Many Sizes", "text": "Some are tiny rocks, others are bigger than planets."}, {"title": "No Light", "text": "Moons shine by reflecting sunlight, not making it."}, {"title": "Hidden Oceans", "text": "Some icy moons may hide oceans under the surface."}], "id-members": [{"title": "Earth’s Moon", "text": "Our Moon causes tides and shows the same face."}, {"title": "Mars Moons", "text": "Phobos and Deimos are small and lumpy."}, {"title": "Jupiter’s Giants", "text": "Io, Europa, Ganymede, and Callisto are huge moons."}, {"title": "Saturn’s Stars", "text": "Titan has a thick atmosphere; Enceladus has ice geysers."}, {"title": "Ice Giants", "text": "Uranus and Neptune also have many icy moons."}], "id-features": [{"title": "Tidal Lock", "text": "Many moons always show the same face to their planet."}, {"title": "Craters", "text": "Old surfaces are covered with impact craters."}, {"title": "Volcanoes", "text": "Io is the most volcanic world in the solar system."}, {"title": "Ice and Water", "text": "Europa and Enceladus may hide liquid water."}, {"title": "Thin Air", "text": "Most moons have little or no atmosphere."}], "id-distance": [{"title": "Near vs Far", "text": "Close moons feel stronger tides and pull."}, {"title": "Orbital Speeds", "text": "Inner moons orbit faster than outer ones."}, {"title": "Ring Shepherds", "text": "Some small moons guide and shape planetary rings."}, {"title": "Eclipse Maker", "text": "Moons can cause eclipses as they pass in front of a planet."}, {"title": "Stable Paths", "text": "Moons follow set paths that can last billions of years."}], "id-compare": [{"title": "Size Range", "text": "Moons range from tiny rocks to Ganymede, bigger than Mercury."}, {"title": "Surface Types", "text": "Some are rocky, some are icy, some are mixed."}, {"title": "Atmospheres", "text": "Titan has a thick atmosphere; most moons do not."}, {"title": "Activity", "text": "Some moons are active with volcanoes or geysers."}, {"title": "Planet Partners", "text": "Moons help shape a planet’s tides and rings."}], "id-quiz": [{"title": "Core Idea", "text": "Use real moon facts."}, {"title": "Key Detail", "text": "Think about orbits, tides, and icy moons."}, {"title": "Quick Clue", "text": "Moons reflect sunlight."}, {"title": "Remember", "text": "Some moons may have hidden oceans."}, {"title": "Extra", "text": "Be precise and use a real example."}]};
	let activeSection = 'id-overview';
	let activeFacts = factsBySection[activeSection];
	let quizAnswers = { q1: '', q2: [], q3: '', q4: '', q5: '' };
	let score = null;
	function setSection(id) { activeSection = id; }
	function submitQuiz() {
		const answerKey = { q1: 'natural', q2: ["orbit", "icy"], q3: 'moon', q4: 'b', q5: 'true' };
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

<main class="satellites-page">
	<section class="top">
		<div class="title">
			<p class="tag">Moon Worlds</p>
			<h1>Satellites</h1>
			<p class="subtitle">Natural moons that orbit planets and shape their worlds.</p>
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

	<section class="satellites-layout">
		<div class="satellites-core" aria-hidden="true">
			<div class="satellites-sphere"></div>
			<div class="satellites-halo"></div>
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
			<p>Satellites are natural moons that orbit planets.</p>
			<p>They shine by reflecting sunlight, not making their own.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-members'} id="id-members">
			<h2>Members</h2>
			<p>Earth’s Moon, Mars’s Phobos and Deimos, and Jupiter’s big four.</p>
			<p>Saturn’s Titan and Enceladus are famous icy moons.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-features'} id="id-features">
			<h2>Features</h2>
			<p>Many moons are tidally locked and covered in craters.</p>
			<p>Some are active with volcanoes or icy geysers.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-distance'} id="id-distance">
			<h2>Distance</h2>
			<p>Closer moons orbit faster and feel stronger tidal forces.</p>
			<p>Some small moons help keep ring edges in place.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-compare'} id="id-compare">
			<h2>Compare</h2>
			<p>Moons range from tiny rocks to Ganymede, bigger than Mercury.</p>
			<p>Titan has a thick atmosphere, while most moons have none.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-quiz'} id="id-quiz">
			<h2>Mini Test</h2>
			<div class="quiz">
				<div class="question">
					<p>1. These are ______ satellites.</p>
					<input type="text" placeholder="One word" bind:value={quizAnswers.q1} />
				</div>
				<div class="question">
					<p>2. Multi-select: Which statements fit moons?</p>
					<label><input type="checkbox" value="orbit" bind:group={quizAnswers.q2} /> They orbit planets</label>
					<label><input type="checkbox" value="icy" bind:group={quizAnswers.q2} /> Some are icy</label>
					<label><input type="checkbox" value="light" bind:group={quizAnswers.q2} /> They make their own light</label>
				</div>
				<div class="question">
					<p>3. Short answer: Name one moon in our solar system.</p>
					<input type="text" placeholder="Answer" bind:value={quizAnswers.q3} />
				</div>
				<div class="question">
					<p>4. Which statement is most accurate?</p>
					<label><input type="radio" name="q4" value="a" bind:group={quizAnswers.q4} /> They are stars</label>
					<label><input type="radio" name="q4" value="b" bind:group={quizAnswers.q4} /> They are smaller than their planets</label>
					<label><input type="radio" name="q4" value="c" bind:group={quizAnswers.q4} /> They are planets with rings</label>
				</div>
				<div class="question">
					<p>5. True or False: Some moons may have hidden oceans.</p>
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
			radial-gradient(circle at 20% 12%, rgba(140, 190, 255, 0.25), transparent 45%),
			radial-gradient(circle at 80% 18%, rgba(120, 160, 220, 0.22), transparent 45%),
			radial-gradient(circle at 45% 90%, rgba(110, 140, 200, 0.2), transparent 45%),
			linear-gradient(160deg, #0a0f1a 15%, #101a26 55%, #0a0f18 100%);
		min-height: 100svh;
	}
	.satellites-page { min-height: 100svh; padding: clamp(1.5rem, 4vw, 3rem); display: grid; gap: clamp(1.2rem, 2.4vw, 2.2rem); }
	.top { display: grid; grid-template-columns: minmax(0, 1fr) minmax(0, 320px); gap: 1.5rem; align-items: center; }
	.title h1 { margin: 0 0 0.6rem; font-family: "Unbounded", "Space Grotesk", system-ui, sans-serif; font-size: clamp(2.4rem, 4.5vw, 3.8rem); }
	.tag { margin: 0 0 0.6rem; letter-spacing: 0.28em; text-transform: uppercase; font-size: 0.8rem; color: rgba(190, 210, 255, 0.85); }
	.subtitle { margin: 0; color: rgba(246, 247, 255, 0.8); line-height: 1.5; }
	.jump { display: grid; gap: 0.5rem; }
	.jump button { border: 1px solid rgba(255, 255, 255, 0.12); background: rgba(255, 255, 255, 0.05); color: inherit; padding: 0.55rem 0.9rem; border-radius: 999px; font-size: 0.85rem; cursor: pointer; transition: transform 0.2s ease, box-shadow 0.2s ease; }
	.jump button.active { background: linear-gradient(120deg, #9ab8ff, #6a8dff); color: #0b0c18; border-color: transparent; box-shadow: 0 15px 30px rgba(150, 180, 255, 0.35); transform: translateY(-1px); }
	.satellites-layout { position: relative; min-height: 320px; display: grid; place-items: center; }
	.satellites-core { position: relative; width: min(240px, 40vw); aspect-ratio: 1; border-radius: 50%; display: grid; place-items: center; filter: drop-shadow(0 20px 50px rgba(150, 180, 255, 0.35)); }
	.satellites-sphere { position: absolute; inset: 0; border-radius: 50%; background: radial-gradient(circle at 30% 30%, rgba(220, 235, 255, 0.9), transparent 40%), radial-gradient(circle at 70% 60%, rgba(140, 170, 230, 0.6), transparent 50%), radial-gradient(circle at 50% 50%, #cbd8f2, #7aa0d6 60%, #3c5e9c 100%); animation: slowspin 22s linear infinite; }
	.satellites-halo { position: absolute; inset: -8%; border-radius: 50%; background: radial-gradient(circle, rgba(150, 180, 255, 0.35), transparent 70%); filter: blur(6px); animation: pulse 4s ease-in-out infinite; }
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
	@media (max-width: 900px) { .top { grid-template-columns: 1fr; } .jump { grid-template-columns: repeat(3, minmax(0, 1fr)); } .fact { display: none; } .satellites-layout { min-height: 240px; } }
</style>
