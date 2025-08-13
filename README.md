# LK7-SCRIPTS-SITE




<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>LK7 Scripts</title>
<style>
    body {
        margin: 0;
        font-family: Arial, sans-serif;
        color: white;
        text-align: center;
        overflow: hidden;
    }

    canvas {
        position: fixed;
        top: 0;
        left: 0;
        z-index: -1;
    }

    .container {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 100vh;
    }

    .button {
        background-color: #333;
        border: none;
        color: white;
        padding: 20px 40px;
        font-size: 20px;
        cursor: pointer;
        border-radius: 8px;
        transition: background 0.3s;
    }

    .button:disabled {
        background-color: #555;
        cursor: not-allowed;
    }

    .button:hover:not(:disabled) {
        background-color: #555;
    }

    .hidden {
        display: none;
    }

    textarea {
        width: 80%;
        height: 150px;
        margin-top: 20px;
        border-radius: 8px;
        padding: 10px;
        font-size: 14px;
        resize: none;
    }

    .copy-btn {
        margin-top: 10px;
        padding: 10px 20px;
        background: #28a745;
        color: white;
        border: none;
        border-radius: 8px;
        cursor: pointer;
    }
</style>
</head>
<body>

<canvas id="stars"></canvas>

<div id="page1" class="container">
    <button class="button" onclick="goToAccess()">LK7 SCRIPTS</button>
</div>

<div id="page2" class="container hidden">
    <button id="accessBtn" class="button" disabled>GET ACCESS 00:10</button>
</div>

<div id="page3" class="container hidden">
    <h2>Seu Script</h2>
    <textarea id="scriptArea" readonly>loadstring(game:HttpGet("https://pastebin.com/raw/rf4N6ZLn"))()</textarea>
    <br>
    <button class="copy-btn" onclick="copyScript()">Copiar Script</button>
</div>

<script>
    // Fundo animado estilo Delta
    const canvas = document.getElementById("stars");
    const ctx = canvas.getContext("2d");
    let stars = [];

    function resizeCanvas() {
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
    }
    window.addEventListener("resize", resizeCanvas);
    resizeCanvas();

    function createStars() {
        stars = [];
        for (let i = 0; i < 150; i++) {
            stars.push({
                x: Math.random() * canvas.width,
                y: Math.random() * canvas.height,
                size: Math.random() * 2,
                speed: Math.random() * 0.5 + 0.2
            });
        }
    }

    function drawStars() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        ctx.fillStyle = "white";
        stars.forEach(star => {
            ctx.beginPath();
            ctx.arc(star.x, star.y, star.size, 0, Math.PI * 2);
            ctx.fill();
        });
    }

    function moveStars() {
        stars.forEach(star => {
            star.y += star.speed;
            if (star.y > canvas.height) {
                star.y = 0;
                star.x = Math.random() * canvas.width;
            }
        });
    }

    function animateStars() {
        drawStars();
        moveStars();
        requestAnimationFrame(animateStars);
    }

    createStars();
    animateStars();

    // Lógica do site
    function goToAccess() {
        document.getElementById("page1").classList.add("hidden");
        document.getElementById("page2").classList.remove("hidden");

        let timeLeft = 10;
        let btn = document.getElementById("accessBtn");

        let timer = setInterval(() => {
            timeLeft--;
            btn.textContent = `GET ACCESS 00:${timeLeft < 10 ? '0' : ''}${timeLeft}`;
            if (timeLeft <= 0) {
                clearInterval(timer);
                btn.textContent = "GET ACCESS";
                btn.disabled = false;
                btn.onclick = showScript;
            }
        }, 1000);
    }

    function showScript() {
        document.getElementById("page2").classList.add("hidden");
        document.getElementById("page3").classList.remove("hidden");
    }

    function copyScript() {
        let script = document.getElementById("scriptArea");
        script.select();
        document.execCommand("copy");
        alert("Script copiado!");
    }
</script>

</body>
</html>
