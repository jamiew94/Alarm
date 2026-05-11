<!DOCTYPE html>

<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
  <meta name="mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="black">
  <meta name="theme-color" content="#0a0a0a">
  <title>WAKEUP PROTOCOL</title>
  <link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Oswald:wght@700&display=swap" rel="stylesheet">
  <style>
    :root {
      --red: #ff1a1a;
      --amber: #ff8c00;
      --green: #00ff88;
      --bg: #0a0a0a;
      --panel: #111111;
      --border: #2a2a2a;
      --text: #e0e0e0;
      --dim: #555;
    }

```
* { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }

body {
  background: var(--bg);
  color: var(--text);
  font-family: 'Share Tech Mono', monospace;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  overflow-x: hidden;
  position: relative;
}

body::before {
  content: '';
  position: fixed;
  inset: 0;
  background: repeating-linear-gradient(
    0deg,
    transparent,
    transparent 2px,
    rgba(0,0,0,0.15) 2px,
    rgba(0,0,0,0.15) 4px
  );
  pointer-events: none;
  z-index: 1;
}

/* ── HEADER ── */
.header {
  width: 100%;
  padding: 18px 20px 10px;
  border-bottom: 1px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.header-title {
  font-family: 'Oswald', sans-serif;
  font-size: 13px;
  letter-spacing: 4px;
  color: var(--red);
  text-transform: uppercase;
}
.status-dot {
  width: 8px; height: 8px;
  border-radius: 50%;
  background: var(--green);
  box-shadow: 0 0 8px var(--green);
  animation: blink 2s infinite;
}
@keyframes blink { 0%,100%{opacity:1} 50%{opacity:0.2} }

/* ── CLOCK ── */
.clock-wrap {
  padding: 30px 20px 20px;
  text-align: center;
  position: relative;
}
.clock {
  font-family: 'Oswald', sans-serif;
  font-size: clamp(64px, 18vw, 100px);
  font-weight: 700;
  letter-spacing: -2px;
  color: #fff;
  text-shadow: 0 0 30px rgba(255,255,255,0.15);
  line-height: 1;
}
.date-line {
  font-size: 11px;
  letter-spacing: 3px;
  color: var(--dim);
  margin-top: 6px;
  text-transform: uppercase;
}

/* ── PANELS ── */
.main {
  width: 100%;
  max-width: 480px;
  padding: 0 16px 40px;
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 14px;
}

.panel {
  background: var(--panel);
  border: 1px solid var(--border);
  border-radius: 4px;
  padding: 18px;
}
.panel-label {
  font-size: 9px;
  letter-spacing: 4px;
  color: var(--dim);
  text-transform: uppercase;
  margin-bottom: 14px;
}

/* ── TIME INPUT ── */
.time-input-row {
  display: flex;
  gap: 10px;
  align-items: center;
}
input[type="time"] {
  flex: 1;
  background: #1a1a1a;
  border: 1px solid #333;
  border-radius: 3px;
  color: #fff;
  font-family: 'Oswald', sans-serif;
  font-size: 36px;
  font-weight: 700;
  padding: 10px 14px;
  outline: none;
  -webkit-appearance: none;
  color-scheme: dark;
}
input[type="time"]:focus { border-color: var(--amber); }

/* ── CHALLENGE SELECTOR ── */
.challenge-row {
  display: flex;
  gap: 8px;
}
.challenge-btn {
  flex: 1;
  background: #1a1a1a;
  border: 1px solid #333;
  border-radius: 3px;
  color: var(--dim);
  font-family: 'Share Tech Mono', monospace;
  font-size: 11px;
  letter-spacing: 1px;
  padding: 10px 6px;
  cursor: pointer;
  text-align: center;
  transition: all 0.15s;
}
.challenge-btn.active {
  border-color: var(--amber);
  color: var(--amber);
  background: rgba(255,140,0,0.08);
}
.challenge-btn .icon { font-size: 18px; display: block; margin-bottom: 4px; }

/* ── BUTTONS ── */
.btn-set {
  width: 100%;
  background: var(--red);
  border: none;
  border-radius: 3px;
  color: #fff;
  font-family: 'Oswald', sans-serif;
  font-size: 20px;
  font-weight: 700;
  letter-spacing: 4px;
  padding: 16px;
  cursor: pointer;
  text-transform: uppercase;
  transition: all 0.15s;
  position: relative;
  overflow: hidden;
}
.btn-set:active { transform: scale(0.98); }
.btn-set.armed {
  background: #1a1a1a;
  border: 1px solid var(--green);
  color: var(--green);
}
.btn-set.armed::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(90deg, transparent 0%, rgba(0,255,136,0.06) 50%, transparent 100%);
  animation: sweep 3s linear infinite;
}
@keyframes sweep { from{transform:translateX(-100%)} to{transform:translateX(100%)} }

.btn-test {
  width: 100%;
  background: transparent;
  border: 1px solid #2a2a2a;
  border-radius: 3px;
  color: var(--dim);
  font-family: 'Share Tech Mono', monospace;
  font-size: 12px;
  letter-spacing: 2px;
  padding: 12px;
  cursor: pointer;
  transition: all 0.15s;
}
.btn-test:active { border-color: var(--amber); color: var(--amber); }

/* ── ALARM STATUS ── */
.alarm-status {
  text-align: center;
  padding: 10px;
  font-size: 11px;
  letter-spacing: 2px;
  color: var(--dim);
}
.alarm-status.armed { color: var(--green); }
.alarm-status span { color: #fff; }

/* ── LOG ── */
.log {
  font-size: 10px;
  letter-spacing: 1px;
  color: var(--dim);
  line-height: 1.8;
  max-height: 80px;
  overflow: hidden;
}
.log-entry { display: block; }
.log-entry.ok { color: var(--green); }
.log-entry.warn { color: var(--amber); }
.log-entry.err { color: var(--red); }

/* ══════════════════════════════════════
   ALARM OVERLAY
══════════════════════════════════════ */
#alarm-overlay {
  display: none;
  position: fixed;
  inset: 0;
  z-index: 9999;
  background: #000;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 30px 20px;
  overflow: hidden;
}
#alarm-overlay.active { display: flex; }

.overlay-bg {
  position: absolute;
  inset: 0;
  background: var(--red);
  opacity: 0;
  animation: pulse-bg 0.8s ease-in-out infinite alternate;
}
@keyframes pulse-bg { from{opacity:0.05} to{opacity:0.25} }

.overlay-scanlines {
  position: absolute;
  inset: 0;
  background: repeating-linear-gradient(
    0deg, transparent, transparent 3px,
    rgba(0,0,0,0.3) 3px, rgba(0,0,0,0.3) 6px
  );
  pointer-events: none;
}

.wake-title {
  font-family: 'Oswald', sans-serif;
  font-size: clamp(48px, 15vw, 80px);
  font-weight: 700;
  color: var(--red);
  letter-spacing: 6px;
  line-height: 1;
  position: relative;
  animation: shake 0.5s infinite;
  text-shadow: 0 0 40px rgba(255,26,26,0.6);
}
@keyframes shake {
  0%,100%{transform:translateX(0)}
  20%{transform:translateX(-3px)}
  40%{transform:translateX(3px)}
  60%{transform:translateX(-2px)}
  80%{transform:translateX(2px)}
}

.wake-sub {
  font-size: 11px;
  letter-spacing: 5px;
  color: var(--dim);
  margin-top: 8px;
  position: relative;
}

/* ── CHALLENGE AREA ── */
.challenge-area {
  position: relative;
  margin-top: 30px;
  width: 100%;
  max-width: 360px;
}

.challenge-counter {
  font-size: 10px;
  letter-spacing: 3px;
  color: var(--dim);
  margin-bottom: 14px;
}
.challenge-counter em { color: var(--amber); font-style: normal; }

.math-problem {
  font-family: 'Oswald', sans-serif;
  font-size: clamp(32px, 10vw, 48px);
  color: #fff;
  font-weight: 700;
  margin-bottom: 16px;
  position: relative;
}

.answer-input {
  width: 100%;
  background: #1a1a1a;
  border: 2px solid var(--amber);
  border-radius: 3px;
  color: #fff;
  font-family: 'Oswald', sans-serif;
  font-size: 32px;
  font-weight: 700;
  text-align: center;
  padding: 12px;
  outline: none;
  -webkit-appearance: none;
}
.answer-input.wrong {
  border-color: var(--red);
  animation: wrong-shake 0.3s ease;
}
@keyframes wrong-shake {
  0%,100%{transform:translateX(0)}
  25%{transform:translateX(-8px)}
  75%{transform:translateX(8px)}
}
.answer-input.correct { border-color: var(--green); }

.btn-submit {
  width: 100%;
  background: var(--amber);
  border: none;
  border-radius: 3px;
  color: #000;
  font-family: 'Oswald', sans-serif;
  font-size: 22px;
  font-weight: 700;
  letter-spacing: 3px;
  padding: 16px;
  cursor: pointer;
  margin-top: 12px;
  text-transform: uppercase;
  transition: all 0.1s;
}
.btn-submit:active { transform: scale(0.97); }

.progress-dots {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-top: 20px;
}
.dot {
  width: 10px; height: 10px;
  border-radius: 50%;
  background: #333;
  transition: all 0.3s;
}
.dot.done { background: var(--green); box-shadow: 0 0 8px var(--green); }
.dot.current { background: var(--amber); box-shadow: 0 0 8px var(--amber); }

/* re-arm notice */
.rearm-bar {
  position: absolute;
  bottom: 0; left: 0; right: 0;
  height: 3px;
  background: var(--dim);
  overflow: hidden;
}
.rearm-progress {
  height: 100%;
  background: var(--red);
  width: 0%;
  transition: width linear;
}

/* ── BUTTON MASH ── */
.mash-area { position: relative; }
.mash-btn {
  width: 180px; height: 180px;
  border-radius: 50%;
  background: radial-gradient(circle at 40% 35%, #ff4444, #aa0000);
  border: 4px solid var(--red);
  box-shadow: 0 0 40px rgba(255,26,26,0.5), inset 0 -4px 10px rgba(0,0,0,0.4);
  font-family: 'Oswald', sans-serif;
  font-size: 14px;
  letter-spacing: 2px;
  color: #fff;
  cursor: pointer;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  transition: transform 0.05s;
  -webkit-user-select: none;
  user-select: none;
}
.mash-btn:active { transform: scale(0.93); box-shadow: 0 0 15px rgba(255,26,26,0.4); }
.mash-count { font-size: 48px; font-weight: 700; line-height: 1; }
.mash-needed { font-size: 10px; letter-spacing: 3px; color: rgba(255,255,255,0.6); margin-top: 4px; }
.mash-bar-wrap {
  width: 200px;
  height: 6px;
  background: #222;
  border-radius: 3px;
  margin-top: 16px;
  overflow: hidden;
}
.mash-bar { height: 100%; background: var(--red); width: 0%; transition: width 0.1s; border-radius: 3px; }

/* ── DISMISSED ── */
.dismissed-screen {
  display: none;
  position: fixed;
  inset: 0;
  z-index: 10000;
  background: #0a0a0a;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 12px;
}
.dismissed-screen.show { display: flex; }
.dismissed-icon { font-size: 64px; }
.dismissed-text {
  font-family: 'Oswald', sans-serif;
  font-size: 28px;
  letter-spacing: 4px;
  color: var(--green);
}
.dismissed-sub { font-size: 11px; letter-spacing: 2px; color: var(--dim); }
.btn-reset {
  margin-top: 20px;
  background: transparent;
  border: 1px solid #333;
  border-radius: 3px;
  color: var(--dim);
  font-family: 'Share Tech Mono', monospace;
  font-size: 12px;
  letter-spacing: 2px;
  padding: 12px 24px;
  cursor: pointer;
}

/* volume warning */
.vol-warning {
  background: rgba(255,140,0,0.08);
  border: 1px solid rgba(255,140,0,0.25);
  border-radius: 3px;
  padding: 10px 14px;
  font-size: 10px;
  letter-spacing: 1px;
  color: var(--amber);
  line-height: 1.7;
}
```

  </style>
