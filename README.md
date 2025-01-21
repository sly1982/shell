<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Matrix Effect</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            background: black;
            color: green;
            font-family: monospace;
            font-size: 18px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
        }
        canvas {
            position: absolute;
            top: 0;
            left: 0;
        }
        h1 {
            position: relative;
            color: white;
            font-size: 36px;
            font-weight: bold;
            z-index: 1;
            margin-bottom: 50px;
        }
        .button-container {
            position: relative;
            z-index: 1;
            display: grid;
            grid-template-columns: repeat(3, 60px);
            grid-gap: 10px;
            justify-content: center;
        }
        button {
            width: 50px;
            height: 50px;
            font-size: 20px;
            font-weight: bold;
            background-color: yellow;
            border: 2px solid red;
            cursor: pointer;
        }
        .result {
            position: relative;
            font-size: 24px;
            color: white;
            margin-top: 20px;
            z-index: 1;
        }
    </style>
</head>
<body>
    <canvas id="matrix"></canvas>
    <h1>VIVO ENERGY MAROC</h1>
    <div class="button-container" id="buttonContainer"></div>
    <div id="result" class="result"></div>

    <script>
        const canvas = document.getElementById('matrix');
        const ctx = canvas.getContext('2d');

        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        const letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789';
        const fontSize = 18;
        const columns = canvas.width / fontSize;
        const drops = Array(Math.floor(columns)).fill(1);

        function drawMatrix() {
            ctx.fillStyle = 'rgba(0, 0, 0, 0.05)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            ctx.fillStyle = 'red';
            ctx.font = `${fontSize}px monospace`;

            drops.forEach((y, x) => {
                const text = letters.charAt(Math.floor(Math.random() * letters.length));
                ctx.fillText(text, x * fontSize, y * fontSize);

                if (y * fontSize > canvas.height && Math.random() > 0.975) {
                    drops[x] = 0;
                }

                drops[x]++;
            });
        }

        setInterval(drawMatrix, 50);

        const buttonContainer = document.getElementById('buttonContainer');
        const result = document.getElementById('result');
        const correctCode = '526';
        let userInput = '';

        // Create buttons for digits 1-9 in a square layout
        for (let i = 1; i <= 9; i++) {
            const button = document.createElement('button');
            button.textContent = i;
            button.addEventListener('click', () => {
                if (userInput.length < 3) {
                    userInput += i;
                }
                if (userInput.length === 3) {
                    if (userInput === correctCode) {
                        result.textContent = 'CORRECT';
                        result.style.color = 'green';
                    } else {
                        result.textContent = 'ERREUR';
                        result.style.color = 'red';
                    }
                    userInput = ''; // Reset input
                }
            });
            buttonContainer.appendChild(button);
        }
    </script>
</body>
</html>
