# navoo
desafio navoo
<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Desafio Navoo - Jogo Interativo</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #0e0e1a;
      color: #fff;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
      margin: 0;
      padding: 20px;
    }
    .container {
      background-color: #1e1e2f;
      padding: 30px;
      border-radius: 12px;
      box-shadow: 0 0 16px rgba(255, 0, 255, 0.4);
      max-width: 700px;
      text-align: center;
    }
    h1 {
      font-size: 28px;
      color: #b23fff;
    }
    .question {
      margin: 20px 0;
      font-size: 18px;
    }
    .options {
      display: flex;
      flex-direction: column;
      gap: 10px;
      margin-top: 10px;
    }
    button.option {
      background-color: #b23fff;
      color: white;
      border: none;
      padding: 12px;
      border-radius: 8px;
      font-size: 16px;
      cursor: pointer;
      transition: background 0.3s;
    }
    button.option:hover {
      background-color: #8a2be2;
    }
    .feedback {
      margin-top: 20px;
      font-style: italic;
    }
    .end-message {
      font-size: 20px;
      margin-top: 30px;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Desafio Navoo 🌟</h1>
    <div id="game">
      <p class="question" id="question">Carregando pergunta...</p>
      <div class="options" id="options"></div>
      <p class="feedback" id="feedback"></p>
    </div>
    <div class="end-message" id="endMessage"></div>
  </div>

  <script>
    const questions = [
      {
        q: "Você é uma marca interessada em campanhas com influenciadores. Qual fator mais atrai você para conhecer a Navoo?",
        options: [
          { text: "A Navoo é uma startup moderna com site", score: 0 },
          { text: "A Navoo cobra comissão apenas por sucesso e não gera custo inicial", score: 1 },
          { text: "A Navoo tem muitos seguidores nas redes sociais", score: 0 }
        ],
        feedback: "O modelo sem custo inicial é o maior diferencial da Navoo!"
      },
      {
        q: "Você é um influenciador e recebeu uma proposta da Navoo. Qual motivo te faria topar participar?",
        options: [
          { text: "A Navoo faz toda a intermediação e te envia propostas já filtradas", score: 1 },
          { text: "Você pode pagar para aparecer mais nas buscas", score: 0 },
          { text: "Você escolhe com quais marcas quer trabalhar manualmente", score: 0 }
        ],
        feedback: "Facilidade e praticidade são fundamentais para influenciadores ocupados."
      },
      {
        q: "Você é uma marca e quer saber se a Navoo é confiável. O que te deixaria mais tranquilo?",
        options: [
          { text: "Saber que tudo é feito por WhatsApp", score: 0 },
          { text: "Ver que eles têm contratos automáticos e banco de dados organizado", score: 1 },
          { text: "Ter um cupom de desconto", score: 0 }
        ],
        feedback: "A automação e organização são pontos profissionais que transmitem segurança."
      },
      {
        q: "Você é um comunicador de rádio/podcast. Como a Navoo pode te ajudar?",
        options: [
          { text: "Te conectando com empresas interessadas em anunciar para seu público", score: 1 },
          { text: "Oferecendo cursos pagos", score: 0 },
          { text: "Criando um Instagram para você", score: 0 }
        ],
        feedback: "A proposta da Navoo é conectar comunicadores com campanhas certas para seu nicho."
      }
    ];

    let current = 0;
    let score = 0;

    const questionEl = document.getElementById("question");
    const optionsEl = document.getElementById("options");
    const feedbackEl = document.getElementById("feedback");
    const endMessageEl = document.getElementById("endMessage");

    function loadQuestion() {
      if (current < questions.length) {
        const q = questions[current];
        questionEl.textContent = q.q;
        optionsEl.innerHTML = "";
        feedbackEl.textContent = "";

        q.options.forEach(option => {
          const btn = document.createElement("button");
          btn.className = "option";
          btn.textContent = option.text;
          btn.onclick = () => {
            score += option.score;
            feedbackEl.textContent = q.feedback;
            current++;
            setTimeout(loadQuestion, 2000);
          };
          optionsEl.appendChild(btn);
        });
      } else {
        endGame();
      }
    }

    function endGame() {
      document.getElementById("game").style.display = "none";
      if (score === questions.length) {
        endMessageEl.textContent = "Parabéns! Você entendeu perfeitamente a proposta da Navoo. 🚀";
      } else if (score >= 2) {
        endMessageEl.textContent = "Bom trabalho! Você captou bem a proposta da Navoo. ✨";
      } else {
        endMessageEl.textContent = "Parece que ainda há o que aprender sobre a Navoo. Vamos conversar? 😉";
      }
    }

    loadQuestion();
  </script>
</body>
</html>
