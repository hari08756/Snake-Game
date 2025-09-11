<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Snake Game Documentation</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #2ecc71;
            --secondary: #3498db;
            --accent: #e74c3c;
            --dark: #2c3e50;
            --light: #ecf0f1;
            --background: #1a252f;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: var(--background);
            color: var(--light);
            line-height: 1.6;
            overflow-x: hidden;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            text-align: center;
            padding: 40px 0;
            background: linear-gradient(135deg, var(--dark), #000);
            border-radius: 0 0 50% 50% / 30%;
            margin-bottom: 40px;
            position: relative;
            overflow: hidden;
        }
        
        header::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: 
                radial-gradient(circle at 20% 30%, rgba(46, 204, 113, 0.2) 0%, transparent 20%),
                radial-gradient(circle at 80% 70%, rgba(52, 152, 219, 0.2) 0%, transparent 20%);
        }
        
        h1 {
            font-size: 3.5rem;
            margin-bottom: 15px;
            color: var(--primary);
            text-shadow: 0 0 15px rgba(46, 204, 113, 0.5);
            position: relative;
        }
        
        h2 {
            font-size: 2.2rem;
            margin: 40px 0 20px;
            color: var(--secondary);
            border-left: 5px solid var(--secondary);
            padding-left: 15px;
        }
        
        h3 {
            font-size: 1.8rem;
            margin: 25px 0 15px;
            color: var(--primary);
        }
        
        p {
            margin-bottom: 20px;
            font-size: 1.1rem;
        }
        
        .header-subtitle {
            font-size: 1.4rem;
            color: var(--light);
            margin-bottom: 25px;
        }
        
        .game-info {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
            margin: 30px 0;
        }
        
        .card {
            background: linear-gradient(145deg, #2c3e50, #1a252f);
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.4);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            position: relative;
            overflow: hidden;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .card::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 5px;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
        }
        
        .card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.5);
        }
        
        .card-title {
            font-size: 1.5rem;
            margin-bottom: 15px;
            color: var(--primary);
            display: flex;
            align-items: center;
        }
        
        .card-title i {
            margin-right: 10px;
            font-size: 1.8rem;
        }
        
        .feature-list {
            list-style-type: none;
        }
        
        .feature-list li {
            padding: 12px 0;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            display: flex;
            align-items: center;
        }
        
        .feature-list li:before {
            content: "🐍";
            margin-right: 15px;
            font-size: 1.5rem;
        }
        
        .score-system {
            display: flex;
            justify-content: space-around;
            margin: 40px 0;
            flex-wrap: wrap;
            gap: 20px;
        }
        
        .score-item {
            background: linear-gradient(135deg, var(--dark), #000);
            color: white;
            padding: 25px;
            border-radius: 15px;
            width: 30%;
            min-width: 250px;
            text-align: center;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3);
            border: 2px solid var(--secondary);
            transition: transform 0.3s ease;
        }
        
        .score-item:hover {
            transform: scale(1.05);
        }
        
        .score-item h3 {
            color: var(--primary);
            margin-bottom: 15px;
            font-size: 1.8rem;
        }
        
        .controls {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-around;
            gap: 25px;
            margin: 40px 0;
        }
        
        .control-item {
            flex: 1;
            min-width: 250px;
            background: linear-gradient(145deg, #2c3e50, #1a252f);
            padding: 20px;
            border-radius: 15px;
            text-align: center;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3);
            border: 2px solid var(--primary);
        }
        
        .control-item h3 {
            color: var(--secondary);
            margin-bottom: 15px;
        }
        
        .btn {
            display: inline-block;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            color: white;
            padding: 15px 35px;
            border-radius: 50px;
            text-decoration: none;
            font-weight: bold;
            margin: 20px 10px;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
            border: none;
            cursor: pointer;
            font-size: 1.1rem;
        }
        
        .btn:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.4);
        }
        
        .snake-animation {
            width: 100%;
            height: 200px;
            position: relative;
            margin: 40px 0;
            overflow: hidden;
            border-radius: 15px;
            background: linear-gradient(145deg, #1a252f, #2c3e50);
        }
        
        .snake-segment {
            position: absolute;
            width: 20px;
            height: 20px;
            background: var(--primary);
            border-radius: 4px;
            transition: all 0.3s ease;
        }
        
        .snake-food {
            position: absolute;
            width: 20px;
            height: 20px;
            background: var(--accent);
            border-radius: 50%;
            animation: pulse 1.5s infinite;
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.2); }
            100% { transform: scale(1); }
        }
        
        .footer {
            text-align: center;
            margin-top: 60px;
            padding: 30px;
            background: linear-gradient(135deg, var(--dark), #000);
            border-radius: 15px;
            box-shadow: 0 -5px 20px rgba(0, 0, 0, 0.3);
        }
        
        .footer p {
            margin: 10px 0;
        }
        
        .copyright {
            color: var(--primary);
            font-weight: bold;
            font-size: 1.2rem;
        }
        
        @media (max-width: 768px) {
            h1 {
                font-size: 2.5rem;
            }
            
            .header-subtitle {
                font-size: 1.2rem;
            }
            
            .score-item {
                width: 100%;
            }
            
            .game-info {
                grid-template-columns: 1fr;
            }
        }
        
        /* Snake animation */
        #snake-head {
            background: var(--secondary);
            z-index: 10;
        }
        
        /* Demo game area */
        .demo-game {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 15px;
            padding: 20px;
            margin: 30px 0;
            text-align: center;
            border: 2px solid var(--primary);
        }
        
        .demo-container {
            max-width: 400px;
            margin: 0 auto;
            position: relative;
        }
        
        .demo-game canvas {
            border: 2px solid var(--secondary);
            border-radius: 8px;
            background: #1a252f;
            margin: 15px 0;
        }
        
        .demo-controls {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-top: 15px;
        }
        
        .demo-btn {
            background: linear-gradient(90deg, var(--secondary), var(--primary));
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
        }
        
        .link-fallback {
            margin-top: 15px;
            color: var(--accent);
            font-size: 0.9rem;
        }
        
        .game-links {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin: 30px 0;
            flex-wrap: wrap;
        }
        
        .game-link {
            display: flex;
            flex-direction: column;
            align-items: center;
            text-decoration: none;
            color: var(--light);
            transition: transform 0.3s ease;
        }
        
        .game-link:hover {
            transform: translateY(-5px);
        }
        
        .game-link i {
            font-size: 2.5rem;
            margin-bottom: 10px;
            color: var(--primary);
        }
        
        .game-link span {
            font-weight: bold;
        }
    </style>
