const gameBoard = document.getElementById("gameBoard");
const timerDisplay = document.getElementById("timer");
const scoreDisplay = document.getElementById("score");
const restartBtn = document.getElementById("restart");

const symbols = ["🍎","🍌","🍇","🍒","🍉","🥝","🍍","🍓"];

let cards = [...symbols, ...symbols];
let flippedCards = [];
let matchedPairs = 0;
let score = 0;
let timer = 0;
let interval;

function shuffleCards() {
    cards.sort(() => Math.random() - 0.5);
}

function startTimer() {
    clearInterval(interval);
    timer = 0;
    timerDisplay.textContent = timer;

    interval = setInterval(() => {
        timer++;
        timerDisplay.textContent = timer;
    }, 1000);
}

function createBoard() {
    gameBoard.innerHTML = "";
    shuffleCards();

    cards.forEach(symbol => {
        const card = document.createElement("div");
        card.classList.add("card");
        card.dataset.symbol = symbol;
        card.textContent = symbol;

        card.addEventListener("click", flipCard);

        gameBoard.appendChild(card);
    });
}

function flipCard() {
    if (
        this.classList.contains("flip") ||
        this.classList.contains("matched") ||
        flippedCards.length === 2
    ) {
        return;
    }

    this.classList.add("flip");
    flippedCards.push(this);

    if (flippedCards.length === 2) {
        checkMatch();
    }
}

function checkMatch() {
    const [card1, card2] = flippedCards;

    if (card1.dataset.symbol === card2.dataset.symbol) {
        card1.classList.add("matched");
        card2.classList.add("matched");

        matchedPairs++;
        score += 10;
        scoreDisplay.textContent = score;

        flippedCards = [];

        if (matchedPairs === symbols.length) {
            clearInterval(interval);

            setTimeout(() => {
                alert(
                    `🎉 You Won!\nScore: ${score}\nTime: ${timer} seconds`
                );
            }, 500);
        }
    } else {
        setTimeout(() => {
            card1.classList.remove("flip");
            card2.classList.remove("flip");
            flippedCards = [];
        }, 1000);
    }
}

function restartGame() {
    matchedPairs = 0;
    score = 0;
    flippedCards = [];

    scoreDisplay.textContent = score;

    createBoard();
    startTimer();
}

restartBtn.addEventListener("click", restartGame);

createBoard();
startTimer();
