<!DOCTYPE html>

<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>税金RUSH — 庶民の逆襲</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Dela+Gothic+One&family=Share+Tech+Mono&display=swap');

:root {
–red: #e8002d;
–gold: #d4a017;
–cream: #f5f0e8;
–dark: #1a1008;
–ink: #2a1a00;
}

- { margin: 0; padding: 0; box-sizing: border-box; }

body {
background: #1a1008;
color: var(–cream);
font-family: ‘Share Tech Mono’, monospace;
display: flex;
flex-direction: column;
align-items: center;
justify-content: center;
min-height: 100vh;
overflow: hidden;
user-select: none;
}

body::before {
content: ‘’;
position: fixed;
inset: 0;
background:
repeating-linear-gradient(
0deg,
transparent,
transparent 38px,
rgba(212,160,23,0.06) 38px,
rgba(212,160,23,0.06) 40px
);
pointer-events: none;
}

h1 {
font-family: ‘Dela Gothic One’, sans-serif;
font-size: clamp(1.4rem, 4.5vw, 2.4rem);
color: var(–gold);
text-shadow: 3px 3px 0 var(–red), 6px 6px 0 rgba(0,0,0,0.4);
letter-spacing: 0.05em;
margin-bottom: 0.1em;
animation: shake 4s ease-in-out infinite;
}

@keyframes shake {
0%,100% { transform: rotate(-1deg); }
50% { transform: rotate(1deg); }
}

.subtitle {
font-size: 0.72rem;
color: rgba(212,160,23,0.6);
letter-spacing: 0.2em;
margin-bottom: 0.8rem;
}

#hud {
display: flex;
gap: 1.5rem;
margin-bottom: 0.7rem;
font-family: ‘Dela Gothic One’, sans-serif;
}

.hud-item { text-align: center; }
.hud-label { font-family: ‘Share Tech Mono’, monospace; font-size: 0.52rem; letter-spacing: 0.15em; color: rgba(245,240,232,0.4); }
.hud-value { font-size: 1.05rem; }

#wallet-val { color: #44ff88; text-shadow: 0 0 8px #44ff88; }
#tax-val { color: var(–red); text-shadow: 0 0 8px var(–red); }
#lives-val { color: var(–gold); }
#level-val { color: #ff9900; }

#canvas-wrap {
position: relative;
border: 2px solid rgba(212,160,23,0.3);
box-shadow: 0 0 30px rgba(212,160,23,0.1), inset 0 0 30px rgba(0,0,0,0.7);
}

canvas { display: block; background: #1a1008; }

#overlay {
position: absolute;
inset: 0;
display: flex;
flex-direction: column;
align-items: center;
justify-content: center;
background: rgba(26,16,8,0.95);
transition: opacity 0.3s;
overflow-y: auto;
padding: 1rem;
}
#overlay.hidden { opacity: 0; pointer-events: none; }

