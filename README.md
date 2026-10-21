<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>HEXAI All-in-One — Live README</title>

<!-- ============================================================
     HEXAI ALL-IN-ONE — SINGLE FILE ANIMATED README / DASHBOARD
     Owner : HexSleuth
     Repo  : https://github.com/HexSleuth/HEXAI-All-in-One
     ============================================================ -->

<style>
  /* ---------- RESET & THEME TOKENS ---------- */
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root{
    --bg-0:#05060a;
    --bg-1:#0a0e18;
    --bg-2:#0f1522;
    --glass:rgba(255,255,255,.045);
    --stroke:rgba(255,255,255,.10);
    --cyan:#00f0ff;
    --magenta:#ff00e5;
    --violet:#8b5cf6;
    --lime:#a3ff12;
    --amber:#ffb020;
    --text:#e8eefc;
    --muted:#8894b0;
    --radius:18px;
    --mono:'JetBrains Mono','Fira Code',ui-monospace,SFMono-Regular,Menlo,monospace;
    --sans:'Inter',system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;
  }

  html{ scroll-behavior:smooth; }

  body{
    background:
      radial-gradient(1100px 600px at 12% -8%, rgba(0,240,255,.14), transparent 60%),
      radial-gradient(900px 520px at 88% 0%, rgba(255,0,229,.12), transparent 62%),
      radial-gradient(900px 700px at 50% 110%, rgba(139,92,246,.12), transparent 65%),
      linear-gradient(180deg,var(--bg-0) 0%, var(--bg-1) 45%, var(--bg-0) 100%);
    color:var(--text);
    font-family:var(--sans);
    line-height:1.65;
    min-height:100vh;
    overflow-x:hidden;
    -webkit-font-smoothing:antialiased;
  }

  /* ---------- ANIMATED GRID / SCANLINE BACKDROP ---------- */
  .backdrop{
    position:fixed; inset:0; z-index:0; pointer-events:none;
    background-image:
      linear-gradient(rgba(0,240,255,.055) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,240,255,.055) 1px, transparent 1px);
    background-size:56px 56px;
    mask-image:radial-gradient(ellipse at 50% 0%, #000 0%, transparent 78%);
    -webkit-mask-image:radial-gradient(ellipse at 50% 0%, #000 0%, transparent 78%);
    animation:gridDrift 22s linear infinite;
  }
  @keyframes gridDrift{
    from{ background-position:0 0, 0 0; }
    to  { background-position:56px 56px, 56px 56px; }
  }

  .scanline{
    position:fixed; left:0; right:0; height:180px; z-index:0; pointer-events:none;
    background:linear-gradient(180deg, transparent, rgba(0,240,255,.055), transparent);
    animation:scan 9s ease-in-out infinite;
  }
  @keyframes scan{
    0%  { transform:translateY(-220px); opacity:0; }
    35% { opacity:1; }
    100%{ transform:translateY(105vh); opacity:0; }
  }

  /* ---------- LAYOUT ---------- */
  .wrap{
    position:relative; z-index:1;
    max-width:1080px;
    margin:0 auto;
    padding:34px 20px 90px;
  }

  /* ---------- HERO ---------- */
  .hero{
    text-align:center;
    padding:38px 18px 30px;
    border:1px solid var(--stroke);
    border-radius:26px;
    background:
      linear-gradient(180deg, rgba(255,255,255,.05), rgba(255,255,255,.012));
    backdrop-filter:blur(14px);
    -webkit-backdrop-filter:blur(14px);
    box-shadow:
      0 0 0 1px rgba(0,240,255,.07) inset,
      0 30px 90px -40px rgba(0,240,255,.45),
      0 30px 90px -60px rgba(255,0,229,.45);
    position:relative;
    overflow:hidden;
  }

  /* rotating conic border glow */
  .hero::before{
    content:"";
    position:absolute; inset:-2px; z-index:-1;
    background:conic-gradient(from 0deg,
      var(--cyan), var(--violet), var(--magenta), var(--lime), var(--cyan));
    filter:blur(26px);
    opacity:.42;
    animation:spin 9s linear infinite;
  }
  @keyframes spin{ to{ transform:rotate(360deg); } }

  .hero-badge{
    display:inline-flex; align-items:center; gap:9px;
    font-family:var(--mono); font-size:.70rem; letter-spacing:.22em;
    text-transform:uppercase; color:var(--cyan);
    border:1px solid rgba(0,240,255,.35);
    background:rgba(0,240,255,.07);
    padding:7px 15px; border-radius:999px;
    margin-bottom:20px;
    animation:pulseGlow 2.6s ease-in-out infinite;
  }
  @keyframes pulseGlow{
    0%,100%{ box-shadow:0 0 0 0 rgba(0,240,255,.35); }
    50%    { box-shadow:0 0 22px 3px rgba(0,240,255,.28); }
  }

  .dot{
    width:7px; height:7px; border-radius:50%;
    background:var(--lime);
    box-shadow:0 0 10px var(--lime);
    animation:blink 1.4s ease-in-out infinite;
  }
  @keyframes blink{ 0%,100%{opacity:1} 50%{opacity:.18} }

  h1.title{
    font-size:clamp(2.05rem, 6.4vw, 3.5rem);
    font-weight:900;
    letter-spacing:-.03em;
    line-height:1.06;
    background:linear-gradient(100deg,var(--cyan) 0%,#7dd3fc 22%,var(--violet) 52%,var(--magenta) 78%,var(--cyan) 100%);
    background-size:280% 100%;
    -webkit-background-clip:text; background-clip:text;
    -webkit-text-fill-color:transparent; color:transparent;
    animation:gradientShift 7s linear infinite;
    margin-bottom:12px;
  }
  @keyframes gradientShift{
    0%  { background-position:0% 50%; }
    100%{ background-position:280% 50%; }
  }

  .tagline{
    color:var(--muted);
    font-size:clamp(.94rem,2.1vw,1.08rem);
    max-width:660px; margin:0 auto 6px;
  }
  .tagline b{ color:var(--text); font-weight:600; }

  /* typing line */
  .typer{
    font-family:var(--mono);
    font-size:clamp(.82rem,2.3vw,1.02rem);
    color:var(--cyan);
    margin-top:18px;
    min-height:1.7em;
    text-shadow:0 0 16px rgba(0,240,255,.5);
  }
  .typer .caret{
    display:inline-block; width:9px; height:1.05em;
    background:var(--cyan); margin-left:3px; vertical-align:-2px;
    animation:blink .9s step-end infinite;
    box-shadow:0 0 12px var(--cyan);
  }

  /* ---------- SECTION ---------- */
  section{ margin-top:52px; }

  .sec-head{
    display:flex; align-items:center; gap:14px;
    margin-bottom:22px;
  }
  .sec-head h2{
    font-size:1.16rem; font-weight:800; letter-spacing:.02em;
    white-space:nowrap;
  }
  .sec-head .line{
    flex:1; height:1px;
    background:linear-gradient(90deg, rgba(0,240,255,.55), rgba(255,0,229,.35), transparent);
    position:relative; overflow:hidden;
  }
  .sec-head .line::after{
    content:""; position:absolute; top:0; left:-40%;
    width:40%; height:100%;
    background:linear-gradient(90deg,transparent,var(--cyan),transparent);
    animation:sweep 3.4s ease-in-out infinite;
  }
  @keyframes sweep{
    0%{ left:-45%; } 100%{ left:110%; }
  }

  /* ---------- BADGE WALL (REALTIME) ---------- */
  .badge-wall{
    display:flex; flex-wrap:wrap; gap:10px;
    justify-content:center;
    padding:22px 16px;
    border:1px solid var(--stroke);
    border-radius:var(--radius);
    background:var(--glass);
    backdrop-filter:blur(10px);
    -webkit-backdrop-filter:blur(10px);
  }

  .badge-wall a,
  .stack a{
    display:inline-block;
    transition:transform .25s cubic-bezier(.2,.8,.2,1), filter .25s ease;
    filter:saturate(.92);
  }
  .badge-wall a:hover,
  .stack a:hover{
    transform:translateY(-4px) scale(1.06);
    filter:saturate(1.35) drop-shadow(0 0 12px rgba(0,240,255,.65));
  }

  .badge-wall img,
  .stack img{
    height:28px; display:block; border-radius:6px;
  }

  /* ---------- CARD GRID ---------- */
  .grid{
    display:grid;
    grid-template-columns:repeat(auto-fit, minmax(250px,1fr));
    gap:16px;
  }

  .card{
    position:relative;
    border:1px solid var(--stroke);
    border-radius:var(--radius);
    background:linear-gradient(180deg, rgba(255,255,255,.055), rgba(255,255,255,.012));
    padding:22px 20px 20px;
    overflow:hidden;
    transition:transform .35s cubic-bezier(.2,.8,.2,1), border-color .35s ease, box-shadow .35s ease;
  }
  .card::after{ /* sheen */
    content:"";
    position:absolute; top:0; left:-120%; width:60%; height:100%;
    background:linear-gradient(100deg,transparent,rgba(0,240,255,.13),transparent);
    transform:skewX(-18deg);
    transition:left .65s ease;
  }
  .card:hover{
    transform:translateY(-6px);
    border-color:rgba(0,240,255,.42);
    box-shadow:0 24px 60px -30px rgba(0,240,255,.55);
  }
  .card:hover::after{ left:130%; }

  .card .ico{
    font-size:1.55rem; line-height:1;
    display:inline-block; margin-bottom:12px;
    filter:drop-shadow(0 0 12px rgba(0,240,255,.5));
  }
  .card h3{
    font-size:.98rem; font-weight:750; margin-bottom:7px; letter-spacing:.01em;
  }
  .card p{
    font-size:.855rem; color:var(--muted); line-height:1.62;
  }

  /* ---------- LIVE STAT STRIP ---------- */
  .stats{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(150px,1fr));
    gap:12px;
  }
  .stat{
    text-align:center;
    padding:20px 12px;
    border:1px solid var(--stroke);
    border-radius:14px;
    background:var(--glass);
    transition:border-color .3s, transform .3s, background .3s;
  }
  .stat:hover{
    border-color:rgba(255,0,229,.4);
    transform:translateY(-4px);
    background:rgba(255,0,229,.055);
  }
  .stat .val{
    font-family:var(--mono);
    font-size:1.55rem; font-weight:800;
    color:var(--cyan);
    text-shadow:0 0 20px rgba(0,240,255,.55);
    line-height:1.15;
    transition:color .3s;
  }
  .stat:hover .val{ color:var(--magenta); text-shadow:0 0 22px rgba(255,0,229,.6); }
  .stat .lbl{
    font-size:.66rem; letter-spacing:.2em; text-transform:uppercase;
    color:var(--muted); margin-top:6px; font-family:var(--mono);
  }

  /* ---------- CODE BLOCKS ---------- */
  pre{
    position:relative;
    background:#070b13;
    border:1px solid rgba(0,240,255,.16);
    border-radius:14px;
    padding:20px 18px 18px;
    overflow-x:auto;
    font-family:var(--mono);
    font-size:.845rem;
    line-height:1.85;
    color:#c9d6f0;
    box-shadow:inset 0 0 40px rgba(0,240,255,.045);
    margin-bottom:14px;
  }
  pre::before{
    content:attr(data-label);
    position:absolute; top:0; left:0;
    font-size:.6rem; letter-spacing:.18em; text-transform:uppercase;
    color:var(--cyan);
    background:rgba(0,240,255,.1);
    border-right:1px solid rgba(0,240,255,.2);
    border-bottom:1px solid rgba(0,240,255,.2);
    padding:3px 11px; border-radius:13px 0 11px 0;
  }
  pre code{ display:block; margin-top:12px; }
  .c-comment{ color:#4d5d7d; }
  .c-key{ color:var(--magenta); }
  .c-str{ color:var(--lime); }
  .c-cmd{ color:var(--cyan); }

  /* ---------- FEATURE LIST ---------- */
  .features{
    display:grid; gap:10px;
  }
  .feature{
    display:flex; gap:14px; align-items:flex-start;
    padding:14px 16px;
    border:1px solid var(--stroke);
    border-radius:12px;
    background:rgba(255,255,255,.028);
    transition:background .3s, border-color .3s, transform .3s;
  }
  .feature:hover{
    background:rgba(0,240,255,.055);
    border-color:rgba(0,240,255,.33);
    transform:translateX(5px);
  }
  .feature .fi{
    font-size:1.05rem; line-height:1.5; flex:0 0 auto;
  }
  .feature strong{ display:block; font-size:.9rem; margin-bottom:2px; }
  .feature span{ font-size:.83rem; color:var(--muted); }

  /* ---------- STACK ---------- */
  .stack{
    display:flex; flex-wrap:wrap; gap:9px;
    padding:20px 16px;
    border:1px solid var(--stroke);
    border-radius:var(--radius);
    background:var(--glass);
  }
  .stack img{ height:26px; }

  /* ---------- TREE ---------- */
  .tree{
    font-family:var(--mono);
    font-size:.82rem;
    line-height:2;
    color:#9fb0cf;
    background:#070b13;
    border:1px solid rgba(139,92,246,.22);
    border-radius:14px;
    padding:20px 18px;
    overflow-x:auto;
    box-shadow:inset 0 0 44px rgba(139,92,246,.07);
  }
  .tree b{ color:var(--cyan); font-weight:600; }
  .tree i{ color:#55647f; font-style:normal; }

  /* ---------- ACTIVITY GRAPH WRAP ---------- */
  .graph-box{
    border:1px solid var(--stroke);
    border-radius:var(--radius);
    background:var(--glass);
    padding:16px;
    overflow:hidden;
  }
  .graph-box img{ width:100%; height:auto; display:block; border-radius:10px; }

  /* ---------- FOOTER ---------- */
  footer{
    margin-top:64px;
    text-align:center;
    padding-top:30px;
    border-top:1px solid var(--stroke);
  }
  footer .glow{
    font-family:var(--mono);
    font-size:.78rem;
    letter-spacing:.16em;
    text-transform:uppercase;
    color:var(--muted);
  }
  footer .sig{
    margin-top:10px;
    font-size:.86rem;
    color:var(--muted);
  }
  footer .sig a{
    color:var(--cyan);
    text-decoration:none;
    border-bottom:1px dashed rgba(0,240,255,.4);
    transition:color .25s, border-color .25s;
  }
  footer .sig a:hover{ color:var(--magenta); border-color:var(--magenta); }

  /* ---------- REVEAL ON SCROLL ---------- */
  .reveal{
    opacity:0;
    transform:translateY(26px);
    transition:opacity .7s cubic-bezier(.2,.8,.2,1), transform .7s cubic-bezier(.2,.8,.2,1);
    will-change:opacity, transform;
  }
  .reveal.in{ opacity:1; transform:none; }

  /* ---------- RESPONSIVE ---------- */
  @media (max-width:640px){
    .wrap{ padding:20px 14px 70px; }
    .hero{ padding:30px 14px 26px; border-radius:20px; }
    .badge-wall img, .stack img{ height:24px; }
    .stat .val{ font-size:1.25rem; }
  }

  /* ---------- REDUCED MOTION ---------- */
  @media (prefers-reduced-motion: reduce){
    *, *::before, *::after{
      animation-duration:.001ms !important;
      animation-iteration-count:1 !important;
      transition-duration:.001ms !important;
    }
    .reveal{ opacity:1; transform:none; }
  }
</style>
</head>

<body>

<div class="backdrop" aria-hidden="true"></div>
<div class="scanline" aria-hidden="true"></div>

<div class="wrap">

  <!-- ══════════════════════════════════════════════════════
       HERO
       ══════════════════════════════════════════════════════ -->
  <header class="hero">
    <div class="hero-badge">
      <span class="dot" aria-hidden="true"></span>
      HexSleuth / HEXAI-All-in-One
    </div>

    <h1 class="title">⚡ HEXAI All-in-One ⚡</h1>

    <p class="tagline">
      <b>The Ultimate Multi-Tool AI Ecosystem &amp; Toolkit</b> —
      streamline your development, automation, and AI workflows
      under a single powerful interface.
    </p>

    <div class="typer" id="typer" aria-live="polite">
      <span id="typerText"></span><span class="caret" aria-hidden="true"></span>
    </div>
  </header>

  <!-- ══════════════════════════════════════════════════════
       REALTIME BADGES
       ══════════════════════════════════════════════════════ -->
  <section class="reveal" id="badges">
    <div class="sec-head">
      <h2>📡 Live Repository Telemetry</h2>
      <div class="line"></div>
    </div>

    <div class="badge-wall">
      <a href="https://github.com/HexSleuth/HEXAI-All-in-One/stargazers">
        <img alt="Stars" src="https://img.shields.io/github/stars/HexSleuth/HEXAI-All-in-One?style=for-the-badge&logo=github&logoColor=white&label=Stars&labelColor=0d1117&color=00f0ff" />
      </a>
      <a href="https://github.com/HexSleuth/HEXAI-All-in-One/network/members">
        <img alt="Forks" src="https://img.shields.io/github/forks/HexSleuth/HEXAI-All-in-One?style=for-the-badge&logo=git&logoColor=white&label=Forks&labelColor=0d1117&color=ff00e5" />
      </a>
      <a href="https://github.com/HexSleuth/HEXAI-All-in-One/watchers">
        <img alt="Watchers" src="https://img.shields.io/github/watchers/HexSleuth/HEXAI-All-in-One?style=for-the-badge&logo=eye&logoColor=white&label=Watchers&labelColor=0d1117&color=8b5cf6" />
      </a>
      <a href="https://github.com/HexSleuth/HEXAI-All-in-One/issues">
        <img alt="Issues" src="https://img.shields.io/github/issues/HexSleuth/HEXAI-All-in-One?style=for-the-badge&logo=githubissues&logoColor=white&label=Issues&labelColor=0d1117&color=ffb020" />
      </a>
      <a href="https://github.com/HexSleuth/HEXAI-All-in-One/pulls">
        <img alt="Pull Requests" src="https://img.shields.io/github/issues-pr/HexSleuth/HEXAI-All-in-One?style=for-the-badge&logo=gitpullrequest&logoColor=white&label=PRs&labelColor=0d1117&color=a3ff12" />
      </a>
      <a href="https://github.com/HexSleuth/HEXAI-All-in-One/graphs/contributors">
        <img alt="Contributors" src="https://img.shields.io/github/contributors/HexSleuth/HEXAI-All-in-One?style=for-the-badge&logo=contributorcovenant&logoColor=white&label=Contributors&labelColor=0d1117&color=00f0ff" />
      </a>
      <a href="https://github.com/HexSleuth/HEXAI-All-in-One/commits">
        <img alt="Last Commit" src="https://img.shields.io/github/last-commit/HexSleuth/HEXAI-All-in-One?style=for-the-badge&logo=git&logoColor=white&label=Last%20Commit&labelColor=0d1117&color=ff00e5" />
      </a>
      <a href="https://github.com/HexSleuth/HEXAI-All-in-One/pulse">
        <img alt="Commit Activity" src="https://img.shields.io/github/commit-activity/m/HexSleuth/HEXAI-All-in-One?style=for-the-badge&logo=githubactions&logoColor=white&label=Commits%2FMonth&labelColor=0d1117&color=8b5cf6" />
      </a>
      <a href="https://github.com/HexSleuth/HEXAI-All-in-One/releases">
        <img alt="Release" src="https://img.shields.io/github/v/release/HexSleuth/HEXAI-All-in-One?style=for-the-badge&logo=github&logoColor=white&label=Release&labelColor=0d1117&color=a3ff12&include_prereleases" />
      </a>
      <a href="https://github.com/HexSleuth/HEXAI-All-in-One/blob/main/LICENSE">
        <img alt="License" src="https://img.shields.io/github/license/HexSleuth/HEXAI-All-in-One?style=for-the-badge&logo=opensourceinitiative&logoColor=white&label=License&labelColor=0d1117&color=ffb020" />
      </a>
      <a href="https://github.com/HexSleuth/HEXAI-All-in-One">
        <img alt="Repo Size" src="https://img.shields.io/github/repo-size/HexSleuth/HEXAI-All-in-One?style=for-the-badge&logo=databricks&logoColor=white&label=Repo%20Size&labelColor=0d1117&color=00f0ff" />
      </a>
      <a href="https://github.com/HexSleuth/HEXAI-All-in-One">
        <img alt="Top Language" src="https://img.shields.io/github/languages/top/HexSleuth/HEXAI-All-in-One?style=for-the-badge&logo=python&logoColor=white&label=Top%20Lang&labelColor=0d1117&color=ff00e5" />
      </a>
      <a href="https://github.com/HexSleuth/HEXAI-All-in-One/actions">
        <img alt="Build Status" src="https://img.shields.io/github/actions/workflow/status/HexSleuth/HEXAI-All-in-One/static.yml?style=for-the-badge&logo=githubactions&logoColor=white&label=Build&labelColor=0d1117&color=a3ff12" />
      </a>
      <a href="https://github.com/HexSleuth">
        <img alt="Followers" src="https://img.shields.io/github/followers/HexSleuth?style=for-the-badge&logo=github&logoColor=white&label=Followers&labelColor=0d1117&color=8b5cf6" />
      </a>
      <a href="https://github.com/HexSleuth/HEXAI-All-in-One">
        <img alt="Visitors" src="https://komarev.com/ghpvc/?username=HexSleuth&repo=HEXAI-All-in-One&style=for-the-badge&label=VISITORS&color=00f0ff" />
      </a>
      <a href="https://github.com/HexSleuth/HEXAI-All-in-One">
        <img alt="Status" src="https://img.shields.io/badge/STATUS-ACTIVE%20DEVELOPMENT-a3ff12?style=for-the-badge&labelColor=0d1117&logo=statuspage&logoColor=white" />
      </a>
    </div>
  </section>

  <!-- ══════════════════════════════════════════════════════
       LIVE STAT STRIP
       ══════════════════════════════════════════════════════ -->
  <section class="reveal" id="live">
    <div class="sec-head">
      <h2>📊 Live Snapshot</h2>
      <div class="line"></div>
    </div>

    <div class="stats">
      <div class="stat"><div class="val" data-live="stars">—</div><div class="lbl">Stars</div></div>
      <div class="stat"><div class="val" data-live="forks">—</div><div class="lbl">Forks</div></div>
      <div class="stat"><div class="val" data-live="issues">—</div><div class="lbl">Open Issues</div></div>
      <div class="stat"><div class="val" data-live="watchers">—</div><div class="lbl">Watchers</div></div>
      <div class="stat"><div class="val" data-live="size">—</div><div class="lbl">Size (KB)</div></div>
      <div class="stat"><div class="val" data-live="lang">—</div><div class="lbl">Top Language</div></div>
    </div>
  </section>

  <!-- ══════════════════════════════════════════════════════
       ABOUT
       ══════════════════════════════════════════════════════ -->
  <section class="reveal" id="about">
    <div class="sec-head">
      <h2>📖 About The Project</h2>
      <div class="line"></div>
    </div>

    <div class="card" style="padding:24px 22px;">
      <p style="font-size:.92rem; color:#b9c6e0; line-height:1.8;">
        <b style="color:var(--cyan);">HEXAI-All-in-One</b> is engineered to bridge the gap between
        fragmented artificial intelligence models and developer productivity. Whether you are looking
        to orchestrate multi-agent pipelines, leverage state-of-the-art NLP models locally or via cloud
        wrappers, or script complex data workflows — HEXAI packages it into an accessible,
        high-performance ecosystem.
      </p>
    </div>
  </section>

  <!-- ══════════════════════════════════════════════════════
       FEATURES
       ══════════════════════════════════════════════════════ -->
  <section class="reveal" id="features">
    <div class="sec-head">
      <h2>✨ Key Features</h2>
      <div class="line"></div>
    </div>

    <div class="grid">
      <div class="card">
        <span class="ico">🚀</span>
        <h3>Unified AI Orchestration</h3>
        <p>Connect and switch seamlessly between multiple AI providers and local models.</p>
      </div>
      <div class="card">
        <span class="ico">🛠️</span>
        <h3>Modular Toolkits</h3>
        <p>Pre-built plugins and hooks for data scraping, code generation, summarization, and task management.</p>
      </div>
      <div class="card">
        <span class="ico">⚡</span>
        <h3>High Performance</h3>
        <p>Optimized architecture designed for asynchronous execution with low latency.</p>
      </div>
      <div class="card">
        <span class="ico">🔒</span>
        <h3>Secure &amp; Privacy-First</h3>
        <p>Strict data handling controls with customizable local-first preferences.</p>
      </div>
      <div class="card">
        <span class="ico">📦</span>
        <h3>Extensible Plugin System</h3>
        <p>Easily write custom tools and integrate them directly into your workflow.</p>
      </div>
      <div class="card">
        <span class="ico">🧩</span>
        <h3>Drop-In Integrations</h3>
        <p>REST &amp; WebSocket endpoints plus containerized deployment out of the box.</p>
      </div>
    </div>
  </section>

  <!-- ══════════════════════════════════════════════════════
       TECH STACK
       ══════════════════════════════════════════════════════ -->
  <section class="reveal" id="stack">
    <div class="sec-head">
      <h2>🛠️ Built With</h2>
      <div class="line"></div>
    </div>

    <div class="stack">
      <a href="https://www.python.org/"><img alt="Python" src="https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white&labelColor=0d1117" /></a>
      <a href="https://nodejs.org/"><img alt="Node.js" src="https://img.shields.io/badge/Node.js-18%2B-339933?style=for-the-badge&logo=nodedotjs&logoColor=white&labelColor=0d1117" /></a>
      <a href="https://www.typescriptlang.org/"><img alt="TypeScript" src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white&labelColor=0d1117" /></a>
      <a href="https://fastapi.tiangolo.com/"><img alt="FastAPI" src="https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white&labelColor=0d1117" /></a>
      <a href="https://www.docker.com/"><img alt="Docker" src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white&labelColor=0d1117" /></a>
      <a href="https://git-scm.com/"><img alt="Git" src="https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white&labelColor=0d1117" /></a>
      <a href="https://github.com/features/actions"><img alt="GitHub Actions" src="https://img.shields.io/badge/GitHub%20Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white&labelColor=0d1117" /></a>
      <a href="https://developer.mozilla.org/docs/Web/API/WebSockets_API"><img alt="WebSocket" src="https://img.shields.io/badge/WebSocket-010101?style=for-the-badge&logo=socketdotio&logoColor=white&labelColor=0d1117" /></a>
      <a href="https://www.markdownguide.org/"><img alt="Markdown" src="https://img.shields.io/badge/Markdown-000000?style=for-the-badge&logo=markdown&logoColor=white&labelColor=0d1117" /></a>
    </div>
  </section>

  <!-- ══════════════════════════════════════════════════════
       GETTING STARTED
       ══════════════════════════════════════════════════════ -->
  <section class="reveal" id="start">
    <div class="sec-head">
      <h2>🚀 Getting Started</h2>
      <div class="line"></div>
    </div>

    <div class="features" style="margin-bottom:20px;">
      <div class="feature">
        <span class="fi">🐍</span>
        <div>
          <strong>Python 3.10+</strong>
          <span>or Node.js 18+ installed — depending on your environment preference.</span>
        </div>
      </div>
      <div class="feature">
        <span class="fi">🐳</span>
        <div>
          <strong>Docker (optional)</strong>
          <span>For containerized deployments.</span>
        </div>
      </div>
    </div>

    <pre data-label="1 · Clone"><code><span class="c-comment"># Clone the repository</span>
<span class="c-cmd">git clone</span> <span class="c-str">https://github.com/HexSleuth/HEXAI-All-in-One.git</span>
<span class="c-cmd">cd</span> HEXAI-All-in-One</code></pre>

    <pre data-label="2 · Configure"><code><span class="c-cmd">cp</span> .env.example .env

<span class="c-comment"># Edit .env and insert your API keys and configuration parameters</span></code></pre>

    <pre data-label="3 · Install"><code><span class="c-cmd">pip install</span> -r requirements.txt

<span class="c-comment"># OR if using npm / pnpm</span>
<span class="c-cmd">npm install</span></code></pre>

    <pre data-label="4 · Run"><code><span class="c-cmd">python</span> main.py

<span class="c-comment"># OR</span>
<span class="c-cmd">npm run</span> start</code></pre>

    <pre data-label="5 · Docker (optional)"><code><span class="c-cmd">docker build</span> -t hexai-all-in-one .
<span class="c-cmd">docker run</span> --env-file .env -p 8000:8000 hexai-all-in-one</code></pre>
  </section>

  <!-- ══════════════════════════════════════════════════════
       PROJECT STRUCTURE
       ══════════════════════════════════════════════════════ -->
  <section class="reveal" id="structure">
    <div class="sec-head">
      <h2>📂 Project Structure</h2>
      <div class="line"></div>
    </div>

    <div class="tree">
HEXAI-All-in-One/<br />
├── <b>core/</b>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<i># Core orchestrator and execution engines</i><br />
├── <b>plugins/</b>&nbsp;&nbsp;&nbsp;<i># Extensible toolkit modules &amp; integrations</i><br />
├── <b>api/</b>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<i># REST &amp; WebSocket endpoints</i><br />
├── <b>config/</b>&nbsp;&nbsp;&nbsp;&nbsp;<i># Configuration files and schemas</i><br />
├── <b>tests/</b>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<i># Automated test suites</i><br />
├── <b>Dockerfile</b>&nbsp;<i># Container configuration</i><br />
└── <b>README.md</b>&nbsp;&nbsp;<i># You are here</i>
    </div>
  </section>

  <!-- ══════════════════════════════════════════════════════
       ACTIVITY GRAPH (REALTIME)
       ══════════════════════════════════════════════════════ -->
  <section class="reveal" id="activity">
    <div class="sec-head">
      <h2>📈 Contribution Pulse</h2>
      <div class="line"></div>
    </div>

    <div class="graph-box">
      <img
        alt="HEXAI activity graph"
        src="https://github-readme-activity-graph.vercel.app/graph?username=HexSleuth&repo=HEXAI-All-in-One&theme=react-dark&hide_border=true&area=true&custom_title=HEXAI%20All-in-One%20Activity"
        loading="lazy"
      />
    </div>
  </section>

  <!-- ══════════════════════════════════════════════════════
       CONTRIBUTING
       ══════════════════════════════════════════════════════ -->
  <section class="reveal" id="contributing">
    <div class="sec-head">
      <h2>🤝 Contributing</h2>
      <div class="line"></div>
    </div>

    <div class="grid">
      <div class="card">
        <span class="ico">🍴</span>
        <h3>Fork &amp; Branch</h3>
        <p>Fork the repo, create a feature branch, and keep commits focused and descriptive.</p>
      </div>
      <div class="card">
        <span class="ico">🧪</span>
        <h3>Test Locally</h3>
        <p>Run the test suite under <code>tests/</code> before opening a pull request.</p>
      </div>
      <div class="card">
        <span class="ico">🚀</span>
        <h3>Open a PR</h3>
        <p>Describe the change, link related issues, and tag a maintainer for review.</p>
      </div>
    </div>
  </section>

  <!-- ══════════════════════════════════════════════════════
       FOOTER
       ══════════════════════════════════════════════════════ -->
  <footer>
    <div class="glow">⚡ Built for builders · Powered by HexSleuth ⚡</div>
    <p class="sig">
      Crafted with 🖤 by
      <a href="https://github.com/HexSleuth" target="_blank" rel="noopener">HexSleuth</a>
      &nbsp;·&nbsp;
      <a href="https://github.com/HexSleuth/HEXAI-All-in-One" target="_blank" rel="noopener">HEXAI-All-in-One</a>
    </p>
    <p class="sig" style="margin-top:14px;">
      <a href="https://github.com/HexSleuth/HEXAI-All-in-One/stargazers" target="_blank" rel="noopener">⭐ Star the repo</a>
      &nbsp;·&nbsp;
      <a href="https://github.com/HexSleuth/HEXAI-All-in-One/issues" target="_blank" rel="noopener">🐛 Report an issue</a>
      &nbsp;·&nbsp;
      <a href="https://github.com/HexSleuth/HEXAI-All-in-One/fork" target="_blank" rel="noopener">🍴 Fork it</a>
    </p>
  </footer>

</div>

<!-- ════════════════════════════════════════════════════════
     SCRIPTS — typing effect, scroll reveal, live GitHub API
     ════════════════════════════════════════════════════════ -->
<script>
(function () {
  'use strict';

  /* ------------------------------------------------------
     1. TYPING / ROTATING TAGLINE
     ------------------------------------------------------ */
  var PHRASES = [
    'Unified AI Orchestration ⚡',
    'Modular Toolkits 🛠️',
    'Low Latency · Privacy First 🔒',
    'Extensible Plugin System 📦',
    'One Interface. Every Model. 🚀'
  ];

  var typerEl = document.getElementById('typerText');
  var pIdx = 0, cIdx = 0, deleting = false;

  function tick() {
    var phrase = PHRASES[pIdx];
    if (!deleting) {
      cIdx++;
      typerEl.textContent = phrase.slice(0, cIdx);
      if (cIdx === phrase.length) {
        deleting = true;
        return setTimeout(tick, 1700);
      }
      return setTimeout(tick, 55 + Math.random() * 45);
    }
    cIdx--;
    typerEl.textContent = phrase.slice(0, cIdx);
    if (cIdx === 0) {
      deleting = false;
      pIdx = (pIdx + 1) % PHRASES.length;
      return setTimeout(tick, 320);
    }
    return setTimeout(tick, 26);
  }

  if (typerEl) setTimeout(tick, 500);

  /* ------------------------------------------------------
     2. SCROLL REVEAL
     ------------------------------------------------------ */
  var revealEls = document.querySelectorAll('.reveal');

  if ('IntersectionObserver' in window) {
    var io = new IntersectionObserver(function (entries) {
      entries.forEach(function (entry) {
        if (entry.isIntersecting) {
          entry.target.classList.add('in');
          io.unobserve(entry.target);
        }
      });
    }, { threshold: 0.12, rootMargin: '0px 0px -60px 0px' });

    revealEls.forEach(function (el) { io.observe(el); });
  } else {
    revealEls.forEach(function (el) { el.classList.add('in'); });
  }

  /* ------------------------------------------------------
     3. LIVE GITHUB REPO STATS (public API, no auth)
        Falls back to shields.io badge scraping if rate-limited
     ------------------------------------------------------ */
  var OWNER = 'HexSleuth';
  var REPO  = 'HEXAI-All-in-One';
  var API   = 'https://api.github.com/repos/' + OWNER + '/' + REPO;

  function setStat(key, value) {
    var el = document.querySelector('[data-live="' + key + '"]');
    if (el && value !== undefined && value !== null) {
      el.textContent = value;
    }
  }

  function animateNumber(el, target) {
    var start = 0;
    var duration = 900;
    var t0 = performance.now();

    function frame(now) {
      var p = Math.min((now - t0) / duration, 1);
      var eased = 1 - Math.pow(1 - p, 3);
      el.textContent = Math.round(start + (target - start) * eased).toLocaleString();
      if (p < 1) requestAnimationFrame(frame);
    }
    requestAnimationFrame(frame);
  }

  function applyRepoData(data) {
    ['stars', 'forks', 'issues', 'watchers'].forEach(function (key) {
      var el = document.querySelector('[data-live="' + key + '"]');
      if (!el) return;
      var map = {
        stars: data.stargazers_count,
        forks: data.forks_count,
        issues: data.open_issues_count,
        watchers: data.subscribers_count
      };
      if (typeof map[key] === 'number') animateNumber(el, map[key]);
    });

    if (typeof data.size === 'number') setStat('size', data.size.toLocaleString());
    if (data.language) setStat('lang', data.language);
  }

  function fetchStats() {
    if (!('fetch' in window)) return;

    fetch(API, { headers: { Accept: 'application/vnd.github+json' } })
      .then(function (r) {
        if (!r.ok) throw new Error('GitHub API responded ' + r.status);
        return r.json();
      })
      .then(applyRepoData)
      .catch(function () {
        /* Graceful fallback: leave em-dashes, badges still show live data */
        console.info('[HEXAI] Live API unavailable — shields.io badges remain authoritative.');
      });
  }

  fetchStats();
  /* Refresh every 60s so the dashboard stays warm */
  setInterval(fetchStats, 60000);

  /* ------------------------------------------------------
     4. SUBTLE PARALLAX ON HERO GLOW
     ------------------------------------------------------ */
  var hero = document.querySelector('.hero');
  if (hero && window.matchMedia('(pointer:fine)').matches) {
    window.addEventListener('mousemove', function (e) {
      var x = (e.clientX / window.innerWidth - 0.5) * 14;
      var y = (e.clientY / window.innerHeight - 0.5) * 14;
      hero.style.transform = 'perspective(1200px) rotateX(' + (-y * 0.16) + 'deg) rotateY(' + (x * 0.16) + 'deg)';
    }, { passive: true });

    window.addEventListener('mouseleave', function () {
      hero.style.transform = 'none';
    });
  }
})();
</script>

</body>
</html>
