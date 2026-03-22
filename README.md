<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Kavya M Injineri — ML & Backend Engineer</title>
  <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@300;400;600;700;800&family=Syne:wght@400;700;800&display=swap" rel="stylesheet"/>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --bg: #060810;
      --surface: #0d1117;
      --surface2: #131a24;
      --border: #1e2d3d;
      --purple: #a78bfa;
      --green: #34d399;
      --cyan: #67e8f9;
      --pink: #f472b6;
      --text: #e2e8f0;
      --muted: #64748b;
      --font-mono: 'JetBrains Mono', monospace;
      --font-display: 'Syne', sans-serif;
    }

    html { scroll-behavior: smooth; }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: var(--font-mono);
      overflow-x: hidden;
      cursor: none;
    }

    /* CUSTOM CURSOR */
    .cursor {
      width: 12px; height: 12px;
      background: var(--green);
      border-radius: 50%;
      position: fixed;
      pointer-events: none;
      z-index: 9999;
      transition: transform 0.15s ease, background 0.2s;
      mix-blend-mode: screen;
    }
    .cursor-ring {
      width: 36px; height: 36px;
      border: 1px solid var(--purple);
      border-radius: 50%;
      position: fixed;
      pointer-events: none;
      z-index: 9998;
      transition: transform 0.35s ease, width 0.2s, height 0.2s;
      transform: translate(-12px, -12px);
    }

    /* SCANLINE OVERLAY */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background: repeating-linear-gradient(
        0deg,
        transparent,
        transparent 2px,
        rgba(0,0,0,0.03) 2px,
        rgba(0,0,0,0.03) 4px
      );
      pointer-events: none;
      z-index: 9000;
    }

    /* GRID BACKGROUND */
    .grid-bg {
      position: fixed;
      inset: 0;
      background-image:
        linear-gradient(rgba(167,139,250,0.04) 1px, transparent 1px),
        linear-gradient(90deg, rgba(167,139,250,0.04) 1px, transparent 1px);
      background-size: 60px 60px;
      pointer-events: none;
      z-index: 0;
    }

    /* GLOW ORBS */
    .orb {
      position: fixed;
      border-radius: 50%;
      filter: blur(120px);
      pointer-events: none;
      z-index: 0;
      opacity: 0.18;
    }
    .orb-1 { width: 600px; height: 600px; background: var(--purple); top: -200px; right: -200px; }
    .orb-2 { width: 400px; height: 400px; background: var(--green); bottom: 100px; left: -150px; }
    .orb-3 { width: 300px; height: 300px; background: var(--cyan); top: 50%; right: 10%; }

    /* LAYOUT */
    .container { max-width: 1100px; margin: 0 auto; padding: 0 2rem; position: relative; z-index: 10; }

    /* ═══ HERO ═══ */
    .hero {
      min-height: 100vh;
      display: flex;
      align-items: center;
      padding: 6rem 0 4rem;
    }

    .boot-sequence {
      font-size: 0.75rem;
      color: var(--green);
      margin-bottom: 3rem;
      line-height: 1.9;
      opacity: 0;
      animation: fadeUp 0.6s ease 0.2s forwards;
    }
    .boot-sequence .prompt { color: var(--muted); }
    .boot-sequence .ok { color: var(--green); }
    .boot-sequence .loading { color: var(--cyan); }

    .hero-name {
      font-family: var(--font-display);
      font-size: clamp(3rem, 8vw, 6.5rem);
      font-weight: 800;
      line-height: 1;
      letter-spacing: -0.03em;
      opacity: 0;
      animation: fadeUp 0.7s ease 0.6s forwards;
    }
    .hero-name .line1 { color: var(--text); display: block; }
    .hero-name .line2 {
      display: block;
      background: linear-gradient(135deg, var(--purple), var(--cyan));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    .hero-role {
      margin-top: 1.5rem;
      font-size: 0.9rem;
      color: var(--muted);
      letter-spacing: 0.15em;
      text-transform: uppercase;
      opacity: 0;
      animation: fadeUp 0.7s ease 0.9s forwards;
    }
    .hero-role span {
      color: var(--green);
      border: 1px solid rgba(52,211,153,0.3);
      padding: 0.25rem 0.75rem;
      border-radius: 2px;
      margin-right: 0.5rem;
      display: inline-block;
      margin-top: 0.4rem;
    }

    .hero-tagline {
      margin-top: 2rem;
      font-size: 1rem;
      color: var(--text);
      opacity: 0;
      animation: fadeUp 0.7s ease 1.1s forwards;
    }
    .hero-tagline .comment { color: var(--muted); }
    .hero-tagline .string { color: var(--pink); }
    .hero-tagline .keyword { color: var(--purple); }

    .hero-links {
      margin-top: 2.5rem;
      display: flex;
      flex-wrap: wrap;
      gap: 1rem;
      opacity: 0;
      animation: fadeUp 0.7s ease 1.3s forwards;
    }
    .btn {
      display: inline-flex;
      align-items: center;
      gap: 0.5rem;
      padding: 0.65rem 1.4rem;
      font-family: var(--font-mono);
      font-size: 0.8rem;
      font-weight: 600;
      letter-spacing: 0.05em;
      text-decoration: none;
      border-radius: 3px;
      transition: all 0.25s ease;
      cursor: none;
    }
    .btn-primary {
      background: var(--purple);
      color: #0d1117;
      border: 1px solid var(--purple);
    }
    .btn-primary:hover { background: transparent; color: var(--purple); box-shadow: 0 0 20px rgba(167,139,250,0.4); }
    .btn-outline {
      background: transparent;
      color: var(--text);
      border: 1px solid var(--border);
    }
    .btn-outline:hover { border-color: var(--green); color: var(--green); box-shadow: 0 0 20px rgba(52,211,153,0.15); }

    .hero-code-block {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 1.5rem 2rem;
      font-size: 0.82rem;
      line-height: 2;
      opacity: 0;
      animation: fadeUp 0.7s ease 1.5s forwards;
      position: relative;
      margin-top: 3rem;
    }
    .hero-code-block::before {
      content: '● ● ●';
      position: absolute;
      top: 0.75rem; left: 1rem;
      font-size: 0.6rem;
      color: var(--muted);
      letter-spacing: 0.3em;
    }
    .code-kw { color: var(--purple); }
    .code-cls { color: var(--cyan); }
    .code-fn { color: var(--green); }
    .code-str { color: var(--pink); }
    .code-num { color: #fb923c; }
    .code-comment { color: var(--muted); font-style: italic; }
    .code-attr { color: var(--text); }

    /* ═══ SECTION ═══ */
    section { padding: 5rem 0; }
    .section-label {
      font-size: 0.7rem;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      color: var(--green);
      margin-bottom: 0.5rem;
    }
    .section-title {
      font-family: var(--font-display);
      font-size: clamp(1.8rem, 4vw, 2.8rem);
      font-weight: 800;
      color: var(--text);
      margin-bottom: 0.5rem;
    }
    .section-title .accent { color: var(--purple); }
    .section-divider {
      width: 60px; height: 2px;
      background: linear-gradient(90deg, var(--purple), transparent);
      margin-bottom: 3rem;
    }

    /* ═══ STATS BAR ═══ */
    .stats-bar {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 1px;
      background: var(--border);
      border: 1px solid var(--border);
      border-radius: 6px;
      overflow: hidden;
      margin-bottom: 5rem;
    }
    .stat-item {
      background: var(--surface);
      padding: 1.5rem;
      text-align: center;
      transition: background 0.2s;
    }
    .stat-item:hover { background: var(--surface2); }
    .stat-value {
      font-family: var(--font-display);
      font-size: 2rem;
      font-weight: 800;
      color: var(--purple);
      display: block;
    }
    .stat-label { font-size: 0.7rem; color: var(--muted); letter-spacing: 0.1em; text-transform: uppercase; margin-top: 0.3rem; }

    /* ═══ PROJECTS ═══ */
    .projects-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
      gap: 1px;
      background: var(--border);
      border: 1px solid var(--border);
      border-radius: 8px;
      overflow: hidden;
    }
    .project-card {
      background: var(--surface);
      padding: 2rem;
      transition: background 0.25s, transform 0.25s;
      position: relative;
      overflow: hidden;
      cursor: none;
    }
    .project-card::before {
      content: '';
      position: absolute;
      top: 0; left: 0; right: 0;
      height: 2px;
      background: linear-gradient(90deg, var(--purple), var(--cyan));
      transform: scaleX(0);
      transition: transform 0.3s ease;
      transform-origin: left;
    }
    .project-card:hover { background: var(--surface2); }
    .project-card:hover::before { transform: scaleX(1); }

    .project-icon { font-size: 1.8rem; margin-bottom: 1rem; display: block; }
    .project-name {
      font-family: var(--font-display);
      font-size: 1.1rem;
      font-weight: 700;
      color: var(--text);
      margin-bottom: 0.5rem;
    }
    .project-desc {
      font-size: 0.78rem;
      color: var(--muted);
      line-height: 1.7;
      margin-bottom: 1.2rem;
    }
    .project-tags { display: flex; flex-wrap: wrap; gap: 0.4rem; }
    .tag {
      font-size: 0.65rem;
      padding: 0.2rem 0.6rem;
      border-radius: 2px;
      letter-spacing: 0.05em;
      font-weight: 600;
    }
    .tag-purple { background: rgba(167,139,250,0.12); color: var(--purple); border: 1px solid rgba(167,139,250,0.2); }
    .tag-green  { background: rgba(52,211,153,0.1);  color: var(--green);  border: 1px solid rgba(52,211,153,0.2); }
    .tag-cyan   { background: rgba(103,232,249,0.1); color: var(--cyan);   border: 1px solid rgba(103,232,249,0.2); }
    .tag-pink   { background: rgba(244,114,182,0.1); color: var(--pink);   border: 1px solid rgba(244,114,182,0.2); }
    .tag-orange { background: rgba(251,146,60,0.1);  color: #fb923c;       border: 1px solid rgba(251,146,60,0.2); }

    /* ═══ SKILLS ═══ */
    .skills-wrapper {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 1.5rem;
    }
    .skill-group {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 6px;
      padding: 1.5rem;
    }
    .skill-group-title {
      font-size: 0.7rem;
      text-transform: uppercase;
      letter-spacing: 0.15em;
      color: var(--green);
      margin-bottom: 1rem;
      padding-bottom: 0.6rem;
      border-bottom: 1px solid var(--border);
    }
    .skill-list { display: flex; flex-wrap: wrap; gap: 0.5rem; }
    .skill-pill {
      font-size: 0.72rem;
      padding: 0.3rem 0.75rem;
      background: var(--surface2);
      border: 1px solid var(--border);
      border-radius: 2px;
      color: var(--text);
      transition: all 0.2s;
      cursor: none;
    }
    .skill-pill:hover { border-color: var(--purple); color: var(--purple); }

    /* ═══ GITHUB STATS ═══ */
    .stats-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 1.5rem;
      margin-bottom: 1.5rem;
    }
    .stats-grid img, .stats-full img {
      width: 100%;
      border-radius: 6px;
      border: 1px solid var(--border);
      display: block;
    }

    /* ═══ TERMINAL QUOTE ═══ */
    .terminal-quote {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 2rem 2.5rem;
      position: relative;
      overflow: hidden;
      text-align: center;
      margin-top: 4rem;
    }
    .terminal-quote::before {
      content: '$ echo "kavya.philosophy"';
      display: block;
      font-size: 0.72rem;
      color: var(--green);
      margin-bottom: 1rem;
      text-align: left;
    }
    .terminal-quote blockquote {
      font-family: var(--font-display);
      font-size: 1.4rem;
      font-weight: 700;
      color: var(--text);
      line-height: 1.5;
    }
    .terminal-quote cite {
      display: block;
      margin-top: 1rem;
      font-size: 0.75rem;
      color: var(--muted);
      font-style: normal;
    }
    .cursor-blink {
      display: inline-block;
      width: 10px; height: 1.1em;
      background: var(--green);
      vertical-align: text-bottom;
      animation: blink 1s step-end infinite;
    }

    /* ═══ FOOTER ═══ */
    footer {
      border-top: 1px solid var(--border);
      padding: 2rem 0;
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 0.72rem;
      color: var(--muted);
      flex-wrap: wrap;
      gap: 1rem;
    }
    .footer-badge {
      background: rgba(52,211,153,0.1);
      border: 1px solid rgba(52,211,153,0.25);
      color: var(--green);
      padding: 0.3rem 0.8rem;
      border-radius: 2px;
      font-size: 0.65rem;
      letter-spacing: 0.1em;
    }

    /* ═══ ANIMATIONS ═══ */
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(20px); }
      to   { opacity: 1; transform: translateY(0); }
    }
    @keyframes blink {
      0%, 100% { opacity: 1; }
      50% { opacity: 0; }
    }
    @keyframes float {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-8px); }
    }

    .reveal {
      opacity: 0;
      transform: translateY(30px);
      transition: opacity 0.7s ease, transform 0.7s ease;
    }
    .reveal.visible {
      opacity: 1;
      transform: none;
    }

    /* RESPONSIVE */
    @media (max-width: 700px) {
      .stats-bar { grid-template-columns: repeat(2, 1fr); }
      .stats-grid { grid-template-columns: 1fr; }
      .hero { padding-top: 4rem; }
    }
  </style>
