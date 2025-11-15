# nursing-escape-room
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nursing Escape Room</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        
        .container {
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            max-width: 700px;
            width: 100%;
            overflow: hidden;
        }
        
        .header {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            color: white;
            padding: 25px;
            text-align: center;
        }
        
        .header h1 {
            font-size: 1.8em;
            margin-bottom: 8px;
        }

        .header p {
            font-size: 0.95em;
            opacity: 0.95;
        }
        
        .timer {
            font-size: 2.5em;
            font-weight: bold;
            color: #ffeb3b;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
            margin-top: 10px;
        }
        
        .timer.critical {
            color: #ff1744;
            animation: pulse 1s infinite;
        }
        
        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.1); }
        }

        @keyframes unlock {
            0% { transform: scale(1) rotate(0deg); }
            50% { transform: scale(1.2) rotate(10deg); }
            100% { transform: scale(1) rotate(0deg); }
        }
        
        .content {
            padding: 25px;
        }
        
        .clues {
            background: #e8eaf6;
            padding: 18px;
            border-radius: 10px;
            margin-bottom: 20px;
        }

        .clues h3 {
            color: #667eea;
            margin-bottom: 12px;
            font-size: 1.1em;
        }

        .clue-item {
            background: white;
            padding: 10px;
            margin: 8px 0;
            border-radius: 8px;
            border-left: 4px solid #4caf50;
            display: flex;
            align-items: center;
            gap: 10px;
            animation: unlock 0.5s ease;
            font-size: 1.05em;
            font-weight: 600;
        }

        .locks {
            display: flex;
            justify-content: center;
            gap: 12px;
            margin: 15px 0;
        }

        .lock {
            width: 50px;
            height: 50px;
            border: 3px solid #ccc;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.8em;
            background: white;
        }

        .lock.unlocked {
            border-color: #4caf50;
            background: #c8e6c9;
            animation: unlock 0.5s ease;
        }
        
        .room {
            background: #f8f9fa;
            border-left: 5px solid #f5576c;
            padding: 20px;
            margin-bottom: 20px;
            border-radius: 8px;
        }
        
        .room h2 {
            color: #f5576c;
            margin-bottom: 12px;
            font-size: 1.3em;
        }
        
        .room p {
            line-height: 1.6;
            margin-bottom: 12px;
        }

        .info-box {
            background: #fff3e0;
            padding: 12px;
            border-radius: 8px;
            margin: 12px 0;
            border: 2px solid #ff9800;
        }

        .info-box strong {
            color: #e65100;
            display: block;
            margin-bottom: 8px;
        }
        
        .choices {
            margin-top: 20px;
        }
        
        .choice-btn {
            display: block;
            width: 100%;
            padding: 15px;
            margin: 10px 0;
            background: white;
            border: 2px solid #667eea;
            border-radius: 10px;
            font-size: 1em;
            cursor: pointer;
            transition: all 0.3s;
            text-align: left;
            line-height: 1.4;
        }
        
        .choice-btn:hover:not(:disabled) {
            background: #667eea;
            color: white;
            transform: translateX(5px);
        }
        
        .choice-btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }
        
        .feedback {
            margin-top: 20px;
            padding: 18px;
            border-radius: 10px;
            display: none;
            line-height: 1.5;
        }
        
        .feedback.correct {
            background: #c8e6c9;
            border-left: 5px solid #4caf50;
            display: block;
        }
        
        .feedback.wrong {
            background: #ffcdd2;
            border-left: 5px solid #f44336;
            display: block;
        }

        .clue-found {
            background: linear-gradient(135deg, #ffd89b 0%, #19547b 100%);
            color: white;
            padding: 15px;
            border-radius: 10px;
            margin: 15px 0;
            text-align: center;
            font-size: 1.3em;
            font-weight: bold;
            animation: unlock 0.8s ease;
        }

        .puzzle-box {
            background: #f5f5f5;
            padding: 20px;
            border-radius: 10px;
            margin: 20px 0;
        }

        .puzzle-box input {
            width: 100%;
            padding: 15px;
            font-size: 1.1em;
            border: 2px solid #667eea;
            border-radius: 8px;
            margin: 12px 0;
            text-transform: uppercase;
        }

        .btn {
            background: #667eea;
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1em;
            margin-top: 10px;
        }

        .btn:hover {
            background: #5568d3;
        }

        .btn-next {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            display: none;
            margin-top: 15px;
            padding: 14px 35px;
            border-radius: 25px;
        }
        
        .end-screen {
            text-align: center;
            padding: 30px;
        }
        
        .end-screen h2 {
            color: #667eea;
            margin-bottom: 20px;
            font-size: 1.8em;
        }

        .summary-box {
            background: #f3e5f5;
            padding: 20px;
            border-radius: 10px;
            margin: 20px 0;
            text-align: left;
        }

        .summary-box h3 {
            color: #7b1fa2;
            margin-bottom: 12px;
        }

        .summary-box ul {
            padding-left: 25px;
            line-height: 1.8;
        }
        
        .btn-restart {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            color: white;
            border: none;
            padding: 15px 40px;
            border-radius: 25px;
            font-size: 1.1em;
            cursor: pointer;
            margin-top: 20px;
        }
        
        .btn-restart:hover {
            transform: scale(1.05);
        }

        .progress {
            background: #e0e0e0;
            height: 6px;
            border-radius: 3px;
            margin-top: 12px;
            overflow: hidden;
        }

        .progress-fill {
            background: linear-gradient(90deg, #4caf50, #8bc34a);
            height: 100%;
            transition: width 0.5s ease;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🔒 Escape Room: Save the Patient</h1>
            <p>Find 4 clues. Unlock the medicine. Save a life.</p>
            <div class="timer" id="timer">08:00</div>
        </div>
        
        <div class="content">
            <div class="clues">
                <h3>🔑 Clues Found: <span id="clueCount">0/4</span></h3>
                <div class="progress">
                    <div class="progress-fill" id="progressFill" style="width: 0%"></div>
                </div>
                <div class="locks">
                    <div class="lock" id="lock1">🔒</div>
                    <div class="lock" id="lock2">🔒</div>
                    <div class="lock" id="lock3">🔒</div>
                    <div class="lock" id="lock4">🔒</div>
                </div>
                <div id="cluesList"></div>
            </div>
            
            <div id="gameArea"></div>
        </div>
    </div>

    <script>
        let level = 0;
        let clues = 0;
        let time = 480;
        let timer;
        let active = true;
        let found = [];

        const rooms = [
            {
                title: "🏥 Room 1: Something's Wrong",
                story: "A patient just had surgery yesterday. He looks... off. His heart is racing. He's sweating. You need to figure out what's wrong.",
                info: "His heart rate jumped from 78 to 118. Blood pressure dropped. He has a fever.",
                question: "What do you check first?",
                options: [
                    { text: "Look at his surgical wound", right: true, hint: "You check the wound. It's red, hot, and leaking infected fluid. Behind the bandage, you find a hidden note!", clue: "CHECK", icon: "🔍" },
                    { text: "Call the doctor right away", right: false, hint: "The doctor doesn't answer. You wasted 5 minutes with no info to report!" },
                    { text: "Give him pain meds", right: false, hint: "Wrong! He's not in pain—something else is wrong. His condition gets worse." },
                    { text: "Write it down and move on", right: false, hint: "You leave. 2 hours later, he's in critical condition. Too late." }
                ]
            },
            {
                title: "⚡ Room 2: Act Fast!",
                story: "He has a serious infection! His organs are shutting down. You need to act NOW. Every second counts.",
                info: "He's getting worse fast. You know what to do, but what comes FIRST?",
                question: "First action?",
                options: [
                    { text: "Give him oxygen", right: true, hint: "YES! Breathing comes first, always. A drawer pops open with a key inside!", clue: "FAST", icon: "⚡" },
                    { text: "Take blood samples", right: false, hint: "Good idea but... he's turning blue. OXYGEN FIRST!" },
                    { text: "Give antibiotics immediately", right: false, hint: "You need blood samples BEFORE antibiotics. And oxygen comes first anyway!" },
                    { text: "Start IV fluids", right: false, hint: "Important, but breathing comes before everything else!" }
                ]
            },
            {
                title: "📢 Room 3: Speak Up",
                story: "A young doctor shows up. He barely looks at the patient and says 'Just give him Tylenol.' You KNOW that's not enough. He could die.",
                info: "The patient needs strong antibiotics and IV fluids, not just Tylenol.",
                question: "What do you do?",
                options: [
                    { text: "Respectfully explain why Tylenol isn't enough and show the data", right: true, hint: "The doctor reviews your findings. 'You're right. Good catch.' He writes better orders. You find a clue taped under the chart!", clue: "SPEAK", icon: "📢" },
                    { text: "Stay quiet—he's the doctor", right: false, hint: "The patient gets worse. You could have saved him but stayed silent." },
                    { text: "Just follow orders and write notes", right: false, hint: "Notes don't save lives. He crashes while you're writing." },
                    { text: "Go over his head to the boss", right: false, hint: "The boss is angry you didn't talk to the doctor first. Bad move." }
                ]
            },
            {
                title: "💧 Room 4: New Problem",
                story: "Treatment started! He got lots of IV fluids quickly. His blood pressure is better but... now his lungs sound wet and he's barely peeing.",
                info: "He got 3 liters of fluids in 2 hours. Now: wet lungs + almost no urine = ???",
                question: "What's happening?",
                options: [
                    { text: "Too much fluid! His body can't handle it. Get a diuretic (water pill) ASAP.", right: true, hint: "EXACTLY! The treatment caused a NEW problem—fluid overload. Behind the monitor, you find the final clue!", clue: "SAVE", icon: "💚" },
                    { text: "Everything's fine, just monitor", right: false, hint: "His lungs fill with fluid. He stops breathing. You missed it." },
                    { text: "Stop his IV without telling anyone", right: false, hint: "NEVER change treatment without permission. What if you're wrong?" },
                    { text: "Wait an hour to see if it gets better", right: false, hint: "An hour later, he needs emergency breathing support. Too late." }
                ]
            }
        ];

        function start() {
            level = 0;
            clues = 0;
            found = [];
            time = 480;
            active = true;
            updateClues();
            showRoom();
            startTimer();
        }

        function startTimer() {
            if (timer) clearInterval(timer);
            timer = setInterval(() => {
                if (!active) return;
                time--;
                const m = Math.floor(time / 60);
                const s = time % 60;
                document.getElementById('timer').textContent = `${String(m).padStart(2, '0')}:${String(s).padStart(2, '0')}`;
                if (time <= 60) document.getElementById('timer').classList.add('critical');
                if (time <= 0) end(false);
            }, 1000);
        }

        function showRoom() {
            const room = rooms[level];
            let html = `
                <div class="room">
                    <h2>${room.title}</h2>
                    <p>${room.story}</p>
                    <div class="info-box">
                        <strong>📊 What you see:</strong>
                        ${room.info}
                    </div>
                    <p style="font-weight: bold; font-size: 1.1em; margin-top: 12px;">❓ ${room.question}</p>
                </div>
                <div class="choices">
                    ${room.options.map((opt, i) => `
                        <button class="choice-btn" onclick="pick(${i})">${opt.text}</button>
                    `).join('')}
                </div>
                <div class="feedback" id="feedback"></div>
                <button class="btn btn-next" id="nextBtn" onclick="next()">Next Room →</button>
            `;
            document.getElementById('gameArea').innerHTML = html;
        }

        function pick(i) {
            const room = rooms[level];
            const opt = room.options[i];
            const fb = document.getElementById('feedback');
            const btns = document.querySelectorAll('.choice-btn');
            btns.forEach(b => b.disabled = true);
            
            if (opt.right) {
                clues++;
                found.push({ word: opt.clue, icon: opt.icon });
                document.getElementById(`lock${clues}`).innerHTML = '✅';
                document.getElementById(`lock${clues}`).classList.add('unlocked');
                updateClues();
                
                fb.className = 'feedback correct';
                fb.innerHTML = `
                    <h3>✅ Yes! Clue Found!</h3>
                    <p>${opt.hint}</p>
                    <div class="clue-found">${opt.icon} "${opt.clue}" ${opt.icon}</div>
                `;
                
                if (clues === 4) {
                    setTimeout(() => final(), 1500);
                } else {
                    document.getElementById('nextBtn').style.display = 'block';
                }
            } else {
                fb.className = 'feedback wrong';
                fb.innerHTML = `<h3>❌ Not quite!</h3><p>${opt.hint}</p><p style="margin-top: 10px;"><strong>Try again!</strong></p>`;
                setTimeout(() => {
                    fb.style.display = 'none';
                    btns.forEach(b => b.disabled = false);
                }, 3000);
            }
        }

        function updateClues() {
            document.getElementById('clueCount').textContent = `${clues}/4`;
            document.getElementById('progressFill').style.width = `${(clues / 4) * 100}%`;
            document.getElementById('cluesList').innerHTML = found.map(c => `
                <div class="clue-item">${c.icon} <strong>${c.word}</strong></div>
            `).join('');
        }

        function next() {
            level++;
            showRoom();
        }

        function final() {
            document.getElementById('gameArea').innerHTML = `
                <div class="room">
                    <h2>🎯 Final Challenge</h2>
                    <p>Put your 4 clues in the RIGHT ORDER to unlock the medicine cabinet!</p>
                    <p style="margin-top: 12px;"><strong>Your clues:</strong> ${found.map(c => c.word).join(', ')}</p>
                    <p style="margin-top: 10px; background: #fff9c4; padding: 12px; border-radius: 8px;">
                        💡 <strong>Hint:</strong> What do nurses do FIRST? Then act how? Use their what? To do what?
                    </p>
                </div>
                <div class="puzzle-box">
                    <input type="text" id="code" placeholder="WORD-WORD-WORD-WORD">
                    <button class="btn" onclick="unlock()">🔓 Unlock</button>
                    <div id="hint" style="margin-top: 10px; color: #666;">Use dashes: WORD-WORD-WORD-WORD</div>
                </div>
            `;
        }

        function unlock() {
            const input = document.getElementById('code').value.toUpperCase().trim();
            if (input === 'CHECK-FAST-SPEAK-SAVE') {
                end(true);
            } else {
                document.getElementById('hint').innerHTML = '❌ Wrong! Think: Check first → Act fast → Speak up → Save lives';
                document.getElementById('hint').style.color = '#f44336';
            }
        }

        function end(won) {
            active = false;
            clearInterval(timer);
            
            if (!won) {
                document.getElementById('gameArea').innerHTML = `
                    <div class="end-screen">
                        <h2>⏰ Time's Up!</h2>
                        <div class="feedback wrong" style="display: block;">
                            <p>The patient didn't make it. In healthcare, time = life.</p>
                        </div>
                        <button class="btn-restart" onclick="start()">Try Again</button>
                    </div>
                `;
                return;
            }

            document.getElementById('gameArea').innerHTML = `
                <div class="end-screen">
                    <h2>🎉 You Did It!</h2>
                    <div class="feedback correct" style="display: block;">
                        <p><strong>Code: CHECK-FAST-SPEAK-SAVE</strong></p>
                        <p>Patient saved! You unlocked the medicine and used your nursing skills to save a life.</p>
                    </div>
                    
                    <div class="summary-box">
                        <h3>What you just learned:</h3>
                        <ul>
                            <li><strong>CHECK:</strong> Nurses assess patients and catch problems early</li>
                            <li><strong>FAST:</strong> In emergencies, nurses act immediately—no waiting</li>
                            <li><strong>SPEAK:</strong> Nurses advocate and speak up for patients</li>
                            <li><strong>SAVE:</strong> Nurses use their knowledge to save lives</li>
                        </ul>
                        <p style="margin-top: 15px;">This happens EVERY DAY in hospitals. Nurses aren't just helpers—they're life-savers with serious skills and knowledge.</p>
                    </div>
                    
                    <button class="btn-restart" onclick="start()">Play Again</button>
                </div>
            `;
        }

        start();
    </script>
</body>
</html>
