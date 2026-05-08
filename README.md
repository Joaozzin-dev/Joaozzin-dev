<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>João Pedro — README</title>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Orbitron:wght@400;700;900&family=Press+Start+2P&display=swap" rel="stylesheet">
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}

:root{
  --bg:#020509;
  --bg2:#050d14;
  --cyan:#00fff5;
  --yellow:#ffe600;
  --magenta:#ff2079;
  --green:#39ff14;
  --dim:#0a1a24;
  --text:#c8e8f0;
  --muted:#3a6070;
  --pixel:4px;
}

html{scroll-behavior:smooth}
body{
  font-family:'Share Tech Mono',monospace;
  background:var(--bg);
  color:var(--text);
  overflow-x:hidden;
  cursor:none;
  min-height:100vh;
}

/* scanlines */
body::before{
  content:'';position:fixed;inset:0;
  background:repeating-linear-gradient(0deg,transparent,transparent 3px,rgba(0,0,0,0.12) 3px,rgba(0,0,0,0.12) 4px);
  pointer-events:none;z-index:9000;
}
/* vignette */
body::after{
  content:'';position:fixed;inset:0;
  background:radial-gradient(ellipse at center,transparent 55%,rgba(0,0,0,0.7) 100%);
  pointer-events:none;z-index:8999;
}

/* CURSOR */
.cur{position:fixed;width:16px;height:16px;pointer-events:none;z-index:9999;transform:translate(-50%,-50%)}
.cur::before,.cur::after{content:'';position:absolute;background:var(--cyan)}
.cur::before{width:16px;height:2px;top:7px;left:0}
.cur::after{width:2px;height:16px;top:0;left:7px}

/* GRID BG */
.grid-bg{
  position:fixed;inset:0;z-index:0;
  background-image:
    linear-gradient(rgba(0,255,245,0.03) 1px,transparent 1px),
    linear-gradient(90deg,rgba(0,255,245,0.03) 1px,transparent 1px);
  background-size:40px 40px;
  animation:grid-drift 20s linear infinite;
}
@keyframes grid-drift{0%{background-position:0 0}100%{background-position:40px 40px}}

/* GLITCH NOISE */
@keyframes noise{
  0%,100%{clip-path:inset(0 0 98% 0)}
  10%{clip-path:inset(15% 0 70% 0)}
  20%{clip-path:inset(40% 0 40% 0)}
  30%{clip-path:inset(65% 0 15% 0)}
  40%{clip-path:inset(5% 0 90% 0)}
  50%{clip-path:inset(80% 0 5% 0)}
  60%{clip-path:inset(30% 0 55% 0)}
  70%{clip-path:inset(55% 0 30% 0)}
  80%{clip-path:inset(90% 0 2% 0)}
  90%{clip-path:inset(2% 0 85% 0)}
}

/* LAYOUT */
.wrap{
  position:relative;z-index:1;
  max-width:860px;margin:0 auto;
  padding:60px 32px 80px;
}

/* ── RETRO GAME ANIMATION ── */
.game-canvas{
  width:100%;height:140px;
  border:1px solid rgba(0,255,245,0.2);
  background:#000;
  position:relative;overflow:hidden;
  margin-bottom:40px;
  image-rendering:pixelated;
}
.game-canvas::before{
  content:'';position:absolute;inset:0;
  background:linear-gradient(180deg,transparent 60%,rgba(0,255,245,0.04) 100%);
}
/* starfield */
.stars{position:absolute;inset:0}
.star{
  position:absolute;
  width:var(--pixel);height:var(--pixel);
  background:var(--cyan);
  opacity:0.4;
  animation:star-move var(--d,4s) linear infinite;
  animation-delay:var(--dl,0s);
}
@keyframes star-move{from{transform:translateX(0)}to{transform:translateX(-900px)}}

