<!DOCTYPE html>
<html lang="ro">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Test AVOIR au présent</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #006B5F 0%, #004d45 100%);
            min-height: 100vh;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        .container {
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            max-width: 700px;
            width: 100%;
            padding: 40px;
        }
        
        h1 {
            color: #006B5F;
            text-align: center;
            margin-bottom: 10px;
            font-size: 2.5em;
        }
        
        .subtitle {
            text-align: center;
            color: #666;
            margin-bottom: 30px;
            font-size: 1.1em;
        }
        
        .progress-bar {
            background: #e0e0e0;
            height: 10px;
            border-radius: 10px;
            margin-bottom: 30px;
            overflow: hidden;
        }
        
        .progress-fill {
            background: linear-gradient(90deg, #006B5F, #004d45);
            height: 100%;
            width: 0%;
            transition: width 0.3s ease;
        }
        
        .question-card {
            background: #f8f9ff;
            padding: 30px;
            border-radius: 15px;
            margin-bottom: 20px;
        }
        
        .question-number {
            color: #006B5F;
            font-weight: bold;
            margin-bottom: 15px;
            font-size: 0.9em;
        }
        
        .question-text {
            font-size: 1.3em;
            color: #333;
            margin-bottom: 20px;
            line-height: 1.6;
        }
        
        .highlight {
            background: #fff3cd;
            padding: 2px 8px;
            border-radius: 4px;
            font-weight: bold;
        }
        
        .options {
            display: flex;
            flex-direction: column;
            gap: 12px;
        }
        
        .option-btn {
            background: white;
            border: 2px solid #e0e0e0;
            padding: 15px 20px;
            border-radius: 10px;
            font-size: 1.1em;
            cursor: pointer;
            transition: all 0.3s ease;
            text-align: left;
        }
        
        .option-btn:hover {
            border-color: #006B5F;
            background: #e6f4f3;
            transform: translateX(5px);
        }
        
        .option-btn.correct {
            background: #d4edda;
            border-color: #28a745;
            animation: pulse 0.5s;
        }
        
        .option-btn.incorrect {
            background: #f8d7da;
            border-color: #dc3545;
            animation: shake 0.5s;
        }
        
        .option-btn:disabled {
            cursor: not-allowed;
            opacity: 0.7;
        }
        
        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.02); }
        }
        
        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-10px); }
            75% { transform: translateX(10px); }
        }
        
        .next-btn {
            background: linear-gradient(135deg, #006B5F, #004d45);
            color: white;
            border: none;
            padding: 15px 40px;
            border-radius: 25px;
            font-size: 1.1em;
            cursor: pointer;
            display: block;
            margin: 20px auto 0;
            transition: transform 0.3s ease;
        }
        
        .next-btn:hover {
            transform: scale(1.05);
        }
        
        .next-btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }
        
        .results {
            text-align: center;
        }
        
        .score {
            font-size: 4em;
            color: #006B5F;
            font-weight: bold;
            margin: 20px 0;
        }
        
        .message {
            font-size: 1.5em;
            color: #333;
            margin-bottom: 30px;
        }
        
        .restart-btn {
            background: linear-gradient(135deg, #006B5F, #004d45);
            color: white;
            border: none;
            padding: 15px 40px;
            border-radius: 25px;
            font-size: 1.1em;
            cursor: pointer;
            transition: transform 0.3s ease;
        }
        
        .restart-btn:hover {
            transform: scale(1.05);
        }
        
        .sound-toggle {
            position: fixed;
            top: 20px;
            right: 20px;
            background: white;
            border: 2px solid #006B5F;
            border-radius: 50%;
            width: 50px;
            height: 50px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5em;
            transition: all 0.3s ease;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }
        
        .sound-toggle:hover {
            transform: scale(1.1);
            box-shadow: 0 6px 15px rgba(0,0,0,0.2);
        }
        
        .sound-toggle.muted {
            background: #f0f0f0;
            border-color: #ccc;
        }
        
        .timer {
            position: absolute;
            top: 10px;
            right: 10px;
            background: #006B5F;
            color: white;
            padding: 8px 16px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 1.1em;
            min-width: 60px;
            text-align: center;
        }
        
        .timer.warning {
            background: #ff6b6b;
            animation: timerPulse 0.5s infinite;
        }
        
        @keyframes timerPulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }
        
        .timer-toggle {
            position: fixed;
            top: 80px;
            right: 20px;
            background: white;
            border: 2px solid #006B5F;
            border-radius: 25px;
            padding: 10px 20px;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 0.9em;
            transition: all 0.3s ease;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }
        
        .timer-toggle:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 15px rgba(0,0,0,0.2);
        }
        
        .timer-toggle.disabled {
            background: #f0f0f0;
            border-color: #ccc;
            color: #999;
        }
        
        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-size: 1em;
            display: none;
        }
        
        .feedback.show {
            display: block;
        }
        
        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }
        
        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }
    </style>
