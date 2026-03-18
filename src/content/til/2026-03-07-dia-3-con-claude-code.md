---
title: "Día 3 con Claude Code"
date: 2026-03-07
tags: ["Claude Code", "Data Viz"]
---

Día 3. Después de los efectos de ratón de ayer, quería ver si dentro de un `.md` se podía construir algo más útil: gráficas de verdad.

Sin librerías externas. Solo Canvas y JavaScript puro. Le describí a Claude cinco tipos de visualización — las que verías en cualquier dashboard serio — con filtro de período estilo iOS y tooltip preciso al hover. Cada una construida con los primitivos mínimos.

## Comparativa de barras

Archivos modificados por sesión: trabajando con Claude vs. trabajando solo.

<div class="viz-pg" id="pg-bars">
  <div class="viz-top">
    <span class="viz-lbl">archivos / sesión</span>
    <div class="seg-ctrl" id="seg-bars">
      <button class="seg active">Día</button>
      <button class="seg">Semana</button>
      <button class="seg">Mes</button>
    </div>
  </div>
  <div class="viz-area" id="area-bars">
    <canvas id="c-bars"></canvas>
    <div class="viz-tt" id="tt-bars"></div>
  </div>
</div>

## Distribución

De qué tipo son los commits que produce cada sesión con Claude.

<div class="viz-pg" id="pg-pie">
  <div class="viz-top">
    <span class="viz-lbl">tipo de commit</span>
    <div class="seg-ctrl" id="seg-pie">
      <button class="seg active">Día</button>
      <button class="seg">Semana</button>
      <button class="seg">Mes</button>
    </div>
  </div>
  <div class="viz-area" id="area-pie">
    <canvas id="c-pie"></canvas>
    <div class="viz-tt" id="tt-pie"></div>
  </div>
</div>

## Perfil de habilidades

El pentágono del PES pero midiendo la sesión de trabajo con Claude.

<div class="viz-pg" id="pg-penta">
  <div class="viz-top">
    <span class="viz-lbl">análisis de sesión</span>
    <div class="seg-ctrl" id="seg-penta">
      <button class="seg active">Día</button>
      <button class="seg">Semana</button>
      <button class="seg">Mes</button>
    </div>
  </div>
  <div class="viz-area" id="area-penta">
    <canvas id="c-penta"></canvas>
    <div class="viz-tt" id="tt-penta"></div>
  </div>
</div>

## Progresión de uso

Tokens consumidos a lo largo del período. El mousemove sigue la curva.

<div class="viz-pg" id="pg-line">
  <div class="viz-top">
    <span class="viz-lbl">tokens / hora</span>
    <div class="seg-ctrl" id="seg-line">
      <button class="seg active">Día</button>
      <button class="seg">Semana</button>
      <button class="seg">Mes</button>
    </div>
  </div>
  <div class="viz-area" id="area-line">
    <canvas id="c-line"></canvas>
    <div class="viz-tt" id="tt-line"></div>
  </div>
</div>

## Anillos de actividad

Inspirado en los Activity Rings del Apple Watch. Tres métricas, tres anillos.

<div class="viz-pg" id="pg-rings">
  <div class="viz-top">
    <span class="viz-lbl">objetivos del período</span>
    <div class="seg-ctrl" id="seg-rings">
      <button class="seg active">Día</button>
      <button class="seg">Semana</button>
      <button class="seg">Mes</button>
    </div>
  </div>
  <div class="viz-area" id="area-rings">
    <canvas id="c-rings"></canvas>
    <div class="viz-tt" id="tt-rings"></div>
  </div>
</div>

## En pequeño

Ocho formatos distintos, misma estética. Inspirado en los widgets del iPhone.

<div class="widget-grid">

  <div class="widget"><span class="w-lbl">resp. media</span><div class="ww" id="ww-spark"><canvas id="wc-spark"></canvas><div class="viz-tt" id="wt-spark"></div></div></div>

  <div class="widget"><span class="w-lbl">uso cpu</span><div class="ww" id="ww-gauge"><canvas id="wc-gauge"></canvas><div class="viz-tt" id="wt-gauge"></div></div></div>

  <div class="widget"><span class="w-lbl">actividad</span><div class="ww" id="ww-heat"><canvas id="wc-heat"></canvas><div class="viz-tt" id="wt-heat"></div></div></div>

  <div class="widget"><span class="w-lbl">tokens / calidad</span><div class="ww" id="ww-scatter"><canvas id="wc-scatter"></canvas><div class="viz-tt" id="wt-scatter"></div></div></div>

  <div class="widget"><span class="w-lbl">commits</span><div class="ww" id="ww-stat"><canvas id="wc-stat"></canvas><div class="viz-tt" id="wt-stat"></div></div></div>

  <div class="widget"><span class="w-lbl">herramientas</span><div class="ww" id="ww-hbars"><canvas id="wc-hbars"></canvas><div class="viz-tt" id="wt-hbars"></div></div></div>

  <div class="widget"><span class="w-lbl">contexto</span><div class="ww" id="ww-ring"><canvas id="wc-ring"></canvas><div class="viz-tt" id="wt-ring"></div></div></div>

  <div class="widget"><span class="w-lbl">errores / hora</span><div class="ww" id="ww-eq"><canvas id="wc-eq"></canvas><div class="viz-tt" id="wt-eq"></div></div></div>

</div>

## TIL

- Canvas API + hitbox manual = charts sin una sola dependencia externa
- `devicePixelRatio` importa: sin él todo se ve borroso en pantallas retina
- Los tooltips con datos específicos hacen que una gráfica pase de decoración a herramienta

<style>
.viz-pg {
  border-radius: 10px;
  margin: 2rem 0;
  background: #0d0d17;
  border: 1px solid rgba(255,255,255,0.06);
  overflow: hidden;
  display: flex;
  flex-direction: column;
}
.viz-top {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 14px 18px 12px;
  border-bottom: 1px solid rgba(255,255,255,0.05);
  flex-shrink: 0;
}
.viz-lbl {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.5625rem;
  color: rgba(255,255,255,0.28);
  text-transform: uppercase;
  letter-spacing: 0.14em;
}
.seg-ctrl {
  display: flex;
  background: rgba(255,255,255,0.05);
  border-radius: 7px;
  padding: 2px;
  gap: 1px;
}
.seg {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.5625rem;
  font-weight: 600;
  letter-spacing: 0.07em;
  text-transform: uppercase;
  color: rgba(255,255,255,0.3);
  background: transparent;
  border: none;
  border-radius: 5px;
  padding: 5px 13px;
  cursor: pointer;
  transition: background 0.16s, color 0.16s;
}
.seg:hover {
  color: rgba(255,255,255,0.55);
}
.seg.active {
  background: rgba(255,255,255,0.11);
  color: rgba(255,255,255,0.88);
}
.viz-area {
  position: relative;
  height: 258px;
  overflow: hidden;
}
.viz-area canvas {
  position: absolute;
  top: 0; left: 0;
}
.viz-tt {
  position: absolute;
  pointer-events: none;
  background: rgba(10,10,22,0.94);
  border: 1px solid rgba(255,255,255,0.11);
  border-radius: 7px;
  padding: 9px 13px;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.625rem;
  color: rgba(255,255,255,0.75);
  white-space: nowrap;
  opacity: 0;
  transition: opacity 0.12s;
  z-index: 10;
  line-height: 1.75;
  box-shadow: 0 8px 24px rgba(0,0,0,0.5);
}
.viz-tt.show { opacity: 1; }
.tt-title { color: rgba(255,255,255,0.4); font-size: 0.5625rem; text-transform: uppercase; letter-spacing: 0.1em; margin-bottom: 4px; }
.tt-val { font-weight: 700; color: #fff; }
.tt-dim { color: rgba(255,255,255,0.35); }

/* ---- WIDGET GRID ---- */
.widget-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
  margin: 2rem 0 2.5rem;
}
@media (max-width: 520px) {
  .widget-grid { grid-template-columns: repeat(2, 1fr); }
}
.widget {
  background: #131320;
  border-radius: 18px;
  border: 1px solid rgba(255,255,255,0.06);
  aspect-ratio: 1;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  padding: 13px 13px 10px;
  box-sizing: border-box;
}
.w-lbl {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.5rem;
  text-transform: uppercase;
  letter-spacing: 0.14em;
  color: rgba(255,255,255,0.28);
  flex-shrink: 0;
  margin-bottom: 5px;
}
.ww {
  position: relative;
  flex: 1;
  overflow: hidden;
}
.ww canvas {
  position: absolute;
  top: 0; left: 0;
}
</style>

