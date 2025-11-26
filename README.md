# GRATTEUX
AFE EN FOLIE
<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<title>Ticket gagnant</title>
<style>
  body {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
    font-family: Arial, sans-serif;
    /* Fond quadrillé rouge et jaune */
    background: repeating-linear-gradient(
      90deg,
      red 0px,
      red 40px,
      yellow 40px,
      yellow 80px
    ),
    repeating-linear-gradient(
      0deg,
      red 0px,
      red 40px,
      yellow 40px,
      yellow 80px
    );
  }
  h1 {
    font-size: 42px;
    margin-bottom: 30px;
    color: #8B0000;
    text-shadow: 2px 2px 6px rgba(0,0,0,0.4);
  }
  #scratchCard {
    position: relative;
    width: 420px;
    height: 280px;
    background: #fff;
    border-radius: 16px;
    box-shadow: 0 6px 14px rgba(0,0,0,0.25);
    overflow: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    font-weight: bold;
    color: #000;
    font-size: 60px;
    line-height: 1.2;
  }
  canvas {
    position: absolute;
    top: 0;
    left: 0;
    cursor: crosshair;
    z-index: 2; /* assure que le doré est au-dessus */
  }
</style>
</head>
<body>
  <h1>**** AFE EN FOLIE ****</h1>
  <div id="scratchCard">
    2:02<br>BRAVO
    <canvas id="scratchLayer"></canvas>
  </div>

<script>
const canvas = document.getElementById('scratchLayer');
const ctx = canvas.getContext('2d');
const card = document.getElementById('scratchCard');

window.onload = () => {
  canvas.width = card.offsetWidth;
  canvas.height = card.offsetHeight;
  ctx.fillStyle = '#FFD700'; // Doré
  ctx.fillRect(0, 0, canvas.width, canvas.height);
};

let isDrawing = false;

function scratch(e) {
  if (!isDrawing) return;
  const rect = canvas.getBoundingClientRect();
  const x = (e.touches ? e.touches[0].clientX : e.clientX) - rect.left;
  const y = (e.touches ? e.touches[0].clientY : e.clientY) - rect.top;
  ctx.globalCompositeOperation = 'destination-out';
  ctx.beginPath();
  ctx.arc(x, y, 25, 0, Math.PI * 2);
  ctx.fill();
}

canvas.addEventListener('mousedown', () => isDrawing = true);
canvas.addEventListener('mouseup', () => isDrawing = false);
canvas.addEventListener('mousemove', scratch);

canvas.addEventListener('touchstart', () => isDrawing = true);
canvas.addEventListener('touchend', () => isDrawing = false);
canvas.addEventListener('touchmove', scratch);
</script>
</body>
</html>
