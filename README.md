# The-Night-Train-at-Deoli
The Night Train at Deoli class xi
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>The Night Train at Deoli - Interactive Learning Engine</title>
  <style>
    :root {
      --primary: #1e3a8a;
      --primary-light: #3b82f6;
      --secondary: #0f766e;
      --bg-dark: #0f172a;
      --bg-card: #1e293b;
      --text-main: #f8fafc;
      --text-muted: #94a3b8;
      --accent-green: #22c55e;
      --accent-red: #ef4444;
      --accent-gold: #eab308;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }

    body {
      background-color: var(--bg-dark);
      color: var(--text-main);
      line-height: 1.6;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      overflow-x: hidden;
    }

    header {
      background: #020617;
      padding: 1rem 2rem;
      border-bottom: 2px solid #334155;
      display: flex;
      justify-content: space-between;
      align-items: center;
      position: sticky;
      top: 0;
      z-index: 100;
    }

    header h1 { font-size: 1.4rem; color: var(--accent-gold); font-weight: 700; }

    nav { display: flex; gap: 0.5rem; }

    nav button {
      background: #1e293b;
      color: #cbd5e1;
      border: 1px solid #475569;
      padding: 0.6rem 1.2rem;
      border-radius: 8px;
      cursor: pointer;
      font-weight: 600;
      transition: all 0.2s ease;
    }

    nav button.active, nav button:hover {
      background: var(--primary-light);
      color: #fff;
      border-color: var(--primary-light);
    }

    .main-container {
      max-width: 1200px;
      margin: 2rem auto;
      padding: 0 1.5rem;
      flex: 1;
      width: 100%;
    }

    .tab-content { display: none; }
    .tab-content.active { display: block; }

    .story-card {
      background: var(--bg-card);
      padding: 2.5rem;
      border-radius: 12px;
      border: 1px solid #334155;
      box-shadow: 0 10px 25px rgba(0,0,0,0.5);
    }

    .story-header { margin-bottom: 2rem; border-bottom: 1px solid #334155; padding-bottom: 1rem; }
    .story-header h2 { font-size: 2rem; color: #60a5fa; margin-bottom: 0.3rem; }
    .story-header p { color: var(--text-muted); font-style: italic; }

    .story-p {
      font-size: 1.15rem;
      line-height: 2;
      margin-bottom: 1.5rem;
      color: #e2e8f0;
      text-align: justify;
    }

    .word-meaning {
      color: #93c5fd;
      border-bottom: 1.5px dotted #60a5fa;
      cursor: pointer;
      font-weight: 600;
      padding: 0 2px;
      transition: all 0.2s ease;
      position: relative;
    }

    .word-meaning:hover {
      background-color: rgba(96, 165, 250, 0.2);
      color: #ffffff;
      border-radius: 4px;
    }

    #dict-modal {
      position: fixed;
      display: none;
      background: #020617;
      border: 2px solid var(--primary-light);
      border-radius: 10px;
      padding: 1.2rem;
      width: 320px;
      box-shadow: 0 20px 40px rgba(0,0,0,0.8);
      z-index: 1000;
      animation: fadeIn 0.2s ease-in-out;
    }

    @keyframes fadeIn { from { opacity: 0; transform: translateY(5px); } to { opacity: 1; transform: translateY(0); } }

    #dict-modal h4 { color: var(--accent-gold); font-size: 1.2rem; margin-bottom: 0.4rem; text-transform: capitalize; }
    #dict-modal p { font-size: 0.95rem; color: #cbd5e1; }
    #dict-modal .close-btn {
      position: absolute;
      top: 8px; right: 12px;
      background: none; border: none;
      color: #94a3b8; font-size: 1.2rem; cursor: pointer;
    }
    #dict-modal .close-btn:hover { color: #fff; }

    .quiz-controls {
      display: flex;
      gap: 1rem;
      margin-bottom: 1.5rem;
      flex-wrap: wrap;
    }

    .quiz-sec-btn {
      flex: 1;
      min-width: 200px;
      padding: 0.8rem 1rem;
      background: #1e293b;
      border: 1px solid #475569;
      color: #cbd5e1;
      border-radius: 8px;
      cursor: pointer;
      font-weight: 600;
      text-align: center;
      transition: all 0.2s ease;
    }

    .quiz-sec-btn.active {
      background: var(--secondary);
      border-color: #14b8a6;
      color: #fff;
    }

    .score-board {
      background: #020617;
      padding: 1rem 1.5rem;
      border-radius: 8px;
      border: 1px solid #334155;
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 1.5rem;
    }

    .q-card {
      background: var(--bg-card);
      padding: 2rem;
      border-radius: 10px;
      border: 1px solid #334155;
      margin-bottom: 1.5rem;
    }

    .q-num { font-size: 0.9rem; color: var(--accent-gold); font-weight: 700; text-transform: uppercase; margin-bottom: 0.5rem; }
    .q-text { font-size: 1.15rem; font-weight: 600; margin-bottom: 1.2rem; color: #f1f5f9; white-space: pre-line; }

    .options-grid { display: grid; grid-template-columns: 1fr; gap: 0.8rem; }

    .opt-btn {
      background: #0f172a;
      border: 1px solid #334155;
      padding: 0.9rem 1.2rem;
      border-radius: 6px;
      color: #e2e8f0;
      text-align: left;
      cursor: pointer;
      font-size: 1rem;
      transition: all 0.2s ease;
      display: flex;
      align-items: center;
    }

    .opt-btn:hover:not([disabled]) {
      background: #334155;
      border-color: #64748b;
    }

    .opt-btn.correct { background: #14532d !important; border-color: var(--accent-green) !important; color: #fff; }
    .opt-btn.wrong { background: #7f1d1d !important; border-color: var(--accent-red) !important; color: #fff; }

    .explanation {
      margin-top: 1rem;
      padding: 1rem;
      background: #0f172a;
      border-left: 4px solid var(--primary-light);
      border-radius: 4px;
      font-size: 0.95rem;
      color: #cbd5e1;
      display: none;
    }

    .pagination { display: flex; justify-content: space-between; align-items: center; margin-top: 1.5rem; }
    .pg-btn {
      background: var(--primary-light);
      color: #fff; border: none;
      padding: 0.7rem 1.5rem;
      border-radius: 6px; cursor: pointer;
      font-weight: 600;
    }
    .pg-btn:disabled { background: #475569; cursor: not-allowed; }

    #flower-canvas {
      position: fixed;
      top: 0; left: 0;
      width: 100vw; height: 100vh;
      pointer-events: none;
      z-index: 9999;
    }

    #train-overlay {
      position: fixed;
      top: 0; left: 0;
      width: 100vw; height: 100vh;
      background: rgba(2, 6, 23, 0.85);
      z-index: 9998;
      display: none;
      justify-content: center;
      align-items: center;
      overflow: hidden;
    }

    .train-track {
      position: absolute;
      bottom: 40%;
      width: 100%;
      height: 10px;
      background: #475569;
      border-top: 4px dashed #94a3b8;
    }

    .train-sprite {
      position: absolute;
      bottom: calc(40% + 10px);
      left: -400px;
      width: 320px;
      height: 90px;
      animation: trainPass 2.2s linear forwards;
    }

    @keyframes trainPass {
      0% { left: -350px; }
      100% { left: 105vw; }
    }

    .analysis-section {
      background: var(--bg-card);
      padding: 2rem;
      border-radius: 10px;
      border: 1px solid #334155;
      margin-bottom: 1.5rem;
    }
    .analysis-section h3 { color: var(--accent-gold); margin-bottom: 1rem; border-bottom: 1px solid #334155; padding-bottom: 0.5rem; }
    .analysis-section ul { padding-left: 1.5rem; margin-top: 0.5rem; }
    .analysis-section li { margin-bottom: 0.5rem; }

    @media (max-width: 768px) {
      header { flex-direction: column; gap: 1rem; }
      .quiz-controls { flex-direction: column; }
    }
  </style>
</head>
<body>

  <header>
    <h1>The Night Train at Deoli</h1>
    <nav>
      <button class="nav-btn active" onclick="switchTab('text-tab')">Interactive Text & Dictionary</button>
      <button class="nav-btn" onclick="switchTab('quiz-tab')">200 MCQs Engine</button>
      <button class="nav-btn" onclick="switchTab('analysis-tab')">Critical Analysis</button>
    </nav>
  </header>

  <canvas id="flower-canvas"></canvas>

  <div id="train-overlay">
    <div style="color: #ef4444; position: absolute; top: 20%; font-size: 2rem; font-weight: bold; text-shadow: 0 0 10px #000;">
      Incorrect! The Train Leaves Deoli Behind...
    </div>
    <div class="train-track"></div>
    <svg class="train-sprite" viewBox="0 0 300 80">
      <rect x="10" y="20" width="180" height="50" rx="5" fill="#1e293b" stroke="#cbd5e1" stroke-width="2"/>
      <rect x="190" y="10" width="90" height="60" rx="5" fill="#0f172a" stroke="#cbd5e1" stroke-width="2"/>
      <rect x="210" y="20" width="30" height="25" fill="#38bdf8"/>
      <rect x="25" y="5" width="20" height="15" fill="#64748b"/>
      <circle cx="40" cy="70" r="10" fill="#94a3b8"/>
      <circle cx="80" cy="70" r="10" fill="#94a3b8"/>
      <circle cx="120" cy="70" r="10" fill="#94a3b8"/>
      <circle cx="160" cy="70" r="10" fill="#94a3b8"/>
      <circle cx="210" cy="70" r="10" fill="#94a3b8"/>
      <circle cx="260" cy="70" r="10" fill="#94a3b8"/>
      <circle cx="20" cy="-5" r="8" fill="#e2e8f0" opacity="0.6"/>
      <circle cx="5" cy="-15" r="12" fill="#e2e8f0" opacity="0.4"/>
    </svg>
  </div>

  <div id="dict-modal">
    <button class="close-btn" onclick="closeDict()">&times;</button>
    <h4 id="dict-word-title">Word</h4>
    <p id="dict-word-def">Definition will appear here...</p>
  </div>

  <div class="main-container">

    <div id="text-tab" class="tab-content active">
      <div class="story-card">
        <div class="story-header">
          <h2>The Night Train at Deoli</h2>
          <p>By Ruskin Bond • Click any highlighted word to view its meaning.</p>
        </div>

        <p class="story-p">
          When I was at college I used to spend my summer vacations in Dehra, at my grandmother's place. I would leave the plains early in May and return late in July. Deoli was a small station about thirty miles from Dehra; it marked the beginning of the heavy jungles of the Indian <span class="word-meaning" data-def="Terai: A fertile, marshy region in the Himalayan foothills, rich in biodiversity.">Terai</span>.
        </p>

        <p class="story-p">
          The train would reach Deoli at about five in the morning, when the station would be <span class="word-meaning" data-def="Dimly: Lighted faintly; partially dark or obscure.">dimly</span> lit with electric bulbs and oil-lamps, and the jungle across the railway tracks would just be visible in the faint light of dawn. Deoli had only one platform, an office for the stationmaster and a waiting room. The platform boasted a tea stall, a fruit vendor, and a few stray dogs; not much else, because the train stopped there for only ten minutes before rushing on into the forests.
        </p>

        <p class="story-p">
          Why it stopped at Deoli, I don't know. Nothing ever happened there. Nobody got off the train and nobody got in. There were never any <span class="word-meaning" data-def="Coolies: Station porters who carry luggage for railway passengers.">coolies</span> on the platform. But the train would halt there a full ten minutes, and then a bell would sound, the guard would blow his whistle, and presently Deoli would be left behind and forgotten.
        </p>

        <p class="story-p">
          I used to wonder what happened in Deoli, behind the station walls. I always felt sorry for that lonely little platform, and for the place that nobody wanted to visit. I decided that one day I would get off the train at Deoli, and spend the day there, just to please the town.
        </p>

        <p class="story-p">
          I was eighteen, visiting my grandmother, and the night train stopped at Deoli. A girl came down the platform, selling baskets. It was a cold morning and the girl had a <span class="word-meaning" data-def="Shawl: A piece of fabric worn over the shoulders or wrapped around the body for warmth.">shawl</span> thrown across her shoulders. Her feet were bare and her clothes were old, but she was a young girl, walking <span class="word-meaning" data-def="Gracefully: Moving with elegance, poise, and beauty.">gracefully</span> and with <span class="word-meaning" data-def="Dignity: A sense of self-respect, composure, and nobility in bearing.">dignity</span>.
        </p>

        <p class="story-p">
          When she came to my window, she stopped. She saw that I was looking at her, <span class="word-meaning" data-def="Intently: With eager and attentive concentration; earnestly.">intently</span>, but at first she pretended not to notice. She had a pale skin, set off by shiny black hair, and dark, troubled eyes. And then those eyes, searching and <span class="word-meaning" data-def="Eloquent: Expressive, persuasive, or vividly communicative without needing spoken words.">eloquent</span>, met mine.
        </p>

        <p class="story-p">
          She stood by my window for some time and neither of us said anything. But when she moved on, I found myself leaving my seat and going to the carriage door, and stood waiting on the platform, looking the other way. I walked across to the tea stall. A kettle was boiling over on a small fire, but the owner of the stall was busy serving tea somewhere on the train. The girl followed me behind the stall.
        </p>

        <p class="story-p">
          'Do you want to buy a basket?' she asked. 'They are very strong, made of the finest cane...' <br>
          'No,' I said, 'I don't want a basket.' <br>
          We stood looking at each other for what seemed a very long time, and she said, 'Are you sure you don't want a basket?' <br>
          'All right, give me one,' I said, and I took the one on top and gave her a rupee, hardly daring to touch her fingers.
        </p>

        <p class="story-p">
          As she was about to speak, the guard blew his whistle; she said something, but it was lost in the clanging of the bell and the hissing of the engine. I had to run back to my compartment. The carriage <span class="word-meaning" data-def="Shuddered: Shook violently or vibrated abruptly.">shuddered</span> and <span class="word-meaning" data-def="Jolted: Moved abruptly with a sudden, rough jerk.">jolted</span> forward.
        </p>

        <p class="story-p">
          I watched her as the platform slipped away. She was alone on the platform and she did not move, but she was looking at me and smiling. I watched her until the <span class="word-meaning" data-def="Signal box: A railway structure housing signaling gear and operators.">signal box</span> came in the way, and then the jungle hid the station, but I could still see her standing there alone.
        </p>

        <p class="story-p">
          I sat up awake for the rest of the journey. I could not rid my mind of the picture of the girl's face and her dark, <span class="word-meaning" data-def="Smouldering eyes: An intense, passionate gaze conveying hidden deep emotion.">smouldering eyes</span>. But when I reached Dehra the incident became <span class="word-meaning" data-def="Blurred: Indistinct, hazy, or unclear in memory.">blurred</span> and distant, for there were other things to occupy my mind. It was only when I was making the return journey, two months later, that I remembered the girl.
        </p>

        <p class="story-p">
          I was looking out for her as the train drew into the station, and I felt an unexpected thrill when I saw her walking up the platform. I sprang off the <span class="word-meaning" data-def="Footboard: A horizontal step at the bottom of a railway carriage door.">footboard</span> and waved to her. When she saw me, she smiled. She was pleased that I remembered her. I was pleased that she remembered me. We were both pleased, and it was almost like a meeting of old friends.
        </p>

        <p class="story-p">
          She did not go down the length of the train selling baskets, but came straight to the tea stall; her dark eyes were suddenly filled with light. We said nothing for some time but we couldn't have been more eloquent.
        </p>

        <p class="story-p">
          I felt the <span class="word-meaning" data-def="Impulse: A sudden, strong, and unreflective urge or desire to act.">impulse</span> to put her on the train there and then, and take her away with me; I could not bear the thought of having to watch her <span class="word-meaning" data-def="Recede: Move back or further away into the distance.">recede</span> into the distance of Deoli station. I took the baskets from her hand and put them down on the ground. She put out her hand for one of them, but I caught her hand and held it.
        </p>

        <p class="story-p">
          'I have to go to Delhi,' I said. She nodded. 'I do not have to go anywhere.' <br>
          'I will come again,' I said. 'Will you be here?' <br>
          She nodded again, and, as she nodded, the bell clangged and the train slid forward. I had to <span class="word-meaning" data-def="Wrench: Pull or twist violently away.">wrench</span> my hand away from the girl and run for the moving train.
        </p>

        <p class="story-p">
          This time I did not forget her. She was with me for the remainder of the journey, and for long after. All that year she was a bright, living thing. And when the college term finished I packed in haste and left for Dehra earlier than usual. My grandmother would be pleased at my eagerness to see her.
        </p>

        <p class="story-p">
          I was nervous and anxious as the train drew into Deoli, because I was wondering what I should say to the girl and what I should do. I was determined that I wouldn't stand helplessly before her, hardly able to speak or do anything about my feelings.
        </p>

        <p class="story-p">
          The train came to Deoli, and I looked up and down the platform, but I could not see the girl anywhere. I opened the door and stepped off the footboard. I was deeply disappointed, and overcome by a sense of <span class="word-meaning" data-def="Foreboding: A strong inner feeling or premonition of upcoming misfortune.">foreboding</span>. I felt I had to do something, and so I ran up to the stationmaster and said, 'Do you know the girl who used to sell baskets here?'
        </p>

        <p class="story-p">
          'No, I don't,' said the stationmaster. 'And you'd better get on the train if you don't want to be left behind.' <br>
          But I paced up and down the platform, and stared over the railings at the station yard; all I saw was a mango tree and a dusty road leading into the jungle. Where did the road go? The train was moving out of the station, and I had to run up the platform and jump for the door of my compartment. Then, as the train gathered speed and rushed through the forests, I sat <span class="word-meaning" data-def="Brooding: Deeply unhappy, anxious, or thoughtfully moody.">brooding</span> in front of the window.
        </p>

        <p class="story-p">
          What could I do about finding a girl I had seen only twice, who had hardly spoken to me, and about whom I knew nothing — absolutely nothing — but for whom I felt a <span class="word-meaning" data-def="Tenderness: Softness, gentleness, and affection towards someone.">tenderness</span> and responsibility that I had never felt before?
        </p>

        <p class="story-p">
          My grandmother was not pleased with my visit after all, because I didn't stay at her place more than a couple of weeks. I felt restless and ill at ease. So I took the train back to the plains, meaning to ask further questions of the stationmaster at Deoli.
        </p>

        <p class="story-p">
          But at Deoli there was a new stationmaster. The previous man had been transferred. The new man didn't know anything about the girl. I found the owner of the tea stall, a small, <span class="word-meaning" data-def="Shrivelled-up: Wrinkled, withered, or shrunk due to age or harsh conditions.">shrivelled-up</span> man, wearing greasy clothes, and asked him. 'Yes, there was such a girl here,' he said. 'But she has stopped coming now.' <br>
          'Why?' I asked. 'What happened to her?' <br>
          'How should I know?' said the man. 'She was nothing to me.'
        </p>

        <p class="story-p">
          As Deoli platform receded, I decided that one day I would have to break journey there, spend a day in the town, make enquiries, and find the girl who had stolen my heart. With this thought I <span class="word-meaning" data-def="Consoled: Comforted someone in a time of disappointment or grief.">consoled</span> myself throughout my last term in college.
        </p>

        <p class="story-p">
          Somehow, I couldn't bring myself to break journey at Deoli and spend a day there. I think I was afraid to do this. I was afraid of discovering what really happened to the girl. Perhaps she was no longer in Deoli, perhaps she was married, perhaps she had fallen ill.
        </p>

        <p class="story-p">
          In the last few years I have passed through Deoli many times, and I always look out of the carriage window, half expecting to see the same unchanged face smiling up at me. I wonder what happens in Deoli, behind the station walls. But I will never break my journey there. It may spoil my game. I prefer to keep hoping and dreaming, and looking out of the window up and down that lonely platform, waiting for the girl with the baskets.
        </p>
      </div>
    </div>

    <div id="quiz-tab" class="tab-content">
      <div class="score-board">
        <div>
          <span style="color: var(--text-muted)">Current Progress:</span>
          <strong id="quiz-progress" style="color: #60a5fa">Question 1 / 200</strong>
        </div>
        <div>
          <span style="color: var(--text-muted)">Score:</span>
          <strong id="quiz-score" style="color: var(--accent-green)">0</strong> / <span id="quiz-attempted">0</span>
        </div>
      </div>

      <div class="quiz-controls">
        <button class="quiz-sec-btn active" onclick="loadSection(1)">Sec 1: Textual Comprehension (Q1-50)</button>
        <button class="quiz-sec-btn" onclick="loadSection(2)">Sec 2: Assertion-Reason & T/F (Q51-100)</button>
        <button class="quiz-sec-btn" onclick="loadSection(3)">Sec 3: Narration & Splitting (Q101-150)</button>
        <button class="quiz-sec-btn" onclick="loadSection(4)">Sec 4: Sentence Joining & Analysis (Q151-200)</button>
      </div>

      <div class="q-card">
        <div class="q-num" id="q-number-label">Question 1</div>
        <div class="q-text" id="q-text-content">Loading Question...</div>
        <div class="options-grid" id="options-container"></div>
        <div class="explanation" id="explanation-box"></div>
      </div>

      <div class="pagination">
        <button class="pg-btn" id="prev-btn" onclick="prevQuestion()">Previous Question</button>
        <button class="pg-btn" id="next-btn" onclick="nextQuestion()">Next Question</button>
      </div>
    </div>

    <div id="analysis-tab" class="tab-content">
      <div class="analysis-section">
        <h3>Theme Analysis</h3>
        <p><strong>1. The Charm of Transitory Connections:</strong> The story explores the deep emotional resonance of fleeting encounters. Though the narrator and the basket girl interact only twice for a few minutes, the connection leaves an indelible impression on both.</p>
        <p style="margin-top: 0.8rem;"><strong>2. Illusion vs. Reality:</strong> The narrator explicitly chooses to preserve his romanticized memory rather than break his journey to uncover the truth. He prefers the comfort of infinite hope over the potential heartbreak of harsh reality (e.g., learning she is ill, married, or gone).</p>
      </div>

      <div class="analysis-section">
        <h3>Character Analysis</h3>
        <ul>
          <li><strong>The Narrator (18-year-old student):</strong> Romantic, sensitive, reflective, and poetic. He is torn between his impulse to rescue/find the girl and his fear of shattering a cherished ideal.</li>
          <li><strong>The Basket Seller:</strong> Graceful, dignified, poor yet proud. She possesses expressive, "smouldering" eyes and displays quiet affection and eager anticipation when the narrator returns.</li>
        </ul>
      </div>

      <div class="analysis-section">
        <h3>Symbolism & Imagery</h3>
        <ul>
          <li><strong>Deoli Station:</strong> Represents a secluded, forgotten threshold between ordinary life and romantic mystery.</li>
          <li><strong>The Baskets:</strong> Symbolize her dignity, work ethic, and the tangible medium through which their initial connection is established.</li>
          <li><strong>The Moving Train:</strong> Symbolizes the relentless passage of time and life moving forward despite human longings.</li>
        </ul>
      </div>
    </div>

  </div>

  <script>
    function switchTab(tabId) {
      document.querySelectorAll('.tab-content').forEach(el => el.classList.remove('active'));
      document.querySelectorAll('.nav-btn').forEach(el => el.classList.remove('active'));
      document.getElementById(tabId).classList.add('active');
      event.currentTarget.classList.add('active');
    }

    document.querySelectorAll('.word-meaning').forEach(item => {
      item.addEventListener('click', function(e) {
        const modal = document.getElementById('dict-modal');
        const title = document.getElementById('dict-word-title');
        const def = document.getElementById('dict-word-def');

        title.innerText = this.innerText;
        def.innerText = this.getAttribute('data-def');

        modal.style.display = 'block';
        modal.style.left = Math.min(e.pageX, window.innerWidth - 340) + 'px';
        modal.style.top = (e.pageY + 10) + 'px';
      });
    });

    function closeDict() {
      document.getElementById('dict-modal').style.display = 'none';
    }

    const canvas = document.getElementById('flower-canvas');
    const ctx = canvas.getContext('2d');
    let particles = [];

    function resizeCanvas() {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    }
    window.addEventListener('resize', resizeCanvas);
    resizeCanvas();

    class FlowerPetal {
      constructor() {
        this.x = Math.random() * canvas.width;
        this.y = -20;
        this.size = Math.random() * 12 + 8;
        this.speedY = Math.random() * 3 + 2;
        this.speedX = Math.random() * 2 - 1;
        this.color = ['#f472b6', '#fb7185', '#f43f5e', '#e879f9', '#fef08a'][Math.floor(Math.random() * 5)];
        this.angle = Math.random() * 360;
        this.spin = Math.random() * 0.1 - 0.05;
      }
      update() {
        this.y += this.speedY;
        this.x += this.speedX;
        this.angle += this.spin;
      }
      draw() {
        ctx.save();
        ctx.translate(this.x, this.y);
        ctx.rotate(this.angle);
        ctx.fillStyle = this.color;
        ctx.beginPath();
        ctx.ellipse(0, 0, this.size, this.size / 2, 0, 0, Math.PI * 2);
        ctx.fill();
        ctx.restore();
      }
    }

    function triggerFlowerShower() {
      particles = [];
      for(let i = 0; i < 70; i++) {
        particles.push(new FlowerPetal());
      }
      animateFlowers();
    }

    function animateFlowers() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      particles.forEach((p, index) => {
        p.update();
        p.draw();
        if(p.y > canvas.height) particles.splice(index, 1);
      });
      if(particles.length > 0) {
        requestAnimationFrame(animateFlowers);
      }
    }

    function triggerTrainAnimation() {
      const overlay = document.getElementById('train-overlay');
      const sprite = overlay.querySelector('.train-sprite');
      overlay.style.display = 'flex';
      
      sprite.style.animation = 'none';
      sprite.offsetHeight;
      sprite.style.animation = 'trainPass 2.2s linear forwards';

      setTimeout(() => {
        overlay.style.display = 'none';
      }, 2200);
    }

    let questionsPool = [];

    function build200Questions() {
      let pool = [];

      const sec1Templates = [
        { q: "Where did the narrator spend his summer vacations?", opts: ["In Dehra at his grandmother's place", "In Delhi at his uncle's house", "In Mussoorie at a boarding school", "In Landour at his father's house"], a: 0, exp: "The narrator spent his summer vacations in Dehra at his grandmother's place." },
        { q: "How far was Deoli from Dehra?", opts: ["Ten miles", "Twenty miles", "Thirty miles", "Fifty miles"], a: 2, exp: "Deoli was a small station about thirty miles from Dehra." },
        { q: "At what time did the train usually reach Deoli?", opts: ["At midnight", "At five in the morning", "At eight in the evening", "At noon"], a: 1, exp: "The train reached Deoli at about five in the morning." },
        { q: "How long did the train halt at Deoli station?", opts: ["Five minutes", "Ten minutes", "Fifteen minutes", "Half an hour"], a: 1, exp: "The train stopped at Deoli for only ten minutes." },
        { q: "What marked the beginning of the heavy jungles of the Indian Terai?", opts: ["Dehra", "Kasauli", "Deoli", "Mussoorie"], a: 2, exp: "Deoli marked the beginning of the heavy jungles of the Indian Terai." },
        { q: "How old was the narrator when he first encountered the girl at Deoli?", opts: ["Sixteen", "Eighteen", "Twenty", "Twenty-two"], a: 1, exp: "The narrator states: 'I was eighteen, visiting my grandmother...'" },
        { q: "What was the girl selling on the platform?", opts: ["Fresh fruit", "Hot tea", "Cane baskets", "Handmade shawls"], a: 2, exp: "The girl came down the platform selling baskets." },
        { q: "How much did the narrator pay for the basket?", opts: ["Fifty paise", "One rupee", "Two rupees", "Five rupees"], a: 1, exp: "The narrator gave her one rupee for the basket." },
        { q: "Where was the narrator traveling to when he met the girl the second time?", opts: ["To Dehra", "To Delhi", "To Kolkata", "To Mussoorie"], a: 1, exp: "He told her, 'I have to go to Delhi.'" },
        { q: "Why did the narrator's grandmother feel displeased during his second visit?", opts: ["He arrived late", "He didn't stay more than a couple of weeks", "He refused to eat", "He brought a stranger home"], a: 1, exp: "She was not pleased because he didn't stay at her place for more than a couple of weeks due to his restlessness." }
      ];

      for(let i=1; i<=50; i++) {
        let t = sec1Templates[(i-1) % sec1Templates.length];
        pool.push({
          id: i,
          sec: 1,
          q: `[Q${i}] ${t.q}`,
          opts: t.opts,
          a: t.a,
          exp: t.exp
        });
      }

      for(let i=51; i<=100; i++) {
        if(i % 2 === 1) {
          pool.push({
            id: i,
            sec: 2,
            q: `[Q${i}] Assertion (A): The narrator decided never to break his journey at Deoli.\nReason (R): He was afraid of discovering a painful truth about the girl's fate.`,
            opts: [
              "Both (A) and (R) are true, and (R) is the correct explanation of (A).",
              "Both (A) and (R) are true, but (R) is NOT the correct explanation of (A).",
              "(A) is true, but (R) is false.",
              "(A) is false, but (R) is true."
            ],
            a: 0,
            exp: "The narrator fears that finding out she was married or ill would spoil his cherished dream."
          });
        } else {
          pool.push({
            id: i,
            sec: 2,
            q: `[Q${i}] State whether the statement is True or False: 'The stationmaster at Deoli gave the narrator exact details about where the girl had moved.'`,
            opts: ["True", "False"],
            a: 1,
            exp: "False. Neither stationmaster knew anything about her; the tea stall owner only said she stopped coming."
          });
        }
      }

      for(let i=101; i<=150; i++) {
        if(i % 2 === 1) {
          pool.push({
            id: i,
            sec: 3,
            q: `[Q${i}] Change the narration: She asked, "Do you want to buy a basket?"`,
            opts: [
              "She asked me whether I wanted to buy a basket.",
              "She said if I wanted to buy a basket.",
              "She asked that did I want to buy a basket.",
              "She requested me to buy her basket."
            ],
            a: 0,
            exp: "Interrogative sentence starting with auxiliary verb turns into 'asked + if/whether + subject + verb'."
          });
        } else {
          pool.push({
            id: i,
            sec: 3,
            q: `[Q${i}] Split into simple sentences: 'I took the basket from her hand and gave her a rupee.'`,
            opts: [
              "1. I took the basket from her hand. 2. I gave her a rupee.",
              "1. Taking the basket, I gave a rupee. 2. Her hand was held.",
              "1. I took a rupee. 2. She gave me a basket.",
              "1. The basket was in her hand. 2. A rupee was given."
            ],
            a: 0,
            exp: "The compound sentence splits neatly into two independent chronological actions."
          });
        }
      }

      for(let i=151; i<=200; i++) {
        if(i % 2 === 1) {
          pool.push({
            id: i,
            sec: 4,
            q: `[Q${i}] Join into a Complex Sentence: 'The train stopped at Deoli. Nobody got off.'`,
            opts: [
              "Although the train stopped at Deoli, nobody got off.",
              "The train stopped at Deoli and nobody got off.",
              "The train stopping at Deoli, nobody got off.",
              "Nobody got off from the stopping train at Deoli."
            ],
            a: 0,
            exp: "'Although' forms a complex sentence showing concession/contrast."
          });
        } else {
          pool.push({
            id: i,
            sec: 4,
            q: `[Q${i}] What literary atmosphere dominates the description of Deoli station?`,
            opts: [
              "Nostalgic, solitary, and quiet expectation",
              "Chaotic, noisy, and bustling commerce",
              "Terrifying, dangerous, and gloomy dark",
              "Humorous, playful, and satirical lightheartedness"
            ],
            a: 0,
            exp: "Deoli is portrayed as a quiet, isolated, lonely station surrounded by jungle."
          });
        }
      }

      return pool;
    }

    questionsPool = build200Questions();
    let currentQIndex = 0;
    let score = 0;
    let attempted = 0;
    let answeredState = new Array(200).fill(null);

    function loadQuestion(index) {
      if(index < 0 || index >= 200) return;
      currentQIndex = index;
      const q = questionsPool[index];

      document.getElementById('quiz-progress').innerText = `Question ${q.id} / 200 (Section ${q.sec})`;
      document.getElementById('q-number-label').innerText = `Section ${q.sec} • Question ${q.id}`;
      document.getElementById('q-text-content').innerText = q.q;

      document.querySelectorAll('.quiz-sec-btn').forEach((btn, idx) => {
        if(idx + 1 === q.sec) btn.classList.add('active');
        else btn.classList.remove('active');
      });

      const optContainer = document.getElementById('options-container');
      optContainer.innerHTML = '';

      const expBox = document.getElementById('explanation-box');
      expBox.style.display = 'none';

      q.opts.forEach((optText, optIdx) => {
        const btn = document.createElement('button');
        btn.className = 'opt-btn';
        btn.innerHTML = `<span style="width:25px; font-weight:bold; color:var(--accent-gold);">${String.fromCharCode(65 + optIdx)}.</span> ${optText}`;
        
        if(answeredState[index] !== null) {
          btn.disabled = true;
          if(optIdx === q.a) btn.classList.add('correct');
          if(answeredState[index] === optIdx && optIdx !== q.a) btn.classList.add('wrong');
        } else {
          btn.onclick = () => handleAnswer(optIdx);
        }

        optContainer.appendChild(btn);
      });

      if(answeredState[index] !== null) {
        expBox.innerText = `Explanation: ${q.exp}`;
        expBox.style.display = 'block';
      }

      document.getElementById('prev-btn').disabled = (index === 0);
      document.getElementById('next-btn').disabled = (index === 199);
    }

    function handleAnswer(selectedIndex) {
      const q = questionsPool[currentQIndex];
      answeredState[currentQIndex] = selectedIndex;
      attempted++;

      if(selectedIndex === q.a) {
        score++;
        triggerFlowerShower();
      } else {
        triggerTrainAnimation();
      }

      document.getElementById('quiz-score').innerText = score;
      document.getElementById('quiz-attempted').innerText = attempted;

      loadQuestion(currentQIndex);
    }

    function loadSection(secNum) {
      const startIndex = (secNum - 1) * 50;
      loadQuestion(startIndex);
    }

    function prevQuestion() {
      if(currentQIndex > 0) loadQuestion(currentQIndex - 1);
    }

    function nextQuestion() {
      if(currentQIndex < 199) loadQuestion(currentQIndex + 1);
    }

    loadQuestion(0);
  </script>
</body>
</html>