/* ship */
.ship{
  position:absolute;left:80px;top:50%;
  transform:translateY(-50%);
  width:40px;height:24px;
  animation:ship-bob 2s ease-in-out infinite;
}
@keyframes ship-bob{0%,100%{top:42%}50%{top:55%}}

/* pixel ship drawn with box-shadow */
.ship-pixel{
  width:4px;height:4px;
  background:transparent;
  position:absolute;
  image-rendering:pixelated;
  box-shadow:
    /* body */
    4px 8px 0 var(--cyan),
    8px 4px 0 var(--cyan), 8px 8px 0 var(--cyan),8px 12px 0 var(--cyan),
    12px 0px 0 var(--cyan),12px 4px 0 var(--cyan),12px 8px 0 var(--cyan),12px 12px 0 var(--cyan),12px 16px 0 var(--cyan),
    16px 0px 0 var(--cyan),16px 4px 0 var(--cyan),16px 8px 0 var(--cyan),16px 12px 0 var(--cyan),16px 16px 0 var(--cyan),
    20px 4px 0 var(--cyan),20px 8px 0 var(--cyan),20px 12px 0 var(--cyan),
    24px 8px 0 var(--cyan),
    28px 8px 0 var(--yellow),
    32px 8px 0 var(--yellow),
    /* engine glow */
    0px 8px 0 var(--magenta),
    4px 6px 0 var(--magenta),4px 10px 0 var(--magenta);
}

/* bullets */
.bullet{
  position:absolute;
  width:12px;height:3px;
  background:var(--yellow);
  box-shadow:0 0 6px var(--yellow);
  top:calc(50% - 1px);
  animation:bullet-fly 0.8s linear infinite;
  animation-delay:var(--dl,0s);
  left:120px;
}
@keyframes bullet-fly{from{transform:translateX(0);opacity:1}to{transform:translateX(800px);opacity:0}}

/* enemies */
.enemy{
  position:absolute;
  animation:enemy-move var(--d,6s) linear infinite;
  animation-delay:var(--dl,0s);
  top:var(--t,30%);
}
@keyframes enemy-move{from{left:110%}to{left:-80px}}
.enemy-pixel{
  width:4px;height:4px;background:transparent;
  image-rendering:pixelated;
  box-shadow:
    4px 0 0 var(--magenta),
    0 4px 0 var(--magenta),4px 4px 0 var(--magenta),8px 4px 0 var(--magenta),
    0 8px 0 var(--magenta),4px 8px 0 var(--magenta),8px 8px 0 var(--magenta),12px 8px 0 var(--magenta),
    4px 12px 0 var(--magenta),8px 12px 0 var(--magenta);
}

/* explosions */
.explosion{
  position:absolute;
  animation:explode 0.5s ease-out forwards;
  display:none;
}
@keyframes explode{
  0%{transform:scale(0);opacity:1}
  50%{transform:scale(2);opacity:1}
  100%{transform:scale(3);opacity:0}
}

/* HUD */
.game-hud{
  position:absolute;top:8px;left:0;right:0;
  display:flex;justify-content:space-between;
  padding:0 12px;
  font-family:'Press Start 2P',monospace;
  font-size:7px;
  color:var(--cyan);
}
.hud-score{color:var(--yellow)}
.hud-lives{color:var(--magenta)}
/* ground line */
.game-ground{
  position:absolute;bottom:16px;left:0;right:0;
  height:1px;background:rgba(0,255,245,0.15);
}
/* label */
.game-label{
  position:absolute;bottom:4px;right:10px;
  font-family:'Press Start 2P',monospace;
  font-size:5px;color:var(--muted);
  letter-spacing:1px;
}

