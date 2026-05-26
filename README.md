# EID-13


<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>بطاقة عيد مبارك - معهد البصائر</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Tajawal:wght@400;700;900&display=swap');
  
  * { margin: 0; padding: 0; box-sizing: border-box; }
  
  body {
    background: linear-gradient(135deg, #1a0533 0%, #3b1060 50%, #1a0533 100%);
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    font-family: 'Tajawal', sans-serif;
    padding: 20px;
  }

  h1 {
    color: #d4a0f0;
    font-size: 1.8rem;
    margin-bottom: 30px;
    text-align: center;
    text-shadow: 0 0 20px rgba(212,160,240,0.5);
    letter-spacing: 1px;
  }

  .card-wrapper {
    position: relative;
    width: 100%;
    max-width: 420px;
  }

  canvas {
    width: 100%;
    border-radius: 16px;
    box-shadow: 0 20px 60px rgba(0,0,0,0.6), 0 0 40px rgba(180,100,240,0.2);
    display: block;
  }

  .controls {
    margin-top: 24px;
    width: 100%;
    max-width: 420px;
    display: flex;
    flex-direction: column;
    gap: 14px;
  }

  .input-group {
    display: flex;
    gap: 10px;
    align-items: center;
  }

  input[type="text"] {
    flex: 1;
    padding: 14px 18px;
    border-radius: 12px;
    border: 2px solid rgba(180,100,240,0.5);
    background: rgba(255,255,255,0.08);
    color: white;
    font-family: 'Tajawal', sans-serif;
    font-size: 1.1rem;
    outline: none;
    transition: border-color 0.3s, background 0.3s;
    text-align: right;
    direction: rtl;
  }

  input[type="text"]::placeholder { color: rgba(255,255,255,0.4); }
  input[type="text"]:focus {
    border-color: #d4a0f0;
    background: rgba(255,255,255,0.12);
  }

  button {
    padding: 14px 22px;
    border-radius: 12px;
    border: none;
    cursor: pointer;
    font-family: 'Tajawal', sans-serif;
    font-size: 1rem;
    font-weight: 700;
    transition: all 0.3s;
  }

  .btn-apply {
    background: linear-gradient(135deg, #9b30d9, #c060f0);
    color: white;
    flex-shrink: 0;
  }
  .btn-apply:hover { transform: translateY(-2px); box-shadow: 0 8px 20px rgba(155,48,217,0.5); }

  .btn-download {
    width: 100%;
    background: linear-gradient(135deg, #1a4a8a, #2a6ab5);
    color: white;
    font-size: 1.1rem;
    padding: 16px;
    letter-spacing: 0.5px;
  }
  .btn-download:hover { transform: translateY(-2px); box-shadow: 0 8px 25px rgba(26,74,138,0.5); }
  .btn-download:disabled { opacity: 0.5; cursor: not-allowed; transform: none; }

  .hint {
    color: rgba(255,255,255,0.45);
    font-size: 0.85rem;
    text-align: center;
  }

  .color-group {
    display: flex;
    align-items: center;
    gap: 12px;
  }

  .color-group label {
    color: rgba(255,255,255,0.8);
    font-family: 'Tajawal', sans-serif;
    font-size: 1rem;
    flex: 1;
  }

  input[type="color"] {
    width: 50px;
    height: 40px;
    border-radius: 8px;
    border: 2px solid rgba(180,100,240,0.5);
    background: none;
    cursor: pointer;
    padding: 2px;
  }
</style>
</head>
<body>

<h1>✨ بطاقة عيد مبارك ✨</h1>

<div class="card-wrapper">
  <canvas id="canvas"></canvas>
</div>

<div class="controls">
  <div class="input-group">
    <input type="text" id="nameInput" placeholder="اكتب اسمك هنا..." maxlength="40" />
    <button class="btn-apply" onclick="drawCard()">تطبيق</button>
  </div>
  <div class="color-group">
    <label>لون الخط:</label>
    <input type="color" id="textColor" value="#3b1060" oninput="drawCard()" />
  </div>
  <button class="btn-download" id="dlBtn" onclick="downloadCard()" disabled>⬇️ تحميل البطاقة</button>
  <p class="hint">اكتب اسمك واضغط تطبيق ثم حمّل البطاقة</p>
</div>

<script>
const canvas = document.getElementById('canvas');
const ctx = canvas.getContext('2d');
const img = new Image();

img.src = "       <a href="https://ibb.co/hJvxZwgg"><img src="https://i.ibb.co/ZpCRY7ff/Whats-App-Image-2026-05-26-at-4-43-08-PM-1779817492163.png" alt="Whats-App-Image-2026-05-26-at-4-43-08-PM-1779817492163" border="0"></a>";

img.onload = () => {
  canvas.width = img.width;
  canvas.height = img.height;
  if (document.fonts && document.fonts.ready) {
    document.fonts.ready.then(() => drawCard());
  } else {
    drawCard();
  }
};

function applyText(name, fontStr) {
  ctx.drawImage(img, 0, 0);
  const x = canvas.width / 2;
  // Position text inside the rectangular frame area (about 78% down)
  const y = canvas.height * 0.71;
  ctx.shadowColor = 'rgba(0,0,0,0.3)';
  ctx.shadowBlur = 8;
  ctx.shadowOffsetX = 1;
  ctx.shadowOffsetY = 1;
  ctx.fillStyle = document.getElementById('textColor').value;
  ctx.font = fontStr;
  ctx.textAlign = 'center';
  ctx.textBaseline = 'middle';
  ctx.direction = 'rtl';
  ctx.fillText(name, x, y);
  ctx.shadowColor = 'transparent';
  ctx.shadowBlur = 0;
  document.getElementById('dlBtn').disabled = false;
}

function drawCard() {
  const name = document.getElementById('nameInput').value.trim();
  ctx.drawImage(img, 0, 0);

  if (!name) {
    document.getElementById('dlBtn').disabled = false;
    return;
  }

  const fontSize = Math.round(canvas.width * 0.058);
  const fontStr = `bold ${fontSize}px 'Tajawal', Arial`;

  if (document.fonts && document.fonts.load) {
    document.fonts.load(fontStr, name)
      .then(() => applyText(name, fontStr))
      .catch(() => applyText(name, `bold ${fontSize}px Arial`));
  } else {
    applyText(name, fontStr);
  }
}

function downloadCard() {
  const name = document.getElementById('nameInput').value.trim() || 'بطاقة-عيد';
  const link = document.createElement('a');
  link.download = `عيد-مبارك-${name}.png`;
  link.href = canvas.toDataURL('image/png');
  link.click();
}

document.getElementById('nameInput').addEventListener('keydown', e => {
  if (e.key === 'Enter') drawCard();
});
</script>
</body>
</html>
