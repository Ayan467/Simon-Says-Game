# Simon-Says-Game
Project using  HTML CSS  &amp; JS
#HTML CODE

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Simon Says Game</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <h1>Simon Says Game</h1>
  <h2>Press any key to start the game</h2>

  <div class="btn-contrainer">
    <div class="line-one">
    <div class="btn red" type="button" id="red">1</div>
    <div class="btn yellow" type="button" id="yellow">2</div>
    </div>
    <div class="line-two">
    <div class="btn green" type="button" id="green">3</div>
    <div class="btn purple" type="button" id="purple">4</div>
    </div>
  </div>


  <script src="index.js"></script>
</body>
</html>



#CSS CODE

body {
    text-align: center;
}
.btn {
    height: 200px;
    width: 200px;
    border-radius: 20%;
    border: 10px solid black;
    margin: 2rem;
}

.btn-contrainer {
    display: flex;
    justify-content: center;
}
.yellow {
    background-color: #f99b45;
}
.red {
    background-color: #d95980;
}
.purple {
    background-color: #819ff9;
}
.green {
    background-color: #63aac0;
}

.flash {
    background-color: white;
}
.userflash {
    background-color: green;
}


#JS CODE

let gameSeq=[];
let userSeq=[];
let btns = ["yellow","red","purple","green"];
let started = false;
let level = 0;
let h2 = document.querySelector("h2");

document.addEventListener("keypress", function () {
       if (started == false) {
        console.log("game is started");
        started = true;

        levelUp();
       }
});

function gameFlash(btn) {
    btn.classList.add("flash");
    setTimeout(function() {
        btn.classList.remove("flash");
    }, 260);
}


function userFlash(btn) {
    btn.classList.add("userflash");
    setTimeout(function() {
        btn.classList.remove("userflash");
    }, 260);
}

function levelUp() {
    userSeq = [];
    level++;
    h2.innerText = `Level ${level}`;
    let randIdx = Math.floor(Math.random() * 3);
    let randColor = btns[randIdx];
    let randBtn = document.querySelector(`.${randColor}`);
    // console.log(randIdx);
    // console.log(randColor);
    // console.log(randBtn);
    gameSeq.push(randColor);
    console.log(gameSeq);
    gameFlash(randBtn);
}

function checkAns(idx) {
    if (userSeq[idx] === gameSeq[idx]) {
        if(userSeq.length == gameSeq.length) {
            setTimeout(levelUp, 1000);
        }
    } else {
        h2.innerHTML =`Game Over! Your Score was <b>${level}</b> <br> Press any key to start.`;
        document.querySelector("body").style.backgroundColor = "red";
        setTimeout(function () {
         document.querySelector("body").style.backgroundColor = "white";
        }, 150);

        reset();
    }

}



function btnPress() {
   
    let btn = this;
    userFlash(btn);

    userColor = btn.getAttribute("id");
    userSeq.push(userColor);

    checkAns(userSeq.length-1);
}


let allBtns = document.querySelectorAll(".btn");
for (btn of allBtns) {
    btn.addEventListener("click", btnPress);
}

function reset() {
    started = false;
    gameSeq = [];
    userSeq = [];
    level = 0;
}