</head>
<body>

  <div class="header">
    <div class="header-title">⚡ Wakeup Protocol</div>
    <div class="status-dot" id="status-dot"></div>
  </div>

  <div class="clock-wrap">
    <div class="clock" id="clock">00:00:00</div>
    <div class="date-line" id="date-line">—</div>
  </div>

  <div class="main">

```
<div class="vol-warning">
  ⚠ BEFORE SETTING ALARM — Turn tablet volume to MAX.<br>
  This app cannot override system volume.
</div>

<div class="panel">
  <div class="panel-label">// Set Alarm Time</div>
  <div class="time-input-row">
    <input type="time" id="alarm-time" value="07:00">
  </div>
</div>

<div class="panel">
  <div class="panel-label">// Dismissal Challenge</div>
  <div class="challenge-row">
    <button class="challenge-btn active" data-mode="math" onclick="selectMode('math')">
      <span class="icon">🧮</span>
      3× MATH
    </button>
    <button class="challenge-btn" data-mode="mash" onclick="selectMode('mash')">
      <span class="icon">👊</span>
      30× MASH
    </button>
    <button class="challenge-btn" data-mode="both" onclick="selectMode('both')">
      <span class="icon">💀</span>
      BOTH
    </button>
  </div>
</div>

<button class="btn-set" id="btn-set" onclick="toggleAlarm()">
  SET ALARM
</button>

<div class="alarm-status" id="alarm-status">No alarm set</div>

<button class="btn-test" onclick="triggerTest()">
  ▶ TEST ALARM NOW
</button>

<div class="panel">
  <div class="panel-label">// System Log</div>
  <div class="log" id="log">
    <span class="log-entry">System ready.</span>
  </div>
</div>
```

  </div>

  <!-- ══ ALARM OVERLAY ══ -->

  <div id="alarm-overlay">
    <div class="overlay-bg"></div>
    <div class="overlay-scanlines"></div>

