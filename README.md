# san-valentin
<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>¿Quieres ser mi San Valentín?</title>
  <style>
    :root{
      --bg1:#ff3b7a;
      --bg2:#7c3aed;
      --card:#ffffffcc;
      --text:#1f2937;
      --yes:#16a34a;
      --no:#ef4444;
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      min-height:100vh;
      display:flex;
      align-items:center;
      justify-content:center;
      font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
      color:var(--text);
      background: radial-gradient(1200px 800px at 20% 20%, #ffd1e3 0%, transparent 55%),
                  radial-gradient(1200px 800px at 80% 30%, #d9c7ff 0%, transparent 55%),
                  linear-gradient(135deg, var(--bg1), var(--bg2));
      overflow:hidden;
    }
    .card{
      width:min(92vw, 560px);
      background:var(--card);
      backdrop-filter: blur(10px);
      border:1px solid #ffffff80;
      border-radius:24px;
      padding:28px 22px;
      box-shadow: 0 20px 60px rgba(0,0,0,.25);
      text-align:center;
      position:relative;
    }
    h1{
      margin:6px 0 10px;
      font-size: clamp(26px, 4vw, 36px);
      letter-spacing:.2px;
    }
    p{
      margin:0 0 18px;
      font-size: 16px;
      line-height:1.4;
      opacity:.9;
    }
    .names{
      font-weight:700;
      color:#111827;
    }
    .btns{
      margin-top:18px;
      display:flex;
      gap:12px;
      justify-content:center;
      flex-wrap:wrap;
      position:relative;
      min-height:60px;
    }
    button{
      border:none;
      border-radius:14px;
      padding:14px 18px;
      font-size:16px;
      font-weight:700;
      cursor:pointer;
      transition: transform .12s ease, filter .12s ease;
      box-shadow: 0 10px 22px rgba(0,0,0,.18);
    }
    button:active{ transform: scale(.98); }
    .yes{ background: linear-gradient(135deg, #22c55e, #16a34a); color:white; }
    .no{ background: linear-gradient(135deg, #fb7185, #ef4444); color:white; position:relative; }
    .footer{
      margin-top:16px;
      font-size:12px;
      opacity:.7;
    }
    .badge{
      display:inline-flex;
      gap:8px;
      align-items:center;
      padding:8px 12px;
      border-radius:999px;
      background:#ffffffb0;
      border:1px solid #ffffff80;
      font-size:12px;
      margin-bottom:12px;
    }
    .badge span{
      width:10px;height:10px;border-radius:999px;
      background: #ff3b7a;
      box-shadow: 0 0 14px #ff3b7a;
    }
    /* corazones */
    .heart{
      position:absolute;
      width:14px;height:14px;
      transform: rotate(45deg);
      opacity:.75;
      animation: floatUp linear forwards;
      pointer-events:none;
      filter: drop-shadow(0 8px 10px rgba(0,0,0,.2));
    }
    .heart:before, .heart:after{
      content:"";
      position:absolute;
      width:14px;height:14px;
      background: inherit;
      border-radius:50%;
    }
    .heart:before{ left:-7px; }
    .heart:after{ top:-7px; }
    @keyframes floatUp{
      from{ transform: translateY(0) rotate(45deg); }
      to{ transform: translateY(-120vh) rotate(45deg); opacity:0; }
    }

    .modal{
      position:fixed; inset:0;
      display:none;
      align-items:center;
      justify-content:center;
      background: rgba(0,0,0,.45);
      padding:18px;
    }
    .modal.open{ display:flex; }
    .modal-box{
      width:min(92vw, 520px);
      background:white;
      border-radius:20px;
      padding:22px;
      text-align:center;
      box-shadow:0 30px 80px rgba(0,0,0,.35);
    }
    .big{
      font-size:44px;
      margin:6px 0 12px;
    }
    .close{
      margin-top:14px;
      background:#111827;
      color:white;
    }
  </style>
</head>
<body>
  <div class="card" id="card">
    <div class="badge"><span></span> Invitación especial</div>
    <h1>¿Quieres ser mi San Valentín? 💘</h1>
    <p>
      <span class="names">Chris</span> ➜ <span class="names">Melanny</span><br>
      Prometo risas, cafecitos y un día lindo contigo.
    </p>

    <div class="btns" id="btns">
      <button class="yes" id="yesBtn">Sí 💚</button>
      <button class="no" id="noBtn">No 🙃</button>
    </div>

    <div class="footer">Tip: si quieres, cámbiale los nombres y el mensaje arriba.</div>
  </div>

  <div class="modal" id="modal">
    <div class="modal-box">
      <div class="big">🥹💖</div>
      <h2>¡Sabía que dirías que sí!</h2>
      <p>Ahora solo falta escoger: ¿cena, helado o ambos? 😄</p>
      <button class="close" id="closeBtn">Cerrar</button>
    </div>
  </div>

  <script>
    const noBtn = document.getElementById("noBtn");
    const yesBtn = document.getElementById("yesBtn");
    const btns = document.getElementById("btns");
    const card = document.getElementById("card");
    const modal = document.getElementById("modal");
    const closeBtn = document.getElementById("closeBtn");

    // Botón "No" se escapa
    function moveNo(){
      const rect = btns.getBoundingClientRect();
      const b = noBtn.getBoundingClientRect();
      const maxX = rect.width - b.width;
      const maxY = rect.height - b.height;
      const x = Math.max(0, Math.min(maxX, Math.random()*maxX));
      const y = Math.max(0, Math.min(maxY, Math.random()*maxY));
      noBtn.style.position = "absolute";
      noBtn.style.left = x + "px";
      noBtn.style.top  = y + "px";
    }
    noBtn.addEventListener("mouseenter", moveNo);
    noBtn.addEventListener("click", moveNo);

    // Aceptar
    yesBtn.addEventListener("click", () => {
      modal.classList.add("open");
      confettiHearts(40);
    });

    closeBtn.addEventListener("click", () => modal.classList.remove("open"));
    modal.addEventListener("click", (e) => {
      if(e.target === modal) modal.classList.remove("open");
    });

    // Corazones flotando
    function spawnHeart(){
      const h = document.createElement("div");
      h.className = "heart";
      const size = 10 + Math.random()*18;
      h.style.width = h.style.height = size + "px";
      const left = Math.random()*100;
      h.style.left = left + "vw";
      h.style.bottom = "-20px";
      const dur = 4 + Math.random()*4;
      h.style.animationDuration = dur + "s";
      const colors = ["#ff2d55","#ff6b9a","#ffd1e3","#c084fc","#fb7185"];
      h.style.background = colors[Math.floor(Math.random()*colors.length)];
      document.body.appendChild(h);
      setTimeout(() => h.remove(), dur*1000);
    }
    setInterval(spawnHeart, 350);

    // Explosión extra al dar "sí"
    function confettiHearts(n){
      for(let i=0;i<n;i++){
        setTimeout(spawnHeart, i*40);
      }
    }
  </script>
</body>
</html>
