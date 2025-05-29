<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Ehsan's Dino Game</title>
<style>
  body {
    font-family: Arial, sans-serif;
    text-align: center;
    margin: 0; padding: 0;
    background: #f0f0f0;
  }
  h1 {
    margin-top: 20px;
  }
  #game {
    position: relative;
    margin: 30px auto;
    width: 600px;
    height: 150px;
    background: #fff;
    border: 2px solid #333;
    overflow: hidden;
  }
  #dino {
    position: absolute;
    bottom: 0;
    left: 50px;
    width: 40px;
    height: 40px;
    background: #444;
    border-radius: 5px;
  }
  #obstacle {
    position: absolute;
    bottom: 0;
    right: 0;
    width: 20px;
    height: 40px;
    background: #888;
    border-radius: 2px;
    animation: moveObstacle 2s linear infinite;
  }
  @keyframes moveObstacle {
    from { right: 0; }
    to { right: 100%; }
  }
  .jump {
    animation: jumpDino 0.5s ease;
  }
  @keyframes jumpDino {
    0% { bottom: 0; }
    50% { bottom: 80px; }
    100% { bottom: 0; }
  }
  #score {
    font-weight: bold;
    margin-top: 10px;
  }
</style>
</head>
<body>

<h1>Hi, I'm Ehsan 👋</h1>

<div id="game">
  <div id="dino"></div>
  <div id="obstacle"></div>
</div>

<div id="score">Score: 0</div>

<script>
  const dino = document.getElementById('dino');
  const obstacle = document.getElementById('obstacle');
  const scoreEl = document.getElementById('score');
  let score = 0;
  let isJumping = false;

  function jump() {
    if (isJumping) return;
    isJumping = true;
    dino.classList.add('jump');
    setTimeout(() => {
      dino.classList.remove('jump');
      isJumping = false;
    }, 500);
  }

  document.addEventListener('keydown', (e) => {
    if (e.code === 'Space' || e.code === 'ArrowUp') {
      jump();
    }
  });

  // Collision detection and score
  setInterval(() => {
    const dinoBottom = parseInt(window.getComputedStyle(dino).getPropertyValue('bottom'));
    const obstacleRight = parseInt(window.getComputedStyle(obstacle).getPropertyValue('right'));

    // If obstacle is near dino horizontally
    if (obstacleRight > 480 && obstacleRight < 520 && dinoBottom < 40) {
      alert('Game Over! Your score: ' + score);
      score = 0;
      scoreEl.textContent = 'Score: ' + score;
    } else if (obstacleRight === 0) {
      score++;
      scoreEl.textContent = 'Score: ' + score;
    }
  }, 50);
</script>

</body>
</html>