</head>
<body>
    <header>
        <div class="container">
            <h1><i class="fas fa-gamepad"></i> Snake Game Documentation</h1>
            <p class="header-subtitle">Comprehensive guide to the Modern Snake Game by Harionn Maurya</p>
            
            <div class="game-links">
                <a href="https://hari08756.github.io/Snake-Game/SnakeGame.html" class="game-link" target="_blank" rel="noopener noreferrer">
                    <i class="fas fa-play-circle"></i>
                    <span>Play Game</span>
                </a>
                <a href="https://github.com/Hari08756/Snake-Game" class="game-link" target="_blank" rel="noopener noreferrer">
                    <i class="fab fa-github"></i>
                    <span>View Source Code</span>
                </a>
            </div>
            
            <a href="https://hari08756.github.io/Snake-Game/SnakeGame.html" class="btn" target="_blank" rel="noopener noreferrer">
                <i class="fas fa-play-circle"></i> Play Game
            </a>
            <a href="https://github.com/Hari08756/Snake-Game" class="btn" target="_blank" rel="noopener noreferrer">
                <i class="fab fa-github"></i> View Source Code
            </a>
        </div>
    </header>
    
    <div class="container">
        <section>
            <h2>Overview</h2>
            <p>This documentation provides comprehensive information about the Snake Game web application created by Harionn Maurya. This modern implementation of the classic Snake game features enhanced gameplay mechanics, special abilities, and a sleek design.</p>
        </section>
        
        <section>
            <h2>Game Description</h2>
            <p>A modern implementation of the classic Snake game with enhanced features including special abilities, score tracking, and responsive touch controls. Navigate your snake to collect food, grow longer, and achieve high scores while avoiding obstacles.</p>
            
            <div class="snake-animation" id="snake-animation">
                <!-- JavaScript will add snake segments here -->
            </div>
        </section>
        
        <section>
            <h2>Features</h2>
            <div class="game-info">
                <div class="card">
                    <h3 class="card-title"><i class="fas fa-star"></i> Core Gameplay</h3>
                    <ul class="feature-list">
                        <li>Classic snake movement mechanics</li>
                        <li>Food collection to grow longer</li>
                        <li>Wall collision detection</li>
                        <li>Self-collision detection</li>
                    </ul>
                </div>
                
                <div class="card">
                    <h3 class="card-title"><i class="fas fa-tachometer-alt"></i> Special Abilities</h3>
                    <ul class="feature-list">
                        <li>Pause game (I Key)</li>
                        <li>Slow motion (II Key)</li>
                        <li>Shrink snake (III Key)</li>
                        <li>Speed boost (IV Key)</li>
                    </ul>
                </div>
                
                <div class="card">
                    <h3 class="card-title"><i class="fas fa-chart-line"></i> Score System</h3>
                    <ul class="feature-list">
                        <li>Real-time score tracking</li>
                        <li>High score preservation</li>
                        <li>Average score calculation</li>
                        <li>Special food bonuses</li>
                    </ul>
                </div>
            </div>
        </section>
        
        <section>
            <h2>How to Play</h2>
            <p>Use the touch controls or swipe on the game area to change direction. Collect food to grow and earn points. Avoid hitting walls or yourself. Collect special food for bonus effects!</p>
            
            <div class="score-system">
                <div class="score-item">
                    <h3>SCORE</h3>
                    <p>Current points earned in the active game session</p>
                </div>
                
                <div class="score-item">
                    <h3>HIGH SCORE</h3>
                    <p>Best performance achieved across all game sessions</p>
                </div>
                
                <div class="score-item">
                    <h3>AVG SCORE</h3>
                    <p>Typical performance across multiple games</p>
                </div>
            </div>
        </section>
        
        <section>
            <h2>Controls</h2>
            <div class="controls">
                <div class="control-item">
                    <h3><i class="fas fa-desktop"></i> Desktop</h3>
                    <p>Use arrow keys or WASD to control the snake's direction</p>
                </div>
                
                <div class="control-item">
                    <h3><i class="fas fa-mobile-alt"></i> Mobile</h3>
                    <p>Swipe in the desired direction to change movement</p>
                </div>
                
                <div class="control-item">
                    <h3><i class="fas fa-keyboard"></i> Special Keys</h3>
                    <p>Press I, II, III, or IV for special abilities</p>
                </div>
            </div>
        </section>
        
        <section>
            <h2>Try a Demo</h2>
            <p>Experience a simplified version of the Snake game right here in the documentation:</p>
            
            <div class="demo-game">
                <div class="demo-container">
                    <canvas id="demo-canvas" width="300" height="200"></canvas>
                    <div class="demo-controls">
                        <button class="demo-btn" id="start-demo">Start Demo</button>
                        <button class="demo-btn" id="reset-demo">Reset</button>
                    </div>
                    <p class="link-fallback">If the external game links don't work, you can try this demo or visit the GitHub repository directly.</p>
                </div>
            </div>
        </section>
        
        <section>
            <h2>Technical Details</h2>
            <p>The game is built with HTML5, CSS3, and JavaScript, utilizing modern web technologies for smooth gameplay and responsive design.</p>
            
            <div class="game-info">
                <div class="card">
                    <h3 class="card-title"><i class="fas fa-code"></i> Technologies</h3>
                    <ul class="feature-list">
                        <li>HTML5 Canvas for rendering</li>
                        <li>CSS3 for styling and animations</li>
                        <li>JavaScript for game logic</li>
                        <li>Responsive design principles</li>
                    </ul>
                </div>
                
                <div class="card">
                    <h3 class="card-title"><i class="fas fa-database"></i> Data Storage</h3>
                    <ul class="feature-list">
                        <li>Local storage for high scores</li>
                        <li>Session management</li>
                        <li>Game state preservation</li>
                    </ul>
                </div>
                
                <div class="card">
                    <h3 class="card-title"><i class="fas fa-paint-brush"></i> Design</h3>
                    <ul class="feature-list">
                        <li>Modern UI with gradient backgrounds</li>
                        <li>Smooth animations and transitions</li>
                        <li>Touch-friendly interface</li>
                    </ul>
                </div>
            </div>
        </section>
        
        <section style="text-align: center; margin: 50px 0;">
            <h2>Ready to Play?</h2>
            <p>Experience the modern take on the classic Snake game with enhanced features and smooth gameplay.</p>
            <a href="https://hari08756.github.io/Snake-Game/SnakeGame.html" class="btn" target="_blank" rel="noopener noreferrer">
                <i class="fas fa-play"></i> Play Snake Game Now
            </a>
            <p class="link-fallback">If the link doesn't work, please check your browser's pop-up settings or try the demo above.</p>
        </section>
    </div>
    
    <div class="footer">
        <div class="container">
            <p class="copyright">Modern Snake Game [Harionn Maurya] © 2025</p>
            <p>This project is open source and available under the MIT License.</p>
        </div>
    </div>

    <script>
        // Create snake animation
        document.addEventListener('DOMContentLoaded', function() {
            const snakeContainer = document.getElementById('snake-animation');
            const containerWidth = snakeContainer.offsetWidth;
            const containerHeight = snakeContainer.offsetHeight;
            
            // Create food
            const food = document.createElement('div');
            food.className = 'snake-food';
            food.style.left = '180px';
            food.style.top = '90px';
            snakeContainer.appendChild(food);
            
            // Create snake segments
            const segments = 8;
            let segmentsElements = [];
            
            for (let i = 0; i < segments; i++) {
                const segment = document.createElement('div');
                segment.className = 'snake-segment';
                segment.style.left = (150 - i * 20) + 'px';
                segment.style.top = '100px';
                if (i === 0) segment.id = 'snake-head';
                snakeContainer.appendChild(segment);
                segmentsElements.push(segment);
            }
            
            // Animate snake
            let moveRight = true;
            let moveDown = false;
            let position = 150;
            
            setInterval(function() {
                if (moveRight) {
                    position += 2;
                    if (position > containerWidth - 50) {
                        moveRight = false;
                        moveDown = true;
                    }
                } else if (moveDown) {
                    position += 2;
                    if (position > containerHeight - 50) {
                        moveDown = false;
                    }
                } else {
                    position -= 2;
                    if (position < 50) {
                        moveRight = true;
                        moveDown = false;
                    }
                }
                
                // Update snake head position
                if (moveRight) {
                    segmentsElements[0].style.left = position + 'px';
                    segmentsElements[0].style.top = '100px';
                } else if (moveDown) {
                    segmentsElements[0].style.left = (containerWidth - 50) + 'px';
                    segmentsElements[0].style.top = (position - containerWidth + 100) + 'px';
                } else {
                    segmentsElements[0].style.left = (containerWidth - position) + 'px';
                    segmentsElements[0].style.top = (containerHeight - 50) + 'px';
                }
                
                // Update other segments to follow the head
                for (let i = 1; i < segments; i++) {
                    setTimeout(function() {
                        segmentsElements[i].style.left = (parseInt(segmentsElements[i-1].style.left) - 20) + 'px';
                        segmentsElements[i].style.top = segmentsElements[i-1].style.top;
                    }, i * 100);
                }
            }, 100);
            
            // Demo game functionality
            const canvas = document.getElementById('demo-canvas');
            const ctx = canvas.getContext('2d');
            const startBtn = document.getElementById('start-demo');
            const resetBtn = document.getElementById('reset-demo');
            
            let demoGameRunning = false;
            let demoInterval;
            
            // Simple demo game
            const demoGame = {
                snake: [{x: 150, y: 100}],
                food: {x: 180, y: 90},
                direction: 'right',
                gridSize: 10,
                speed: 100
            };
            
            function drawDemo() {
                // Clear canvas
                ctx.fillStyle = '#1a252f';
                ctx.fillRect(0, 0, canvas.width, canvas.height);
                
                // Draw food
                ctx.fillStyle = '#e74c3c';
                ctx.beginPath();
                ctx.arc(demoGame.food.x, demoGame.food.y, 5, 0, Math.PI * 2);
                ctx.fill();
                
                // Draw snake
                ctx.fillStyle = '#2ecc71';
                demoGame.snake.forEach(segment => {
                    ctx.fillRect(segment.x - 5, segment.y - 5, 10, 10);
                });
                
                // Draw head
                ctx.fillStyle = '#3498db';
                ctx.fillRect(demoGame.snake[0].x - 5, demoGame.snake[0].y - 5, 10, 10);
            }
            
            function updateDemo() {
                if (!demoGameRunning) return;
                
                // Move snake
                const head = {...demoGame.snake[0]};
                
                switch(demoGame.direction) {
                    case 'up': head.y -= demoGame.gridSize; break;
                    case 'down': head.y += demoGame.gridSize; break;
                    case 'left': head.x -= demoGame.gridSize; break;
                    case 'right': head.x += demoGame.gridSize; break;
                }
                
                // Check boundaries
                if (head.x < 5 || head.x > canvas.width - 5 || 
                    head.y < 5 || head.y > canvas.height - 5) {
                    demoGameRunning = false;
                    alert('Demo ended! Try the full game for more features.');
                    return;
                }
                
                demoGame.snake.unshift(head);
                
                // Check if food eaten
                const dx = Math.abs(head.x - demoGame.food.x);
                const dy = Math.abs(head.y - demoGame.food.y);
                
                if (dx < 10 && dy < 10) {
                    // Generate new food
                    demoGame.food.x = Math.floor(Math.random() * (canvas.width - 20) + 10);
                    demoGame.food.y = Math.floor(Math.random() * (canvas.height - 20) + 10);
                } else {
                    demoGame.snake.pop();
                }
                
                drawDemo();
            }
            
            startBtn.addEventListener('click', function() {
                if (!demoGameRunning) {
                    demoGameRunning = true;
                    demoInterval = setInterval(updateDemo, demoGame.speed);
                    startBtn.textContent = 'Pause Demo';
                } else {
                    demoGameRunning = false;
                    clearInterval(demoInterval);
                    startBtn.textContent = 'Resume Demo';
                }
            });
            
            resetBtn.addEventListener('click', function() {
                demoGameRunning = false;
                clearInterval(demoInterval);
                demoGame.snake = [{x: 150, y: 100}];
                demoGame.food = {x: 180, y: 90};
                demoGame.direction = 'right';
                startBtn.textContent = 'Start Demo';
                drawDemo();
            });
            
            // Initial draw
            drawDemo();
            
            // Keyboard controls for demo
            document.addEventListener('keydown', function(e) {
                if (!demoGameRunning) return;
                
                switch(e.key) {
                    case 'ArrowUp': 
                        if (demoGame.direction !== 'down') demoGame.direction = 'up';
                        break;
                    case 'ArrowDown': 
                        if (demoGame.direction !== 'up') demoGame.direction = 'down';
                        break;
                    case 'ArrowLeft': 
                        if (demoGame.direction !== 'right') demoGame.direction = 'left';
                        break;
                    case 'ArrowRight': 
                        if (demoGame.direction !== 'left') demoGame.direction = 'right';
                        break;
                }
            });
        });
    </script>
</body>
</html>
