<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Happy Birthday ❤️</title>
  <style>
    :root{--bg:#0b1020;--card:#0f1724;--accent:#ff6b81;--accent2:#ffd166}
    *{box-sizing:border-box}
    body{margin:0;font-family:system-ui,-apple-system,Segoe UI,Roboto,'Noto Sans',sans-serif;background:linear-gradient(180deg,#07102a 0%,#0b1020 60%);color:#fff;min-height:100vh;display:flex;align-items:center;justify-content:center;padding:24px}
    .wrap{width:100%;max-width:900px;background:linear-gradient(180deg,rgba(255,255,255,0.03),rgba(255,255,255,0.02));border-radius:18px;padding:28px;box-shadow:0 10px 40px rgba(2,6,23,0.6);position:relative;overflow:hidden}
    header{display:flex;gap:16px;align-items:center}
    .heart{width:84px;height:84px;border-radius:20px;background:linear-gradient(135deg,var(--accent),#ff9bb3);display:flex;align-items:center;justify-content:center;box-shadow:0 8px 30px rgba(255,107,129,0.18);font-size:34px}
    h1{margin:0;font-size:28px;line-height:1;color:#fff}
    p.lead{margin:6px 0 0;color:#e6e6e6;opacity:0.95}

    .card{margin-top:18px;background:rgba(255,255,255,0.02);padding:18px;border-radius:12px;display:grid;grid-template-columns:1fr 320px;gap:16px;align-items:center}
    .message{font-size:18px;line-height:1.5}
    .controls{display:flex;flex-direction:column;gap:10px}
    .btn{appearance:none;border:0;padding:12px 14px;border-radius:10px;background:linear-gradient(90deg,var(--accent),#ff8aa0);color:#fff;font-weight:600;cursor:pointer}
    .btn.secondary{background:transparent;border:1px solid rgba(255,255,255,0.06);color:#fff}
    input[type="text"],textarea{width:100%;padding:10px;border-radius:8px;border:0;background:rgba(255,255,255,0.02);color:#fff}
    .right{display:flex;flex-direction:column;gap:10px;align-items:center}
    .photo{width:260px;height:260px;border-radius:12px;background:linear-gradient(180deg,#0b1324,#071025);display:flex;align-items:center;justify-content:center;border:2px dashed rgba(255,255,255,0.03);overflow:hidden}
    .photo img{width:100%;height:100%;object-fit:cover}
    .small{font-size:13px;opacity:0.9}

    /* confetti canvas */
    canvas#confetti{position:absolute;left:0;top:0;width:100%;height:100%;pointer-events:none}

    footer{margin-top:14px;display:flex;gap:10px;align-items:center;justify-content:space-between}

    @media(max-width:820px){.card{grid-template-columns:1fr;}.photo{width:100%;height:260px}}

    /* little floating hearts */
    .floating-heart{position:absolute;right:30px;top:30px;font-size:22px;opacity:0.12}

    /* countdown overlay */
    #countdownOverlay {position:absolute;top:0;left:0;width:100%;height:100%;background:#0b1020;display:flex;align-items:center;justify-content:center;font-size:72px;font-weight:bold;color:#ff6b81;z-index:10;}
  </style>
</head>
<body>
  <div class="wrap" id="page">
    <canvas id="confetti"></canvas>
    <div class="floating-heart">❤️</div>
    <div id="countdownOverlay">10</div>
    <header>
      <div class="heart">💝</div>
      <div>
        <h1 id="title">Happy Birthday, Jaanu ❤️</h1>
        <p class="lead">4 October · Midnight Surprise · From: <strong>You</strong></p>
      </div>
    </header>

    <div class="card">
      <div>
        <div class="message" id="messagePreview">Har pal tumhari muskaan mere liye ek nayi roshni laati hai. Janamdin mubarak, meri jaan. ❤️</div>

        <div style="margin-top:12px;display:flex;gap:8px;flex-wrap:wrap">
          <button class="btn" id="playBtn">Play Surprise (Speak + Music)</button>
          <button class="btn secondary" id="confettiBtn">Celebrate (Confetti)</button>
          <button class="btn secondary" id="downloadBtn">Download as Image</button>
        </div>

        <div style="margin-top:14px;display:grid;gap:8px">
          <label class="small">Customize name:</label>
          <input type="text" id="nameInput" placeholder="Type her name (e.g. Jaanu)" value="Jaanu">
          <label class="small">Custom message (shayarana):</label>
          <textarea id="textInput" rows="8">
Tere bina zindagi adhoori si lagti hai,
Teri muskaan se rooh roshan ho jaati hai,
Janamdin pe bas itna kehna hai,
Tu meri duaon ka sabse khoobsurat silsila hai. ❤️

Har khushi tumhari ho jaye,
Har gham tumse door ho jaye,
Tumhari zindagi mein sirf pyar ho,
Aur tumhari har dua qubool ho jaye. 💕

Tum meri duniya ki sabse khoobsurat tasveer ho,
Mere dil ki dhadkan aur meri rooh ki zaroorat ho,
Iss khaas din par bas dua hai,
Tum sada hasti raho, meri zindagi ki roshni banti raho. 🌹

Janamdin mubarak ho meri Jaan! 🎂✨
          </textarea>
        </div>
      </div>

      <div class="right">
        <div class="photo" id="photoBox"> 
          <img id="photoImg" src="data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='600' height='600'><rect width='100%' height='100%' fill='%230b1020'/><text x='50%' y='50%' fill='%23ffffff' font-size='22' font-family='Arial' text-anchor='middle'>Add her photo</text></svg>" alt="photo">
        </div>
        <input type="file" id="photoUpload" accept="image/*">
        <div class="small">Tip: Upload a photo, set name, press "Play" at midnight. Use headphones for best effect.</div>
      </div>
    </div>

    <footer>
      <div class="small">Made with ❤️ — Midnight Surprise</div>
      <div style="display:flex;gap:8px">
        <button class="btn secondary" id="shareInstr">How to share</button>
      </div>
    </footer>
  </div>

  <script>
    // Simple confetti
    const canvas = document.getElementById('confetti');
    const ctx = canvas.getContext('2d');
    let W, H;
    function resize(){W=canvas.width=page.offsetWidth;H=canvas.height=page.offsetHeight}
    window.addEventListener('resize',resize);resize();

    function random(min,max){return Math.random()*(max-min)+min}

    function launchConfetti(){
      const pieces = [];
      for(let i=0;i<120;i++){
        pieces.push({x:random(0,W),y:random(-H,0),vx:random(-1.5,1.5),vy:random(2,6),r:random(4,9),c: ['#ff6b81','#ffd166','#8ad2ff','#c2ffb3'][Math.floor(Math.random()*4)],rot:random(0,360)})
      }
      let t=0;ctx.clearRect(0,0,W,H);
      function draw(){t++;ctx.clearRect(0,0,W,H);for(const p of pieces){p.x+=p.vx;p.y+=p.vy;p.vy+=0.04;p.rot+=0.2;ctx.save();ctx.translate(p.x,p.y);ctx.rotate(p.rot);ctx.fillStyle=p.c;ctx.fillRect(-p.r/2,-p.r/2,p.r,p.r);ctx.restore()}if(t<200)requestAnimationFrame(draw);}
      draw();
    }

    // text-to-speech + music using WebAudio API (simple oscillator melody)
    const playBtn = document.getElementById('playBtn');
    playBtn.addEventListener('click',async()=>{
      const name = document.getElementById('nameInput').value || 'Jaanu';
      const text = document.getElementById('textInput').value || '';
      document.getElementById('title').textContent = `Happy Birthday, ${name} ❤️`;
      document.getElementById('messagePreview').textContent = text;

      // Speak
      if('speechSynthesis' in window){
        const utter = new SpeechSynthesisUtterance(`${name}, Happy Birthday. ${text}`);
        utter.rate = 0.95;
        utter.pitch = 1.05;
        utter.lang = 'hi-IN';
        speechSynthesis.cancel();
        speechSynthesis.speak(utter);
      }
      // simple melody
      try{
        const AudioCtx = window.AudioContext || window.webkitAudioContext;
        const ctxA = new AudioCtx();
        const notes = [440, 523.25, 659.25, 523.25, 440];
        let t = ctxA.currentTime;
        for(let n of notes){const o = ctxA.createOscillator();const g = ctxA.createGain();o.type='sine';o.frequency.setValueAtTime(n,t);g.gain.setValueAtTime(0.0001,t);g.gain.exponentialRampToValueAtTime(0.08,t+0.02);g.gain.exponentialRampToValueAtTime(0.0001,t+0.45);o.connect(g);g.connect(ctxA.destination);o.start(t);o.stop(t+0.5);t+=0.45}
      }catch(e){console.log('audio err',e)}

      launchConfetti();
    })

    document.getElementById('confettiBtn').addEventListener('click',launchConfetti);

    // upload photo
    const upload = document.getElementById('photoUpload');
    const img = document.getElementById('photoImg');
    upload.addEventListener('change',(e)=>{
      const f = e.target.files[0]; if(!f) return; const url = URL.createObjectURL(f); img.src = url;
    })

    // download as image (simple html2canvas-free approach: draw to canvas)
    document.getElementById('downloadBtn').addEventListener('click',()=>{
      html2canvas(document.querySelector('.wrap')).then(canvas=>{
        const a = document.createElement('a'); a.href = canvas.toDataURL('image/png'); a.download = 'happy-birthday.png'; a.click();
      })
    })

    // include a tiny html2canvas implementation loader
    (function(){
      if(window.html2canvas) return;
      const s = document.createElement('script');
      s.src = 'https://cdn.jsdelivr.net/npm/html2canvas@1.4.1/dist/html2canvas.min.js';
      s.onload = ()=>console.log('html2canvas loaded');
      document.head.appendChild(s);
    })();

    document.getElementById('shareInstr').addEventListener('click',()=>{
      alert('Tip: To share this page: 1) Save this HTML file and open it in browser. 2) Customize name & photo. 3) At midnight click Play. You can also host it on Netlify/GitHub Pages for a shareable link.')
    })

    // small accessibility: update preview when inputs change
    document.getElementById('nameInput').addEventListener('input',e=>{document.getElementById('title').textContent = `Happy Birthday, ${e.target.value||'Jaanu'} ❤️`})
    document.getElementById('textInput').addEventListener('input',e=>{document.getElementById('messagePreview').textContent = e.target.value})

    // countdown overlay logic
    let countdown = 10;
    const overlay = document.getElementById('countdownOverlay');
    const timer = setInterval(()=>{
      countdown--;
      if(countdown<=0){
        overlay.style.display='none';
        clearInterval(timer);
        // Auto play when countdown ends
        playBtn.click();
      } else {
        overlay.textContent = countdown;
      }
    },1000);
  </script>
</body>
</html>