```
<div class="wake-title">WAKE UP</div>
<div class="wake-sub">ALARM FIRING — SOLVE TO DISMISS</div>

<div class="challenge-area" id="challenge-area">
  <!-- populated by JS -->
</div>

<div class="rearm-bar"><div class="rearm-progress" id="rearm-progress"></div></div>
```

  </div>

  <!-- ══ DISMISSED SCREEN ══ -->

  <div class="dismissed-screen" id="dismissed-screen">
    <div class="dismissed-icon">✅</div>
    <div class="dismissed-text">ALARM DISMISSED</div>
    <div class="dismissed-sub" id="dismissed-sub">Good morning. Alarm cleared.</div>
    <button class="btn-reset" onclick="fullReset()">SET NEW ALARM</button>
  </div>

<script>
// ── STATE ──────────────────────────────────────────────────────────
let alarmTime = null;
let alarmArmed = false;
let challengeMode = 'math';
let audioCtx = null;
let sirenNodes = [];
let checkInterval = null;
let rearmTimer = null;
let rearmProgressInterval = null;
let mathPhase = 0;
let mathProblems = [];
let mashCount = 0;
const MASH_TARGET = 30;
const REARM_SECONDS = 120; // re-fires after 2 minutes if not dismissed

// ── CLOCK ──────────────────────────────────────────────────────────
function updateClock() {
  const now = new Date();
  const h = String(now.getHours()).padStart(2,'0');
  const m = String(now.getMinutes()).padStart(2,'0');
  const s = String(now.getSeconds()).padStart(2,'0');
  document.getElementById('clock').textContent = `${h}:${m}:${s}`;
  const days = ['SUN','MON','TUE','WED','THU','FRI','SAT'];
  const months = ['JAN','FEB','MAR','APR','MAY','JUN','JUL','AUG','SEP','OCT','NOV','DEC'];
  document.getElementById('date-line').textContent =
    `${days[now.getDay()]} ${now.getDate()} ${months[now.getMonth()]} ${now.getFullYear()}`;
}
setInterval(updateClock, 1000);
updateClock();