<script>
/* ===================== SHARED UTIL ===================== */
function setupCanvas(canvasId, areaId) {
  var canvas = document.getElementById(canvasId);
  var area   = document.getElementById(areaId);
  if (!canvas || !area) return null;
  var ctx = canvas.getContext('2d');
  var dpr = window.devicePixelRatio || 1;
  var _draw = null;
  function resize() {
    var W = area.clientWidth;
    var H = area.clientHeight;
    canvas.width  = W * dpr;
    canvas.height = H * dpr;
    canvas.style.width  = W + 'px';
    canvas.style.height = H + 'px';
    ctx.setTransform(dpr, 0, 0, dpr, 0, 0);
    if (_draw) requestAnimationFrame(_draw);
  }
  resize();
  if (typeof ResizeObserver !== 'undefined') {
    new ResizeObserver(resize).observe(area);
  }
  return { canvas: canvas, ctx: ctx, area: area, resize: resize, dpr: function() { return window.devicePixelRatio || 1; }, onResize: function(fn) { _draw = fn; } };
}
function positionTooltip(tt, area, mx, my, w, h) {
  var aW = area.clientWidth;
  var aH = area.clientHeight;
  var ttW = 140;
  var ttH = 72;
  var x = mx + 14;
  var y = my - 16;
  if (x + ttW > aW - 8) x = mx - ttW - 10;
  if (y + ttH > aH - 8) y = aH - ttH - 8;
  if (y < 8) y = 8;
  tt.style.left = x + 'px';
  tt.style.top  = y + 'px';
}
function setupSegCtrl(segId, periods, onChange) {
  var ctrl = document.getElementById(segId);
  if (!ctrl) return;
  var btns = ctrl.querySelectorAll('.seg');
  btns.forEach(function(btn, i) {
    btn.addEventListener('click', function() {
      btns.forEach(function(b) { b.classList.remove('active'); });
      btn.classList.add('active');
      onChange(periods[i]);
    });
  });
}

/* ===================== 1. BAR CHART ===================== */
(function() {
  var r = setupCanvas('c-bars', 'area-bars');
  if (!r) return;
  var ctx = r.ctx, canvas = r.canvas, area = r.area;
  var tt = document.getElementById('tt-bars');

  var PERIODS = ['day', 'week', 'month'];
  var period  = 'day';

  var DATA = {
    day: {
      labels: ['Lun', 'Mar', 'Mié', 'Jue', 'Vie', 'Sáb', 'Dom'],
      claude: [8,  14, 5, 11, 3, 9,  12],
      solo:   [3,   6, 8,  4, 9, 2,   5]
    },
    week: {
      labels: ['S−6', 'S−5', 'S−4', 'S−3', 'S−2', 'S−1', 'Ahora'],
      claude: [42, 65, 28, 71, 38, 55, 89],
      solo:   [18, 32, 45, 22, 60, 20, 35]
    },
    month: {
      labels: ['Sep', 'Oct', 'Nov', 'Dic', 'Ene', 'Feb', 'Mar'],
      claude: [120, 280, 95, 310, 180, 240, 380],
      solo:   [95,  140, 200, 85, 220, 110, 160]
    }
  };

  var hovIdx = -1;
  var animFrom = null;
  var animT    = 1;
  var animStart = 0;
  var ANIM_DUR  = 420;

  function ease(t) { return t < 0.5 ? 2*t*t : -1+(4-2*t)*t; }
  function lerp(a, b, t) { return a + (b - a) * t; }

  function currentVals() {
    var d = DATA[period];
    if (animT >= 1 || !animFrom) return { labels: d.labels, claude: d.claude.slice(), solo: d.solo.slice() };
    var t = ease(animT);
    return {
      labels: d.labels,
      claude: d.claude.map(function(v, i) { return lerp(animFrom.claude[i] || 0, v, t); }),
      solo:   d.solo.map(function(v, i)   { return lerp(animFrom.solo[i]   || 0, v, t); })
    };
  }

  function drawBar(x, y, w, h, color, alpha) {
    ctx.globalAlpha = alpha;
    var r = Math.min(3, w / 2);
    ctx.fillStyle = color;
    ctx.beginPath();
    ctx.roundRect(x, y, w, h, [r, r, 0, 0]);
    ctx.fill();
    if (h > 6) {
      var g = ctx.createLinearGradient(x, y, x, y + Math.min(h * 0.4, 18));
      g.addColorStop(0, 'rgba(255,255,255,0.18)');
      g.addColorStop(1, 'rgba(255,255,255,0)');
      ctx.fillStyle = g;
      ctx.beginPath();
      ctx.roundRect(x, y, w, Math.min(h * 0.4, 18), [r, r, 0, 0]);
      ctx.fill();
    }
    ctx.globalAlpha = 1;
  }

  function draw(ts) {
    if (ts && animT < 1) {
      animT = Math.min((ts - animStart) / ANIM_DUR, 1);
      requestAnimationFrame(draw);
    }
    var d = DATA[period];
    var dpr = r.dpr();
    var W = canvas.width / dpr;
    var H = canvas.height / dpr;
    ctx.clearRect(0, 0, W, H);

    var vals = currentVals();
    var PAD  = { t: 28, r: 18, b: 38, l: 46 };
    var cW   = W - PAD.l - PAD.r;
    var cH   = H - PAD.t - PAD.b;
    var maxV = Math.max.apply(null, d.claude.concat(d.solo)) * 1.18;
    var n    = vals.labels.length;
    var grpW = cW / n;
    var bW   = grpW * 0.28;
    var gap  = grpW * 0.05;

    /* grid */
    ctx.strokeStyle = 'rgba(255,255,255,0.05)';
    ctx.lineWidth = 1;
    ctx.font = '9px JetBrains Mono, monospace';
    ctx.textAlign = 'right';
    for (var gi = 0; gi <= 4; gi++) {
      var gy = PAD.t + cH - (gi / 4) * cH;
      ctx.beginPath(); ctx.moveTo(PAD.l, gy); ctx.lineTo(PAD.l + cW, gy); ctx.stroke();
      ctx.fillStyle = 'rgba(255,255,255,0.18)';
      ctx.fillText(Math.round((gi / 4) * maxV), PAD.l - 6, gy + 3.5);
    }

    /* bars */
    for (var i = 0; i < n; i++) {
      var cx  = PAD.l + i * grpW + grpW / 2;
      var hov = (hovIdx === i);
      var alpha1 = hov ? 1 : (hovIdx === -1 ? 0.78 : 0.3);
      var alpha2 = hov ? 1 : (hovIdx === -1 ? 0.78 : 0.3);

      var h1 = (vals.claude[i] / maxV) * cH;
      drawBar(cx - bW - gap / 2, PAD.t + cH - h1, bW, h1, '#7c6ff7', alpha1);

      var h2 = (vals.solo[i] / maxV) * cH;
      drawBar(cx + gap / 2, PAD.t + cH - h2, bW, h2, '#4ade80', alpha2);

      /* x label */
      ctx.fillStyle = hov ? 'rgba(255,255,255,0.7)' : 'rgba(255,255,255,0.22)';
      ctx.font = '9px JetBrains Mono, monospace';
      ctx.textAlign = 'center';
      ctx.fillText(vals.labels[i], cx, H - PAD.b + 16);
    }

    /* legend */
    function dot(lx, ly, color, label) {
      ctx.fillStyle = color;
      ctx.globalAlpha = 0.85;
      ctx.beginPath(); ctx.arc(lx + 4, ly, 3.5, 0, Math.PI * 2); ctx.fill();
      ctx.globalAlpha = 1;
      ctx.fillStyle = 'rgba(255,255,255,0.28)';
      ctx.font = '8.5px JetBrains Mono, monospace';
      ctx.textAlign = 'left';
      ctx.fillText(label, lx + 11, ly + 3);
    }
    dot(PAD.l + 2, 14, '#7c6ff7', 'con Claude');
    dot(PAD.l + 88, 14, '#4ade80', 'solo');
  }

  area.addEventListener('mousemove', function(e) {
    var dpr = r.dpr();
    var W = canvas.width / dpr;
    var PAD = { t: 28, r: 18, b: 38, l: 46 };
    var cW = W - PAD.l - PAD.r;
    var n  = DATA[period].labels.length;
    var grpW = cW / n;
    var mx = e.offsetX, my = e.offsetY;
    var idx = Math.floor((mx - PAD.l) / grpW);
    if (idx >= 0 && idx < n && mx >= PAD.l && mx <= PAD.l + cW) {
      hovIdx = idx;
      var cv = Math.round(DATA[period].claude[idx]);
      var sv = Math.round(DATA[period].solo[idx]);
      tt.innerHTML = '<div class="tt-title">' + DATA[period].labels[idx] + '</div>' +
        '<span style="color:#7c6ff7">■</span> Claude&nbsp;<span class="tt-val">' + cv + '</span> <span class="tt-dim">archivos</span><br>' +
        '<span style="color:#4ade80">■</span> Solo&nbsp;&nbsp;&nbsp;<span class="tt-val">' + sv + '</span> <span class="tt-dim">archivos</span>';
      positionTooltip(tt, area, mx, my);
      tt.classList.add('show');
    } else {
      hovIdx = -1;
      tt.classList.remove('show');
    }
    draw();
  });
  area.addEventListener('mouseleave', function() { hovIdx = -1; tt.classList.remove('show'); draw(); });

  r.onResize(draw);
  requestAnimationFrame(draw);
  setupSegCtrl('seg-bars', PERIODS, function(p) {
    animFrom = currentVals();
    while (animFrom.claude.length < DATA[p].claude.length) { animFrom.claude.push(0); animFrom.solo.push(0); }
    period = p;
    animT = 0;
    animStart = performance.now();
    requestAnimationFrame(draw);
  });
})();


