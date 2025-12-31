# index.html<!DOCTYPE html>
<html lang="ro">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Joc Animale Distractiv</title>
<style>
  body { font-family: Arial; text-align: center; background: #ccf2ff; padding: 20px; }
  h1 { color: #2e8b57; font-size: 36px; }
  button { padding: 15px 25px; margin: 10px; font-size: 20px; cursor: pointer; border-radius: 15px; border: none; background: #ffcc00; transition: 0.3s; }
  button:hover { background: #ffdd33; transform: scale(1.1); }
  #animal-img { width: 250px; height: 250px; margin: 20px auto; border-radius: 20px; border: 3px solid #2e8b57; }
  #feedback { font-size: 24px; color: #ff4500; margin-top: 10px; min-height: 30px; }
</style>
</head>
<body>

<h1>Joc Animale 🐶🐱🦁🦒</h1>
<img id="animal-img" src="" alt="Animal">
<div id="question"></div>
<div id="options"></div>
<div id="feedback"></div>

<audio id="animal-sound"></audio>

<script>
const animals = [
  { name: "Pisică", soundUrl: "https://www.soundjay.com/cat-sound.mp3", img: "https://i.imgur.com/1ZQZ1Zm.png" },
  { name: "Câine", soundUrl: "https://www.soundjay.com/dog-sound.mp3", img: "https://i.imgur.com/4AiXzf8.png" },
  { name: "Elefant", soundUrl: "https://www.soundjay.com/elephant-sound.mp3", img: "https://i.imgur.com/3WcG1X0.png" },
  { name: "Cangur", soundUrl: "https://www.soundjay.com/kangaroo-sound.mp3", img: "https://i.imgur.com/yLqkF3h.png" },
  { name: "Pește", soundUrl: "https://www.soundjay.com/fish-sound.mp3", img: "https://i.imgur.com/Q8dH6Bb.png" },
  { name: "Leu", soundUrl: "https://www.soundjay.com/lion-roar.mp3", img: "https://i.imgur.com/N4h2b0y.png" },
  { name: "Urs", soundUrl: "https://www.soundjay.com/bear-sound.mp3", img: "https://i.imgur.com/XoJZK4v.png" },
  { name: "Papagal", soundUrl: "https://www.soundjay.com/parrot-sound.mp3", img: "https://i.imgur.com/GtLQK3D.png" },
  { name: "Vulpe", soundUrl: "https://www.soundjay.com/fox-sound.mp3", img: "https://i.imgur.com/8h2N6lP.png" },
  { name: "Girafă", soundUrl: "https://www.soundjay.com/giraffe-sound.mp3", img: "https://i.imgur.com/HJtAqQd.png" }
];

const questions = [
  { question: "Ce animal face 'miau'?", answer: "Pisică", options: ["Câine","Pisică","Elefant","Cangur"] },
  { question: "Ce animal face 'ham ham'?", answer: "Câine", options: ["Câine","Pește","Cangur","Elefant"] },
  { question: "Care animal are trompă?", answer: "Elefant", options: ["Câine","Elefant","Pisică","Pește"] },
  { question: "Ce animal sare foarte sus și are buzunar?", answer: "Cangur", options: ["Pește","Cangur","Pisică","Elefant"] },
  { question: "Ce animal trăiește în apă și are solzi?", answer: "Pește", options: ["Pește","Câine","Elefant","Pisică"] },
  { question: "Ce animal este regele junglei?", answer: "Leu", options: ["Leu","Urs","Câine","Girafă"] },
  { question: "Ce animal iubește mierea și trăiește în pădure?", answer: "Urs", options: ["Leu","Urs","Papagal","Pisică"] },
  { question: "Ce animal poate vorbi imitând sunete?", answer: "Papagal", options: ["Vulpe","Papagal","Pește","Cangur"] },
  { question: "Ce animal este roșcat și viclean?", answer: "Vulpe", options: ["Vulpe","Leu","Câine","Elefant"] },
  { question: "Ce animal are gât foarte lung?", answer: "Girafă", options: ["Girafă","Leu","Pisică","Urs"] }
];

let currentQuestion;

function speak(text) {
  const utterance = new SpeechSynthesisUtterance(text);
  speechSynthesis.speak(utterance);
}

function newQuestion() {
  currentQuestion = questions[Math.floor(Math.random() * questions.length)];
  const animalData = animals.find(a => a.name === currentQuestion.answer);

  document.getElementById('animal-img').src = animalData.img;
  document.getElementById('question').innerText = currentQuestion.question;
  speak(currentQuestion.question);

  const audio = document.getElementById('animal-sound');
  audio.src = animalData.soundUrl;
  audio.play();

  let optionsHtml = '';
  currentQuestion.options.forEach(option => {
    optionsHtml += `<button onclick="checkAnswer('${option}')">${option}</button>`;
  });
  document.getElementById('options').innerHTML = optionsHtml;
  document.getElementById('feedback').innerText = '';
}

function checkAnswer(selected) {
  if(selected === currentQuestion.answer){
    document.getElementById('feedback').innerText = `🌟 Corect! Este ${currentQuestion.answer} 🌟`;
    speak(`Corect! Este ${currentQuestion.answer}`);
  } else {
    document.getElementById('feedback').innerText = `Ups! 😅 Este ${currentQuestion.answer}`;
    speak(`Ups! 😅 Este ${currentQuestion.answer}`);
  }
  setTimeout(newQuestion, 2500);
}

newQuestion();
</script>

</body>
</html>