// ── LOG ────────────────────────────────────────────────────────────
function log(msg, type='') {
  const logEl = document.getElementById('log');
  const now = new Date();
  const ts = `${String(now.getHours()).padStart(2,'0')}:${String(now.getMinutes()).padStart(2,'0')}:${String(now.getSeconds()).padStart(2,'0')}`;
  const entry = document.createElement('span');
  entry.className = `log-entry ${type}`;
  entry.textContent = `[${ts}] ${msg}`;
  logEl.insertBefore(entry, logEl.firstChild);
  while (logEl.children.length > 6) logEl.removeChild(logEl.lastChild);
}

// ── CHALLENGE MODE ─────────────────────────────────────────────────
function selectMode(mode) {
  challengeMode = mode;
  document.querySelectorAll('.challenge-btn').forEach(b => {
    b.classList.toggle('active', b.dataset.mode === mode);
  });
  log(`Challenge mode: ${mode.toUpperCase()}`, 'ok');
}

// ── AUDIO ──────────────────────────────────────────────────────────
function initAudio() {
  if (!audioCtx) {
    audioCtx = new (window.AudioContext || window.webkitAudioContext)();
  }
  if (audioCtx.state === 'suspended') audioCtx.resume();
}

function startSiren() {
  initAudio();
  stopSiren();

  const ctx = audioCtx;
  const master = ctx.createGain();
  master.gain.value = 0.9;
  master.connect(ctx.destination);

  // Layer 1: high warble
  const osc1 = ctx.createOscillator();
  osc1.type = 'sawtooth';
  osc1.frequency.value = 960;
  const lfo1 = ctx.createOscillator();
  lfo1.frequency.value = 4;
  const lfoG1 = ctx.createGain();
  lfoG1.gain.value = 200;
  lfo1.connect(lfoG1);
  lfoG1.connect(osc1.frequency);

  // Layer 2: low pulse
  const osc2 = ctx.createOscillator();
  osc2.type = 'square';
  osc2.frequency.value = 320;
  const lfo2 = ctx.createOscillator();
  lfo2.frequency.value = 2;
  const lfoG2 = ctx.createGain();
  lfoG2.gain.value = 0.3;
  lfo2.connect(lfoG2);
  lfoG2.connect(osc2.frequency);

  // Pulse gain
  const pulseGain = ctx.createGain();
  pulseGain.gain.value = 0.5;
  const pulseLFO = ctx.createOscillator();
  pulseLFO.frequency.value = 2.5;
  const pulseMod = ctx.createGain();
  pulseMod.gain.value = 0.45;
  pulseLFO.connect(pulseMod);
  pulseMod.connect(pulseGain.gain);

  osc1.connect(pulseGain);
  osc2.connect(pulseGain);
  pulseGain.connect(master);

  osc1.start(); lfo1.start();
  osc2.start(); lfo2.start();
  pulseLFO.start();

  sirenNodes = [osc1, lfo1, osc2, lfo2, pulseLFO, pulseGain, master];
}