/* ===================== 2. PIE / DONUT CHART ===================== */
(function() {
  var r = setupCanvas('c-pie', 'area-pie');
  if (!r) return;
  var ctx = r.ctx, canvas = r.canvas, area = r.area;
  var tt = document.getElementById('tt-pie');

  var PERIODS = ['day', 'week', 'month'];
  var period  = 'day';

  var COLORS = ['#7c6ff7', '#ef4444', '#4ade80', '#f59e0b', '#60a5fa'];
  var DATA = {
    day: [
      { label: 'Feature',  val: 35 },
      { label: 'Fix',      val: 28 },
      { label: 'Style',    val: 18 },
      { label: 'Docs',     val: 12 },
      { label: 'Refactor', val: 7  }
    ],
    week: [
      { label: 'Feature',  val: 42 },
      { label: 'Fix',      val: 22 },
      { label: 'Style',    val: 15 },
      { label: 'Refactor', val: 13 },
      { label: 'Docs',     val: 8  }
    ],
    month: [
      { label: 'Feature',  val: 38 },
      { label: 'Fix',      val: 18 },
      { label: 'Style',    val: 20 },
      { label: 'Refactor', val: 12 },
      { label: 'Docs',     val: 12 }
    ]
  };

  var hovSeg   = -1;
  var animFrom = null;
  var animT    = 1;
  var animStart = 0;
  var ANIM_DUR  = 380;
  var segments = []; /* [{startAngle, endAngle, color, label, val, pct}] */

  function ease(t) { return t < 0.5 ? 2*t*t : -1+(4-2*t)*t; }
  function lerp(a, b, t) { return a + (b - a) * t; }

  function currentVals() {
    var d = DATA[period];
    if (animT >= 1 || !animFrom) return d.map(function(s) { return s.val; });
    var t = ease(animT);
    return d.map(function(s, i) { return lerp(animFrom[i] || 0, s.val, t); });
  }

  function draw(ts) {
    if (ts && animT < 1) {
      animT = Math.min((ts - animStart) / ANIM_DUR, 1);
      requestAnimationFrame(draw);
    }
    var dpr = r.dpr();
    var W = canvas.width / dpr;
    var H = canvas.height / dpr;
    ctx.clearRect(0, 0, W, H);

    var d    = DATA[period];
    var vals = currentVals();
    var total = vals.reduce(function(a, b) { return a + b; }, 0);
    var cx = W * 0.38, cy = H / 2;
    var outerR = Math.min(cx, cy) - 12;
    var innerR = outerR * 0.58;

    var angle = -Math.PI / 2;
    segments = [];
    for (var i = 0; i < d.length; i++) {
      var sweep = (vals[i] / total) * Math.PI * 2;
      var isHov = (hovSeg === i);
      var expand = isHov ? 6 : 0;
      var midA = angle + sweep / 2;
      var ox = Math.cos(midA) * expand;
      var oy = Math.sin(midA) * expand;

      ctx.beginPath();
      ctx.moveTo(cx + ox, cy + oy);
      ctx.arc(cx + ox, cy + oy, outerR + (isHov ? 4 : 0), angle, angle + sweep);
      ctx.arc(cx + ox, cy + oy, innerR - (isHov ? 2 : 0), angle + sweep, angle, true);
      ctx.closePath();
      ctx.fillStyle = COLORS[i % COLORS.length];
      ctx.globalAlpha = isHov ? 1 : (hovSeg === -1 ? 0.82 : 0.35);
      ctx.fill();
      if (isHov) {
        ctx.strokeStyle = 'rgba(255,255,255,0.25)';
        ctx.lineWidth = 1.5;
        ctx.stroke();
      }
      ctx.globalAlpha = 1;

      segments.push({ startAngle: angle, endAngle: angle + sweep, color: COLORS[i % COLORS.length], label: d[i].label, val: Math.round(vals[i]), pct: Math.round(vals[i] / total * 100) });
      angle += sweep;
    }

    /* center label */
    var hovD = hovSeg >= 0 ? d[hovSeg] : null;
    ctx.textAlign = 'center';
    if (hovD) {
      ctx.fillStyle = COLORS[hovSeg % COLORS.length];
      ctx.font = '700 13px JetBrains Mono, monospace';
      ctx.fillText(segments[hovSeg].pct + '%', cx, cy + 5);
      ctx.fillStyle = 'rgba(255,255,255,0.35)';
      ctx.font = '8px JetBrains Mono, monospace';
      ctx.fillText(hovD.label.toUpperCase(), cx, cy + 20);
    } else {
      ctx.fillStyle = 'rgba(255,255,255,0.5)';
      ctx.font = '700 12px JetBrains Mono, monospace';
      ctx.fillText(d.length + ' tipos', cx, cy + 5);
    }

    /* legend */
    var legX = W * 0.64;
    var legY = cy - (d.length * 20) / 2 + 4;
    for (var j = 0; j < d.length; j++) {
      var isH = (hovSeg === j);
      ctx.globalAlpha = isH ? 1 : (hovSeg === -1 ? 0.72 : 0.3);
      ctx.fillStyle = COLORS[j % COLORS.length];
      ctx.beginPath(); ctx.roundRect(legX, legY + j * 22, 10, 10, 2); ctx.fill();
      ctx.fillStyle = isH ? 'rgba(255,255,255,0.85)' : 'rgba(255,255,255,0.35)';
      ctx.font = (isH ? '600 ' : '') + '9.5px JetBrains Mono, monospace';
      ctx.textAlign = 'left';
      ctx.fillText(d[j].label, legX + 16, legY + j * 22 + 9);
      ctx.globalAlpha = 1;
    }
  }

  area.addEventListener('mousemove', function(e) {
    var dpr = r.dpr();
    var W = canvas.width / dpr;
    var H = canvas.height / dpr;
    var mx = e.offsetX, my = e.offsetY;
    var cx = W * 0.38, cy = H / 2;
    var outerR = Math.min(cx, cy) - 12;
    var innerR = outerR * 0.58;
    var dx = mx - cx, dy = my - cy;
    var dist = Math.sqrt(dx * dx + dy * dy);
    hovSeg = -1;
    if (dist >= innerR && dist <= outerR + 8) {
      var ang = Math.atan2(dy, dx);
      if (ang < -Math.PI / 2) ang += Math.PI * 2;
      for (var i = 0; i < segments.length; i++) {
        var s = segments[i];
        var sa = s.startAngle, ea = s.endAngle;
        if (sa < -Math.PI / 2) { sa += Math.PI * 2; ea += Math.PI * 2; }
        if (ang >= sa && ang <= ea) { hovSeg = i; break; }
      }
    }
    if (hovSeg >= 0) {
      var s = segments[hovSeg];
      tt.innerHTML = '<div class="tt-title">' + s.label + '</div>' +
        '<span class="tt-val">' + s.pct + '%</span> <span class="tt-dim">de commits</span><br>' +
        '<span class="tt-dim">~' + s.val + ' este período</span>';
      positionTooltip(tt, area, mx, my);
      tt.classList.add('show');
    } else {
      tt.classList.remove('show');
    }
    draw();
  });
  area.addEventListener('mouseleave', function() { hovSeg = -1; tt.classList.remove('show'); draw(); });

  r.onResize(draw);
  requestAnimationFrame(draw);
  setupSegCtrl('seg-pie', PERIODS, function(p) {
    animFrom = currentVals();
    while (animFrom.length < DATA[p].length) animFrom.push(0);
    period = p;
    animT = 0;
    animStart = performance.now();
    requestAnimationFrame(draw);
  });
})();


