<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>English Tense Quiz Game</title>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
  <style>
    body {
      background: linear-gradient(135deg, #fbc2eb 0%, #a6c1ee 100%);
    }
    .question-card {
      transition: transform 0.3s ease-in-out;
    }
    .question-card:hover {
      transform: scale(1.02);
    }
    .correct {
      background-color: #c6f6d5 !important; /* green-100 */
    }
    .incorrect {
      background-color: #fed7d7 !important; /* red-100 */
    }
    #feedback-image {
      text-align: center;
      margin-top: 20px;
      display: none;
    }
    #feedback-img {
      width: 150px;
      height: 150px;
    }
  </style>
</head>
<body class="min-h-screen flex items-center justify-center p-4">
  <div class="w-full max-w-3xl bg-white rounded-2xl shadow-2xl p-8">
    <h1 class="text-3xl font-bold text-center mb-6 text-blue-600">English Tense Quiz: Past vs Future</h1>
    <div id="quiz-container" class="space-y-6"></div>
    <div id="result" class="hidden text-center mt-6">
      <p class="text-xl font-semibold">Your Score: <span id="score">0</span>/100</p>
      <button onclick="location.reload()" class="mt-4 px-4 py-2 bg-green-500 text-white rounded hover:bg-green-600">Play Again</button>
    </div>
    <!-- Gambar feedback (Einstein atau Monyet) -->
    <div id="feedback-image">
      <img id="feedback-img" src="" alt="Feedback Image">
    </div>
  </div>

  <script>
    const questions = [
      { q: "I ____ to the market yesterday.", a: ["go", "went", "goes", "gone"], c: 1 },
      { q: "They ____ a movie tomorrow.", a: ["watched", "watching", "will watch", "watches"], c: 2 },
      { q: "She ____ her homework last night.", a: ["did", "does", "do", "will do"], c: 0 },
      { q: "We ____ the museum next week.", a: ["visited", "visits", "will visit", "visit"], c: 2 },
      { q: "He ____ football with his friends yesterday.", a: ["plays", "play", "played", "will play"], c: 2 },
      { q: "They ____ their grandmother next weekend.", a: ["visited", "will visit", "visiting", "visits"], c: 1 },
      { q: "I ____ breakfast at 7 AM yesterday.", a: ["eat", "ate", "eats", "eating"], c: 1 },
      { q: "She ____ to the dentist tomorrow.", a: ["go", "went", "will go", "goes"], c: 2 },
      { q: "We ____ the concert last Saturday.", a: ["attends", "attended", "attending", "will attend"], c: 1 },
      { q: "He ____ his bike to school tomorrow.", a: ["rode", "rides", "will ride", "ride"], c: 2 },
      { q: "They ____ a cake for her birthday last year.", a: ["make", "made", "makes", "will make"], c: 1 },
      { q: "I ____ to Bali next month.", a: ["went", "goes", "go", "will go"], c: 3 },
      { q: "She ____ me with my homework yesterday.", a: ["helps", "help", "helped", "will help"], c: 2 },
      { q: "We ____ basketball next Saturday.", a: ["played", "plays", "playing", "will play"], c: 3 },
      { q: "He ____ a book last night.", a: ["reads", "read", "reading", "will read"], c: 1 },
      { q: "They ____ to the zoo tomorrow.", a: ["go", "went", "going", "will go"], c: 3 },
      { q: "I ____ lunch with Sarah yesterday.", a: ["have", "had", "having", "will have"], c: 1 },
      { q: "She ____ the dishes tomorrow.", a: ["wash", "washed", "washes", "will wash"], c: 3 },
      { q: "We ____ a new project last month.", a: ["start", "started", "starting", "will start"], c: 1 },
      { q: "He ____ new shoes next week.", a: ["buys", "bought", "buy", "will buy"], c: 3 }
    ];

    let current = 0;
    let score = 0;

    const quizContainer = document.getElementById('quiz-container');
    const resultContainer = document.getElementById('result');
    const scoreSpan = document.getElementById('score');
    const feedbackImage = document.getElementById('feedback-image');
    const feedbackImg = document.getElementById('feedback-img');

    function renderQuestion() {
      quizContainer.innerHTML = '';
      const q = questions[current];

      const card = document.createElement('div');
      card.className = 'question-card bg-blue-100 p-6 rounded-xl shadow-md';

      const questionText = document.createElement('p');
      questionText.className = 'text-lg font-medium mb-4';
      questionText.textContent = `Question ${current + 1}: ${q.q}`;
      card.appendChild(questionText);

      q.a.forEach((option, i) => {
        const btn = document.createElement('button');
        btn.textContent = option;
        btn.className = 'answer-btn block w-full text-left px-4 py-2 my-2 bg-white border border-blue-300 rounded hover:bg-blue-200';
        btn.onclick = () => {
          const allButtons = card.querySelectorAll('.answer-btn');
          allButtons.forEach((b, index) => {
            b.disabled = true;
            if (index === q.c) {
              b.classList.add('correct');
            }
          });
          if (i === q.c) {
            score += 5;
            feedbackImg.src = 'https://upload.wikimedia.org/wikipedia/commons/6/6f/Albert_Einstein_Head.jpg'; // Albert Einstein
          } else {
            btn.classList.add('incorrect');
            feedbackImg.src = 'https://p2.piqsels.com/preview/973/783/618/animal-ape-black-clever.jpg'; // Monyet
          }
          feedbackImage.style.display = 'block'; // Tampilkan gambar
          setTimeout(() => {
            current++;
            if (current < questions.length) {
              renderQuestion();
            } else {
              quizContainer.classList.add('hidden');
              resultContainer.classList.remove('hidden');
              scoreSpan.textContent = score;
            }
          }, 1500);
        };
        card.appendChild(btn);
      });

      quizContainer.appendChild(card);
    }

    renderQuestion();
  </script>
</body>
</html>
