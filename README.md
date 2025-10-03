<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Happy Birthday ❤️</title>
  <style>
    :root{--bg:#0b1020;--accent:#ff6b81;--accent2:#ffd166}
    *{box-sizing:border-box}
    body{margin:0;font-family:sans-serif;background:linear-gradient(180deg,#07102a,#0b1020);color:#fff;
      min-height:100vh;display:flex;align-items:center;justify-content:center;padding:20px}
    .wrap{max-width:800px;width:100%;background:rgba(255,255,255,0.05);padding:24px;border-radius:16px;
      text-align:center;box-shadow:0 10px 40px rgba(0,0,0,0.6);position:relative}
    h1{margin:0 0 8px;font-size:32px;color:#ff6b81}
    p{margin:0 0 16px}
    textarea{width:100%;height:160px;background:rgba(255,255,255,0.05);color:#fff;
      border:0;border-radius:8px;padding:10px}
    button{margin-top:12px;padding:12px 20px;border:0;border-radius:8px;cursor:pointer;
      font-weight:bold;background:linear-gradient(90deg,#ff6b81,#ff9bb3);color:#fff}
    #countdownOverlay {position:absolute;top:0;left:0;width:100%;height:100%;
      background:#0b1020;display:flex;align-items:center;justify-content:center;
      font-size:72px;font-weight:bold;color:#ff6b81;z-index:10;}
    canvas{position:absolute;left:0;top:0;width:100%;height:100%;pointer-events:none}
  </style>
</head>
<body>
  <div class="wrap">
    <canvas id="confetti"></canvas>
    <div id="countdownOverlay">10</div>
    <h1 id="title">Happy Birthday, Jaanu ❤️</h1>
    <p>4 October · From Your Love</p>
    <div id="messagePreview">
      Tere bina zindagi adhoori si lagti hai,<br>
      Teri muskaan se rooh roshan ho jaati hai,<br>
      Janamdin pe bas itna kehna hai,<br>
      Tu meri duaon ka sabse khoobsurat silsila hai ❤️<br><br>
      Har khushi tumhari ho jaye,<br>
      Tum sada hasti raho 🌹
    </div>
    <button id="playBtn">Play Surprise 🎶</button>
  </div>

  <script>
    // Confetti setup
    const canvas = document.getElementById('confetti');
    const ctx = canvas.getContext('2d'); let W,H;
    function resize(){W=canvas.width=innerWidth;H=canvas.height=innerHeight}
    window.addEventListener('resize',resize);resize();
    function random(min,max){return Math.random()*(max-min)+min}
    function launchConfetti(){
      const pieces=[];for(let i=0;i<100;i++){
        pieces.push({x:random(0,W),y:random(-H,0),vx:random(-1,1),vy:random(2,6),
          r:random(4,9),c:['#ff6b81','#ffd166','#8ad2ff','#c2ffb3'][Math.floor(Math.random()*4)]})
      }
      let t=0;function draw(){t++;ctx.clearRect(0,0,W,H);
        for(const p of pieces){p.x+=p.vx;p.y+=p.vy;p.vy+=0.05;
          ctx.fillStyle=p.c;ctx.beginPath();ctx.arc(p.x,p.y,p.r,0,Math.PI*2);ctx.fill();}
        if(t<200)requestAnimationFrame(draw);} draw();
    }

    // TTS + music with male voice
    document.getElementById('playBtn').addEventListener('click',()=>{
      let text=document.getElementById('messagePreview').innerText;
      if('speechSynthesis' in window){
        let u=new SpeechSynthesisUtterance(`Happy Birthday Jaanu! ${text}`);
        u.lang='hi-IN'; u.rate=0.9;

        // Select male voice if available
        let voices = speechSynthesis.getVoices();
        let maleVoice = voices.find(v => 
          (v.name.toLowerCase().includes("male") || v.name.toLowerCase().includes("man"))
          && v.lang.startsWith("hi")
        );
        if(maleVoice) u.voice = maleVoice;

        speechSynthesis.speak(u);
      }

      try{
        const A=new (window.AudioContext||window.webkitAudioContext)();
        const notes=[440,523.25,659.25,523.25,440]; let t=A.currentTime;
        for(let n of notes){const o=A.createOscillator(),g=A.createGain();
          o.type='sine';o.frequency.setValueAtTime(n,t);
          g.gain.setValueAtTime(0.0001,t);g.gain.exponentialRampToValueAtTime(0.08,t+0.02);
          g.gain.exponentialRampToValueAtTime(0.0001,t+0.4);
          o.connect(g);g.connect(A.destination);o.start(t);o.stop(t+0.5); t+=0.4}
      }catch(e){}
      launchConfetti();
    });

    // Countdown
    let countdown=10;const overlay=document.getElementById('countdownOverlay');
    const timer=setInterval(()=>{
      countdown--;if(countdown<=0){overlay.style.display='none';clearInterval(timer);
        document.getElementById('playBtn').click();}
      else overlay.textContent=countdown;
    },1000);
  </script>
</body>
</html>
