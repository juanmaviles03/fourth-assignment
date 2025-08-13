const questions = [
  {
    question: "Which of the following is NOT a valid JavaScript data type?",
    answers: [
      { text: "Boolean", correct: false },
      { text: "Number", correct: false },
      { text: "String", correct: false },
      { text: "Character", correct: true } // Not a JS type
    ]
  },
  {
    question: "What is the correct way to check strict equality in JavaScript?",
    answers: [
      { text: "if (i === 5)", correct: true },
      { text: "if (i == 5)", correct: false },
      { text: "if i = 5", correct: false },
      { text: "if i === 5 then", correct: false }
    ]
  },
  {
    question: "Which of the following is a valid block comment in JavaScript?",
    answers: [
      { text: "// This is a single-line comment", correct: false },
      { text: "/* This is a comment */", correct: true },
      { text: "<!-- This is a comment -->", correct: false },
      { text: "# This is a single-line comment", correct: false }
    ]
  },
  {
    question: "Which keyword is used to declare a variable in JavaScript?",
    answers: [
      { text: "let", correct: false },
      { text: "const", correct: false },
      { text: "var", correct: false },
      { text: "All of the above", correct: true }
    ]
  },
  {
    question: "What is the purpose of addEventListener() in JavaScript?",
    answers: [
      { text: "To create a new event.", correct: false },
      { text: "To prevent the default action of an event.", correct: false },
      { text: "To attach an event handler to a specified element.", correct: true },
      { text: "To remove an event listener from an element.", correct: false }
    ]
  }
];

const questionEl     = document.getElementById("question");
const answerButtons  = document.getElementById("answer-buttons");
const nextBtn        = document.getElementById("next-btn");
const progressEl     = document.getElementById("progress");

let currentQuestionIndex = 0;
let score = 0;

function startQuiz() {
  currentQuestionIndex = 0;
  score = 0;
  setNextButtonMode("next", "Next");
  showQuestion();
}

function setNextButtonMode(mode, label) {
  nextBtn.dataset.action = mode; // 'next' | 'score' | 'restart'
  nextBtn.textContent = label;
}

function showQuestion() {
  resetState();

  const current = questions[currentQuestionIndex];
  questionEl.textContent = current.question;
  progressEl.textContent = `Question ${currentQuestionIndex + 1} of ${questions.length}`;

  current.answers.forEach(answer => {
    const btn = document.createElement("button");
    btn.type = "button";
    btn.textContent = answer.text;
    btn.className = "btn";
    if (answer.correct) {
      btn.dataset.correct = "true"; // store as string for dataset
    }
    btn.addEventListener("click", selectAnswer, { once: true });
    answerButtons.appendChild(btn);
  });
}

function resetState() {
  nextBtn.style.display = "none";
  // clear old answers
  while (answerButtons.firstChild) answerButtons.removeChild(answerButtons.firstChild);
}

function selectAnswer(e) {
  const selectedBtn = e.target;
  const isCorrect = selectedBtn.dataset.correct === "true";
  if (isCorrect) score++;

  // Lock UI and show correctness
  Array.from(answerButtons.children).forEach(btn => {
    btn.disabled = true;
    if (btn.dataset.correct === "true") {
      btn.classList.add("correct");
    } else {
      btn.classList.add("wrong");
    }
  });

  // Decide next button label/mode
  if (currentQuestionIndex < questions.length - 1) {
    setNextButtonMode("next", "Next");
  } else {
    setNextButtonMode("score", "Show Score");
  }
  nextBtn.style.display = "inline-block";
}

// Single handler for all next/restart behavior
nextBtn.addEventListener("click", () => {
  const action = nextBtn.dataset.action;
  if (action === "next") {
    currentQuestionIndex++;
    showQuestion();
  } else if (action === "score") {
    showScore();
  } else if (action === "restart") {
    startQuiz();
  }
});

function showScore() {
  resetState();
  questionEl.textContent = `You scored ${score} out of ${questions.length}!`;
  progressEl.textContent = "";
  setNextButtonMode("restart", "Restart Quiz");
  nextBtn.style.display = "inline-block";
}

startQuiz();