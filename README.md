<!--
Ləman üçün animasiyalı ad günü kartı (HTML faylı).
İstifadə: bu faylı .html kimi yükləyib GitHub Pages, Netlify, Vercel və ya Google Sites-a yerləşdirərək birbaşa link əldə edə bilərsən.
Local işlətmək üçün brauzerdə aç: faylı iki dəfə kliklə.
-->
<!doctype html>
<html lang="az">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Ad günün mübarək, Ləman!</title>
  <style>
    :root{--bg:#FFF7F0;--accent:#FF6B9A;--accent2:#FFBE76;--text:#3b2b2b}
    html,body{height:100%;margin:0;font-family:system-ui,-apple-system,Segoe UI,Roboto,'Helvetica Neue',Arial}
    body{background:linear-gradient(180deg,var(--bg),#FFF);display:flex;align-items:center;justify-content:center;padding:20px}
    .card{width:900px;max-width:100%;background:linear-gradient(180deg,#ffffff, #fff3f7);border-radius:18px;box-shadow:0 14px 40px rgba(0,0,0,.12);overflow:hidden;position:relative}
    header{padding:28px 32px 0;display:flex;align-items:center;gap:18px}
    .logo{width:72px;height:72px;border-radius:14px;background:linear-gradient(135deg,var(--accent),var(--accent2));display:flex;align-items:center;justify-content:center;color:white;font-weight:700;font-size:22px}
    .title{flex:1}
    .title h1{margin:0;font-size:20px;color:var(--text)}
    .title p{margin:6px 0 0;color:#6b5660}
    .content{padding:18px 32px 32px;display:flex;gap:24px}
    .left{flex:1;display:flex;align-items:center;justify-content:center;position:relative}
    .cake{width:320px;max-width:48%;transform:translateY(0);transition:transform .6s}
    .right{flex:1;display:flex;flex-direction:column;justify-content:center}
    .message{background:rgba(255,255,255,0.85);padding:22px;border-radius:12px;box-shadow:0 6px 18px rgba(0,0,0,.06)}
    .message h2{margin:0 0 8px;font-size:28px;color:var(--accent)}
    .message p{margin:6px 0;color:var(--text);line-height:1.4}
    .controls{margin-top:12px;display:flex;gap:8px}
    .btn{border:0;padding:10px 14px;border-radius:10px;cursor:pointer;font-weight:600}
    .btn.play{background:linear-gradient(90deg,var(--accent),#ff99b4);color:white}
    .btn.stop{background:#eee}
    .btn.share{background:linear-gradient(90deg,#7ad7ff,#6f9cff);color:white}
    /* Balloons */
    .balloon{position:absolute;width:64px;height:90px;border-radius:50% 50% 50% 50%;transform-origin:center bottom}
    .balloon::after{content:'';position:absolute;left:50%;bottom:-18px;width:2px;height:18px;background:#444;transform:translateX(-50%)}
    .b1{background:linear-gradient(180deg,#FF7BAC,#FF3D6B);left:8%;bottom:20px;animation:float 6s ease-in-out infinite}
    .b2{background:linear-gradient(180deg,#FFD166,#FF9F1C);left:22%;bottom:10px;animation:float 5.2s ease-in-out .6s infinite}
    .b3{background:linear-gradient(180deg,#7EE8FA,#4CC9F0);left:40%;bottom:8px;animation:float 5.8s ease-in-out .2s infinite}
    .b4{background:linear-gradient(180deg,#B39CD0,#8E79D6);right:10%;bottom:22px;animation:float 6.6s ease-in-out .3s infinite}
    @keyframes float{0%{transform:translateY(0) rotate(-2deg)}50%{transform:translateY(-28px) rotate(4deg)}100%{transform:translateY(0) rotate(-2deg)}}
    /* confetti canvas covers entire card */
    canvas.confetti{position:absolute;left:0;top:0;width:100%;height:100%;pointer-events:none}
    /* responsive */
    @media(max-width:700px){.content{flex-direction:column}.cake{max-width:80%;margin-bottom:12px}}
    /* small sparkle */
    .sparkle{position:absolute;width:8px;height:8px;border-radius:50%;background:gold;box-shadow:0 0 12px rgba(255,215,0,.9);opacity:.9}
    footer{padding:10px 18px;text-align:center;color:#7b6a72;font-size:13px}
  </style>
</head>
<body>
  <div class="card" role="main">
    <canvas class="confetti" aria-hidden="true"></canvas>
    <header>
      <div class="logo">🎉</div>
      <div class="title">
        <h1>Ad günün mübarək, Ləman!</h1>
        <p>Bu kiçik sürpriz sənə xüsusi hazırlandı — oxu, dinlə və əylən 🎂</p>
      </div>
      <div style="margin-right:20px;">
        <button class="btn play" id="playBtn">Musiqini başlat</button>
      </div>
    </header>

    <div class="content">
      <div class="left">
        <!-- Simple cake SVG -->
        <div class="cake" id="cake">
          <svg viewBox="0 0 300 300" width="320" height="320" xmlns="http://www.w3.org/2000/svg">
            <defs>
              <linearGradient id="g1" x1="0" x2="1"><stop offset="0" stop-color="#ffd1dc"/><stop offset="1" stop-color="#ff9db1"/></linearGradient>
            </defs>
            <rect x="30" y="170" width="240" height="80" rx="12" fill="#7dd3fc" />
            <rect x="60" y="140" width="180" height="40" rx="10" fill="#ffe082" />
            <rect x="70" y="110" width="160" height="40" rx="10" fill="url(#g1)" />
            <!-- candles -->
            <g id="candles">
              <rect x="90" y="70" width="8" height="40" fill="#FF5D8F" rx="2" />
              <rect x="120" y="70" width="8" height="40" fill="#FFB86B" rx="2" />
              <rect x="150" y="70" width="8" height="40" fill="#8AF3C5" rx="2" />
              <rect x="180" y="70" width="8" height="40" fill="#8DB4FF" rx="2" />
            </g>
            <!-- flames (will animate via JS) -->
            <g id="flames" fill="orange">
              <ellipse cx="94" cy="65" rx="8" ry="12" fill="#FFEB99" opacity="0.95"/>
              <ellipse cx="124" cy="65" rx="8" ry="12" fill="#FFEB99" opacity="0.95"/>
              <ellipse cx="154" cy="65" rx="8" ry="12" fill="#FFEB99" opacity="0.95"/>
              <ellipse cx="184" cy="65" rx="8" ry="12" fill="#FFEB99" opacity="0.95"/>
            </g>
          </svg>
        </div>
        <!-- balloons -->
        <div class="balloon b1" aria-hidden="true"></div>
        <div class="balloon b2" aria-hidden="true"></div>
        <div class="balloon b3" aria-hidden="true"></div>
        <div class="balloon b4" aria-hidden="true"></div>
      </div>

      <div class="right">
        <div class="message" role="article">
          <h2>🎈 Ad günün mübarək, Ləman!</h2>
          <p>Ad gününü təbrik edirəm. Artıq bir yaşda böyüdün, yəni uşaqlıq sona çatdı 🤩.</p>
          <p>Gələcək həyatında uğurlar. Sənə nə olur olsun təbrik edəcəm demişdim.</p>
          <div class="controls">
            <button class="btn play" id="play2">Dinlə / Dayandır</button>
            <button class="btn stop" id="confettiBtn">Konfeti partlat</button>
            <button class="btn share" id="downloadBtn">HTML-i yüklə</button>
          </div>
        </div>
      </div>
    </div>
    <footer>Paylaşmaq üçün bu faylı host et (GitHub Pages / Netlify / Vercel) və linki Ləman ilə paylaş.</footer>
  </div>

  <script>
    // Simple confetti implementation
    const canvas = document.querySelector('canvas.confetti');
    const ctx = canvas.getContext('2d');
    let W, H, confettiPieces = [];
    function resize(){ W = canvas.width = canvas.clientWidth; H = canvas.height = canvas.clientHeight }
    window.addEventListener('resize', resize); resize();

    function rand(min,max){ return Math.random()*(max-min)+min }
    function makeConfetti(n=120){ confettiPieces = []; const colors=['#FF5D8F','#FFD166','#7EE8FA','#8E79D6','#6fffd6','#ffb3cc'];
      for(let i=0;i<n;i++){ confettiPieces.push({x:rand(0,W),y:rand(-H,0),w:rand(6,12),h:rand(8,14),color:colors[i%colors.length],rot:rand(0,360),velX:rand(-0.7,0.7),velY:rand(2,6),spin:rand(-0.2,0.2)}) }
    }
    function drawConfetti(){ ctx.clearRect(0,0,W,H); for(const p of confettiPieces){ p.x += p.velX; p.y += p.velY; p.rot += p.spin; ctx.save(); ctx.translate(p.x,p.y); ctx.rotate(p.rot); ctx.fillStyle = p.color; ctx.fillRect(-p.w/2,-p.h/2,p.w,p.h); ctx.restore(); }
      // remove pieces off-screen
      confettiPieces = confettiPieces.filter(p=>p.y < H+40);
      if(confettiPieces.length) requestAnimationFrame(drawConfetti);
    }
    document.getElementById('confettiBtn').addEventListener('click', ()=>{ makeConfetti(180); drawConfetti(); })

    // Simple sparkle generator
    function makeSparkle(){ const s=document.createElement('div'); s.className='sparkle'; s.style.left=rand(20,880)+'px'; s.style.top=rand(20,260)+'px'; document.querySelector('.card').appendChild(s); setTimeout(()=>s.remove(),900); }
    setInterval(makeSparkle,1200);

    // Play a simple melody using WebAudio
    const AudioCtx = window.AudioContext||window.webkitAudioContext;
    let audioCtx = null; let playing=false; let seqTimer=null;
    function playMelody(){ if(!audioCtx) audioCtx=new AudioCtx(); const now = audioCtx.currentTime; const o = audioCtx.createOscillator(); const g = audioCtx.createGain(); o.connect(g); g.connect(audioCtx.destination); o.type='sine'; o.frequency.setValueAtTime(440, now); g.gain.setValueAtTime(0, now); // helper to play note
      const notes = [440,494,523,659,587,523,494,440]; // A B C E D C B A (simple)
      let t=0; for(let i=0;i<notes.length;i++){ (function(freq,delay){ const osc = audioCtx.createOscillator(); const gain=audioCtx.createGain(); osc.connect(gain); gain.connect(audioCtx.destination); osc.type='triangle'; osc.frequency.setValueAtTime(freq, audioCtx.currentTime + delay); gain.gain.setValueAtTime(0, audioCtx.currentTime + delay); gain.gain.linearRampToValueAtTime(0.08, audioCtx.currentTime + delay + 0.01); gain.gain.linearRampToValueAtTime(0.0, audioCtx.currentTime + delay + 0.45); osc.start(audioCtx.currentTime + delay); osc.stop(audioCtx.currentTime + delay + 0.5);
        })(notes[i], t); t += 0.5 }
    }

    function startLoop(){ if(playing) return; playing=true; playMelody(); seqTimer=setInterval(playMelody, 4500); }
    function stopLoop(){ if(!playing) return; playing=false; clearInterval(seqTimer); seqTimer=null; if(audioCtx && audioCtx.state!=='closed') { try{ audioCtx.close(); }catch(e){} audioCtx=null } }

    document.getElementById('playBtn').addEventListener('click', ()=>{ if(!playing){ startLoop(); document.getElementById('playBtn').textContent='Musiqi işləyir'; document.getElementById('play2').textContent='Dayandır' } else { stopLoop(); document.getElementById('playBtn').textContent='Musiqini başlat'; document.getElementById('play2').textContent='Dinlə / Dayandır' } })
    document.getElementById('play2').addEventListener('click', ()=>{ document.getElementById('playBtn').click(); })

    // Download HTML file (serialize current document)
    document.getElementById('downloadBtn').addEventListener('click', ()=>{
      const doctype = '<!doctype html>\n';
      const html = document.documentElement.outerHTML;
      const blob = new Blob([doctype + html], {type:'text/html'});
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a'); a.href = url; a.download = 'leman_ad_gunu_karti.html'; document.body.appendChild(a); a.click(); a.remove(); URL.revokeObjectURL(url);
    });

    // Small entrance animation for cake
    window.addEventListener('load', ()=>{
      const cake = document.getElementById('cake'); cake.style.transform='translateY(-6px)';
      // initial confetti
      setTimeout(()=>{ document.getElementById('confettiBtn').click() }, 900);
    });
  </script>
</body>
</html>

