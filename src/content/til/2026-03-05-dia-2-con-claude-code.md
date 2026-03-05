---
title: "Día 2 con Claude Code"
date: 2026-03-05
tags: ["Claude Code"]
---

Ayer monté el blog. Hoy quería ver hasta dónde podía estirar esto.

Le pregunté a Claude si podía meter algo interactivo dentro de una entrada — no un link ni una imagen, sino algo que respondiera al ratón. Me dijo que sí: en Astro dentro de un `.md` puedes escribir HTML, CSS y JavaScript directo, y funciona.

Así que empecé a pedirle cosas. Cada caja de abajo es un efecto diferente que le describí a Claude y que él construyó.

## Sacré-Cœur

Quería que al pasar el ratón cayeran fotos polaroid. Primera prueba de que esto funcionaba.

<div id="pg-polaroid" class="dark-playground">
  <span class="pg-hint">// hover</span>
</div>

## Partículas de oro

Que salieran partículas pequeñas doradas desde donde estuviera el cursor.

<div id="pg-gold" class="dark-playground">
  <span class="pg-hint">// hover</span>
</div>

## Patrón escondido

Que hubiera puntos escondidos que solo aparecieran donde apuntara el ratón.

<div id="pg-pattern" class="dark-playground">
  <canvas id="pattern-canvas"></canvas>
  <span class="pg-hint pg-over">// hover</span>
</div>

## Cinco cursores

Que aparecieran cinco cursores siguiendo al mío, cada uno con más retraso que el anterior.

<div id="pg-cursors" class="dark-playground">
  <span class="pg-hint">// hover</span>
</div>

## Cable colgando

Que colgara un cable físico del icono del cursor.

<div id="pg-rope" class="dark-playground">
  <svg id="rope-svg"></svg>
  <span class="pg-hint pg-over">// hover</span>
</div>


## El botón

Que hubiera un botón con muchas ganas de ser pulsado.

<div id="pg-button" class="dark-playground">
  <button id="the-button">pulsa</button>
  <div id="btn-feedback">Qué pasa!?</div>
</div>

## TIL

- Que puedes meter HTML, CSS y JavaScript dentro de un `.md` en Astro
- Que describir lo que quieres ver es suficiente para que Claude lo construya
- Que hay muchos más efectos posibles con el ratón de los que jamás habría intentado explorar solo

<style>
.dark-playground {
  position: relative;
  height: 260px;
  border-radius: 8px;
  margin: 2rem 0;
  background: #09090f;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  cursor: crosshair;
}
.pg-hint {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.6875rem;
  color: rgba(255,255,255,0.18);
  text-transform: uppercase;
  letter-spacing: 0.1em;
  pointer-events: none;
  user-select: none;
  transition: opacity 0.4s;
}
.pg-over {
  position: absolute;
  z-index: 2;
}
.dark-playground.pg-active .pg-hint {
  opacity: 0;
}
#pg-pattern canvas {
  position: absolute;
  top: 0; left: 0;
}
#rope-svg {
  position: absolute;
  top: 0; left: 0;
  pointer-events: none;
  overflow: visible;
}
#pg-cursors,
#pg-rope {
  cursor: none;
}

#the-button {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.9rem;
  font-weight: 700;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: #09090f;
  background: #f0ede8;
  border: none;
  padding: 16px 44px;
  border-radius: 50px;
  cursor: pointer;
  position: relative;
  z-index: 1;
  animation: btnBreath 2.2s ease-in-out infinite;
  transition: transform 0.12s, box-shadow 0.15s;
}
#the-button:hover {
  animation: none;
  transform: scale(1.03);
  box-shadow: 0 0 24px rgba(255,255,255,0.12), 0 0 50px rgba(255,255,255,0.05);
  transition: transform 0.35s ease, box-shadow 0.35s ease;
}
#the-button:active {
  transform: scale(0.97);
  box-shadow: 0 0 8px rgba(255,255,255,0.06);
}
@keyframes btnBreath {
  0%,100% { box-shadow: 0 0 14px rgba(255,255,255,0.07), 0 0 30px rgba(255,255,255,0.03); transform: scale(1); }
  50%      { box-shadow: 0 0 22px rgba(255,255,255,0.13), 0 0 50px rgba(255,255,255,0.06); transform: scale(1.02); }
}
#btn-feedback {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: 'JetBrains Mono', monospace;
  font-size: clamp(3.5rem, 12vw, 7rem);
  font-weight: 800;
  letter-spacing: -0.04em;
  color: rgba(255,255,255,0.10);
  pointer-events: none;
  opacity: 0;
  z-index: 0;
}
#btn-feedback.show {
  animation: feedbackPop 2.8s ease forwards;
}
@keyframes feedbackPop {
  0%   { opacity: 0; transform: scale(0.92); }
  18%  { opacity: 1; transform: scale(1); }
  65%  { opacity: 1; }
  100% { opacity: 0; transform: scale(1.04); }
}
</style>