/* ===================== 3. PENTAGON / RADAR ===================== */
(function() {
  var r = setupCanvas('c-penta', 'area-penta');
  if (!r) return;
  var ctx = r.ctx, canvas = r.canvas, area = r.area;
  var tt = document.getElementById('tt-penta');

  var PERIODS = ['day', 'week', 'month'];
  var period  = 'day';
  var SKILLS  = ['Velocidad', 'Precisión', 'Creatividad', 'Contexto', 'Debug'];
  var DATA = {
    day:   [75, 88, 70, 82, 91],
    week:  [82, 90, 78, 88, 94],
    month: [89, 93, 85, 91, 96]
  };

  var hovVtx   = -1;
  var animFrom = null;
  var animT    = 1;
  var animStart = 0;
  var ANIM_DUR  = 450;
  var vtxPoints = [];

  function ease(t) { return t < 0.5 ? 2*t*t : -1+(4-2*t)*t; }
  function lerp(a, b, t) { return a + (b - a) * t; }

  function currentVals() {
    var d = DATA[period];
    if (animT >= 1 || !animFrom) return d.slice();
    var t = ease(animT);
    return d.map(function(v, i) { return lerp(animFrom[i] || 0, v, t); });
  }

  function vtxPos(cx, cy, radius, i, total) {
    var angle = (i / total) * Math.PI * 2 - Math.PI / 2;
    return { x: cx + Math.cos(angle) * radius, y: cy + Math.sin(angle) * radius };
  }

  function draw(ts) {
    if (ts && animT < 1) {
      animT = Math.min((ts - animStart) / ANIM_DUR, 1);
      requestAnimationFrame(draw);
    }
    var dpr = r.dpr();
    var W = canvas.width / dpr;
    var H = canvas.height / dpr;
    ctx.clearRect(0, 0, W, H);

    var vals = currentVals();
    var N   = SKILLS.length;
    var cx  = W / 2;
    var cy  = H / 2 + 6;
    var maxR = Math.min(W, H) / 2 - 36;

    /* background grid */
    var levels = [0.25, 0.5, 0.75, 1.0];
    levels.forEach(function(lv) {
      ctx.beginPath();
      for (var i = 0; i < N; i++) {
        var p = vtxPos(cx, cy, maxR * lv, i, N);
        if (i === 0) ctx.moveTo(p.x, p.y); else ctx.lineTo(p.x, p.y);
      }
      ctx.closePath();
      ctx.strokeStyle = lv === 1.0 ? 'rgba(255,255,255,0.08)' : 'rgba(255,255,255,0.04)';
      ctx.lineWidth = 1;
      ctx.stroke();
    });

    /* axis lines */
    for (var i = 0; i < N; i++) {
      var p = vtxPos(cx, cy, maxR, i, N);
      ctx.beginPath(); ctx.moveTo(cx, cy); ctx.lineTo(p.x, p.y);
      ctx.strokeStyle = 'rgba(255,255,255,0.05)';
      ctx.stroke();
    }

    /* data polygon */
    ctx.beginPath();
    vtxPoints = [];
    for (var i = 0; i < N; i++) {
      var p = vtxPos(cx, cy, maxR * (vals[i] / 100), i, N);
      vtxPoints.push(p);
      if (i === 0) ctx.moveTo(p.x, p.y); else ctx.lineTo(p.x, p.y);
    }
    ctx.closePath();
    ctx.fillStyle = 'rgba(124,111,247,0.12)';
    ctx.fill();
    ctx.strokeStyle = '#7c6ff7';
    ctx.lineWidth = 1.5;
    ctx.globalAlpha = 0.85;
    ctx.stroke();
    ctx.globalAlpha = 1;

    /* vertices */
    for (var i = 0; i < N; i++) {
      var p = vtxPoints[i];
      var isHov = (hovVtx === i);
      ctx.beginPath(); ctx.arc(p.x, p.y, isHov ? 5.5 : 3.5, 0, Math.PI * 2);
      ctx.fillStyle = isHov ? '#fff' : '#7c6ff7';
      ctx.fill();
      if (isHov) {
        ctx.strokeStyle = '#7c6ff7';
        ctx.lineWidth = 1.5;
        ctx.stroke();
      }
    }

    /* skill labels */
    for (var i = 0; i < N; i++) {
      var lp  = vtxPos(cx, cy, maxR + 22, i, N);
      var isH = (hovVtx === i);
      ctx.fillStyle = isH ? 'rgba(255,255,255,0.85)' : 'rgba(255,255,255,0.28)';
      ctx.font = (isH ? '600 ' : '') + '8.5px JetBrains Mono, monospace';
      ctx.textAlign = 'center';
      ctx.fillText(SKILLS[i].toUpperCase(), lp.x, lp.y + 3);
    }
  }

  area.addEventListener('mousemove', function(e) {
    var mx = e.offsetX, my = e.offsetY;
    var THRESH = 24;
    hovVtx = -1;
    var bestDist = THRESH;
    for (var i = 0; i < vtxPoints.length; i++) {
      var dx = mx - vtxPoints[i].x;
      var dy = my - vtxPoints[i].y;
      var dist = Math.sqrt(dx * dx + dy * dy);
      if (dist < bestDist) { bestDist = dist; hovVtx = i; }
    }
    if (hovVtx >= 0) {
      var realVal = DATA[period][hovVtx];
      tt.innerHTML = '<div class="tt-title">' + SKILLS[hovVtx] + '</div>' +
        '<span class="tt-val">' + realVal + '</span><span class="tt-dim"> / 100</span>';
      positionTooltip(tt, area, mx, my);
      tt.classList.add('show');
    } else {
      tt.classList.remove('show');
    }
    draw();
  });
  area.addEventListener('mouseleave', function() { hovVtx = -1; tt.classList.remove('show'); draw(); });

  r.onResize(draw);
  requestAnimationFrame(draw);
  setupSegCtrl('seg-penta', PERIODS, function(p) {
    animFrom = currentVals();
    period = p;
    animT = 0;
    animStart = performance.now();
    requestAnimationFrame(draw);
  });
})();


