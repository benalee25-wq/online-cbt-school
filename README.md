<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Excellentia Digital Academy - CBT</title>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f2f5f9;
  color: #222;
}

.header {
  background: #075e54;
  color: white;
  text-align: center;
  padding: 28px 15px;
  border-radius: 0 0 25px 25px;
}

.header h1 {
  margin: 0;
  font-size: 28px;
}

.header p {
  font-size: 18px;
  margin: 10px 0 0;
}

.container {
  max-width: 700px;
  margin: auto;
  padding: 20px;
}

.card {
  background: white;
  margin-top: 20px;
  padding: 28px;
  border-radius: 18px;
  box-shadow: 0 3px 15px rgba(0,0,0,0.08);
}

.hidden {
  display: none;
}

h2 {
  color: #075e54;
}

input,
select {
  width: 100%;
  padding: 15px;
  margin: 10px 0;
  border: 1px solid #ccc;
  border-radius: 9px;
  font-size: 17px;
}

button {
  width: 100%;
  padding: 15px;
  margin-top: 12px;
  border: none;
  border-radius: 9px;
  background: #075e54;
  color: white;
  font-size: 17px;
  cursor: pointer;
}

button:hover {
  background: #064c44;
}

.timer {
  background: #fff3cd;
  color: #856404;
  padding: 15px;
  border-radius: 10px;
  text-align: center;
  font-size: 21px;
  font-weight: bold;
  margin-bottom: 22px;
}

.subject-box {
  border: 2px solid #e0e0e0;
  padding: 18px;
  margin: 12px 0;
  border-radius: 12px;
  cursor: pointer;
  background: #fafafa;
}

.subject-box:hover {
  border-color: #075e54;
  background: #e8f5f3;
}

.question-number {
  color: #075e54;
  font-weight: bold;
  font-size: 18px;
}

.option {
  display: block;
  background: #f5f5f5;
  padding: 16px;
  margin: 11px 0;
  border-radius: 10px;
  cursor: pointer;
  font-size: 17px;
}

.option:hover {
  background: #e8f5f3;
}

.option input {
  width: auto;
  margin-right: 10px;
}

.result {
  text-align: center;
}

.score {
  font-size: 42px;
  font-weight: bold;
  color: #075e54;
}

.info {
  background: #e8f5f3;
  padding: 15px;
  border-radius: 10px;
  margin: 15px 0;
}
</style>
</head>

<body>

<div class="header">
  <h1>Excellentia Digital Academy</h1>
  <p>Computer Based Test (CBT)</p>
</div>

<div class="container">

<!-- STEP 1: STUDENT NAME -->

<div id="startPage" class="card">

  <h2>Welcome to the CBT</h2>

  <p>Please enter your full name to continue.</p>

  <input
    type="text"
    id="studentName"
    placeholder="Enter your full name"
  >

  <button onclick="continueToSubjects()">
    Continue
  </button>

</div>


<!-- STEP 2: SUBJECT SELECTION -->

<div id="subjectPage" class="card hidden">

  <h2>Select Your Subject</h2>

  <p>
    Welcome, <strong id="displayName"></strong>.
  </p>

  <div class="info">
    Select the subject you want to write.
  </div>

  <div class="subject-box" onclick="selectSubject('Mathematics')">
    📐 <strong>Mathematics</strong>
  </div>

  <div class="subject-box" onclick="selectSubject('English')">
    📖 <strong>English Language</strong>
  </div>

  <div class="subject-box" onclick="selectSubject('Biology')">
    🧬 <strong>Biology</strong>
  </div>

  <div class="subject-box" onclick="selectSubject('Chemistry')">
    ⚗️ <strong>Chemistry</strong>
  </div>

  <div class="subject-box" onclick="selectSubject('Physics')">
    ⚡ <strong>Physics</strong>
  </div>

  <div class="subject-box" onclick="selectSubject('Computer Studies')">
    💻 <strong>Computer Studies</strong>
  </div>

</div>


<!-- STEP 3: TEST -->

<div id="testPage" class="card hidden">

  <div class="info">
    <strong>Student:</strong>
    <span id="testStudent"></span>
    <br>
    <strong>Subject:</strong>
    <span id="testSubject"></span>
  </div>

  <div class="timer">
    Time Remaining:
    <span id="timer">10:00</span>
  </div>

  <div id="questionContainer"></div>

  <button onclick="nextQuestion()" id="nextButton">
    Next Question
  </button>