<script>
/* ---- POLAROIDS ---- */
(function () {
  var pg = document.getElementById('pg-polaroid');
  if (!pg) return;
  var last = 0;
  function spawn(x, y) {
    var now = Date.now();
    if (now - last < 110) return;
    last = now;
    var size = Math.random() * 28 + 62;
    var iR = Math.random() * 32 - 16;
    var fR = iR + Math.random() * 50 - 25;
    var fall = Math.random() * 130 + 160;
    var dur  = Math.random() * 500 + 1700;
    var f = document.createElement('div');
    f.style.cssText = 'position:fixed;left:'+x+'px;top:'+y+'px;width:'+size+'px;background:#fff;padding:4px 4px 14px;box-shadow:0 4px 20px rgba(0,0,0,.55);transform:translate(-50%,-50%) rotate('+iR+'deg);pointer-events:none;z-index:9999;';
    var img = document.createElement('img');
    img.src = '/sacrecoeur.jpg';
    img.style.cssText = 'width:'+(size-8)+'px;height:'+(size-8)+'px;object-fit:cover;display:block;';
    f.appendChild(img);
    document.body.appendChild(f);
    f.animate(
      [{opacity:1,transform:'translate(-50%,-50%) rotate('+iR+'deg)'},{opacity:0,transform:'translate(-50%,calc(-50% + '+fall+'px)) rotate('+fR+'deg)'}],
      {duration:dur,easing:'cubic-bezier(0.25,0.46,0.45,0.94)',fill:'forwards'}
    ).onfinish = function(){ f.remove(); };
  }
  pg.addEventListener('mousemove', function(e){ pg.classList.add('pg-active'); spawn(e.clientX, e.clientY); });
  pg.addEventListener('mouseleave', function(){ pg.classList.remove('pg-active'); });
})();

/* ---- GOLD PARTICLES ---- */
(function () {
  var pg = document.getElementById('pg-gold');
  if (!pg) return;
  var last = 0;
  function burst(x, y) {
    var now = Date.now();
    if (now - last < 14) return;
    last = now;
    for (var i = 0; i < 4; i++) {
      (function(){
        var el = document.createElement('div');
        var sz  = Math.random() * 4 + 2;
        var ang = Math.random() * Math.PI * 2;
        var spd = Math.random() * 55 + 18;
        var dx  = Math.cos(ang) * spd;
        var dy  = Math.sin(ang) * spd;
        var dur = Math.random() * 500 + 380;
        var hue = Math.random() * 22 + 36;
        var lit = Math.random() * 20 + 55;
        el.style.cssText = 'position:fixed;left:'+x+'px;top:'+y+'px;width:'+sz+'px;height:'+sz+'px;border-radius:50%;background:hsl('+hue+',100%,'+lit+'%);box-shadow:0 0 '+(sz*2.5)+'px hsl('+hue+',100%,70%);pointer-events:none;z-index:9999;';
        document.body.appendChild(el);
        el.animate(
          [{opacity:1,transform:'translate(-50%,-50%) scale(1)'},{opacity:0,transform:'translate(calc(-50% + '+dx+'px),calc(-50% + '+dy+'px)) scale(0.08)'}],
          {duration:dur,easing:'cubic-bezier(0,0.9,0.57,1)',fill:'forwards'}
        ).onfinish = function(){ el.remove(); };
      })();
    }
  }
  pg.addEventListener('mousemove', function(e){ pg.classList.add('pg-active'); burst(e.clientX, e.clientY); });
  pg.addEventListener('mouseleave', function(){ pg.classList.remove('pg-active'); });
})();

