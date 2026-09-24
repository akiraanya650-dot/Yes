
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pro Racing: Asphalt Circuit</title>
    <style>
        * {
            box-sizing: border-box;
            user-select: none;
        }
        body {
            margin: 0;
            padding: 0;
            background: #0b0c10;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            overflow: hidden;
            color: #ffffff;
        }

        #game-container {
            position: relative;
            box-shadow: 0 15px 40px rgba(0,0,0,0.8);
            border-radius: 12px;
            overflow: hidden;
            border: 2px solid #1f2833;
        }

        canvas {
            display: block;
            background: #111;
        }

        .hud {
            position: absolute;
            top: 15px;
            left: 15px;
            right: 15px;
            display: flex;
            justify-content: space-between;
            pointer-events: none;
            font-weight: bold;
            font-size: 1.1rem;
            text-shadow: 0 2px 4px rgba(0,0,0,0.8);
        }

        .hud-panel {
            background: rgba(15, 17, 23, 0.85);
            padding: 10px 18px;
            border-radius: 8px;
            border-left: 4px solid #66fcf1;
            box-shadow: 0 4px 10px rgba(0,0,0,0.5);
        }

        #dashboard {
            position: absolute;
            bottom: 15px;
            right: 15px;
            background: rgba(15, 17, 23, 0.85);
            padding: 12px 20px;
            border-radius: 8px;
            text-align: right;
            border-right: 4px solid #45a29e;
            pointer-events: none;
        }

        .speedometer {
            font-size: 2rem;
            color: #66fcf1;
            font-family: monospace;
        }

        /* Overlay Screens */
        .overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(11, 12, 16, 0.9);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            z-index: 10;
            text-align: center;
            padding: 20px;
        }

        .overlay h1 {
            font-size: 3.5rem;
            margin: 0 0 10px 0;
            color: #66fcf1;
            text-shadow: 0 0 20px rgba(102, 252, 241, 0.4);
            letter-spacing: 2px;
        }

        .overlay p {
            color: #c5c6c7;
            font-size: 1.1rem;
            max-width: 500px;
            line-height: 1.5;
            margin-bottom: 25px;
        }

        .btn {
            background: #66fcf1;
            color: #0b0c10;
            border: none;
            padding: 14px 35px;
            font-size: 1.2rem;
            font-weight: bold;
            border-radius: 6px;
            cursor: pointer;
            transition: all 0.2s ease;
            box-shadow: 0 4px 15px rgba(102, 252, 241, 0.3);
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .btn:hover {
            background: #45a29e;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(69, 162, 158, 0.5);
        }

        .controls-hint {
            margin-top: 20px;
            font-size: 0.85rem;
            color: #888;
        }
        
        .controls-hint span {
            color: #fff;
            background: #222;
            padding: 3px 8px;
            border-radius: 4px;
            border: 1px solid #444;
        }
    </style>
</head>
<body>

    <div id="game-container">
        <!-- HUD Overlay -->
        <div class="hud" id="hudDisplay" style="display: none;">
            <div class="hud-panel">
                LAP: <span id="lapCount">1</span> / 3
            </div>
            <div class="hud-panel">
                POSITION: <span id="racePosition">3</span> / 3
            </div>
            <div class="hud-panel">
                TIME: <span id="lapTime">00.00</span>s
            </div>
        </div>

        <div id="dashboard" style="display: none;">
            <div style="font-size: 0.75rem; color: #888; letter-spacing: 1px;">SPEED</div>
            <div class="speedometer"><span id="speedVal">0</span> <span style="font-size: 1rem;">MPH</span></div>
        </div>

        <!-- Start Screen -->
        <div id="startScreen" class="overlay">
            <h1>PRO RACING</h1>
            <p>Experience high-speed arcade circuit racing. Master precision steering, control your drifts through hairpin turns, and beat rival AI racers to claim the championship trophy!</p>
            <button class="btn" onclick="startGame()">Start Engine</button>
            <div class="controls-hint">
                Steer: <span>A / D</span> or <span>← / →</span> | 
                Accelerate: <span>W</span> or <span>↑</span> | 
                Brake: <span>S</span> or <span>↓</span> | 
                Drift: <span>SPACE</span>
            </div>
        </div>

        <!-- Game Over / Victory Screen -->
        <div id="endScreen" class="overlay" style="display: none;">
            <h1 id="endTitle">Race Finished</h1>
            <p id="endMessage">You crossed the finish line!</p>
            <button class="btn" onclick="startGame()">Play Again</button>
        </div>

        <canvas id="gameCanvas" width="900" height="600"></canvas>
    </div>

    <script>
        const canvas = document.getElementById("gameCanvas");
        const ctx = canvas.getContext("2d");

        // Game State
        let gameState = "START"; // START, PLAYING, GAMEOVER
        let keys = {};
        let particles = [];
        let skidMarks = [];

        // Track Design (Waypoints forming a loop circuit)
        const trackWaypoints = [
            { x: 150, y: 480 },
            { x: 150, y: 180 },
            { x: 300, y: 100 },
            { x: 600, y: 100 },
            { x: 750, y: 220 },
            { x: 750, y: 480 },
            { x: 600, y: 530 },
            { x: 300, y: 530 }
        ];

        // Car Class
        class Car {
            constructor(x, y, color, isPlayer = false, name = "AI") {
                this.x = x;
                this.y = y;
                this.width = 24;
                this.height = 46;
                this.angle = -Math.PI / 2;
                this.speed = 0;
                this.maxSpeed = isPlayer ? 6.5 : 5.8;
                this.minSpeed = -2;
                this.acceleration = 0.12;
                this.braking = 0.25;
                this.friction = 0.04;
                this.steerSpeed = 0.045;
                this.color = color;
                this.isPlayer = isPlayer;
                this.name = name;
                
                // Racing Logic Stats
                this.currentWaypoint = 0;
                this.laps = 0;
                this.lapStartTime = 0;
                this.lastLapTime = 0;
                this.bestLapTime = 999;
                this.totalTime = 0;
                this.finished = false;
            }

            update() {
                if (this.finished) return;

                if (this.isPlayer) {
                    // Player Controls
                    let isAccelerating = false;
                    let isBraking = false;
                    let isDrifting = false;

                    if (keys['KeyW'] || keys['ArrowUp']) {
                        this.speed = Math.min(this.speed + this.acceleration, this.maxSpeed);
                        isAccelerating = true;
                    } else if (keys['KeyS'] || keys['ArrowDown']) {
                        if (this.speed > 0) {
                            this.speed -= this.braking;
                        } else {
                            this.speed = Math.max(this.speed - this.acceleration * 0.6, this.minSpeed);
                        }
                        isBraking = true;
                    } else {
                        // Natural friction deceleration
                        if (this.speed > 0) this.speed = Math.max(0, this.speed - this.friction);
                        if (this.speed < 0) this.speed = Math.min(0, this.speed + this.friction);
                    }

                    if (keys['Space']) {
                        isDrifting = true;
                        this.friction = 0.01; // Less grip during drift
                    } else {
                        this.friction = 0.04;
                    }

                    // Steering factors (effective at higher speeds)
                    let effectiveSteer = this.steerSpeed * (Math.abs(this.speed) / this.maxSpeed);
                    if (this.speed !== 0) {
                        if (keys['KeyA'] || keys['ArrowLeft']) {
                            this.angle -= effectiveSteer * (this.speed < 0 ? -1 : 1);
                        }
                        if (keys['KeyD'] || keys['ArrowRight']) {
                            this.angle += effectiveSteer * (this.speed < 0 ? -1 : 1);
                        }
                    }

                    // Tire smoke & skid tracks when drifting or turning sharp
                    if (isDrifting && Math.abs(this.speed) > 3) {
                        skidMarks.push({ x: this.x, y: this.y, alpha: 0.5 });
                        if (skidMarks.length > 300) skidMarks.shift();
                    }
                } else {
                    // AI Driving Logic: Navigate waypoints
                    let target = trackWaypoints[this.currentWaypoint];
                    let dx = target.x - this.x;
                    let dy = target.y - this.y;
                    let targetAngle = Math.atan2(dy, dx);

                    // Smooth steering adjustment toward waypoint
                    let angleDiff = targetAngle - this.angle;
                    while (angleDiff < -Math.PI) angleDiff += Math.PI * 2;
                    while (angleDiff > Math.PI) angleDiff -= Math.PI * 2;

                    if (angleDiff > 0.05) this.angle += this.steerSpeed * 0.8;
                    else if (angleDiff < -0.05) this.angle -= this.steerSpeed * 0.8;

                    // AI Target Speed variation
                    let distToWaypoint = Math.hypot(dx, dy);
                    if (distToWaypoint < 120) {
                        this.currentWaypoint = (this.currentWaypoint + 1) % trackWaypoints.length;
                    }

                    // AI acceleration
                    this.speed = Math.min(this.speed + this.acceleration * 0.8, this.maxSpeed * 0.85);
                }

                // Physics movement update
                this.x += Math.cos(this.angle) * this.speed;
                this.y += Math.sin(this.angle) * this.speed;

                // Track Boundary Limits (Off-road slow down)
                let onTrack = checkTrackCollision(this.x, this.y);
                if (!onTrack) {
                    this.speed *= 0.95; // Mud/Grass slow down penalty
                }

                // Check Lap Progression using Start/Finish line line segment (between waypoint 0 and position X: 150, Y: 400-560)
                checkLapProgress(this);
            }

            draw() {
                ctx.save();
                ctx.translate(this.x, this.y);
                ctx.rotate(this.angle);

                // Draw Tire Marks / Shadow under car
                ctx.fillStyle = "rgba(0,0,0,0.3)";
                ctx.fillRect(-this.width/2 - 2, -this.height/2 - 2, this.width + 4, this.height + 4);

                // Car Chassis
                ctx.fillStyle = this.color;
                ctx.beginPath();
                ctx.roundRect(-this.width/2, -this.height/2, this.width, this.height, 6);
                ctx.fill();
                ctx.strokeStyle = "#111";
                ctx.lineWidth = 1.5;
                ctx.stroke();

                // Windshield & Roof
                ctx.fillStyle = "#111";
                ctx.fillRect(-this.width/2 + 3, -this.height/4, this.width - 6, this.height/3);

                // Headlights
                ctx.fillStyle = "#ffffaa";
                ctx.fillRect(-this.width/2 + 2, -this.height/2 - 2, 4, 3);
                ctx.fillRect(this.width/2 - 6, -this.height/2 - 2, 4, 3);

                // Rear wing spoiler for player/sports cars
                ctx.fillStyle = "#222";
                ctx.fillRect(-this.width/2 - 2, this.height/2 - 4, this.width + 4, 3);

                ctx.restore();
            }
        }

        // Setup Cars
        let playerCar = new Car(150, 480, "#e74c3c", true, "Player");
        let aiCar1 = new Car(130, 520, "#3498db", false, "Rival Alpha");
        let aiCar2 = new Car(170, 520, "#f1c40f", false, "Rival Beta");
        let cars = [playerCar, aiCar1, aiCar2];

        // Track verification function
        function checkTrackCollision(x, y) {
            // Simple distance check to central track curves
            // Outer boundaries (rough polygon approximation or area check)
            let distToCenter = Math.hypot(x - 450, y - 315);
            // Main circuit loop verification
            if (x > 80 && x < 820 && y > 80 && y < 540) {
                // Check if inside inner grass island
                let inInnerIsland = (x > 250 && x < 650 && y > 180 && y < 450);
                return !inInnerIsland;
            }
            return false;
        }

        function checkLapProgress(car) {
            // Finish line detector: X between 100 and 200, Y between 450 and 550 moving upwards
            if (car.x >= 100 && car.x <= 200 && car.y >= 450 && car.y <= 550) {
                // Prevent duplicate triggering by verifying car was recently past waypoint 3 or 4
                if (car.currentWaypoint >= 3 && !car.lapCooldown) {
                    car.laps++;
                    car.lapCooldown = true;
                    setTimeout(() => { car.lapCooldown = false; }, 3000); // cooldown to avoid rapid triggers

                    if (car.isPlayer) {
                        if (car.laps > 3) {
                            endGame(true);
                        }
                    }
                }
            }
        }

        // Keyboard Event Listeners
        window.addEventListener("keydown", (e) => { keys[e.code] = true; });
        window.addEventListener("keyup", (e) => { keys[e.code] = false; });

        function startGame() {
            document.getElementById("startScreen").style.display = "none";
            document.getElementById("endScreen").style.display = "none";
            document.getElementById("hudDisplay").style.display = "flex";
            document.getElementById("dashboard").style.display = "block";

            // Reset car positions
            playerCar = new Car(150, 480, "#e74c3c", true, "Player");
            aiCar1 = new Car(130, 520, "#3498db", false, "Rival Alpha");
            aiCar2 = new Car(170, 520, "#f1c40f", false, "Rival Beta");
            cars = [playerCar, aiCar1, aiCar2];
            skidMarks = [];

            gameState = "PLAYING";
        }

        function endGame(won) {
            gameState = "GAMEOVER";
            document.getElementById("hudDisplay").style.display = "none";
            document.getElementById("dashboard").style.display = "none";
            
            let endScreen = document.getElementById("endScreen");
            let endTitle = document.getElementById("endTitle");
            let endMessage = document.getElementById("endMessage");

            endScreen.style.display = "flex";
            if (won) {
                endTitle.innerText = "VICTORY!";
                endTitle.style.color = "#66fcf1";
                endMessage.innerText = "Fantastic driving! You dominated the asphalt circuit and won the race.";
            } else {
                endTitle.innerText = "RACE OVER";
                endTitle.style.color = "#e74c3c";
                endMessage.innerText = "Better luck next time. Fine-tune your cornering and try again!";
            }
        }

        function drawTrack() {
            // Asphalt Road Background
            ctx.fillStyle = "#1f2833";
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            // Infield Grass / Scenery
            ctx.fillStyle = "#112211";
            ctx.beginPath();
            ctx.roundRect(50, 50, 800, 500, 30);
            ctx.fill();

            // Inner Green Island
            ctx.fillStyle = "#0b0c10";
            ctx.beginPath();
            ctx.roundRect(230, 160, 440, 310, 20);
            ctx.fill();

            // Road Track Outer & Inner borders (Kerbs)
            ctx.strokeStyle = "#c5c6c7";
            ctx.lineWidth = 4;
            ctx.setLineDash([15, 15]);
            
            // Outer Circuit Outline
            ctx.beginPath();
            ctx.roundRect(90, 90, 720, 420, 40);
            ctx.stroke();

            // Inner Island Outline
            ctx.beginPath();
            ctx.roundRect(210, 140, 480, 350, 30);
            ctx.stroke();
            ctx.setLineDash([]); // Reset line dash

            // Draw Skid Marks
            for (let mark of skidMarks) {
                ctx.fillStyle = `rgba(0, 0, 0, 0.4)`;
                ctx.fillRect(mark.x - 2, mark.y - 2, 4, 4);
            }

            // Start / Finish Line Grid
            ctx.fillStyle = "#ffffff";
            for (let i = 0; i < 5; i++) {
                ctx.fillRect(140, 450 + (i * 12), 20, 6);
                ctx.fillStyle = ctx.fillStyle === "#ffffff" ? "#000000" : "#ffffff";
            }
        }

        function updateHUD() {
            document.getElementById("lapCount").innerText = Math.min(playerCar.laps, 3);
            document.getElementById("speedVal").innerText = Math.floor(Math.abs(playerCar.speed) * 22);

            // Calculate position ranking
            let sortedCars = [...cars].sort((a, b) => {
                if (b.laps !== a.laps) return b.laps - a.laps;
                return b.currentWaypoint - a.currentWaypoint;
            });
            let playerRank = sortedCars.findIndex(c => c.isPlayer) + 1;
            document.getElementById("racePosition").innerText = playerRank;
        }

        function loop() {
            if (gameState === "PLAYING") {
                // Update Cars
                for (let car of cars) {
                    car.update();
                }

                // Check AI win condition
                for (let car of cars) {
                    if (!car.isPlayer && car.laps > 3) {
                        endGame(false);
                        break;
                    }
                }

                updateHUD();
            }

            // Render Graphics
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            drawTrack();

            for (let car of cars) {
                car.draw();
            }

            requestAnimationFrame(loop);
        }

        // Run the main animation loop
        loop();
    </script>
</body>
</html>
