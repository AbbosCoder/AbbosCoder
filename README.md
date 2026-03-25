<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Abbosbek — Python Full-Stack Developer</title>
<link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@300;400;500;600;700&family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #050a0f;
    --surface: #0d1821;
    --card: #111d2b;
    --border: #1a3a52;
    --neon: #00e5ff;
    --neon2: #00ff88;
    --neon3: #7c3aed;
    --text: #e0f4ff;
    --muted: #5a8aa0;
    --gold: #ffd700;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Syne', sans-serif;
    overflow-x: hidden;
    min-height: 100vh;
  }

  /* ── PARTICLE CANVAS ── */
  #particles {
    position: fixed; top: 0; left: 0;
    width: 100%; height: 100%;
    pointer-events: none; z-index: 0;
  }

  /* ── GRID LINES ── */
  .grid-bg {
    position: fixed; inset: 0; z-index: 0;
    background-image:
      linear-gradient(rgba(0,229,255,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,229,255,0.03) 1px, transparent 1px);
    background-size: 60px 60px;
    animation: gridMove 20s linear infinite;
  }
  @keyframes gridMove {
    from { background-position: 0 0; }
    to   { background-position: 60px 60px; }
  }

  /* ── MAIN CONTAINER ── */
  .container {
    position: relative; z-index: 1;
    max-width: 900px; margin: 0 auto;
    padding: 60px 24px;
  }

  /* ── HERO ── */
  .hero {
    text-align: center;
    margin-bottom: 80px;
    animation: fadeUp .8s ease both;
  }

  .avatar-ring {
    width: 120px; height: 120px;
    margin: 0 auto 28px;
    border-radius: 50%;
    position: relative;
  }
  .avatar-ring::before {
    content: '';
    position: absolute; inset: -4px;
    border-radius: 50%;
    background: conic-gradient(var(--neon), var(--neon2), var(--neon3), var(--neon));
    animation: spinRing 3s linear infinite;
  }
  @keyframes spinRing {
    to { transform: rotate(360deg); }
  }
  .avatar-inner {
    position: relative; z-index: 1;
    width: 100%; height: 100%;
    border-radius: 50%;
    background: var(--surface);
    display: flex; align-items: center; justify-content: center;
    font-size: 3rem;
    border: 3px solid var(--bg);
  }

  .status-dot {
    width: 14px; height: 14px;
    border-radius: 50%;
    background: var(--neon2);
    position: absolute; bottom: 8px; right: 8px;
    border: 2px solid var(--bg);
    box-shadow: 0 0 8px var(--neon2);
    animation: pulse 1.8s ease-in-out infinite;
    z-index: 2;
  }
  @keyframes pulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50%       { opacity: .5; transform: scale(1.3); }
  }

  .hero-name {
    font-size: clamp(2.2rem, 6vw, 3.8rem);
    font-weight: 800;
    letter-spacing: -1px;
    background: linear-gradient(135deg, var(--neon) 0%, var(--neon2) 60%, var(--gold) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    margin-bottom: 8px;
  }

  .hero-tagline {
    font-family: 'Fira Code', monospace;
    font-size: 1rem;
    color: var(--neon);
    margin-bottom: 18px;
    letter-spacing: 1px;
  }

  /* typing cursor */
  .typed-cursor { animation: blink .7s step-end infinite; }
  @keyframes blink { 50% { opacity: 0; } }

  .hero-desc {
    color: var(--muted);
    font-size: .95rem;
    max-width: 500px;
    margin: 0 auto 30px;
    line-height: 1.7;
  }

  /* ── SECTION TITLES ── */
  .section-title {
    font-size: 1.3rem;
    font-weight: 700;
    color: var(--neon);
    letter-spacing: 2px;
    text-transform: uppercase;
    margin-bottom: 28px;
    display: flex; align-items: center; gap: 12px;
  }
  .section-title::after {
    content: '';
    flex: 1;
    height: 1px;
    background: linear-gradient(to right, var(--border), transparent);
  }

  /* ── GLITCH BADGE ── */
  .glitch-badge {
    display: inline-block;
    font-family: 'Fira Code', monospace;
    font-size: .75rem;
    padding: 5px 14px;
    border-radius: 30px;
    border: 1px solid;
    margin: 4px;
    transition: all .25s;
    cursor: default;
    position: relative;
    overflow: hidden;
  }
  .glitch-badge::before {
    content: '';
    position: absolute; inset: 0;
    background: currentColor;
    opacity: 0;
    transition: opacity .25s;
  }
  .glitch-badge:hover::before { opacity: .1; }
  .glitch-badge:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 20px currentColor;
  }
  .badge-cyan  { color: var(--neon);  border-color: var(--neon); }
  .badge-green { color: var(--neon2); border-color: var(--neon2); }
  .badge-purple{ color: #a78bfa;      border-color: #a78bfa; }
  .badge-gold  { color: var(--gold);  border-color: var(--gold); }

  /* ── SKILL GRID ── */
  .skills-section { margin-bottom: 70px; }

  .skills-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
  }
  @media(max-width: 600px) { .skills-grid { grid-template-columns: 1fr; } }

  .skill-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 24px;
    position: relative;
    overflow: hidden;
    transition: transform .3s, border-color .3s, box-shadow .3s;
    animation: fadeUp .8s ease both;
  }
  .skill-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(to right, var(--neon), var(--neon2));
    transform: scaleX(0);
    transform-origin: left;
    transition: transform .4s;
  }
  .skill-card:hover::before { transform: scaleX(1); }
  .skill-card:hover {
    transform: translateY(-4px);
    border-color: var(--neon);
    box-shadow: 0 10px 40px rgba(0,229,255,.12);
  }

  .skill-card-title {
    font-size: .7rem;
    font-weight: 700;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 16px;
  }

  .skill-bar-wrap { margin: 10px 0; }
  .skill-bar-label {
    display: flex; justify-content: space-between;
    font-family: 'Fira Code', monospace;
    font-size: .78rem;
    color: var(--text);
    margin-bottom: 5px;
  }
  .skill-bar-track {
    height: 5px;
    background: rgba(255,255,255,.06);
    border-radius: 10px;
    overflow: hidden;
  }
  .skill-bar-fill {
    height: 100%;
    border-radius: 10px;
    width: 0;
    transition: width 1.4s cubic-bezier(.16,1,.3,1);
  }
  .fill-cyan   { background: linear-gradient(to right, var(--neon2), var(--neon)); }
  .fill-purple { background: linear-gradient(to right, #7c3aed, #a78bfa); }

  /* ── SERVICES ── */
  .services-section { margin-bottom: 70px; }

  .services-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
    gap: 18px;
  }

  .service-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 22px 20px;
    display: flex; gap: 14px; align-items: flex-start;
    transition: all .3s;
    animation: fadeUp .8s ease both;
  }
  .service-card:hover {
    border-color: var(--neon2);
    box-shadow: 0 0 30px rgba(0,255,136,.08);
    transform: translateY(-3px);
  }

  .service-icon {
    font-size: 1.6rem;
    flex-shrink: 0;
    filter: drop-shadow(0 0 6px currentColor);
  }
  .service-card h3 { font-size: .9rem; font-weight: 700; margin-bottom: 4px; color: var(--text); }
  .service-card p  { font-size: .8rem; color: var(--muted); line-height: 1.5; }

  /* ── STATS ── */
  .stats-section { margin-bottom: 70px; }
  .stats-row {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
    gap: 16px;
  }
  .stat-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 22px;
    text-align: center;
    transition: all .3s;
    animation: fadeUp .8s ease both;
  }
  .stat-card:hover {
    border-color: var(--neon);
    box-shadow: 0 0 24px rgba(0,229,255,.15);
    transform: scale(1.03);
  }
  .stat-num {
    font-size: 2rem;
    font-weight: 800;
    background: linear-gradient(135deg, var(--neon), var(--neon2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }
  .stat-label {
    font-family: 'Fira Code', monospace;
    font-size: .7rem;
    color: var(--muted);
    margin-top: 4px;
    letter-spacing: 1px;
  }

  /* ── SOCIAL ── */
  .social-section { margin-bottom: 60px; }
  .social-links {
    display: flex; flex-wrap: wrap; gap: 12px;
    justify-content: center;
  }
  .social-btn {
    display: inline-flex; align-items: center; gap: 8px;
    padding: 10px 20px;
    border-radius: 50px;
    text-decoration: none;
    font-family: 'Fira Code', monospace;
    font-size: .8rem;
    font-weight: 600;
    letter-spacing: .5px;
    border: 1px solid;
    transition: all .3s;
    position: relative;
    overflow: hidden;
  }
  .social-btn::before {
    content: '';
    position: absolute; inset: 0;
    background: currentColor;
    opacity: 0;
    transition: opacity .3s;
  }
  .social-btn:hover::before { opacity: .12; }
  .social-btn:hover { transform: translateY(-2px); }

  .btn-github  { color: #fff;      border-color: #333; box-shadow: 0 0 0 rgba(255,255,255,0); }
  .btn-github:hover  { box-shadow: 0 4px 20px rgba(255,255,255,.2); }
  .btn-linkedin{ color: #0ea5e9;   border-color: #0ea5e9; }
  .btn-linkedin:hover{ box-shadow: 0 4px 20px rgba(14,165,233,.4); }
  .btn-youtube { color: #ef4444;   border-color: #ef4444; }
  .btn-youtube:hover { box-shadow: 0 4px 20px rgba(239,68,68,.4); }
  .btn-instagram{ color: #ec4899; border-color: #ec4899; }
  .btn-instagram:hover{ box-shadow: 0 4px 20px rgba(236,72,153,.4); }
  .btn-telegram{ color: var(--neon); border-color: var(--neon); }
  .btn-telegram:hover{ box-shadow: 0 4px 20px rgba(0,229,255,.4); }

  /* ── GITHUB STATS CARDS ── */
  .github-section { margin-bottom: 70px; }
  .github-cards {
    display: flex; flex-wrap: wrap; gap: 16px; justify-content: center;
  }
  .github-card-img {
    border-radius: 12px;
    max-width: 100%;
    height: auto;
    transition: transform .3s, box-shadow .3s;
    border: 1px solid var(--border);
  }
  .github-card-img:hover {
    transform: scale(1.02);
    box-shadow: 0 8px 32px rgba(0,229,255,.2);
  }

  /* ── FOOTER ── */
  .footer {
    text-align: center;
    font-family: 'Fira Code', monospace;
    font-size: .75rem;
    color: var(--muted);
    padding: 20px;
    border-top: 1px solid var(--border);
  }
  .footer span { color: var(--neon2); }

  /* ── ANIMATIONS ── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(28px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  .delay-1 { animation-delay: .1s; }
  .delay-2 { animation-delay: .2s; }
  .delay-3 { animation-delay: .3s; }
  .delay-4 { animation-delay: .4s; }
  .delay-5 { animation-delay: .5s; }

  /* ── SCAN LINE ── */
  .scanline {
    position: fixed; inset: 0; z-index: 0; pointer-events: none;
    background: repeating-linear-gradient(
      to bottom,
      transparent 0, transparent 3px,
      rgba(0,229,255,.01) 3px, rgba(0,229,255,.01) 4px
    );
  }

  /* ── GLOW ORBS ── */
  .orb {
    position: fixed;
    border-radius: 50%;
    filter: blur(90px);
    pointer-events: none;
    z-index: 0;
    animation: floatOrb 12s ease-in-out infinite alternate;
  }
  .orb-1 { width:380px; height:380px; background:rgba(0,229,255,.07); top:-80px; right:-80px; }
  .orb-2 { width:300px; height:300px; background:rgba(0,255,136,.05); bottom:-60px; left:-60px; animation-duration:15s; }
  .orb-3 { width:200px; height:200px; background:rgba(124,58,237,.07); top:40%; left:50%; animation-duration:18s; }

  @keyframes floatOrb {
    from { transform: translate(0,0) scale(1); }
    to   { transform: translate(40px, 30px) scale(1.1); }
  }

  /* ── TERMINAL TYPING ── */
  .terminal-box {
    background: #050d14;
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 20px 24px;
    font-family: 'Fira Code', monospace;
    font-size: .85rem;
    margin-bottom: 32px;
    position: relative;
    overflow: hidden;
  }
  .terminal-box::before {
    content: '';
    position: absolute; top:0; left:0; right:0;
    height: 32px;
    background: rgba(255,255,255,.03);
    border-bottom: 1px solid var(--border);
  }
  .term-dots {
    position: absolute;
    top: 10px; left: 16px;
    display: flex; gap: 6px;
  }
  .dot { width:10px; height:10px; border-radius:50%; }
  .dot-r { background:#ff5f57; }
  .dot-y { background:#febc2e; }
  .dot-g { background:#28c840; }
  .term-body { margin-top: 28px; }
  .term-line { margin: 4px 0; }
  .term-prompt { color: var(--neon2); margin-right: 8px; }
  .term-cmd { color: var(--neon); }
  .term-out { color: var(--muted); }
  .term-typing {
    overflow: hidden;
    white-space: nowrap;
    border-right: 2px solid var(--neon);
    animation: typeIn 2s steps(40,end) 1s both, blinkCaret .7s step-end 1s infinite;
  }
  @keyframes typeIn {
    from { width: 0; }
    to   { width: 100%; }
  }
  @keyframes blinkCaret {
    50% { border-color: transparent; }
  }
</style>
</head>
<body>

<div class="grid-bg"></div>
<div class="scanline"></div>
<div class="orb orb-1"></div>
<div class="orb orb-2"></div>
<div class="orb orb-3"></div>
<canvas id="particles"></canvas>

<div class="container">

  <!-- ══ HERO ══ -->
  <section class="hero">
    <div class="avatar-ring">
      <div class="avatar-inner">👨‍💻</div>
      <div class="status-dot"></div>
    </div>

    <div class="hero-name">Abbosbek Turdaliyev</div>
    <div class="hero-tagline">&gt; Python Full-Stack Developer<span class="typed-cursor">_</span></div>
    <p class="hero-desc">
      Crafting scalable web applications, powerful REST APIs and smart Telegram bots.<br>
      Turning complex problems into clean, elegant code.
    </p>

    <div>
      <span class="glitch-badge badge-cyan">🐍 Python</span>
      <span class="glitch-badge badge-green">⚡ Django</span>
      <span class="glitch-badge badge-purple">🤖 Aiogram</span>
      <span class="glitch-badge badge-gold">🚀 FastAPI</span>
      <span class="glitch-badge badge-cyan">🔗 DRF</span>
      <span class="glitch-badge badge-green">🐧 Linux</span>
    </div>
  </section>

  <!-- ══ TERMINAL ══ -->
  <div class="terminal-box" style="animation: fadeUp .8s ease .3s both;">
    <div class="term-dots">
      <div class="dot dot-r"></div>
      <div class="dot dot-y"></div>
      <div class="dot dot-g"></div>
    </div>
    <div class="term-body">
      <div class="term-line"><span class="term-prompt">❯</span> <span class="term-cmd">whoami</span></div>
      <div class="term-line term-out">abbosbek — python developer & bot architect</div>
      <div class="term-line" style="margin-top:8px;"><span class="term-prompt">❯</span> <span class="term-cmd">cat skills.txt</span></div>
      <div class="term-line term-typing term-out">Django · DRF · FastAPI · Aiogram · PostgreSQL · Linux · Docker</div>
      <div class="term-line" style="margin-top:8px;"><span class="term-prompt">❯</span> <span class="term-cmd" style="color:var(--neon2);">status</span></div>
      <div class="term-line term-out">🟢 Open to freelance & collaboration</div>
    </div>
  </div>

  <!-- ══ SKILLS ══ -->
  <section class="skills-section">
    <div class="section-title">⚡ Skill Matrix</div>
    <div class="skills-grid">

      <div class="skill-card delay-1">
        <div class="skill-card-title">Backend</div>
        <div class="skill-bar-wrap">
          <div class="skill-bar-label"><span>Python</span><span>95%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill fill-cyan" data-width="95"></div></div>
        </div>
        <div class="skill-bar-wrap">
          <div class="skill-bar-label"><span>Django / DRF</span><span>92%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill fill-cyan" data-width="92"></div></div>
        </div>
        <div class="skill-bar-wrap">
          <div class="skill-bar-label"><span>FastAPI</span><span>85%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill fill-cyan" data-width="85"></div></div>
        </div>
        <div class="skill-bar-wrap">
          <div class="skill-bar-label"><span>PostgreSQL / MySQL</span><span>80%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill fill-cyan" data-width="80"></div></div>
        </div>
      </div>

      <div class="skill-card delay-2">
        <div class="skill-card-title">Telegram Bots</div>
        <div class="skill-bar-wrap">
          <div class="skill-bar-label"><span>Aiogram</span><span>93%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill fill-purple" data-width="93"></div></div>
        </div>
        <div class="skill-bar-wrap">
          <div class="skill-bar-label"><span>Pyrogram</span><span>85%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill fill-purple" data-width="85"></div></div>
        </div>
        <div class="skill-bar-wrap">
          <div class="skill-bar-label"><span>Telethon</span><span>78%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill fill-purple" data-width="78"></div></div>
        </div>
        <div class="skill-bar-wrap">
          <div class="skill-bar-label"><span>python-telegram-bot</span><span>75%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill fill-purple" data-width="75"></div></div>
        </div>
      </div>

      <div class="skill-card delay-3">
        <div class="skill-card-title">Frontend</div>
        <div class="skill-bar-wrap">
          <div class="skill-bar-label"><span>HTML5 / CSS3</span><span>88%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill fill-cyan" data-width="88"></div></div>
        </div>
        <div class="skill-bar-wrap">
          <div class="skill-bar-label"><span>Bootstrap / Tailwind</span><span>82%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill fill-cyan" data-width="82"></div></div>
        </div>
        <div class="skill-bar-wrap">
          <div class="skill-bar-label"><span>JavaScript / jQuery</span><span>70%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill fill-cyan" data-width="70"></div></div>
        </div>
      </div>

      <div class="skill-card delay-4">
        <div class="skill-card-title">DevOps / Tools</div>
        <div class="skill-bar-wrap">
          <div class="skill-bar-label"><span>Linux / Bash</span><span>85%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill fill-purple" data-width="85"></div></div>
        </div>
        <div class="skill-bar-wrap">
          <div class="skill-bar-label"><span>Git / GitHub</span><span>88%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill fill-purple" data-width="88"></div></div>
        </div>
        <div class="skill-bar-wrap">
          <div class="skill-bar-label"><span>Docker</span><span>72%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill fill-purple" data-width="72"></div></div>
        </div>
        <div class="skill-bar-wrap">
          <div class="skill-bar-label"><span>Swagger / API Docs</span><span>80%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill fill-purple" data-width="80"></div></div>
        </div>
      </div>

    </div>
  </section>

  <!-- ══ SERVICES ══ -->
  <section class="services-section">
    <div class="section-title">🛠 What I Build</div>
    <div class="services-grid">
      <div class="service-card delay-1">
        <span class="service-icon">🌐</span>
        <div>
          <h3>Web Applications</h3>
          <p>Full-stack Django apps with REST APIs, Swagger docs, authentication & admin panels.</p>
        </div>
      </div>
      <div class="service-card delay-2">
        <span class="service-icon">🤖</span>
        <div>
          <h3>Telegram Bots</h3>
          <p>Smart, feature-rich bots using Aiogram, Pyrogram & Telethon with database backends.</p>
        </div>
      </div>
      <div class="service-card delay-3">
        <span class="service-icon">⚡</span>
        <div>
          <h3>REST & Fast APIs</h3>
          <p>High-performance APIs with FastAPI, async support, JWT auth and full documentation.</p>
        </div>
      </div>
      <div class="service-card delay-4">
        <span class="service-icon">🗄️</span>
        <div>
          <h3>Database Design</h3>
          <p>Efficient PostgreSQL and MySQL schemas, ORM optimization and query performance.</p>
        </div>
      </div>
    </div>
  </section>

  <!-- ══ STATS ══ -->
  <section class="stats-section">
    <div class="section-title">📊 GitHub Activity</div>
    <div class="github-cards">
      <img class="github-card-img"
        src="https://github-readme-stats.vercel.app/api?username=AbbosCoder&show_icons=true&count_private=true&hide_border=true&bg_color=050a0f&title_color=00e5ff&icon_color=00ff88&text_color=e0f4ff&border_radius=12"
        alt="GitHub Stats" width="420">
      <img class="github-card-img"
        src="https://github-readme-stats.vercel.app/api/top-langs/?username=AbbosCoder&layout=compact&hide_border=true&bg_color=050a0f&title_color=00e5ff&text_color=e0f4ff&border_radius=12"
        alt="Top Languages" width="300">
    </div>
    <br>
    <div style="text-align:center;">
      <img class="github-card-img"
        src="https://github-readme-streak-stats.herokuapp.com/?user=AbbosCoder&hide_border=true&background=050a0f&stroke=1a3a52&ring=00e5ff&fire=00ff88&currStreakLabel=00e5ff&sideNums=e0f4ff&sideLabels=5a8aa0&dates=5a8aa0"
        alt="Streak Stats" style="max-width:500px;">
    </div>
  </section>

  <!-- ══ SOCIALS ══ -->
  <section class="social-section">
    <div class="section-title">🔗 Connect</div>
    <div class="social-links">
      <a href="https://github.com/Abboscoder" class="social-btn btn-github" target="_blank">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0 0 24 12c0-6.63-5.37-12-12-12z"/></svg>
        GitHub
      </a>
      <a href="https://linkedin.com/in/abbosbek-turdaliyev-953976255/" class="social-btn btn-linkedin" target="_blank">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
        LinkedIn
      </a>
      <a href="https://www.youtube.com/@Abbos_Tech" class="social-btn btn-youtube" target="_blank">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M23.495 6.205a3.007 3.007 0 0 0-2.088-2.088c-1.87-.501-9.396-.501-9.396-.501s-7.507-.01-9.396.501A3.007 3.007 0 0 0 .527 6.205a31.247 31.247 0 0 0-.522 5.805 31.247 31.247 0 0 0 .522 5.783 3.007 3.007 0 0 0 2.088 2.088c1.868.502 9.396.502 9.396.502s7.506 0 9.396-.502a3.007 3.007 0 0 0 2.088-2.088 31.247 31.247 0 0 0 .5-5.783 31.247 31.247 0 0 0-.5-5.805zM9.609 15.601V8.408l6.264 3.602z"/></svg>
        YouTube
      </a>
      <a href="https://instagram.com/abbosbek_turdaliyev" class="social-btn btn-instagram" target="_blank">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 1 0 0 12.324 6.162 6.162 0 0 0 0-12.324zM12 16a4 4 0 1 1 0-8 4 4 0 0 1 0 8zm6.406-11.845a1.44 1.44 0 1 0 0 2.881 1.44 1.44 0 0 0 0-2.881z"/></svg>
        Instagram
      </a>
      <a href="https://t.me/abbosbek_turdaliyev" class="social-btn btn-telegram" target="_blank">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.373 0 0 5.373 0 12s5.373 12 12 12 12-5.373 12-12S18.627 0 12 0zm5.894 8.221-1.97 9.28c-.145.658-.537.818-1.084.508l-3-2.21-1.447 1.394c-.16.16-.295.295-.605.295l.213-3.053 5.56-5.023c.242-.213-.054-.333-.373-.12l-6.871 4.326-2.962-.924c-.643-.204-.657-.643.136-.953l11.57-4.461c.537-.194 1.006.131.833.941z"/></svg>
        Telegram
      </a>
    </div>
  </section>

  <footer class="footer">
    Built with <span>❤️</span> by Abbosbek · Python Full-Stack Developer · Tashkent, Uzbekistan
  </footer>

</div>

<script>
/* ── PARTICLES ── */
const canvas = document.getElementById('particles');
const ctx = canvas.getContext('2d');
let W, H, particles = [];

function resize() { W = canvas.width = window.innerWidth; H = canvas.height = window.innerHeight; }
resize();
window.addEventListener('resize', resize);

class Particle {
  constructor() { this.reset(); }
  reset() {
    this.x = Math.random() * W;
    this.y = Math.random() * H;
    this.size = Math.random() * 1.8 + .4;
    this.speedX = (Math.random() - .5) * .4;
    this.speedY = (Math.random() - .5) * .4;
    this.alpha = Math.random() * .5 + .1;
    this.color = Math.random() > .5 ? '0,229,255' : '0,255,136';
  }
  update() {
    this.x += this.speedX; this.y += this.speedY;
    if (this.x < 0 || this.x > W || this.y < 0 || this.y > H) this.reset();
  }
  draw() {
    ctx.save();
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
    ctx.fillStyle = `rgba(${this.color},${this.alpha})`;
    ctx.fill();
    ctx.restore();
  }
}

for (let i = 0; i < 100; i++) particles.push(new Particle());

(function loop() {
  ctx.clearRect(0, 0, W, H);
  particles.forEach(p => { p.update(); p.draw(); });
  // connect nearby
  for (let i = 0; i < particles.length; i++) {
    for (let j = i + 1; j < particles.length; j++) {
      const dx = particles[i].x - particles[j].x;
      const dy = particles[i].y - particles[j].y;
      const dist = Math.sqrt(dx * dx + dy * dy);
      if (dist < 90) {
        ctx.beginPath();
        ctx.strokeStyle = `rgba(0,229,255,${.07 * (1 - dist / 90)})`;
        ctx.lineWidth = .5;
        ctx.moveTo(particles[i].x, particles[i].y);
        ctx.lineTo(particles[j].x, particles[j].y);
        ctx.stroke();
      }
    }
  }
  requestAnimationFrame(loop);
})();

/* ── SKILL BARS ── */
function animateBars() {
  document.querySelectorAll('.skill-bar-fill').forEach(bar => {
    const rect = bar.getBoundingClientRect();
    if (rect.top < window.innerHeight - 60) {
      bar.style.width = bar.dataset.width + '%';
    }
  });
}
window.addEventListener('scroll', animateBars);
setTimeout(animateBars, 600);
</script>
</body>
</html>