/* ---- PATTERN REVEAL ---- */
(function () {
  var pg     = document.getElementById('pg-pattern');
  var canvas = document.getElementById('pattern-canvas');
  if (!pg || !canvas) return;
  var ctx = canvas.getContext('2d');
  var SPACING = 22, RADIUS = 88;
  var mx = 0, my = 0, hovering = false;
  function resize() { canvas.width = pg.clientWidth; canvas.height = pg.clientHeight; }
  resize();
  if (typeof ResizeObserver !== 'undefined') new ResizeObserver(resize).observe(pg);
  function frame() {
    var W = canvas.width, H = canvas.height;
    ctx.fillStyle = '#09090f';
    ctx.fillRect(0, 0, W, H);
    for (var x = SPACING; x < W; x += SPACING) {
      for (var y = SPACING; y < H; y += SPACING) {
        var dx = x - mx, dy = y - my;
        var dist = Math.sqrt(dx*dx + dy*dy);
        if (hovering && dist < RADIUS) {
          var t = 1 - dist / RADIUS;
          ctx.fillStyle = 'rgba(160,190,255,' + (t*t*0.9) + ')';
          ctx.beginPath();
          ctx.arc(x, y, 1.8, 0, Math.PI*2);
          ctx.fill();
        } else {
          ctx.fillStyle = 'rgba(255,255,255,0.04)';
          ctx.beginPath();
          ctx.arc(x, y, 1.2, 0, Math.PI*2);
          ctx.fill();
        }
      }
    }
    requestAnimationFrame(frame);
  }
  frame();
  pg.addEventListener('mousemove', function(e){ hovering = true; mx = e.offsetX; my = e.offsetY; pg.classList.add('pg-active'); });
  pg.addEventListener('mouseleave', function(){ hovering = false; pg.classList.remove('pg-active'); });
})();

/* ---- 5 CURSOR FOLLOWERS ---- */
(function () {
  var pg = document.getElementById('pg-cursors');
  if (!pg) return;
  var N = 5;
  var LERPS    = [0.22, 0.15, 0.10, 0.07, 0.045];
  var OPACITIES= [1.0,  0.82, 0.62, 0.42, 0.26];
  var cursorPath = '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 20"><path d="M2,0 L2,14 L5,11 L8,18 L10,17 L7,10 L12,10 Z" fill="white" stroke="rgba(0,0,0,0.45)" stroke-width="0.7" stroke-linejoin="round"/></svg>';
  var src = 'data:image/svg+xml,' + encodeURIComponent(cursorPath);
  var tx = 100, ty = 100, hovering = false;
  var positions = [];
  var els = [];
  for (var i = 0; i < N; i++) {
    positions.push({ x: 100, y: 100 });
    var el = document.createElement('img');
    el.src = src;
    el.style.cssText = 'position:absolute;width:16px;height:20px;pointer-events:none;opacity:0;transition:opacity .25s;';
    pg.appendChild(el);
    els.push(el);
  }
  function tick() {
    for (var i = 0; i < N; i++) {
      var s = i === 0 ? { x: tx, y: ty } : positions[i-1];
      positions[i].x += (s.x - positions[i].x) * LERPS[i];
      positions[i].y += (s.y - positions[i].y) * LERPS[i];
      els[i].style.left    = (positions[i].x - 2) + 'px';
      els[i].style.top     = (positions[i].y - 2) + 'px';
      els[i].style.opacity = hovering ? OPACITIES[i] : 0;
    }
    requestAnimationFrame(tick);
  }
  tick();
  pg.addEventListener('mousemove', function(e){ hovering = true; tx = e.offsetX; ty = e.offsetY; pg.classList.add('pg-active'); });
  pg.addEventListener('mouseleave', function(){ hovering = false; pg.classList.remove('pg-active'); });
})();