/* ── HEADER ── */
.header{margin-bottom:48px;position:relative}
.header-tag{
  font-family:'Press Start 2P',monospace;
  font-size:8px;letter-spacing:2px;
  color:var(--magenta);margin-bottom:16px;
  text-shadow:0 0 12px var(--magenta);
}
.name{
  font-family:'Orbitron',sans-serif;
  font-size:clamp(36px,7vw,72px);
  font-weight:900;
  line-height:1;
  letter-spacing:-2px;
  color:var(--text);
  position:relative;
}
.name em{
  font-style:normal;
  color:var(--cyan);
  text-shadow:0 0 30px rgba(0,255,245,0.5);
}
/* glitch effect on name */
.name::before,.name::after{
  content:attr(data-text);
  position:absolute;top:0;left:0;
  width:100%;
  font-family:'Orbitron',sans-serif;
  font-weight:900;
  font-size:inherit;
  letter-spacing:-2px;
}
.name::before{
  color:var(--magenta);
  animation:glitch-a 4s infinite;
  clip-path:inset(0 0 0 0);
}
.name::after{
  color:var(--cyan);
  animation:glitch-b 4s infinite;
}
@keyframes glitch-a{
  0%,94%,100%{transform:translateX(0);opacity:0}
  95%{transform:translateX(-3px);opacity:0.7}
  97%{transform:translateX(2px);opacity:0.5}
  98%{transform:translateX(-1px);opacity:0.3}
}
@keyframes glitch-b{
  0%,94%,100%{transform:translateX(0);opacity:0}
  95%{transform:translateX(3px);opacity:0.5}
  97%{transform:translateX(-2px);opacity:0.3}
  98%{transform:translateX(1px);opacity:0.2}
}
.subtitle{
  margin-top:12px;
  font-family:'Share Tech Mono',monospace;
  font-size:13px;letter-spacing:3px;text-transform:uppercase;
  color:var(--muted);
}
.subtitle span{color:var(--yellow);text-shadow:0 0 8px rgba(255,230,0,0.4)}

/* status pill */
.status-pill{
  display:inline-flex;align-items:center;gap:8px;
  margin-top:20px;
  padding:8px 18px;
  border:1px solid rgba(57,255,20,0.3);
  background:rgba(57,255,20,0.04);
  font-family:'Press Start 2P',monospace;font-size:7px;
  color:var(--green);letter-spacing:1px;
  text-shadow:0 0 8px var(--green);
}
.status-dot{
  width:6px;height:6px;border-radius:50%;
  background:var(--green);
  box-shadow:0 0 8px var(--green);
  animation:blink 1.5s infinite;
}
@keyframes blink{0%,100%{opacity:1}50%{opacity:0.1}}

/* ── SECTION ── */
.section{margin-bottom:48px}
.section-label{
  display:flex;align-items:center;gap:10px;
  font-family:'Press Start 2P',monospace;
  font-size:8px;letter-spacing:2px;
  color:var(--yellow);
  margin-bottom:20px;
  text-shadow:0 0 10px rgba(255,230,0,0.4);
}
.section-label::before{content:'▶';color:var(--cyan);font-size:7px}
.section-label::after{content:'';flex:1;height:1px;background:linear-gradient(90deg,rgba(255,230,0,0.3),transparent)}

/* ── CODE BLOCK ── */
.code-block{
  background:var(--dim);
  border:1px solid rgba(0,255,245,0.1);
  border-left:3px solid var(--cyan);
  padding:20px 24px;
  font-size:12px;
  line-height:1.9;
  position:relative;
  overflow:hidden;
}
.code-block::before{
  content:'';position:absolute;top:0;right:0;bottom:0;width:1px;
  background:linear-gradient(180deg,var(--cyan),transparent,var(--magenta));
  opacity:0.3;
}
.kw{color:var(--magenta)}
.fn{color:var(--cyan)}
.str{color:var(--yellow)}
.num{color:var(--green)}
.cm{color:var(--muted)}
.obj{color:var(--text)}

