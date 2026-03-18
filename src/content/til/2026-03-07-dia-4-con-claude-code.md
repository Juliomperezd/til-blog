---
title: "Día 4 con Claude Code"
date: 2026-03-07
tags: ["Claude Code", "Canvas", "Retro UI"]
---

Día 4. La primera versión tenía la paleta equivocada.

El Evangelion real no es verde terminal. Es naranja sobre negro para las alertas. Teal puro para el MAGI — que además es un flowchart literal de cajas conectadas con líneas, no un radar. Magenta para el análisis de frecuencias. Y la pantalla de sincronía neuronal son columnas EEG verticales con una línea roja que avanza.

Las referencias importan. Siete representaciones. Esta vez con los originales delante.

## MAGI::DECISION

El MAGI vota y comunica el resultado en una sola palabra. APPROVED o REFUSED. Nada más necesario.

<div class="ev2-pg ev2-alert" id="pg-decision">
  <div class="ev2-c tl"></div><div class="ev2-c tr"></div><div class="ev2-c bl"></div><div class="ev2-c br"></div>
  <div class="ev2-hdr"><span class="ev2-lbl">MAGI::DECISION — COMMAND RELAY</span><span class="ev2-st ev2-blink">■ PROCESSING</span></div>
  <div class="ev2-area" id="area-decision"><canvas id="c-decision"></canvas></div>
</div>

## NEURAL::WAVEFORM

Cinco regiones cerebrales. Actividad en tiempo real. La línea roja marca el presente.

<div class="ev2-pg ev2-cyan" id="pg-neural">
  <div class="ev2-c tl"></div><div class="ev2-c tr"></div><div class="ev2-c bl"></div><div class="ev2-c br"></div>
  <div class="ev2-hdr"><span class="ev2-lbl">NEURAL::WAVEFORM — SYNC MONITOR</span><span class="ev2-st" style="color:#00e5ff">■ RECORDING</span></div>
  <div class="ev2-area" id="area-neural"><canvas id="c-neural"></canvas></div>
</div>

## AT::FIELD

Análisis de campo AT. Líneas de flujo entre el polo generador y el polo sumidero. El anillo interior muestra el reactor toroidal activo.

<div class="ev2-pg ev2-teal" id="pg-atf">
  <div class="ev2-c tl"></div><div class="ev2-c tr"></div><div class="ev2-c bl"></div><div class="ev2-c br"></div>
  <div class="ev2-hdr"><span class="ev2-lbl">AT::FIELD — DIPOLE ANALYSIS</span><span class="ev2-st" style="color:#00ff99">■ EXTENDED</span></div>
  <div class="ev2-area" id="area-atf"><canvas id="c-atf"></canvas><div class="ev2-tt" id="tt-atf"></div></div>
</div>

## WAVE::ANALYZER

Análisis de frecuencia de la señal de sincronía. Múltiples armónicos superpuestos. Las ondas se desplazan en fase.

<div class="ev2-pg ev2-pink" id="pg-wave">
  <div class="ev2-c tl"></div><div class="ev2-c tr"></div><div class="ev2-c bl"></div><div class="ev2-c br"></div>
  <div class="ev2-hdr"><span class="ev2-lbl">WAVE::ANALYZER — FREQUENCY SPECTRUM</span><span class="ev2-st" style="color:#ff3399">■ ACTIVE</span></div>
  <div class="ev2-area" id="area-wave"><canvas id="c-wave"></canvas></div>
</div>

## MAGI::CIRCUIT

El MAGI por dentro. Tres sistemas, un flujo. Los paquetes de datos se mueven por las conexiones en tiempo real.

<div class="ev2-pg ev2-teal" id="pg-circuit">
  <div class="ev2-c tl"></div><div class="ev2-c tr"></div><div class="ev2-c bl"></div><div class="ev2-c br"></div>
  <div class="ev2-hdr"><span class="ev2-lbl">MAGI::CIRCUIT — LOGIC FLOW</span><span class="ev2-st" style="color:#00ff99">■ NOMINAL</span></div>
  <div class="ev2-area" id="area-circuit"><canvas id="c-circuit"></canvas></div>
</div>

## THERMAL::SCAN

Escáner de patrón. Distribución de energía en cuadrícula. Zona caliente detectada en sector norte.

<div class="ev2-pg ev2-alert" id="pg-thermal">
  <div class="ev2-c tl"></div><div class="ev2-c tr"></div><div class="ev2-c bl"></div><div class="ev2-c br"></div>
  <div class="ev2-hdr"><span class="ev2-lbl">THERMAL::SCAN — PATTERN ANALYSIS</span><span class="ev2-st ev2-blink" style="color:#ff4400">■ ANOMALY DETECTED</span></div>
  <div class="ev2-area" id="area-thermal"><canvas id="c-thermal"></canvas></div>
</div>

## TACTICAL::OVERLAY

Vista táctica de Tokyo-3. Posiciones de unidades Eva y contactos confirmados.

<div class="ev2-pg ev2-teal" id="pg-tactical">
  <div class="ev2-c tl"></div><div class="ev2-c tr"></div><div class="ev2-c bl"></div><div class="ev2-c br"></div>
  <div class="ev2-hdr"><span class="ev2-lbl">TACTICAL::OVERLAY — TOKYO-3 GRID</span><span class="ev2-st ev2-blink" style="color:#ff4400">■ HOSTILE CONTACT</span></div>
  <div class="ev2-area" id="area-tactical"><canvas id="c-tactical"></canvas><div class="ev2-tt" id="tt-tactical"></div></div>
</div>