/* ---- ROPE / CABLE ---- */
(function () {
  var pg  = document.getElementById('pg-rope');
  var svg = document.getElementById('rope-svg');
  if (!pg || !svg) return;
  var N = 12, SEG = 18, GRAVITY = 0.55, DAMP = 0.96, ITERS = 8;
  var W = pg.clientWidth, H = pg.clientHeight;
  svg.setAttribute('width', W);
  svg.setAttribute('height', H);
  var cx = W / 2;
  var nodes = [];
  for (var i = 0; i < N; i++) nodes.push({ x:cx, y:30+i*SEG, ox:cx, oy:30+i*SEG });
  var curX = cx, curY = 40, hovering = false;

  var polyline = document.createElementNS('http://www.w3.org/2000/svg','polyline');
  polyline.setAttribute('fill','none');
  polyline.setAttribute('stroke','rgba(255,255,255,0.75)');
  polyline.setAttribute('stroke-width','2');
  polyline.setAttribute('stroke-linecap','round');
  polyline.setAttribute('stroke-linejoin','round');
  svg.appendChild(polyline);

  var cursorPath = '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 20"><path d="M2,0 L2,14 L5,11 L8,18 L10,17 L7,10 L12,10 Z" fill="white" stroke="rgba(0,0,0,0.4)" stroke-width="0.7" stroke-linejoin="round"/></svg>';
  var curEl = document.createElement('img');
  curEl.src = 'data:image/svg+xml,' + encodeURIComponent(cursorPath);
  curEl.style.cssText = 'position:absolute;width:16px;height:20px;pointer-events:none;opacity:0;transition:opacity .3s;';
  pg.appendChild(curEl);

  function update() {
    if (hovering) {
      for (var i = 1; i < N; i++) {
        var n = nodes[i];
        var vx = (n.x - n.ox) * DAMP, vy = (n.y - n.oy) * DAMP;
        n.ox = n.x; n.oy = n.y;
        n.x += vx; n.y += vy + GRAVITY;
      }
      nodes[0].x = curX; nodes[0].y = curY;
      nodes[0].ox = curX; nodes[0].oy = curY;
      for (var iter = 0; iter < ITERS; iter++) {
        for (var i = 0; i < N-1; i++) {
          var a = nodes[i], b = nodes[i+1];
          var dx = b.x-a.x, dy = b.y-a.y;
          var dist = Math.sqrt(dx*dx+dy*dy)||0.001;
          var diff = (dist-SEG)/dist*0.5;
          if (i > 0) { a.x += dx*diff; a.y += dy*diff; }
          b.x -= dx*diff; b.y -= dy*diff;
        }
        nodes[0].x = curX; nodes[0].y = curY;
      }
      var pts = nodes.map(function(n){ return n.x.toFixed(1)+','+n.y.toFixed(1); }).join(' ');
      polyline.setAttribute('points', pts);
      curEl.style.left    = (curX - 2) + 'px';
      curEl.style.top     = (curY - 2) + 'px';
      curEl.style.opacity = '1';
    } else {
      curEl.style.opacity = '0';
    }
    requestAnimationFrame(update);
  }
  update();

  pg.addEventListener('mousemove', function(e){ hovering = true; curX = e.offsetX; curY = e.offsetY; pg.classList.add('pg-active'); });
  pg.addEventListener('mouseleave', function(){ hovering = false; pg.classList.remove('pg-active'); });
  if (typeof ResizeObserver !== 'undefined') {
    new ResizeObserver(function(){
      W = pg.clientWidth; H = pg.clientHeight;
      svg.setAttribute('width', W); svg.setAttribute('height', H);
    }).observe(pg);
  }
})();

/* ---- BUTTON ---- */
(function () {
  var btn      = document.getElementById('the-button');
  var feedback = document.getElementById('btn-feedback');
  if (!btn || !feedback) return;

  btn.addEventListener('click', function () {
    feedback.classList.remove('show');
    void feedback.offsetWidth; // restart animation
    feedback.classList.add('show');

    var rect = btn.getBoundingClientRect();
    var cx = rect.left + rect.width  / 2;
    var cy = rect.top  + rect.height / 2;
    for (var i = 0; i < 14; i++) {
      (function () {
        var el  = document.createElement('div');
        var sz  = Math.random() * 7 + 3;
        var ang = Math.random() * Math.PI * 2;
        var spd = Math.random() * 90 + 40;
        var dx  = Math.cos(ang) * spd, dy = Math.sin(ang) * spd;
        var dur = Math.random() * 400 + 450;
        el.style.cssText = 'position:fixed;left:'+cx+'px;top:'+cy+'px;width:'+sz+'px;height:'+sz+'px;border-radius:50%;background:#fff;box-shadow:0 0 '+(sz*2)+'px rgba(255,255,255,0.6);pointer-events:none;z-index:9999;';
        document.body.appendChild(el);
        el.animate(
          [{opacity:1,transform:'translate(-50%,-50%) scale(1)'},{opacity:0,transform:'translate(calc(-50% + '+dx+'px),calc(-50% + '+dy+'px)) scale(0.05)'}],
          {duration:dur,easing:'cubic-bezier(0,0.9,0.57,1)',fill:'forwards'}
        ).onfinish = function(){ el.remove(); };
      })();
    }
  });
})();

</script>
