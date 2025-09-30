<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Green Light — Red Light (Three.js)</title>
<style>
  html,body { height:100%; margin:0; background:#0b1220; color:#eee; font-family: Arial, Helvetica, sans-serif; }
  #game {
    display:block;
    width:100%;
    height:100vh;
  }
  .ui {
    position: absolute;
    left: 16px;
    top: 16px;
    z-index: 10;
    user-select: none;
  }
  .ui .title { font-weight:700; font-size:18px; color:#88ce02; letter-spacing:1px; }
  .ui .controls { margin-top:8px; font-size:13px; opacity:0.9; }
  .status {
    position:absolute;
    right:16px;
    top:16px;
    z-index:10;
    background: rgba(0,0,0,0.35);
    padding:10px 14px;
    border-radius:8px;
    text-align:center;
    font-weight:700;
    color:#fff;
    min-width:120px;
    box-shadow: 0 6px 18px rgba(0,0,0,0.6);
  }
  .status .light {
    display:block;
    height:12px;
    width:12px;
    border-radius:50%;
    margin:0 auto 8px auto;
    box-shadow: 0 2px 6px rgba(0,0,0,0.6);
  }
  .footer {
    position:absolute;
    left:50%;
    transform:translateX(-50%);
    bottom:16px;
    z-index:10;
    color:#ccc;
    font-size:13px;
  }
  button {
    background:#121823;
    color:#88ce02;
    border:1px solid rgba(136,206,2,0.12);
    padding:8px 12px;
    border-radius:6px;
    cursor:pointer;
    font-weight:700;
  }
  button:active{ transform:translateY(1px); }
  #overlay {
    position:absolute;
    inset:0;
    display:flex;
    align-items:center;
    justify-content:center;
    background:linear-gradient(180deg, rgba(0,0,0,0.4), rgba(0,0,0,0.7));
    z-index:20;
  }
  #overlay .panel {
    background:linear-gradient(180deg,#081018,#0f1622);
    padding:24px;
    border-radius:12px;
    text-align:center;
    box-shadow:0 10px 40px rgba(0,0,0,0.7);
  }
  #overlay h1 { margin:0 0 8px 0; color:#88ce02; }
  #overlay p { margin:8px 0 18px 0; color:#cfd8d8; }
</style>
</head>
<body>
<canvas id="game"></canvas>

<div class="ui">
  <div class="title">RIALO — Green Light / Red Light</div>
  <div class="controls">Hold / Tap to move forward. (W / ↑ works too)</div>
</div>

<div class="status" id="statusBox">
  <div class="light" id="lightDot" style="background:#999;"></div>
  <div id="phaseText">Ready</div>
  <div style="font-size:12px; margin-top:8px;" id="timerText">--</div>
</div>

<div class="footer">Reach the finish line to win</div>

<div id="overlay">
  <div class="panel">
    <h1>Green Light — Red Light</h1>
    <p>Hold or tap to move while the guard looks away (green). Move during red and you lose.</p>
    <div style="display:flex;gap:8px;justify-content:center">
      <button id="startBtn">Start Game</button>
      <button id="easyBtn">Easy</button>
      <button id="hardBtn">Hard</button>
    </div>
  </div>
</div>

<script type="module">
// Import three via CDN (module). Use dynamic import so this single file works offline-ish.
import * as THREE from 'https://unpkg.com/three@0.152.2/build/three.module.js';

let canvas = document.getElementById('game');
let renderer = new THREE.WebGLRenderer({ canvas, antialias: true });
renderer.setSize(window.innerWidth, window.innerHeight);
renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
document.body.appendChild(renderer.domElement);

const scene = new THREE.Scene();
scene.fog = new THREE.FogExp2(0x0b1220, 0.002);

// camera
const camera = new THREE.PerspectiveCamera(55, window.innerWidth/window.innerHeight, 0.1, 2000);
camera.position.set(0, 18, 28);
camera.lookAt(0, 8, 0);

// lights
const hemi = new THREE.HemisphereLight(0xbde0b4, 0x080820, 0.8);
scene.add(hemi);
const dir = new THREE.DirectionalLight(0xffffff, 0.7);
dir.position.set(-10,40,20);
scene.add(dir);

// ground
const groundGeo = new THREE.PlaneGeometry(140, 60);
const groundMat = new THREE.MeshStandardMaterial({ color: 0x223338, roughness:0.9, metalness:0.02 });
const ground = new THREE.Mesh(groundGeo, groundMat);
ground.rotation.x = -Math.PI/2;
ground.position.y = 0;
scene.add(ground);

// lanes (visual)
function makeLane(x, color){
  const g = new THREE.BoxGeometry(40, 0.2, 6);
  const m = new THREE.MeshStandardMaterial({ color, roughness:0.9 });
  const mesh = new THREE.Mesh(g,m);
  mesh.position.set(x, 0.05, 0);
  scene.add(mesh);
}
makeLane(-40, 0x1a2a2a); // left
makeLane(40, 0x1a2a2a);  // right