function stopSiren() {
  sirenNodes.forEach(n => { try { n.stop ? n.stop() : n.disconnect(); } catch(e){} });
  sirenNodes = [];
}

// ── ALARM ARM/DISARM ───────────────────────────────────────────────
function toggleAlarm() {
  initAudio(); // grab gesture for audio context

  if (alarmArmed) {
    disarmAlarm();
    return;
  }

  const timeVal = document.getElementById('alarm-time').value;
  if (!timeVal) { log('No time set!', 'err'); return; }

  alarmTime = timeVal;
  alarmArmed = true;

  const btn = document.getElementById('btn-set');
  btn.textContent = '⏹ CANCEL ALARM';
  btn.classList.add('armed');

  document.getElementById('status-dot').style.background = 'var(--amber)';
  document.getElementById('status-dot').style.boxShadow = '0 0 8px var(--amber)';

  const statusEl = document.getElementById('alarm-status');
  statusEl.textContent = `Armed for ${timeVal}`;
  statusEl.className = 'alarm-status armed';

  clearInterval(checkInterval);
  checkInterval = setInterval(checkAlarm, 1000);

  log(`Alarm armed → ${timeVal}`, 'ok');
}

function disarmAlarm() {
  alarmArmed = false;
  alarmTime = null;
  clearInterval(checkInterval);

  const btn = document.getElementById('btn-set');
  btn.textContent = 'SET ALARM';
  btn.classList.remove('armed');

  document.getElementById('status-dot').style.background = 'var(--green)';
  document.getElementById('status-dot').style.boxShadow = '0 0 8px var(--green)';

  document.getElementById('alarm-status').textContent = 'No alarm set';
  document.getElementById('alarm-status').className = 'alarm-status';

  log('Alarm disarmed.', 'warn');
}

// ── ALARM CHECK ────────────────────────────────────────────────────
let lastFiredMinute = null;

function checkAlarm() {
  if (!alarmArmed || !alarmTime) return;
  const now = new Date();
  const h = String(now.getHours()).padStart(2,'0');
  const m = String(now.getMinutes()).padStart(2,'0');
  const current = `${h}:${m}`;
  const alarmMin = alarmTime.substring(0,5);

  if (current === alarmMin && lastFiredMinute !== alarmMin) {
    lastFiredMinute = alarmMin;
    fireAlarm();
  }
  // reset fire lock after minute passes
  if (current !== alarmMin && lastFiredMinute === alarmMin) {
    lastFiredMinute = null;
  }
}

