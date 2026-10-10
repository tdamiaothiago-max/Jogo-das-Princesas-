<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Reino Silábico Encantado - Jogo Educativo de Sílabas</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;600;700&family=Quicksand:wght@500;700;800&display=swap" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.9.3/dist/confetti.browser.min.js"></script>
  <style>
    :root {
      --bg-gradient: linear-gradient(135deg, #fce7f3 0%, #f3e8ff 50%, #e0f2fe 100%);
      --pink-primary: #ec4899;
      --pink-dark: #db2777;
      --purple-primary: #a855f7;
      --amber-gold: #f59e0b;
      --emerald-green: #10b981;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      -webkit-tap-highlight-color: transparent;
      user-select: none;
    }

    body {
      font-family: 'Quicksand', sans-serif;
      background: var(--bg-gradient);
      height: 100vh;
      max-height: 100vh;
      width: 100vw;
      overflow: hidden;
      color: #334155;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      position: relative;
      padding: 6px 12px;
    }

    /* Ambient floating elements */
    .ambient-deco {
      position: fixed;
      pointer-events: none;
      z-index: 1;
      opacity: 0.25;
      animation: float 4s ease-in-out infinite;
    }
    @keyframes float {
      0%, 100% { transform: translateY(0px) rotate(0deg); }
      50% { transform: translateY(-10px) rotate(3deg); }
    }

    /* Top Bar */
    .top-bar {
      display: flex;
      align-items: center;
      justify-content: space-between;
      background: rgba(255, 255, 255, 0.85);
      backdrop-filter: blur(8px);
      border: 1px solid rgba(244, 114, 182, 0.4);
      border-radius: 16px;
      padding: 6px 14px;
      max-width: 1050px;
      width: 100%;
      margin: 0 auto;
      z-index: 10;
      flex-shrink: 0;
    }
    .top-brand {
      display: flex;
      align-items: center;
      gap: 6px;
      font-family: 'Fredoka', cursive;
      font-weight: 700;
      font-size: 1.15rem;
      color: #ec4899;
    }
    .top-actions {
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .score-badge {
      display: flex;
      align-items: center;
      gap: 5px;
      background: #fef3c7;
      border: 1.5px solid #f59e0b;
      padding: 3px 10px;
      border-radius: 12px;
      font-family: 'Fredoka', cursive;
      font-weight: 700;
      color: #b45309;
      font-size: 0.95rem;
    }
    .icon-btn {
      background: #fdf2f8;
      border: 1px solid #fbcfe8;
      border-radius: 12px;
      padding: 5px 10px;
      cursor: pointer;
      font-size: 0.85rem;
      font-weight: 700;
      color: #be185d;
      transition: all 0.15s;
    }
    .icon-btn:hover { background: #fce7f3; }
    .icon-btn:active { transform: scale(0.95); }

    /* Level Selector Bar */
    .level-bar {
      display: flex;
      gap: 8px;
      max-width: 1050px;
      width: 100%;
      margin: 4px auto;
      z-index: 10;
      flex-shrink: 0;
    }
    .level-btn {
      flex: 1;
      padding: 6px 10px;
      border-radius: 14px;
      border: 1.5px solid #fbcfe8;
      background: rgba(255, 255, 255, 0.9);
      cursor: pointer;
      font-family: 'Fredoka', cursive;
      font-weight: 700;
      font-size: 0.85rem;
      color: #475569;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 6px;
      transition: all 0.15s;
    }
    .level-btn.active.lvl1 {
      background: linear-gradient(135deg, #10b981, #059669);
      color: white;
      border-color: #059669;
      box-shadow: 0 3px 0 #047857;
    }
    .level-btn.active.lvl2 {
      background: linear-gradient(135deg, #a855f7, #ec4899);
      color: white;
      border-color: #9333ea;
      box-shadow: 0 3px 0 #7e22ce;
    }
    .level-btn.active.lvl3 {
      background: linear-gradient(135deg, #f59e0b, #ea580c);
      color: white;
      border-color: #d97706;
      box-shadow: 0 3px 0 #b45309;
    }

    /* Main Stage Card */
    .stage-wrapper {
      flex: 1;
      min-height: 0;
      display: flex;
      align-items: center;
      justify-content: center;
      max-width: 1050px;
      width: 100%;
      margin: 0 auto;
      z-index: 10;
      overflow: hidden;
    }
    .game-card {
      background: rgba(255, 255, 255, 0.96);
      backdrop-filter: blur(12px);
      border: 3px solid #fbcfe8;
      border-radius: 24px;
      padding: 12px 18px;
      box-shadow: 0 10px 25px -5px rgba(244, 114, 182, 0.3);
      width: 100%;
      height: 100%;
      max-height: 520px;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      overflow: hidden;
    }

    .card-nav {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding-bottom: 6px;
      border-bottom: 1px solid #fce7f3;
      flex-shrink: 0;
    }
    .nav-arrow {
      background: #fdf2f8;
      border: 1px solid #fbcfe8;
      border-radius: 10px;
      width: 32px;
      height: 32px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.1rem;
      color: #be185d;
      cursor: pointer;
      transition: all 0.15s;
    }
    .nav-arrow:hover { background: #fce7f3; }
    .nav-arrow:active { transform: scale(0.9); }
    .word-counter {
      font-family: 'Fredoka', cursive;
      font-size: 0.85rem;
      font-weight: 700;
      color: #9333ea;
      background: #f3e8ff;
      padding: 2px 10px;
      border-radius: 10px;
    }

    /* 2-Column Content Grid */
    .stage-grid {
      display: grid;
      grid-template-columns: 280px 1fr;
      gap: 16px;
      align-items: center;
      height: 100%;
      min-height: 0;
      padding: 4px 0;
    }
    @media (max-width: 768px) {
      .stage-grid {
        grid-template-columns: 1fr;
        grid-template-rows: auto 1fr;
        gap: 8px;
      }
    }

    /* Left Panel: Visual + Speech */
    .left-panel {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      background: linear-gradient(to bottom, #fdf2f8, #f5f3ff);
      border: 1.5px solid #fbcfe8;
      border-radius: 18px;
      padding: 10px;
      height: 100%;
      max-height: 420px;
    }
    .unit-mode-toggle {
      display: flex;
      width: 100%;
      gap: 4px;
      margin-bottom: 8px;
    }
    .mode-btn {
      flex: 1;
      padding: 4px;
      border-radius: 8px;
      border: 1px solid #fbcfe8;
      background: white;
      font-size: 0.72rem;
      font-weight: 700;
      color: #64748b;
      cursor: pointer;
      transition: all 0.15s;
    }
    .mode-btn.active {
      background: linear-gradient(to right, #ec4899, #a855f7);
      color: white;
      border-color: #ec4899;
    }

    .illustration-frame {
      width: 170px;
      height: 170px;
      background: linear-gradient(135deg, #f472b6, #c084fc, #fbbf24);
      padding: 5px;
      border-radius: 26px;
      box-shadow: 0 8px 24px rgba(236, 72, 153, 0.35);
      display: flex;
      align-items: center;
      justify-content: center;
      position: relative;
      cursor: pointer;
      margin-bottom: 8px;
      transition: transform 0.25s;
    }
    .illustration-frame:hover { transform: scale(1.04); }
    .illustration-frame:active { transform: scale(0.96); }
    .illustration-frame svg {
      width: 100%;
      height: 100%;
      border-radius: 22px;
    }
    .illustration-badge {
      position: absolute;
      bottom: 4px;
      right: 4px;
      background: rgba(255, 255, 255, 0.95);
      border: 1px solid #fbcfe8;
      border-radius: 50%;
      width: 26px;
      height: 26px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 0.85rem;
    }

    .listen-btn {
      background: linear-gradient(135deg, #ec4899 0%, #a855f7 100%);
      color: white;
      border: none;
      border-radius: 14px;
      padding: 7px 14px;
      font-family: 'Fredoka', cursive;
      font-size: 0.9rem;
      font-weight: 700;
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 6px;
      box-shadow: 0 3px 0 #be185d;
      transition: all 0.15s;
      width: 100%;
      max-width: 200px;
      justify-content: center;
    }
    .listen-btn:active { transform: translateY(2px); box-shadow: 0 1px 0 #be185d; }
    .word-hint {
      font-size: 0.75rem;
      color: #64748b;
      text-align: center;
      margin-top: 6px;
      line-height: 1.2;
    }

    /* Right Panel: Target Slots + Choice Options */
    .right-panel {
      display: flex;
      flex-direction: column;
      justify-content: center;
      gap: 12px;
      height: 100%;
    }

    .slots-box {
      background: linear-gradient(to right, rgba(253, 242, 248, 0.8), rgba(245, 243, 255, 0.8));
      border: 2px dashed #f472b6;
      border-radius: 18px;
      padding: 10px 14px;
      text-align: center;
    }
    .slots-title {
      font-family: 'Fredoka', cursive;
      font-size: 0.8rem;
      font-weight: 700;
      color: #ec4899;
      text-transform: uppercase;
      letter-spacing: 0.5px;
      margin-bottom: 6px;
    }
    .slots-grid {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 8px;
      min-height: 52px;
    }
    .slot-item {
      min-width: 60px;
      height: 52px;
      padding: 0 10px;
      border-radius: 14px;
      font-family: 'Fredoka', cursive;
      font-size: 1.6rem;
      font-weight: 700;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: all 0.2s;
    }
    .slot-item.empty {
      border: 2px dashed #f472b6;
      background: white;
      color: #f472b6;
      opacity: 0.5;
      font-size: 0.85rem;
    }
    .slot-item.missing-target {
      border: 2px dashed #f59e0b;
      background: #fef3c7;
      color: #d97706;
      font-size: 0.95rem;
      animation: pulse 1s infinite;
    }
    .slot-item.filled {
      background: linear-gradient(135deg, #ec4899, #a855f7);
      color: white;
      box-shadow: 0 4px 0 #be185d;
      cursor: pointer;
    }
    .slot-item.solved {
      background: linear-gradient(135deg, #10b981, #059669);
      color: white;
      box-shadow: 0 4px 0 #047857;
    }

    /* Choices Area */
    .choices-box {
      background: rgba(255, 255, 255, 0.7);
      border: 1px solid #f3e8ff;
      border-radius: 18px;
      padding: 10px 14px;
      text-align: center;
    }
    .choices-title {
      font-family: 'Fredoka', cursive;
      font-size: 0.8rem;
      font-weight: 700;
      color: #9333ea;
      text-transform: uppercase;
      letter-spacing: 0.5px;
      margin-bottom: 8px;
    }
    .choices-grid {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 10px;
    }
    .choice-cloud {
      background: white;
      border: 2px solid #f472b6;
      border-radius: 16px;
      padding: 8px 16px;
      font-family: 'Fredoka', cursive;
      font-size: 1.5rem;
      font-weight: 700;
      color: #db2777;
      cursor: pointer;
      box-shadow: 0 4px 0 #f472b6;
      transition: all 0.15s;
    }
    .choice-cloud:hover { background: #fdf2f8; transform: translateY(-2px); }
    .choice-cloud:active { transform: translateY(3px); box-shadow: 0 1px 0 #f472b6; }
    .choice-cloud.used {
      opacity: 0.2;
      pointer-events: none;
      transform: scale(0.9);
      box-shadow: none;
    }

    /* Feedback Banner */
    .feedback-banner {
      padding: 8px 14px;
      border-radius: 14px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
    }
    .feedback-banner.success {
      background: #ecfdf5;
      border: 2px solid #34d399;
      color: #065f46;
    }
    .feedback-banner.error {
      background: #fff1f2;
      border: 2px solid #fda4af;
      color: #9f1239;
    }
    .next-btn {
      background: linear-gradient(to right, #10b981, #059669);
      color: white;
      border: none;
      border-radius: 12px;
      padding: 6px 14px;
      font-family: 'Fredoka', cursive;
      font-size: 0.95rem;
      font-weight: 700;
      cursor: pointer;
      box-shadow: 0 3px 0 #047857;
      display: flex;
      align-items: center;
      gap: 4px;
    }

    /* Bottom Quick Selector Bar */
    .word-strip {
      max-width: 1050px;
      width: 100%;
      margin: 4px auto 0 auto;
      background: rgba(255, 255, 255, 0.85);
      border: 1px solid #fbcfe8;
      border-radius: 14px;
      padding: 3px 6px;
      display: flex;
      align-items: center;
      gap: 6px;
      overflow-x: auto;
      flex-shrink: 0;
      scrollbar-width: none;
    }
    .word-strip::-webkit-scrollbar { display: none; }
    .strip-chip {
      background: white;
      border: 1px solid #fbcfe8;
      border-radius: 8px;
      padding: 2px 8px;
      font-size: 0.75rem;
      font-weight: 700;
      color: #475569;
      cursor: pointer;
      white-space: nowrap;
      display: flex;
      align-items: center;
      gap: 4px;
      transition: all 0.15s;
    }
    .strip-chip.active {
      background: linear-gradient(to right, #ec4899, #a855f7);
      color: white;
      border-color: #ec4899;
      transform: scale(1.05);
    }
  </style>
</head>
<body>
  <!-- Ambient Decor -->
  <div class="ambient-deco" style="top: 15px; left: 15px; font-size: 2.5rem;">☁️</div>
  <div class="ambient-deco" style="top: 25px; right: 25px; font-size: 2.2rem;">✨</div>
  <div class="ambient-deco" style="bottom: 25px; left: 20px; font-size: 2.5rem;">🧚‍♀️</div>
  <div class="ambient-deco" style="bottom: 25px; right: 20px; font-size: 2.5rem;">🦄</div>

  <!-- Header -->
  <header class="top-bar">
    <div class="top-brand">
      <span>👑</span>
      <span>Reino Silábico Encantado</span>
    </div>
    <div class="top-actions">
      <div class="score-badge">
        <span>⭐</span>
        <span id="starsCount">0</span>
      </div>
      <button class="icon-btn" onclick="toggleSound()">
        <span id="soundIcon">🔊 Som</span>
      </button>
      <button class="icon-btn" onclick="speakPrincessMessage()">
        <span>👑 Princesa</span>
      </button>
    </div>
  </header>

  <!-- Level Selector -->
  <div class="level-bar">
    <button class="level-btn lvl1 active" onclick="switchLevel(1)">
      <span>🌸 Nível 1: Sílabas Simples</span>
    </button>
    <button class="level-btn lvl2" onclick="switchLevel(2)">
      <span>🦄 Nível 2: Sílabas Complexas</span>
    </button>
    <button class="level-btn lvl3" onclick="switchLevel(3)">
      <span>⭐ Nível 3: Complete a Sílaba</span>
    </button>
  </div>

  <!-- Main Stage Card -->
  <div class="stage-wrapper">
    <main class="game-card">
      <div class="card-nav">
        <button class="nav-arrow" onclick="prevWord()">❮</button>
        <span class="word-counter" id="wordCounter">Palavra 1 de 12</span>
        <button class="nav-arrow" onclick="nextWord()">❯</button>
      </div>

      <div class="stage-grid">
        <!-- Left Panel: Picture & Audio -->
        <div class="left-panel">
          <div class="unit-mode-toggle" id="unitModeToggle">
            <button class="mode-btn active" id="btnModeLetras" onclick="setUnitMode('letras')">🔤 Por Letras</button>
            <button class="mode-btn" id="btnModeSilabas" onclick="setUnitMode('silabas')">🧩 Por Sílabas</button>
          </div>

          <div class="illustration-frame" onclick="speakCurrentWord()" title="Toque para ouvir a palavra!">
            <div id="illustrationSvg" style="width:100%;height:100%;"></div>
            <div class="illustration-badge" id="cornerEmoji">🧚‍♀️</div>
          </div>

          <button class="listen-btn" onclick="speakCurrentWord()">
            <span>🔊</span>
            <span id="listenBtnLabel">Ouvir Palavra</span>
          </button>

          <p class="word-hint" id="wordHint">Dica mágica...</p>
        </div>

        <!-- Right Panel: Slots & Options -->
        <div class="right-panel">
          <div class="slots-box">
            <div class="slots-title" id="slotsTitle">Sua Palavra:</div>
            <div class="slots-grid" id="slotsContainer"></div>
          </div>

          <div class="choices-box">
            <div class="choices-title" id="choicesTitle">Toque para escolher:</div>
            <div class="choices-grid" id="choicesGrid"></div>
          </div>

          <!-- Feedback Banner -->
          <div id="feedbackBanner" class="feedback-banner" style="display: none;">
            <div id="feedbackMsg" style="font-weight: 700; font-size: 0.95rem;"></div>
            <button class="next-btn" id="feedbackNextBtn" onclick="nextWord()">
              <span>Próxima</span>
              <span>❯</span>
            </button>
          </div>
        </div>
      </div>
    </main>
  </div>

  <!-- Quick Word Strip Bar -->
  <div class="word-strip" id="wordStrip"></div>

  <script>
    let soundEnabled = true;
    let audioCtx = null;

    function getAudioContext() {
      if (!audioCtx && (window.AudioContext || window.webkitAudioContext)) {
        audioCtx = new (window.AudioContext || window.webkitAudioContext)();
      }
      if (audioCtx && audioCtx.state === 'suspended') audioCtx.resume();
      return audioCtx;
    }

    function playPop() {
      if (!soundEnabled) return;
      const ctx = getAudioContext();
      if (!ctx) return;
      const osc = ctx.createOscillator();
      const gain = ctx.createGain();
      osc.type = 'sine';
      osc.frequency.setValueAtTime(320, ctx.currentTime);
      osc.frequency.exponentialRampToValueAtTime(760, ctx.currentTime + 0.08);
      gain.gain.setValueAtTime(0.2, ctx.currentTime);
      gain.gain.exponentialRampToValueAtTime(0.01, ctx.currentTime + 0.09);
      osc.connect(gain); gain.connect(ctx.destination);
      osc.start(); osc.stop(ctx.currentTime + 0.1);
    }

    function playFanfare() {
      if (!soundEnabled) return;
      const ctx = getAudioContext();
      if (!ctx) return;
      const notes = [523.25, 659.25, 783.99, 1046.5];
      notes.forEach((f, i) => {
        const osc = ctx.createOscillator();
        const gain = ctx.createGain();
        osc.type = 'triangle';
        osc.frequency.setValueAtTime(f, ctx.currentTime + i * 0.07);
        gain.gain.setValueAtTime(0.2, ctx.currentTime + i * 0.07);
        gain.gain.exponentialRampToValueAtTime(0.001, ctx.currentTime + i * 0.07 + 0.4);
        osc.connect(gain); gain.connect(ctx.destination);
        osc.start(ctx.currentTime + i * 0.07);
        osc.stop(ctx.currentTime + i * 0.07 + 0.42);
      });
    }

    const PRAISES = [
      "Sensacional! Você conseguiu!",
      "Sua varinha mágica acertou em cheio!",
      "Uau, você é super inteligente!",
      "Que brilho incrível, você conseguiu!",
      "Maravilhoso! Os unicórnios estão dançando de alegria!",
      "Perfeito, estrelinha! Você é um encanto de sabedoria!"
    ];

    const ENCOURAGEMENTS = [
      "Quase lá! Tente mais uma vez.",
      "Não foi dessa vez, mas o unicórnio confia em você!",
      "Respira fundo, com calma a sua varinha mágica acerta!"
    ];

    function speakText(text) {
      if (!soundEnabled || !('speechSynthesis' in window)) return;
      window.speechSynthesis.cancel();
      const u = new SpeechSynthesisUtterance(text);
      u.lang = 'pt-BR';
      u.rate = 0.86;
      u.pitch = 1.28;
      window.speechSynthesis.speak(u);
    }

    function speakPraise() {
      speakText(PRAISES[Math.floor(Math.random() * PRAISES.length)]);
    }

    function speakEncouragement() {
      speakText(ENCOURAGEMENTS[Math.floor(Math.random() * ENCOURAGEMENTS.length)]);
    }

    function toggleSound() {
      soundEnabled = !soundEnabled;
      document.getElementById('soundIcon').innerText = soundEnabled ? '🔊 Som' : '🔇 Mudo';
    }

    function speakPrincessMessage() {
      speakText("Olá! Nosso reino mágico está repleto de letras brilhantes para você aprender!");
    }

    const SVG_MAP = {
      fada: '<svg viewBox="0 0 160 160"><circle cx="80" cy="80" r="70" fill="#FDF2F8"/><ellipse cx="48" cy="70" rx="30" ry="20" fill="#E0E7FF" opacity="0.85" transform="rotate(-25 48 70)"/><ellipse cx="112" cy="70" rx="30" ry="20" fill="#E0E7FF" opacity="0.85" transform="rotate(25 112 70)"/><path d="M68 85 L92 85 L106 130 L54 130 Z" fill="#EC4899"/><circle cx="80" cy="62" r="22" fill="#FED7AA"/><path d="M58 60 Q80 36 102 60 Q106 48 95 42 Q80 34 65 42 Z" fill="#F59E0B"/><circle cx="73" cy="63" r="3" fill="#374151"/><circle cx="87" cy="63" r="3" fill="#374151"/><path d="M75 71 Q80 76 85 71" stroke="#E11D48" stroke-width="2.5" fill="none"/><polygon points="72,44 80,38 88,44 85,47 75,47" fill="#FBBF24"/><line x1="94" y1="88" x2="128" y2="54" stroke="#FBBF24" stroke-width="3.5"/><polygon points="128,46 132,54 140,54 134,59 136,67 128,62 120,67 122,59 116,54 124,54" fill="#FDE047"/></svg>',
      coroa: '<svg viewBox="0 0 160 160"><circle cx="80" cy="80" r="70" fill="#FEF3C7"/><ellipse cx="80" cy="120" rx="52" ry="12" fill="#DB2777"/><path d="M36 108 L30 68 L54 84 L80 50 L106 84 L130 68 L124 108 Z" fill="#F59E0B"/><circle cx="30" cy="66" r="7" fill="#F43F5E"/><circle cx="54" cy="82" r="5" fill="#3B82F6"/><circle cx="80" cy="46" r="10" fill="#EC4899"/><circle cx="106" cy="82" r="5" fill="#3B82F6"/><circle cx="130" cy="66" r="7" fill="#F43F5E"/><rect x="44" y="96" width="12" height="8" rx="3" fill="#10B981"/><polygon points="80,88 88,98 80,104 72,98" fill="#EF4444"/><rect x="104" y="96" width="12" height="8" rx="3" fill="#10B981"/></svg>',
      castelo: '<svg viewBox="0 0 160 160"><circle cx="80" cy="80" r="70" fill="#EDE9FE"/><rect x="62" y="56" width="36" height="74" fill="#F472B6"/><polygon points="60,56 80,26 100,56" fill="#8B5CF6"/><line x1="80" y1="26" x2="80" y2="14" stroke="#4B5563" stroke-width="2"/><polygon points="80,14 96,19 80,24" fill="#EC4899"/><rect x="30" y="72" width="26" height="58" fill="#FBCFE8"/><polygon points="28,72 43,46 58,72" fill="#A78BFA"/><rect x="104" y="72" width="26" height="58" fill="#FBCFE8"/><polygon points="102,72 117,46 132,72" fill="#A78BFA"/><path d="M70 130 L70 106 Q80 96 90 106 L90 130 Z" fill="#7C2D12"/></svg>',
      doce: '<svg viewBox="0 0 160 160"><circle cx="80" cy="80" r="70" fill="#FFF1F2"/><line x1="80" y1="84" x2="80" y2="148" stroke="#E5E7EB" stroke-width="8" stroke-linecap="round"/><circle cx="80" cy="62" r="42" fill="#EC4899"/><circle cx="80" cy="62" r="34" fill="#FDE047"/><circle cx="80" cy="62" r="26" fill="#60A5FA"/><circle cx="80" cy="62" r="18" fill="#A78BFA"/><circle cx="80" cy="62" r="10" fill="#F43F5E"/></svg>',
      lua: '<svg viewBox="0 0 160 160"><circle cx="80" cy="80" r="70" fill="#1E1B4B"/><circle cx="36" cy="40" r="2.5" fill="#FDE047"/><circle cx="128" cy="120" r="3" fill="#FDE047"/><path d="M80 32 C48 32 32 60 32 94 C32 124 58 136 82 136 C68 124 62 102 62 86 C62 58 76 42 80 32 Z" fill="#FDE047"/><path d="M48 80 Q54 84 60 80" stroke="#78350F" stroke-width="2.5" fill="none"/><circle cx="48" cy="90" r="3" fill="#F43F5E" opacity="0.6"/><path d="M44 48 Q56 36 78 40 L70 54 Z" fill="#EC4899"/><circle cx="82" cy="38" r="6" fill="#FFFFFF"/></svg>',
      dado: '<svg viewBox="0 0 160 160"><circle cx="80" cy="80" r="70" fill="#FEF3C7"/><polygon points="80,34 122,54 80,74 38,54" fill="#F87171"/><polygon points="38,54 80,74 80,126 38,106" fill="#EF4444"/><polygon points="80,74 122,54 122,106 80,126" fill="#DC2626"/><circle cx="80" cy="54" r="5" fill="#FFFFFF"/><circle cx="52" cy="74" r="4.5" fill="#FFFFFF"/><circle cx="66" cy="87" r="4.5" fill="#FFFFFF"/><circle cx="94" cy="87" r="4.5" fill="#FFFFFF"/><circle cx="108" cy="98" r="4.5" fill="#FFFFFF"/></svg>',
      nuvem: '<svg viewBox="0 0 160 160"><circle cx="80" cy="80" r="70" fill="#E0F2FE"/><path d="M44 108 L116 108 C128 108 136 98 134 86 C132 74 120 68 112 70 C108 52 90 42 74 46 C62 49 52 60 52 72 C42 72 32 80 34 92 Z" fill="#FFFFFF"/><circle cx="68" cy="84" r="3" fill="#1E293B"/><circle cx="92" cy="84" r="3" fill="#1E293B"/><path d="M74 91 Q80 97 86 91" stroke="#E11D48" stroke-width="2.5" fill="none"/></svg>',
      sapo: '<svg viewBox="0 0 160 160"><circle cx="80" cy="80" r="70" fill="#DCFCE7"/><ellipse cx="80" cy="126" rx="58" ry="16" fill="#16A34A"/><ellipse cx="80" cy="96" rx="36" ry="28" fill="#4ADE80"/><circle cx="58" cy="64" r="16" fill="#4ADE80"/><circle cx="58" cy="64" r="10" fill="#FFFFFF"/><circle cx="58" cy="64" r="5" fill="#1E293B"/><circle cx="102" cy="64" r="16" fill="#4ADE80"/><circle cx="102" cy="64" r="10" fill="#FFFFFF"/><circle cx="102" cy="64" r="5" fill="#1E293B"/><polygon points="72,50 76,42 80,47 84,42 88,50" fill="#FBBF24"/><path d="M68 86 Q80 100 92 86" stroke="#15803D" stroke-width="3" fill="none"/></svg>',
      bolo: '<svg viewBox="0 0 160 160"><circle cx="80" cy="80" r="70" fill="#FDF2F8"/><ellipse cx="80" cy="132" rx="54" ry="10" fill="#E5E7EB"/><path d="M38 98 L38 124 Q80 134 122 124 L122 98 Z" fill="#F472B6"/><path d="M50 72 L50 94 Q80 102 110 94 L110 72 Z" fill="#EC4899"/><circle cx="62" cy="68" r="6" fill="#EF4444"/><circle cx="80" cy="70" r="6" fill="#EF4444"/><circle cx="98" cy="68" r="6" fill="#EF4444"/><rect x="78" y="44" width="4" height="22" fill="#60A5FA"/><path d="M80 34 Q85 40 80 44 Q75 40 80 34 Z" fill="#FBBF24"/></svg>',
      gato: '<svg viewBox="0 0 160 160"><circle cx="80" cy="80" r="70" fill="#FEF3C7"/><polygon points="50,70 42,34 70,54" fill="#F59E0B"/><polygon points="110,70 118,34 90,54" fill="#F59E0B"/><circle cx="80" cy="84" r="36" fill="#FBBF24"/><ellipse cx="68" cy="80" rx="6" ry="8" fill="#1E293B"/><ellipse cx="92" cy="80" rx="6" ry="8" fill="#1E293B"/><polygon points="77,88 83,88 80,92" fill="#EC4899"/><path d="M80 92 Q76 98 72 94 M80 92 Q84 98 88 94" stroke="#78350F" stroke-width="2" fill="none"/></svg>',
      bala: '<svg viewBox="0 0 160 160"><circle cx="80" cy="80" r="70" fill="#FFF1F2"/><polygon points="56,80 24,54 28,106" fill="#A855F7"/><polygon points="104,80 136,54 132,106" fill="#A855F7"/><ellipse cx="80" cy="80" rx="32" ry="24" fill="#EC4899"/><path d="M68 60 Q72 80 66 100" stroke="#FDE047" stroke-width="5" fill="none"/><path d="M80 56 Q84 80 80 104" stroke="#FFFFFF" stroke-width="5" fill="none"/></svg>',
      pato: '<svg viewBox="0 0 160 160"><circle cx="80" cy="80" r="70" fill="#E0F2FE"/><path d="M50 88 C40 88 38 104 46 114 C56 124 96 124 116 114 C126 104 126 94 116 88 Z" fill="#FBBF24"/><circle cx="98" cy="72" r="20" fill="#FBBF24"/><circle cx="104" cy="68" r="4" fill="#1E293B"/><path d="M116 70 L136 74 L116 80 Z" fill="#F97316"/></svg>',
      princesa: '<svg viewBox="0 0 160 160"><circle cx="80" cy="80" r="70" fill="#FDF2F8"/><circle cx="80" cy="72" r="32" fill="#92400E"/><path d="M54 104 L106 104 L122 144 L38 144 Z" fill="#EC4899"/><circle cx="80" cy="74" r="24" fill="#FED7AA"/><circle cx="72" cy="74" r="3.5" fill="#1E293B"/><circle cx="88" cy="74" r="3.5" fill="#1E293B"/><path d="M75 82 Q80 87 85 82" stroke="#E11D48" stroke-width="2.5" fill="none"/><polygon points="68,54 74,42 80,50 86,42 92,54" fill="#FBBF24"/></svg>',
      unicornio: '<svg viewBox="0 0 160 160"><circle cx="80" cy="80" r="70" fill="#F5F3FF"/><path d="M48 60 Q34 80 44 116" stroke="#F472B6" stroke-width="8" fill="none"/><path d="M56 54 Q44 76 52 114" stroke="#A78BFA" stroke-width="8" fill="none"/><path d="M68 56 L104 74 L126 96 L112 122 L86 116 L72 82 Z" fill="#FFFFFF"/><polygon points="86,52 124,18 96,44" fill="#FBBF24"/><circle cx="94" cy="78" r="4.5" fill="#4338CA"/></svg>',
      algodao: '<svg viewBox="0 0 160 160"><circle cx="80" cy="80" r="70" fill="#FDF2F8"/><polygon points="76,96 84,96 81,148 79,148" fill="#E5E7EB"/><ellipse cx="80" cy="64" rx="42" ry="34" fill="#F472B6"/><circle cx="56" cy="62" r="24" fill="#FBCFE8"/><circle cx="104" cy="62" r="24" fill="#FBCFE8"/><circle cx="70" cy="46" r="22" fill="#F472B6"/><circle cx="90" cy="46" r="22" fill="#FBCFE8"/></svg>',
      borboleta: '<svg viewBox="0 0 160 160"><circle cx="80" cy="80" r="70" fill="#FAF5FF"/><path d="M80 80 Q50 30 26 50 Q16 80 80 84 Z" fill="#EC4899"/><path d="M80 80 Q110 30 134 50 Q144 80 80 84 Z" fill="#EC4899"/><circle cx="44" cy="62" r="6" fill="#FDE047"/><circle cx="116" cy="62" r="6" fill="#FDE047"/><path d="M80 84 Q46 92 36 114 Q58 132 80 96 Z" fill="#A855F7"/><path d="M80 84 Q114 92 124 114 Q102 132 80 96 Z" fill="#A855F7"/><ellipse cx="80" cy="88" rx="5" ry="24" fill="#374151"/></svg>',
      estrela: '<svg viewBox="0 0 160 160"><circle cx="80" cy="80" r="70" fill="#1E1B4B"/><polygon points="80,24 95,64 138,64 103,90 116,132 80,106 44,132 57,90 22,64 65,64" fill="#FBBF24"/><circle cx="72" cy="78" r="3.5" fill="#78350F"/><circle cx="88" cy="78" r="3.5" fill="#78350F"/><path d="M76 86 Q80 90 84 86" stroke="#B45309" stroke-width="2.5" fill="none"/></svg>',
      chocolate: '<svg viewBox="0 0 160 160"><circle cx="80" cy="80" r="70" fill="#FEF3C7"/><polygon points="46,80 114,80 106,134 54,134" fill="#EC4899"/><rect x="52" y="38" width="56" height="54" rx="4" fill="#78350F"/><rect x="56" y="42" width="22" height="22" rx="3" fill="#92400E"/><rect x="82" y="42" width="22" height="22" rx="3" fill="#92400E"/><rect x="56" y="66" width="22" height="22" rx="3" fill="#92400E"/><rect x="82" y="66" width="22" height="22" rx="3" fill="#92400E"/></svg>'
    };

    const WORDS = [
      { id: 'fada', word: 'FADA', syllables: ['FA', 'DA'], emoji: '🧚‍♀️', level: 1, hint: 'Fadinha com asinhas brilhantes.' },
      { id: 'coroa', word: 'COROA', syllables: ['CO', 'RO', 'A'], emoji: '👑', level: 1, hint: 'Acessório dourado da realeza.' },
      { id: 'castelo', word: 'CASTELO', syllables: ['CAS', 'TE', 'LO'], emoji: '🏰', level: 1, hint: 'Palácio com torres altas.' },
      { id: 'doce', word: 'DOCE', syllables: ['DO', 'CE'], emoji: '🍭', level: 1, hint: 'Guloseima saborosa e docinha.' },
      { id: 'lua', word: 'LUA', syllables: ['LU', 'A'], emoji: '🌙', level: 1, hint: 'Ilumina o céu à noite.' },
      { id: 'dado', word: 'DADO', syllables: ['DA', 'DO'], emoji: '🎲', level: 1, hint: 'Cubinho numérico para jogar.' },
      { id: 'nuvem', word: 'NUVEM', syllables: ['NU', 'VEM'], emoji: '☁️', level: 1, hint: 'Flutua no céu azul.' },
      { id: 'sapo', word: 'SAPO', syllables: ['SA', 'PO'], emoji: '🐸', level: 1, hint: 'Adora pular na lagoa.' },
      { id: 'bolo', word: 'BOLO', syllables: ['BO', 'LO'], emoji: '🎂', level: 1, hint: 'Bolo de aniversário fofinho.' },
      { id: 'gato', word: 'GATO', syllables: ['GA', 'TO'], emoji: '🐱', level: 1, hint: 'Bichinho fofo que faz miau.' },
      { id: 'bala', word: 'BALA', syllables: ['BA', 'LA'], emoji: '🍬', level: 1, hint: 'Docinho colorido.' },
      { id: 'pato', word: 'PATO', syllables: ['PA', 'TO'], emoji: '🦆', level: 1, hint: 'Nada no laguinho e faz quá-quá.' },
      { id: 'princesa', word: 'PRINCESA', syllables: ['PRIN', 'CE', 'SA'], emoji: '👸', level: 2, hint: 'Vive em um lindo castelo.' },
      { id: 'unicornio', word: 'UNICÓRNIO', syllables: ['U', 'NI', 'CÓR', 'NIO'], emoji: '🦄', level: 2, hint: 'Cavalo com chifre mágico.' },
      { id: 'algodao', word: 'ALGODÃO', syllables: ['AL', 'GO', 'DÃO'], emoji: '☁️', level: 2, hint: 'Algodão doce cor-de-rosa.' },
      { id: 'borboleta', word: 'BORBOLETA', syllables: ['BOR', 'BO', 'LE', 'TA'], emoji: '🦋', level: 2, hint: 'Asas coloridas no jardim.' },
      { id: 'estrela', word: 'ESTRELA', syllables: ['ES', 'TRE', 'LA'], emoji: '⭐', level: 2, hint: 'Ponto brilhante no céu.' },
      { id: 'chocolate', word: 'CHOCOLATE', syllables: ['CHO', 'CO', 'LA', 'TE'], emoji: '🍫', level: 2, hint: 'Doce cremoso e irresistível.' }
    ];

    let currentLevel = parseInt(localStorage.getItem('reino_silabico_level') || '1', 10);
    let stars = parseInt(localStorage.getItem('reino_silabico_stars') || '0', 10);
    let currentWordIdx = 0;
    let unitMode = 'letras';
    let placedUnits = [];
    let missingIdx = 0;
    let missingSolved = false;

    function saveProgress() {
      localStorage.setItem('reino_silabico_level', currentLevel.toString());
      localStorage.setItem('reino_silabico_stars', stars.toString());
      document.getElementById('starsCount').innerText = stars;
    }

    function getActiveWords() {
      if (currentLevel === 1) return WORDS.filter(w => w.level === 1);
      if (currentLevel === 2) return WORDS.filter(w => w.level === 2);
      return WORDS;
    }

    function switchLevel(lvl) {
      currentLevel = lvl;
      currentWordIdx = 0;
      document.querySelectorAll('.level-btn').forEach((b, i) => {
        b.classList.toggle('active', i + 1 === lvl);
      });
      saveProgress();
      renderWordStrip();
      loadWord();
    }

    function setUnitMode(mode) {
      unitMode = mode;
      document.getElementById('btnModeLetras').classList.toggle('active', mode === 'letras');
      document.getElementById('btnModeSilabas').classList.toggle('active', mode === 'silabas');
      loadWord();
    }

    function triggerConfetti() {
      if (typeof confetti === 'function') {
        confetti({ particleCount: 70, spread: 70, origin: { y: 0.6 } });
      }
    }

    function loadWord() {
      const activeWords = getActiveWords();
      if (currentWordIdx >= activeWords.length) currentWordIdx = 0;
      const word = activeWords[currentWordIdx];

      placedUnits = [];
      missingSolved = false;
      document.getElementById('feedbackBanner').style.display = 'none';

      document.getElementById('wordCounter').innerText = 'Palavra ' + (currentWordIdx + 1) + ' de ' + activeWords.length;
      document.getElementById('wordHint').innerText = word.hint;

      const svgContainer = document.getElementById('illustrationSvg');
      svgContainer.innerHTML = SVG_MAP[word.id] || '<div style="font-size:4rem;display:flex;align-items:center;justify-content:center;height:100%">' + word.emoji + '</div>';
      document.getElementById('cornerEmoji').innerText = word.emoji;

      document.getElementById('unitModeToggle').style.display = currentLevel === 3 ? 'none' : 'flex';

      if (currentLevel === 3) {
        setupLevel3(word);
      } else {
        setupAssemble(word);
      }

      highlightActiveStripChip();
    }

    function setupAssemble(word) {
      const targetUnits = unitMode === 'letras' ? word.word.split('') : word.syllables;
      document.getElementById('slotsTitle').innerText = 'Sua Palavra (' + (unitMode === 'letras' ? 'Letras' : 'Sílabas') + '):';
      document.getElementById('choicesTitle').innerText = unitMode === 'letras' ? 'Toque nas Letrinhas:' : 'Toque nas Nuvens:';

      renderAssembleSlots(targetUnits);
      renderAssembleChoices(targetUnits);
    }

    function renderAssembleSlots(targetUnits) {
      const container = document.getElementById('slotsContainer');
      container.innerHTML = '';

      targetUnits.forEach((expected, idx) => {
        const slot = document.createElement('div');
        const filled = placedUnits[idx];
        if (filled) {
          slot.className = 'slot-item filled';
          slot.innerText = filled;
          slot.onclick = () => removePlacedUnit(idx);
        } else {
          slot.className = 'slot-item empty';
          slot.innerText = (idx + 1) + 'º';
        }
        container.appendChild(slot);
      });
    }

    function renderAssembleChoices(targetUnits) {
      const container = document.getElementById('choicesGrid');
      container.innerHTML = '';

      const shuffled = [...targetUnits].sort(() => Math.random() - 0.5);
      shuffled.forEach((text) => {
        const btn = document.createElement('button');
        btn.className = 'choice-cloud';
        btn.innerText = unitMode === 'letras' ? text : '☁️ ' + text;
        btn.onclick = () => {
          playPop();
          placedUnits.push(text);
          btn.classList.add('used');
          renderAssembleSlots(targetUnits);
          checkAssembleAnswer(targetUnits);
        };
        container.appendChild(btn);
      });
    }

    function removePlacedUnit(idx) {
      playPop();
      placedUnits.splice(idx, 1);
      const word = getActiveWords()[currentWordIdx];
      const targetUnits = unitMode === 'letras' ? word.word.split('') : word.syllables;
      renderAssembleSlots(targetUnits);
      renderAssembleChoices(targetUnits);
    }

    function checkAssembleAnswer(targetUnits) {
      if (placedUnits.length < targetUnits.length) return;
      const word = getActiveWords()[currentWordIdx];
      const expected = targetUnits.join('');
      const answer = placedUnits.join('');

      if (answer === expected) {
        stars += 10;
        saveProgress();
        playFanfare();
        triggerConfetti();
        speakPraise();

        const banner = document.getElementById('feedbackBanner');
        banner.className = 'feedback-banner success';
        document.getElementById('feedbackMsg').innerText = '✨ Sensacional! Você acertou ' + word.word + '! (+10 ⭐)';
        banner.style.display = 'flex';
      } else {
        playPop();
        speakEncouragement();
        const banner = document.getElementById('feedbackBanner');
        banner.className = 'feedback-banner error';
        document.getElementById('feedbackMsg').innerText = 'Quase lá! Tente montar mais uma vez!';
        banner.style.display = 'flex';
      }
    }

    function setupLevel3(word) {
      document.getElementById('slotsTitle').innerText = 'Complete a Sílaba Que Falta:';
      document.getElementById('choicesTitle').innerText = 'Escolha a Sílaba Mágica:';

      missingIdx = word.syllables.length > 2 ? 1 : word.syllables.length - 1;
      const correctSyllable = word.syllables[missingIdx];

      const container = document.getElementById('slotsContainer');
      container.innerHTML = '';

      word.syllables.forEach((s, idx) => {
        const slot = document.createElement('div');
        if (idx === missingIdx) {
          slot.className = missingSolved ? 'slot-item solved' : 'slot-item missing-target';
          slot.innerText = missingSolved ? s : '❓';
        } else {
          slot.className = 'slot-item filled';
          slot.innerText = s;
        }
        container.appendChild(slot);
      });

      const distractors = ['BA', 'CA', 'DA', 'LA', 'MA', 'PA', 'TA', 'RA'].filter(s => s !== correctSyllable);
      const pool = [correctSyllable, ...distractors.slice(0, 3)].sort(() => Math.random() - 0.5);

      const choicesGrid = document.getElementById('choicesGrid');
      choicesGrid.innerHTML = '';

      pool.forEach(syllable => {
        const btn = document.createElement('button');
        btn.className = 'choice-cloud';
        btn.innerText = '☁️ ' + syllable;
        btn.onclick = () => {
          if (missingSolved) return;
          playPop();
          if (syllable === correctSyllable) {
            missingSolved = true;
            stars += 15;
            saveProgress();
            playFanfare();
            triggerConfetti();
            speakPraise();

            setupLevel3(word);
            const banner = document.getElementById('feedbackBanner');
            banner.className = 'feedback-banner success';
            document.getElementById('feedbackMsg').innerText = '🎉 Perfeito! Você completou ' + word.word + '! (+15 ⭐)';
            banner.style.display = 'flex';
          } else {
            speakEncouragement();
            btn.classList.add('used');
          }
        };
        choicesGrid.appendChild(btn);
      });
    }

    function speakCurrentWord() {
      const word = getActiveWords()[currentWordIdx];
      if (currentLevel === 3) {
        speakText('Qual sílaba completa a palavra ' + word.word + '?');
      } else {
        speakText(word.word);
      }
    }

    function nextWord() {
      playPop();
      const activeWords = getActiveWords();
      currentWordIdx = (currentWordIdx + 1) % activeWords.length;
      loadWord();
    }

    function prevWord() {
      playPop();
      const activeWords = getActiveWords();
      currentWordIdx = (currentWordIdx - 1 + activeWords.length) % activeWords.length;
      loadWord();
    }

    function renderWordStrip() {
      const strip = document.getElementById('wordStrip');
      strip.innerHTML = '';
      const activeWords = getActiveWords();
      activeWords.forEach((w, idx) => {
        const chip = document.createElement('button');
        chip.className = 'strip-chip' + (idx === currentWordIdx ? ' active' : '');
        chip.innerHTML = '<span>' + w.emoji + '</span><span>' + w.word + '</span>';
        chip.onclick = () => {
          playPop();
          currentWordIdx = idx;
          loadWord();
        };
        strip.appendChild(chip);
      });
    }

    function highlightActiveStripChip() {
      document.querySelectorAll('.strip-chip').forEach((c, i) => {
        c.classList.toggle('active', i === currentWordIdx);
      });
    }

    window.addEventListener('DOMContentLoaded', () => {
      saveProgress();
      switchLevel(currentLevel);
    });
  </script>
</body>
</html>
