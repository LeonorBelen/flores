<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Para Sharon</title>
<meta name="theme-color" content="#A9D8F2">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Caveat:wght@600;700&family=Nunito:wght@500;700&display=swap" rel="stylesheet">
<style>
:root{
  box-sizing:border-box;
  padding-top:env(safe-area-inset-top,0px);
  padding-bottom:env(safe-area-inset-bottom,0px);
  --u:1vh;
  --sky-top:#A9D8F2; --sky-bottom:#FFF0B0; --glow:rgba(255,248,205,.95);
  --ink:#3A2E0F; --ink-soft:#5A4820;
  --hill-back:#93D482; --hill-front:#5DB55B;
  --leaf:#4E9F4A; --leaf-dark:#2F7A3A;
  --btn-bg:#3A2E0F; --btn-ink:#FFE04D;
  --focus:#1B4FD8;
  --stars:0; --bloom:none;
  --dot-off:rgba(58,46,15,.12);
}
@supports (height:1svh){ :root{ --u:1svh; } }

@media (prefers-color-scheme: dark){
  :root:not([data-theme="light"]){
    --sky-top:#0D1838; --sky-bottom:#3C3577; --glow:rgba(150,140,255,.28);
    --ink:#FFF4C7; --ink-soft:#E8DCA8;
    --hill-back:#1F5B4C; --hill-front:#133F37;
    --leaf:#3F9B63; --leaf-dark:#2A7A4D;
    --btn-bg:#FFD21F; --btn-ink:#2B1F05;
    --focus:#FFF4C7;
    --stars:1; --bloom:drop-shadow(0 0 14px rgba(255,210,50,.45));
    --dot-off:rgba(255,244,199,.14);
  }
}
:root[data-theme="dark"]{
  --sky-top:#0D1838; --sky-bottom:#3C3577; --glow:rgba(150,140,255,.28);
  --ink:#FFF4C7; --ink-soft:#E8DCA8;
  --hill-back:#1F5B4C; --hill-front:#133F37;
  --leaf:#3F9B63; --leaf-dark:#2A7A4D;
  --btn-bg:#FFD21F; --btn-ink:#2B1F05;
  --focus:#FFF4C7;
  --stars:1; --bloom:drop-shadow(0 0 14px rgba(255,210,50,.45));
  --dot-off:rgba(255,244,199,.14);
}