</head>
<body>

  <!-- CURSOR -->
  <div class="cursor" id="cursor"></div>
  <div class="cursor-ring" id="cursorRing"></div>

  <!-- BACKGROUND -->
  <div class="grid-bg"></div>
  <div class="orb orb-1"></div>
  <div class="orb orb-2"></div>
  <div class="orb orb-3"></div>

  <!-- ═══ HERO ═══ -->
  <section class="hero">
    <div class="container">

      <div class="boot-sequence">
        <div><span class="prompt">$</span> <span class="loading">SYSTEM BOOT</span> ............... <span class="ok">[OK]</span></div>
        <div><span class="prompt">$</span> Loading <span class="loading">kavya.ml_models</span> ........ <span class="ok">[OK]</span></div>
        <div><span class="prompt">$</span> Loading <span class="loading">kavya.backend_stack</span> ..... <span class="ok">[OK]</span></div>
        <div><span class="prompt">$</span> Brewing <span class="loading">tea.exe</span> ................ <span class="ok">[OK ☕]</span></div>
        <div><span class="prompt">$</span> STATUS: <span class="ok">ONLINE — Ready to build ⚡</span></div>
      </div>

      <h1 class="hero-name">
        <span class="line1">Kavya M</span>
        <span class="line2">Injineri</span>
      </h1>

      <div class="hero-role">
        <span>ML Engineer</span>
        <span>Backend Dev</span>
        <span>AI Builder</span>
      </div>

      <div class="hero-tagline" style="margin-top:1.8rem;">
        <span class="comment">// CS @ MITM &nbsp;·&nbsp; CGPA 9.275 &nbsp;·&nbsp; Bluestock Fintech Intern</span><br/>
        <span class="keyword">const</span> mission = <span class="string">"Build ML systems that actually ship"</span>;
      </div>

      <div class="hero-links">
        <a href="https://portfolio-six-pied-83.vercel.app" class="btn btn-primary" target="_blank">🌐 Portfolio</a>
        <a href="https://linkedin.com/in/kavya-injineri" class="btn btn-outline" target="_blank">🔗 LinkedIn</a>
        <a href="https://github.com/Kavya-M-Injineri" class="btn btn-outline" target="_blank">⌥ GitHub</a>
      </div>

      <div class="hero-code-block">
        <br/>
        <span class="code-kw">class</span> <span class="code-cls">KavyaInjineri</span>:<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;<span class="code-kw">def</span> <span class="code-fn">__init__</span>(self):<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;self.<span class="code-attr">college</span>    = <span class="code-str">"Maharaja Institute of Technology Mysuru"</span><br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;self.<span class="code-attr">cgpa</span>       = <span class="code-num">9.275</span><br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;self.<span class="code-attr">domains</span>    = [<span class="code-str">"ML"</span>, <span class="code-str">"Computer Vision"</span>, <span class="code-str">"Backend"</span>, <span class="code-str">"AI Agents"</span>]<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;self.<span class="code-attr">tea_cups</span>   = <span class="code-fn">float</span>(<span class="code-str">"inf"</span>)  <span class="code-comment"># critical dependency</span><br/>
        <br/>
        &nbsp;&nbsp;&nbsp;&nbsp;<span class="code-kw">def</span> <span class="code-fn">fun_fact</span>(self):<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="code-kw">return</span> <span class="code-str">"My code works. I have no idea why. My tea is ready. I know exactly why ☕"</span>
      </div>

    </div>
  </section>

  <!-- ═══ STATS BAR ═══ -->
  <div class="container">
    <div class="stats-bar reveal">
      <div class="stat-item">
        <span class="stat-value">9.275</span>
        <span class="stat-label">CGPA</span>
      </div>
      <div class="stat-item">
        <span class="stat-value">8+</span>
        <span class="stat-label">Projects Shipped</span>
      </div>
      <div class="stat-item">
        <span class="stat-value">10+</span>
        <span class="stat-label">Tech Stack</span>
      </div>
      <div class="stat-item">
        <span class="stat-value">∞</span>
        <span class="stat-label">Tea Consumed</span>
      </div>
    </div>
  </div>

  <!-- ═══ PROJECTS ═══ -->
  <section>
    <div class="container">
      <div class="reveal">
        <div class="section-label">$ ls ~/projects</div>
        <h2 class="section-title">Things I've <span class="accent">Built</span></h2>
        <div class="section-divider"></div>
      </div>

      <div class="projects-grid reveal">

        <div class="project-card">
          <span class="project-icon">🌾</span>
          <div class="project-name">KrishiSarthi AI</div>
          <div class="project-desc">Real-time crop disease detection system. EfficientNet-B0 + YOLOv8 trained on field data. Built for farmers who can't afford to lose a harvest.</div>
          <div class="project-tags">
            <span class="tag tag-purple">EfficientNet-B0</span>
            <span class="tag tag-green">YOLOv8</span>
            <span class="tag tag-cyan">Flask</span>
          </div>
        </div>

        <div class="project-card">
          <span class="project-icon">📄</span>
          <div class="project-name">DevDoc AI</div>
          <div class="project-desc">RAG-based documentation retrieval engine. FAISS vector store + BERT embeddings. Search code docs the way they should be searched — semantically.</div>
          <div class="project-tags">
            <span class="tag tag-purple">FAISS</span>
            <span class="tag tag-green">BERT</span>
            <span class="tag tag-cyan">RAG</span>
            <span class="tag tag-pink">FastAPI</span>
          </div>
        </div>

        <div class="project-card">
          <span class="project-icon">🛡️</span>
          <div class="project-name">SoldierCare+</div>
          <div class="project-desc">Real-time biometric health dashboard for soldiers. WebSocket-powered vitals monitoring with instant alert systems. Full-stack, production-grade.</div>
          <div class="project-tags">
            <span class="tag tag-cyan">React</span>
            <span class="tag tag-green">Node.js</span>
            <span class="tag tag-purple">WebSockets</span>
            <span class="tag tag-pink">PostgreSQL</span>
          </div>
        </div>

        <div class="project-card">
          <span class="project-icon">🛰️</span>
          <div class="project-name">SpaceGuard</div>
          <div class="project-desc">LSTM Autoencoder detecting spacecraft anomalies from telemetry data. Containerized with Docker, deployed on Hugging Face. Space-grade anomaly detection.</div>
          <div class="project-tags">
            <span class="tag tag-purple">LSTM Autoencoder</span>
            <span class="tag tag-green">Docker</span>
            <span class="tag tag-cyan">Hugging Face</span>
          </div>
        </div>

        <div class="project-card">
          <span class="project-icon">🩺</span>
          <div class="project-name">Medical AI Chest X-ray</div>
          <div class="project-desc">MobileNetV2 chest X-ray classifier with a twist — outputs both Modern Medicine AND Ayurvedic treatment recommendations. Dual-diagnosis, one model.</div>
          <div class="project-tags">
            <span class="tag tag-purple">MobileNetV2</span>
            <span class="tag tag-green">TensorFlow</span>
            <span class="tag tag-pink">Flask</span>
          </div>
        </div>

        <div class="project-card">
          <span class="project-icon">🫁</span>
          <div class="project-name">Pneumonia Detection</div>
          <div class="project-desc">CNN-based medical image classifier for pneumonia detection from chest X-rays. Flask-served inference pipeline, lightweight and deployable.</div>
          <div class="project-tags">
            <span class="tag tag-cyan">CNN</span>
            <span class="tag tag-green">Flask</span>
            <span class="tag tag-purple">Medical AI</span>
          </div>
        </div>

        <div class="project-card">
          <span class="project-icon">🎨</span>
          <div class="project-name">DC-GAN MNIST</div>
          <div class="project-desc">Deep Convolutional GAN that generates handwritten digits from pure noise. PyTorch-built, Flask-served. Because generating data from scratch is cool.</div>
          <div class="project-tags">
            <span class="tag tag-orange">PyTorch</span>
            <span class="tag tag-purple">GAN</span>
            <span class="tag tag-green">Flask</span>
          </div>
        </div>

        <div class="project-card">
          <span class="project-icon">✅</span>
          <div class="project-name">Task Manager</div>
          <div class="project-desc">Full-stack production app — JWT auth, REST API with Swagger docs, Docker-compose deployment. PostgreSQL + Sequelize + React/Vite. Ships like it means it.</div>
          <div class="project-tags">
            <span class="tag tag-cyan">PostgreSQL</span>
            <span class="tag tag-green">Docker</span>
            <span class="tag tag-purple">JWT</span>
            <span class="tag tag-pink">React</span>
          </div>
        </div>

      </div>
    </div>
  </section>

  <!-- ═══ SKILLS ═══ -->
  <section>
    <div class="container">
      <div class="reveal">
        <div class="section-label">$ cat skills.json</div>
        <h2 class="section-title">Tech <span class="accent">Stack</span></h2>
        <div class="section-divider"></div>
      </div>

      <div class="skills-wrapper reveal">
        <div class="skill-group">
          <div class="skill-group-title">🧠 ML / AI / Vision</div>
          <div class="skill-list">
            <span class="skill-pill">Python</span>
            <span class="skill-pill">PyTorch</span>
            <span class="skill-pill">TensorFlow</span>
            <span class="skill-pill">YOLOv8</span>
            <span class="skill-pill">EfficientNet</span>
            <span class="skill-pill">MobileNetV2</span>
            <span class="skill-pill">LSTM</span>
            <span class="skill-pill">FAISS</span>
            <span class="skill-pill">BERT</span>
            <span class="skill-pill">OpenCV</span>
            <span class="skill-pill">Hugging Face</span>
          </div>
        </div>

        <div class="skill-group">
          <div class="skill-group-title">⚙️ Backend / APIs</div>
          <div class="skill-list">
            <span class="skill-pill">FastAPI</span>
            <span class="skill-pill">Flask</span>
            <span class="skill-pill">Node.js</span>
            <span class="skill-pill">Express</span>
            <span class="skill-pill">PostgreSQL</span>
            <span class="skill-pill">Sequelize</span>
            <span class="skill-pill">JWT</span>
            <span class="skill-pill">REST API</span>
            <span class="skill-pill">WebSockets</span>
            <span class="skill-pill">Swagger</span>
          </div>
        </div>

        <div class="skill-group">
          <div class="skill-group-title">🎨 Frontend</div>
          <div class="skill-list">
            <span class="skill-pill">React</span>
            <span class="skill-pill">Vite</span>
            <span class="skill-pill">JavaScript</span>
            <span class="skill-pill">HTML5</span>
            <span class="skill-pill">CSS3</span>
            <span class="skill-pill">IndexedDB</span>
          </div>
        </div>

        <div class="skill-group">
          <div class="skill-group-title">🛠️ DevOps / Tools</div>
          <div class="skill-list">
            <span class="skill-pill">Docker</span>
            <span class="skill-pill">Git</span>
            <span class="skill-pill">GitHub</span>
            <span class="skill-pill">Linux</span>
            <span class="skill-pill">VS Code</span>
            <span class="skill-pill">Postman</span>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- ═══ GITHUB STATS ═══ -->
  <section>
    <div class="container">
      <div class="reveal">
        <div class="section-label">$ git log --stats</div>
        <h2 class="section-title">GitHub <span class="accent">Stats</span></h2>
        <div class="section-divider"></div>
      </div>

      <div class="stats-grid reveal">
        <img src="https://github-readme-stats.vercel.app/api?username=Kavya-M-Injineri&show_icons=true&theme=tokyonight&hide_border=true&bg_color=0d1117&title_color=a78bfa&icon_color=34d399&text_color=c9d1d9" alt="GitHub Stats"/>
        <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=Kavya-M-Injineri&layout=compact&theme=tokyonight&hide_border=true&bg_color=0d1117&title_color=a78bfa&text_color=c9d1d9" alt="Top Languages"/>
      </div>

      <div class="stats-full reveal">
        <img src="https://streak-stats.demolab.com?user=Kavya-M-Injineri&theme=tokyonight&hide_border=true&background=0d1117&stroke=a78bfa&ring=a78bfa&fire=34d399&currStreakLabel=34d399" alt="Streak Stats"/>
      </div>

      <div style="margin-top:1.5rem;" class="reveal">
        <img src="https://github-readme-activity-graph.vercel.app/graph?username=Kavya-M-Injineri&bg_color=0d1117&color=a78bfa&line=34d399&point=ffffff&area=true&hide_border=true" alt="Activity Graph" style="width:100%;border-radius:6px;border:1px solid #1e2d3d;"/>
      </div>
    </div>
  </section>

  <!-- ═══ QUOTE ═══ -->
  <div class="container">
    <div class="terminal-quote reveal">
      <blockquote>
        "The best model is the one that ships."
        <span class="cursor-blink"></span>
      </blockquote>
      <cite>— Kavya, probably, after her 3rd cup of tea ☕</cite>
    </div>
  </div>

  <!-- ═══ FOOTER ═══ -->
  <div class="container">
    <footer class="reveal">
      <span>© 2025 Kavya M Injineri &nbsp;·&nbsp; Built with ☕ and too many model epochs</span>
      <span class="footer-badge">OPEN TO INTERNSHIPS ⚡</span>
    </footer>
  </div>

  <script>
    // CURSOR
    const cursor = document.getElementById('cursor');
    const ring = document.getElementById('cursorRing');
    let mx = 0, my = 0, rx = 0, ry = 0;
    document.addEventListener('mousemove', e => {
      mx = e.clientX; my = e.clientY;
      cursor.style.left = mx - 6 + 'px';
      cursor.style.top  = my - 6 + 'px';
    });
    function animRing() {
      rx += (mx - rx - 18) * 0.12;
      ry += (my - ry - 18) * 0.12;
      ring.style.left = rx + 'px';
      ring.style.top  = ry + 'px';
      requestAnimationFrame(animRing);
    }
    animRing();
    document.querySelectorAll('a, .project-card, .skill-pill, .stat-item').forEach(el => {
      el.addEventListener('mouseenter', () => { cursor.style.transform = 'scale(2)'; ring.style.width = '60px'; ring.style.height = '60px'; });
      el.addEventListener('mouseleave', () => { cursor.style.transform = 'scale(1)'; ring.style.width = '36px'; ring.style.height = '36px'; });
    });

    // SCROLL REVEAL
    const reveals = document.querySelectorAll('.reveal');
    const observer = new IntersectionObserver(entries => {
      entries.forEach((e, i) => {
        if (e.isIntersecting) {
          e.target.style.transitionDelay = (i % 4) * 0.1 + 's';
          e.target.classList.add('visible');
        }
      });
    }, { threshold: 0.1 });
    reveals.forEach(el => observer.observe(el));
  </script>
</body>
</html>