</div>


<!-- STEP 4: RESULT -->

<div id="resultPage" class="card result hidden">

  <h2>Test Completed!</h2>

  <p id="studentResult"></p>

  <p id="subjectResult"></p>

  <p>Your Score</p>

  <div class="score" id="score"></div>

  <p id="percentage"></p>

  <p id="message"></p>

  <button onclick="location.reload()">
    Take Another Test
  </button>

</div>

</div>


<script>

/* =========================
   QUESTIONS
========================= */

const questionBank = {

Mathematics: [

{
question: "What is 5 + 7?",
options: ["10", "11", "12", "13"],
answer: 2
},

{
question: "What is 10 × 5?",
options: ["15", "50", "55", "100"],
answer: 1
},

{
question: "What is half of 20?",
options: ["5", "10", "15", "20"],
answer: 1
},

{
question: "What is 100 ÷ 10?",
options: ["5", "10", "20", "50"],
answer: 1
},

{
question: "What is 9 × 9?",
options: ["72", "81", "90", "99"],
answer: 1
}

],

English: [

{
question: "Choose the correct spelling.",
options: [
"Beautifull",
"Beautiful",
"Beutiful",
"Beautifol"
],
answer: 1
},

{
question: "Which word is a noun?",
options: [
"Run",
"Beautiful",
"School",
"Quickly"
],
answer: 2
},

{
question: "Choose the opposite of 'Hot'.",
options: [
"Warm",
"Cold",
"Heat",
"Fire"
],
answer: 1
},

{
question: "Which word is a verb?",
options: [
"Jump",
"Table",
"Beautiful",
"House"
],
answer: 0
},

{
question: "Choose the correct sentence.",
options: [
"He are going home.",
"He is going home.",
"He am going home.",
"He be going home."
],
answer: 1
}

],

Biology: [

{
question: "What is the basic unit of life?",
options: [
"Tissue",
"Organ",
"Cell",
"Bone"
],
answer: 2
},

{
question: "Which organ pumps blood around the body?",
options: [
"Brain",
"Heart",
"Lung",
"Kidney"
],
answer: 1
},

{
question: "Plants make their food through?",
options: [
"Respiration",
"Digestion",
"Photosynthesis",
"Transpiration"
],
answer: 2
},

{
question: "Which organ is used for breathing?",
options: [
"Heart",
"Lung",
"Stomach",
"Brain"
],
answer: 1
},

{
question: "Which of these is a mammal?",
options: [
"Fish",
"Frog",
"Dog",
"Lizard"
],
answer: 2
}

],

Chemistry: [

{
question: "What is the chemical symbol for water?",
options: [
"CO2",
"H2O",
"O2",
"NaCl"
],
answer: 1
},

{
question: "What gas do humans breathe in?",
options: [
"Carbon dioxide",
"Oxygen",
"Nitrogen",
"Hydrogen"
],
answer: 1
},

{
question: "What is NaCl commonly called?",
options: [
"Sugar",
"Water",
"Salt",
"Acid"
],
answer: 2
},

{
question: "Which of these is an element?",
options: [
"Water",
"Oxygen",
"Salt",
"Sugar"
],
answer: 1
},

{
question: "What is the symbol for oxygen?",
options: [
"O",
"Ox",
"C",
"Og"
],
answer: 0
}

],

Physics: [

{
question: "What force pulls objects toward the Earth?",
options: [
"Friction",
"Gravity",
"Magnetism",
"Pressure"
],
answer: 1
},

{
question: "What is the SI unit of force?",
options: [
"Joule",
"Watt",
"Newton",
"Volt"
],
answer: 2
},

{
question: "Which device measures temperature?",
options: [
"Barometer",
"Thermometer",
"Speedometer",
"Voltmeter"
],
answer: 1
},

{
question: "Light travels fastest through?",
options: [
"Water",
"Glass",
"Air",
"Vacuum"
],
answer: 3
},

{
question: "What is the unit of electrical current?",
options: [
"Volt",
"Ampere",
"Watt",
"Ohm"
],
answer: 1
}

],

"Computer Studies": [

{
question: "What is the full meaning of CPU?",
options: [
"Central Processing Unit",
"Computer Personal Unit",
"Central Program Utility",
"Computer Processing Utility"
],
answer: 0
},

{
question: "Which device is used to type information?",
options: [
"Monitor",
"Keyboard",
"Speaker",
"Printer"
],
answer: 1
},

{
question: "Which is an output device?",
options: [
"Keyboard",
"Mouse",
"Monitor",
"Scanner"
],
answer: 2
},

{
question: "What does HTML stand for?",
options: [
"Hyper Text Markup Language",
"High Text Machine Language",
"Hyper Tool Markup Language",
"Home Text Markup Language"
],
answer: 0
},

{
question: "Which is a storage device?",
options: [
"Keyboard",
"Hard drive",
"Monitor",
"Mouse"
],
answer: 1
}

]

};


