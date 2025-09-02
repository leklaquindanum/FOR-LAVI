# FOR-LAVI
a small yet big anniversary gift

<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>SECRET CALCULATOR FOR MY IYATOOTS</title>
  <style>
    :root {
      --bg: #0f1226;
      --panel: #171a36;
      --accent: #7c5cff;
      --accent-2: #00d4ff;
      --text: #f5f6fb;
      --muted: #a8adcf;
      --danger: #ff5c7c;
    }
    * { box-sizing: border-box; }
    html, body { height: 100%; }
    body {
      margin: 0;
      font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, "Helvetica Neue", Arial, "Noto Sans", "Apple Color Emoji", "Segoe UI Emoji";
      color: var(--text);
      background: radial-gradient(1200px 800px at 20% 10%, #1b1f44, #0b0e1e 70%),
                  linear-gradient(135deg, #0c0f22, #0b0e1e);
      display: grid;
      place-items: center;
      padding: 24px;
    }
    .calc {
      width: min(380px, 92vw);
      background: linear-gradient(180deg, #1b1f40 0%, #141835 100%);
      border: 1px solid rgba(255,255,255,.06);
      border-radius: 24px;
      box-shadow: 0 20px 60px rgba(0,0,0,.4), inset 0 1px 0 rgba(255,255,255,.05);
      overflow: hidden;
    }
    .header {
      padding: 18px 20px 0 20px;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }
    .brand {
      font-weight: 700;
      letter-spacing: .5px;
      opacity: .9;
    }
    .display {
      padding: 18px 20px 24px 20px;
      text-align: right;
      min-height: 84px;
      display: flex;
      flex-direction: column;
      gap: 6px;
    }
    .history {
      font-size: 0.9rem;
      color: var(--muted);
      min-height: 1.2em;
      overflow: hidden;
      white-space: nowrap;
      text-overflow: ellipsis;
    }
    .screen {
      font-size: clamp(28px, 6vw, 42px);
      font-weight: 700;
      letter-spacing: .5px;
      overflow: hidden;
      white-space: nowrap;
      text-overflow: ellipsis;
    }
    .keys {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;
      padding: 16px;
      background: linear-gradient(180deg, #121530, #10122b);
      border-top: 1px solid rgba(255,255,255,.06);
    }
    button {
      appearance: none;
      border: 0;
      border-radius: 16px;
      padding: 16px 14px;
      font-size: 1.05rem;
      font-weight: 700;
      background: #1c2046;
      color: var(--text);
      box-shadow: inset 0 -2px 0 rgba(0,0,0,.25), 0 6px 16px rgba(0,0,0,.25);
      cursor: pointer;
      transition: transform .06s ease, filter .2s ease, background .2s ease;
      user-select: none;
    }
    button:active { transform: translateY(1px) scale(0.995); }
    button:hover { filter: brightness(1.07); }
    .op { background: linear-gradient(180deg, #2a2d62, #232659); }
    .accent { background: linear-gradient(180deg, var(--accent), #5b3dff); }
    .span-2 { grid-column: span 2; }
    .footer {
      padding: 10px 18px 18px 18px;
      font-size: .8rem;
      color: var(--muted);
      text-align: center;
      opacity: .8;
    }
    .overlay {
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,.65);
      display: none;
      align-items: center;
      justify-content: center;
      z-index: 50;
      backdrop-filter: blur(4px);
    }
    .overlay.show { display: flex; }
    .modal {
      width: min(680px, 92vw);
      background: linear-gradient(180deg, #1b1f40, #121531);
      border: 1px solid rgba(255,255,255,.08);
      border-radius: 24px;
      padding: 28px 24px;
      text-align: center;
      box-shadow: 0 30px 80px rgba(0,0,0,.5);
      position: relative;
      overflow: hidden;
    }

    .modal h1 {
      margin: 0 0 6px 0;
      font-size: clamp(22px, 4.8vw, 34px);
    }
    .modal p { margin: 6px 0 18px 0; color: var(--muted); }

    .close {
      position: absolute;
      top: 8px; right: 8px;
      background: transparent;
      border-radius: 10px;
      padding: 8px 10px;
      font-weight: 800;
      box-shadow: none;
    }

    .hearts { position: absolute; inset: 0; pointer-events: none; overflow: hidden; }
    .heart { position: absolute; bottom: -20px; font-size: 16px; opacity: .85; animation: floatUp 4.5s linear infinite; }
    @keyframes floatUp {
      0% { transform: translateY(0) translateX(0) rotate(0); opacity: .2; }
      30% { opacity: .95; }
      100% { transform: translateY(-120vh) translateX(var(--x, 0)) rotate(12deg); opacity: 0; }
    }
  </style>
</head>
<body>
  <div class="calc" role="application" aria-label="Calculator">
    <div class="header">
      <div class="brand">Enter the code (Clue: special date natin)</div>
    </div>
    <div class="display" aria-live="polite">
      <div id="history" class="history"></div>
      <div id="screen" class="screen">0</div>
    </div>
    <div class="keys">
      <button class="op" data-key="C" aria-label="Clear">C</button>
      <button class="op" data-key="(">(</button>
      <button class="op" data-key=")">)</button>
      <button class="op" data-key="/">÷</button>

      <button data-key="7">7</button>
      <button data-key="8">8</button>
      <button data-key="9">9</button>
      <button class="op" data-key="*">×</button>

      <button data-key="4">4</button>
      <button data-key="5">5</button>
      <button data-key="6">6</button>
      <button class="op" data-key="-">−</button>

      <button data-key="1">1</button>
      <button data-key="2">2</button>
      <button data-key="3">3</button>
      <button class="op" data-key="+">+</button>

      <button data-key="0" class="span-2">0</button>
      <button data-key=".">.</button>
      <button class="accent" data-key="=">=</button>
    </div>

  <!-- Celebration Modal -->
  <div class="overlay" id="overlay" role="dialog" aria-modal="true" aria-labelledby="celebrate-title">
    <div class="modal">
      <button class="close" id="close">✕</button>
      <h1 id="celebrate-title">HAPPY MOTMOT AND ANNIVERSARY</h1>
      <p>BABY BUBU LAVI</p>
      <div class="hearts" id="hearts"></div>
    </div>
  </div>

  <script>
    const screen = document.getElementById('screen');
    const historyEl = document.getElementById('history');
    let expr = '';

    const allowed = /[^0-9+\-*/(). %]/g;

    function updateScreen() {
      screen.textContent = expr || '0';
    }

    function append(ch) {
      if (ch === 'C') { expr = ''; historyEl.textContent = ''; updateScreen(); return; }
      if (ch === '=') { onEquals(); return; }
      if (ch === '%') { expr += '%'; updateScreen(); return; }
      if (ch === '⌫') { expr = expr.slice(0, -1); updateScreen(); return; }
      if (expr.length > 48) return;
      expr += ch;
      updateScreen();
    }

    function sanitize(s) { return (s || '').replace(allowed, ''); }

    function digitsOnly(s) { return (s || '').replace(/\D/g, ''); }

    function showSurprise() {
      const overlay = document.getElementById('overlay');
      const hearts = document.getElementById('hearts');
      overlay.classList.add('show');
      hearts.innerHTML = '';
    
      for (let i = 0; i < 42; i++) {
        const span = document.createElement('div');
        span.className = 'heart';
        span.textContent = ['❤','💜','💙','💖','💗','💞'][Math.floor(Math.random()*6)];
        span.style.left = Math.random()*100 + 'vw';
        span.style.fontSize = (14 + Math.random()*18) + 'px';
        span.style.animationDelay = (Math.random()*2) + 's';
        span.style.setProperty('--x', (Math.random()*80 - 40) + 'px');
        hearts.appendChild(span);
      }
      
      document.getElementById('close').focus();
    }

    function hideSurprise() {
      document.getElementById('overlay').classList.remove('show');
    }

    function onEquals() {
      const digits = digitsOnly(expr);
      if (digits === '060323') {
        historyEl.textContent = expr + ' =';
        expr = 'HAPPY MOTMOT AND ANNIVERSARY BABY BUBU LAVI';
        updateScreen();
        showSurprise();
        return;
      }
      const safe = sanitize(expr);
      if (!safe) return;
      try {
        const prepared = safe.replace(/(\d+(?:\.\d+)?)%/g, '($1/100)');
        const result = Function(`"use strict"; return (${prepared})`)();
        historyEl.textContent = safe + ' =';
        expr = String(result);
        updateScreen();
      } catch (e) {
        historyEl.textContent = '';
        expr = 'Error';
        updateScreen();
        setTimeout(() => { expr = ''; updateScreen(); }, 900);
      }
    }
    document.querySelectorAll('button[data-key]').forEach(btn => {
      btn.addEventListener('click', () => append(btn.dataset.key));
    });
    window.addEventListener('keydown', (e) => {
      const { key } = e;
      if (key === 'Enter' || key === '=') { e.preventDefault(); append('='); return; }
      if (key === 'Escape') { append('C'); return; }
      if (key === 'Backspace') { e.preventDefault(); expr = expr.slice(0, -1); updateScreen(); return; }
      if (/^[0-9+\-*/().%]$/.test(key)) { append(key); }
    });
    document.getElementById('close').addEventListener('click', hideSurprise);
    document.getElementById('overlay').addEventListener('click', (e) => {
      if (e.target.id === 'overlay') hideSurprise();
    });
    updateScreen();
  </script>
</body>
</html>