/* ===================== 4. LINE CHART ===================== */
(function() {
  var r = setupCanvas('c-line', 'area-line');
  if (!r) return;
  var ctx = r.ctx, canvas = r.canvas, area = r.area;
  var tt = document.getElementById('tt-line');

  var PERIODS = ['day', 'week', 'month'];
  var period  = 'day';

  var DATA = {
    day: {
      labels: ['00h','01h','02h','03h','04h','05h','06h','07h','08h','09h','10h','11h','12h','13h','14h','15h','16h','17h','18h','19h','20h','21h','22h','23h'],
      vals:   [10,7,4,3,2,3,12,38,72,90,108,85,72,115,130,138,122,92,68,52,36,24,16,9]
    },
    week: {
      labels: ['Lun','Mar','Mié','Jue','Vie','Sáb','Dom'],
      vals:   [280, 320, 195, 410, 385, 140, 90]
    },
    month: {
      labels: ['1','5','10','15','20','25','30'],
      vals:   [180, 260, 310, 390, 480, 620, 890]
    }
  };

  var hovPt    = -1;
  var animFrom = null;
  var animT    = 1;
  var animStart = 0;
  var ANIM_DUR  = 480;

  function ease(t) { return t < 0.5 ? 2*t*t : -1+(4-2*t)*t; }
  function lerp(a, b, t) { return a + (b - a) * t; }

  function currentVals() {
    var d = DATA[period].vals;
    if (animT >= 1 || !animFrom) return d.slice();
    var t = ease(animT);
    var len = Math.max(d.length, animFrom.length);
    var result = [];
    for (var i = 0; i < d.length; i++) {
      result.push(lerp(animFrom[Math.round(i / d.length * (animFrom.length - 1))] || 0, d[i], t));
    }
    return result;
  }

  function draw(ts) {
    if (ts && animT < 1) {
      animT = Math.min((ts - animStart) / ANIM_DUR, 1);
      requestAnimationFrame(draw);
    }
    var dpr = r.dpr();
    var W = canvas.width / dpr;
    var H = canvas.height / dpr;
    ctx.clearRect(0, 0, W, H);

    var vals = currentVals();
    var lbls = DATA[period].labels;
    var PAD  = { t: 20, r: 18, b: 38, l: 46 };
    var cW   = W - PAD.l - PAD.r;
    var cH   = H - PAD.t - PAD.b;
    var maxV = Math.max.apply(null, vals) * 1.18;
    var n    = vals.length;

    /* grid */
    ctx.strokeStyle = 'rgba(255,255,255,0.05)';
    ctx.lineWidth = 1;
    ctx.font = '9px JetBrains Mono, monospace';
    ctx.textAlign = 'right';
    for (var gi = 0; gi <= 4; gi++) {
      var gy = PAD.t + cH - (gi / 4) * cH;
      ctx.beginPath(); ctx.moveTo(PAD.l, gy); ctx.lineTo(PAD.l + cW, gy); ctx.stroke();
      ctx.fillStyle = 'rgba(255,255,255,0.18)';
      ctx.fillText(Math.round((gi / 4) * maxV), PAD.l - 6, gy + 3.5);
    }

    /* x labels — show subset */
    var step = Math.ceil(n / 6);
    ctx.fillStyle = 'rgba(255,255,255,0.22)';
    ctx.font = '9px JetBrains Mono, monospace';
    ctx.textAlign = 'center';
    for (var i = 0; i < n; i += step) {
      var px = PAD.l + (i / (n - 1)) * cW;
      ctx.fillText(lbls[i], px, H - PAD.b + 16);
    }

    /* compute points */
    var pts = vals.map(function(v, i) {
      return { x: PAD.l + (i / (n - 1)) * cW, y: PAD.t + cH - (v / maxV) * cH };
    });

    /* area fill */
    ctx.beginPath();
    ctx.moveTo(pts[0].x, PAD.t + cH);
    ctx.lineTo(pts[0].x, pts[0].y);
    for (var i = 1; i < pts.length; i++) {
      var cpx = (pts[i-1].x + pts[i].x) / 2;
      ctx.bezierCurveTo(cpx, pts[i-1].y, cpx, pts[i].y, pts[i].x, pts[i].y);
    }
    ctx.lineTo(pts[pts.length-1].x, PAD.t + cH);
    ctx.closePath();
    var grad = ctx.createLinearGradient(0, PAD.t, 0, PAD.t + cH);
    grad.addColorStop(0, 'rgba(124,111,247,0.18)');
    grad.addColorStop(1, 'rgba(124,111,247,0)');
    ctx.fillStyle = grad;
    ctx.fill();

    /* line */
    ctx.beginPath();
    ctx.moveTo(pts[0].x, pts[0].y);
    for (var i = 1; i < pts.length; i++) {
      var cpx = (pts[i-1].x + pts[i].x) / 2;
      ctx.bezierCurveTo(cpx, pts[i-1].y, cpx, pts[i].y, pts[i].x, pts[i].y);
    }
    ctx.strokeStyle = '#7c6ff7';
    ctx.lineWidth   = 1.75;
    ctx.globalAlpha = 0.9;
    ctx.stroke();
    ctx.globalAlpha = 1;

    /* hover vertical line + dot */
    if (hovPt >= 0 && hovPt < pts.length) {
      var p = pts[hovPt];
      ctx.strokeStyle = 'rgba(255,255,255,0.12)';
      ctx.lineWidth = 1;
      ctx.setLineDash([3, 3]);
      ctx.beginPath(); ctx.moveTo(p.x, PAD.t); ctx.lineTo(p.x, PAD.t + cH);
      ctx.stroke();
      ctx.setLineDash([]);

      ctx.beginPath(); ctx.arc(p.x, p.y, 4.5, 0, Math.PI * 2);
      ctx.fillStyle = '#7c6ff7'; ctx.fill();
      ctx.beginPath(); ctx.arc(p.x, p.y, 2.5, 0, Math.PI * 2);
      ctx.fillStyle = '#fff'; ctx.fill();
    }
  }

  area.addEventListener('mousemove', function(e) {
    var dpr = r.dpr();
    var W = canvas.width / dpr;
    var PAD = { t: 20, r: 18, b: 38, l: 46 };
    var cW = W - PAD.l - PAD.r;
    var n  = DATA[period].vals.length;
    var mx = e.offsetX, my = e.offsetY;
    var idx = Math.round((mx - PAD.l) / cW * (n - 1));
    idx = Math.max(0, Math.min(n - 1, idx));
    if (mx >= PAD.l && mx <= PAD.l + cW) {
      hovPt = idx;
      var v = Math.round(DATA[period].vals[idx]);
      var lbl = DATA[period].labels[idx];
      tt.innerHTML = '<div class="tt-title">' + lbl + '</div>' +
        '<span class="tt-val">' + v + '</span><span class="tt-dim"> tokens</span>';
      positionTooltip(tt, area, mx, my);
      tt.classList.add('show');
    } else {
      hovPt = -1;
      tt.classList.remove('show');
    }
    draw();
  });
  area.addEventListener('mouseleave', function() { hovPt = -1; tt.classList.remove('show'); draw(); });

  r.onResize(draw);
  requestAnimationFrame(draw);
  setupSegCtrl('seg-line', PERIODS, function(p) {
    animFrom = currentVals();
    period = p;
    animT = 0;
    animStart = performance.now();
    requestAnimationFrame(draw);
  });
})();


/* ===================== 5. ACTIVITY RINGS ===================== */
(function() {
  var r = setupCanvas('c-rings', 'area-rings');
  if (!r) return;
  var ctx = r.ctx, canvas = r.canvas, area = r.area;
  var tt = document.getElementById('tt-rings');

  var PERIODS = ['day', 'week', 'month'];
  var period  = 'day';

  var RINGS = [
    { key: 'commits', label: 'Commits',  color: '#7c6ff7', track: 'rgba(124,111,247,0.1)' },
    { key: 'tests',   label: 'Tests',    color: '#4ade80', track: 'rgba(74,222,128,0.08)'  },
    { key: 'docs',    label: 'Docs',     color: '#f59e0b', track: 'rgba(245,158,11,0.08)'  }
  ];

  var DATA = {
    day:   { commits: { pct: 72, curr: 18, total: 25 }, tests: { pct: 45, curr:  9, total: 20 }, docs: { pct: 28, curr:  7, total: 25 } },
    week:  { commits: { pct: 88, curr: 22, total: 25 }, tests: { pct: 62, curr:  5, total:  8 }, docs: { pct: 41, curr: 12, total: 30 } },
    month: { commits: { pct: 95, curr: 95, total:100 }, tests: { pct: 78, curr: 31, total: 40 }, docs: { pct: 65, curr: 65, total:100 } }
  };

  var hovRing  = -1;
  var animFrom = null;
  var animT    = 1;
  var animStart = 0;
  var ANIM_DUR  = 520;

  function ease(t) { return 1 - Math.pow(1 - t, 3); }
  function lerp(a, b, t) { return a + (b - a) * t; }

  function currentPcts() {
    var d = DATA[period];
    var base = RINGS.map(function(rg) { return d[rg.key].pct / 100; });
    if (animT >= 1 || !animFrom) return base;
    var t = ease(animT);
    return base.map(function(v, i) { return lerp(animFrom[i] || 0, v, t); });
  }

  function draw(ts) {
    if (ts && animT < 1) {
      animT = Math.min((ts - animStart) / ANIM_DUR, 1);
      requestAnimationFrame(draw);
    }
    var dpr = r.dpr();
    var W = canvas.width / dpr;
    var H = canvas.height / dpr;
    ctx.clearRect(0, 0, W, H);

    var pcts = currentPcts();
    var cx   = W * 0.4;
    var cy   = H / 2;
    var GAP  = 16;
    var THICK = 18;
    var maxR = Math.min(cx, cy) - 14;
    var START = -Math.PI / 2;

    for (var i = 0; i < RINGS.length; i++) {
      var rg  = RINGS[i];
      var rad = maxR - i * (THICK + GAP);
      var isH = (hovRing === i);

      /* track */
      ctx.beginPath();
      ctx.arc(cx, cy, rad, 0, Math.PI * 2);
      ctx.strokeStyle = rg.track;
      ctx.lineWidth   = THICK + (isH ? 2 : 0);
      ctx.lineCap     = 'round';
      ctx.stroke();

      /* progress */
      var sweep = pcts[i] * Math.PI * 2;
      if (sweep > 0.01) {
        ctx.beginPath();
        ctx.arc(cx, cy, rad, START, START + sweep);
        ctx.strokeStyle = rg.color;
        ctx.lineWidth   = THICK + (isH ? 2 : 0);
        ctx.globalAlpha = isH ? 1 : (hovRing === -1 ? 0.85 : 0.35);
        ctx.lineCap     = 'round';
        ctx.stroke();
        ctx.globalAlpha = 1;
      }
    }

    /* legend on the right */
    var legX = W * 0.66;
    var legY = cy - RINGS.length * 28 / 2 + 8;
    for (var i = 0; i < RINGS.length; i++) {
      var rg  = RINGS[i];
      var isH = (hovRing === i);
      var d   = DATA[period][rg.key];

      ctx.globalAlpha = isH ? 1 : (hovRing === -1 ? 0.72 : 0.28);
      ctx.fillStyle = rg.color;
      ctx.beginPath(); ctx.arc(legX, legY + i * 28 + 5, 5, 0, Math.PI * 2); ctx.fill();

      ctx.fillStyle = isH ? 'rgba(255,255,255,0.85)' : 'rgba(255,255,255,0.35)';
      ctx.font = (isH ? '600 ' : '') + '9px JetBrains Mono, monospace';
      ctx.textAlign = 'left';
      ctx.fillText(rg.label.toUpperCase(), legX + 13, legY + i * 28 + 4);

      ctx.fillStyle = isH ? rg.color : 'rgba(255,255,255,0.22)';
      ctx.font = '700 11px JetBrains Mono, monospace';
      ctx.fillText(d.pct + '%', legX + 13, legY + i * 28 + 18);
      ctx.globalAlpha = 1;
    }
  }

  area.addEventListener('mousemove', function(e) {
    var dpr = r.dpr();
    var W = canvas.width / dpr;
    var H = canvas.height / dpr;
    var mx = e.offsetX, my = e.offsetY;
    var cx = W * 0.4, cy = H / 2;
    var GAP = 16, THICK = 18;
    var maxR = Math.min(cx, cy) - 14;
    var dx = mx - cx, dy = my - cy;
    var dist = Math.sqrt(dx * dx + dy * dy);
    hovRing = -1;
    for (var i = 0; i < RINGS.length; i++) {
      var rad = maxR - i * (THICK + GAP);
      if (Math.abs(dist - rad) <= THICK / 2 + 5) { hovRing = i; break; }
    }
    if (hovRing >= 0) {
      var d   = DATA[period][RINGS[hovRing].key];
      var rg  = RINGS[hovRing];
      tt.innerHTML = '<div class="tt-title">' + rg.label + '</div>' +
        '<span class="tt-val" style="color:' + rg.color + '">' + d.pct + '%</span><br>' +
        '<span class="tt-dim">' + d.curr + ' / ' + d.total + ' completados</span>';
      positionTooltip(tt, area, mx, my);
      tt.classList.add('show');
    } else {
      tt.classList.remove('show');
    }
    draw();
  });
  area.addEventListener('mouseleave', function() { hovRing = -1; tt.classList.remove('show'); draw(); });

  r.onResize(draw);
  requestAnimationFrame(draw);
  setupSegCtrl('seg-rings', PERIODS, function(p) {
    animFrom = currentPcts();
    period = p;
    animT = 0;
    animStart = performance.now();
    requestAnimationFrame(draw);
  });
})();

