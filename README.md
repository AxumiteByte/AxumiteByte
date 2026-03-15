<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Abenezer Niguse // Kal10</title>
  <link href="https://fonts.googleapis.com/css2?family=VT323&family=Share+Tech+Mono&display=swap" rel="stylesheet">
  <style>
    :root {
      --green: #00ffb8;
      --pink: #ff00ff;
      --yellow: #ffff00;
      --orange: #ff6600;
      --bg: #0d0b1e;
      --bg2: #0a0818;
      --border: #00ffb8;
      --dim: #1a3a2a;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      background: var(--bg);
      font-family: 'VT323', 'Share Tech Mono', monospace;
      color: var(--green);
      min-height: 100vh;
      overflow-x: hidden;
      cursor: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='16' height='16'%3E%3Crect width='16' height='16' fill='%2300ffb8'/%3E%3C/svg%3E") 8 8, crosshair;
    }

    /* CRT scanlines overlay */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background: repeating-linear-gradient(
        0deg, transparent, transparent 2px,
        rgba(0,0,0,0.08) 2px, rgba(0,0,0,0.08) 4px
      );
      pointer-events: none;
      z-index: 9999;
    }

    /* CRT flicker */
    body::after {
      content: '';
      position: fixed;
      inset: 0;
      background: rgba(0,255,184,0.015);
      pointer-events: none;
      z-index: 9998;
      animation: flicker 8s infinite;
    }

    @keyframes flicker {
      0%,19%,21%,23%,25%,54%,56%,100% { opacity: 1; }
      20%,24%,55% { opacity: 0.7; }
    }

    /* Taskbar */
    .taskbar {
      background: var(--bg2);
      border-bottom: 2px solid var(--green);
      padding: 8px 20px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      font-size: 22px;
      letter-spacing: 2px;
      position: sticky;
      top: 0;
      z-index: 100;
    }
    .taskbar-logo { color: var(--green); display: flex; align-items: center; gap: 10px; }
    .taskbar-logo .pixel-icon {
      display: grid;
      grid-template-columns: repeat(4,8px);
      gap: 1px;
    }
    .taskbar-logo .pixel-icon div { width: 8px; height: 8px; }
    .taskbar-title { color: var(--pink); animation: pulse 2s ease-in-out infinite; }
    .taskbar-clock { color: var(--yellow); font-size: 18px; }

    @keyframes pulse { 0%,100%{opacity:1} 50%{opacity:0.6} }

    /* Marquee */
    .marquee-wrap {
      background: var(--bg2);
      border-bottom: 1px solid var(--pink);
      border-top: 1px solid var(--pink);
      padding: 6px 0;
      overflow: hidden;
      white-space: nowrap;
    }
    .marquee-inner {
      display: inline-block;
      animation: marquee 25s linear infinite;
      font-size: 18px;
      color: var(--pink);
      letter-spacing: 3px;
    }
    @keyframes marquee {
      0% { transform: translateX(100vw); }
      100% { transform: translateX(-100%); }
    }

    /* Layout */
    .desktop {
      padding: 16px;
      max-width: 960px;
      margin: 0 auto;
      display: flex;
      flex-direction: column;
      gap: 14px;
    }

    /* Windows */
    .window {
      border: 2px solid var(--green);
      background: var(--bg2);
      animation: boot 0.4s ease both;
    }
    .window:nth-child(1) { animation-delay: 0.1s; }
    .window:nth-child(2) { animation-delay: 0.2s; }
    .window:nth-child(3) { animation-delay: 0.3s; }
    .window:nth-child(4) { animation-delay: 0.4s; }
    .window:nth-child(5) { animation-delay: 0.5s; }

    @keyframes boot {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .win-title {
      background: var(--green);
      color: var(--bg2);
      padding: 4px 12px;
      font-size: 20px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      letter-spacing: 2px;
    }
    .win-controls { display: flex; gap: 6px; }
    .wc {
      width: 18px; height: 18px;
      border: 1px solid var(--bg2);
      display: flex; align-items: center; justify-content: center;
      font-size: 13px; cursor: pointer;
      background: var(--bg);
      color: var(--green);
      transition: background 0.1s;
    }
    .wc:hover { background: var(--pink); color: var(--bg); }

    .win-body { padding: 16px 20px; }

    /* Two column */
    .two-col {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 14px;
    }

    /* Pixel avatar */
    .pixel-avatar {
      display: grid;
      grid-template-columns: repeat(12, 18px);
      gap: 2px;
      margin: 0 auto 14px;
      width: fit-content;
    }
    .px { width: 18px; height: 18px; border-radius: 1px; }
    .p0 { background: transparent; }
    .p1 { background: #ff00ff; }
    .p2 { background: #ffff00; }
    .p3 { background: #00ffb8; }
    .p4 { background: #ff6600; }
    .p5 { background: #0a0818; }
    .p6 { background: #ff4444; }

    /* Bio */
    .bio-name {
      color: var(--pink);
      font-size: 36px;
      text-align: center;
      text-shadow: 3px 3px 0 rgba(255,0,255,0.3);
      letter-spacing: 3px;
      animation: glow-pink 2s ease-in-out infinite alternate;
    }
    @keyframes glow-pink {
      from { text-shadow: 0 0 8px var(--pink), 3px 3px 0 rgba(255,0,255,0.3); }
      to   { text-shadow: 0 0 20px var(--pink), 3px 3px 0 rgba(255,0,255,0.5); }
    }
    .bio-handle { color: var(--green); font-size: 20px; text-align: center; margin: 4px 0 10px; }
    .bio-divider { border: none; border-top: 1px dashed var(--dim); margin: 10px 0; }
    .bio-lines { font-size: 18px; line-height: 2; }
    .bio-lines div { display: flex; gap: 8px; }
    .bio-lines .arrow { color: var(--yellow); }
    .bio-lines .text { color: var(--green); }

    .blink { animation: blink 1s step-end infinite; }
    @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

    /* Stats */
    .stat-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 10px;
    }
    .stat-box {
      border: 2px solid var(--green);
      padding: 12px;
      text-align: center;
      position: relative;
      overflow: hidden;
      transition: border-color 0.2s;
    }
    .stat-box:hover { border-color: var(--pink); }
    .stat-box::before {
      content: '';
      position: absolute;
      inset: 0;
      background: linear-gradient(135deg, rgba(0,255,184,0.05), transparent);
    }
    .stat-num {
      color: var(--yellow);
      font-size: 40px;
      display: block;
      animation: count-glow 3s ease-in-out infinite alternate;
    }
    @keyframes count-glow {
      from { text-shadow: 0 0 6px var(--yellow); }
      to   { text-shadow: 0 0 20px var(--yellow), 0 0 40px rgba(255,255,0,0.3); }
    }
    .stat-lbl { color: var(--green); font-size: 16px; letter-spacing: 2px; }

    /* Skills */
    .skill-row { margin: 6px 0; font-size: 18px; }
    .sk-label { color: var(--pink); display: inline-block; width: 130px; letter-spacing: 1px; }
    .sk-bar-wrap {
      display: inline-block;
      width: 200px;
      height: 18px;
      background: var(--dim);
      vertical-align: middle;
      position: relative;
      overflow: hidden;
    }
    .sk-bar {
      height: 100%;
      background: var(--green);
      width: 0;
      transition: width 1.5s cubic-bezier(0.4,0,0.2,1);
      position: relative;
    }
    .sk-bar::after {
      content: '';
      position: absolute;
      right: 0; top: 0; bottom: 0;
      width: 3px;
      background: white;
      animation: bar-blink 0.5s step-end infinite;
    }
    @keyframes bar-blink { 0%,100%{opacity:1} 50%{opacity:0} }
    .sk-pct { color: var(--yellow); font-size: 16px; margin-left: 8px; vertical-align: middle; }

    /* Pinned repos */
    .pin-list { list-style: none; }
    .pin-item {
      border-bottom: 1px dashed var(--dim);
      padding: 10px 0;
      display: grid;
      grid-template-columns: auto 1fr auto;
      gap: 12px;
      align-items: start;
      transition: background 0.15s;
      cursor: pointer;
    }
    .pin-item:last-child { border-bottom: none; }
    .pin-item:hover { background: rgba(0,255,184,0.04); }
    .pin-emoji { font-size: 20px; }
    .pin-name { color: var(--pink); font-size: 18px; letter-spacing: 1px; }
    .pin-desc { color: var(--green); font-size: 15px; margin-top: 2px; opacity: 0.8; }
    .pin-meta { color: var(--yellow); font-size: 15px; white-space: nowrap; text-align: right; }
    .pin-lang { color: var(--dim); font-size: 13px; }

    /* Connect */
    .connect-box {
      border: 2px solid var(--pink);
      padding: 16px 20px;
      font-size: 18px;
      line-height: 2.2;
    }
    .connect-box .title { color: var(--pink); margin-bottom: 8px; font-size: 20px; }
    .connect-row { display: flex; gap: 10px; align-items: center; }
    .connect-key { color: var(--yellow); width: 30px; }
    .connect-label { color: var(--green); width: 120px; }
    .connect-val a {
      color: var(--pink);
      text-decoration: none;
      border-bottom: 1px dashed var(--pink);
      transition: color 0.2s;
    }
    .connect-val a:hover { color: var(--yellow); border-color: var(--yellow); }

    /* Bottom bar */
    .bottom-bar {
      background: var(--green);
      color: var(--bg2);
      font-size: 18px;
      padding: 6px 16px;
      display: flex;
      justify-content: space-between;
      letter-spacing: 1px;
      position: sticky;
      bottom: 0;
    }
    .mem-bar { display: inline-flex; gap: 3px; margin-left: 8px; vertical-align: middle; }
    .mem-seg {
      width: 16px; height: 14px;
      background: var(--bg2);
      display: inline-block;
    }
    .mem-seg.active { background: var(--pink); }

    /* Boot screen */
    #boot-screen {
      position: fixed;
      inset: 0;
      background: var(--bg);
      z-index: 10000;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      font-size: 22px;
      gap: 8px;
      color: var(--green);
    }
    .boot-line { opacity: 0; animation: boot-appear 0.3s ease forwards; }
    .boot-line:nth-child(1)  { animation-delay: 0.2s; }
    .boot-line:nth-child(2)  { animation-delay: 0.5s; }
    .boot-line:nth-child(3)  { animation-delay: 0.9s; }
    .boot-line:nth-child(4)  { animation-delay: 1.3s; }
    .boot-line:nth-child(5)  { animation-delay: 1.7s; }
    .boot-line:nth-child(6)  { animation-delay: 2.1s; color: var(--yellow); }
    .boot-line:nth-child(7)  { animation-delay: 2.5s; color: var(--pink); font-size: 28px; }
    @keyframes boot-appear {
      from { opacity: 0; transform: translateX(-10px); }
      to   { opacity: 1; transform: translateX(0); }
    }

    .progress-wrap { width: 400px; height: 20px; border: 2px solid var(--green); margin-top: 16px; opacity: 0; animation: boot-appear 0.3s ease 1.7s forwards; }
    .progress-fill { height: 100%; background: var(--green); width: 0; animation: fill-bar 1s ease 2s forwards; }
    @keyframes fill-bar { to { width: 100%; } }

    /* Responsive */
    @media (max-width: 640px) {
      .two-col { grid-template-columns: 1fr; }
      .pixel-avatar { grid-template-columns: repeat(12, 14px); }
      .px { width: 14px; height: 14px; }
      .sk-bar-wrap { width: 130px; }
    }
  </style>
</head>
<body>

  <!-- Boot screen -->
  <div id="boot-screen">
    <div class="boot-line">GITHUB OS v1.0 — INITIALIZING...</div>
    <div class="boot-line">LOADING USER: KAL10...</div>
    <div class="boot-line">CHECKING REPOS: OK</div>
    <div class="boot-line">MOUNTING SKILLS.SYS: OK</div>
    <div class="boot-line">LOADING PROFILE DATA...</div>
    <div class="boot-line">ALL SYSTEMS GO.</div>
    <div class="boot-line">WELCOME, ABENEZER NIGUSE</div>
    <div class="progress-wrap"><div class="progress-fill"></div></div>
  </div>

  <!-- Taskbar -->
  <div class="taskbar">
    <div class="taskbar-logo">
      <div class="pixel-icon">
        <div style="background:#00ffb8"></div><div style="background:#00ffb8"></div><div style="background:transparent"></div><div style="background:#00ffb8"></div>
        <div style="background:#00ffb8"></div><div style="background:transparent"></div><div style="background:#00ffb8"></div><div style="background:#00ffb8"></div>
        <div style="background:transparent"></div><div style="background:#00ffb8"></div><div style="background:#00ffb8"></div><div style="background:transparent"></div>
      </div>
      GITHUB OS v1.0
    </div>
    <span class="taskbar-title">[ ABENEZER NIGUSE ]</span>
    <span class="taskbar-clock" id="clock">00:00:00</span>
  </div>

  <!-- Marquee -->
  <div class="marquee-wrap">
    <span class="marquee-inner">★ WELCOME TO KAL10'S PORTFOLIO ★ &nbsp;&nbsp;&nbsp; FULL-STACK DEVELOPER &nbsp;&nbsp;&nbsp; ROTTERDAM, NETHERLANDS &nbsp;&nbsp;&nbsp; JAVASCRIPT · TYPESCRIPT · REACT · NODE.JS &nbsp;&nbsp;&nbsp; OPEN SOURCE BUILDER &nbsp;&nbsp;&nbsp; AVAILABLE FOR HIRE &nbsp;&nbsp;&nbsp; ★ &nbsp;&nbsp;&nbsp;</span>
  </div>

  <!-- Desktop -->
  <div class="desktop">

    <div class="two-col">

      <!-- USER.EXE -->
      <div class="window">
        <div class="win-title">
          [ USER.EXE ]
          <div class="win-controls">
            <div class="wc">_</div><div class="wc">□</div><div class="wc">✕</div>
          </div>
        </div>
        <div class="win-body">
          <!-- Pixel avatar face -->
          <div class="pixel-avatar">
            <!-- row 1 -->
            <div class="px p0"></div><div class="px p0"></div><div class="px p1"></div><div class="px p1"></div><div class="px p1"></div><div class="px p1"></div><div class="px p1"></div><div class="px p1"></div><div class="px p1"></div><div class="px p1"></div><div class="px p0"></div><div class="px p0"></div>
            <!-- row 2 -->
            <div class="px p0"></div><div class="px p1"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p1"></div><div class="px p0"></div>
            <!-- row 3 eyes -->
            <div class="px p1"></div><div class="px p2"></div><div class="px p5"></div><div class="px p5"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p5"></div><div class="px p5"></div><div class="px p2"></div><div class="px p1"></div>
            <!-- row 4 -->
            <div class="px p1"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p1"></div>
            <!-- row 5 smile -->
            <div class="px p1"></div><div class="px p2"></div><div class="px p4"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p4"></div><div class="px p2"></div><div class="px p1"></div>
            <!-- row 6 -->
            <div class="px p1"></div><div class="px p2"></div><div class="px p2"></div><div class="px p4"></div><div class="px p4"></div><div class="px p4"></div><div class="px p4"></div><div class="px p4"></div><div class="px p4"></div><div class="px p2"></div><div class="px p2"></div><div class="px p1"></div>
            <!-- row 7 body -->
            <div class="px p0"></div><div class="px p1"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p2"></div><div class="px p1"></div><div class="px p0"></div>
            <!-- row 8 -->
            <div class="px p0"></div><div class="px p0"></div><div class="px p3"></div><div class="px p3"></div><div class="px p3"></div><div class="px p3"></div><div class="px p3"></div><div class="px p3"></div><div class="px p3"></div><div class="px p3"></div><div class="px p0"></div><div class="px p0"></div>
          </div>

          <div class="bio-name">ABENEZER NIGUSE</div>
          <div class="bio-handle">@Kal10</div>
          <hr class="bio-divider">
          <div class="bio-lines">
            <div><span class="arrow">&gt;</span><span class="text">Full-stack developer</span></div>
            <div><span class="arrow">&gt;</span><span class="text">Rotterdam, Netherlands</span></div>
            <div><span class="arrow">&gt;</span><span class="text">Open source builder</span></div>
            <div><span class="arrow">&gt;</span><span class="text"><span class="blink">_</span></span></div>
          </div>
        </div>
      </div>

      <div style="display:flex;flex-direction:column;gap:14px;">

        <!-- STATS.DAT -->
        <div class="window">
          <div class="win-title">
            [ STATS.DAT ]
            <div class="win-controls">
              <div class="wc">_</div><div class="wc">□</div><div class="wc">✕</div>
            </div>
          </div>
          <div class="win-body">
            <div class="stat-grid">
              <div class="stat-box"><span class="stat-num" data-target="387">0</span><span class="stat-lbl">COMMITS</span></div>
              <div class="stat-box"><span class="stat-num" data-target="210">0</span><span class="stat-lbl">STARS</span></div>
              <div class="stat-box"><span class="stat-num" data-target="42">0</span><span class="stat-lbl">REPOS</span></div>
              <div class="stat-box"><span class="stat-num" data-target="18">0</span><span class="stat-lbl">PRs</span></div>
            </div>
          </div>
        </div>

        <!-- SKILLS.SYS -->
        <div class="window">
          <div class="win-title">
            [ SKILLS.SYS ]
            <div class="win-controls">
              <div class="wc">_</div><div class="wc">□</div><div class="wc">✕</div>
            </div>
          </div>
          <div class="win-body">
            <div class="skill-row"><span class="sk-label">REACT</span><span class="sk-bar-wrap"><span class="sk-bar" data-pct="85"></span></span><span class="sk-pct">85%</span></div>
            <div class="skill-row"><span class="sk-label">NODE.JS</span><span class="sk-bar-wrap"><span class="sk-bar" data-pct="80"></span></span><span class="sk-pct">80%</span></div>
            <div class="skill-row"><span class="sk-label">TYPESCRIPT</span><span class="sk-bar-wrap"><span class="sk-bar" data-pct="82"></span></span><span class="sk-pct">82%</span></div>
            <div class="skill-row"><span class="sk-label">PYTHON</span><span class="sk-bar-wrap"><span class="sk-bar" data-pct="65"></span></span><span class="sk-pct">65%</span></div>
            <div class="skill-row"><span class="sk-label">DOCKER</span><span class="sk-bar-wrap"><span class="sk-bar" data-pct="55"></span></span><span class="sk-pct">55%</span></div>
          </div>
        </div>

      </div>
    </div>

    <!-- PINNED.REPOS -->
    <div class="window">
      <div class="win-title">
        [ PINNED.REPOS ]
        <div class="win-controls">
          <div class="wc">_</div><div class="wc">□</div><div class="wc">✕</div>
        </div>
      </div>
      <div class="win-body">
        <ul class="pin-list">
          <li class="pin-item">
            <span class="pin-emoji">📦</span>
            <div><div class="pin-name">weather-app</div><div class="pin-desc">Real-time weather dashboard with interactive maps & 7-day forecasts</div></div>
            <div class="pin-meta"><div>★ 84</div><div class="pin-lang">[TS]</div></div>
          </li>
          <li class="pin-item">
            <span class="pin-emoji">🤖</span>
            <div><div class="pin-name">ml-image-classifier</div><div class="pin-desc">Image classification using PyTorch with REST API for inference</div></div>
            <div class="pin-meta"><div>★ 61</div><div class="pin-lang">[PY]</div></div>
          </li>
          <li class="pin-item">
            <span class="pin-emoji">🛒</span>
            <div><div class="pin-name">ecommerce-api</div><div class="pin-desc">Scalable REST API for e-commerce with auth, payments & orders</div></div>
            <div class="pin-meta"><div>★ 43</div><div class="pin-lang">[JS]</div></div>
          </li>
          <li class="pin-item">
            <span class="pin-emoji">📊</span>
            <div><div class="pin-name">data-viz-kit</div><div class="pin-desc">Lightweight library for building interactive charts & dashboards</div></div>
            <div class="pin-meta"><div>★ 29</div><div class="pin-lang">[TS]</div></div>
          </li>
          <li class="pin-item">
            <span class="pin-emoji">🔐</span>
            <div><div class="pin-name">auth-service</div><div class="pin-desc">Plug-and-play authentication microservice with JWT & OAuth2</div></div>
            <div class="pin-meta"><div>★ 22</div><div class="pin-lang">[GO]</div></div>
          </li>
          <li class="pin-item">
            <span class="pin-emoji">📝</span>
            <div><div class="pin-name">markdown-editor</div><div class="pin-desc">Browser-based markdown editor with live preview & export options</div></div>
            <div class="pin-meta"><div>★ 17</div><div class="pin-lang">[JS]</div></div>
          </li>
        </ul>
      </div>
    </div>

    <!-- CONNECT.EXE -->
    <div class="window">
      <div class="win-title">
        [ CONNECT.EXE ]
        <div class="win-controls">
          <div class="wc">_</div><div class="wc">□</div><div class="wc">✕</div>
        </div>
      </div>
      <div class="win-body">
        <div class="connect-box">
          <div class="title">&gt; SELECT CONNECTION METHOD:</div>
          <div class="connect-row"><span class="connect-key">[1]</span><span class="connect-label">🌐 PORTFOLIO</span><span class="connect-val"><a href="https://your-site.dev" target="_blank">your-site.dev</a></span></div>
          <div class="connect-row"><span class="connect-key">[2]</span><span class="connect-label">💼 LINKEDIN</span><span class="connect-val"><a href="https://linkedin.com/in/yourhandle" target="_blank">/in/yourhandle</a></span></div>
          <div class="connect-row"><span class="connect-key">[3]</span><span class="connect-label">🐦 TWITTER/X</span><span class="connect-val"><a href="https://twitter.com/yourhandle" target="_blank">@yourhandle</a></span></div>
          <div class="connect-row"><span class="connect-key">[4]</span><span class="connect-label">📧 EMAIL</span><span class="connect-val"><a href="mailto:your@email.com">your@email.com</a></span></div>
          <div style="margin-top:10px; color: var(--green);">&gt; AWAITING INPUT<span class="blink">_</span></div>
        </div>
      </div>
    </div>

  </div>

  <!-- Bottom bar -->
  <div class="bottom-bar">
    <span>F1=ABOUT &nbsp; F2=REPOS &nbsp; F3=CONTACT &nbsp; F5=REFRESH</span>
    <span>MEM: 640K <span class="mem-bar"><span class="mem-seg active"></span><span class="mem-seg active"></span><span class="mem-seg active"></span><span class="mem-seg"></span><span class="mem-seg"></span></span></span>
  </div>

  <script>
    // Boot screen dismiss
    setTimeout(() => {
      const boot = document.getElementById('boot-screen');
      boot.style.transition = 'opacity 0.5s';
      boot.style.opacity = '0';
      setTimeout(() => boot.remove(), 500);
    }, 3800);

    // Live clock
    function updateClock() {
      const now = new Date();
      const h = String(now.getHours()).padStart(2,'0');
      const m = String(now.getMinutes()).padStart(2,'0');
      const s = String(now.getSeconds()).padStart(2,'0');
      document.getElementById('clock').textContent = `${h}:${m}:${s}`;
    }
    setInterval(updateClock, 1000);
    updateClock();

    // Animated stat counters
    function animateCounters() {
      document.querySelectorAll('.stat-num[data-target]').forEach(el => {
        const target = parseInt(el.dataset.target);
        const duration = 1800;
        const start = performance.now();
        function step(now) {
          const progress = Math.min((now - start) / duration, 1);
          const ease = 1 - Math.pow(1 - progress, 3);
          el.textContent = Math.floor(ease * target);
          if (progress < 1) requestAnimationFrame(step);
          else el.textContent = target;
        }
        requestAnimationFrame(step);
      });
    }

    // Animate skill bars
    function animateBars() {
      document.querySelectorAll('.sk-bar[data-pct]').forEach(el => {
        setTimeout(() => {
          el.style.width = el.dataset.pct + '%';
        }, 200);
      });
    }

    // Trigger after boot
    setTimeout(() => {
      animateCounters();
      animateBars();
    }, 4000);

    // F-key shortcuts hint
    document.addEventListener('keydown', e => {
      if (e.key === 'F5') { e.preventDefault(); location.reload(); }
    });
  </script>
</body>
</html>
