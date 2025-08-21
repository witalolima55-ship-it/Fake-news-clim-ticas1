<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Feira de Ciências – Fake News Climáticas</title>
  <style>
    body {
      margin: 0;
      font-family: system-ui, Arial, sans-serif;
      background: #0b1020;
      color: #e8f1ff;
      text-align: center;
    }

    .card{
      width:min(920px, 92vw);
      background:linear-gradient(180deg, rgba(255,255,255,.05), rgba(255,255,255,.01));
      border:1px solid rgba(255,255,255,.12);
      box-shadow:0 20px 60px rgba(0,0,0,.45);
      border-radius:28px; padding:28px 26px 22px; margin: 20px auto;
    }
    .badge{ 
      display:inline-flex; gap:.5rem; align-items:center; font-weight:700;
      background:rgba(124,241,200,.12); color:#7cf1c8;
      border:1px solid rgba(124,241,200,.35); padding:.35rem .7rem; border-radius:999px; font-size:.88rem;
    }
    .badge .dot{ width:.6rem; height:.6rem; border-radius:50%; background:#7cf1c8; box-shadow:0 0 18px #7cf1c8; }
    .title{ 
      margin:14px 0 4px; line-height:1.1; font-weight:900;
      font-size: clamp(32px, 6.2vw, 68px);
      display:flex; flex-wrap:wrap; gap:.35rem .6rem; align-items:baseline;
    }
    .title .glitch{
      text-shadow: -2px 0 #76a7ff, 2px 0 #ff6b6b;
      animation: glitch 2.1s infinite ease-in-out alternate;
    }
    @keyframes glitch{
      0%{ transform:translate(0,0) skew(0deg); }
      50%{ transform:translate(.5px, -.5px) skew(.4deg); }
      100%{ transform:translate(-.5px, .5px) skew(-.4deg); }
    }
    .subtitle{ font-size:clamp(14px, 2.4vw, 18px); opacity:.9; margin-top:8px; }
    .row{ display:flex; gap:14px; margin-top:18px; justify-content:center; flex-wrap:wrap; }
    button{
      border:none; background:rgba(255,255,255,.06); color:#e8f1ff; cursor:pointer;
      padding:12px 16px; border-radius:14px; font-weight:700;
      border:1px solid rgba(255,255,255,.14);
    }
    button:hover{ background:rgba(255,255,255,.12) }

    /* Cards explicativos */
    .cards {
      display: flex;
      justify-content: center;
      gap: 20px;
      margin: 40px;
      flex-wrap: wrap;
    }
    .flip-card {
      background: transparent;
      width: 220px;
      height: 160px;
      perspective: 1000px;
    }
    .flip-inner {
      position: relative;
      width: 100%;
      height: 100%;
      text-align: center;
      transition: transform 0.6s;
      transform-style: preserve-3d;
      cursor: pointer;
    }
    .flip-card:hover .flip-inner {
      transform: rotateY(180deg);
    }
    .flip-front, .flip-back {
      position: absolute;
      width: 100%;
      height: 100%;
      backface-visibility: hidden;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 15px;
      border-radius: 12px;
    }
    .flip-front {
      background: #121833;
      border: 1px solid #7cf1c8;
    }
    .flip-back {
      background: #ff6b6b;
      color: white;
      transform: rotateY(180deg);
    }

    /* Quiz */
    .quiz {
      background: #121833;
      padding: 20px;
      margin: 40px auto;
      border-radius: 14px;
      max-width: 500px;
    }
    .quiz button {
      margin-top: 10px;
      padding: 10px 15px;
      border-radius: 8px;
      border: none;
      cursor: pointer;
    }
    .correct { background: #7cf1c8; color: #000; }
    .incorrect { background: #ff6b6b; color: #fff; }

    /* Timeline */
    .timeline {
      margin: 40px auto;
      max-width: 600px;
      text-align: left;
    }
    .timeline ul {
      list-style: none;
      padding: 0;
    }
    .timeline li {
      margin: 10px 0;
      background: rgba(255,255,255,0.1);
      padding: 10px;
      border-radius: 8px;
    }

    /* Rodapé */
    footer {
      margin-top: 50px;
      padding: 15px;
      background: #121833;
      font-size: 14px;
    }
  </style>
</head>
<body>
  <!-- Seção do título -->
  <header>
    <main class="card">
      <span class="badge"><span class="dot"></span> Feira de Ciências 2025</span>
      <h1 id="titulo" class="title">
        <span class="chunk" id="lead"></span>
        <span class="chunk glitch">Fake News</span>
        <span class="chunk">Climáticas 🌎🔎🧪</span>
      </h1>
      <p class="subtitle"><b>Dica:</b> Clique nos botões para interagir com o conteúdo!</p>
      <div class="row">
        <button id="btnTrocar">Trocar título</button>
        <button id="btnCopiar">Copiar título</button>
      </div>
    </main>
  </header>

  <!-- Seção explicativa -->
  <section class="cards">
    <div class="flip-card">
      <div class="flip-inner">
        <div class="flip-front">❓ O que são Fake News Climáticas?</div>
        <div class="flip-back">São informações falsas ou distorcidas sobre mudanças climáticas, espalhadas para confundir ou manipular opiniões.</div>
      </div>
    </div>

    <div class="flip-card">
      <div class="flip-inner">
        <div class="flip-front">🔥 Exemplo de Fake</div>
        <div class="flip-back">“O aquecimento global é invenção da mídia.” → Isso é falso, dados científicos comprovam o aumento da temperatura.</div>
      </div>
    </div>
  </section>

  <!-- Quiz -->
  <section class="quiz">
    <h2>🎯 Teste seu conhecimento</h2>
    <div id="quiz-container"></div>
    <button id="quiz-reset">Reiniciar Quiz</button>
  </section>

  <!-- Linha do tempo -->
  <section class="timeline">
    <h2>📅 Linha do Tempo Climática</h2>
    <ul>
      <li><b>1988:</b> ONU cria o IPCC para estudar mudanças climáticas.</li>
      <li><b>2005:</b> Furacão Katrina gera debate sobre aquecimento global.</li>
      <li><b>2015:</b> Acordo de Paris assinado por 195 países.</li>
      <li><b>2023:</b> Ano mais quente já registrado no planeta.</li>
    </ul>
  </section>

  <!-- Rodapé -->
  <footer>
    <p>🌎 Feito para a Feira de Ciências 2025 | Tema: Fake News Climáticas 🚫🔥❄️</p>
  </footer>

  <script>
    // ==== Título interativo ====
    const ideias = ["Clima ou Caô?", "Fato ou Fatoide?", "Boato Congelado vs Dado Quente"];
    const elLead = document.getElementById("lead");
    let idx = 0;

    function trocarTitulo(){
      idx = (idx + 1) % ideias.length;
      elLead.textContent = ideias[idx];
    }
    document.getElementById("btnTrocar").addEventListener("click", trocarTitulo);
    document.getElementById("btnCopiar").addEventListener("click", ()=>{
      navigator.clipboard.writeText(elLead.textContent + " Fake News Climáticas 🌎🔎🧪");
      alert("Título copiado!");
    });
    elLead.textContent = ideias[idx];

    // ==== Quiz ====
    const perguntas = [
      { q: "O aquecimento global é uma invenção?", a: false },
      { q: "O CO₂ é um dos gases responsáveis pelas mudanças climáticas?", a: true },
      { q: "Nevar em um país significa que não existe aquecimento global?", a: false }
    ];

    const quizContainer = document.getElementById("quiz-container");

    function carregarQuiz(){
      quizContainer.innerHTML = "";
      perguntas.forEach((pergunta, i)=>{
        const div = document.createElement("div");
        div.innerHTML = `<p>${pergunta.q}</p>
          <button onclick="responder(${i}, true)">Verdadeiro</button>
          <button onclick="responder(${i}, false)">Falso</button>`;
        quizContainer.appendChild(div);
      });
    }
    function responder(i, resposta){
      const botoes = quizContainer.children[i].querySelectorAll("button");
      botoes.forEach(btn => btn.disabled = true);
      if(resposta === perguntas[i].a){
        botoes[resposta ? 0 : 1].classList.add("correct");
      } else {
        botoes[resposta ? 0 : 1].classList.add("incorrect");
      }
    }
    document.getElementById("quiz-reset").addEventListener("click", carregarQuiz);

    carregarQuiz();
  </script>
</body>
</html>