/* ===================== WIDGET HELPERS ===================== */
function wSetup(canvasId, wrapId, drawFn) {
  var canvas = document.getElementById(canvasId);
  var wrap   = document.getElementById(wrapId);
  if (!canvas || !wrap) return;
  var ctx = canvas.getContext('2d');
  function resize() {
    var dpr = window.devicePixelRatio || 1;
    var W = wrap.clientWidth, H = wrap.clientHeight;
    canvas.width  = W * dpr; canvas.height = H * dpr;
    canvas.style.width = W + 'px'; canvas.style.height = H + 'px';
    ctx.setTransform(dpr, 0, 0, dpr, 0, 0);
    if (W > 0 && H > 0) drawFn(ctx, W, H);
  }
  if (typeof ResizeObserver !== 'undefined') new ResizeObserver(resize).observe(wrap);
  requestAnimationFrame(resize);
  return { ctx: ctx, wrap: wrap, redraw: function() { drawFn(ctx, wrap.clientWidth, wrap.clientHeight); } };
}
function wTT(tt, wrap, mx, my, html) {
  tt.innerHTML = html;
  var x = mx + 10, y = my - 36;
  if (x + 110 > wrap.clientWidth) x = mx - 118;
  if (y < 4) y = my + 10;
  tt.style.left = x + 'px'; tt.style.top = y + 'px';
  tt.classList.add('show');
}

/* ---- 1. SPARKLINE ---- */
(function() {
  var DATA = [65,58,72,48,61,79,55,68,74,62,83,71];
  var hovIdx = -1;
  var tt = document.getElementById('wt-spark');
  var wrap = document.getElementById('ww-spark');

  function draw(ctx, W, H) {
    ctx.clearRect(0, 0, W, H);
    var PAD = {t:8, r:6, b:26, l:6}, n = DATA.length;
    var cW = W - PAD.l - PAD.r, cH = H - PAD.t - PAD.b;
    var mn = Math.min.apply(null,DATA)*0.92, mx2 = Math.max.apply(null,DATA)*1.06;
    var pts = DATA.map(function(v,i){ return {x:PAD.l+(i/(n-1))*cW, y:PAD.t+cH-((v-mn)/(mx2-mn))*cH}; });

    ctx.beginPath(); ctx.moveTo(pts[0].x, PAD.t+cH); ctx.lineTo(pts[0].x, pts[0].y);
    for (var i=1;i<pts.length;i++){var cx=(pts[i-1].x+pts[i].x)/2;ctx.bezierCurveTo(cx,pts[i-1].y,cx,pts[i].y,pts[i].x,pts[i].y);}
    ctx.lineTo(pts[pts.length-1].x, PAD.t+cH); ctx.closePath();
    var g=ctx.createLinearGradient(0,PAD.t,0,PAD.t+cH);
    g.addColorStop(0,'rgba(124,111,247,0.28)'); g.addColorStop(1,'rgba(124,111,247,0)');
    ctx.fillStyle=g; ctx.fill();

    ctx.beginPath(); ctx.moveTo(pts[0].x,pts[0].y);
    for (var i=1;i<pts.length;i++){var cx=(pts[i-1].x+pts[i].x)/2;ctx.bezierCurveTo(cx,pts[i-1].y,cx,pts[i].y,pts[i].x,pts[i].y);}
    ctx.strokeStyle='#7c6ff7'; ctx.lineWidth=1.5; ctx.stroke();

    ctx.fillStyle='#fff'; ctx.font='700 20px JetBrains Mono,monospace'; ctx.textAlign='left';
    ctx.fillText(DATA[DATA.length-1], PAD.l, H-6);
    ctx.fillStyle='rgba(255,255,255,0.3)'; ctx.font='8px JetBrains Mono,monospace';
    ctx.fillText('ms', PAD.l+28, H-6);

    if (hovIdx>=0) {
      var p=pts[hovIdx];
      ctx.beginPath(); ctx.arc(p.x,p.y,3.5,0,Math.PI*2); ctx.fillStyle='#7c6ff7'; ctx.fill();
      ctx.beginPath(); ctx.arc(p.x,p.y,2,0,Math.PI*2); ctx.fillStyle='#fff'; ctx.fill();
    }
  }

  var h = wSetup('wc-spark','ww-spark',draw);
  if (!h || !wrap || !tt) return;
  wrap.addEventListener('mousemove', function(e) {
    var W=wrap.clientWidth, PAD={l:6,r:6}, cW=W-PAD.l-PAD.r, n=DATA.length;
    var idx=Math.round((e.offsetX-PAD.l)/cW*(n-1)); idx=Math.max(0,Math.min(n-1,idx));
    hovIdx=idx;
    wTT(tt,wrap,e.offsetX,e.offsetY,'<span class="tt-val">'+DATA[idx]+'</span><span class="tt-dim"> ms</span>');
    h.redraw();
  });
  wrap.addEventListener('mouseleave',function(){hovIdx=-1;tt.classList.remove('show');h.redraw();});
})();

