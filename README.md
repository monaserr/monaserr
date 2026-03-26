<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>Mohamed Nasser · Web Developer</title>

<!-- Bracket favicon -->
<link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 32 32'><text y='26' font-size='26' font-family='monospace' fill='%23111'>&lt;/&gt;</text></svg>"/>

<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;700;800&display=swap" rel="stylesheet"/>

<style>
*{margin:0;padding:0;box-sizing:border-box}
:root{
  --bg:#f9f8f6;
  --ink:#0d0d0d;
  --muted:#999;
  --border:rgba(0,0,0,.07);
  --hover:rgba(0,0,0,.03);
}
html{scroll-behavior:smooth}
body{background:var(--bg);color:var(--ink);font-family:'Syne',sans-serif;overflow-x:hidden;cursor:none}

/* CURSOR */
#cur{position:fixed;width:10px;height:10px;background:var(--ink);border-radius:50%;pointer-events:none;z-index:9999;transform:translate(-50%,-50%);transition:width .2s,height .2s,background .2s}
#cur.big{width:36px;height:36px;background:rgba(0,0,0,.08);border:1px solid rgba(0,0,0,.15)}
#cur2{position:fixed;width:32px;height:32px;border:1px solid rgba(0,0,0,.12);border-radius:50%;pointer-events:none;z-index:9998;transform:translate(-50%,-50%);transition:left .1s ease,top .1s ease}

/* CANVAS */
#cv{position:fixed;inset:0;z-index:0;opacity:.18}

