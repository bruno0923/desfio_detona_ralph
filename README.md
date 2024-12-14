# desfio_detona_ralph
Projeto Criando o jogo Detona Ralph 

<!-- index.html -->

<!DOCTYPE html>
<html lang="pt-br">
<head>

    <!-- setting -->

    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Detona Ralph</title>

<!-- fonts -->

    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap" rel="stylesheet">

<!----- styles ----->

    <link rel="stylesheet" href="./src/styles/reset.css">
    <link rel="stylesheet" href="./src/styles/main.css">
</head>
<body>
    
    <div class="container">
        <div class="menu">
            <div class="menu-time">
                <h2 style="color: red;">Time Left</h2>
                <h2>0</h2>
            </div>
            <div class="menu-score">
                <h2 style="color: red;">Your Score</h2>
                <h2 id="score">0</h2>  
            </div>
            <div class="menu-lives">
                <img src="./src/images/player.png" alt="foto do jogador" height="60px" />
                <h2>x3</h2>
            </div>

        </div>
    </div>

    <div class="panel">
        <div class="panel-row">
            <div class="square enemy" id="1"></div>
            <div class="square" id="2"></div>
            <div class="square" id="3"></div>
        </div>
    
        <div class="panel-row">
            <div class="square" id="4"></div>
            <div class="square" id="5"></div>
            <div class="square" id="6"></div>
        </div>

        <div class="panel-row">
            <div class="square" id="7"></div>
            <div class="square" id="8"></div>
            <div class="square" id="9"></div>
        </div>

    </div>
    <script defer src=".src/scripts/engine.js"></script>
</body>
</html>

<!-- main.css -->

.container {
    display: flex;
    flex-direction: column;
    height: 100vh;
    background-image: url("./images/wall.png");
}

.menu{
    display: flex;
    justify-content: space-evenly;
    align-items: center;

    height: 90px;
    width: 100%;
    background-color: #000000;
    color: #ffffff;
    border-bottom: 5px solid gold;
}

.panel{
    margin-top: 1rem;
    display: flex;
    align-items: center;
    justify-content: center;
}

.square{
    height: 150px;
    height: 150px;
    border: 1px solid black;
    background-color: #1aeaa5;
}

.enemy {
    background-image: url("../images/ralph.png");
    background-size: cover;
}

.menu-lives {
    display: flex;
    align-items: center;
    justify-content: center;
}

.menu-time h2:nth-child(2),
.menu-score h2:nth-child(2){
    margin-top: 40px;
}

<!-- engine.js -->

const state = {
    view: {
        squares: document.querySelectorAll(".square"),
        enemy: document.querySelectorAll(".enemy"),
        timeLeft: document.querySelector("#time-left"),
        score: document.querySelector("#score"),
    },
    values: {
        timeId: null,
        countdownTimerId: setInterval(countdown, 1000),
        gameVelocity: 1000,
        hitPosition: 0,
        result: 0,
        curretTime: 60,
    },

    actions: {
        timeId: setInterval(randomSqare, 1000),
        countdownTimerId: setInterval(countdown, 1000),
    }
};

function countdown(){
    state.values.curretTime--;
    state.view.timeLeft.textContent = state.values.curretTime;

    if (state.values.curretTime < 0) {
        clearInterval(state.actions.countdownTimerId);
        clearInterval(state.actions.TimerId);
        alert("Game Over! O seu resultado foi: " + state.value.result);
    }
}

function playSound(){
    let audio = new Audio("./src/audios/hit.m4a")
    audio.volume = 0.2;
    audio.play();

}

function randomSqare() {
    state.view.squares.forEach((square) =={
        square.classlist.remove("enemy");
    })

    let randomNumber = Math.floor(Math.random() * 9);
    let randomSqare = state.view.squares[randomNumber];
    randomSqare.classlist.add("enemy");
    state.values.hitPosition = randomSquare.id;
}

function moveEnemy(){
    state.values.timeId = setInterval(randomSquare, state.values.gameVelocity);
}

function addListenerHitBox() {
    state.squares.forEach((square) --> {
        square.addEventlistener("mousedown", () ==> {
            if(square.id === state.values.hitPosition){
                state.value.result++
                state.view.score.textContent = state.value.result;
                state.values.hitPosition = null;
                playSound();
            }
        });
    });
}

function  initialize() {
   moveEnemy();
   addListenerHitBox();
}

initialize();

