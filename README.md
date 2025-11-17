# Game-Tebak-Hewan
# Game yang dimainkan dengan cara menebak hewan dari inisial huruf yang diberikan

<!doctype html>
<html lang="id">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Game Tebak Hewan</title>
  <style>
    :root{font-family:Inter,system-ui,Segoe UI,Roboto,Helvetica,Arial,sans-serif}
    body{display:flex;align-items:center;justify-content:center;min-height:100vh;background:#f3f6fb;margin:0}
    .card{background:#fff;border-radius:12px;padding:28px;box-shadow:0 8px 24px rgba(20,30,60,0.08);max-width:520px;width:92%}
    h1{margin:0 0 6px;font-size:20px}
    p.lead{margin:0 0 18px;color:#405073}
    .hint{font-size:32px;font-weight:700;letter-spacing:3px;margin:18px 0}
    .row{display:flex;gap:8px;align-items:center}
    input[type=text]{flex:1;padding:10px 12px;border-radius:8px;border:1px solid #d9e2f0;font-size:16px}
    button{background:#2563eb;color:#fff;border:none;padding:10px 14px;border-radius:8px;font-weight:600;cursor:pointer}
    button.ghost{background:transparent;color:#2563eb;border:1px solid #cfe0ff}
    .result{margin-top:16px;padding:12px;border-radius:8px;background:#f8fafc;color:#0f172a}
    .small{font-size:13px;color:#55607a}
    footer{margin-top:18px;font-size:13px;color:#6b7280}
  </style>
</head>
<body>
  <main class="card" role="main">
    <h1>=== GAME TEBAK HEWAN ===</h1>
    <p class="lead">Selamat datang di permainan tebak hewan! Komputer akan memilih sebuah hewan secara acak. Tebak berdasarkan inisial yang diberikan.</p>

    <div id="game-area">
      <div class="small">--- Ronde Baru ---</div>
      <div class="hint" id="initial">A</div>

      <div class="row" style="margin-top:8px">
        <input id="guess" type="text" placeholder="Masukkan jawaban (mis. kucing)" autocomplete="off" />
        <button id="submit">Tebak</button>
      </div>

      <div class="result" id="feedback" style="display:none"></div>

      <div style="margin-top:12px;display:flex;gap:8px">
        <button id="next" class="ghost">Lewati / Tampilkan Jawaban</button>
        <button id="play-again" class="ghost">Main Lagi</button>
      </div>

      <footer>
        <div class="small">Petunjuk: inisial huruf ditampilkan di atas. Tulis nama hewan lengkap tanpa tanda baca.</div>
      </footer>
    </div>
  </main>

  <script>
    (function(){
      const hewanList = ["kucing", "anjing", "gajah", "harimau", "singa", "ular", "burung", "ikan", "kura-kura"];

      const elInitial = document.getElementById('initial');
      const elGuess = document.getElementById('guess');
      const elSubmit = document.getElementById('submit');
      const elFeedback = document.getElementById('feedback');
      const elNext = document.getElementById('next');
      const elPlayAgain = document.getElementById('play-again');

      let jawabanBenar = '';

      function pickAnimal(){
        jawabanBenar = hewanList[Math.floor(Math.random()*hewanList.length)];
        elInitial.textContent = jawabanBenar.charAt(0).toUpperCase();
        elGuess.value = '';
        elFeedback.style.display = 'none';
        elGuess.focus();
      }

      function showFeedback(message){
        elFeedback.style.display = 'block';
        elFeedback.textContent = message;
      }

      elSubmit.addEventListener('click', ()=>{
        const tebakan = elGuess.value.trim().toLowerCase();
        if(!tebakan){
          showFeedback('Tolong masukkan tebakan terlebih dahulu.');
          return;
        }

        if(tebakan === jawabanBenar){
          showFeedback('Keren! Tebakanmu tepat sekali! 🎉');
        } else {
          showFeedback('Yah, belum tepat. Hewan yang benar adalah: ' + jawabanBenar + '. Jangan menyerah, coba lagi!');
        }
      });

      // Enter key triggers tebakan
      elGuess.addEventListener('keydown', (e)=>{
        if(e.key === 'Enter'){
          elSubmit.click();
        }
      });

      // Lewati / tampilkan jawaban
      elNext.addEventListener('click', ()=>{
        showFeedback('Hewan yang benar adalah: ' + jawabanBenar + '.');
      });

      // Main lagi (mulai ronde baru)
      elPlayAgain.addEventListener('click', ()=>{
        pickAnimal();
      });

      // Mulai permainan pada pemuatan
      pickAnimal();

    })();
  </script>
</body>
</html>