/* =========================
   VARIABLES
========================= */

let studentName = "";

let selectedSubject = "";

let questions = [];

let currentQuestion = 0;

let score = 0;

let timeLeft = 600;

let timerInterval;


/* =========================
   STUDENT NAME
========================= */

function continueToSubjects() {

studentName =
document.getElementById("studentName").value.trim();

if (studentName === "") {

alert("Please enter your full name.");

return;

}

document.getElementById("displayName").textContent =
studentName;

document.getElementById("startPage").classList.add("hidden");

document.getElementById("subjectPage").classList.remove("hidden");

}


/* =========================
   SELECT SUBJECT
========================= */

function selectSubject(subject) {

selectedSubject = subject;

questions = questionBank[subject];

currentQuestion = 0;

score = 0;

timeLeft = 600;

document.getElementById("subjectPage").classList.add("hidden");

document.getElementById("testPage").classList.remove("hidden");

document.getElementById("testStudent").textContent =
studentName;

document.getElementById("testSubject").textContent =
selectedSubject;

showQuestion();

timerInterval = setInterval(updateTimer, 1000);

}


/* =========================
   SHOW QUESTION
========================= */

function showQuestion() {

const q = questions[currentQuestion];

let html = `

<p class="question-number">
Question ${currentQuestion + 1}
of ${questions.length}
</p>

<h3>${q.question}</h3>

`;

q.options.forEach((option, index) => {

html += `

<label class="option">

<input
type="radio"
name="answer"
value="${index}"
>

${option}

</label>

`;

});

document.getElementById("questionContainer").innerHTML = html;

if (currentQuestion === questions.length - 1) {

document.getElementById("nextButton").textContent =
"Submit Test";

} else {

document.getElementById("nextButton").textContent =
"Next Question";

}

}


/* =========================
   NEXT QUESTION
========================= */

function nextQuestion() {

const selected =
document.querySelector(
'input[name="answer"]:checked'
);

if (!selected) {

alert("Please select an answer.");

return;

}

if (
parseInt(selected.value)
===
questions[currentQuestion].answer
) {

score++;

}

currentQuestion++;

if (currentQuestion < questions.length) {

showQuestion();

} else {

finishTest();

}

}


/* =========================
   TIMER
========================= */

function updateTimer() {

timeLeft--;

let minutes =
Math.floor(timeLeft / 60);

let seconds =
timeLeft % 60;

seconds =
seconds < 10
? "0" + seconds
: seconds;

document.getElementById("timer").textContent =
minutes + ":" + seconds;

if (timeLeft <= 0) {

finishTest();

}

}


/* =========================
   FINISH TEST
========================= */

function finishTest() {

clearInterval(timerInterval);

document.getElementById("testPage")
.classList.add("hidden");

document.getElementById("resultPage")
.classList.remove("hidden");

let percentage =
Math.round(
(score / questions.length) * 100
);

document.getElementById("studentResult").textContent =
"Student: " + studentName;

document.getElementById("subjectResult").textContent =
"Subject: " + selectedSubject;

document.getElementById("score").textContent =
score + " / " + questions.length;

document.getElementById("percentage").textContent =
"Percentage: " + percentage + "%";


if (percentage >= 70) {

document.getElementById("message").textContent =
"Excellent performance! Congratulations.";

}

else if (percentage >= 50) {

document.getElementById("message").textContent =
"Good effort. Keep studying and improving.";

}

else {

document.getElementById("message").textContent =
"Keep practicing. You can do better next time.";

}

}

</script>

</body>
</html>