html{ scroll-padding-top:env(safe-area-inset-top,0px); }
*,*::before,*::after{ box-sizing:inherit; }
body{
  margin:0; min-height:100%;
  background:var(--sky-bottom); color:var(--ink);
  font-family:"Nunito",system-ui,-apple-system,"Segoe UI",Roboto,sans-serif;
  -webkit-font-smoothing:antialiased;
  overflow-x:hidden;
}
.sky{
  position:fixed; inset:0; z-index:-2;
  background:
    radial-gradient(70vmax 70vmax at 88% 6%, var(--glow), transparent 62%),
    linear-gradient(180deg, var(--sky-top), var(--sky-bottom));
}
.stars{ position:fixed; inset:0; z-index:-1; opacity:var(--stars); pointer-events:none; }
.stars i{ position:absolute; border-radius:50%; background:#FFF4C7; }

.scene{
  min-height:calc(100 * var(--u) - env(safe-area-inset-top,0px) - env(safe-area-inset-bottom,0px));
  display:flex; flex-direction:column; align-items:center;
}
.date{
  margin:0; padding:18px 20px 0;
  font-weight:700; font-size:.98rem; color:var(--ink-soft);
}

/* Flor principal */
.hero{
  --size:max(96px, min(78vw, calc(44 * var(--u))));
  width:var(--size); height:var(--size);
  margin-top:8px; padding:0; border:0; background:none;
  border-radius:50%; cursor:pointer; flex:none;
  -webkit-tap-highlight-color:transparent;
  transition:width 1.1s cubic-bezier(.65,0,.25,1), height 1.1s cubic-bezier(.65,0,.25,1);
}
.scene.ready .hero{ --size:max(96px, min(38vw, calc(17 * var(--u)))); }
.hero:focus-visible, .plant-btn:focus-visible{ outline:3px solid var(--focus); outline-offset:4px; }
.hero svg{ display:block; width:100%; height:100%; overflow:visible; filter:var(--bloom); }
.hero.open svg{ animation:heroSway 7s ease-in-out infinite alternate; }
@keyframes heroSway{ from{ transform:rotate(-2.2deg); } to{ transform:rotate(2.2deg); } }

.pt path, .petal{ stroke:rgba(196,120,0,.35); stroke-width:1.3; }
.petal{
  transform-box:fill-box; transform-origin:50% 100%;
  transform:scale(.08);
  transition:transform 1.25s cubic-bezier(.22,1.25,.36,1) calc(var(--i) * 40ms + 250ms);
}
.hero.open .petal{ transform:scale(1); }
.disc{
  transform-box:fill-box; transform-origin:center;
  transform:scale(0);
  transition:transform .9s cubic-bezier(.3,1.5,.5,1) .6s;
}
.hero.open .disc{ transform:scale(1); }
.bud{
  transform-box:fill-box; transform-origin:50% 100%;
  transition:transform .7s ease-in, opacity .6s ease-in .1s;
}
.hero:not(.open) .bud{ animation:breathe 2.8s ease-in-out infinite; }
.hero.open .bud{ transform:scale(1.3); opacity:0; }
@keyframes breathe{ 50%{ transform:scale(1.05); } }
.bud-a{ fill:var(--leaf); } .bud-b{ fill:var(--leaf-dark); opacity:.45; }
.halo{
  transform-box:fill-box; transform-origin:center;
  transition:opacity .8s;
}
.hero:not(.open) .halo{ animation:halo 2.8s ease-in-out infinite; }
.hero.open .halo{ opacity:0; }
@keyframes halo{ 0%,100%{ transform:scale(.9); opacity:.7; } 50%{ transform:scale(1.06); opacity:1; } }

/* Texto */
.text{ width:min(calc(100% - 2.5rem), 32rem); text-align:center; margin-top:4px; }
h1{
  margin:0;
  font-family:"Caveat","Segoe Print","Bradley Hand",cursive;
  font-weight:700; line-height:1;
  font-size:clamp(3.2rem, 15vw, 5rem);
  text-wrap:balance;
  transition:opacity .35s;
}
h1.small{ font-size:clamp(2rem, 7.4vw, 2.9rem); line-height:1.04; }
h1.out{ opacity:0; }
.hint{ margin:10px 0 0; font-weight:700; font-size:1.08rem; color:var(--ink-soft); transition:opacity .4s; }
.hint.gone{ opacity:0; }

.reveal{
  display:grid; grid-template-rows:0fr; width:100%;
  transition:grid-template-rows 1s cubic-bezier(.4,0,.2,1);
}
.reveal > .inner{
  min-height:0; overflow:hidden; visibility:hidden; opacity:0;
  transition:opacity .9s .5s;
}
.scene.ready .reveal{ grid-template-rows:1fr; }
.scene.ready .reveal > .inner{ visibility:visible; opacity:1; }

.message{ width:min(calc(100% - 2.5rem), 30rem); margin:0 auto; text-align:center; }
.message p{
  margin:8px 0 0;
  font-size:clamp(1rem, 3.8vw, 1.16rem); line-height:1.55; font-weight:500;
  text-wrap:pretty;
}
.message .sign{
  font-family:"Caveat","Segoe Print","Bradley Hand",cursive;
  font-size:1.9rem; font-weight:700; line-height:1.1; margin-top:4px;
}

.controls .inner{
  display:flex; flex-direction:column; align-items:center; gap:10px;
  padding:8px 12px 10px;
}
.wish{
  margin:0; min-height:2.5em; max-width:24rem;
  display:flex; align-items:center; justify-content:center; text-align:center;
  font-family:"Caveat","Segoe Print","Bradley Hand",cursive;
  font-size:1.5rem; font-weight:600; line-height:1.1;
}
.wish.pop{ animation:wishIn .5s cubic-bezier(.2,.8,.3,1); }
@keyframes wishIn{ from{ opacity:0; transform:translateY(8px); } to{ opacity:1; transform:none; } }
.dots{ display:flex; gap:9px; }
.dots i{
  width:14px; height:14px; border-radius:50%;
  border:2px solid var(--ink-soft); background:var(--dot-off);
  transition:background .3s, transform .4s cubic-bezier(.3,1.6,.5,1);
}
.dots i.on{ background:#FFC800; transform:scale(1.22); }
.plant-btn{
  font:700 1.08rem/1 "Nunito",system-ui,sans-serif;
  min-height:48px; padding:14px 28px; border:0; border-radius:999px;
  background:var(--btn-bg); color:var(--btn-ink); cursor:pointer;
  transition:transform .15s;
}
.plant-btn:active{ transform:scale(.96); }

/* Jardín */
.garden{
  position:relative; width:100%; margin-top:auto;
  height:clamp(180px, calc(28 * var(--u)), 320px);
  overflow:hidden; touch-action:manipulation;
}
.scene.ready .garden{ cursor:pointer; }
.hills{ position:absolute; inset:0; width:100%; height:100%; }
.hills .b{ fill:var(--hill-back); } .hills .f{ fill:var(--hill-front); }
.plants{ position:absolute; inset:0; pointer-events:none; }
.plant{ position:absolute; transform-origin:50% 100%; animation:sway 4s ease-in-out var(--sd,0s) infinite alternate; }
@keyframes sway{
  from{ transform:rotate(calc(var(--sw,2deg) * -1)); }
  to{ transform:rotate(var(--sw,2deg)); }
}
.plant svg{ display:block; width:100%; height:100%; transform-origin:50% 100%; filter:var(--bloom); }
.stem{ stroke:var(--leaf-dark); }
.leaf{ fill:var(--leaf); }

/* Pétalos que vuelan */
#fx{ position:fixed; inset:0; pointer-events:none; overflow:hidden; z-index:30; }
.fp{
  position:absolute; left:0; top:0;
  border-radius:60% 40% 60% 40% / 85% 85% 30% 30%;
  will-change:transform, opacity;
}

@media (prefers-reduced-motion: reduce){
  *,*::before,*::after{
    animation-duration:.01ms !important; animation-iteration-count:1 !important;
    transition-duration:.01ms !important; transition-delay:0s !important;
  }
}
</style>
</head>
<body>
<div class="sky" aria-hidden="true"></div>
<div class="stars" id="stars" aria-hidden="true"></div>

<svg width="0" height="0" style="position:absolute" aria-hidden="true" focusable="false">
  <defs>
    <linearGradient id="gBack" x1="0" y1="1" x2="0" y2="0"><stop offset="0" style="stop-color:#F09A00"/><stop offset="1" style="stop-color:#FFC21A"/></linearGradient>
    <linearGradient id="gFront" x1="0" y1="1" x2="0" y2="0"><stop offset="0" style="stop-color:#FFB800"/><stop offset="1" style="stop-color:#FFE24D"/></linearGradient>
    <linearGradient id="gDaisy" x1="0" y1="1" x2="0" y2="0"><stop offset="0" style="stop-color:#FFE066"/><stop offset="1" style="stop-color:#FFF6B8"/></linearGradient>
    <radialGradient id="gDisc"><stop offset="0" style="stop-color:#B0651F"/><stop offset="1" style="stop-color:#5E2C09"/></radialGradient>
    <radialGradient id="gHalo"><stop offset="0" style="stop-color:#FFE24D;stop-opacity:.75"/><stop offset="1" style="stop-color:#FFE24D;stop-opacity:0"/></radialGradient>
  </defs>
</svg>

<main class="scene" id="scene">
  <p class="date" id="date"></p>

  <button class="hero" id="hero" type="button" aria-label="Abrir la flor">
    <svg id="heroSvg" viewBox="0 0 400 400" aria-hidden="true"></svg>
  </button>

  <section class="text">
    <h1 id="title">Para Sharon</h1>
    <p class="hint" id="hint">Toca la flor</p>
  </section>

  <section class="reveal" id="message">
    <div class="inner">
      <div class="message">
        <p>Hoy se regalan flores amarillas a la gente que uno quiere. Como no te puedo llevar un ramo de verdad, te armé este jardín. Plántalo tú.</p>
        <p class="sign">Con cariño, Leonor</p>
      </div>
    </div>
  </section>

  <section class="reveal controls" id="controls">
    <div class="inner">
      <p class="wish" id="wish" aria-live="polite">Planta 7 flores para armar tu ramo.</p>
      <div class="dots" id="dots" role="img" aria-label="Flores plantadas: 0 de 7"></div>
      <button class="plant-btn" id="plant" type="button">Plantar una flor</button>
    </div>
  </section>

  <section class="garden" id="garden" aria-label="Jardín: toca para plantar flores">
    <svg class="hills" viewBox="0 0 400 200" preserveAspectRatio="none" aria-hidden="true">
      <path class="b" d="M0,58 C70,34 130,64 210,50 C290,36 350,58 400,44 L400,200 L0,200Z"/>
      <path class="f" d="M0,110 C80,86 150,120 240,98 C310,80 360,96 400,90 L400,200 L0,200Z"/>
    </svg>
    <div class="plants" id="plants"></div>
  </section>
</main>

<div id="fx" aria-hidden="true"></div>

<script>
(() => {
  const $ = s => document.querySelector(s);
  const RM = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  const rand = (a, b) => a + Math.random() * (b - a);
  const pick = a => a[Math.floor(Math.random() * a.length)];

  const scene = $('#scene'), hero = $('#hero'), heroSvg = $('#heroSvg');
  const title = $('#title'), hint = $('#hint');
  const garden = $('#garden'), plantsEl = $('#plants');
  const wishEl = $('#wish'), dotsEl = $('#dots'), plantBtn = $('#plant'), fx = $('#fx');

  const GOAL = 7;
  const WISHES = [
    'Que hoy todo te salga bonito.',
    'Que nunca te falten motivos para reírte.',
    'Que haya sol en tus días, incluso en los nublados.',
    'Que lo que estás sembrando este año florezca.',
    'Gracias por estar, en las buenas y en las que no.',
    'Ojalá siempre te acuerdes de lo increíble que eres.'
  ];
  const FINAL = 'Ya está tu ramo completo. Feliz día, Sharon.';

  /* Fecha */
  const now = new Date();
  const isToday = now.getMonth() === 8 && now.getDate() === 21;
  $('#date').textContent = isToday ? 'Hoy, 21 de septiembre' : '21 de septiembre';

  /* Estrellas (solo se ven en modo oscuro) */
  const stars = $('#stars');
  for (let i = 0; i < 46; i++) {
    const s = document.createElement('i');
    const sz = rand(1.5, 3).toFixed(1);
    s.style.cssText = `left:${rand(0, 100).toFixed(1)}%;top:${rand(0, 60).toFixed(1)}%;width:${sz}px;height:${sz}px;opacity:${rand(.35, .9).toFixed(2)}`;
    stars.appendChild(s);
  }

  /* Puntos de progreso */
  for (let i = 0; i < GOAL; i++) dotsEl.appendChild(document.createElement('i'));

  /* Flor principal */
  (function buildHero() {
    const PET = 'M0,-26 C 42,-62 38,-160 0,-196 C -38,-160 -42,-62 0,-26 Z';
    const n = 12;
    let back = '', front = '';
    for (let i = 0; i < n; i++) {
      const a = i * 360 / n;
      back  += `<g transform="rotate(${a})"><path class="petal" style="--i:${i}" fill="url(#gBack)" d="${PET}"/></g>`;
      front += `<g transform="rotate(${a + 180 / n}) scale(.9)"><path class="petal" style="--i:${i + n}" fill="url(#gFront)" d="${PET}"/></g>`;
    }
    let dots = '';
    const ga = Math.PI * (3 - Math.sqrt(5));
    for (let k = 1; k <= 70; k++) {
      const r = 6.4 * Math.sqrt(k), t = k * ga;
      dots += `<circle cx="${(r * Math.cos(t)).toFixed(1)}" cy="${(r * Math.sin(t)).toFixed(1)}" r="${(1.6 + k / 70 * 1.2).toFixed(1)}"/>`;
    }
    heroSvg.innerHTML = `
      <circle class="halo" cx="200" cy="200" r="190" fill="url(#gHalo)"/>
      <g transform="translate(200 200)">
        ${back}${front}
        <g class="disc"><circle r="58" fill="url(#gDisc)"/><g fill="#3B1C05" fill-opacity=".55">${dots}</g></g>
        <g class="bud"><g transform="translate(0 105) scale(1.4)">
          <path class="bud-a" d="M0,-8 C 48,-34 48,-104 0,-150 C -48,-104 -48,-34 0,-8Z"/>
          <path class="bud-b" d="M0,-8 C 20,-40 20,-104 0,-150 C -20,-104 -20,-40 0,-8Z"/>
          <path d="M-20,-108 C -10,-124 -4,-138 0,-150 C 4,-138 10,-124 20,-108 C 8,-116 -8,-116 -20,-108Z" fill="#FFD21F"/>
        </g></g>
      </g>`;
  })();

  /* Flores del jardín */
  const KINDS = ['sun', 'flower', 'flower', 'daisy'];
  function plantSVG(kind) {
    const c = {
      sun:    { n: 12, d: 'M0,-12 C 12,-22 12,-40 0,-47 C -12,-40 -12,-22 0,-12Z', fill: 'url(#gFront)', r: 19, disc: 'url(#gDisc)' },
      flower: { n: 9,  d: 'M0,-10 C 15,-20 15,-40 0,-47 C -15,-40 -15,-20 0,-10Z', fill: 'url(#gFront)', r: 12, disc: 'url(#gDisc)' },
      daisy:  { n: 14, d: 'M0,-9 C 6,-18 6,-38 0,-46 C -6,-38 -6,-18 0,-9Z',       fill: 'url(#gDaisy)', r: 10, disc: '#EFA400' }
    }[kind];
    let pet = '';
    for (let i = 0; i < c.n; i++) pet += `<path d="${c.d}" transform="rotate(${(i * 360 / c.n).toFixed(1)})"/>`;
    return `<svg viewBox="0 0 120 200" aria-hidden="true">
      <path class="stem" d="M60,200 C57,160 63,118 60,64" fill="none" stroke-width="5" stroke-linecap="round"/>
      <path class="leaf" d="M60,158 C36,158 20,142 15,120 C40,122 56,136 60,158Z"/>
      <path class="leaf" d="M60,136 C86,136 101,120 106,100 C80,102 64,114 60,136Z"/>
      <g transform="translate(60 52)"><g class="pt" fill="${c.fill}">${pet}</g><circle r="${c.r}" fill="${c.disc}"/></g>
    </svg>`;
  }

  /* Pétalos que vuelan */
  const COLORS = ['#FFD21F', '#FFC107', '#FFE04D', '#FFB800'];
  function petalEl() {
    const p = document.createElement('i');
    p.className = 'fp';
    const s = rand(.7, 1.3);
    p.style.cssText = `width:${(14 * s).toFixed(1)}px;height:${(20 * s).toFixed(1)}px;background:${pick(COLORS)}`;
    fx.appendChild(p);
    return p;
  }
  function burst(cx, cy, n, k = 1) {
    if (RM) return;
    for (let i = 0; i < n; i++) {
      const p = petalEl();
      const ang = rand(0, Math.PI * 2), dist = rand(80, 220) * k;
      const dx = Math.cos(ang) * dist, dy = Math.sin(ang) * dist - 40 * k;
      const fall = dy + rand(120, 320) * k, rot = rand(-260, 260);
      const a = p.animate([
        { transform: `translate(${cx}px,${cy}px) rotate(0deg) scale(.4)`, opacity: 0 },
        { transform: `translate(${cx + dx}px,${cy + dy}px) rotate(${rot / 2}deg) scale(1)`, opacity: 1, offset: .3 },
        { transform: `translate(${cx + dx * 1.15}px,${cy + fall}px) rotate(${rot}deg) scale(.9)`, opacity: 0 }
      ], { duration: rand(1800, 3200), easing: 'cubic-bezier(.2,.7,.4,1)', fill: 'forwards' });
      a.onfinish = () => p.remove();
    }
  }
  function shower(n) {
    if (RM) return;
    const W = innerWidth, H = innerHeight;
    for (let i = 0; i < n; i++) {
      const p = petalEl();
      const x = rand(0, W), sway = rand(-80, 80);
      const a = p.animate([
        { transform: `translate(${x}px,-30px) rotate(0deg)`, opacity: 0 },
        { opacity: 1, offset: .1 },
        { transform: `translate(${x + sway}px,${H + 30}px) rotate(${rand(-540, 540)}deg)`, opacity: .9 }
      ], { duration: rand(3200, 5800), delay: rand(0, 1600), easing: 'ease-in-out', fill: 'both' });
      a.onfinish = () => p.remove();
    }
  }

  /* Estado */
  let opened = false, ready = false, count = 0;

  function swapTitle(text) {
    title.classList.add('out');
    setTimeout(() => {
      title.textContent = text;
      title.classList.add('small');
      title.classList.remove('out');
    }, RM ? 0 : 350);
  }

  function openFlower() {
    opened = true;
    hero.classList.add('open');
    hero.setAttribute('aria-label', 'Soltar pétalos');
    hint.classList.add('gone');
    setTimeout(() => { hint.hidden = true; }, RM ? 0 : 450);
    const r = hero.getBoundingClientRect();
    setTimeout(() => burst(r.left + r.width / 2, r.top + r.height / 2, 28), RM ? 0 : 700);
    setTimeout(() => {
      ready = true;
      scene.classList.add('ready');
      swapTitle('Feliz día de las flores amarillas, Sharon');
    }, RM ? 300 : 2600);
  }

  hero.addEventListener('click', () => {
    if (!opened) { openFlower(); return; }
    const r = hero.getBoundingClientRect();
    burst(r.left + r.width / 2, r.top + r.height / 2, 14);
  });

  function updateDots() {
    [...dotsEl.children].forEach((d, i) => d.classList.toggle('on', i < count));
    dotsEl.setAttribute('aria-label', `Flores plantadas: ${Math.min(count, GOAL)} de ${GOAL}`);
  }
  function showWish() {
    const text = count === GOAL ? FINAL : WISHES[(count < GOAL ? count - 1 : count - GOAL - 1) % WISHES.length];
    wishEl.textContent = text;
    wishEl.classList.remove('pop');
    void wishEl.offsetWidth;
    wishEl.classList.add('pop');
    if (count === GOAL) shower(46);
  }

  function plantAt(x, y) {
    const H = garden.clientHeight, W = garden.clientWidth;
    const minY = H * 0.34;
    y = Math.min(Math.max(y, minY), H - 6);
    x = Math.min(Math.max(x, 24), W - 24);
    const t = (y - minY) / Math.max(1, H - 6 - minY);
    let h = (46 + 72 * t) * rand(.92, 1.08);
    h = Math.min(h, y - 4);
    const w = h * 0.6;

    const div = document.createElement('div');
    div.className = 'plant';
    div.style.cssText = `left:${(x - w / 2).toFixed(1)}px;top:${(y - h).toFixed(1)}px;width:${w.toFixed(1)}px;height:${h.toFixed(1)}px;z-index:${Math.round(y)};--sd:${rand(0, 3).toFixed(2)}s;--sw:${rand(1.6, 3.2).toFixed(1)}deg;animation-duration:${rand(3.4, 5.2).toFixed(1)}s`;
    div.innerHTML = plantSVG(pick(KINDS));
    plantsEl.appendChild(div);
    while (plantsEl.children.length > 36) plantsEl.firstChild.remove();

    if (!RM) {
      div.firstElementChild.animate([
        { transform: 'scale(0)' },
        { transform: 'scale(1.1)', offset: .65 },
        { transform: 'scale(1)' }
      ], { duration: 900, easing: 'cubic-bezier(.2,.8,.3,1)' });
    }

    const gr = garden.getBoundingClientRect();
    burst(gr.left + x, gr.top + y - h * .6, 6, .35);

    count++;
    updateDots();
    showWish();
  }

  garden.addEventListener('click', e => {
    if (!ready) return;
    const r = garden.getBoundingClientRect();
    plantAt(e.clientX - r.left, e.clientY - r.top);
  });
  plantBtn.addEventListener('click', () => {
    const W = garden.clientWidth, H = garden.clientHeight;
    plantAt(rand(30, W - 30), rand(H * .4, H - 10));
  });
})();
</script>
</body>
</html>