/* ── TECH GRID ── */
.tech-grid{
  display:grid;
  grid-template-columns:repeat(auto-fill,minmax(180px,1fr));
  gap:2px;
}
.tech-card{
  background:var(--dim);
  border:1px solid rgba(0,255,245,0.08);
  padding:16px 18px;
  display:flex;align-items:center;gap:12px;
  transition:all 0.2s;
  position:relative;overflow:hidden;
}
.tech-card::before{
  content:'';position:absolute;
  bottom:0;left:0;right:0;height:1px;
  background:var(--cyan);
  transform:scaleX(0);transform-origin:left;
  transition:transform 0.3s;
}
.tech-card:hover{
  background:#0a1e2a;
  border-color:rgba(0,255,245,0.25);
}
.tech-card:hover::before{transform:scaleX(1)}
.tech-icon{
  font-size:18px;width:32px;height:32px;
  display:flex;align-items:center;justify-content:center;
  flex-shrink:0;
}
.tech-name{font-size:11px;color:var(--text);letter-spacing:1px}
.tech-cat{font-size:9px;color:var(--muted);margin-top:2px;letter-spacing:0.5px}

/* ── STATS STRIP ── */
.stats-row{
  display:flex;gap:2px;margin-bottom:2px;
}
.stat-box{
  flex:1;background:var(--dim);
  border:1px solid rgba(0,255,245,0.08);
  padding:20px 16px;text-align:center;
}
.stat-n{
  font-family:'Orbitron',sans-serif;
  font-size:32px;font-weight:700;
  color:var(--cyan);
  text-shadow:0 0 20px rgba(0,255,245,0.4);
  line-height:1;
}
.stat-l{font-size:9px;color:var(--muted);margin-top:6px;letter-spacing:2px;text-transform:uppercase}

/* ── EXPERIENCE ── */
.xp-item{
  display:grid;grid-template-columns:120px 1fr;
  gap:0;
  border-top:1px solid rgba(0,255,245,0.08);
}
.xp-item:last-child{border-bottom:1px solid rgba(0,255,245,0.08)}
.xp-year{
  padding:20px 16px 20px 0;
  font-family:'Orbitron',sans-serif;
  font-size:18px;font-weight:700;
  color:var(--cyan);
  text-align:right;
  border-right:1px solid rgba(0,255,245,0.15);
  display:flex;flex-direction:column;justify-content:flex-start;
  padding-top:22px;
}
.xp-period{font-size:8px;color:var(--muted);margin-top:4px;font-family:'Share Tech Mono',monospace;letter-spacing:1px}
.xp-body{padding:20px 0 20px 24px}
.xp-role{
  font-family:'Orbitron',sans-serif;
  font-size:13px;font-weight:700;
  color:var(--text);margin-bottom:4px;letter-spacing:1px;
}
.xp-where{
  font-size:10px;color:var(--magenta);
  letter-spacing:2px;text-transform:uppercase;
  margin-bottom:10px;
}
.xp-badge{
  display:inline-block;
  font-family:'Press Start 2P',monospace;font-size:6px;
  padding:2px 7px;
  border:1px solid rgba(57,255,20,0.3);
  color:var(--green);
  text-shadow:0 0 6px var(--green);
  margin-left:8px;
  vertical-align:middle;
}
.xp-desc{font-size:12px;color:var(--muted);line-height:1.8;margin-bottom:10px}
.tag-row{display:flex;flex-wrap:wrap;gap:6px}
.tag{
  font-size:9px;padding:3px 9px;
  border:1px solid rgba(0,255,245,0.12);
  color:var(--muted);letter-spacing:1px;text-transform:uppercase;
}

