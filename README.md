<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Quiz Play Guima</title>
<style>
    body {
        margin: 0;
        background: #111;
        color: #fff;
        font-family: Arial, sans-serif;
        text-align: center;
        user-select: none;
    }
    #quiz, #gameover {
        display: none;
        padding: 20px;
    }
    .btn {
        padding: 12px 20px;
        background: #2ecc71;
        color: #000;
        cursor: pointer;
        margin-top: 20px;
        border-radius: 6px;
        font-weight: bold;
        border: none;
        font-size: 18px;
    }
    #gameover img {
        width: 250px;
        border-radius: 12px;
        margin-top: 20px;
    }
</style>
</head>
<body>

<div id="quiz">
    <h2 id="counter">Pergunta 1 / 50</h2>
    <h1 id="question">Carregando...</h1>
    <div id="answers"></div>
</div>

<div id="gameover">
    <h1>GAME OVER</h1>
    <img src="guima_calva.png" alt="Guima Calva" />
    <br>
    <button class="btn" onclick="restart()">EU SOU CALVA E CLT E VOU COMEÇAR DE NOVO</button>
</div>

<audio id="failSound" src="cortando_cabelo.mp3"></audio>

<script>
const quizEl = document.getElementById("quiz");
const gameoverEl = document.getElementById("gameover");
const counterEl = document.getElementById("counter");
const questionEl = document.getElementById("question");
const answersEl = document.getElementById("answers");
const failSound = document.getElementById("failSound");

let index = 0;

const perguntas = [
    { q: "Quantos vídeos a Play Guima já postou?", a: ["100", "200", "300", "Pessoas demais fugiram antes de contar"], c: 3 },
    { q: "Qual a comida favorita da Guima?", a: ["Arroz", "Bala fine", "Pizza", "Depende do dia"], c: 1 },
    { q: "Qual é a cor mais aleatória que a Guima já usou?", a: ["Laranja radioativo", "Azul triste", "Roxo tóxico", "Todas"], c: 3 },
    { q: "Qual objeto a Guima mais perdeu em live?", a: ["Celular", "Prendedor", "Peruca", "Cabo do carregador"], c: 2 },
    { q: "Se a Guima fosse um Pokémon, qual seria o tipo?", a: ["Fada", "Psíquico", "Bug", "Caótico"], c: 3 },
    { q: "O que a Play Guima mais gosta de fazer?", a: ["Gravar", "Rir", "Bagunça", "Todas"], c: 3 },
    { q: "Qual item a Guima já quebrou sem querer?", a: ["O mouse", "A luz", "O tripé", "Mais de um"], c: 3 },
    { q: "Quantas Guimas são necessárias pra arrumar um quarto?", a: ["1", "2", "8", "Ainda não descobriram"], c: 3 },
    { q: "Qual é o bordão secreto da Guima?", a: ["oiii gente", "hmmm", "não sei não", "Todos"], c: 3 },
    { q: "Em que ano a Guima dominou a internet?", a: ["2020", "2021", "2023", "Ela sempre dominou"], c: 3 },
    // 40 placeholders
    ...Array.from({ length: 40 }).map((_, i) => ({
        q: `Pergunta impossível número ${i+11}: quantos fios de cabelo a Guima perdeu hoje?`,
        a: ["0", "7", "42", "Todos os que estavam na foto dela calva"],
        c: 3
    }))
];

function loadQuestion() {
    if (index >= perguntas.length) index = 0;

    quizEl.style.display = "block";
    gameoverEl.style.display = "none";

    const p = perguntas[index];
    questionEl.textContent = p.q;
    counterEl.textContent = `Pergunta ${index + 1} / ${perguntas.length}`;

    answersEl.innerHTML = "";
    p.a.forEach((alt, i) => {
        const btn = document.createElement("button");
        btn.textContent = alt;
        btn.className = "btn";
        btn.onclick = () => check(i);
        answersEl.appendChild(btn);
    });
}

function check(i) {
    if (i !== perguntas[index].c) {
        failSound.play();
        quizEl.style.display = "none";
        gameoverEl.style.display = "block";
        return;
    }
    index++;
    loadQuestion();
}

function restart() {
    index = 0;
    loadQuestion();
}

window.onload = loadQuestion;
</script>

</body>
</html>
