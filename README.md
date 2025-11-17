# Food-game
<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<title>Bạn nên ăn gì? (Món Singapore)</title>
<style>
  body {
    font-family: Arial, sans-serif;
    text-align: center;
    padding: 20px;
    background-color: #fffbe6;
  }
  h1 { margin-bottom: 20px; }
  .board {
    display: grid;
    grid-template-columns: repeat(4, 120px);
    grid-gap: 10px;
    justify-content: center;
  }
  .card {
    width: 120px;
    height: 120px;
    background-color: #ff7043;
    border-radius: 10px;
    cursor: pointer;
    background-size: cover;
    background-position: center;
    transition: transform 0.3s;
  }
  .flipped { transform: rotateY(180deg); }
</style>
</head>
<body>

<h1>Bạn nên ăn gì? (Món Singapore)</h1>
<p>Lật 2 lá bài giống nhau để nhận gợi ý món ăn!</p>
<div class="board" id="board"></div>
<p id="message"></p>

<script>
// 4 món ăn Singapore, mỗi món 2 lá bài, link ảnh từ Postimages.org (hoạt động trên Sites)
let cards = [
  'https://i.postimg.cc/3Rz7vW1X/hainanese-chicken-rice.jpg', // Hainanese Chicken Rice
  'https://i.postimg.cc/3Rz7vW1X/hainanese-chicken-rice.jpg',
  'https://i.postimg.cc/5NfJrJHq/chili-crab.jpg', // Chili Crab
  'https://i.postimg.cc/5NfJrJHq/chili-crab.jpg',
  'https://i.postimg.cc/3N6D3y5q/laksa.jpg', // Laksa
  'https://i.postimg.cc/3N6D3y5q/laksa.jpg',
  'https://i.postimg.cc/bvLv7h2B/satay.jpg', // Satay
  'https://i.postimg.cc/bvLv7h2B/satay.jpg'
];

// Trộn bài
cards.sort(() => 0.5 - Math.random());

const board = document.getElementById('board');
const message = document.getElementById('message');
let flippedCards = [];
let matchedCards = [];

function createBoard() {
  for (let i = 0; i < cards.length; i++) {
    const card = document.createElement('div');
    card.classList.add('card');
    card.dataset.value = cards[i];
    card.addEventListener('click', flipCard);
    board.appendChild(card);
  }
}

function flipCard() {
  if (flippedCards.length < 2 && !this.classList.contains('flipped')) {
    this.classList.add('flipped');
    this.style.backgroundImage = `url('${this.dataset.value}')`;
    flippedCards.push(this);

    if (flippedCards.length === 2) setTimeout(checkMatch, 800);
  }
}

function checkMatch() {
  const [card1, card2] = flippedCards;
  if (card1.dataset.value === card2.dataset.value) {
    matchedCards.push(card1, card2);
    message.textContent = `Bạn tìm thấy cặp món ăn! 🎉`;
  } else {
    card1.classList.remove('flipped');
    card2.classList.remove('flipped');
    card1.style.backgroundImage = '';
    card2.style.backgroundImage = '';
    message.textContent = `Không trùng! Thử lại.`;
  }
  flippedCards = [];

  if (matchedCards.length === cards.length) {
    message.textContent = `Chúc mừng! Bạn đã ghép hết các món ăn Singapore! 🎉`;
  }
}

createBoard();
</script>

</body>
</html>