.ol-title {
font-family: ‘Dela Gothic One’, sans-serif;
font-size: clamp(1.3rem, 4vw, 2rem);
color: var(–gold);
text-shadow: 2px 2px 0 var(–red);
margin-bottom: 0.3em;
text-align: center;
}
.ol-sub { font-size: 0.78rem; color: rgba(245,240,232,0.5); margin-bottom: 0.4rem; text-align: center; line-height: 1.6; }
.ol-score { font-family: ‘Dela Gothic One’, sans-serif; font-size: 1rem; color: #44ff88; margin-bottom: 0.8rem; }

#ranking-wrap {
width: 88%;
margin-bottom: 0.8rem;
border: 1px solid rgba(212,160,23,0.2);
background: rgba(212,160,23,0.04);
}
.ranking-header {
font-family: ‘Dela Gothic One’, sans-serif;
font-size: 0.6rem;
letter-spacing: 0.15em;
color: var(–gold);
padding: 0.45rem 0.8rem;
border-bottom: 1px solid rgba(212,160,23,0.15);
}
.rank-row {
display: flex;
align-items: center;
padding: 0.35rem 0.8rem;
font-size: 0.75rem;
border-bottom: 1px solid rgba(255,255,255,0.04);
}
.rank-row:last-child { border-bottom: none; }
.rank-row.highlight { background: rgba(212,160,23,0.1); }
.rank-num { width: 1.6rem; color: rgba(255,255,255,0.4); font-size: 0.65rem; }
.rank-num.gold { color: #ffd700; }
.rank-num.silver { color: #c0c0c0; }
.rank-num.bronze { color: #cd7f32; }
.rank-name { flex: 1; color: rgba(245,240,232,0.8); }
.rank-score { color: #44ff88; font-family: ‘Dela Gothic One’, sans-serif; font-size: 0.7rem; }
.rank-date { font-size: 0.55rem; color: rgba(255,255,255,0.22); margin-left: 0.4rem; }
.empty-rank { padding: 0.7rem; text-align: center; color: rgba(255,255,255,0.2); font-size: 0.7rem; }

#name-wrap {
display: flex; gap: 0.5rem; margin-bottom: 0.8rem; width: 88%;
}
#name-input {
flex: 1;
background: rgba(212,160,23,0.06);
border: 1px solid rgba(212,160,23,0.35);
color: var(–cream);
font-family: ‘Share Tech Mono’, monospace;
font-size: 0.8rem;
padding: 0.45em 0.7em;
outline: none;
}
#name-input:focus { border-color: var(–gold); }
#name-input::placeholder { color: rgba(255,255,255,0.2); }

button {
font-family: ‘Dela Gothic One’, sans-serif;
font-size: 0.82rem;
letter-spacing: 0.1em;
padding: 0.6em 1.8em;
background: transparent;
color: var(–gold);
border: 2px solid var(–gold);
cursor: pointer;
transition: all 0.2s;
}
button:hover { background: var(–gold); color: var(–dark); box-shadow: 0 0 20px rgba(212,160,23,0.5); }
#start-btn { padding: 0.7em 2.2em; font-size: 0.95rem; }

.instructions {
margin-top: 0.8rem;
font-size: 0.65rem;
color: rgba(255,255,255,0.22);
text-align: center;
line-height: 1.9;
}
.instructions span { color: rgba(212,160,23,0.6); }

.news-ticker {
position: fixed;
bottom: 0; left: 0; right: 0;
background: var(–red);
padding: 0.3rem 0;
font-size: 0.7rem;
overflow: hidden;
white-space: nowrap;
}
.ticker-inner {
display: inline-block;
animation: ticker 30s linear infinite;
padding-left: 100%;
}
@keyframes ticker {
from { transform: translateX(0); }
to { transform: translateX(-100%); }
}
</style>

</head>
<body>

<h1>💸 税金RUSH</h1>
<p class="subtitle">庶民の逆襲 — 取られる前に逃げろ！</p>

<div id="hud">
  <div class="hud-item">
    <div class="hud-label">お財布</div>
    <div class="hud-value" id="wallet-val">¥0</div>
  </div>
  <div class="hud-item">
    <div class="hud-label">徴収額</div>
    <div class="hud-value" id="tax-val">¥0</div>
  </div>
  <div class="hud-item">
    <div class="hud-label">体力</div>
    <div class="hud-value" id="lives-val">💴💴💴</div>
  </div>
  <div class="hud-item">
    <div class="hud-label">圧力</div>
    <div class="hud-value" id="level-val">LV1</div>
  </div>
</div>

<div id="canvas-wrap">
  <canvas id="game" width="400" height="540"></canvas>

  <div id="overlay">
    <div class="ol-title" id="ol-title">💸 税金RUSH</div>
    <div class="ol-sub" id="ol-sub">給付金💴を拾い、税務署👮・増税パンチ💥・<br>特殊法人👔を避けて生き残れ！</div>
    <div class="ol-score" id="ol-score"></div>

```
<div id="name-wrap" style="display:none">
  <input id="name-input" maxlength="10" placeholder="なまえ (最大10文字)">
  <button id="save-btn">登録</button>
</div>

<div id="ranking-wrap">
  <div class="ranking-header">🏆 逃げ切り名人 ランキング</div>
  <div id="ranking-list"></div>
</div>

<button id="start-btn">ゲームスタート</button>
<div class="instructions">
  <span>← →</span> キー または スワイプで移動<br>
  💴 給付金を拾うとお財布UP<br>
  👮‍♂️ 税務署・💰 増税・🏦 天下り に当たると徴収！<br>
  <span>※このゲームはフィクションです</span>
</div>
```

  </div>
</div>

<div class="news-ticker">
  <span class="ticker-inner">
    【速報】消費税がさらに引き上げへ　▶　【緊急】給付金1人あたり¥500　▶　【独自】特殊法人への補助金、今年も最高額更新　▶　【解説】なぜ我々の財布は軽くなるのか　▶　【速報】インボイス制度で個人事業主に追い打ち　▶　【独自】議員歳費は据え置き、庶民だけ増税　▶
  </span>
</div>

<script>
// ===== Audio =====
let actx;
function getActx() {
  if (!actx) actx = new (window.AudioContext||window.webkitAudioContext)();
  if (actx.state === 'suspended') actx.resume();
  return actx;
}
function playTone(freq, type, dur, vol=0.25) {
  try {
    const ac = getActx(), o = ac.createOscillator(), g = ac.createGain();
    o.connect(g); g.connect(ac.destination);
    o.type = type; o.frequency.value = freq;
    g.gain.setValueAtTime(vol, ac.currentTime);
    g.gain.exponentialRampToValueAtTime(0.001, ac.currentTime + dur);
    o.start(); o.stop(ac.currentTime + dur);
  } catch(e) {}
}
function playCoin() { playTone(880,'sine',0.08,0.2); setTimeout(()=>playTone(1100,'sine',0.08,0.18),60); }
function playTax() { playTone(180,'sawtooth',0.22,0.35); setTimeout(()=>playTone(120,'square',0.15,0.3),90); }
function playLevelUp() { [261,329,392,523].forEach((f,i)=>setTimeout(()=>playTone(f,'sine',0.18,0.25),i*80)); }
function playGameOver() { [350,280,220,160].forEach((f,i)=>setTimeout(()=>playTone(f,'sawtooth',0.28,0.35),i*110)); }

// ===== BGM =====
// コード進行: Am - F - C - G (庶民の哀愁漂うループ)
let bgmNodes = [];
let bgmPlaying = false;

const BGM_NOTES = {
  // ベースライン
  bass: [
    [110,0.0],[110,0.5],[165,1.0],[110,1.5],
    [87, 2.0],[87, 2.5],[130,3.0],[87, 3.5],
    [98, 4.0],[98, 4.5],[146,5.0],[98, 5.5],
    [98, 6.0],[98, 6.5],[123,7.0],[98, 7.5],
  ],
  // メロディ
  melody: [
    [440,0.0,0.4],[392,0.5,0.4],[349,1.0,0.7],
    [330,2.0,0.4],[349,2.5,0.4],[392,3.0,0.7],
    [392,4.0,0.4],[440,4.5,0.4],[392,5.0,0.4],[349,5.5,0.4],
    [330,6.0,0.9],[392,7.0,0.4],[440,7.5,0.4],
  ],
  // コード（和音）
  chords: [
    [[220,262,330], 0.0, 1.8],
    [[174,220,261], 2.0, 1.8],
    [[196,247,294], 4.0, 1.8],
    [[196,233,294], 6.0, 1.8],
  ]
};

const BGM_LOOP = 8; // seconds

function startBGM() {
  if (bgmPlaying) return;
  bgmPlaying = true;
  scheduleBGM();
}

function scheduleBGM() {
  if (!bgmPlaying) return;
  try {
    const ac = getActx();
    const now = ac.currentTime;
    const masterGain = ac.createGain();
    masterGain.gain.value = 0.13;
    masterGain.connect(ac.destination);
    bgmNodes.push(masterGain);

    // ベース
    BGM_NOTES.bass.forEach(([freq, t]) => {
      const o = ac.createOscillator(), g = ac.createGain();
      o.type = 'triangle'; o.frequency.value = freq;
      g.gain.setValueAtTime(0.6, now + t);
      g.gain.exponentialRampToValueAtTime(0.001, now + t + 0.45);
      o.connect(g); g.connect(masterGain);
      o.start(now + t); o.stop(now + t + 0.5);
      bgmNodes.push(o, g);
    });

    // メロディ
    BGM_NOTES.melody.forEach(([freq, t, dur]) => {
      const o = ac.createOscillator(), g = ac.createGain();
      o.type = 'sine'; o.frequency.value = freq;
      g.gain.setValueAtTime(0.35, now + t);
      g.gain.setValueAtTime(0.25, now + t + dur * 0.6);
      g.gain.exponentialRampToValueAtTime(0.001, now + t + dur);
      o.connect(g); g.connect(masterGain);
      o.start(now + t); o.stop(now + t + dur + 0.05);
      bgmNodes.push(o, g);
    });

    // コード（柔らかめ）
    BGM_NOTES.chords.forEach(([freqs, t, dur]) => {
      freqs.forEach(freq => {
        const o = ac.createOscillator(), g = ac.createGain();
        o.type = 'sine'; o.frequency.value = freq;
        g.gain.setValueAtTime(0.0, now + t);
        g.gain.linearRampToValueAtTime(0.12, now + t + 0.1);
        g.gain.setValueAtTime(0.10, now + t + dur - 0.2);
        g.gain.exponentialRampToValueAtTime(0.001, now + t + dur);
        o.connect(g); g.connect(masterGain);
        o.start(now + t); o.stop(now + t + dur + 0.05);
        bgmNodes.push(o, g);
      });
    });

    // 次のループをスケジュール
    setTimeout(() => {
      bgmNodes = [];
      scheduleBGM();
    }, BGM_LOOP * 1000 - 100);

  } catch(e) {}
}

function stopBGM() {
  bgmPlaying = false;
  bgmNodes.forEach(n => { try { n.disconnect(); } catch(e) {} });
  bgmNodes = [];
}

// ===== Storage =====
const KEY = 'zeikin_rush_v1';
function loadRankings() { try { return JSON.parse(localStorage.getItem(KEY))||[]; } catch { return []; } }
function saveRanking(name, score) {
  const r = loadRankings();
  r.push({ name: name||'名無し', score, date: new Date().toLocaleDateString('ja-JP',{month:'numeric',day:'numeric'}) });
  r.sort((a,b)=>b.score-a.score);
  const top = r.slice(0,10);
  localStorage.setItem(KEY, JSON.stringify(top));
  return top;
}
function getBest() { const r=loadRankings(); return r.length?r[0].score:0; }

// ===== Game =====
const canvas = document.getElementById('game');
const ctx = canvas.getContext('2d');
const W=canvas.width, H=canvas.height;

const overlay=document.getElementById('overlay');
const olTitle=document.getElementById('ol-title');
const olSub=document.getElementById('ol-sub');
const olScore=document.getElementById('ol-score');
const startBtn=document.getElementById('start-btn');
const nameWrap=document.getElementById('name-wrap');
const nameInput=document.getElementById('name-input');
const saveBtn=document.getElementById('save-btn');

const walletEl=document.getElementById('wallet-val');
const taxEl=document.getElementById('tax-val');
const livesEl=document.getElementById('lives-val');
const levelEl=document.getElementById('level-val');

let state, player, objects, particles, floats;
let wallet, taxed, lives, level, frameCount, lastTime, animId, lastLevel;
let keys={}, touchStartX=null, pendingScore=null;

// Satirical enemy types
const ENEMY_TYPES = [
  { type:'officer',  emoji:'👮', label:'税務署',   color:'#e8002d', r:16, msg:['ちょっとよろしいですか？','税金払えや！','申告漏れ発見！'] },
  { type:'tax',      emoji:'💰', label:'増税',     color:'#cc4400', r:14, msg:['また増税だ〜','消費税15%！','財源確保！'] },
  { type:'corp',     emoji:'👔', label:'天下り',   color:'#884400', r:15, msg:['退職金3億円！','補助金ゲット','特権階級です'] },
  { type:'invoice',  emoji:'📋', label:'インボイス',color:'#aa0055', r:13, msg:['インボイス登録！','フリーランス死亡','制度改正です'] },
  { type:'politic',  emoji:'🎩', label:'議員',     color:'#660033', r:17, msg:['歳費は据え置き','政治資金です','裏金？知らん'] },
];

const GOOD_TYPES = [
  { type:'kyufu',   emoji:'💴', label:'給付金¥500', color:'#44ff88', r:14, pts:100, msg:['給付金ゲット！','たった¥500…','ありがとう政府(棒)'] },
  { type:'bento',   emoji:'🍱', label:'節約弁当',   color:'#ffdd44', r:12, pts:40,  msg:['自炊が最強！','外食は贅沢…','節約！節約！'] },
  { type:'point',   emoji:'🪙', label:'ポイント還元', color:'#44ddff', r:12, pts:60,  msg:['2%還元！','ポイ活民！','実質無料！'] },
  { type:'furusato',emoji:'📦', label:'ふるさと納税', color:'#ff88cc', r:13, pts:80,  msg:['制度の抜け穴！','庶民の知恵！','牛肉ゲット！'] },
];

canvas.addEventListener('touchstart', e=>{ touchStartX=e.touches[0].clientX; getActx(); e.preventDefault(); },{passive:false});
canvas.addEventListener('touchmove', e=>{
  if (!state||touchStartX===null) return;
  const dx=e.touches[0].clientX-touchStartX;
  player.x=Math.max(player.w/2, Math.min(W-player.w/2, player.x+dx));
  touchStartX=e.touches[0].clientX;
  e.preventDefault();
},{passive:false});
document.addEventListener('keydown', e=>{ keys[e.key]=true; getActx(); });
document.addEventListener('keyup', e=>keys[e.key]=false);
startBtn.addEventListener('click', startGame);
saveBtn.addEventListener('click', ()=>{
  const name=nameInput.value.trim()||'名無し';
  saveRanking(name, pendingScore);
  pendingScore=null; nameWrap.style.display='none'; renderRanking();
});

// Background elements
const bgElements = [
  {x:20,  y:80,  text:'¥', size:60, alpha:0.04},
  {x:300, y:200, text:'税', size:80, alpha:0.04},
  {x:60,  y:350, text:'₀', size:50, alpha:0.03},
  {x:340, y:430, text:'¥', size:55, alpha:0.04},
  {x:180, y:480, text:'税', size:45, alpha:0.03},
];

const bgStars = Array.from({length:40}, ()=>({
  x:Math.random()*400, y:Math.random()*540,
  r:0.5+Math.random()*0.8, speed:0.15+Math.random()*0.3,
  opacity:0.06+Math.random()*0.12
}));

function startGame() {
  wallet=0; taxed=0; lives=3; level=1; frameCount=0; lastLevel=1;
  player={ x:W/2, y:H-65, w:38, h:38, speed:5.2, trail:[], invincible:0, shake:0 };
  objects=[]; particles=[]; floats=[];
  state='playing';
  overlay.classList.add('hidden');
  nameWrap.style.display='none';
  pendingScore=null;
  updateHUD();
  cancelAnimationFrame(animId);
  lastTime=null;
  stopBGM();
  startBGM();
  animId=requestAnimationFrame(loop);
}

function spawnObject() {
  const isEnemy = Math.random() < 0.65;
  const x = 22 + Math.random()*(W-44);
  const speed = (1.5 + level*0.35) * (0.75+Math.random()*0.55);

  if (isEnemy) {
    const pool = level >= 3 ? ENEMY_TYPES : ENEMY_TYPES.slice(0,3);
    const t = pool[Math.floor(Math.random()*pool.length)];
    objects.push({...t, x, y:-25, speed, angle:0, wobble:Math.random()*Math.PI*2, isEnemy:true});
  } else {
    const pool = level >= 2 ? GOOD_TYPES : GOOD_TYPES.slice(0,1);
    const t = pool[Math.floor(Math.random()*pool.length)];
    objects.push({...t, x, y:-25, speed:speed*0.82, angle:0, wobble:Math.random()*Math.PI*2, isEnemy:false});
  }
}

function spawnParticles(x, y, color, n, spd=3) {
  for (let i=0;i<n;i++) {
    const a=(Math.PI*2*i)/n+Math.random()*0.5, s=spd*(0.6+Math.random());
    particles.push({x, y, vx:Math.cos(a)*s, vy:Math.sin(a)*s, life:1, color, r:2+Math.random()*2});
  }
}

function addFloat(x, y, text, color, bg=null) {
  floats.push({x, y, text, color, bg, life:1, vy:-1.4});
}

const MESSAGES = [
  '増税反対！', '給料上がらん！', '物価だけ上がる…', '選挙行こ…', 'なんで俺だけ！',
  '政治家よ聞いてるか！', '消費税どこいった！', '年金大丈夫？', 'ふるさと納税しかない'
];

function loop(ts) {
  if (!lastTime) lastTime=ts;
  const dt=Math.min((ts-lastTime)/16.67, 3);
  lastTime=ts; frameCount++;

  if (keys['ArrowLeft']||keys['a']) player.x-=player.speed*dt;
  if (keys['ArrowRight']||keys['d']) player.x+=player.speed*dt;
  player.x=Math.max(player.w/2, Math.min(W-player.w/2, player.x));
  if (player.invincible>0) player.invincible-=dt;
  if (player.shake>0) player.shake-=dt;

  player.trail.unshift({x:player.x, y:player.y});
  if (player.trail.length>12) player.trail.pop();

  const spawnRate=Math.max(20, 50-level*3.5);
  if (frameCount%Math.round(spawnRate)===0) spawnObject();

  const newLevel=1+Math.floor(wallet/500);
  if (newLevel!==lastLevel) {
    lastLevel=newLevel; level=newLevel;
    playLevelUp();
    addFloat(W/2, H/2-30, `圧力レベル${level}！`, '#ff9900');
    // Satirical level messages
    const msgs=['','物価上昇中…','インフレ加速！','給付金打ち切り','増税ラッシュ！','もう逃げ場なし'];
    if (msgs[level]) addFloat(W/2, H/2+10, msgs[level], '#e8002d');
  }
  levelEl.textContent=`LV${level}`;

  bgStars.forEach(s=>{ s.y+=s.speed*dt; if(s.y>H) s.y=-2; });

  for (let i=objects.length-1; i>=0; i--) {
    const o=objects[i];
    o.y+=o.speed*dt;
    o.angle+=0.05*dt;
    o.wobble+=0.04*dt;
    if (!o.isEnemy) o.x+=Math.sin(o.wobble)*0.7;

    if (!o.isEnemy) {
      const dx=o.x-player.x, dy=o.y-player.y;
      if (Math.sqrt(dx*dx+dy*dy)<o.r+17) {
        wallet+=o.pts;
        playCoin();
        spawnParticles(o.x, o.y, o.color, 9, 3.5);
        addFloat(o.x, o.y-20, `+¥${o.pts}`, o.color);
        addFloat(o.x, o.y-40, o.msg[Math.floor(Math.random()*o.msg.length)], 'rgba(255,255,255,0.6)');
        objects.splice(i,1);
        updateHUD();
        continue;
      }
    }

    if (o.isEnemy && player.invincible<=0) {
      const dx=o.x-player.x, dy=o.y-player.y;
      if (Math.sqrt(dx*dx+dy*dy)<o.r+15) {
        const taken=Math.min(wallet, 100+level*30);
        wallet=Math.max(0, wallet-taken);
        taxed+=taken;
        lives--;
        player.invincible=100; player.shake=25;
        updateHUD();
        playTax();
        spawnParticles(player.x, player.y, '#e8002d', 14, 5);
        addFloat(player.x, player.y-25, `-¥${taken}`, '#ffffff', 'rgba(220,0,40,0.85)');
        addFloat(player.x, player.y-50, o.msg[Math.floor(Math.random()*o.msg.length)], '#ffee44', 'rgba(100,40,0,0.85)');
        if (Math.random()<0.3) addFloat(player.x, player.y-75, MESSAGES[Math.floor(Math.random()*MESSAGES.length)], '#ffffff', 'rgba(0,0,0,0.75)');
        objects.splice(i,1);
        if (lives<=0) { gameOver(); return; }
        continue;
      }
    }

    if (o.y>H+25) {
      if (!o.isEnemy) { taxed+=o.pts*0.1; } // "missed subsidy"
      objects.splice(i,1);
    }
  }

  draw();
  animId=requestAnimationFrame(loop);
}

function draw() {
  ctx.save();
  if (player.shake>0) {
    ctx.translate((Math.random()-0.5)*6*(player.shake/25), (Math.random()-0.5)*3*(player.shake/25));
  }
  ctx.clearRect(-10,-10,W+20,H+20);

  // BG texture
  bgElements.forEach(e=>{
    ctx.save();
    ctx.font=`${e.size}px 'Dela Gothic One', sans-serif`;
    ctx.fillStyle=`rgba(212,160,23,${e.alpha})`;
    ctx.fillText(e.text, e.x, e.y);
    ctx.restore();
  });

  // BG stars (money rain effect — tiny ¥ marks)
  bgStars.forEach(s=>{
    ctx.globalAlpha=s.opacity;
    ctx.fillStyle='#d4a017';
    ctx.font=`${s.r*8}px serif`;
    ctx.fillText('¥', s.x, s.y);
  });
  ctx.globalAlpha=1;

  // Horizontal lines (ledger paper feel)
  ctx.strokeStyle='rgba(212,160,23,0.05)';
  ctx.lineWidth=1;
  for (let y=0;y<H;y+=20) {
    ctx.beginPath(); ctx.moveTo(0,y); ctx.lineTo(W,y); ctx.stroke();
  }

  // Particles
  for (let i=particles.length-1; i>=0; i--) {
    const p=particles[i];
    p.x+=p.vx; p.y+=p.vy; p.vx*=0.91; p.vy*=0.91; p.life-=0.035;
    if (p.life<=0) { particles.splice(i,1); continue; }
    ctx.save(); ctx.globalAlpha=p.life;
    ctx.fillStyle=p.color; ctx.shadowColor=p.color; ctx.shadowBlur=8;
    ctx.beginPath(); ctx.arc(p.x,p.y,p.r*p.life,0,Math.PI*2); ctx.fill();
    ctx.restore();
  }

  // Floating texts
  for (let i=floats.length-1; i>=0; i--) {
    const t=floats[i];
    t.y+=t.vy; t.life-=0.018;
    if (t.life<=0) { floats.splice(i,1); continue; }
    ctx.save();
    ctx.globalAlpha=t.life;
    ctx.font=`bold 12px 'Dela Gothic One', sans-serif`;
    ctx.textAlign='center'; ctx.textBaseline='middle';
    // 背景ピル
    const tw = ctx.measureText(t.text).width;
    const px=t.x-(tw/2+5), py=t.y-8, pw=tw+10, ph=16;
    ctx.fillStyle= t.bg || 'rgba(0,0,0,0.72)';
    ctx.beginPath(); ctx.roundRect(px, py, pw, ph, 4); ctx.fill();
    // テキスト
    ctx.fillStyle=t.color;
    ctx.shadowColor=t.color; ctx.shadowBlur=8;
    ctx.fillText(t.text, t.x, t.y);
    ctx.restore();
  }

  // Objects
  for (const o of objects) {
    ctx.save();
    ctx.translate(o.x, o.y);

    if (o.isEnemy) {
      // Warning glow
      const pulse=0.5+0.5*Math.sin(frameCount*0.15+o.wobble);
      ctx.beginPath(); ctx.arc(0,0,o.r+8,0,Math.PI*2);
      ctx.fillStyle=`rgba(${o.color.replace('#','').match(/../g).map(x=>parseInt(x,16)).join(',')},${0.12*pulse})`;
      ctx.fill();

      // Spinning ring
      ctx.rotate(o.angle);
      ctx.strokeStyle=o.color; ctx.lineWidth=2; ctx.globalAlpha=0.5;
      ctx.beginPath(); ctx.arc(0,0,o.r+2,0,Math.PI*2); ctx.stroke();
      ctx.globalAlpha=1; ctx.rotate(-o.angle);

      // Emoji
      ctx.font=`${o.r*1.5}px serif`;
      ctx.textAlign='center'; ctx.textBaseline='middle';
      ctx.shadowColor=o.color; ctx.shadowBlur=15;
      ctx.fillText(o.emoji, 0, 1);

      // Label below — pill background
      ctx.shadowBlur=0;
      ctx.font=`bold 7px 'Share Tech Mono', monospace`;
      ctx.textAlign='center'; ctx.textBaseline='middle';
      const ew = ctx.measureText(o.label).width;
      const lx=-(ew/2+3), ly=o.r+4, lw=ew+6, lh=11;
      ctx.fillStyle='rgba(0,0,0,0.8)';
      ctx.beginPath(); ctx.roundRect(lx, ly, lw, lh, 2); ctx.fill();
      ctx.fillStyle='#ffffff';
      ctx.fillText(o.label, 0, ly+lh/2);

    } else {
      // Good item glow ring
      const pulse=0.7+0.3*Math.sin(frameCount*0.12+o.wobble);
      ctx.strokeStyle=`rgba(${o.color.replace('#','').match(/../g).map(x=>parseInt(x,16)).join(',')},${0.35*pulse})`;
      ctx.lineWidth=2; ctx.shadowColor=o.color; ctx.shadowBlur=12*pulse;
      ctx.beginPath(); ctx.arc(0,0,o.r+5,0,Math.PI*2); ctx.stroke();

      ctx.font=`${o.r*2}px serif`;
      ctx.textAlign='center'; ctx.textBaseline='middle';
      ctx.fillText(o.emoji, 0, 1);

      // Label below — pill background
      ctx.shadowBlur=0;
      ctx.font=`bold 7px 'Share Tech Mono', monospace`;
      const gw = ctx.measureText(o.label).width;
      const glx=-(gw/2+3), gly=o.r+4, glw=gw+6, glh=11;
      ctx.fillStyle='rgba(0,0,0,0.8)';
      ctx.beginPath(); ctx.roundRect(glx, gly, glw, glh, 2); ctx.fill();
      ctx.fillStyle='#ffffff';
      ctx.fillText(o.label, 0, gly+glh/2);
    }
    ctx.restore();
  }

  // Player trail
  for (let i=player.trail.length-1; i>=0; i--) {
    const t=player.trail[i];
    const alpha=(1-i/player.trail.length)*0.15;
    ctx.save(); ctx.globalAlpha=alpha;
    ctx.fillStyle='#44ff88'; ctx.shadowColor='#44ff88'; ctx.shadowBlur=6;
    ctx.beginPath(); ctx.arc(t.x, t.y+10, (1-i/player.trail.length)*7, 0, Math.PI*2); ctx.fill();
    ctx.restore();
  }

  // Player — 庶民キャラ
  ctx.save();
  ctx.translate(player.x, player.y);
  const blink=player.invincible>0 && Math.floor(player.invincible/6)%2===0;

  if (!blink) {
    // Shadow
    ctx.fillStyle='rgba(0,0,0,0.3)';
    ctx.beginPath(); ctx.ellipse(2, 22, 14, 5, 0, 0, Math.PI*2); ctx.fill();

    // Body (salaryman shape)
    ctx.fillStyle='#334466';
    ctx.shadowColor='#44ff88'; ctx.shadowBlur=12;
    // Legs
    ctx.fillRect(-7, 10, 6, 12);
    ctx.fillRect(1, 10, 6, 12);
    // Body
    ctx.fillStyle='#2255aa';
    ctx.fillRect(-10, -5, 20, 16);
    // Tie
    ctx.fillStyle='#e8002d';
    ctx.beginPath(); ctx.moveTo(0,-4); ctx.lineTo(3,6); ctx.lineTo(0,8); ctx.lineTo(-3,6); ctx.closePath(); ctx.fill();
    // Head
    ctx.fillStyle='#ffcc99';
    ctx.shadowColor='#44ff88'; ctx.shadowBlur=8;
    ctx.beginPath(); ctx.arc(0,-13, 9, 0, Math.PI*2); ctx.fill();
    // Hair
    ctx.fillStyle='#332200';
    ctx.beginPath(); ctx.arc(0,-18, 8, Math.PI, 0); ctx.fill();
    // Eyes (worried)
    ctx.fillStyle='#333';
    ctx.beginPath(); ctx.arc(-3,-14,1.5,0,Math.PI*2); ctx.fill();
    ctx.beginPath(); ctx.arc(3,-14,1.5,0,Math.PI*2); ctx.fill();
    // Sweat drop
    ctx.fillStyle='rgba(100,180,255,0.7)';
    ctx.beginPath(); ctx.arc(9,-10,2,0,Math.PI*2); ctx.fill();
    // Briefcase
    ctx.fillStyle='#8b6914';
    ctx.fillRect(11, 2, 8, 7);
    ctx.strokeStyle='#6b4a0a'; ctx.lineWidth=1;
    ctx.strokeRect(11,2,8,7);
    ctx.fillRect(13,0,4,3);
    // Protest sign (tiny)
    if (Math.floor(frameCount/30)%2===0) {
      ctx.fillStyle='#fff8e1';
      ctx.fillRect(-22, -18, 16, 10);
      ctx.fillStyle='#e8002d';
      ctx.font='bold 5px sans-serif'; ctx.textAlign='center';
      ctx.fillText('増税反対', -14, -10);
      ctx.strokeStyle='#8b6914'; ctx.lineWidth=1;
      ctx.beginPath(); ctx.moveTo(-14,-8); ctx.lineTo(-14,5); ctx.stroke();
    }
    ctx.shadowBlur=0;
  }
  ctx.restore();

  // Bottom border
  ctx.strokeStyle='rgba(212,160,23,0.15)';
  ctx.lineWidth=1;
  ctx.beginPath(); ctx.moveTo(0,H-28); ctx.lineTo(W,H-28); ctx.stroke();

  // Wallet bar
  const maxWallet=1000;
  const barW=Math.min(wallet/maxWallet, 1)*(W-40);
  ctx.fillStyle='rgba(68,255,136,0.1)'; ctx.fillRect(20,H-22,W-40,5);
  if (barW>0) {
    ctx.fillStyle='#44ff88'; ctx.shadowColor='#44ff88'; ctx.shadowBlur=6;
    ctx.fillRect(20,H-22,barW,5);
  }
  ctx.shadowBlur=0;

  ctx.restore(); // end shake
}

function updateHUD() {
  walletEl.textContent=`¥${wallet.toLocaleString()}`;
  taxEl.textContent=`¥${taxed.toLocaleString()}`;
  livesEl.textContent='💴'.repeat(Math.max(0,lives))+'🈳'.repeat(Math.max(0,3-lives));
}

function gameOver() {
  state=null;
  cancelAnimationFrame(animId);
  stopBGM();
  playGameOver();

  const ratio = taxed>0 ? Math.round(taxed/(wallet+taxed)*100) : 0;
  const ending = ratio>60 ? '完全に搾り取られました…' : ratio>30 ? 'まあまあ生き延びた' : '上手く逃げ切った！';

  olTitle.textContent='💸 ゲームオーバー';
  olSub.textContent=`お財布: ¥${wallet.toLocaleString()} / 徴収: ¥${taxed.toLocaleString()}\n徴収率 ${ratio}% — ${ending}`;
  olScore.textContent=`スコア: ¥${wallet.toLocaleString()}`;

  if (wallet>0) {
    pendingScore=wallet;
    nameWrap.style.display='flex';
    nameInput.value=''; nameInput.focus();
  }
  startBtn.textContent='もう一度逃げる';
  renderRanking(wallet);
  overlay.classList.remove('hidden');
}

function renderRanking(currentScore) {
  const rankings=loadRankings();
  const list=document.getElementById('ranking-list');
  if (!rankings.length) { list.innerHTML='<div class="empty-rank">まだ記録がありません</div>'; return; }
  const medals=['gold','silver','bronze'];
  const medalEmoji=['🥇','🥈','🥉'];
  list.innerHTML=rankings.map((r,i)=>{
    const isNew=currentScore!=null && r.score===currentScore;
    const numClass=medals[i]||'';
    const numLabel=medalEmoji[i]||(i+1)+'位';
    return `<div class="rank-row${isNew?' highlight':''}">
      <span class="rank-num ${numClass}">${numLabel}</span>
      <span class="rank-name">${r.name}</span>
      <span class="rank-score">¥${r.score.toLocaleString()}</span>
      <span class="rank-date">${r.date}</span>
    </div>`;
  }).join('');
}

// Init
olTitle.textContent='💸 税金RUSH';
olSub.textContent='給付金💴を拾い、税務署👮・増税💰・\n天下り👔を避けて生き残れ！';
olScore.textContent='';
nameWrap.style.display='none';
renderRanking();
</script>

</body>
</html>
