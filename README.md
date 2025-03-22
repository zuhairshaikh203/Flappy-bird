# Flappy-bird
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Flappy Bird</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            background: skyblue;
        }
        canvas {
            display: block;
        }
    </style>
</head>
<body>
    <canvas id="gameCanvas"></canvas>
    <script>
        const canvas = document.getElementById("gameCanvas");
        const ctx = canvas.getContext("2d");

        canvas.width = 800;
        canvas.height = 500;

        const bird = {
            x: 100,
            y: canvas.height / 2,
            width: 30,
            height: 30,
            gravity: 0.6,
            lift: -10,
            velocity: 0
        };

        const pipes = [];
        const pipeWidth = 50;
        const pipeGap = 150;
        let frame = 0;
        let score = 0;
        let highScore = localStorage.getItem("highScore") || 0;

        function drawBird() {
            ctx.fillStyle = "yellow";
            ctx.fillRect(bird.x, bird.y, bird.width, bird.height);
        }

        function drawPipes() {
            ctx.fillStyle = "green";
            pipes.forEach(pipe => {
                ctx.fillRect(pipe.x, 0, pipeWidth, pipe.topHeight);
                ctx.fillRect(pipe.x, pipe.topHeight + pipeGap, pipeWidth, canvas.height - pipe.topHeight - pipeGap);
            });
        }

        function drawBackground() {
            ctx.fillStyle = "white";
            for (let i = 0; i < 5; i++) {
                ctx.beginPath();
                ctx.arc(100 + i * 150, 50, 20, 0, Math.PI * 2);
                ctx.arc(120 + i * 150, 60, 25, 0, Math.PI * 2);
                ctx.arc(140 + i * 150, 50, 20, 0, Math.PI * 2);
                ctx.fill();
            }
        }

        function drawScore() {
            ctx.fillStyle = "black";
            ctx.font = "20px Arial";
            ctx.fillText(`Score: ${score}`, 20, 30);
            ctx.fillText(`High Score: ${highScore}`, 20, 60);
        }

        function updateBird() {
            bird.velocity += bird.gravity;
            bird.y += bird.velocity;
            if (bird.y + bird.height > canvas.height) {
                resetGame();
            }
        }

        function updatePipes() {
            if (frame % 100 === 0) {
                const topHeight = Math.random() * (canvas.height / 2);
                pipes.push({ x: canvas.width, topHeight });
            }

            pipes.forEach((pipe, index) => {
                pipe.x -= 2;
                if (pipe.x + pipeWidth < 0) {
                    pipes.splice(index, 1);
                    score++;
                    if (score > highScore) {
                        highScore = score;
                        localStorage.setItem("highScore", highScore);
                    }
                }

                if (
                    bird.x < pipe.x + pipeWidth &&
                    bird.x + bird.width > pipe.x &&
                    (bird.y < pipe.topHeight || bird.y + bird.height > pipe.topHeight + pipeGap)
                ) {
                    resetGame();
                }
            });
        }

        function resetGame() {
            bird.y = canvas.height / 2;
            bird.velocity = 0;
            pipes.length = 0;
            score = 0;
        }

        function gameLoop() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            drawBackground();
            drawPipes();
            drawBird();
            drawScore();
            updateBird();
            updatePipes();
            frame++;
            requestAnimationFrame(gameLoop);
        }

        document.addEventListener("keydown", function (e) {
            if (e.code === "Space") {
                bird.velocity = bird.lift;
            }
        });

        gameLoop();
    </script>
</body>
</html><!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Flappy Bird</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            background: skyblue;
        }
        canvas {
            display: block;
        }
    </style>
</head>
<body>
    <canvas id="gameCanvas"></canvas>
    <script>
        const canvas = document.getElementById("gameCanvas");
        const ctx = canvas.getContext("2d");

        canvas.width = 800;
        canvas.height = 500;

        const bird = {
            x: 100,
            y: canvas.height / 2,
            width: 30,
            height: 30,
            gravity: 0.6,
            lift: -10,
            velocity: 0
        };

        const pipes = [];
        const pipeWidth = 50;
        const pipeGap = 150;
        let frame = 0;
        let score = 0;
        let highScore = localStorage.getItem("highScore") || 0;

        function drawBird() {
            ctx.fillStyle = "yellow";
            ctx.fillRect(bird.x, bird.y, bird.width, bird.height);
        }

        function drawPipes() {
            ctx.fillStyle = "green";
            pipes.forEach(pipe => {
                ctx.fillRect(pipe.x, 0, pipeWidth, pipe.topHeight);
                ctx.fillRect(pipe.x, pipe.topHeight + pipeGap, pipeWidth, canvas.height - pipe.topHeight - pipeGap);
            });
        }

        function drawBackground() {
            ctx.fillStyle = "white";
            for (let i = 0; i < 5; i++) {
                ctx.beginPath();
                ctx.arc(100 + i * 150, 50, 20, 0, Math.PI * 2);
                ctx.arc(120 + i * 150, 60, 25, 0, Math.PI * 2);
                ctx.arc(140 + i * 150, 50, 20, 0, Math.PI * 2);
                ctx.fill();
            }
        }

        function drawScore() {
            ctx.fillStyle = "black";
            ctx.font = "20px Arial";
            ctx.fillText(`Score: ${score}`, 20, 30);
            ctx.fillText(`High Score: ${highScore}`, 20, 60);
        }

        function updateBird() {
            bird.velocity += bird.gravity;
            bird.y += bird.velocity;
            if (bird.y + bird.height > canvas.height) {
                resetGame();
            }
        }

        function updatePipes() {
            if (frame % 100 === 0) {
                const topHeight = Math.random() * (canvas.height / 2);
                pipes.push({ x: canvas.width, topHeight });
            }

            pipes.forEach((pipe, index) => {
                pipe.x -= 2;
                if (pipe.x + pipeWidth < 0) {
                    pipes.splice(index, 1);
                    score++;
                    if (score > highScore) {
                        highScore = score;
                        localStorage.setItem("highScore", highScore);
                    }
                }

                if (
                    bird.x < pipe.x + pipeWidth &&
                    bird.x + bird.width > pipe.x &&
                    (bird.y < pipe.topHeight || bird.y + bird.height > pipe.topHeight + pipeGap)
                ) {
                    resetGame();
                }
            });
        }

        function resetGame() {
            bird.y = canvas.height / 2;
            bird.velocity = 0;
            pipes.length = 0;
            score = 0;
        }

        function gameLoop() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            drawBackground();
            drawPipes();
            drawBird();
            drawScore();
            updateBird();
            updatePipes();
            frame++;
            requestAnimationFrame(gameLoop);
        }

        document.addEventListener("keydown", function (e) {
            if (e.code === "Space") {
                bird.velocity = bird.lift;
            }
        });

        gameLoop();
    </script>
</body>
</html>