// start & finish visuals
const startGroup = new THREE.Group();
const startMat = new THREE.MeshStandardMaterial({ color:0x88ce02 });
const startMesh = new THREE.Mesh(new THREE.BoxGeometry(8,0.2,18), startMat);
startMesh.position.set(-40,0.101,0);
scene.add(startMesh);
const finishMesh = new THREE.Mesh(new THREE.BoxGeometry(8,0.2,18), new THREE.MeshStandardMaterial({color:0xff3b30}));
finishMesh.position.set(52,0.101,0);
scene.add(finishMesh);

// guard (simple robot with a head that turns)
const guard = new THREE.Group();
// body
const body = new THREE.Mesh(new THREE.BoxGeometry(6,10,3), new THREE.MeshStandardMaterial({color:0x0f6a3a}));
body.position.y = 8;
guard.add(body);
// neck
const neck = new THREE.Mesh(new THREE.CylinderGeometry(0.9,0.9,1.6), new THREE.MeshStandardMaterial({color:0x333}));
neck.position.y = 12.2;
guard.add(neck);
// head
const head = new THREE.Mesh(new THREE.BoxGeometry(6,4,4), new THREE.MeshStandardMaterial({color:0xf7f3f1}));
head.position.y = 15;
guard.add(head);
// eyes as black plane
const eyeGeo = new THREE.PlaneGeometry(2.6,0.6);
const eyeMat = new THREE.MeshBasicMaterial({color:0x000});
const leftEye = new THREE.Mesh(eyeGeo, eyeMat);
leftEye.position.set(-1.2,15,2.01);
guard.add(leftEye);
const rightEye = new THREE.Mesh(eyeGeo, eyeMat);
rightEye.position.set(1.2,15,2.01);
guard.add(rightEye);

guard.position.set(0,0, -18);
scene.add(guard);

// small decorative doll/face texture alternative omitted for simplicity

// player — simple capsule-ish: sphere + cylinder
const player = new THREE.Group();
const pMat = new THREE.MeshStandardMaterial({ color:0x88d2ff, roughness:0.6 });
const bodySphere = new THREE.Mesh(new THREE.SphereGeometry(1.6, 24, 20), pMat);
bodySphere.position.y = 1.85;
player.add(bodySphere);
const bodyBottom = new THREE.Mesh(new THREE.CylinderGeometry(1.08,1.08,1.6,16), pMat);
bodyBottom.position.y = 0.6;
player.add(bodyBottom);
player.position.set(-44, 0, 0);
scene.add(player);

// camera follow settings
let cameraOffset = new THREE.Vector3(0, 12, 20);

// game state
let phase = 'idle'; // 'idle' | 'green' | 'red' | 'ended'
let phaseTime = 0;
let phaseDuration = 0;
let score = 0;
let eliminated = false;
let win = false;

// settings (difficulty)
let minGreen = 2.0, maxGreen = 4.0, minRed = 1.2, maxRed = 3.0;
let moveSpeed = 0.12; // units per frame (adjusted by delta)

// input state
let moving = false; // user is holding input to move

// UI refs
const overlay = document.getElementById('overlay');
const startBtn = document.getElementById('startBtn');
const easyBtn = document.getElementById('easyBtn');
const hardBtn = document.getElementById('hardBtn');
const lightDot = document.getElementById('lightDot');
const phaseText = document.getElementById('phaseText');
const timerText = document.getElementById('timerText');

// sound via WebAudio (synth)
const audioCtx = new (window.AudioContext || window.webkitAudioContext)();

function beep(freq, time=0.08, type='sine', gain=0.18){
  const now = audioCtx.currentTime;
  const o = audioCtx.createOscillator();
  const g = audioCtx.createGain();
  o.type = type;
  o.frequency.value = freq;
  g.gain.setValueAtTime(gain, now);
  o.connect(g);
  g.connect(audioCtx.destination);
  o.start(now);
  g.gain.exponentialRampToValueAtTime(0.0001, now + time);
  o.stop(now + time + 0.02);
}
function mixedBell(){ beep(880,0.18,'sine',0.18); beep(1320,0.18,'triangle',0.12); }
function warnTone(){ beep(220,0.12,'sine',0.22); }

// manage phases with randomized durations
function nextPhase(){
  if(eliminated || win) return;
  if(phase === 'idle' || phase === 'red'){
    // become green (guard looks away)
    phase = 'green';
    phaseDuration = minGreen + Math.random() * (maxGreen - minGreen);
    phaseTime = 0;
    phaseText.textContent = 'GREEN';
    lightDot.style.background = '#88ce02';
    mixedBell();
    // rotate guard to look away (turn its head 180deg over short time)
    TweenMax.to(guard.rotation, 0.75, { y: Math.PI, ease: Power1.easeInOut });
  } else {
    // become red (guard faces forward)
    phase = 'red';
    phaseDuration = minRed + Math.random() * (maxRed - minRed);
    phaseTime = 0;
    phaseText.textContent = 'RED';
    lightDot.style.background = '#ff3b30';
    warnTone();
    TweenMax.to(guard.rotation, 0.25, { y: 0, ease: Power1.easeInOut });
  }
}