/* ---- 2. GAUGE (semicircle) ---- */
(function() {
  var VALUE = 68;
  var tt = document.getElementById('wt-gauge');
  var wrap = document.getElementById('ww-gauge');

  function draw(ctx, W, H) {
    ctx.clearRect(0,0,W,H);
    var cx=W/2, cy=H*0.62, r=Math.min(W,H*1.3)*0.38;
    var START=Math.PI*0.85, END=Math.PI*2.15, pct=VALUE/100;

    ctx.beginPath(); ctx.arc(cx,cy,r,START,END);
    ctx.strokeStyle='rgba(255,255,255,0.06)'; ctx.lineWidth=10; ctx.lineCap='round'; ctx.stroke();

    ctx.beginPath(); ctx.arc(cx,cy,r,START,START+(END-START)*pct);
    var g=ctx.createLinearGradient(cx-r,cy,cx+r,cy);
    g.addColorStop(0,'#4ade80'); g.addColorStop(0.5,'#7c6ff7'); g.addColorStop(1,'#ef4444');
    ctx.strokeStyle=g; ctx.lineWidth=10; ctx.lineCap='round'; ctx.stroke();

    ctx.fillStyle='#fff'; ctx.font='700 28px JetBrains Mono,monospace'; ctx.textAlign='center';
    ctx.fillText(VALUE+'%', cx, cy+10);
    ctx.fillStyle='rgba(255,255,255,0.28)'; ctx.font='8px JetBrains Mono,monospace';
    ctx.fillText('CPU', cx, cy+26);

    ctx.fillStyle='rgba(255,255,255,0.18)'; ctx.font='8px JetBrains Mono,monospace';
    ctx.textAlign='left'; ctx.fillText('0', cx-r+2, cy+18);
    ctx.textAlign='right'; ctx.fillText('100', cx+r-2, cy+18);
  }

  var h = wSetup('wc-gauge','ww-gauge',draw);
  if (!h || !wrap || !tt) return;
  wrap.addEventListener('mousemove', function(e) {
    wTT(tt,wrap,e.offsetX,e.offsetY,'<span class="tt-val">'+VALUE+'%</span> <span class="tt-dim">· 2.4 GHz</span>');
  });
  wrap.addEventListener('mouseleave',function(){tt.classList.remove('show');});
})();

/* ---- 3. HEATMAP ---- */
(function() {
  var COLS=7, ROWS=5;
  var DATA=(function(){var d=[];for(var i=0;i<COLS*ROWS;i++)d.push(Math.round(Math.random()*9));return d;})();
  DATA[34]=9;DATA[33]=8;DATA[27]=7;DATA[26]=8;DATA[20]=6;
  var DAYS=['L','M','X','J','V','S','D'];
  var hovIdx=-1;
  var tt=document.getElementById('wt-heat');
  var wrap=document.getElementById('ww-heat');
  var cells=[];

  function draw(ctx,W,H){
    ctx.clearRect(0,0,W,H);
    var PAD={t:4,r:4,b:4,l:4};
    var cellW=(W-PAD.l-PAD.r)/COLS, cellH=(H-PAD.t-PAD.b)/ROWS;
    cells=[];
    for(var r=0;r<ROWS;r++) for(var c=0;c<COLS;c++){
      var idx=r*COLS+c, v=DATA[idx], isH=(hovIdx===idx);
      var x=PAD.l+c*cellW+2, y=PAD.t+r*cellH+2, w=cellW-4, h=cellH-4;
      cells.push({x:PAD.l+c*cellW,y:PAD.t+r*cellH,w:cellW,h:cellH,idx:idx,v:v,col:c,row:r});
      var alpha=v/9*0.85+0.05;
      ctx.fillStyle=isH?'rgba(74,222,128,1)':'rgba(74,222,128,'+alpha+')';
      ctx.beginPath(); ctx.roundRect(x,y,w,h,3); ctx.fill();
    }
  }

  var h=wSetup('wc-heat','ww-heat',draw);
  if(!h||!wrap||!tt)return;
  wrap.addEventListener('mousemove',function(e){
    hovIdx=-1;
    for(var i=0;i<cells.length;i++){var c=cells[i];if(e.offsetX>=c.x&&e.offsetX<=c.x+c.w&&e.offsetY>=c.y&&e.offsetY<=c.y+c.h){hovIdx=c.idx;wTT(tt,wrap,e.offsetX,e.offsetY,'<span class="tt-dim">'+DAYS[c.col]+'</span> <span class="tt-val">'+c.v+'</span><span class="tt-dim"> commits</span>');break;}}
    if(hovIdx<0)tt.classList.remove('show');
    h.redraw();
  });
  wrap.addEventListener('mouseleave',function(){hovIdx=-1;tt.classList.remove('show');h.redraw();});
})();

/* ---- 4. SCATTER ---- */
(function() {
  var PTS=[
    {x:42,y:71,label:'GPT-4'},{x:78,y:88,label:'Claude'},{x:31,y:60,label:'Gemini'},
    {x:55,y:79,label:'Mistral'},{x:88,y:92,label:'Claude 3'},{x:22,y:55,label:'Llama'},
    {x:65,y:82,label:'Grok'},{x:90,y:95,label:'Opus'},{x:48,y:74,label:'Sonnet'},
    {x:35,y:65,label:'GPT-3.5'},{x:72,y:85,label:'Gemini P'},{x:18,y:48,label:'Mixtral'}
  ];
  var hovIdx=-1;
  var tt=document.getElementById('wt-scatter');
  var wrap=document.getElementById('ww-scatter');
  var drawnPts=[];

  function draw(ctx,W,H){
    ctx.clearRect(0,0,W,H);
    var PAD={t:8,r:8,b:22,l:22};
    var cW=W-PAD.l-PAD.r, cH=H-PAD.t-PAD.b;

    ctx.strokeStyle='rgba(255,255,255,0.04)'; ctx.lineWidth=1;
    for(var i=1;i<=3;i++){var gy=PAD.t+cH-(i/4)*cH;ctx.beginPath();ctx.moveTo(PAD.l,gy);ctx.lineTo(PAD.l+cW,gy);ctx.stroke();}
    for(var i=1;i<=3;i++){var gx=PAD.l+(i/4)*cW;ctx.beginPath();ctx.moveTo(gx,PAD.t);ctx.lineTo(gx,PAD.t+cH);ctx.stroke();}

    ctx.fillStyle='rgba(255,255,255,0.15)'; ctx.font='7px JetBrains Mono,monospace';
    ctx.textAlign='right'; ctx.fillText('calidad',PAD.l-2,PAD.t+4);
    ctx.textAlign='right'; ctx.fillText('tokens',W-2,PAD.t+cH+14);

    drawnPts=PTS.map(function(p){return {sx:PAD.l+(p.x/100)*cW,sy:PAD.t+cH-(p.y/100)*cH,p:p};});
    drawnPts.forEach(function(dp,i){
      var isH=(hovIdx===i);
      ctx.beginPath(); ctx.arc(dp.sx,dp.sy,isH?5:3.5,0,Math.PI*2);
      ctx.fillStyle=isH?'#fff':'rgba(124,111,247,0.75)';
      ctx.fill();
      if(isH){ctx.strokeStyle='rgba(255,255,255,0.3)';ctx.lineWidth=1;ctx.stroke();}
    });
  }

  var h=wSetup('wc-scatter','ww-scatter',draw);
  if(!h||!wrap||!tt)return;
  wrap.addEventListener('mousemove',function(e){
    var best=22,bi=-1;
    drawnPts.forEach(function(dp,i){var d=Math.hypot(e.offsetX-dp.sx,e.offsetY-dp.sy);if(d<best){best=d;bi=i;}});
    hovIdx=bi;
    if(bi>=0){var p=PTS[bi];wTT(tt,wrap,e.offsetX,e.offsetY,'<span class="tt-dim">'+p.label+'</span><br><span class="tt-val">'+p.x+'k</span><span class="tt-dim"> tokens · </span><span class="tt-val">'+p.y+'</span><span class="tt-dim"> cal</span>');}
    else tt.classList.remove('show');
    h.redraw();
  });
  wrap.addEventListener('mouseleave',function(){hovIdx=-1;tt.classList.remove('show');h.redraw();});
})();

