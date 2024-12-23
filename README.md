<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>We've Got This - League of Legends</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #1a1a2e;
            color: #eaeaea;
            text-align: center;
            padding: 20px;
        }
        h1 {
            color: #00ff88;
        }
        .champion {
            margin: 20px;
            padding: 15px;
            background: #252540;
            border-radius: 8px;
        }
        .champion h2 {
            color: #00bcd4;
        }
        .motivation {
            margin-top: 30px;
            font-size: 1.2em;
            color: #ffd700;
        }
        #pressButton {
            padding: 15px 30px;
            font-size: 1.2em;
            background-color: #00bcd4;
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            margin-top: 20px;
        }
        #pressButton:disabled {
            background-color: #777;
            cursor: not-allowed;
        }
        #pressCount {
            font-size: 1.5em;
            color: #ffd700;
            margin-top: 10px;
        }
        #timer {
            font-size: 1.5em;
            color: #ff6347;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <h1>We've Got This!</h1>
    <p>Our team composition is unbeatable. Here's why:</p>

    <div class="champion">
        <h2>Top Lane: Malphite</h2>
        <p>Malphite's unstoppable engage and tankiness make him the ultimate teamfight initiator.</p>
    </div>

    <div class="champion">
        <h2>Jungle: Nocturne</h2>
        <p>Nocturne's map control and fear-inducing ultimate will dominate the game.</p>
    </div>

    <div class="champion">
        <h2>Mid Lane: Ahri</h2>
        <p>Ahri's mobility and charm will dismantle their carries effortlessly.</p>
    </div>

    <div class="champion">
        <h2>ADC: Jinx</h2>
        <p>Jinx's late-game power and AoE damage will carry teamfights.</p>
    </div>

    <div class="champion">
        <h2>Support: Leona</h2>
        <p>Leona's crowd control will lock down their entire team.</p>
    </div>

    <div class="motivation">
        <p>Stay focused, play smart, and let's crush this game!</p>
    </div>

    <!-- Button and Tracking Section -->
    <button id="pressButton" onclick="pressButton()">Press to Confirm</button>
    <p id="pressCount">Players Pressed: 0/5</p>
    <p id="timer"></p>

    <script>
        let playersPressed = 0;
        let playersLimit = 5;
        let pressTimer;
        let resetTimer;
        let button = document.getElementById('pressButton');
        let pressCountText = document.getElementById('pressCount');
        let timerText = document.getElementById('timer');
        
        // Function to handle button press
        function pressButton() {
            // Disable button after press
            button.disabled = true;
            
            // Increase player press count
            playersPressed++;
            pressCountText.innerText = `Players Pressed: ${playersPressed}/${playersLimit}`;
            
            // Check if all players have pressed the button
            if (playersPressed === playersLimit) {
                clearInterval(resetTimer); // Stop the reset timer
                timerText.innerText = "All players confirmed! Button will reset in 10 minutes.";
                startResetTimer();
            }
        }

        // Function to start a countdown to reset the button
        function startResetTimer() {
            let minutes = 10;
            let seconds = 0;

            // Update the timer every second
            resetTimer = setInterval(function() {
                if (seconds === 0) {
                    if (minutes === 0) {
                        resetButton();
                        clearInterval(resetTimer); // Stop the countdown
                    } else {
                        minutes--;
                        seconds = 59;
                    }
                } else {
                    seconds--;
                }

                timerText.innerText = `Time until reset: ${minutes}:${seconds < 10 ? '0' + seconds : seconds}`;
            }, 1000);
        }

        // Function to reset the button and counter after 10 minutes or when all players press
        function resetButton() {
            playersPressed = 0;
            pressCountText.innerText = `Players Pressed: 0/${playersLimit}`;
            button.disabled = false;
            timerText.innerText = "Button has been reset. Please press again!";
        }

        // Timer reset after 10 minutes if players haven't all pressed
        pressTimer = setTimeout(function() {
            if (playersPressed < playersLimit) {
                resetButton();
            }
        }, 10 * 60 * 1000); // 10 minutes in milliseconds
    </script>
</body>
</html>