/* ── LINKS ── */
.links-row{display:flex;flex-wrap:wrap;gap:2px}
.lnk{
  display:inline-flex;align-items:center;gap:8px;
  padding:14px 20px;
  background:var(--dim);
  border:1px solid rgba(0,255,245,0.08);
  text-decoration:none;color:var(--muted);
  font-size:10px;letter-spacing:2px;text-transform:uppercase;
  transition:all 0.2s;flex:1;min-width:150px;
}
.lnk:hover{color:var(--cyan);border-color:rgba(0,255,245,0.3);background:#0a1e2a}
.lnk-icon{font-size:14px}

/* ── BOTTOM BAR ── */
.bottom{
  margin-top:60px;
  border-top:1px solid rgba(0,255,245,0.1);
  padding-top:24px;
  display:flex;justify-content:space-between;align-items:center;
  flex-wrap:wrap;gap:12px;
}
.bottom-logo{
  font-family:'Orbitron',sans-serif;font-size:14px;font-weight:900;
  letter-spacing:4px;color:var(--muted);
}
.bottom-logo em{color:var(--cyan);font-style:normal}
.bottom-quote{
  font-family:'Press Start 2P',monospace;font-size:6px;
  color:var(--muted);letter-spacing:1px;
  text-align:right;max-width:280px;line-height:2;
}

/* typing cursor */
.cursor-blink{animation:cur-blink 1s infinite;color:var(--cyan)}
@keyframes cur-blink{0%,100%{opacity:1}50%{opacity:0}}
</style>
</head>
<body>

<div class="grid-bg"></div>
<div class="cur" id="cur"></div>

<div class="wrap">

  <!-- RETRO GAME -->
  <div class="game-canvas" id="gameCanvas">
    <div class="game-hud">
      <span>JOÃO.EXE</span>
      <span class="hud-score">SCORE: <span id="score">0000</span></span>
      <span class="hud-lives">LIVES: ♥♥♥</span>
    </div>
    <div class="stars" id="stars"></div>
    <div class="ship">
      <div class="ship-pixel"></div>
    </div>
    <!-- bullets -->
    <div class="bullet" style="--dl:0s"></div>
    <div class="bullet" style="--dl:0.4s"></div>
    <div class="bullet" style="--dl:0.8s"></div>
    <!-- enemies -->
    <div class="enemy" style="--d:5s;--dl:0s;--t:25%"><div class="enemy-pixel"></div></div>
    <div class="enemy" style="--d:7s;--dl:1.5s;--t:45%"><div class="enemy-pixel"></div></div>
    <div class="enemy" style="--d:6s;--dl:3s;--t:20%"><div class="enemy-pixel"></div></div>
    <div class="enemy" style="--d:8s;--dl:0.8s;--t:60%"><div class="enemy-pixel"></div></div>
    <div class="enemy" style="--d:5.5s;--dl:2.2s;--t:35%"><div class="enemy-pixel"></div></div>
    <div class="game-ground"></div>
    <div class="game-label">INSERT COIN</div>
  </div>

  <!-- HEADER -->
  <div class="header">
    <div class="header-tag">// PLAYER_001.PROFILE</div>
    <div class="name" data-text="João Pedro">
      João <em>Pedro</em>
    </div>
    <div class="subtitle">
      Mobile Dev <span>·</span> UnB <span>·</span> Brasília<span class="cursor-blink">_</span>
    </div>
    <div class="status-pill">
      <div class="status-dot"></div>
      ONLINE — BUSCANDO ESTÁGIO
    </div>
  </div>

  <!-- SOBRE -->
  <div class="section">
    <div class="section-label">SOBRE</div>
    <div class="code-block">
<span class="kw">const</span> <span class="fn">joaoPedro</span> = {<br>
&nbsp;&nbsp;<span class="str">idade</span>: <span class="num">20</span>,<br>
&nbsp;&nbsp;<span class="str">universidade</span>: <span class="str">"UnB — CIC"</span>,<br>
&nbsp;&nbsp;<span class="str">especialidade</span>: <span class="str">"Mobile Dev · React Native"</span>,<br>
&nbsp;&nbsp;<span class="str">stack</span>: [<span class="str">"TypeScript"</span>, <span class="str">"Firebase"</span>, <span class="str">"Go"</span>, <span class="str">"GraphQL"</span>],<br>
&nbsp;&nbsp;<span class="str">status</span>: <span class="str">"<span class="cm">apps em produção, sempre evoluindo</span>"</span><br>
}
    </div>
  </div>

  <!-- TECH -->
  <div class="section">
    <div class="section-label">STACK</div>
    <div class="tech-grid">
      <div class="tech-card"><div class="tech-icon">📱</div><div><div class="tech-name">React Native</div><div class="tech-cat">Mobile</div></div></div>
      <div class="tech-card"><div class="tech-icon">🔷</div><div><div class="tech-name">TypeScript</div><div class="tech-cat">Language</div></div></div>
      <div class="tech-card"><div class="tech-icon">🔥</div><div><div class="tech-name">Firebase</div><div class="tech-cat">Cloud</div></div></div>
      <div class="tech-card"><div class="tech-icon">🐹</div><div><div class="tech-name">Go</div><div class="tech-cat">Backend</div></div></div>
      <div class="tech-card"><div class="tech-icon">🔺</div><div><div class="tech-name">GraphQL</div><div class="tech-cat">API</div></div></div>
      <div class="tech-card"><div class="tech-icon">🟩</div><div><div class="tech-name">Node.js</div><div class="tech-cat">Backend</div></div></div>
      <div class="tech-card"><div class="tech-icon">🐍</div><div><div class="tech-name">Python</div><div class="tech-cat">Data / IA</div></div></div>
      <div class="tech-card"><div class="tech-icon">🧠</div><div><div class="tech-name">Machine Learning</div><div class="tech-cat">IA</div></div></div>
    </div>
  </div>

  <!-- STATS -->
  <div class="section">
    <div class="section-label">STATS</div>
    <div class="stats-row">
      <div class="stat-box"><div class="stat-n" id="st-repos">—</div><div class="stat-l">Repos</div></div>
      <div class="stat-box"><div class="stat-n" id="st-stars">—</div><div class="stat-l">Stars</div></div>
      <div class="stat-box"><div class="stat-n">3+</div><div class="stat-l">Anos</div></div>
      <div class="stat-box"><div class="stat-n" style="font-size:18px;padding-top:6px">1k+</div><div class="stat-l">Usuários</div></div>
    </div>
  </div>

  <!-- EXPERIÊNCIA -->
  <div class="section">
    <div class="section-label">EXPERIÊNCIA</div>

    <div class="xp-item">
      <div class="xp-year">2026<div class="xp-period">— hoje</div></div>
      <div class="xp-body">
        <div class="xp-role">Extensão — Ciência de Dados & IA <span class="xp-badge">ATIVO</span></div>
        <div class="xp-where">Universidade de Brasília — UnB</div>
        <div class="xp-desc">Machine learning, modelos preditivos, análise de dados e aplicações práticas de IA.</div>
        <div class="tag-row"><span class="tag">Python</span><span class="tag">ML</span><span class="tag">Pandas</span><span class="tag">Scikit-learn</span></div>
      </div>
    </div>

    <div class="xp-item">
      <div class="xp-year">2025<div class="xp-period">— hoje</div></div>
      <div class="xp-body">
        <div class="xp-role">Ciências da Computação <span class="xp-badge">ATIVO</span></div>
        <div class="xp-where">Universidade de Brasília — UnB</div>
        <div class="xp-desc">Algoritmos, estruturas de dados, SO, redes e engenharia de software.</div>
        <div class="tag-row"><span class="tag">C/C++</span><span class="tag">Python</span><span class="tag">Algoritmos</span><span class="tag">Redes</span></div>
      </div>
    </div>

    <div class="xp-item">
      <div class="xp-year">2024<div class="xp-period">— hoje</div></div>
      <div class="xp-body">
        <div class="xp-role">Mobile Developer <span class="xp-badge">ATIVO</span></div>
        <div class="xp-where">HC Brito — App de Ordem de Serviço</div>
        <div class="xp-desc">App em produção com +1k usuários. Firebase Auth, Firestore, push notifications e deep linking.</div>
        <div class="tag-row"><span class="tag">React Native</span><span class="tag">Firebase</span><span class="tag">TypeScript</span><span class="tag">GraphQL</span></div>
      </div>
    </div>

    <div class="xp-item">
      <div class="xp-year">2023<div class="xp-period">— hoje</div></div>
      <div class="xp-body">
        <div class="xp-role">Dev Freelancer <span class="xp-badge">ATIVO</span></div>
        <div class="xp-where">Projetos Independentes</div>
        <div class="xp-desc">Sites, landing pages, sistemas web e automações do levantamento até o deploy.</div>
        <div class="tag-row"><span class="tag">React</span><span class="tag">Node.js</span><span class="tag">MongoDB</span><span class="tag">Vercel</span></div>
      </div>
    </div>

    <div class="xp-item">
      <div class="xp-year">2022<div class="xp-period">— início</div></div>
      <div class="xp-body">
        <div class="xp-role">Início na Programação</div>
        <div class="xp-where">Autodidata</div>
        <div class="xp-desc">Primeiros projetos funcionais em meses. Aprendeu errando, depurando e entregando.</div>
        <div class="tag-row"><span class="tag">HTML</span><span class="tag">CSS</span><span class="tag">JavaScript</span></div>
      </div>
    </div>
  </div>

  <!-- LINKS -->
  <div class="section">
    <div class="section-label">CONNECT</div>
    <div class="links-row">
      <a class="lnk" href="https://wa.me/5561999393545" target="_blank"><span class="lnk-icon">📱</span>WhatsApp</a>
      <a class="lnk" href="https://github.com/Joaozzin-dev" target="_blank"><span class="lnk-icon">⌨</span>GitHub</a>
      <a class="lnk" href="https://www.linkedin.com/in/jo%C3%A3o-pedro-rodrigues-de-souza-8a440627a/" target="_blank"><span class="lnk-icon">💼</span>LinkedIn</a>
      <a class="lnk" href="mailto:redjp15@gmail.com"><span class="lnk-icon">✉</span>Email</a>
    </div>
  </div>

  <!-- BOTTOM -->
  <div class="bottom">
    <div class="bottom-logo">JP<em>.</em>DEV</div>
    <div class="bottom-quote">"TRANSFORMANDO IDEIAS<br>EM APPS QUE AS PESSOAS<br>AMAM USAR"</div>
  </div>

</div>

<script>
// cursor
const cur=document.getElementById('cur');
document.addEventListener('mousemove',e=>{cur.style.left=e.clientX+'px';cur.style.top=e.clientY+'px'});

// stars
const starsEl=document.getElementById('stars');
for(let i=0;i<28;i++){
  const s=document.createElement('div');
  s.className='star';
  const size=Math.random()<0.3?8:4;
  s.style.cssText=`
    width:${size}px;height:${size}px;
    top:${Math.random()*100}%;
    left:${Math.random()*100}%;
    --d:${3+Math.random()*6}s;
    --dl:-${Math.random()*6}s;
    opacity:${0.2+Math.random()*0.5};
  `;
  starsEl.appendChild(s);
}

// score counter
let score=0;
const scoreEl=document.getElementById('score');
setInterval(()=>{
  score+=Math.floor(Math.random()*50+10);
  scoreEl.textContent=String(score).padStart(4,'0');
},600);

// github stats
async function loadStats(){
  try{
    const[ur,rr]=await Promise.all([
      fetch('https://api.github.com/users/Joaozzin-dev'),
      fetch('https://api.github.com/users/Joaozzin-dev/repos?per_page=100')
    ]);
    if(!ur.ok||!rr.ok)return;
    const u=await ur.json(),repos=await rr.json();
    const stars=repos.reduce((a,r)=>a+r.stargazers_count,0);
    document.getElementById('st-repos').textContent=u.public_repos||'—';
    document.getElementById('st-stars').textContent=stars||'0';
  }catch(e){}
}
loadStats();
</script>
</body>
</html>