</head>
<body>
    <button class="sound-toggle" id="soundToggle" onclick="toggleSound()">🔊</button>
    <button class="timer-toggle" id="timerToggle" onclick="toggleTimer()">⏱️ Cronometru: ON</button>
    
    <div class="container">
        <h1>AVOIR au présent</h1>
        <p class="subtitle">Test de antrenament</p>
        <p class="subtitle" style="margin-top: -20px; font-size: 0.95em;">Alege răspunsul corect.</p>
        
        <div class="progress-bar">
            <div class="progress-fill" id="progressBar"></div>
        </div>
        
        <div id="quizContent"></div>
    </div>

    <script>
        const questions = [
            {
                question: "J'<span class='highlight'>___</span> un chat.",
                options: ["ai", "as", "a", "ont"],
                correct: 0,
                feedback: "Cu 'je' folosim 'ai' → J'ai (cu apostrof înaintea vocalei sau înainte de h mut)."
            },
            {
                question: "Tu <span class='highlight'>___</span> une voiture rouge.",
                options: ["ai", "as", "a", "avez"],
                correct: 1,
                feedback: "Cu 'tu' folosim 'as' → Tu as."
            },
            {
                question: "Elle <span class='highlight'>___</span> dix ans.",
                options: ["ai", "as", "a", "ont"],
                correct: 2,
                feedback: "Cu 'il/elle/on' folosim 'a' → Elle a."
            },
            {
                question: "Nous n'<span class='highlight'>___</span> pas de voiture.",
                options: ["avons", "avez", "ont", "as"],
                correct: 0,
                feedback: "Cu 'nous' folosim 'avons' → Nous n'avons pas (forma negativă: ne/n' + verbe + pas)."
            },
            {
                question: "Vous n'<span class='highlight'>___</span> pas raison.",
                options: ["avons", "avez", "ont", "a"],
                correct: 1,
                feedback: "Cu 'vous' folosim 'avez' → Vous n'avez pas (forma negativă: ne/n' + verbe + pas)."
            },
            {
                question: "Ils n'<span class='highlight'>___</span> pas de chance.",
                options: ["avons", "avez", "ont", "a"],
                correct: 2,
                feedback: "Cu 'ils/elles' folosim 'ont' → Ils n'ont pas (forma negativă: ne/n' + verbe + pas)."
            },
            {
                question: "J'<span class='highlight'>___</span> faim.",
                options: ["ai", "as", "a", "ont"],
                correct: 0,
                feedback: "'Avoir faim' = a avea foame → J'ai faim."
            },
            {
                question: "Elle <span class='highlight'>___</span> de la chance!",
                options: ["ai", "as", "a", "avons"],
                correct: 2,
                feedback: "Cu 'il/elle' folosim 'a' → Elle a."
            },
            {
                question: "Marie et Paul <span class='highlight'>___</span> raison.",
                options: ["avons", "avez", "ont", "a"],
                correct: 2,
                feedback: "Marie et Paul = ils → ont."
            },
            {
                question: "Est-ce que tu <span class='highlight'>___</span> soif?",
                options: ["ai", "as", "a", "ont"],
                correct: 1,
                feedback: "'Avoir soif' = a avea sete → Tu as soif."
            }
        ];

        let currentQuestion = 0;
        let score = 0;
        let answered = false;
        let soundEnabled = true;
        let timerEnabled = true;
        let timerInterval = null;
        let timeLeft = 40;
        
        // Audio Context for sound effects
        const AudioContext = window.AudioContext || window.webkitAudioContext;
        const audioCtx = new AudioContext();
        
        function playCorrectSound() {
            if (!soundEnabled) return;
            
            const oscillator = audioCtx.createOscillator();
            const gainNode = audioCtx.createGain();
            
            oscillator.connect(gainNode);
            gainNode.connect(audioCtx.destination);
            
            oscillator.frequency.value = 523.25; // C5
            oscillator.type = 'sine';
            
            gainNode.gain.setValueAtTime(0.3, audioCtx.currentTime);
            gainNode.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.3);
            
            oscillator.start(audioCtx.currentTime);
            oscillator.stop(audioCtx.currentTime + 0.3);
            
            // Second note for pleasant sound
            setTimeout(() => {
                const osc2 = audioCtx.createOscillator();
                const gain2 = audioCtx.createGain();
                
                osc2.connect(gain2);
                gain2.connect(audioCtx.destination);
                
                osc2.frequency.value = 659.25; // E5
                osc2.type = 'sine';
                
                gain2.gain.setValueAtTime(0.2, audioCtx.currentTime);
                gain2.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.3);
                
                osc2.start(audioCtx.currentTime);
                osc2.stop(audioCtx.currentTime + 0.3);
            }, 100);
        }
        
        function playIncorrectSound() {
            if (!soundEnabled) return;
            
            const oscillator = audioCtx.createOscillator();
            const gainNode = audioCtx.createGain();
            
            oscillator.connect(gainNode);
            gainNode.connect(audioCtx.destination);
            
            oscillator.frequency.value = 200; // Low tone
            oscillator.type = 'sawtooth';
            
            gainNode.gain.setValueAtTime(0.3, audioCtx.currentTime);
            gainNode.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.2);
            
            oscillator.start(audioCtx.currentTime);
            oscillator.stop(audioCtx.currentTime + 0.2);
        }
        
        function toggleSound() {
            soundEnabled = !soundEnabled;
            const btn = document.getElementById('soundToggle');
            btn.textContent = soundEnabled ? '🔊' : '🔇';
            btn.classList.toggle('muted');
            
            // Resume audio context if needed (browser policy)
            if (soundEnabled && audioCtx.state === 'suspended') {
                audioCtx.resume();
            }
        }
        
        function toggleTimer() {
            timerEnabled = !timerEnabled;
            const btn = document.getElementById('timerToggle');
            btn.textContent = timerEnabled ? '⏱️ Cronometru: ON' : '⏱️ Cronometru: OFF';
            btn.classList.toggle('disabled');
            
            if (!timerEnabled && timerInterval) {
                clearInterval(timerInterval);
                const timerEl = document.getElementById('timer');
                if (timerEl) timerEl.style.display = 'none';
            } else if (timerEnabled && !answered) {
                startTimer();
            }
        }
        
        function startTimer() {
            if (!timerEnabled) return;
            
            timeLeft = 40;
            const timerEl = document.getElementById('timer');
            if (timerEl) {
                timerEl.style.display = 'block';
                timerEl.textContent = timeLeft + 's';
                timerEl.classList.remove('warning');
            }
            
            if (timerInterval) clearInterval(timerInterval);
            
            timerInterval = setInterval(() => {
                timeLeft--;
                const timerEl = document.getElementById('timer');
                
                if (timerEl) {
                    timerEl.textContent = timeLeft + 's';
                    
                    if (timeLeft <= 10) {
                        timerEl.classList.add('warning');
                    }
                }
                
                if (timeLeft <= 0) {
                    clearInterval(timerInterval);
                    if (!answered) {
                        autoNextQuestion();
                    }
                }
            }, 1000);
        }
        
        function stopTimer() {
            if (timerInterval) {
                clearInterval(timerInterval);
                timerInterval = null;
            }
        }
        
        function autoNextQuestion() {
            // Automatically move to next question when time runs out
            const nextBtn = document.getElementById('nextBtn');
            if (nextBtn && !answered) {
                // Mark as skipped
                const feedback = document.getElementById('feedback');
                if (feedback) {
                    feedback.textContent = '⏰ Timpul a expirat! Trecem la următoarea întrebare.';
                    feedback.classList.add('incorrect', 'show');
                }
                
                const options = document.querySelectorAll('.option-btn');
                options.forEach(btn => btn.disabled = true);
                
                // Show correct answer
                const q = questions[currentQuestion];
                options[q.correct].classList.add('correct');
                
                answered = true;
                nextBtn.disabled = false;
                
                // Auto advance after 2 seconds
                setTimeout(() => {
                    nextQuestion();
                }, 2000);
            }
        }

        function updateProgress() {
            const progress = (currentQuestion / questions.length) * 100;
            document.getElementById('progressBar').style.width = progress + '%';
        }

        function showQuestion() {
            answered = false;
            const q = questions[currentQuestion];
            
            let html = `
                <div class="question-card" style="position: relative;">
                    <div class="timer" id="timer" style="display: ${timerEnabled ? 'block' : 'none'};">40s</div>
                    <div class="question-number">Question ${currentQuestion + 1} sur ${questions.length}</div>
                    <div class="question-text">${q.question}</div>
                    <div class="options">
                        ${q.options.map((option, index) => `
                            <button class="option-btn" onclick="checkAnswer(${index})">${option}</button>
                        `).join('')}
                    </div>
                    <div class="feedback" id="feedback"></div>
                </div>
                <button class="next-btn" id="nextBtn" onclick="nextQuestion()" disabled>Următoarea →</button>
            `;
            
            document.getElementById('quizContent').innerHTML = html;
            updateProgress();
            
            if (timerEnabled) {
                startTimer();
            }
        }

        function checkAnswer(selected) {
            if (answered) return;
            answered = true;
            
            stopTimer(); // Stop timer when answer is selected
            
            const q = questions[currentQuestion];
            const options = document.querySelectorAll('.option-btn');
            const feedback = document.getElementById('feedback');
            const nextBtn = document.getElementById('nextBtn');
            
            options.forEach(btn => btn.disabled = true);
            
            if (selected === q.correct) {
                playCorrectSound();
                options[selected].classList.add('correct');
                feedback.textContent = '✓ ' + q.feedback;
                feedback.classList.add('correct', 'show');
                score++;
            } else {
                playIncorrectSound();
                options[selected].classList.add('incorrect');
                options[q.correct].classList.add('correct');
                feedback.textContent = '✗ Incorect! Răspunsul corect era: ' + q.options[q.correct] + '. ' + q.feedback;
                feedback.classList.add('incorrect', 'show');
            }
            
            nextBtn.disabled = false;
        }

        function nextQuestion() {
            stopTimer();
            currentQuestion++;
            if (currentQuestion < questions.length) {
                showQuestion();
            } else {
                showResults();
            }
        }

        function showResults() {
            const percentage = Math.round((score / questions.length) * 100);
            let message = '';
            
            if (percentage === 100) {
                message = '🎉 Perfect! Ești un campion la AVOIR!';
            } else if (percentage >= 80) {
                message = '👏 Foarte bine! Cunoști bine verbul AVOIR!';
            } else if (percentage >= 60) {
                message = '👍 Bine! Mai exersează puțin!';
            } else {
                message = '💪 Continuă să exersezi! Vei reuși!';
            }
            
            let html = `
                <div class="results">
                    <h2>Rezultate</h2>
                    <div class="score">${score}/${questions.length}</div>
                    <div class="message">${message}</div>
                    <p style="color: #666; margin-bottom: 20px;">Ai obținut ${percentage}% răspunsuri corecte!</p>
                    <button class="restart-btn" onclick="restartQuiz()">🔄 Încearcă din nou</button>
                </div>
            `;
            
            document.getElementById('quizContent').innerHTML = html;
            document.getElementById('progressBar').style.width = '100%';
        }

        function restartQuiz() {
            stopTimer();
            currentQuestion = 0;
            score = 0;
            answered = false;
            showQuestion();
        }

        // Start quiz
        showQuestion();
    </script>
</body>
</html>