// ── FIRE ALARM ─────────────────────────────────────────────────────
function fireAlarm() {
  log('🔴 ALARM FIRING', 'err');
  startSiren();

  // Try fullscreen on Android
  const el = document.documentElement;
  if (el.requestFullscreen) el.requestFullscreen().catch(()=>{});
  else if (el.webkitRequestFullscreen) el.webkitRequestFullscreen();

  const overlay = document.getElementById('alarm-overlay');
  overlay.classList.add('active');

  buildChallenge();
  startRearmTimer();
}

// ── RE-ARM TIMER ───────────────────────────────────────────────────
function startRearmTimer() {
  clearTimeout(rearmTimer);
  clearInterval(rearmProgressInterval);

  const bar = document.getElementById('rearm-progress');
  bar.style.transition = 'none';
  bar.style.width = '0%';

  let elapsed = 0;
  rearmProgressInterval = setInterval(() => {
    elapsed++;
    const pct = (elapsed / REARM_SECONDS) * 100;
    bar.style.transition = `width 1s linear`;
    bar.style.width = pct + '%';
    if (elapsed >= REARM_SECONDS) {
      clearInterval(rearmProgressInterval);
    }
  }, 1000);

  rearmTimer = setTimeout(() => {
    log('⚠ Dismissed attempt failed — re-firing!', 'err');
    buildChallenge(); // reset challenge
    startRearmTimer();
    startSiren(); // restart siren
  }, REARM_SECONDS * 1000);
}

// ── CHALLENGE BUILDER ──────────────────────────────────────────────
function buildChallenge() {
  const area = document.getElementById('challenge-area');
  area.innerHTML = '';
  mathPhase = 0;
  mashCount = 0;

  if (challengeMode === 'math') {
    buildMathChallenge(area);
  } else if (challengeMode === 'mash') {
    buildMashChallenge(area);
  } else {
    // BOTH: math first, then mash
    buildMathChallenge(area);
  }
}

// ── MATH CHALLENGE ─────────────────────────────────────────────────
function generateProblems() {
  const ops = ['+', '-', '×'];
  const probs = [];
  for (let i = 0; i < 3; i++) {
    const op = ops[Math.floor(Math.random() * ops.length)];
    let a, b, answer;
    if (op === '+') {
      a = 10 + Math.floor(Math.random() * 60);
      b = 10 + Math.floor(Math.random() * 60);
      answer = a + b;
    } else if (op === '-') {
      a = 30 + Math.floor(Math.random() * 50);
      b = 10 + Math.floor(Math.random() * (a - 10));
      answer = a - b;
    } else {
      a = 2 + Math.floor(Math.random() * 10);
      b = 2 + Math.floor(Math.random() * 10);
      answer = a * b;
    }
    probs.push({ q: `${a} ${op} ${b} = ?`, answer });
  }
  return probs;
}

function buildMathChallenge(container) {
  mathProblems = generateProblems();

  const html = `
    <div class="challenge-counter">
      PROBLEM <em id="prob-num">1</em> OF 3 — ALL MUST BE SOLVED
    </div>
    <div class="math-problem" id="math-q">${mathProblems[0].q}</div>
    <input type="number" class="answer-input" id="answer-input"
      placeholder="?" inputmode="numeric" autocomplete="off"
      oninput="clearWrong()" onkeydown="handleEnter(event)">
    <button class="btn-submit" onclick="checkAnswer()">SUBMIT</button>
    <div class="progress-dots" id="progress-dots">
      <div class="dot current"></div>
      <div class="dot"></div>
      <div class="dot"></div>
    </div>
  `;
  container.innerHTML = html;
  setTimeout(() => {
    const inp = document.getElementById('answer-input');
    if (inp) inp.focus();
  }, 300);
}

function handleEnter(e) {
  if (e.key === 'Enter') checkAnswer();
}

function clearWrong() {
  const inp = document.getElementById('answer-input');
  if (inp) inp.classList.remove('wrong');
}