/* GRAIN overlay */
.grain{position:fixed;inset:0;z-index:2;pointer-events:none;opacity:.035;
  background-image:url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E")}

/* NAV */
nav{position:fixed;top:0;left:0;right:0;z-index:100;padding:26px 48px;display:flex;justify-content:space-between;align-items:center;background:rgba(249,248,246,.85);backdrop-filter:blur(12px);border-bottom:1px solid var(--border)}
.nav-logo{font-family:'Space Mono',monospace;font-size:14px;font-weight:700;letter-spacing:.04em;display:flex;align-items:center;gap:8px}
.nav-logo .bracket{color:var(--muted)}
.nav-links{display:flex;gap:32px}
.nav-links a{font-family:'Space Mono',monospace;font-size:11px;letter-spacing:.18em;text-transform:uppercase;color:var(--muted);text-decoration:none;transition:color .25s}
.nav-links a:hover{color:var(--ink)}

/* PAGE */
section{position:relative;z-index:10;max-width:900px;margin:0 auto;padding:0 48px}

/* HERO */
#hero{min-height:100vh;display:flex;flex-direction:column;justify-content:center;padding-top:90px}

.hero-eyebrow{font-family:'Space Mono',monospace;font-size:11px;letter-spacing:.22em;color:var(--muted);text-transform:uppercase;margin-bottom:28px;display:flex;align-items:center;gap:12px;opacity:0;animation:fadeUp .6s .1s forwards}
.hero-eyebrow::before{content:'<>';font-size:13px;color:var(--ink);font-weight:700}

.hero-name{font-size:clamp(54px,10vw,104px);font-weight:800;line-height:.93;letter-spacing:-.04em;margin-bottom:28px}
.hero-name .line{overflow:hidden;display:block}
.hero-name .line span{display:block;transform:translateY(110%);animation:slideUp .9s cubic-bezier(.16,1,.3,1) forwards}
.hero-name .line:nth-child(1) span{animation-delay:.08s}
.hero-name .line:nth-child(2) span{animation-delay:.17s;color:transparent;-webkit-text-stroke:1.5px rgba(0,0,0,.2)}

.hero-sub{font-size:16px;color:var(--muted);line-height:1.75;max-width:400px;margin-bottom:52px;opacity:0;animation:fadeUp .7s .5s forwards}

.hero-ctas{display:flex;gap:12px;flex-wrap:wrap;opacity:0;animation:fadeUp .7s .65s forwards}
.btn{font-family:'Space Mono',monospace;font-size:11px;letter-spacing:.14em;text-transform:uppercase;padding:13px 26px;text-decoration:none;transition:all .3s;position:relative;overflow:hidden;display:inline-block}
.btn-solid{background:var(--ink);color:#fff}
.btn-solid::before{content:'';position:absolute;inset:0;background:#333;transform:scaleX(0);transform-origin:left;transition:transform .35s cubic-bezier(.16,1,.3,1)}
.btn-solid:hover::before{transform:scaleX(1)}
.btn-solid span{position:relative;z-index:1}
.btn-outline{border:1px solid rgba(0,0,0,.15);color:var(--muted)}
.btn-outline:hover{color:var(--ink);border-color:rgba(0,0,0,.3)}

/* SCROLL HINT */
.scroll-ind{position:absolute;bottom:44px;left:48px;display:flex;align-items:center;gap:12px;font-family:'Space Mono',monospace;font-size:10px;letter-spacing:.18em;color:var(--muted);opacity:0;animation:fadeIn 1s 1.5s forwards}
.scroll-bar{width:1px;height:48px;background:linear-gradient(to bottom,var(--ink),transparent);animation:scrollDrop 2s ease-in-out infinite;opacity:.3}

/* DIVIDER */
.sep{max-width:900px;margin:0 auto;padding:0 48px}
.sep-line{height:1px;background:var(--border);margin:100px 0 80px}

/* SECTION LABEL */
.s-label{font-family:'Space Mono',monospace;font-size:10px;letter-spacing:.28em;color:var(--muted);text-transform:uppercase;margin-bottom:44px;display:flex;align-items:center;gap:12px}
.s-label::after{content:'';flex:1;height:1px;background:var(--border)}

/* STACK */
.stack-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(130px,1fr));gap:1px;background:var(--border);border:1px solid var(--border)}
.s-item{background:var(--bg);padding:20px 16px;display:flex;flex-direction:column;gap:6px;transition:background .25s;position:relative;overflow:hidden}
.s-item::after{content:'';position:absolute;bottom:0;left:0;width:100%;height:1.5px;background:var(--ink);transform:scaleX(0);transform-origin:left;transition:transform .4s cubic-bezier(.16,1,.3,1)}
.s-item:hover{background:rgba(0,0,0,.02)}
.s-item:hover::after{transform:scaleX(1)}
.s-cat{font-family:'Space Mono',monospace;font-size:9px;letter-spacing:.2em;color:var(--muted);text-transform:uppercase}
.s-name{font-size:15px;font-weight:700;color:var(--ink)}

/* STATS */
.stats-wrap{display:grid;grid-template-columns:1fr 1fr;gap:1px;background:var(--border);border:1px solid var(--border);margin-bottom:1px}
.stat-box{background:var(--bg);padding:32px 24px}
.stat-box img{width:100%;height:auto;display:block}
.streak-box{background:var(--bg);border:1px solid var(--border);padding:32px 24px}
.streak-box img{width:100%;height:auto;display:block}

/* CONNECT */
.connect-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:1px;background:var(--border);border:1px solid var(--border)}
.c-item{background:var(--bg);padding:32px 24px;text-decoration:none;display:flex;flex-direction:column;gap:10px;transition:background .25s}
.c-item:hover{background:rgba(0,0,0,.025)}
.c-platform{font-family:'Space Mono',monospace;font-size:9px;letter-spacing:.2em;color:var(--muted);text-transform:uppercase}
.c-handle{font-size:17px;font-weight:700;color:var(--ink)}
.c-arrow{font-size:18px;color:rgba(0,0,0,.2);margin-top:auto;transition:transform .3s,color .3s}
.c-item:hover .c-arrow{transform:translate(4px,-4px);color:var(--ink)}

/* FOOTER */
footer{position:relative;z-index:10;max-width:900px;margin:0 auto;padding:36px 48px 60px;display:flex;justify-content:space-between;align-items:center;border-top:1px solid var(--border);flex-wrap:wrap;gap:12px}
.f-name{font-weight:800;font-size:15px;display:flex;align-items:center;gap:8px}
.f-name .bracket{color:var(--muted);font-family:'Space Mono',monospace;font-size:13px}
.f-meta{font-family:'Space Mono',monospace;font-size:10px;color:var(--muted);letter-spacing:.1em}

/* REVEAL */
.rv{opacity:0;transform:translateY(24px);transition:opacity .8s ease,transform .8s ease}
.rv.on{opacity:1;transform:none}

@keyframes slideUp{to{transform:translateY(0)}}
@keyframes fadeUp{from{opacity:0;transform:translateY(14px)}to{opacity:1;transform:none}}
@keyframes fadeIn{to{opacity:1}}
@keyframes scrollDrop{0%,100%{opacity:.2}50%{opacity:.6}}

@media(max-width:640px){
  nav{padding:20px 24px}
  section,.sep{padding:0 24px}
  .stats-wrap,.connect-grid{grid-template-columns:1fr}
  footer{padding:32px 24px 48px}
}
</style>
</head>
<body>

<div id="cur"></div>
<div id="cur2"></div>
<canvas id="cv"></canvas>
<div class="grain"></div>

