# may-2026-tracker

html_content = '''<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>May 2026 - Complete Life Tracker</title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Rajdhani:wght@300;500;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --neon-blue: #00f0ff;
            --neon-pink: #ff00e4;
            --neon-purple: #b829dd;
            --neon-green: #00ff88;
            --neon-orange: #ff6b35;
            --dark-bg: #0a0a1a;
            --card-bg: rgba(20, 20, 45, 0.85);
            --glass: rgba(255, 255, 255, 0.05);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Rajdhani', sans-serif;
            background: var(--dark-bg);
            color: #e0e0ff;
            min-height: 100vh;
            overflow-x: hidden;
        }

        /* Animated Background */
        .bg-animation {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            background: linear-gradient(135deg, #0a0a1a 0%, #1a0a2e 50%, #0a1a2e 100%);
        }

        .bg-animation::before {
            content: '';
            position: absolute;
            width: 200%;
            height: 200%;
            top: -50%;
            left: -50%;
            background: 
                radial-gradient(circle at 20% 80%, rgba(0, 240, 255, 0.08) 0%, transparent 50%),
                radial-gradient(circle at 80% 20%, rgba(255, 0, 228, 0.08) 0%, transparent 50%),
                radial-gradient(circle at 40% 40%, rgba(184, 41, 221, 0.06) 0%, transparent 50%);
            animation: bgMove 20s ease-in-out infinite;
        }

        .stars {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            pointer-events: none;
        }

        .star {
            position: absolute;
            width: 2px;
            height: 2px;
            background: white;
            border-radius: 50%;
            animation: twinkle 3s ease-in-out infinite;
        }

        @keyframes twinkle {
            0%, 100% { opacity: 0.2; }
            50% { opacity: 1; }
        }

        @keyframes bgMove {
            0%, 100% { transform: translate(0, 0) rotate(0deg); }
            33% { transform: translate(30px, -30px) rotate(1deg); }
            66% { transform: translate(-20px, 20px) rotate(-1deg); }
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }

        header {
            text-align: center;
            padding: 30px 0;
            position: relative;
        }

        header h1 {
            font-family: 'Orbitron', sans-serif;
            font-size: 3rem;
            font-weight: 900;
            background: linear-gradient(90deg, var(--neon-blue), var(--neon-pink), var(--neon-purple));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            text-shadow: 0 0 30px rgba(0, 240, 255, 0.3);
            letter-spacing: 3px;
        }

        header p {
            color: #8899aa;
            font-size: 1.1rem;
            margin-top: 10px;
        }

        .main-grid {
            display: grid;
            grid-template-columns: 1fr 2fr;
            gap: 20px;
            margin-top: 20px;
        }

        @media (max-width: 1024px) {
            .main-grid {
                grid-template-columns: 1fr;
            }
        }

        .card {
            background: var(--card-bg);
            border: 1px solid rgba(0, 240, 255, 0.15);
            border-radius: 20px;
            padding: 25px;
            backdrop-filter: blur(10px);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3), inset 0 1px 0 rgba(255, 255, 255, 0.05);
            transition: all 0.3s ease;
        }

        .card:hover {
            border-color: rgba(0, 240, 255, 0.3);
            box-shadow: 0 12px 40px rgba(0, 240, 255, 0.1), inset 0 1px 0 rgba(255, 255, 255, 0.1);
        }

        .card-title {
            font-family: 'Orbitron', sans-serif;
            font-size: 1.2rem;
            color: var(--neon-blue);
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        .card-title::after {
            content: '';
            flex: 1;
            height: 1px;
            background: linear-gradient(90deg, var(--neon-blue), transparent);
        }

        /* Calendar */
        .calendar-grid {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 8px;
        }

        .day-header {
            text-align: center;
            font-weight: 700;
            color: var(--neon-purple);
            font-size: 0.85rem;
            padding: 8px 0;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .calendar-day {
            aspect-ratio: 1;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            background: var(--glass);
            border: 1px solid rgba(255, 255, 255, 0.05);
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            font-size: 0.9rem;
            min-height: 50px;
        }

        .calendar-day:hover {
            border-color: var(--neon-blue);
            background: rgba(0, 240, 255, 0.08);
            transform: translateY(-2px);
        }

        .calendar-day.active {
            border-color: var(--neon-blue);
            background: rgba(0, 240, 255, 0.15);
            box-shadow: 0 0 20px rgba(0, 240, 255, 0.2);
        }

        .calendar-day .day-num {
            font-weight: 700;
            font-size: 1.1rem;
        }

        .calendar-day .day-eff {
            font-size: 0.65rem;
            color: var(--neon-green);
            margin-top: 2px;
        }

        .calendar-day.jummah {
            border-color: var(--neon-orange);
        }

        .calendar-day.jummah .day-num {
            color: var(--neon-orange);
        }

        .calendar-day.empty {
            opacity: 0.3;
            cursor: default;
            pointer-events: none;
        }

        /* Task Items */
        .task-item {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 14px 16px;
            margin-bottom: 10px;
            background: var(--glass);
            border: 1px solid rgba(255, 255, 255, 0.05);
            border-radius: 14px;
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .task-item:hover {
            background: rgba(255, 255, 255, 0.08);
            border-color: rgba(0, 240, 255, 0.2);
        }

        .task-item.completed {
            border-color: var(--neon-green);
            background: rgba(0, 255, 136, 0.08);
        }

        .task-item.completed .task-icon {
            color: var(--neon-green);
        }

        .task-left {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .task-icon {
            font-size: 1.4rem;
            width: 36px;
            text-align: center;
        }

        .task-info h4 {
            font-size: 0.95rem;
            font-weight: 600;
            color: #e0e0ff;
        }

        .task-info span {
            font-size: 0.8rem;
            color: #8899aa;
        }

        .task-points {
            font-family: 'Orbitron', sans-serif;
            font-weight: 700;
            color: var(--neon-green);
            font-size: 0.9rem;
        }

        /* Namaz Section */
        .namaz-grid {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 8px;
            margin-top: 15px;
        }

        .namaz-btn {
            padding: 12px 8px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 12px;
            background: var(--glass);
            color: #8899aa;
            font-family: 'Rajdhani', sans-serif;
            font-weight: 600;
            font-size: 0.85rem;
            cursor: pointer;
            transition: all 0.3s ease;
            text-align: center;
        }

        .namaz-btn:hover {
            border-color: var(--neon-blue);
            color: var(--neon-blue);
        }

        .namaz-btn.ada {
            border-color: var(--neon-green);
            background: rgba(0, 255, 136, 0.15);
            color: var(--neon-green);
        }

        .namaz-btn.qaza {
            border-color: var(--neon-orange);
            background: rgba(255, 107, 53, 0.15);
            color: var(--neon-orange);
        }

        .qaza-toggle {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 15px;
            padding: 10px;
            background: var(--glass);
            border-radius: 10px;
            cursor: pointer;
        }

        .qaza-toggle input {
            width: 18px;
            height: 18px;
            accent-color: var(--neon-orange);
        }

        .qaza-toggle label {
            font-size: 0.9rem;
            color: var(--neon-orange);
            font-weight: 600;
            cursor: pointer;
        }

        /* Slider */
        .slider-container {
            margin-top: 15px;
        }

        .slider-labels {
            display: flex;
            justify-content: space-between;
            font-size: 0.75rem;
            color: #8899aa;
            margin-bottom: 8px;
        }

        input[type="range"] {
            width: 100%;
            height: 8px;
            border-radius: 4px;
            background: var(--glass);
            outline: none;
            -webkit-appearance: none;
        }

        input[type="range"]::-webkit-slider-thumb {
            -webkit-appearance: none;
            width: 20px;
            height: 20px;
            border-radius: 50%;
            background: var(--neon-blue);
            cursor: pointer;
            box-shadow: 0 0 10px rgba(0, 240, 255, 0.5);
        }

        .slider-value {
            text-align: center;
            margin-top: 8px;
            font-family: 'Orbitron', sans-serif;
            color: var(--neon-blue);
            font-size: 0.9rem;
        }

        /* Finance */
        .finance-input {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 12px;
            padding: 12px;
            background: var(--glass);
            border-radius: 12px;
        }

        .finance-input label {
            font-weight: 600;
            min-width: 120px;
            font-size: 0.9rem;
        }

        .finance-input input {
            flex: 1;
            background: transparent;
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 8px;
            padding: 8px 12px;
            color: #e0e0ff;
            font-family: 'Rajdhani', sans-serif;
            font-size: 1rem;
            outline: none;
        }

        .finance-input input:focus {
            border-color: var(--neon-blue);
        }

        .finance-input .balance {
            font-family: 'Orbitron', sans-serif;
            color: var(--neon-green);
            font-size: 0.9rem;
            min-width: 80px;
            text-align: right;
        }

        /* Stats */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin-top: 20px;
        }

        .stat-box {
            background: var(--glass);
            border: 1px solid rgba(255, 255, 255, 0.05);
            border-radius: 16px;
            padding: 20px;
            text-align: center;
            transition: all 0.3s ease;
        }

        .stat-box:hover {
            border-color: rgba(0, 240, 255, 0.2);
            transform: translateY(-3px);
        }

        .stat-value {
            font-family: 'Orbitron', sans-serif;
            font-size: 2rem;
            font-weight: 900;
            color: var(--neon-blue);
        }

        .stat-label {
            font-size: 0.85rem;
            color: #8899aa;
            margin-top: 5px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .efficiency-bar {
            width: 100%;
            height: 30px;
            background: var(--glass);
            border-radius: 15px;
            overflow: hidden;
            margin-top: 20px;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .efficiency-fill {
            height: 100%;
            background: linear-gradient(90deg, var(--neon-green), var(--neon-blue));
            border-radius: 15px;
            transition: width 0.5s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            font-family: 'Orbitron', sans-serif;
            font-weight: 700;
            font-size: 0.85rem;
            color: #000;
            min-width: 50px;
        }

        /* Mission Toggle */
        .mission-toggle {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 15px;
            padding: 12px;
            background: var(--glass);
            border-radius: 12px;
            cursor: pointer;
            border: 1px solid rgba(0, 240, 255, 0.2);
        }

        .mission-toggle input {
            width: 18px;
            height: 18px;
            accent-color: var(--neon-blue);
        }

        .mission-toggle label {
            font-size: 0.9rem;
            color: var(--neon-blue);
            font-weight: 600;
            cursor: pointer;
        }

        .mission-status {
            margin-left: auto;
            font-size: 0.8rem;
            padding: 4px 10px;
            border-radius: 20px;
            background: rgba(255, 0, 0, 0.2);
            color: #ff4444;
        }

        .mission-status.on {
            background: rgba(0, 255, 136, 0.2);
            color: var(--neon-green);
        }

        /* Date Display */
        .date-display {
            font-family: 'Orbitron', sans-serif;
            font-size: 1.5rem;
            color: var(--neon-pink);
            text-align: center;
            margin-bottom: 20px;
            text-shadow: 0 0 20px rgba(255, 0, 228, 0.3);
        }

        /* OTP Date Notice */
        .otp-notice {
            background: rgba(184, 41, 221, 0.1);
            border: 1px solid var(--neon-purple);
            border-radius: 10px;
            padding: 10px;
            margin-bottom: 15px;
            font-size: 0.85rem;
            color: var(--neon-purple);
            text-align: center;
        }

        .otp-notice.active {
            background: rgba(0, 255, 136, 0.1);
            border-color: var(--neon-green);
            color: var(--neon-green);
        }

        /* TikTok Notice */
        .tiktok-notice {
            background: rgba(0, 240, 255, 0.1);
            border: 1px solid var(--neon-blue);
            border-radius: 10px;
            padding: 10px;
            margin-bottom: 15px;
            font-size: 0.85rem;
            color: var(--neon-blue);
            text-align: center;
        }

        .tiktok-notice.active {
            background: rgba(0, 255, 136, 0.1);
            border-color: var(--neon-green);
            color: var(--neon-green);
        }

        /* Save Button */
        .save-btn {
            width: 100%;
            padding: 16px;
            margin-top: 20px;
            background: linear-gradient(135deg, var(--neon-blue), var(--neon-purple));
            border: none;
            border-radius: 14px;
            color: white;
            font-family: 'Orbitron', sans-serif;
            font-weight: 700;
            font-size: 1rem;
            letter-spacing: 2px;
            text-transform: uppercase;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 20px rgba(0, 240, 255, 0.3);
        }

        .save-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 30px rgba(0, 240, 255, 0.4);
        }

        .save-btn:active {
            transform: translateY(0);
        }

        /* Section Divider */
        .section-divider {
            height: 1px;
            background: linear-gradient(90deg, transparent, rgba(0, 240, 255, 0.3), transparent);
            margin: 25px 0;
        }

        /* Responsive */
        @media (max-width: 768px) {
            header h1 { font-size: 2rem; }
            .namaz-grid { grid-template-columns: repeat(3, 1fr); }
            .stats-grid { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>
    <div class="bg-animation"></div>
    <div class="stars" id="stars"></div>

    <div class="container">
        <header>
            <h1>May 2026</h1>
            <p>Complete Life Tracker | 1 May - 31 May 2026</p>
        </header>

        <div class="main-grid">
            <!-- Left Column -->
            <div class="left-column">
                <!-- Calendar -->
                <div class="card">
                    <div class="card-title">Calendar</div>
                    <div class="calendar-grid" id="calendar">
                        <div class="day-header">Sun</div>
                        <div class="day-header">Mon</div>
                        <div class="day-header">Tue</div>
                        <div class="day-header">Wed</div>
                        <div class="day-header">Thu</div>
                        <div class="day-header">Fri</div>
                        <div class="day-header">Sat</div>
                    </div>
                </div>

                <!-- Monthly Stats -->
                <div class="card" style="margin-top: 20px;">
                    <div class="card-title">May 2026 Overview</div>
                    <div class="stats-grid">
                        <div class="stat-box">
                            <div class="stat-value" id="totalHealth">0</div>
                            <div class="stat-label">Health Points</div>
                        </div>
                        <div class="stat-box">
                            <div class="stat-value" id="totalNamaz">0</div>
                            <div class="stat-label">Namaz Points</div>
                        </div>
                        <div class="stat-box">
                            <div class="stat-value" id="totalSpiritual">0</div>
                            <div class="stat-label">Spiritual</div>
                        </div>
                        <div class="stat-box">
                            <div class="stat-value" id="totalWork">0</div>
                            <div class="stat-label">Work Tasks</div>
                        </div>
                        <div class="stat-box">
                            <div class="stat-value" id="totalQaza">0</div>
                            <div class="stat-label">Qaza Done</div>
                        </div>
                        <div class="stat-box">
                            <div class="stat-value" id="totalMAvoided">0</div>
                            <div class="stat-label">M Avoided</div>
                        </div>
                        <div class="stat-box">
                            <div class="stat-value" id="mmmBalance">₨0</div>
                            <div class="stat-label">MMM Balance</div>
                        </div>
                        <div class="stat-box">
                            <div class="stat-value" id="papaBalance">₨0</div>
                            <div class="stat-label">Papa Balance</div>
                        </div>
                    </div>
                    <div class="stat-box" style="margin-top: 15px;">
                        <div class="stat-value" id="originalBalance">₨0</div>
                        <div class="stat-label">Original Account</div>
                    </div>
                    <div class="efficiency-bar">
                        <div class="efficiency-fill" id="avgEfficiency" style="width: 0%">0%</div>
                    </div>
                </div>
            </div>

            <!-- Right Column -->
            <div class="right-column">
                <div class="card">
                    <div class="date-display" id="selectedDate">1 May 2026</div>

                    <!-- Health Section -->
                    <div class="card-title">Health</div>
                    
                    <div class="task-item" data-task="brush" data-points="3" onclick="toggleTask(this)">
                        <div class="task-left">
                            <div class="task-icon">🪥</div>
                            <div class="task-info">
                                <h4>Brush</h4>
                                <span>+3 points</span>
                            </div>
                        </div>
                        <div class="task-points">+3</div>
                    </div>

                    <div class="task-item" data-task="facewash" data-points="3" onclick="toggleTask(this)">
                        <div class="task-left">
                            <div class="task-icon">🧼</div>
                            <div class="task-info">
                                <h4>Face Wash</h4>
                                <span>+3 points</span>
                            </div>
                        </div>
                        <div class="task-points">+3</div>
                    </div>

                    <div class="task-item" data-task="water" data-points="3" onclick="toggleTask(this)">
                        <div class="task-left">
                            <div class="task-icon">💧</div>
                            <div class="task-info">
                                <h4>Water Intake</h4>
                                <span>+3 points</span>
                            </div>
                        </div>
                        <div class="task-points">+3</div>
                    </div>

                    <div class="section-divider"></div>

                    <!-- Spiritual Section -->
                    <div class="card-title">Spiritual</div>

                    <div class="qaza-toggle">
                        <input type="checkbox" id="qazaMode" onchange="toggleQazaMode()">
                        <label for="qazaMode">Enable Qaza Option</label>
                    </div>

                    <div style="margin-bottom: 10px; font-size: 0.9rem; color: #8899aa;">5 Namaz (10 pts if all Ada)</div>
                    <div class="namaz-grid" id="namazGrid">
                        <button class="namaz-btn" data-namaz="fajr" onclick="toggleNamaz(this)">Fajr</button>
                        <button class="namaz-btn" data-namaz="zuhr" onclick="toggleNamaz(this)">Zuhr</button>
                        <button class="namaz-btn" data-namaz="asr" onclick="toggleNamaz(this)">Asr</button>
                        <button class="namaz-btn" data-namaz="maghrib" onclick="toggleNamaz(this)">Maghrib</button>
                        <button class="namaz-btn" data-namaz="isha" onclick="toggleNamaz(this)">Isha</button>
                    </div>

                    <div class="task-item" data-task="tahajjud" data-points="5" onclick="toggleTask(this)" style="margin-top: 15px;">
                        <div class="task-left">
                            <div class="task-icon">🌙</div>
                            <div class="task-info">
                                <h4>Tahajjud</h4>
                                <span>+5 points</span>
                            </div>
                        </div>
                        <div class="task-points">+5</div>
                    </div>

                    <div class="task-item" data-task="dua" data-points="5" onclick="toggleTask(this)">
                        <div class="task-left">
                            <div class="task-icon">🤲</div>
                            <div class="task-info">
                                <h4>Dua</h4>
                                <span>+5 points</span>
                            </div>
                        </div>
                        <div class="task-points">+5</div>
                    </div>

                    <div class="task-item" data-task="quran" data-points="3" onclick="toggleTask(this)">
                        <div class="task-left">
                            <div class="task-icon">📖</div>
                            <div class="task-info">
                                <h4>Quran - 1 Ruku</h4>
                                <span>+3 points</span>
                            </div>
                        </div>
                        <div class="task-points">+3</div>
                    </div>

                    <div class="otp-notice" id="otpNotice">
                        🔒 OTP starts from 12th May 2026
                    </div>

                    <div class="task-item" data-task="otp" data-points="3" onclick="toggleTask(this)" id="otpTask">
                        <div class="task-left">
                            <div class="task-icon">📿</div>
                            <div class="task-info">
                                <h4>OTP</h4>
                                <span>+3 points (From 12 May)</span>
                            </div>
                        </div>
                        <div class="task-points">+3</div>
                    </div>

                    <div class="task-item" data-task="mstatus" data-points="5" onclick="toggleTask(this)">
                        <div class="task-left">
                            <div class="task-icon">Ⓜ️</div>
                            <div class="task-info">
                                <h4>M Status</h4>
                                <span>+5 if avoided</span>
                            </div>
                        </div>
                        <div class="task-points" id="mPoints">+5</div>
                    </div>

                    <div class="section-divider"></div>

                    <!-- Work Section -->
                    <div class="card-title">Work</div>

                    <div class="mission-toggle">
                        <input type="checkbox" id="missionToggle" onchange="toggleMission()">
                        <label for="missionToggle">Mission ON/OFF</label>
                        <div class="mission-status" id="missionStatus">OFF</div>
                    </div>

                    <div class="task-item" data-task="mission" data-points="3" onclick="toggleTask(this)" id="missionTask">
                        <div class="task-left">
                            <div class="task-icon">🎯</div>
                            <div class="task-info">
                                <h4>Mission</h4>
                                <span>+3 points (Only when ON)</span>
                            </div>
                        </div>
                        <div class="task-points">+3</div>
                    </div>

                    <div class="task-item" data-task="linkedin" data-points="3" onclick="toggleTask(this)">
                        <div class="task-left">
                            <div class="task-icon">💼</div>
                            <div class="task-info">
                                <h4>LinkedIn</h4>
                                <span>+3 points</span>
                            </div>
                        </div>
                        <div class="task-points">+3</div>
                    </div>

                    <div class="tiktok-notice" id="tiktokNotice">
                        🔒 TikTok Post starts from 12th May 2026
                    </div>

                    <div class="task-item" data-task="tiktok" data-points="3" onclick="toggleTask(this)" id="tiktokTask">
                        <div class="task-left">
                            <div class="task-icon">🎵</div>
                            <div class="task-info">
                                <h4>TikTok Post</h4>
                                <span>+3 points (From 12 May)</span>
                            </div>
                        </div>
                        <div class="task-points">+3</div>
                    </div>

                    <div class="task-item" data-task="snap" data-points="3" onclick="toggleTask(this)">
                        <div class="task-left">
                            <div class="task-icon">👻</div>
                            <div class="task-info">
                                <h4>Snap</h4>
                                <span>+3 points</span>
                            </div>
                        </div>
                        <div class="task-points">+3</div>
                    </div>

                    <div class="task-item" style="cursor: default;">
                        <div class="task-left">
                            <div class="task-icon">📱</div>
                            <div class="task-info">
                                <h4>Mobile Usage</h4>
                                <span>&lt;4h = 3pts | 4-8h = 1pt | 8-12h = 0pts</span>
                            </div>
                        </div>
                        <div class="task-points" id="mobilePoints">+3</div>
                    </div>

                    <div class="slider-container">
                        <div class="slider-labels">
                            <span>0h</span>
                            <span>4h</span>
                            <span>8h</span>
                            <span>12h</span>
                        </div>
                        <input type="range" id="mobileSlider" min="0" max="12" step="0.5" value="0" oninput="updateMobileUsage(this.value)">
                        <div class="slider-value" id="mobileValue">0 hours = +3 points</div>
                    </div>

                    <div class="section-divider"></div>

                    <!-- Finance Section -->
                    <div class="card-title">Finance</div>

                    <div class="finance-input">
                        <label>MMM Account</label>
                        <input type="number" id="mmmInput" placeholder="Enter amount" onchange="updateFinance('mmm', this.value)">
                        <div class="balance" id="mmmDisplay">₨0</div>
                    </div>

                    <div class="finance-input">
                        <label>Papa Account</label>
                        <input type="number" id="papaInput" placeholder="Enter amount" onchange="updateFinance('papa', this.value)">
                        <div class="balance" id="papaDisplay">₨0</div>
                    </div>

                    <div class="finance-input">
                        <label>Original Account</label>
                        <input type="number" id="originalInput" placeholder="Enter amount" onchange="updateFinance('original', this.value)">
                        <div class="balance" id="originalDisplay">₨0</div>
                    </div>

                    <button class="save-btn" onclick="saveDay()">Save Day Data</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // ==================== DATA STORAGE ====================
        const mayData = JSON.parse(localStorage.getItem('may2026_tracker')) || {};
        let currentDate = new Date(2026, 4, 1); // May 1, 2026
        let qazaMode = false;
        let missionOn = false;

        // ==================== STAR BACKGROUND ====================
        function createStars() {
            const starsContainer = document.getElementById('stars');
            for (let i = 0; i < 100; i++) {
                const star = document.createElement('div');
                star.className = 'star';
                star.style.left = Math.random() * 100 + '%';
                star.style.top = Math.random() * 100 + '%';
                star.style.animationDelay = Math.random() * 3 + 's';
                star.style.width = Math.random() * 3 + 1 + 'px';
                star.style.height = star.style.width;
                starsContainer.appendChild(star);
            }
        }

        // ==================== CALENDAR ====================
        function generateCalendar() {
            const calendar = document.getElementById('calendar');
            const daysInMonth = 31;
            const firstDay = new Date(2026, 4, 1).getDay(); // Friday = 5
            
            // Empty cells before 1st
            for (let i = 0; i < firstDay; i++) {
                const empty = document.createElement('div');
                empty.className = 'calendar-day empty';
                calendar.appendChild(empty);
            }

            // Days
            for (let day = 1; day <= daysInMonth; day++) {
                const dateStr = `2026-05-${String(day).padStart(2, '0')}`;
                const dayDiv = document.createElement('div');
                dayDiv.className = 'calendar-day';
                dayDiv.dataset.date = dateStr;
                
                const dateObj = new Date(2026, 4, day);
                const dayOfWeek = dateObj.getDay();
                
                // Jummah (Friday)
                if (dayOfWeek === 5) {
                    dayDiv.classList.add('jummah');
                }

                // Check if data exists
                if (mayData[dateStr]) {
                    const eff = calculateEfficiency(mayData[dateStr]);
                    dayDiv.innerHTML = `<div class="day-num">${day}</div><div class="day-eff">${eff}%</div>`;
                } else {
                    dayDiv.innerHTML = `<div class="day-num">${day}</div>`;
                }

                dayDiv.onclick = () => selectDate(day);
                calendar.appendChild(dayDiv);
            }
        }

        function selectDate(day) {
            currentDate = new Date(2026, 4, day);
            const dateStr = formatDate(currentDate);
            
            // Update active state
            document.querySelectorAll('.calendar-day').forEach(d => d.classList.remove('active'));
            document.querySelector(`[data-date="${dateStr}"]`)?.classList.add('active');
            
            // Update display
            document.getElementById('selectedDate').textContent = `${day} May 2026`;
            
            // Load data
            loadDayData(dateStr);
            
            // Check date restrictions
            checkDateRestrictions(day);
        }

        function checkDateRestrictions(day) {
            const otpNotice = document.getElementById('otpNotice');
            const otpTask = document.getElementById('otpTask');
            const tiktokNotice = document.getElementById('tiktokNotice');
            const tiktokTask = document.getElementById('tiktokTask');

            // OTP starts from 12th May
            if (day >= 12) {
                otpNotice.textContent = '✅ OTP is Active (From 12 May)';
                otpNotice.classList.add('active');
                otpTask.style.opacity = '1';
                otpTask.style.pointerEvents = 'auto';
            } else {
                otpNotice.textContent = '🔒 OTP starts from 12th May 2026';
                otpNotice.classList.remove('active');
                otpTask.style.opacity = '0.4';
                otpTask.style.pointerEvents = 'none';
            }

            // TikTok starts from 12th May
            if (day >= 12) {
                tiktokNotice.textContent = '✅ TikTok Post is Active (From 12 May)';
                tiktokNotice.classList.add('active');
                tiktokTask.style.opacity = '1';
                tiktokTask.style.pointerEvents = 'auto';
            } else {
                tiktokNotice.textContent = '🔒 TikTok Post starts from 12th May 2026';
                tiktokNotice.classList.remove('active');
                tiktokTask.style.opacity = '0.4';
                tiktokTask.style.pointerEvents = 'none';
            }
        }

        // ==================== TASK TOGGLE ====================
        function toggleTask(element) {
            const task = element.dataset.task;
            const dateStr = formatDate(currentDate);
            
            if (!mayData[dateStr]) mayData[dateStr] = {};
            if (!mayData[dateStr].tasks) mayData[dateStr].tasks = {};
            
            // Toggle
            mayData[dateStr].tasks[task] = !mayData[dateStr].tasks[task];
            
            // Update UI
            if (mayData[dateStr].tasks[task]) {
                element.classList.add('completed');
            } else {
                element.classList.remove('completed');
            }
            
            // Recalculate efficiency
            updateEfficiency(dateStr);
            updateCalendarDay(dateStr);
        }

        // ==================== NAMAZ ====================
        function toggleQazaMode() {
            qazaMode = document.getElementById('qazaMode').checked;
        }

        function toggleNamaz(btn) {
            const namaz = btn.dataset.namaz;
            const dateStr = formatDate(currentDate);
            
            if (!mayData[dateStr]) mayData[dateStr] = {};
            if (!mayData[dateStr].namaz) mayData[dateStr].namaz = {};
            
            // Cycle: none -> ada -> qaza (if enabled) -> none
            const current = mayData[dateStr].namaz[namaz] || 'none';
            
            if (current === 'none') {
                mayData[dateStr].namaz[namaz] = 'ada';
                btn.className = 'namaz-btn ada';
            } else if (current === 'ada' && qazaMode) {
                mayData[dateStr].namaz[namaz] = 'qaza';
                btn.className = 'namaz-btn qaza';
            } else {
                mayData[dateStr].namaz[namaz] = 'none';
                btn.className = 'namaz-btn';
            }
            
            updateEfficiency(dateStr);
            updateCalendarDay(dateStr);
        }

        // ==================== MISSION TOGGLE ====================
        function toggleMission() {
            missionOn = document.getElementById('missionToggle').checked;
            const status = document.getElementById('missionStatus');
            const missionTask = document.getElementById('missionTask');
            
            if (missionOn) {
                status.textContent = 'ON';
                status.classList.add('on');
                missionTask.style.opacity = '1';
                missionTask.style.pointerEvents = 'auto';
            } else {
                status.textContent = 'OFF';
                status.classList.remove('on');
                missionTask.style.opacity = '0.4';
                missionTask.style.pointerEvents = 'none';
                
                // Reset mission task if turning off
                const dateStr = formatDate(currentDate);
                if (mayData[dateStr] && mayData[dateStr].tasks) {
                    mayData[dateStr].tasks.mission = false;
                    missionTask.classList.remove('completed');
                }
            }
            
            const dateStr = formatDate(currentDate);
            updateEfficiency(dateStr);
            updateCalendarDay(dateStr);
        }

        // ==================== MOBILE USAGE ====================
        function updateMobileUsage(hours) {
            const dateStr = formatDate(currentDate);
            if (!mayData[dateStr]) mayData[dateStr] = {};
            mayData[dateStr].mobileHours = parseFloat(hours);
            
            let points = 0;
            let label = '';
            
            if (hours < 4) {
                points = 3;
                label = `${hours} hours = +3 points`;
            } else if (hours >= 4 && hours < 8) {
                points = 1;
                label = `${hours} hours = +1 point`;
            } else {
                points = 0;
                label = `${hours} hours = 0 points`;
            }
            
            document.getElementById('mobileValue').textContent = label;
            document.getElementById('mobilePoints').textContent = `+${points}`;
            
            mayData[dateStr].mobilePoints = points;
            updateEfficiency(dateStr);
            updateCalendarDay(dateStr);
        }

        // ==================== FINANCE ====================
        function updateFinance(account, value) {
            const dateStr = formatDate(currentDate);
            if (!mayData[dateStr]) mayData[dateStr] = {};
            if (!mayData[dateStr].finance) mayData[dateStr].finance = {};
            
            const numValue = parseFloat(value) || 0;
            mayData[dateStr].finance[account] = numValue;
            
            // MMM affects Original, but Original does NOT affect MMM
            if (account === 'mmm') {
                mayData[dateStr].finance.original = numValue;
                document.getElementById('originalInput').value = numValue;
                document.getElementById('originalDisplay').textContent = '₨' + numValue;
            }
            
            document.getElementById(account + 'Display').textContent = '₨' + numValue;
            
            updateMonthlyStats();
        }

        // ==================== EFFICIENCY CALCULATION ====================
        function calculateEfficiency(dayData) {
            if (!dayData) return 0;
            
            let totalPossible = 0;
            let earned = 0;
            
            const day = currentDate.getDate();
            
            // Health tasks (always count)
            const healthTasks = ['brush', 'facewash', 'water'];
            healthTasks.forEach(t => {
                totalPossible += 3;
                if (dayData.tasks && dayData.tasks[t]) earned += 3;
            });
            
            // Namaz
            if (dayData.namaz) {
                let adaCount = 0;
                let qazaCount = 0;
                Object.values(dayData.namaz).forEach(status => {
                    if (status === 'ada') adaCount++;
                    if (status === 'qaza') qazaCount++;
                });
                
                totalPossible += 10;
                if (adaCount === 5) earned += 10;
                else if (adaCount + qazaCount === 5) earned += 5;
                else earned += (adaCount * 2);
            } else {
                totalPossible += 10;
            }
            
            // Tahajjud
            totalPossible += 5;
            if (dayData.tasks && dayData.tasks.tahajjud) earned += 5;
            
            // Dua
            totalPossible += 5;
            if (dayData.tasks && dayData.tasks.dua) earned += 5;
            
            // Quran
            totalPossible += 3;
            if (dayData.tasks && dayData.tasks.quran) earned += 3;
            
            // OTP (only from 12th May)
            if (day >= 12) {
                totalPossible += 3;
                if (dayData.tasks && dayData.tasks.otp) earned += 3;
            }
            
            // M Status
            totalPossible += 5;
            if (dayData.tasks && dayData.tasks.mstatus) earned += 5;
            
            // Mission (only if ON)
            if (missionOn || (dayData.missionOn)) {
                totalPossible += 3;
                if (dayData.tasks && dayData.tasks.mission) earned += 3;
            }
            
            // LinkedIn
            totalPossible += 3;
            if (dayData.tasks && dayData.tasks.linkedin) earned += 3;
            
            // TikTok (only from 12th May)
            if (day >= 12) {
                totalPossible += 3;
                if (dayData.tasks && dayData.tasks.tiktok) earned += 3;
            }
            
            // Snap
            totalPossible += 3;
            if (dayData.tasks && dayData.tasks.snap) earned += 3;
            
            // Mobile Usage
            totalPossible += 3;
            earned += (dayData.mobilePoints || 0);
            
            if (totalPossible === 0) return 0;
            return Math.round((earned / totalPossible) * 100);
        }

        function updateEfficiency(dateStr) {
            const eff = calculateEfficiency(mayData[dateStr]);
            if (!mayData[dateStr]) mayData[dateStr] = {};
            mayData[dateStr].efficiency = eff;
        }

        function updateCalendarDay(dateStr) {
            const dayEl = document.querySelector(`[data-date="${dateStr}"]`);
            if (dayEl) {
                const day = parseInt(dateStr.split('-')[2]);
                const eff = calculateEfficiency(mayData[dateStr]);
                dayEl.innerHTML = `<div class="day-num">${day}</div><div class="day-eff">${eff}%</div>`;
            }
        }

        // ==================== SAVE ====================
        function saveDay() {
            const dateStr = formatDate(currentDate);
            if (!mayData[dateStr]) mayData[dateStr] = {};
            
            mayData[dateStr].missionOn = missionOn;
            mayData[dateStr].saved = true;
            
            localStorage.setItem('may2026_tracker', JSON.stringify(mayData));
            
            updateMonthlyStats();
            updateCalendarDay(dateStr);
            
            // Show save animation
            const btn = document.querySelector('.save-btn');
            const originalText = btn.textContent;
            btn.textContent = '✓ Saved!';
            btn.style.background = 'linear-gradient(135deg, #00ff88, #00cc66)';
            setTimeout(() => {
                btn.textContent = originalText;
                btn.style.background = '';
            }, 1500);
        }

        // ==================== LOAD DAY DATA ====================
        function loadDayData(dateStr) {
            const data = mayData[dateStr] || {};
            
            // Reset all tasks
            document.querySelectorAll('.task-item[data-task]').forEach(el => {
                el.classList.remove('completed');
            });
            document.querySelectorAll('.namaz-btn').forEach(btn => {
                btn.className = 'namaz-btn';
            });
            
            // Load tasks
            if (data.tasks) {
                Object.entries(data.tasks).forEach(([task, completed]) => {
                    if (completed) {
                        const el = document.querySelector(`[data-task="${task}"]`);
                        if (el) el.classList.add('completed');
                    }
                });
            }
            
            // Load namaz
            if (data.namaz) {
                Object.entries(data.namaz).forEach(([namaz, status]) => {
                    const btn = document.querySelector(`[data-namaz="${namaz}"]`);
                    if (btn) {
                        if (status === 'ada') btn.className = 'namaz-btn ada';
                        else if (status === 'qaza') btn.className = 'namaz-btn qaza';
                    }
                });
            }
            
            // Load mission state
            if (data.missionOn !== undefined) {
                document.getElementById('missionToggle').checked = data.missionOn;
                toggleMission();
            }
            
            // Load mobile usage
            if (data.mobileHours !== undefined) {
                document.getElementById('mobileSlider').value = data.mobileHours;
                updateMobileUsage(data.mobileHours);
            } else {
                document.getElementById('mobileSlider').value = 0;
                document.getElementById('mobileValue').textContent = '0 hours = +3 points';
                document.getElementById('mobilePoints').textContent = '+3';
            }
            
            // Load finance
            if (data.finance) {
                document.getElementById('mmmInput').value = data.finance.mmm || '';
                document.getElementById('mmmDisplay').textContent = '₨' + (data.finance.mmm || 0);
                document.getElementById('papaInput').value = data.finance.papa || '';
                document.getElementById('papaDisplay').textContent = '₨' + (data.finance.papa || 0);
                document.getElementById('originalInput').value = data.finance.original || '';
                document.getElementById('originalDisplay').textContent = '₨' + (data.finance.original || 0);
            } else {
                document.getElementById('mmmInput').value = '';
                document.getElementById('mmmDisplay').textContent = '₨0';
                document.getElementById('papaInput').value = '';
                document.getElementById('papaDisplay').textContent = '₨0';
                document.getElementById('originalInput').value = '';
                document.getElementById('originalDisplay').textContent = '₨0';
            }
            
            checkDateRestrictions(currentDate.getDate());
        }

        // ==================== MONTHLY STATS ====================
        function updateMonthlyStats() {
            let health = 0, namaz = 0, spiritual = 0, work = 0, qaza = 0, mAvoided = 0;
            let mmmTotal = 0, papaTotal = 0, originalTotal = 0;
            let totalEff = 0, effCount = 0;
            
            Object.entries(mayData).forEach(([date, data]) => {
                if (!data.saved) return;
                
                // Health
                if (data.tasks) {
                    if (data.tasks.brush) health += 3;
                    if (data.tasks.facewash) health += 3;
                    if (data.tasks.water) health += 3;
                }
                
                // Namaz
                if (data.namaz) {
                    let adaCount = 0, qazaCount = 0;
                    Object.values(data.namaz).forEach(status => {
                        if (status === 'ada') adaCount++;
                        if (status === 'qaza') qazaCount++;
                    });
                    if (adaCount === 5) namaz += 10;
                    else if (adaCount + qazaCount === 5) namaz += 5;
                    else namaz += (adaCount * 2);
                    qaza += qazaCount;
                }
                
                // Spiritual
                if (data.tasks) {
                    if (data.tasks.tahajjud) spiritual += 5;
                    if (data.tasks.dua) spiritual += 5;
                    if (data.tasks.quran) spiritual += 3;
                    if (data.tasks.otp) spiritual += 3;
                    if (data.tasks.mstatus) { spiritual += 5; mAvoided++; }
                }
                
                // Work
                if (data.tasks) {
                    if (data.tasks.mission && data.missionOn) work += 3;
                    if (data.tasks.linkedin) work += 3;
                    if (data.tasks.tiktok) work += 3;
                    if (data.tasks.snap) work += 3;
                }
                work += (data.mobilePoints || 0);
                
                // Finance
                if (data.finance) {
                    mmmTotal += (data.finance.mmm || 0);
                    papaTotal += (data.finance.papa || 0);
                    originalTotal += (data.finance.original || 0);
                }
                
                // Efficiency
                if (data.efficiency !== undefined) {
                    totalEff += data.efficiency;
                    effCount++;
                }
            });
            
            document.getElementById('totalHealth').textContent = health;
            document.getElementById('totalNamaz').textContent = namaz;
            document.getElementById('totalSpiritual').textContent = spiritual;
            document.getElementById('totalWork').textContent = work;
            document.getElementById('totalQaza').textContent = qaza;
            document.getElementById('totalMAvoided').textContent = mAvoided;
            document.getElementById('mmmBalance').textContent = '₨' + mmmTotal;
            document.getElementById('papaBalance').textContent = '₨' + papaTotal;
            document.getElementById('originalBalance').textContent = '₨' + originalTotal;
            
            const avgEff = effCount > 0 ? Math.round(totalEff / effCount) : 0;
            const effBar = document.getElementById('avgEfficiency');
            effBar.style.width = avgEff + '%';
            effBar.textContent = avgEff + '%';
        }

        // ==================== UTILITIES ====================
        function formatDate(date) {
            return date.toISOString().split('T')[0];
        }

        // ==================== INIT ====================
        function init() {
            createStars();
            generateCalendar();
            selectDate(1);
            updateMonthlyStats();
        }

        init();
    </script>
</body>
</html>'''

# Save to output
with open('/mnt/agents/output/may-2026-tracker.html', 'w', encoding='utf-8') as f:
    f.write(html_content)

print("May 2026 Tracker saved successfully!")
print(f"File size: {len(html_content)} characters")