/* ---- 5. BIG STAT ---- */
(function() {
  var VALUE=124, TREND='+12', SPARK=[68,72,81,75,89,94,101,98,108,114,119,124];
  var tt=document.getElementById('wt-stat');
  var wrap=document.getElementById('ww-stat');

  function draw(ctx,W,H){
    ctx.clearRect(0,0,W,H);
    ctx.fillStyle='#fff'; ctx.font='700 34px JetBrains Mono,monospace'; ctx.textAlign='left';
    ctx.fillText(VALUE, 8, H*0.5);
    ctx.fillStyle='#4ade80'; ctx.font='700 10px JetBrains Mono,monospace';
    ctx.fillText(TREND+' hoy', 8, H*0.5+18);

    var PAD={t:H*0.65,b:6,l:6,r:6}, n=SPARK.length;
    var cW=W-PAD.l-PAD.r, cH=H-PAD.t-PAD.b;
    var mn=SPARK[0]*0.95, mx2=SPARK[SPARK.length-1]*1.02;
    var pts=SPARK.map(function(v,i){return{x:PAD.l+(i/(n-1))*cW,y:PAD.t+cH-((v-mn)/(mx2-mn))*cH};});

    ctx.beginPath(); ctx.moveTo(pts[0].x,PAD.t+cH); ctx.lineTo(pts[0].x,pts[0].y);
    for(var i=1;i<pts.length;i++){var cx=(pts[i-1].x+pts[i].x)/2;ctx.bezierCurveTo(cx,pts[i-1].y,cx,pts[i].y,pts[i].x,pts[i].y);}
    ctx.lineTo(pts[pts.length-1].x,PAD.t+cH); ctx.closePath();
    var g=ctx.createLinearGradient(0,PAD.t,0,PAD.t+cH);
    g.addColorStop(0,'rgba(74,222,128,0.2)'); g.addColorStop(1,'rgba(74,222,128,0)');
    ctx.fillStyle=g; ctx.fill();
    ctx.beginPath(); ctx.moveTo(pts[0].x,pts[0].y);
    for(var i=1;i<pts.length;i++){var cx=(pts[i-1].x+pts[i].x)/2;ctx.bezierCurveTo(cx,pts[i-1].y,cx,pts[i].y,pts[i].x,pts[i].y);}
    ctx.strokeStyle='#4ade80'; ctx.lineWidth=1.5; ctx.stroke();
  }

  var h=wSetup('wc-stat','ww-stat',draw);
  if(!h||!wrap||!tt)return;
  wrap.addEventListener('mousemove',function(e){wTT(tt,wrap,e.offsetX,e.offsetY,'<span class="tt-val">'+VALUE+'</span><span class="tt-dim"> commits este mes</span>');});
  wrap.addEventListener('mouseleave',function(){tt.classList.remove('show');});
})();

/* ---- 6. HORIZONTAL BARS ---- */
(function() {
  var ITEMS=[{label:'Claude',val:88,color:'#7c6ff7'},{label:'Python',val:72,color:'#4ade80'},{label:'Git',val:61,color:'#60a5fa'},{label:'VS Code',val:55,color:'#f59e0b'},{label:'Figma',val:38,color:'#ef4444'}];
  var hovIdx=-1;
  var tt=document.getElementById('wt-hbars');
  var wrap=document.getElementById('ww-hbars');

  function draw(ctx,W,H){
    ctx.clearRect(0,0,W,H);
    var n=ITEMS.length, rowH=H/n, PAD={l:4,r:8};
    ITEMS.forEach(function(it,i){
      var isH=(hovIdx===i);
      var y=i*rowH+rowH*0.2, h=rowH*0.6;
      var barW=(W-PAD.l-PAD.r)*(it.val/100);

      ctx.fillStyle=isH?'rgba(255,255,255,0.04)':'transparent';
      ctx.fillRect(0,i*rowH,W,rowH);

      ctx.fillStyle=isH?it.color:it.color.replace(')',',0.55)').replace('rgb','rgba').replace('#','rgba(').replace('rgba(','rgba(');
      var alpha=isH?1:0.55;
      ctx.globalAlpha=alpha;
      ctx.beginPath(); ctx.roundRect(PAD.l,y,barW,h,[0,3,3,0]); ctx.fill();
      ctx.globalAlpha=1;

      ctx.fillStyle=isH?'rgba(255,255,255,0.8)':'rgba(255,255,255,0.28)';
      ctx.font=(isH?'600 ':'')+'8px JetBrains Mono,monospace'; ctx.textAlign='left';
      ctx.fillText(it.label, PAD.l+4, y+h*0.72);
    });
  }

  var h=wSetup('wc-hbars','ww-hbars',draw);
  if(!h||!wrap||!tt)return;
  wrap.addEventListener('mousemove',function(e){
    var n=ITEMS.length, rowH=wrap.clientHeight/n;
    var idx=Math.floor(e.offsetY/rowH); idx=Math.max(0,Math.min(n-1,idx));
    hovIdx=idx;
    var it=ITEMS[idx];
    wTT(tt,wrap,e.offsetX,e.offsetY,'<span class="tt-dim">'+it.label+'</span> <span class="tt-val">'+it.val+'%</span>');
    h.redraw();
  });
  wrap.addEventListener('mouseleave',function(){hovIdx=-1;tt.classList.remove('show');h.redraw();});
})();

/* ---- 7. RING (single) ---- */
(function() {
  var PCT=0.82, CURR=164, TOTAL=200;
  var tt=document.getElementById('wt-ring');
  var wrap=document.getElementById('ww-ring');

  function draw(ctx,W,H){
    ctx.clearRect(0,0,W,H);
    var cx=W/2, cy=H/2, r=Math.min(W,H)*0.36, thick=12;
    var START=-Math.PI/2;

    ctx.beginPath(); ctx.arc(cx,cy,r,0,Math.PI*2);
    ctx.strokeStyle='rgba(255,255,255,0.06)'; ctx.lineWidth=thick; ctx.stroke();

    ctx.beginPath(); ctx.arc(cx,cy,r,START,START+PCT*Math.PI*2);
    ctx.strokeStyle='#7c6ff7'; ctx.lineWidth=thick; ctx.lineCap='round'; ctx.stroke();

    ctx.fillStyle='#fff'; ctx.font='700 26px JetBrains Mono,monospace'; ctx.textAlign='center';
    ctx.fillText(Math.round(PCT*100)+'%', cx, cy+9);
    ctx.fillStyle='rgba(255,255,255,0.28)'; ctx.font='7px JetBrains Mono,monospace';
    ctx.fillText(CURR+'k / '+TOTAL+'k tokens', cx, cy+24);
  }

  var h=wSetup('wc-ring','ww-ring',draw);
  if(!h||!wrap||!tt)return;
  wrap.addEventListener('mousemove',function(e){wTT(tt,wrap,e.offsetX,e.offsetY,'<span class="tt-val">'+Math.round(PCT*100)+'%</span> <span class="tt-dim">contexto</span><br><span class="tt-dim">'+CURR+'k / '+TOTAL+'k tokens</span>');});
  wrap.addEventListener('mouseleave',function(){tt.classList.remove('show');});
})();

/* ---- 8. EQ BARS ---- */
(function() {
  var DATA=[1,3,2,5,4,7,6,8,5,9,6,4,7,3,5,2];
  var hovIdx=-1;
  var tt=document.getElementById('wt-eq');
  var wrap=document.getElementById('ww-eq');

  function barColor(v){if(v<=4)return'#4ade80';if(v<=7)return'#f59e0b';return'#ef4444';}

  function draw(ctx,W,H){
    ctx.clearRect(0,0,W,H);
    var n=DATA.length, PAD={t:12,b:20,l:6,r:6};
    var cW=W-PAD.l-PAD.r, cH=H-PAD.t-PAD.b;
    var bW=cW/n*0.6, gap=cW/n;

    DATA.forEach(function(v,i){
      var isH=(hovIdx===i);
      var bh=(v/9)*cH, x=PAD.l+i*gap+(gap-bW)/2, y=PAD.t+cH-bh;
      ctx.globalAlpha=isH?1:(hovIdx===-1?0.72:0.28);
      ctx.fillStyle=barColor(v);
      ctx.beginPath(); ctx.roundRect(x,y,bW,bh,[2,2,0,0]); ctx.fill();
      ctx.globalAlpha=1;
      if(i%4===0){ctx.fillStyle='rgba(255,255,255,0.18)';ctx.font='7px JetBrains Mono,monospace';ctx.textAlign='center';ctx.fillText(i+'h',x+bW/2,H-4);}
    });
  }

  var h=wSetup('wc-eq','ww-eq',draw);
  if(!h||!wrap||!tt)return;
  wrap.addEventListener('mousemove',function(e){
    var n=DATA.length, PAD={l:6,r:6}, gap=(wrap.clientWidth-PAD.l-PAD.r)/n;
    var idx=Math.floor((e.offsetX-PAD.l)/gap); idx=Math.max(0,Math.min(n-1,idx));
    hovIdx=idx;
    wTT(tt,wrap,e.offsetX,e.offsetY,'<span class="tt-dim">'+idx+'h</span> <span class="tt-val">'+DATA[idx]+'</span><span class="tt-dim"> errores</span>');
    h.redraw();
  });
  wrap.addEventListener('mouseleave',function(){hovIdx=-1;tt.classList.remove('show');h.redraw();});
})();
</script>