<!-- NAV -->
<nav>
  <div class="nav-logo">
    <span class="bracket">&lt;</span>MN<span class="bracket">/&gt;</span>
  </div>
  <div class="nav-links">
    <a href="#stack">Stack</a>
    <a href="#stats">Stats</a>
    <a href="#connect">Connect</a>
  </div>
</nav>

<!-- HERO -->
<section id="hero">
  <div class="hero-eyebrow">Available for collaborations</div>
  <h1 class="hero-name">
    <span class="line"><span>Mohamed</span></span>
    <span class="line"><span>Nasser</span></span>
  </h1>
  <p class="hero-sub">Web Developer · Computing & Bioinformatics Student<br/>Building things where code meets biology.</p>
  <div class="hero-ctas">
    <a class="btn btn-solid" href="https://github.com/monaserr" target="_blank"><span>GitHub ↗</span></a>
    <a class="btn btn-outline" href="https://www.linkedin.com/in/mohamed-nasser-9588a533b" target="_blank"><span>LinkedIn ↗</span></a>
    <a class="btn btn-outline" href="https://wa.me/qr/QRX3RHEVJUXXO1" target="_blank"><span>WhatsApp →</span></a>
  </div>
  <div class="scroll-ind">
    <div class="scroll-bar"></div>
    scroll
  </div>
</section>

<div class="sep"><div class="sep-line"></div></div>

<!-- STACK -->
<section id="stack" class="rv">
  <div class="s-label">Tech Stack</div>
  <div class="stack-grid">
    <div class="s-item"><span class="s-cat">Frontend</span><span class="s-name">React</span></div>
    <div class="s-item"><span class="s-cat">Frontend</span><span class="s-name">Next.js</span></div>
    <div class="s-item"><span class="s-cat">Frontend</span><span class="s-name">TypeScript</span></div>
    <div class="s-item"><span class="s-cat">Frontend</span><span class="s-name">Tailwind</span></div>
    <div class="s-item"><span class="s-cat">Frontend</span><span class="s-name">HTML / CSS</span></div>
    <div class="s-item"><span class="s-cat">Backend</span><span class="s-name">Node.js</span></div>
    <div class="s-item"><span class="s-cat">Backend</span><span class="s-name">Python</span></div>
    <div class="s-item"><span class="s-cat">Backend</span><span class="s-name">Express</span></div>
    <div class="s-item"><span class="s-cat">Bio</span><span class="s-name">Biopython</span></div>
    <div class="s-item"><span class="s-cat">Bio</span><span class="s-name">Pandas</span></div>
    <div class="s-item"><span class="s-cat">Bio</span><span class="s-name">Jupyter</span></div>
    <div class="s-item"><span class="s-cat">Tools</span><span class="s-name">Git / Linux</span></div>
  </div>
</section>

<div class="sep"><div class="sep-line"></div></div>

<!-- STATS -->
<section id="stats" class="rv">
  <div class="s-label">GitHub Stats</div>
  <div class="stats-wrap">
    <div class="stat-box">
      <img src="https://github-readme-stats.vercel.app/api?username=monaserr&show_icons=true&theme=default&hide_border=true&bg_color=00000000&title_color=0d0d0d&icon_color=0d0d0d&text_color=888888&include_all_commits=true&count_private=true" alt="GitHub Stats"/>
    </div>
    <div class="stat-box">
      <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=monaserr&layout=compact&theme=default&hide_border=true&bg_color=00000000&title_color=0d0d0d&text_color=888888&langs_count=6" alt="Top Languages"/>
    </div>
  </div>
  <div class="streak-box">
    <img src="https://github-readme-streak-stats.herokuapp.com/?user=monaserr&theme=default&hide_border=true&background=00000000&ring=0d0d0d&fire=0d0d0d&currStreakLabel=0d0d0d&sideLabels=999&dates=bbb" alt="Streak"/>
  </div>
</section>

<div class="sep"><div class="sep-line"></div></div>