// start game
function startGame(){
  // reset state
  overlay.style.display = 'none';
  player.position.set(-44, 0, 0);
  eliminated = false;
  win = false;
  score = 0;
  phase = 'idle';
  phaseText.textContent = 'Get Ready';
  lightDot.style.background = '#999';
  nextPhase();
}

// easy / hard buttons
easyBtn.addEventListener('click', function(){
  minGreen = 3; maxGreen = 4.5; minRed = 1.5; maxRed = 2.8; moveSpeed = 0.10;
});
hardBtn.addEventListener('click', function(){
  minGreen = 1.4; maxGreen = 3.2; minRed = 1.0; maxRed = 2.0; moveSpeed = 0.145;
});
startBtn.addEventListener('click', function(){
  // unlock audio on iOS / mobile
  if(audioCtx.state === 'suspended'){ audioCtx.resume(); }
  startGame();
});

// input handling: keyboard & pointer/touch
window.addEventListener('keydown', (e) => {
  if(e.key === 'w' || e.key === 'ArrowUp') moving = true;
});
window.addEventListener('keyup', (e) => {
  if(e.key === 'w' || e.key === 'ArrowUp') moving = false;
});

// pointer/touch: press anywhere to move; release to stop
let pointerDown = false;
window.addEventListener('pointerdown', (e)=> {
  // ignore clicks on UI buttons
  if(e.target.closest('button')) return;
  pointerDown = true;
  moving = true;
});
window.addEventListener('pointerup', (e)=> { pointerDown = false; moving = false; });

// movement and detection logic
function updateMovement(delta){
  if(eliminated || win) return;
  if(moving){
    // move along +x axis toward finish
    player.position.x += moveSpeed * delta * 60; // scale by frame delta
    // small bob
    player.position.y = Math.sin(Date.now() * 0.01) * 0.02 + 0.0;
  }
  // camera follow
  const desiredCamX = player.position.x + cameraOffset.x;
  camera.position.x += (desiredCamX - camera.position.x) * 0.08;
  camera.position.z += ((player.position.z + cameraOffset.z) - camera.position.z) * 0.06;
  camera.position.y += ((player.position.y + cameraOffset.y) - camera.position.y) * 0.06;
  camera.lookAt(player.position.x + 6, player.position.y + 4, player.position.z);

  // if moving during red -> eliminated
  if(phase === 'red' && moving){
    // small tolerance to avoid micro movement from bobbing: require distance moved above threshold
    eliminated = true;
    phase = 'ended';
    phaseText.textContent = 'ELIMINATED';
    lightDot.style.background = '#111';
    beep(120,0.18,'sine',0.22);
    beep(70,0.25,'sine',0.22);
    // show head-on spin & fall (visual)
    TweenMax.to(player.rotation, 0.6, { x: Math.PI*0.4, ease: Back.easeOut });
    // overlay show
    setTimeout(()=> {
      alert('Eliminated! You moved during RED light.');
      overlay.style.display = 'flex';
    }, 600);
    return;
  }

  // check win condition
  if(player.position.x >= 52 && !win){
    win = true;
    phase = 'ended';
    phaseText.textContent = 'YOU WIN';
    lightDot.style.background = '#ffd24a';
    mixedBell();
    setTimeout(()=> {
      alert('You reached the finish line — Victory!');
      overlay.style.display = 'flex';
    }, 400);
  }
}

// animation loop
let lastTime = performance.now();
function animate(now){
  const delta = (now - lastTime) / 1000;
  lastTime = now;

  // phase timer
  if(phase === 'green' || phase === 'red'){
    phaseTime += delta;
    timerText.textContent = `${(phaseDuration - phaseTime).toFixed(1)}s`;
    if(phaseTime >= phaseDuration){
      nextPhase();
    }
  }

  // guard head subtle idle (when looking away, add slight bob)
  guard.children.forEach(child => { /* placeholder */ });

  // update movement & check
  updateMovement(delta);

  renderer.render(scene, camera);
  requestAnimationFrame(animate);
}
requestAnimationFrame(animate);

// resize
window.addEventListener('resize', ()=> {
  renderer.setSize(window.innerWidth, window.innerHeight);
  camera.aspect = window.innerWidth / window.innerHeight;
  camera.updateProjectionMatrix();
});

/* Minor UX: Show overlay when clicking start again if ended */
overlay.addEventListener('pointerdown', (e)=> {
  // do nothing; clicks handled by buttons
});

</script>
</body>
</html>