<style>
/* ===== BASE CONTAINER ===== */
.ev2-pg {
  background: #000;
  margin: 2rem 0 2.5rem;
  font-family: 'JetBrains Mono', monospace;
  position: relative;
  overflow: hidden;
}
.ev2-pg::after {
  content: '';
  position: absolute;
  inset: 0;
  background: repeating-linear-gradient(0deg, transparent, transparent 3px, rgba(0,0,0,0.18) 3px, rgba(0,0,0,0.18) 4px);
  pointer-events: none;
  z-index: 5;
}
/* color variants */
.ev2-alert  { border: 1px solid rgba(255,102,0,0.45); }
.ev2-teal   { border: 1px solid rgba(0,255,153,0.35); }
.ev2-pink   { border: 1px solid rgba(255,51,153,0.4); }
.ev2-cyan   { border: 1px solid rgba(0,229,255,0.4); }
/* corner brackets */
.ev2-c { position: absolute; width: 12px; height: 12px; z-index: 6; }
.ev2-c.tl { top: 0; left: 0;   border-top: 2px solid; border-left:  2px solid; }
.ev2-c.tr { top: 0; right: 0;  border-top: 2px solid; border-right: 2px solid; }
.ev2-c.bl { bottom: 0; left: 0;  border-bottom: 2px solid; border-left:  2px solid; }
.ev2-c.br { bottom: 0; right: 0; border-bottom: 2px solid; border-right: 2px solid; }
.ev2-alert .ev2-c { border-color: #ff6600; }
.ev2-teal  .ev2-c { border-color: #00ff99; }
.ev2-pink  .ev2-c { border-color: #ff3399; }
.ev2-cyan  .ev2-c { border-color: #00e5ff; }
/* header */
.ev2-hdr {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 9px 14px 8px;
  border-bottom: 1px solid;
  font-size: 0.49rem;
  letter-spacing: 0.13em;
  text-transform: uppercase;
}
.ev2-alert .ev2-hdr { border-color: rgba(255,102,0,0.2);  color: #ff6600; }
.ev2-teal  .ev2-hdr { border-color: rgba(0,255,153,0.15); color: #00ff99; }
.ev2-pink  .ev2-hdr { border-color: rgba(255,51,153,0.18);color: #ff3399; }
.ev2-cyan  .ev2-hdr { border-color: rgba(0,229,255,0.18);  color: #00e5ff; }
.ev2-lbl { opacity: 0.9; }
.ev2-st  { opacity: 0.65; }
@keyframes ev2-blink { 0%,100%{opacity:1} 50%{opacity:0.1} }
.ev2-blink { animation: ev2-blink 1s step-end infinite; }
/* canvas area */
.ev2-area { height: 260px; position: relative; }
.ev2-area canvas { position: absolute; top: 0; left: 0; }
/* tooltip */
.ev2-tt {
  position: absolute;
  pointer-events: none;
  background: rgba(0,0,0,0.95);
  border: 1px solid rgba(255,102,0,0.4);
  padding: 8px 12px;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.5625rem;
  color: #ff6600;
  white-space: nowrap;
  opacity: 0;
  transition: opacity 0.1s;
  z-index: 10;
  line-height: 1.8;
  text-transform: uppercase;
  letter-spacing: 0.08em;
}
.ev2-tt.show { opacity: 1; }
</style>

<script>
/* ===== SHARED HELPERS ===== */
function ev2Setup(canvasId, areaId) {
  var canvas = document.getElementById(canvasId);
  var area   = document.getElementById(areaId);
  if (!canvas || !area) return null;
  var ctx = canvas.getContext('2d');
  var _cb = null;
  function dpr() { return window.devicePixelRatio || 1; }
  function resize() {
    var d = dpr(), W = area.clientWidth, H = area.clientHeight;
    canvas.width = W*d; canvas.height = H*d;
    canvas.style.width = W+'px'; canvas.style.height = H+'px';
    ctx.setTransform(d, 0, 0, d, 0, 0);
    if (_cb) requestAnimationFrame(_cb);
  }
  resize();
  if (typeof ResizeObserver !== 'undefined') new ResizeObserver(resize).observe(area);
  return {
    canvas: canvas, ctx: ctx, area: area,
    W: function(){ return canvas.width/(window.devicePixelRatio||1); },
    H: function(){ return canvas.height/(window.devicePixelRatio||1); },
    dpr: dpr, onResize: function(fn){ _cb = fn; }
  };
}
function ev2TT(tt, area, mx, my) {
  var aW = area.clientWidth, aH = area.clientHeight;
  var tW = 180, tH = 80;
  var x = mx+14, y = my-16;
  if (x+tW > aW-8) x = mx-tW-10;
  if (y+tH > aH-8) y = aH-tH-8;
  if (y < 8) y = 8;
  tt.style.left = x+'px'; tt.style.top = y+'px';
}
function noise1(t) {
  /* simple deterministic noise via sin sum */
  return Math.sin(t*1.0)*0.5 + Math.sin(t*2.3+1.1)*0.3 + Math.sin(t*5.7+2.3)*0.15 + Math.sin(t*11.3+0.7)*0.05;
}

/* ===== 1. MAGI::DECISION ===== */
(function(){
  var r = ev2Setup('c-decision','area-decision');
  if (!r) return;
  var ctx = r.ctx, canvas = r.canvas;

  var COMMANDS = [
    { lines: ['EVA-01 ENTRY PLUG','EJECT COMMAND'],
      from: 'BALTHASAR DIRECT CONNECTION NO.102',
      to:   'EVA-01 ENTRY PLUG SYSTEM LINK 2',
      verdict: 'REFUSED', vc: '#cc0000' },
    { lines: ['EVA-01 UNIT ACTIVATION','COMMAND'],
      from: 'MELCHIOR DIRECT LINK 047',
      to:   'EVA-01 POWER SYSTEM ALPHA',
      verdict: 'APPROVED', vc: '#ff6600' },
    { lines: ['AT-FIELD','NEUTRALIZATION ORDER'],
      from: 'CASPER DIRECT LINK 201',
      to:   'EVA-01 INTERFACE SYSTEM 3',
      verdict: 'APPROVED', vc: '#ff6600' },
    { lines: ['PILOT EJECTION','EMERGENCY PROTOCOL'],
      from: 'BALTHASAR DIRECT CONNECTION NO.117',
      to:   'EVA-01 LIFE SUPPORT LINK 1',
      verdict: 'REFUSED', vc: '#cc0000' },
  ];
  var cidx = 0, stateStart = 0, STATE_DUR = 3200, FADE = 350;

  function draw(ts) {
    requestAnimationFrame(draw);
    if (!stateStart) stateStart = ts;
    var age = ts - stateStart;
    if (age > STATE_DUR) { cidx = (cidx+1) % COMMANDS.length; stateStart = ts; age = 0; }
    var alpha = Math.min(age/FADE, 1) * (age > STATE_DUR-FADE ? 1-(age-(STATE_DUR-FADE))/FADE : 1);

    var W = r.W(), H = r.H();
    ctx.clearRect(0,0,W,H);
    ctx.fillStyle = '#000'; ctx.fillRect(0,0,W,H);

    var cmd = COMMANDS[cidx];
    ctx.globalAlpha = Math.max(0.01, alpha);

    /* small header lines */
    ctx.fillStyle = '#ff6600';
    ctx.font = 'bold 9px JetBrains Mono, monospace';
    ctx.textAlign = 'center';
    cmd.lines.forEach(function(l, li) {
      ctx.fillText(l, W/2, H*0.18 + li*14);
    });

    /* from / to lines */
    ctx.fillStyle = 'rgba(255,102,0,0.55)';
    ctx.font = '7px JetBrains Mono, monospace';
    ctx.fillText('from: ' + cmd.from, W/2, H*0.18 + cmd.lines.length*14 + 12);
    ctx.fillText('to: ' + cmd.to,     W/2, H*0.18 + cmd.lines.length*14 + 22);

    /* separator line */
    ctx.strokeStyle = '#ff2200';
    ctx.lineWidth = 1.5;
    ctx.beginPath(); ctx.moveTo(W*0.06, H*0.44); ctx.lineTo(W*0.94, H*0.44); ctx.stroke();

    /* big verdict */
    var verdict = cmd.verdict;
    ctx.fillStyle = cmd.vc;
    ctx.textAlign = 'center';
    /* measure and scale to fit */
    ctx.font = 'bold 100px JetBrains Mono, monospace';
    var mW = ctx.measureText(verdict).width;
    var fs = Math.min(100 * (W * 0.82 / mW), H * 0.44);
    ctx.font = 'bold ' + fs + 'px JetBrains Mono, monospace';
    ctx.shadowColor = cmd.vc; ctx.shadowBlur = fs * 0.08;
    ctx.fillText(verdict, W/2, H*0.44 + fs*0.78);
    ctx.shadowBlur = 0;

    /* border box around verdict */
    ctx.strokeStyle = cmd.vc + '55';
    ctx.lineWidth = 1;
    var bpad = 8;
    var bx = W*0.04, bw = W*0.92;
    var by = H*0.46, bh = H*0.50;
    ctx.strokeRect(bx, by, bw, bh);
    /* box corners bright */
    ctx.strokeStyle = cmd.vc;
    ctx.lineWidth = 2;
    var clen = 14;
    [[bx,by],[bx+bw,by],[bx,by+bh],[bx+bw,by+bh]].forEach(function(c,ci) {
      var sx = ci%2===0?1:-1, sy = ci<2?1:-1;
      ctx.beginPath();
      ctx.moveTo(c[0],c[1]); ctx.lineTo(c[0]+sx*clen,c[1]);
      ctx.moveTo(c[0],c[1]); ctx.lineTo(c[0],c[1]+sy*clen);
      ctx.stroke();
    });

    ctx.globalAlpha = 1;
  }
  requestAnimationFrame(draw);
})();

/* ===== 2. NEURAL::WAVEFORM ===== */
(function(){
  var r = ev2Setup('c-neural','area-neural');
  if (!r) return;
  var ctx = r.ctx, canvas = r.canvas;

  var CHANNELS = [
    { label:'AMYGDALA',      num:'-01', freq:3.1, seed:0.0,  color:'#a0d8ff' },
    { label:'HIPPOCAMPUS',   num:'-02', freq:1.8, seed:1.7,  color:'#80ccff' },
    { label:'PARIETAL LOBE', num:'-03', freq:0.9, seed:3.2,  color:'#c0e0ff' },
    { label:'MOTOR CORTEX',  num:'-04', freq:2.4, seed:5.1,  color:'#90d0ff' },
    { label:'SENSORY CORTEX',num:'-05', freq:4.2, seed:7.8,  color:'#b0d8ff' },
  ];
  var phase = 0;

  function sig(ch, t) {
    return noise1(t * ch.freq + ch.seed) + Math.sin(t * ch.freq * 0.3 + ch.seed) * 0.4;
  }

  function draw(ts) {
    requestAnimationFrame(draw);
    phase = (ts||0) / 500;

    var W = r.W(), H = r.H();
    ctx.clearRect(0,0,W,H);
    ctx.fillStyle = '#00080f'; ctx.fillRect(0,0,W,H);

    var SCAN_Y = H * 0.62; /* red scan line position */
    var n = CHANNELS.length;
    var PAD = { t:22, b:24, l:4, r:4 };
    var cH = H - PAD.t - PAD.b;
    var colW = (W - PAD.l - PAD.r) / n;

    /* column backgrounds */
    CHANNELS.forEach(function(ch, ci) {
      var cx0 = PAD.l + ci * colW;
      /* subtle column tint */
      ctx.fillStyle = ci%2===0 ? 'rgba(0,20,40,0.3)' : 'rgba(0,10,30,0.2)';
      ctx.fillRect(cx0, PAD.t, colW, cH);
    });

    /* column dividers */
    ctx.strokeStyle = 'rgba(0,140,200,0.2)'; ctx.lineWidth = 1;
    CHANNELS.forEach(function(ch, ci) {
      if (ci === 0) return;
      var cx0 = PAD.l + ci * colW;
      ctx.beginPath(); ctx.moveTo(cx0, PAD.t); ctx.lineTo(cx0, PAD.t+cH); ctx.stroke();
    });

    /* waveforms */
    CHANNELS.forEach(function(ch, ci) {
      var colCX = PAD.l + ci * colW + colW / 2;
      var halfW  = colW * 0.38;

      ctx.strokeStyle = ch.color;
      ctx.lineWidth = 1.2;
      ctx.beginPath();
      for (var py = 0; py < cH; py++) {
        var t = phase - py * 0.045;
        var val = sig(ch, t);
        var px = colCX + val * halfW;
        py === 0 ? ctx.moveTo(px, PAD.t + py) : ctx.lineTo(px, PAD.t + py);
      }
      ctx.stroke();

      /* label top */
      ctx.fillStyle = 'rgba(0,180,255,0.6)';
      ctx.font = '5.5px JetBrains Mono, monospace';
      ctx.textAlign = 'center';
      /* rotated label */
      ctx.save();
      ctx.translate(colCX, PAD.t - 4);
      ctx.fillText(ch.label, 0, 0);
      ctx.restore();

      /* number bottom */
      ctx.fillStyle = '#ff4400';
      ctx.font = 'bold 8px JetBrains Mono, monospace';
      ctx.fillText(ch.num, colCX, PAD.t + cH + 14);
    });

    /* red scan line */
    ctx.strokeStyle = '#ff0000';
    ctx.lineWidth = 1.5;
    ctx.setLineDash([]);
    ctx.beginPath(); ctx.moveTo(PAD.l, SCAN_Y); ctx.lineTo(PAD.l + colW*n, SCAN_Y); ctx.stroke();
    /* scan line glow */
    ctx.strokeStyle = 'rgba(255,0,0,0.2)';
    ctx.lineWidth = 4;
    ctx.beginPath(); ctx.moveTo(PAD.l, SCAN_Y); ctx.lineTo(PAD.l + colW*n, SCAN_Y); ctx.stroke();
  }
  requestAnimationFrame(draw);
})();

/* ===== 3. AT::FIELD ===== */
(function(){
  var r = ev2Setup('c-atf','area-atf');
  if (!r) return;
  var ctx = r.ctx, canvas = r.canvas, area = r.area;
  var tt = document.getElementById('tt-atf');

  /* dipole field: source + sink */
  function field(x, y, W, H) {
    var src = {x: W*0.28, y: H*0.5};
    var snk = {x: W*0.72, y: H*0.5};
    var dx1 = x-src.x, dy1 = y-src.y, r1 = dx1*dx1+dy1*dy1+60;
    var dx2 = x-snk.x, dy2 = y-snk.y, r2 = dx2*dx2+dy2*dy2+60;
    return { fx: dx1/r1 - dx2/r2, fy: dy1/r1 - dy2/r2 };
  }

  function drawField(W, H) {
    ctx.clearRect(0,0,W,H);
    ctx.fillStyle = '#050a08'; ctx.fillRect(0,0,W,H);

    var src = {x:W*0.28, y:H*0.5};
    var snk = {x:W*0.72, y:H*0.5};

    /* grid background */
    ctx.strokeStyle = 'rgba(0,180,80,0.06)'; ctx.lineWidth = 1;
    for (var gx = 0; gx < W; gx += 28) { ctx.beginPath(); ctx.moveTo(gx,0); ctx.lineTo(gx,H); ctx.stroke(); }
    for (var gy = 0; gy < H; gy += 28) { ctx.beginPath(); ctx.moveTo(0,gy); ctx.lineTo(W,gy); ctx.stroke(); }

    /* streamlines */
    var NUM_LINES = 22;
    for (var li = 0; li < NUM_LINES; li++) {
      var startAngle = li * Math.PI * 2 / NUM_LINES;
      var x = src.x + Math.cos(startAngle) * 16;
      var y = src.y + Math.sin(startAngle) * 16;

      var alpha = 0.7;
      ctx.beginPath(); ctx.moveTo(x, y);
      for (var step = 0; step < 320; step++) {
        var f = field(x, y, W, H);
        var flen = Math.sqrt(f.fx*f.fx + f.fy*f.fy) + 0.0001;
        x += f.fx/flen * 3.5;
        y += f.fy/flen * 3.5;
        if (x < 2||x > W-2||y < 2||y > H-2) break;
        /* stop near sink */
        var dsnk = Math.hypot(x-snk.x, y-snk.y);
        if (dsnk < 14) break;
        ctx.lineTo(x, y);
      }
      ctx.strokeStyle = 'rgba(0,220,100,' + alpha + ')';
      ctx.lineWidth = 1;
      ctx.stroke();
    }

    /* source — torus ring (angel AT field) */
    var ringR = Math.min(W,H) * 0.18;
    /* outer gradient ring */
    var grad = ctx.createRadialGradient(snk.x,snk.y, ringR*0.55, snk.x,snk.y, ringR*1.05);
    grad.addColorStop(0, 'rgba(180,60,0,0.8)');
    grad.addColorStop(0.4,'rgba(220,80,0,0.5)');
    grad.addColorStop(1, 'rgba(100,20,0,0)');
    ctx.beginPath(); ctx.arc(snk.x,snk.y, ringR, 0, Math.PI*2);
    ctx.fillStyle = grad; ctx.fill();
    /* ring stroke */
    ctx.beginPath(); ctx.arc(snk.x,snk.y, ringR, 0, Math.PI*2);
    ctx.strokeStyle = 'rgba(255,120,0,0.8)'; ctx.lineWidth = 2;
    ctx.shadowColor = '#ff6600'; ctx.shadowBlur = 12; ctx.stroke(); ctx.shadowBlur = 0;
    /* inner rings */
    [0.75,0.55,0.38].forEach(function(frac) {
      ctx.beginPath(); ctx.arc(snk.x,snk.y, ringR*frac, 0, Math.PI*2);
      ctx.strokeStyle = 'rgba(180,60,0,0.35)'; ctx.lineWidth = 1; ctx.stroke();
    });
    /* center void */
    ctx.beginPath(); ctx.arc(snk.x,snk.y, ringR*0.3, 0, Math.PI*2);
    ctx.fillStyle = '#020402'; ctx.fill();
    /* INNER TORUS label */
    ctx.fillStyle = 'rgba(255,120,0,0.7)';
    ctx.font = '6px JetBrains Mono, monospace'; ctx.textAlign = 'center';
    ctx.fillText('INNER TORUS REACTOR', snk.x, snk.y-4);
    ctx.fillText('ACTIVE', snk.x, snk.y+6);

    /* source pole */
    ctx.beginPath(); ctx.arc(src.x,src.y, 5, 0, Math.PI*2);
    ctx.fillStyle = '#00ff66'; ctx.fill();
    ctx.shadowColor = '#00ff66'; ctx.shadowBlur = 8; ctx.fill(); ctx.shadowBlur = 0;
    ctx.fillStyle = '#00ff66'; ctx.font = '6px JetBrains Mono, monospace'; ctx.textAlign = 'left';
    ctx.fillText('+' + (Math.random()*9999+70000|0).toString().padStart(8,'0'), src.x+10, src.y-6);
    ctx.fillText('-' + (Math.random()*9999+60000|0).toString().padStart(8,'0'), src.x+10, src.y+8);

    /* 5th ANGEL label box */
    var lbx = snk.x + ringR + 8, lby = snk.y - ringR*0.5;
    ctx.fillStyle = 'rgba(255,120,0,0.9)'; ctx.strokeStyle = 'rgba(255,120,0,0.7)'; ctx.lineWidth = 1;
    ctx.fillRect(lbx, lby, 118, 28);
    ctx.strokeRect(lbx, lby, 118, 28);
    ctx.fillStyle = '#000';
    ctx.font = 'bold 7px JetBrains Mono, monospace'; ctx.textAlign = 'left';
    ctx.fillText('5th ANGEL:', lbx+5, lby+10);
    ctx.fillText('A.T.Field; extended', lbx+5, lby+21);

    /* axis tick numbers */
    ctx.fillStyle = 'rgba(0,200,80,0.5)';
    ctx.font = '6px JetBrains Mono, monospace'; ctx.textAlign = 'left';
    for (var ti = -3; ti <= 3; ti++) {
      if (ti===0) continue;
      ctx.fillText(ti*10, PAD_X(W,ti), H-6);
      ctx.fillText(ti*10, 4, PAD_Y(H,ti));
    }
  }
  function PAD_X(W,v){ return W/2 + v/3*W*0.15; }
  function PAD_Y(H,v){ return H/2 - v/3*H*0.4; }

  r.onResize(function(){ drawField(r.W(), r.H()); });
  requestAnimationFrame(function(){ drawField(r.W(), r.H()); });
})();

/* ===== 4. WAVE::ANALYZER ===== */
(function(){
  var r = ev2Setup('c-wave','area-wave');
  if (!r) return;
  var ctx = r.ctx, canvas = r.canvas;
  var phase = 0;

  /* wave layers: 10 overlapping, slightly offset */
  var WAVES = (function(){
    var arr = [];
    for (var i = 0; i < 10; i++) {
      arr.push({
        freqX:  1.2 + i*0.18,
        freqY:  0.9 + i*0.11,
        pOff:   i * 0.28,
        amp:    0.36 - i*0.02,
        colorT: i / 9  /* 0 = hot pink, 1 = deep red */
      });
    }
    return arr;
  })();

  function waveColor(t, alpha) {
    /* t=0 -> hot pink, t=1 -> deep magenta/red */
    var r = Math.round(255);
    var g = Math.round(20  + (1-t)*40);
    var b = Math.round(180 - t*160);
    return 'rgba('+r+','+g+','+b+','+alpha+')';
  }

  function draw(ts) {
    requestAnimationFrame(draw);
    phase = (ts||0) / 900;

    var W = r.W(), H = r.H();
    ctx.clearRect(0,0,W,H);
    ctx.fillStyle = '#060008'; ctx.fillRect(0,0,W,H);

    var CY = H/2;

    /* grid + cross markers */
    var GRID = 48;
    ctx.strokeStyle = 'rgba(255,60,150,0.12)'; ctx.lineWidth = 1;
    for (var gx = 0; gx < W; gx += GRID) {
      ctx.beginPath(); ctx.moveTo(gx,0); ctx.lineTo(gx,H); ctx.stroke();
    }
    for (var gy = 0; gy < H; gy += GRID) {
      ctx.beginPath(); ctx.moveTo(0,gy); ctx.lineTo(W,gy); ctx.stroke();
    }
    /* + markers at intersections */
    ctx.fillStyle = 'rgba(255,100,180,0.35)';
    ctx.font = '8px JetBrains Mono, monospace'; ctx.textAlign = 'center';
    for (var mx = GRID; mx < W; mx += GRID) {
      for (var my = GRID; my < H; my += GRID) {
        ctx.fillText('+', mx, my+3);
      }
    }

    /* axis numbers */
    ctx.fillStyle = 'rgba(255,60,150,0.4)'; ctx.font = '6px JetBrains Mono, monospace';
    ctx.textAlign = 'left';
    [-4,-3,-2,-1,0,1,2,3,4].forEach(function(v,i){
      ctx.fillText(v, 4, CY - v * H*0.1 + 3);
    });

    /* waves — draw from back to front */
    WAVES.forEach(function(w) {
      ctx.beginPath();
      for (var px = 0; px <= W; px += 2) {
        var t = px / W * 4 * Math.PI;
        var py = CY + Math.sin(t * w.freqX + phase + w.pOff) * H * w.amp
                     * Math.cos(t * w.freqY * 0.3 + phase * 0.4 + w.pOff);
        px === 0 ? ctx.moveTo(px, py) : ctx.lineTo(px, py);
      }
      ctx.strokeStyle = waveColor(w.colorT, 0.7);
      ctx.lineWidth = 1.2;
      ctx.shadowColor = waveColor(w.colorT, 0.5);
      ctx.shadowBlur = 4;
      ctx.stroke();
    });
    ctx.shadowBlur = 0;

    /* frequency labels */
    ctx.fillStyle = 'rgba(255,60,150,0.55)';
    ctx.font = '7px JetBrains Mono, monospace'; ctx.textAlign = 'right';
    ctx.fillText('FREQ: ' + (1.2 + phase % 3).toFixed(3) + ' Hz', W-8, 14);
    ctx.fillText('PHASE: ' + (phase % (Math.PI*2)).toFixed(4), W-8, 24);
  }
  requestAnimationFrame(draw);
})();

/* ===== 5. MAGI::CIRCUIT ===== */
(function(){
  var r = ev2Setup('c-circuit','area-circuit');
  if (!r) return;
  var ctx = r.ctx, canvas = r.canvas;

  /* packet animation */
  var packets = [];
  var packetTimer = 0;

  function draw(ts) {
    requestAnimationFrame(draw);

    var W = r.W(), H = r.H();
    ctx.clearRect(0,0,W,H);
    ctx.fillStyle = '#000'; ctx.fillRect(0,0,W,H);

    /* ---- layout nodes ---- */
    /* MAIN on far left */
    var mainX = W*0.08, mainY = H*0.5;
    /* I/Osys */
    var ioX = W*0.30, ioY = H*0.5;
    /* LOGICsys */
    var lgX = W*0.52, lgY = H*0.3;
    /* CLsys */
    var clX = W*0.52, clY = H*0.5;
    /* X-prog */
    var xpX = W*0.52, xpY = H*0.72;
    /* CASPER / MELCHIOR / BALTHASAR outputs */
    var c1X = W*0.78, c1Y = H*0.22;
    var c2X = W*0.78, c2Y = H*0.5;
    var c3X = W*0.78, c3Y = H*0.76;

    var CONN = '#00ff99';
    var BOX  = '#00cc77';
    var DIM  = 'rgba(0,200,100,0.35)';

    function box(x, y, w, h, label, sublabel) {
      var bx = x-w/2, by = y-h/2;
      ctx.strokeStyle = BOX; ctx.lineWidth = 1;
      ctx.strokeRect(bx, by, w, h);
      ctx.fillStyle = 'rgba(0,40,20,0.7)';
      ctx.fillRect(bx+1, by+1, w-2, h-2);
      ctx.fillStyle = CONN;
      ctx.font = 'bold 8px JetBrains Mono, monospace'; ctx.textAlign = 'center';
      ctx.fillText(label, x, y + (sublabel ? -2 : 3));
      if (sublabel) {
        ctx.fillStyle = DIM;
        ctx.font = '6px JetBrains Mono, monospace';
        ctx.fillText(sublabel, x, y+8);
      }
    }

    function line(x1,y1, x2,y2) {
      ctx.beginPath(); ctx.moveTo(x1,y1); ctx.lineTo(x2,y2);
      ctx.strokeStyle = 'rgba(0,200,100,0.3)'; ctx.lineWidth = 1; ctx.stroke();
    }
    function arrow(x2,y2) {
      ctx.fillStyle = 'rgba(0,220,110,0.6)';
      ctx.beginPath(); ctx.moveTo(x2,y2); ctx.lineTo(x2-6,y2-4); ctx.lineTo(x2-6,y2+4); ctx.closePath(); ctx.fill();
    }

    /* MAIN — big vertical text */
    ctx.save();
    ctx.translate(mainX, mainY);
    ctx.rotate(-Math.PI/2);
    ctx.fillStyle = '#00ff99';
    ctx.font = 'bold 28px JetBrains Mono, monospace'; ctx.textAlign = 'center';
    ctx.shadowColor = '#00ff99'; ctx.shadowBlur = 10;
    ctx.fillText('MAIN', 0, 10);
    ctx.shadowBlur = 0;
    ctx.restore();

    /* connections */
    line(mainX+18, mainY, ioX-30, ioY);
    line(ioX+30, ioY, lgX-30, lgY); line(ioX+30, ioY, clX-30, clY); line(ioX+30, ioY, xpX-30, xpY);
    line(lgX+30, lgY, c1X-28, c1Y); line(clX+30, clY, c2X-28, c2Y); line(xpX+30, xpY, c3X-28, c3Y);

    /* arrowheads */
    arrow(ioX-30, ioY); arrow(lgX-30, lgY); arrow(clX-30, clY); arrow(xpX-30, xpY);
    arrow(c1X-28, c1Y); arrow(c2X-28, c2Y); arrow(c3X-28, c3Y);

    /* boxes */
    box(ioX,  ioY,  58,24, 'I/Osys',   'INPUT/OUTPUT');
    box(lgX,  lgY,  58,22, 'LOGICsys', 'REASONING');
    box(clX,  clY,  58,22, 'CLsys',    'CONTROL');
    box(xpX,  xpY,  58,22, 'X-prog',   'EXTERNAL');
    box(c1X,  c1Y,  52,20, 'CASPER',   null);
    box(c2X,  c2Y,  52,20, 'MELCHIOR', null);
    box(c3X,  c3Y,  52,20, 'BALTHASAR',null);

    /* animated data packets */
    if (ts - packetTimer > 320) {
      packetTimer = ts;
      var ROUTES = [
        [{x:mainX+18,y:mainY},{x:ioX-30,y:ioY}],
        [{x:ioX+30,y:ioY},{x:lgX-30,y:lgY}],
        [{x:ioX+30,y:ioY},{x:clX-30,y:clY}],
        [{x:ioX+30,y:ioY},{x:xpX-30,y:xpY}],
        [{x:lgX+30,y:lgY},{x:c1X-28,y:c1Y}],
        [{x:clX+30,y:clY},{x:c2X-28,y:c2Y}],
        [{x:xpX+30,y:xpY},{x:c3X-28,y:c3Y}],
      ];
      var route = ROUTES[Math.floor(Math.random()*ROUTES.length)];
      packets.push({x:route[0].x, y:route[0].y, tx:route[1].x, ty:route[1].y, t:0, speed:0.05+Math.random()*0.04});
    }
    packets = packets.filter(function(p){ return p.t < 1; });
    packets.forEach(function(p) {
      p.t = Math.min(p.t + p.speed, 1);
      var px = p.x + (p.tx-p.x)*p.t;
      var py = p.y + (p.ty-p.y)*p.t;
      ctx.beginPath(); ctx.arc(px, py, 3, 0, Math.PI*2);
      ctx.fillStyle = '#00ff99'; ctx.shadowColor = '#00ff99'; ctx.shadowBlur = 8; ctx.fill(); ctx.shadowBlur = 0;
    });

    /* status footer */
    ctx.fillStyle = 'rgba(0,200,100,0.3)';
    ctx.font = '6px JetBrains Mono, monospace'; ctx.textAlign = 'left';
    ctx.fillText('MAGI SYSTEM v14.0 // CASPER+MELCHIOR+BALTHASAR // STATUS: NOMINAL', 8, H-8);
  }
  requestAnimationFrame(draw);
})();

/* ===== 6. THERMAL::SCAN ===== */
(function(){
  var r = ev2Setup('c-thermal','area-thermal');
  if (!r) return;
  var ctx = r.ctx, canvas = r.canvas;

  /* pre-generate dot field */
  var DOTS = (function(){
    var arr = [];
    /* hotspot cluster 1 — top area */
    for (var i = 0; i < 80; i++) {
      var cx = 0.38 + (Math.sin(i*2.3)*0.5+0.5)*0.22;
      var cy = 0.22 + (Math.cos(i*1.7)*0.5+0.5)*0.18;
      arr.push({ x:cx, y:cy, heat: 0.6+Math.sin(i*0.9)*0.4, r:2+Math.sin(i*1.3)*1.5 });
    }
    /* scattered background */
    for (var j = 0; j < 140; j++) {
      arr.push({ x: Math.abs(Math.sin(j*137.5)*1)%1, y: Math.abs(Math.cos(j*97.3)*1)%1,
                 heat: 0.1+Math.abs(Math.sin(j*0.71))*0.35, r:1+Math.sin(j*2.1)*1 });
    }
    return arr;
  })();

  var scanLine = 0;

  function heatColor(h) {
    if (h > 0.75) return 'rgba(255,'+(80+h*40|0)+',0,' + (0.6+h*0.4) + ')';
    if (h > 0.45) return 'rgba(255,'+(30+h*60|0)+',0,' + (0.4+h*0.4) + ')';
    return 'rgba('+(150+h*80|0)+',30,0,'+(0.2+h*0.4)+')';
  }

  function draw(ts) {
    requestAnimationFrame(draw);
    scanLine = ((ts||0) / 4000) % 1;

    var W = r.W(), H = r.H();
    ctx.clearRect(0,0,W,H);
    ctx.fillStyle = '#020505'; ctx.fillRect(0,0,W,H);

    /* grid */
    ctx.strokeStyle = 'rgba(0,160,80,0.12)'; ctx.lineWidth = 1;
    var GRID = 32;
    for (var gx = 0; gx < W; gx += GRID) { ctx.beginPath(); ctx.moveTo(gx,0); ctx.lineTo(gx,H); ctx.stroke(); }
    for (var gy = 0; gy < H; gy += GRID) { ctx.beginPath(); ctx.moveTo(0,gy); ctx.lineTo(W,gy); ctx.stroke(); }

    /* dots */
    DOTS.forEach(function(d) {
      var px = d.x * W, py = d.y * H;
      /* only show dots that scan line has passed */
      var scanY = scanLine * H;
      var visible = py < scanY;
      if (!visible) return;
      var fadeAlpha = Math.min((scanY - py) / (H*0.25), 1);
      ctx.beginPath(); ctx.arc(px, py, d.r * (1 + d.heat*0.5), 0, Math.PI*2);
      ctx.fillStyle = heatColor(d.heat);
      ctx.globalAlpha = fadeAlpha;
      ctx.fill();
      ctx.globalAlpha = 1;
    });

    /* scan line */
    var sy = scanLine * H;
    ctx.strokeStyle = 'rgba(0,255,100,0.7)'; ctx.lineWidth = 1.5;
    ctx.beginPath(); ctx.moveTo(0, sy); ctx.lineTo(W, sy); ctx.stroke();
    ctx.strokeStyle = 'rgba(0,255,100,0.15)'; ctx.lineWidth = 8;
    ctx.beginPath(); ctx.moveTo(0, sy); ctx.lineTo(W, sy); ctx.stroke();

    /* corner labels */
    ctx.fillStyle = 'rgba(255,100,0,0.8)';
    ctx.font = 'bold 7px JetBrains Mono, monospace'; ctx.textAlign = 'left';
    ctx.fillText('シグマユニット D-17', 10, 18);
    ctx.fillText('第87ランパ量', 10, 29);
    ctx.fillStyle = 'rgba(0,200,80,0.6)';
    ctx.fillText('SCANNER: No.8768', 10, 40);

    ctx.textAlign = 'right';
    ctx.fillStyle = 'rgba(255,100,0,0.7)';
    ctx.fillText('◄ プリブラウクラス', W-8, H-22);
    ctx.fillText('主大量現象 ►', W-8, H-12);

    /* hotspot marker */
    var hx = W*0.49, hy = H*0.31;
    if (scanLine * H > hy) {
      ctx.strokeStyle = 'rgba(255,160,0,0.8)'; ctx.lineWidth = 1.5;
      var ms = 12;
      ctx.beginPath();
      ctx.moveTo(hx-ms,hy); ctx.lineTo(hx+ms,hy);
      ctx.moveTo(hx,hy-ms); ctx.lineTo(hx,hy+ms);
      ctx.stroke();
      ctx.strokeRect(hx-ms*1.5, hy-ms*1.5, ms*3, ms*3);
    }
  }
  requestAnimationFrame(draw);
})();

/* ===== 7. TACTICAL::OVERLAY ===== */
(function(){
  var r = ev2Setup('c-tactical','area-tactical');
  if (!r) return;
  var ctx = r.ctx, canvas = r.canvas, area = r.area;
  var tt = document.getElementById('tt-tactical');

  var UNITS = [
    { id:'EVA-01', x:0.50, y:0.52, color:'#7700ff', friendly:true  },
    { id:'EVA-02', x:0.44, y:0.60, color:'#ff2200', friendly:true  },
    { id:'EVA-00', x:0.57, y:0.58, color:'#00aaff', friendly:true  },
  ];
  var ANGELS = [
    { id:'6th ANGEL', x:0.50, y:0.25, color:'#ff6600', size:1.0 },
  ];
  var hovEl = null;
  var pulseT = 0;

  /* pre-generated city grid lines */
  var CITY = (function(){
    var lines = [];
    /* horizontal streets */
    var hs = [0.18,0.28,0.38,0.45,0.52,0.60,0.68,0.76,0.84];
    var vs = [0.12,0.22,0.32,0.44,0.56,0.67,0.78,0.88];
    hs.forEach(function(y){ lines.push({x1:0.05,y1:y,x2:0.95,y2:y,w:0.5+Math.random()*1.5}); });
    vs.forEach(function(x){ lines.push({x1:x,y1:0.05,x2:x,y2:0.95,w:0.5+Math.random()*1.5}); });
    return lines;
  })();

  function draw(ts) {
    requestAnimationFrame(draw);
    pulseT = (ts||0)/1000;

    var W = r.W(), H = r.H();
    ctx.clearRect(0,0,W,H);
    ctx.fillStyle = '#000d0a'; ctx.fillRect(0,0,W,H);

    /* city streets */
    CITY.forEach(function(l) {
      ctx.beginPath();
      ctx.moveTo(l.x1*W, l.y1*H); ctx.lineTo(l.x2*W, l.y2*H);
      ctx.strokeStyle = 'rgba(0,180,80,0.18)'; ctx.lineWidth = l.w; ctx.stroke();
    });

    /* grid overlay */
    var GRID = 40;
    ctx.strokeStyle = 'rgba(0,220,100,0.07)'; ctx.lineWidth = 1;
    for (var gx = 0; gx < W; gx += GRID) { ctx.beginPath(); ctx.moveTo(gx,0); ctx.lineTo(gx,H); ctx.stroke(); }
    for (var gy = 0; gy < H; gy += GRID) { ctx.beginPath(); ctx.moveTo(0,gy); ctx.lineTo(W,gy); ctx.stroke(); }

    /* crosshair markers at grid intersections */
    ctx.fillStyle = 'rgba(0,200,80,0.2)';
    ctx.font = '6px JetBrains Mono, monospace'; ctx.textAlign = 'center';
    for (var ix = GRID; ix < W-GRID; ix += GRID) {
      for (var iy = GRID; iy < H-GRID; iy += GRID) {
        ctx.fillText('+', ix, iy+2);
      }
    }

    /* coordinate labels */
    ctx.fillStyle = 'rgba(0,200,80,0.3)'; ctx.font = '6px JetBrains Mono, monospace';
    for (var ci = 0; ci*GRID < W; ci++) {
      if (ci===0) continue;
      ctx.textAlign = 'center';
      ctx.fillText(ci, ci*GRID, H-5);
      ctx.textAlign = 'right';
      ctx.fillText(ci, 16, ci*GRID+3);
    }

    /* angel pulse rings */
    ANGELS.forEach(function(a) {
      var ax = a.x*W, ay = a.y*H;
      var pulse = (Math.sin(pulseT*2)+1)/2;
      [1.8,2.8,4.0].forEach(function(mul) {
        ctx.beginPath(); ctx.arc(ax, ay, (16+a.size*12)*mul*(1+pulse*0.15), 0, Math.PI*2);
        ctx.strokeStyle = 'rgba(255,100,0,' + (0.12-mul*0.02) + ')'; ctx.lineWidth = 1; ctx.stroke();
      });
      /* angel marker: diamond */
      ctx.beginPath();
      var s = 10+a.size*6;
      ctx.moveTo(ax,ay-s); ctx.lineTo(ax+s,ay); ctx.lineTo(ax,ay+s); ctx.lineTo(ax-s,ay); ctx.closePath();
      ctx.fillStyle = 'rgba(255,80,0,0.15)'; ctx.fill();
      ctx.strokeStyle = '#ff6600'; ctx.lineWidth = 1.5;
      ctx.shadowColor = '#ff6600'; ctx.shadowBlur = 12; ctx.stroke(); ctx.shadowBlur = 0;
      /* crosshair */
      ctx.strokeStyle = 'rgba(255,100,0,0.5)'; ctx.lineWidth = 1;
      ctx.beginPath();
      ctx.moveTo(ax-30,ay); ctx.lineTo(ax-s-2,ay);
      ctx.moveTo(ax+s+2,ay); ctx.lineTo(ax+30,ay);
      ctx.moveTo(ax,ay-30); ctx.lineTo(ax,ay-s-2);
      ctx.moveTo(ax,ay+s+2); ctx.lineTo(ax,ay+30);
      ctx.stroke();
      ctx.fillStyle = '#ff6600'; ctx.font = '6.5px JetBrains Mono, monospace'; ctx.textAlign = 'left';
      ctx.fillText(a.id, ax+s+4, ay-4);
    });

    /* Eva units */
    UNITS.forEach(function(u) {
      var ux = u.x*W, uy = u.y*H;
      /* friendly marker: + cross with box */
      var s = 8;
      ctx.strokeStyle = u.color; ctx.lineWidth = 1.5;
      ctx.shadowColor = u.color; ctx.shadowBlur = 8;
      ctx.beginPath();
      ctx.moveTo(ux-s,uy); ctx.lineTo(ux+s,uy);
      ctx.moveTo(ux,uy-s); ctx.lineTo(ux,uy+s);
      ctx.stroke();
      ctx.strokeRect(ux-s*0.6, uy-s*0.6, s*1.2, s*1.2);
      ctx.shadowBlur = 0;
      ctx.fillStyle = u.color; ctx.font = '6.5px JetBrains Mono, monospace'; ctx.textAlign = 'left';
      ctx.fillText(u.id, ux+s+4, uy+3);
    });

    /* status box top-right */
    var bx = W-130, by = 10, bw = 120, bh = 66;
    ctx.fillStyle = 'rgba(0,30,15,0.85)'; ctx.fillRect(bx,by,bw,bh);
    ctx.strokeStyle = 'rgba(255,100,0,0.6)'; ctx.lineWidth = 1; ctx.strokeRect(bx,by,bw,bh);
    ctx.fillStyle = '#ff6600'; ctx.font = 'bold 6.5px JetBrains Mono, monospace'; ctx.textAlign = 'left';
    ctx.fillText('SIGMA UNIT D-15', bx+5, by+12);
    ctx.fillText('SIGMA UNIT D-17', bx+5, by+22);
    ctx.fillText('SIGMA UNIT D-18', bx+5, by+32);
    ctx.strokeStyle = 'rgba(255,80,0,0.5)'; ctx.lineWidth = 1;
    ctx.strokeRect(bx+5, by+36, bw-10, 16);
    ctx.fillStyle = '#ff6600'; ctx.font = 'bold 7px JetBrains Mono, monospace'; ctx.textAlign = 'center';
    ctx.fillText('PRIBNOW BOX', bx+bw/2, by+47);
    ctx.fillStyle = 'rgba(255,80,0,0.7)'; ctx.font = '5.5px JetBrains Mono, monospace';
    ctx.fillText('OBJECT 1      OBJECT 2', bx+bw/2, by+56);

    /* POLLUTED AREA / ALERT box bottom right */
    var ax2 = W-90, ay2 = H-38, aw = 82, ah = 30;
    ctx.fillStyle = 'rgba(150,30,0,0.8)'; ctx.fillRect(ax2,ay2,aw,ah);
    ctx.strokeStyle = '#ff4400'; ctx.lineWidth = 1; ctx.strokeRect(ax2,ay2,aw,ah);
    ctx.fillStyle = '#ff4400'; ctx.font = 'bold 6px JetBrains Mono, monospace'; ctx.textAlign = 'center';
    ctx.fillText('POLLUTED AREA', ax2+aw/2, ay2+12);
    ctx.font = 'bold 8px JetBrains Mono, monospace';
    ctx.fillText('ALERT', ax2+aw/2, ay2+24);

    /* top-left title */
    ctx.fillStyle = 'rgba(0,220,100,0.55)'; ctx.font = '6px JetBrains Mono, monospace'; ctx.textAlign = 'left';
    ctx.fillText('OPERATIONSTERRAIN', 8, 14);
    ctx.fillText('TOKYO-3 / GEOFRONT', 8, 24);
  }

  requestAnimationFrame(draw);
})();
</script>
