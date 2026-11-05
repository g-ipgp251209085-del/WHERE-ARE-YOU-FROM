<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Year 4 English: World Explorer Passport Challenge</title>
    <style>
        :root {
            --primary: #1e3a8a;
            --accent: #f59e0b;
            --success: #10b981;
            --danger: #ef4444;
            --bg-light: #f3f4f6;
            --card-bg: #ffffff;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #0f172a;
            background-image: 
                radial-gradient(rgba(255, 255, 255, 0.1) 1px, transparent 1px),
                radial-gradient(rgba(255, 255, 255, 0.05) 1px, transparent 1px);
            background-size: 40px 40px;
            background-position: 0 0, 20px 20px;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            color: #334155;
            position: relative;
            overflow-x: hidden;
        }

        /* Decorative Floating Cultural Badges */
        .decor-icon {
            position: absolute;
            font-size: 2.5rem;
            opacity: 0.25;
            user-select: none;
            animation: float 6s ease-in-out infinite alternate;
        }
        @keyframes float {
            0% { transform: translateY(0px) rotate(0deg); }
            100% { transform: translateY(-20px) rotate(10deg); }
        }
        .d1 { top: 8%; left: 6%; animation-delay: 0s; }
        .d2 { top: 15%; right: 8%; animation-delay: 1s; }
        .d3 { bottom: 12%; left: 8%; animation-delay: 2s; }
        .d4 { bottom: 10%; right: 6%; animation-delay: 3s; }

        .game-wrapper {
            background: var(--card-bg);
            border-radius: 24px;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.3);
            width: 100%;
            max-width: 680px;
            padding: 28px;
            position: relative;
            z-index: 10;
            border: 4px solid #3b82f6;
        }

        .header {
            text-align: center;
            margin-bottom: 20px;
        }

        .header h1 {
            color: var(--primary);
            font-size: 1.8rem;
            margin-bottom: 6px;
        }

        .badge-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: #eff6ff;
            padding: 10px 18px;
            border-radius: 12px;
            font-weight: 600;
            color: #1e40af;
            font-size: 0.95rem;
            margin-bottom: 20px;
        }

        /* 1 Question Card Display */
        .card-container {
            background: #f8fafc;
            border: 2px dashed #cbd5e1;
            border-radius: 16px;
            padding: 20px;
            text-align: center;
            margin-bottom: 20px;
        }

        .flag-title {
            font-size: 1.3rem;
            font-weight: bold;
            color: #1e293b;
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .illustration {
            width: 100%;
            height: 180px;
            border-radius: 12px;
            background: #e2e8f0;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 16px;
            overflow: hidden;
            box-shadow: inset 0 2px 4px rgba(0,0,0,0.05);
        }

        .question-text {
            font-size: 1.2rem;
            color: #0f172a;
            font-weight: 600;
            margin-bottom: 16px;
            line-height: 1.4;
        }

        /* Speech Controls */
        .controls {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 12px;
        }

        .mic-btn {
            background-color: #ef4444;
            color: white;
            border: none;
            padding: 14px 28px;
            font-size: 1.05rem;
            font-weight: 600;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.2s ease;
            box-shadow: 0 4px 12px rgba(239, 68, 68, 0.3);
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .mic-btn:hover {
            transform: translateY(-2px);
            background-color: #dc2626;
        }

        .mic-btn.listening {
            background-color: #10b981;
            animation: pulse-ring 1.5s infinite;
        }

        @keyframes pulse-ring {
            0% { box-shadow: 0 0 0 0 rgba(16, 185, 129, 0.7); }
            70% { box-shadow: 0 0 0 15px rgba(16, 185, 129, 0); }
            100% { box-shadow: 0 0 0 0 rgba(16, 185, 129, 0); }
        }

        .transcript-box {
            font-style: italic;
            color: #475569;
            min-height: 24px;
            font-size: 0.95rem;
        }

        .status-message {
            font-size: 1.1rem;
            font-weight: bold;
            min-height: 28px;
            margin-top: 4px;
        }
        .status-message.correct { color: var(--success); }
        .status-message.incorrect { color: var(--danger); }

        .action-btn {
            background-color: #2563eb;
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 10px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: background 0.2s;
            display: none;
            margin-top: 10px;
        }
        .action-btn:hover { background-color: #1d4ed8; }

        .toggle-text-btn {
            background: none;
            border: none;
            color: #64748b;
            text-decoration: underline;
            font-size: 0.85rem;
            cursor: pointer;
            margin-top: 8px;
        }

        .text-input-area {
            display: none;
            gap: 8px;
            margin-top: 10px;
            width: 100%;
            max-width: 400px;
        }

        .text-input-area input {
            flex: 1;
            padding: 10px 14px;
            border: 2px solid #cbd5e1;
            border-radius: 8px;
            font-size: 0.95rem;
        }

        .text-input-area button {
            background-color: #3b82f6;
            color: white;
            border: none;
            padding: 10px 16px;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
        }

        /* Final Results */
        .results {
            text-align: center;
            padding: 20px 0;
        }
        .results h2 {
            color: var(--primary);
            font-size: 2rem;
            margin-bottom: 10px;
        }
        .passport-stamps {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 12px;
            margin: 20px 0;
        }
        .stamp {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            border: 3px dashed #2563eb;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            background: #eff6ff;
        }
    </style>
</head>
<body>

<!-- Floating Cultural Decorative Badges -->
<div class="decor-icon d1">⛩️</div>
<div class="decor-icon d2">🦘</div>
<div class="decor-icon d3">🕌</div>
<div class="decor-icon d4">🗽</div>

<div class="game-wrapper">
    <div class="header">
        <h1>🌍 World Explorer Challenge</h1>
        <p style="color: #64748b; font-size: 0.9rem;">Topic 1: Where Are You From? (LS 2.1.5)</p>
    </div>

    <div class="badge-bar">
        <span>Destination: <strong id="question-count">1 / 8</strong></span>
        <span>Passport Score: <strong id="score-display">0 pts</strong></span>
    </div>

    <div id="game-body">
        <div class="card-container">
            <div class="flag-title" id="country-title">🇲🇾 Destination 1: Malaysia</div>
            
            <div class="illustration" id="illustration-box">
                <!-- SVG Illustration injected via JavaScript -->
            </div>

            <div class="question-text" id="question-prompt">
                Loading question...
            </div>

            <div class="controls">
                <button class="mic-btn" id="mic-btn" onclick="toggleListening()">
                    🎤 Click to Speak Answer
                </button>

                <div class="transcript-box" id="transcript">Click mic and speak your descriptive sentence...</div>
                <div class="status-message" id="status"></div>

                <div class="text-input-area" id="text-input-area">
                    <input type="text" id="manual-input" placeholder="Type your descriptive sentence...">
                    <button onclick="submitTypedAnswer()">Submit</button>
                </div>

                <button class="toggle-text-btn" onclick="toggleInputMethod()">Can't use microphone? Type instead</button>

                <button class="action-btn" id="next-btn" onclick="nextQuestion()">Next Destination ➔</button>
            </div>
        </div>
    </div>
</div>

<script>
    const destinations = [
        {
            country: "🇲🇾 Malaysia",
            title: "Malaysia - KLCC Twin Towers",
            svg: `<svg viewBox="0 0 300 150" width="100%" height="100%">
                    <rect width="300" height="150" fill="#e0f2fe"/>
                    <!-- Twin Towers -->
                    <rect x="110" y="30" width="30" height="100" fill="#94a3b8"/>
                    <rect x="160" y="30" width="30" height="100" fill="#94a3b8"/>
                    <polygon points="125,10 115,30 135,30" fill="#64748b"/>
                    <polygon points="175,10 165,30 185,30" fill="#64748b"/>
                    <rect x="135" y="70" width="30" height="10" fill="#cbd5e1"/>
                    <circle cx="150" cy="20" r="12" fill="#fef08a"/>
                  </svg>`,
            prompt: "Look at the tall KLCC Twin Towers! Can you describe them?",
            speechHint: "Example: They are tall glass towers in Malaysia.",
            keywords: ["tall", "glass", "towers", "malaysia", "building", "twin"]
        },
        {
            country: "🇧🇷 Brazil",
            title: "Brazil - Carnival Parade",
            svg: `<svg viewBox="0 0 300 150" width="100%" height="100%">
                    <rect width="300" height="150" fill="#fef9c3"/>
                    <!-- Dancer feather hat -->
                    <path d="M150 40 Q130 10 110 30 Q150 20 150 40 Z" fill="#ef4444"/>
                    <path d="M150 40 Q150 5 150 30 Q150 20 150 40 Z" fill="#10b981"/>
                    <path d="M150 40 Q170 10 190 30 Q150 20 150 40 Z" fill="#3b82f6"/>
                    <circle cx="150" cy="55" r="14" fill="#fde047"/>
                    <rect x="140" y="70" width="20" height="40" fill="#f59e0b"/>
                  </svg>`,
            prompt: "Look at the dancer's vibrant outfit! What is he wearing?",
            speechHint: "Example: He is wearing colorful Brazilian carnival clothes.",
            keywords: ["wearing", "colorful", "clothes", "outfit", "costume", "brazilian", "brazil"]
        },
        {
            country: "🇦🇺 Australia",
            title: "Australia - Outback Kangaroo",
            svg: `<svg viewBox="0 0 300 150" width="100%" height="100%">
                    <rect width="300" height="150" fill="#ffedd5"/>
                    <!-- Kangaroo Silhouette -->
                    <path d="M120 110 Q140 100 150 80 Q160 60 170 50 Q180 40 185 45 Q175 55 165 65 Q170 80 190 95 L200 110 L170 110 Q150 110 120 110 Z" fill="#ea580c"/>
                    <circle cx="180" cy="42" r="3" fill="#ffffff"/>
                  </svg>`,
            prompt: "What animal is this and what can it do?",
            speechHint: "Example: It is a kangaroo and it can jump high.",
            keywords: ["kangaroo", "jump", "hop", "australia", "animal"]
        },
        {
            country: "🇯🇵 Japan",
            title: "Japan - Mount Fuji & Cherry Blossoms",
            svg: `<svg viewBox="0 0 300 150" width="100%" height="100%">
                    <rect width="300" height="150" fill="#fce7f3"/>
                    <!-- Mt Fuji -->
                    <polygon points="150,30 80,120 220,120" fill="#38bdf8"/>
                    <polygon points="150,30 130,55 170,55" fill="#ffffff"/>
                    <!-- Cherry blossom branch -->
                    <path d="M40 20 Q100 40 120 30" stroke="#78350f" stroke-width="4" fill="none"/>
                    <circle cx="80" cy="25" r="8" fill="#f472b6"/>
                    <circle cx="100" cy="35" r="7" fill="#f472b6"/>
                  </svg>`,
            prompt: "Describe the cherry blossom tree near Mount Fuji!",
            speechHint: "Example: It has beautiful pink flowers.",
            keywords: ["pink", "flowers", "cherry", "blossoms", "beautiful", "tree", "japan"]
        },
        {
            country: "🇬🇧 United Kingdom",
            title: "United Kingdom - London Red Bus",
            svg: `<svg viewBox="0 0 300 150" width="100%" height="100%">
                    <rect width="300" height="150" fill="#f1f5f9"/>
                    <!-- Red Double Decker Bus -->
                    <rect x="80" y="40" width="140" height="70" rx="10" fill="#dc2626"/>
                    <rect x="90" y="50" width="25" height="18" fill="#e2e8f0"/>
                    <rect x="125" y="50" width="25" height="18" fill="#e2e8f0"/>
                    <rect x="160" y="50" width="25" height="18" fill="#e2e8f0"/>
                    <rect x="90" y="75" width="25" height="18" fill="#e2e8f0"/>
                    <rect x="125" y="75" width="25" height="18" fill="#e2e8f0"/>
                    <circle cx="110" cy="110" r="12" fill="#1e293b"/>
                    <circle cx="190" cy="110" r="12" fill="#1e293b"/>
                  </svg>`,
            prompt: "Describe the famous bus from London!",
            speechHint: "Example: It is a big red double-decker bus.",
            keywords: ["red", "big", "double", "decker", "bus", "london", "uk"]
        },
        {
            country: "🇨🇳 China",
            title: "China - Giant Panda",
            svg: `<svg viewBox="0 0 300 150" width="100%" height="100%">
                    <rect width="300" height="150" fill="#ecfdf5"/>
                    <!-- Panda -->
                    <circle cx="150" cy="80" r="35" fill="#ffffff" stroke="#000" stroke-width="2"/>
                    <circle cx="125" cy="55" r="10" fill="#000000"/>
                    <circle cx="175" cy="55" r="10" fill="#000000"/>
                    <ellipse cx="138" cy="75" rx="6" ry="8" fill="#000000"/>
                    <ellipse cx="162" cy="75" rx="6" ry="8" fill="#000000"/>
                    <circle cx="150" cy="88" r="5" fill="#000000"/>
                  </svg>`,
            prompt: "Look at the cute panda! Describe what it looks like.",
            speechHint: "Example: The panda is black and white.",
            keywords: ["panda", "black", "white", "cute", "fluffy", "bear", "china"]
        },
        {
            country: "🇮🇳 India",
            title: "India - Taj Mahal",
            svg: `<svg viewBox="0 0 300 150" width="100%" height="100%">
                    <rect width="300" height="150" fill="#fdf4ff"/>
                    <!-- Taj Mahal Dome -->
                    <path d="M120 110 L120 70 Q120 40 150 30 Q180 40 180 70 L180 110 Z" fill="#ffffff" stroke="#cbd5e1" stroke-width="2"/>
                    <rect x="90" y="50" width="12" height="60" fill="#ffffff" stroke="#cbd5e1"/>
                    <rect x="198" y="50" width="12" height="60" fill="#ffffff" stroke="#cbd5e1"/>
                  </svg>`,
            prompt: "Look at the magnificent Taj Mahal! Describe its color and material.",
            speechHint: "Example: It is a large white marble building.",
            keywords: ["white", "marble", "large", "building", "palace", "beautiful", "india"]
        },
        {
            country: "🇺🇸 United States",
            title: "United States - Statue of Liberty",
            svg: `<svg viewBox="0 0 300 150" width="100%" height="100%">
                    <rect width="300" height="150" fill="#e0f2fe"/>
                    <!-- Torch -->
                    <path d="M150 110 L150 60 L140 45 L160 45 L150 60" fill="#0d9488"/>
                    <polygon points="150,20 142,38 158,38" fill="#f59e0b"/>
                    <circle cx="150" cy="25" r="8" fill="#ef4444"/>
                  </svg>`,
            prompt: "Look at the Statue of Liberty! What is she holding in her hand?",
            speechHint: "Example: She is holding a bright golden torch.",
            keywords: ["holding", "torch", "golden", "bright", "flame", "statue", "liberty"]
        }
    ];

    let currentIdx = 0;
    let score = 0;
    let recognition;
    let isListening = false;

    // Initialize Web Speech API
    const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;

    if (SpeechRecognition) {
        recognition = new SpeechRecognition();
        recognition.continuous = false;
        recognition.lang = 'en-US';
        recognition.interimResults = false;

        recognition.onstart = () => {
            isListening = true;
            const btn = document.getElementById('mic-btn');
            btn.classList.add('listening');
            btn.innerText = "🎙️ Listening... Speak now!";
            document.getElementById('status').innerText = "";
        };

        recognition.onresult = (event) => {
            const speechText = event.results[0][0].transcript;
            document.getElementById('transcript').innerText = `You said: "${speechText}"`;
            evaluateAnswer(speechText);
        };

        recognition.onerror = () => {
            document.getElementById('status').innerText = "Could not hear clearly. Please try again!";
            resetMicState();
        };

        recognition.onend = () => {
            resetMicState();
        };
    }

    function loadDestination() {
        const dest = destinations[currentIdx];
        document.getElementById('country-title').innerText = dest.country;
        document.getElementById('illustration-box').innerHTML = dest.svg;
        document.getElementById('question-prompt').innerText = dest.prompt;
        document.getElementById('question-count').innerText = `${currentIdx + 1} / ${destinations.length}`;
        document.getElementById('transcript').innerText = dest.speechHint;
        document.getElementById('status').innerText = "";
        document.getElementById('next-btn').style.display = "none";
        document.getElementById('mic-btn').disabled = false;
        document.getElementById('manual-input').value = "";

        // Play Question Audio Readout
        if ('speechSynthesis' in window) {
            window.speechSynthesis.cancel();
            const utterance = new SpeechSynthesisUtterance(dest.prompt);
            utterance.rate = 0.9;
            window.speechSynthesis.speak(utterance);
        }
    }

    function toggleListening() {
        if (!recognition) {
            alert("Speech recognition is not supported on this browser. Please try Chrome or Edge, or use the type option!");
            return;
        }
        if (isListening) {
            recognition.stop();
        } else {
            recognition.start();
        }
    }

    function resetMicState() {
        isListening = false;
        const btn = document.getElementById('mic-btn');
        btn.classList.remove('listening');
        btn.innerText = "🎤 Click to Speak Answer";
    }

    function evaluateAnswer(userText) {
        const lowerText = userText.toLowerCase();
        const keywords = destinations[currentIdx].keywords;
        
        // Count matching descriptive words
        const matches = keywords.filter(kw => lowerText.includes(kw));
        const isCorrect = matches.length >= 1; // Needs at least 1 key descriptive word

        const statusEl = document.getElementById('status');
        if (isCorrect) {
            statusEl.innerText = "🎉 Excellent descriptive sentence!";
            statusEl.className = "status-message correct";
            score += 10;
            document.getElementById('score-display').innerText = `${score} pts`;
            document.getElementById('mic-btn').disabled = true;
            document.getElementById('next-btn').style.display = "inline-block";
        } else {
            statusEl.innerText = "❌ Try describing it using more details!";
            statusEl.className = "status-message incorrect";
        }
    }

    function toggleInputMethod() {
        const area = document.getElementById('text-input-area');
        area.style.display = area.style.display === "flex" ? "none" : "flex";
    }

    function submitTypedAnswer() {
        const val = document.getElementById('manual-input').value;
        if (val.trim() !== "") {
            document.getElementById('transcript').innerText = `You wrote: "${val}"`;
            evaluateAnswer(val);
        }
    }

    function nextQuestion() {
        currentIdx++;
        if (currentIdx < destinations.length) {
            loadDestination();
        } else {
            showFinalPassport();
        }
    }

    function showFinalPassport() {
        const stamps = destinations.map(d => `<div class="stamp" title="${d.country}">${d.country.split(' ')[0]}</div>`).join('');
        document.getElementById('game-body').innerHTML = `
            <div class="results">
                <h2>🎓 Passport Completed!</h2>
                <p style="font-size: 1.1rem; color: #475569; margin-bottom: 15px;">
                    Great job describing landmarks, people, and objects around the world!
                </p>
                <div style="font-size: 1.4rem; font-weight: bold; color: #2563eb; margin-bottom: 20px;">
                    Final Score: ${score} / ${destinations.length * 10}
                </div>
                <div class="passport-stamps">${stamps}</div>
                <button class="action-btn" style="display:inline-block; margin-top:20px;" onclick="location.reload()">
                    🔄 Play Again
                </button>
            </div>
        `;
    }

    // Start on load
    window.onload = loadDestination;
</script>

</body>
</html>
