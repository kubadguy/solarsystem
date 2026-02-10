<script>
	const sections = ["id-overview", "id-surface", "id-atmosphere", "id-orbit", "id-missions", "id-quiz"];
	const factsBySection = {"id-overview": [{"title": "Earth Twin", "text": "Venus is similar in size to Earth."}, {"title": "Hottest Planet", "text": "It is the hottest planet in the solar system."}, {"title": "Bright in Sky", "text": "Venus is one of the brightest objects at night."}, {"title": "Rocky World", "text": "It has a solid rocky surface."}, {"title": "No Moons", "text": "Venus has no moons or rings."}], "id-surface": [{"title": "Volcanoes", "text": "The surface has many volcanoes."}, {"title": "Lava Plains", "text": "Large lava plains cover wide areas."}, {"title": "Mountains", "text": "High mountains and ridges rise up."}, {"title": "Craters", "text": "Impact craters dot the surface."}, {"title": "Hidden View", "text": "Thick clouds hide the surface from view."}], "id-atmosphere": [{"title": "Very Thick", "text": "The atmosphere is extremely thick."}, {"title": "Carbon Dioxide", "text": "CO2 makes up most of the air."}, {"title": "Acid Clouds", "text": "Clouds contain sulfuric acid."}, {"title": "High Pressure", "text": "Pressure is much higher than on Earth."}, {"title": "Greenhouse", "text": "Heat is trapped by a strong greenhouse effect."}], "id-orbit": [{"title": "Slow Spin", "text": "Venus rotates very slowly."}, {"title": "Backward Spin", "text": "It spins in the opposite direction of most planets."}, {"title": "Long Day", "text": "A day on Venus is longer than its year."}, {"title": "Near Sun", "text": "It is the second planet from the Sun."}, {"title": "Bright Dawn", "text": "It is often seen as the morning or evening star."}], "id-missions": [{"title": "Venera", "text": "Soviet landers sent surface data."}, {"title": "Magellan", "text": "Mapped the surface with radar."}, {"title": "Akatsuki", "text": "Studies Venus’s atmosphere today."}, {"title": "Radar Maps", "text": "We use radar to see through clouds."}, {"title": "Future", "text": "New missions are planned to return."}], "id-quiz": [{"title": "Quick Recall", "text": "Use the facts from each section."}, {"title": "Be Precise", "text": "Short answers should be clear."}, {"title": "Think First", "text": "Try to answer before guessing."}, {"title": "Challenge", "text": "Some answers need details."}, {"title": "You Got This", "text": "Check your score at the end."}]};
	let activeSection = 'id-overview';
	let activeFacts = factsBySection[activeSection];
	let quizAnswers = { q1: '', q2: [], q3: '', q4: '', q5: '' };
	let score = null;
	function setSection(id) { activeSection = id; }
	function submitQuiz() {
		const answerKey = { q1: 'hottest', q2: ["thick air", "acid clouds"], q3: 'magellan', q4: 'b', q5: 'true' };
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

<main class="venus-page">
	<section class="top">
		<div class="title">
			<p class="tag">Bright Twin</p>
			<h1>Venus</h1>
			<p class="subtitle">Hot, cloudy world with thick air.</p>
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
						class:active={activeSection === 'id-surface'}
						on:click={() => setSection('id-surface')}
					>
						Surface
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
						class:active={activeSection === 'id-orbit'}
						on:click={() => setSection('id-orbit')}
					>
						Orbit
					</button>
					<button
						type="button"
						class:active={activeSection === 'id-missions'}
						on:click={() => setSection('id-missions')}
					>
						Missions
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

	<section class="venus-layout">
		<div class="venus-core" aria-hidden="true">
			<div class="venus-sphere"></div>
			<div class="venus-halo"></div>
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
			<p>Venus is Earth’s size twin but far hotter.</p>
			<p>It shines brightly in our sky and has no moons.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-surface'} id="id-surface">
			<h2>Surface</h2>
			<p>Volcanoes and lava plains cover much of the surface.</p>
			<p>Radar images reveal mountains and impact craters.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-atmosphere'} id="id-atmosphere">
			<h2>Atmosphere</h2>
			<p>Venus has a thick CO2 atmosphere with acid clouds.</p>
			<p>The greenhouse effect traps heat and makes it scorching.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-orbit'} id="id-orbit">
			<h2>Orbit</h2>
			<p>Venus is the second planet from the Sun.</p>
			<p>It spins very slowly and in the opposite direction.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-missions'} id="id-missions">
			<h2>Missions</h2>
			<p>Magellan mapped the surface using radar.</p>
			<p>Venera landers sent data from the surface.</p>
		</article>
		<article class="panel" data-active={activeSection === 'id-quiz'} id="id-quiz">
			<h2>Mini Test</h2>
			<div class="quiz">
				<div class="question">
					<p>1. Venus is the ______ planet.</p>
					<input type="text" placeholder="One word" bind:value={quizAnswers.q1} />
				</div>
				<div class="question">
					<p>2. Multi-select: Which two describe Venus?</p>
					<label><input type="checkbox" value="thick air" bind:group={quizAnswers.q2} /> Thick atmosphere</label>
					<label><input type="checkbox" value="acid clouds" bind:group={quizAnswers.q2} /> Acid clouds</label>
					<label><input type="checkbox" value="many moons" bind:group={quizAnswers.q2} /> Many moons</label>
				</div>
				<div class="question">
					<p>3. Short answer: Name one Venus mission.</p>
					<input type="text" placeholder="Answer" bind:value={quizAnswers.q3} />
				</div>
				<div class="question">
					<p>4. Which statement is most accurate?</p>
					<label><input type="radio" name="q4" value="a" bind:group={quizAnswers.q4} /> Venus is a gas giant</label>
					<label><input type="radio" name="q4" value="b" bind:group={quizAnswers.q4} /> Venus has a rocky surface</label>
					<label><input type="radio" name="q4" value="c" bind:group={quizAnswers.q4} /> Venus has rings</label>
				</div>
				<div class="question">
					<p>5. True or False: Venus is similar in size to Earth.</p>
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
			radial-gradient(circle at 20% 12%, rgba(255, 200, 150, 0.25), transparent 45%),
			radial-gradient(circle at 80% 18%, rgba(255, 170, 120, 0.22), transparent 45%),
			radial-gradient(circle at 45% 90%, rgba(210, 140, 110, 0.2), transparent 45%),
			linear-gradient(160deg, #120b08 15%, #1a1210 55%, #100a10 100%);
		min-height: 100svh;
	}
	.venus-page { min-height: 100svh; padding: clamp(1.5rem, 4vw, 3rem); display: grid; gap: clamp(1.2rem, 2.4vw, 2.2rem); }
	.top { display: grid; grid-template-columns: minmax(0, 1fr) minmax(0, 320px); gap: 1.5rem; align-items: center; }
	.title h1 { margin: 0 0 0.6rem; font-family: "Unbounded", "Space Grotesk", system-ui, sans-serif; font-size: clamp(2.4rem, 4.5vw, 3.8rem); }
	.tag { margin: 0 0 0.6rem; letter-spacing: 0.28em; text-transform: uppercase; font-size: 0.8rem; color: rgba(255, 220, 170, 0.85); }
	.subtitle { margin: 0; color: rgba(246, 247, 255, 0.8); line-height: 1.5; }
	.jump { display: grid; gap: 0.5rem; }
	.jump button { border: 1px solid rgba(255, 255, 255, 0.12); background: rgba(255, 255, 255, 0.05); color: inherit; padding: 0.55rem 0.9rem; border-radius: 999px; font-size: 0.85rem; cursor: pointer; transition: transform 0.2s ease, box-shadow 0.2s ease; }
	.jump button.active { background: linear-gradient(120deg, #ffb27a, #ff7a5a); color: #0b0c18; border-color: transparent; box-shadow: 0 15px 30px rgba(255, 170, 120, 0.35); transform: translateY(-1px); }
	.venus-layout { position: relative; min-height: 320px; display: grid; place-items: center; }
	.venus-core { position: relative; width: min(240px, 40vw); aspect-ratio: 1; border-radius: 50%; display: grid; place-items: center; filter: drop-shadow(0 20px 50px rgba(255, 170, 120, 0.35)); }
	.venus-sphere { position: absolute; inset: 0; border-radius: 50%; background: radial-gradient(circle at 30% 30%, rgba(255, 235, 220, 0.9), transparent 40%), radial-gradient(circle at 70% 60%, rgba(255, 170, 120, 0.6), transparent 50%), radial-gradient(circle at 50% 50%, #f4caa2, #dd8a5c 60%, #a05135 100%); animation: slowspin 22s linear infinite; }
	.venus-halo { position: absolute; inset: -8%; border-radius: 50%; background: radial-gradient(circle, rgba(255, 170, 120, 0.35), transparent 70%); filter: blur(6px); animation: pulse 4s ease-in-out infinite; }
	.fact { position: absolute; width: min(220px, 40vw); background: rgba(20, 15, 14, 0.78); border: 1px solid rgba(255, 255, 255, 0.1); border-radius: 16px; padding: 0.8rem 1rem; box-shadow: 0 20px 40px rgba(0, 0, 0, 0.45); animation: float 4s ease-in-out infinite; }
	.fact h3 { margin: 0 0 0.3rem; font-size: 1rem; }
	.fact p { margin: 0; font-size: 0.9rem; color: rgba(246, 247, 255, 0.8); }
	.orbit-1 { top: 0; left: 4%; animation-delay: 0s; }
	.orbit-2 { top: 10%; right: 6%; animation-delay: 0.6s; }
	.orbit-3 { bottom: 10%; right: 4%; animation-delay: 1.2s; }
	.orbit-4 { bottom: 0; left: 10%; animation-delay: 1.8s; }
	.orbit-5 { top: 42%; left: -2%; animation-delay: 2.4s; }
	.panels { display: grid; grid-template-columns: minmax(0, 1fr); }
	.panel { display: none; background: rgba(20, 15, 14, 0.78); border-radius: 18px; padding: 1.3rem 1.6rem; border: 1px solid rgba(255, 255, 255, 0.1); box-shadow: 0 25px 50px rgba(0, 0, 0, 0.45); animation: fadeIn 0.35s ease; }
	.panel[data-active='true'] { display: block; }
	.panel h2 { margin: 0 0 0.6rem; }
	.panel p { color: rgba(246, 247, 255, 0.8); line-height: 1.6; }
	.quiz { display: grid; gap: 0.8rem; }
	.question { display: grid; gap: 0.35rem; font-size: 0.95rem; }
	.question label { display: flex; align-items: center; gap: 0.4rem; }
	.question input[type='text'] { border-radius: 10px; border: 1px solid rgba(255, 255, 255, 0.15); background: rgba(255, 255, 255, 0.06); color: inherit; padding: 0.35rem 0.6rem; }
	.submit { border: none; background: linear-gradient(120deg, #ffb27a, #ff7a5a); color: #0b0c18; padding: 0.6rem 1.2rem; border-radius: 999px; font-weight: 600; cursor: pointer; width: fit-content; }
	.score { margin: 0; font-weight: 600; color: rgba(200, 220, 255, 0.9); }
	@keyframes slowspin { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
	@keyframes pulse { 0%, 100% { transform: scale(1); opacity: 0.6; } 50% { transform: scale(1.08); opacity: 0.9; } }
	@keyframes float { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-8px); } }
	@keyframes fadeIn { from { opacity: 0; transform: translateY(6px); } to { opacity: 1; transform: translateY(0); } }
	@media (max-width: 900px) { .top { grid-template-columns: 1fr; } .jump { grid-template-columns: repeat(3, minmax(0, 1fr)); } .fact { display: none; } .venus-layout { min-height: 240px; } }
</style>