function checkAnswer() {
  const inp = document.getElementById('answer-input');
  if (!inp) return;
  const val = parseInt(inp.value.trim(), 10);
  if (isNaN(val)) { inp.classList.add('wrong'); return; }

  if (val === mathProblems[mathPhase].answer) {
    inp.classList.add('correct');
    // update dots
    const dots = document.querySelectorAll('.dot');
    dots[mathPhase].classList.remove('current');
    dots[mathPhase].classList.add('done');
    mathPhase++;

    if (mathPhase < 3) {
      setTimeout(() => {
        inp.value = '';
        inp.classList.remove('correct');
        document.getElementById('math-q').textContent = mathProblems[mathPhase].q;
        document.getElementById('prob-num').textContent = mathPhase + 1;
        if (dots[mathPhase]) dots[mathPhase].classList.add('current');
        inp.focus();
      }, 400);
    } else {
      // All 3 solved
      setTimeout(() => {
        if (challengeMode === 'both') {
          // Now do mash
          const area = document.getElementById('challenge-area');
          buildMashChallenge(area);
        } else {
          dismissAlarm();
        }
      }, 500);
    }
  } else {
    inp.classList.add('wrong');
    inp.value = '';
    log('Wrong answer — try again', 'err');
    // Penalise: add 20s to re-arm timer? No, just shake is enough
    setTimeout(() => inp.focus(), 100);
  }
}

// ── MASH CHALLENGE ─────────────────────────────────────────────────
function buildMashChallenge(container) {
  mashCount = 0;
  const html = `
    <div class="mash-area" style="display:flex;flex-direction:column;align-items:center">
      <div style="font-size:10px;letter-spacing:3px;color:var(--dim);margin-bottom:16px">
        MASH THE BUTTON ${MASH_TARGET} TIMES
      </div>
      <button class="mash-btn" id="mash-btn" onclick="mash()">
        <span class="mash-count" id="mash-count">${MASH_TARGET}</span>
        <span class="mash-needed">LEFT</span>
      </button>
      <div class="mash-bar-wrap">
        <div class="mash-bar" id="mash-bar"></div>
      </div>
    </div>
  `;
  container.innerHTML = html;
}

function mash() {
  mashCount++;
  const remaining = MASH_TARGET - mashCount;
  document.getElementById('mash-count').textContent = Math.max(0, remaining);
  const pct = (mashCount / MASH_TARGET) * 100;
  document.getElementById('mash-bar').style.width = Math.min(pct, 100) + '%';

  if (mashCount >= MASH_TARGET) {
    dismissAlarm();
  }
}

// ── DISMISS ────────────────────────────────────────────────────────
function dismissAlarm() {
  stopSiren();
  clearTimeout(rearmTimer);
  clearInterval(rearmProgressInterval);

  document.getElementById('alarm-overlay').classList.remove('active');

  // Exit fullscreen
  if (document.exitFullscreen) document.exitFullscreen().catch(()=>{});
  else if (document.webkitExitFullscreen) document.webkitExitFullscreen();

  const dismissedEl = document.getElementById('dismissed-screen');
  const now = new Date();
  document.getElementById('dismissed-sub').textContent =
    `Dismissed at ${String(now.getHours()).padStart(2,'0')}:${String(now.getMinutes()).padStart(2,'0')}. Good morning.`;
  dismissedEl.classList.add('show');

  alarmArmed = false;
  clearInterval(checkInterval);

  log('Alarm dismissed.', 'ok');
}

function fullReset() {
  document.getElementById('dismissed-screen').classList.remove('show');
  lastFiredMinute = null;
  alarmArmed = false;
  alarmTime = null;

  const btn = document.getElementById('btn-set');
  btn.textContent = 'SET ALARM';
  btn.classList.remove('armed');
  document.getElementById('alarm-status').textContent = 'No alarm set';
  document.getElementById('alarm-status').className = 'alarm-status';
  document.getElementById('status-dot').style.background = 'var(--green)';
  document.getElementById('status-dot').style.boxShadow = '0 0 8px var(--green)';

  log('System reset. Ready.', 'ok');
}

// ── TEST ───────────────────────────────────────────────────────────
function triggerTest() {
  initAudio();
  log('TEST FIRE initiated', 'warn');
  fireAlarm();
}

// ── KEEP SCREEN AWAKE (where supported) ───────────────────────────
async function requestWakeLock() {
  if ('wakeLock' in navigator) {
    try {
      await navigator.wakeLock.request('screen');
      log('Screen wake lock acquired.', 'ok');
    } catch(e) {
      log('Wake lock unavailable.', 'warn');
    }
  }
}
requestWakeLock();
document.addEventListener('visibilitychange', () => {
  if (document.visibilityState === 'visible') requestWakeLock();
});

log('System initialised. Set your alarm.', 'ok');
</script>

</body>
</html>