<!-- CONNECT -->
<section id="connect" class="rv" style="padding-bottom:0">
  <div class="s-label">Connect</div>
  <div class="connect-grid">
    <a class="c-item" href="https://github.com/monaserr" target="_blank">
      <span class="c-platform">GitHub</span>
      <span class="c-handle">monaserr</span>
      <span class="c-arrow">↗</span>
    </a>
    <a class="c-item" href="https://www.linkedin.com/in/mohamed-nasser-9588a533b" target="_blank">
      <span class="c-platform">LinkedIn</span>
      <span class="c-handle">Mohamed Nasser</span>
      <span class="c-arrow">↗</span>
    </a>
    <a class="c-item" href="https://wa.me/qr/QRX3RHEVJUXXO1" target="_blank">
      <span class="c-platform">WhatsApp</span>
      <span class="c-handle">Chat with me</span>
      <span class="c-arrow">↗</span>
    </a>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="f-name">
    <span class="bracket">&lt;</span>Mohamed Nasser<span class="bracket">/&gt;</span>
  </div>
  <div class="f-meta">Computing & Bioinformatics · Egypt 🇪🇬 · 2025</div>
</footer>

<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script>
// Cursor
const cur=document.getElementById('cur'),cur2=document.getElementById('cur2');
document.addEventListener('mousemove',e=>{
  cur.style.left=e.clientX+'px';cur.style.top=e.clientY+'px';
  setTimeout(()=>{cur2.style.left=e.clientX+'px';cur2.style.top=e.clientY+'px';},90);
});
document.querySelectorAll('a,.s-item,.c-item').forEach(el=>{
  el.addEventListener('mouseenter',()=>cur.classList.add('big'));
  el.addEventListener('mouseleave',()=>cur.classList.remove('big'));
});

// Three.js — light particles on white bg
const canvas=document.getElementById('cv');
const renderer=new THREE.WebGLRenderer({canvas,alpha:true,antialias:true});
renderer.setPixelRatio(Math.min(devicePixelRatio,2));
renderer.setSize(innerWidth,innerHeight);
const scene=new THREE.Scene();
const camera=new THREE.PerspectiveCamera(55,innerWidth/innerHeight,.1,1000);
camera.position.z=30;

// Particles — dark on white
const N=2400;
const geo=new THREE.BufferGeometry();
const pos=new Float32Array(N*3);
for(let i=0;i<N;i++){
  const t2=Math.random()*Math.PI*2;
  const p=Math.acos(2*Math.random()-1);
  const r=10+Math.random()*30;
  pos[i*3]=r*Math.sin(p)*Math.cos(t2);
  pos[i*3+1]=r*Math.sin(p)*Math.sin(t2);
  pos[i*3+2]=r*Math.cos(p);
}
geo.setAttribute('position',new THREE.BufferAttribute(pos,3));
const mat=new THREE.PointsMaterial({color:0x111111,size:.12,transparent:true,opacity:.35,sizeAttenuation:true});
const pts=new THREE.Points(geo,mat);
scene.add(pts);

// Wireframe icosahedron — light
const wgeo=new THREE.IcosahedronGeometry(13,1);
const wmat=new THREE.MeshBasicMaterial({color:0x111111,wireframe:true,transparent:true,opacity:.04});
const wire=new THREE.Mesh(wgeo,wmat);
scene.add(wire);

// Sparse lines
const lmat=new THREE.LineBasicMaterial({color:0x111111,transparent:true,opacity:.04});
for(let i=0;i<16;i++){
  const lg=new THREE.BufferGeometry().setFromPoints([
    new THREE.Vector3((Math.random()-.5)*80,(Math.random()-.5)*80,(Math.random()-.5)*40),
    new THREE.Vector3((Math.random()-.5)*80,(Math.random()-.5)*80,(Math.random()-.5)*40)
  ]);
  scene.add(new THREE.Line(lg,lmat));
}

let mx=0,my=0,t=0;
document.addEventListener('mousemove',e=>{
  mx=(e.clientX/innerWidth-.5)*2;
  my=(e.clientY/innerHeight-.5)*2;
});
(function animate(){
  requestAnimationFrame(animate);
  t+=.0003;
  pts.rotation.y=t+mx*.05;
  pts.rotation.x=t*.35+my*.035;
  wire.rotation.y=t*.55+mx*.04;
  wire.rotation.x=t*.22+my*.03;
  camera.position.x+=(mx*1.5-camera.position.x)*.018;
  camera.position.y+=(-my*1.5-camera.position.y)*.018;
  camera.lookAt(scene.position);
  renderer.render(scene,camera);
})();

window.addEventListener('resize',()=>{
  camera.aspect=innerWidth/innerHeight;
  camera.updateProjectionMatrix();
  renderer.setSize(innerWidth,innerHeight);
});

// Scroll reveal
const obs=new IntersectionObserver(entries=>entries.forEach(e=>{
  if(e.isIntersecting)e.target.classList.add('on');
}),{threshold:.1});
document.querySelectorAll('.rv').forEach(el=>obs.observe(el));
</script>
</body>
</html>
