<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Brain and Mind Academy - AP Calculus AB: Slope of Tangent & Normal Lines</title>
    <!-- Desmos API Script -->
    <script src="https://www.desmos.com/api/v1.8/calculator.js?apiKey=d2822b107a6c49f6a00a221957776319"></script>
    <style>
        :root {
            --primary-header: #1e3a8a;
            --header-gradient: linear-gradient(135deg, #0f172a 0%, #1e3a8a 100%);
            --accent-gold: #d97706;
            --accent-gold-light: #fcd34d;
            --correct-green: #059669;
            --correct-bg: #d1fae5;
            --incorrect-red: #dc2626;
            --incorrect-bg: #fee2e2;
            --skipped-orange: #f59e0b;
            --skipped-bg: #fef3c7;
            --bg-body: #f8fafc;
            --text-dark: #1e293b;
            --text-muted: #64748b;
            --border-color: #e2e8f0;
            --card-bg: #ffffff;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--bg-body);
            color: var(--text-dark);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        header {
            background: var(--header-gradient);
            color: white;
            padding: 1.25rem 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
        }

        .brand-title {
            font-size: 1.5rem;
            font-weight: 700;
            letter-spacing: 0.5px;
            color: #ffffff;
        }

        .brand-subtitle {
            font-size: 0.9rem;
            color: var(--accent-gold-light);
            font-weight: 600;
            margin-top: 2px;
        }

        .user-info {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        .user-email {
            font-size: 0.85rem;
            background: rgba(255, 255, 255, 0.15);
            padding: 0.4rem 0.8rem;
            border-radius: 6px;
        }

        .btn {
            padding: 0.6rem 1.25rem;
            border: none;
            border-radius: 6px;
            font-weight: 600;
            font-size: 0.9rem;
            cursor: pointer;
            transition: all 0.2s ease;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
        }

        .btn-sm {
            padding: 0.4rem 0.85rem;
            font-size: 0.8rem;
            border-radius: 4px;
        }

        .btn-primary { background-color: var(--primary-header); color: white; }
        .btn-primary:hover { background-color: #172554; }
        .btn-gold { background-color: var(--accent-gold); color: white; }
        .btn-gold:hover { background-color: #b45309; }
        .btn-outline { background: transparent; border: 1.5px solid var(--border-color); color: var(--text-dark); }
        .btn-outline:hover { background-color: #f1f5f9; }
        .btn-danger { background-color: var(--incorrect-red); color: white; }
        .btn-danger:hover { background-color: #b91c1c; }
        .btn-success { background-color: var(--correct-green); color: white; }
        .btn-success:hover { background-color: #047857; }

        .screen {
            display: none;
            padding: 2rem;
            max-width: 1400px;
            margin: 0 auto;
            width: 100%;
            flex: 1;
        }

        .screen.active { display: block; }

        #auth-screen {
            max-width: 450px;
            margin: auto;
            padding-top: 4rem;
        }

        .auth-card {
            background: var(--card-bg);
            padding: 2.5rem;
            border-radius: 12px;
            box-shadow: 0 10px 25px -5px rgba(0,0,0,0.05);
            border: 1px solid var(--border-color);
            text-align: center;
        }

        .auth-card h2 { margin-bottom: 0.5rem; color: var(--primary-header); }
        .auth-card p { color: var(--text-muted); font-size: 0.9rem; margin-bottom: 1.5rem; }

        .form-group { margin-bottom: 1.25rem; text-align: left; }
        .form-group label { display: block; margin-bottom: 0.4rem; font-size: 0.85rem; font-weight: 600; }
        .form-group input {
            width: 100%; padding: 0.75rem; border: 1px solid var(--border-color);
            border-radius: 6px; font-size: 1rem; outline: none;
        }
        .form-group input:focus { border-color: var(--primary-header); box-shadow: 0 0 0 3px rgba(30, 58, 138, 0.1); }

        .quiz-container {
            display: grid;
            grid-template-columns: 1fr 380px;
            gap: 2rem;
            align-items: start;
        }

        .quiz-card {
            background: var(--card-bg);
            border-radius: 12px;
            padding: 2rem;
            border: 1px solid var(--border-color);
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.05);
        }

        .quiz-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 2px solid var(--bg-body);
            padding-bottom: 1rem;
            margin-bottom: 1.5rem;
        }

        .q-badge {
            background: #eff6ff;
            color: var(--primary-header);
            font-weight: 700;
            padding: 0.3rem 0.8rem;
            border-radius: 20px;
            font-size: 0.85rem;
        }

        .q-title {
            font-size: 1.2rem;
            line-height: 1.5;
            margin-bottom: 0.75rem;
            font-weight: 700;
            color: var(--primary-header);
        }

        .problem-statement {
            background: #f1f5f9;
            border-left: 4px solid var(--primary-header);
            padding: 1rem 1.25rem;
            border-radius: 6px;
            font-size: 1rem;
            line-height: 1.6;
            margin-bottom: 1.5rem;
            font-weight: 600;
        }

        /* Micro Step Blocks */
        .step-block {
            background: #f8fafc;
            border: 1.5px solid var(--border-color);
            border-radius: 10px;
            padding: 1.25rem;
            margin-bottom: 1.5rem;
            transition: all 0.3s ease;
        }

        .step-block.locked {
            opacity: 0.4;
            pointer-events: none;
            filter: grayscale(0.8);
        }

        .step-block.active-step {
            border-color: var(--primary-header);
            box-shadow: 0 0 0 3px rgba(30, 58, 138, 0.1);
        }

        .step-block.completed-step {
            border-color: var(--correct-green);
            background-color: #f0fdf4;
        }

        .step-block.skipped-step {
            border-color: var(--skipped-orange);
            background-color: var(--skipped-bg);
        }

        .step-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 0.75rem;
        }

        .step-tag {
            font-weight: 700;
            font-size: 0.85rem;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            color: var(--accent-gold);
        }

        .completed-step .step-tag { color: var(--correct-green); }
        .skipped-step .step-tag { color: var(--skipped-orange); }

        .step-prompt {
            font-size: 0.95rem;
            font-weight: 600;
            margin-bottom: 1rem;
            line-height: 1.5;
        }

        .step-actions {
            display: flex;
            gap: 0.5rem;
            margin-top: 1rem;
            padding-top: 0.75rem;
            border-top: 1px dashed var(--border-color);
        }

        .step-options-list {
            display: flex;
            flex-direction: column;
            gap: 0.6rem;
            margin-bottom: 0.5rem;
        }

        .step-option-item {
            display: flex;
            align-items: center;
            padding: 0.75rem 1rem;
            border: 1.5px solid var(--border-color);
            border-radius: 6px;
            cursor: pointer;
            transition: all 0.2s ease;
            background: white;
            font-size: 0.95rem;
            font-weight: 600;
        }

        .step-option-item:hover:not(.disabled) {
            border-color: var(--primary-header);
            background-color: #eff6ff;
        }

        .step-option-item.selected {
            border-color: var(--primary-header);
            background-color: #eff6ff;
        }

        .step-option-item.correct {
            border-color: var(--correct-green);
            background-color: var(--correct-bg);
            color: #065f46;
        }

        .step-option-item.incorrect {
            border-color: var(--incorrect-red);
            background-color: var(--incorrect-bg);
            color: #991b1b;
        }

        .step-option-item.disabled { cursor: default; }

        .step-opt-prefix {
            width: 24px;
            height: 24px;
            border-radius: 50%;
            background: #e2e8f0;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 700;
            font-size: 0.75rem;
            margin-right: 0.75rem;
            flex-shrink: 0;
        }

        .step-option-item.selected .step-opt-prefix { background: var(--primary-header); color: white; }
        .step-option-item.correct .step-opt-prefix { background: var(--correct-green); color: white; }
        .step-option-item.incorrect .step-opt-prefix { background: var(--incorrect-red); color: white; }

        .action-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding-top: 1.5rem;
            border-top: 1px solid var(--border-color);
        }

        .rationale-box {
            margin-top: 1.5rem;
            padding: 1.25rem;
            border-radius: 8px;
            background: #f1f5f9;
            border-left: 4px solid var(--primary-header);
        }

        .rationale-title { font-weight: 700; color: var(--primary-header); margin-bottom: 0.5rem; }

        .quiz-sidebar {
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
            position: sticky;
            top: 2rem;
        }

        .sidebar-card {
            background: var(--card-bg);
            border-radius: 12px;
            padding: 1.5rem;
            border: 1px solid var(--border-color);
        }

        .sidebar-title {
            font-size: 1.1rem;
            font-weight: 700;
            margin-bottom: 1rem;
            color: var(--primary-header);
        }

        .legend-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 0.5rem;
            margin-bottom: 1.5rem;
            font-size: 0.8rem;
        }

        .legend-item { display: flex; align-items: center; gap: 0.4rem; }
        .legend-dot { width: 12px; height: 12px; border-radius: 3px; }
        .dot-active { border: 2px solid var(--primary-header); background: transparent; }
        .dot-attempted { background: var(--correct-green); }
        .dot-skipped { background: var(--skipped-orange); }
        .dot-unvisited { background: #cbd5e1; }

        .question-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 0.5rem;
            max-height: 220px;
            overflow-y: auto;
        }

        .grid-btn {
            aspect-ratio: 1; border: 1px solid var(--border-color); background: #f8fafc;
            color: var(--text-dark); border-radius: 6px; font-weight: 600; font-size: 0.85rem;
            cursor: pointer; transition: all 0.15s ease;
        }

        .grid-btn.active { border: 2px solid var(--primary-header); color: var(--primary-header); font-weight: 800; background: #eff6ff; }
        .grid-btn.attempted { background: var(--correct-green); color: white; border-color: var(--correct-green); }
        .grid-btn.skipped { background: var(--skipped-orange); color: white; border-color: var(--skipped-orange); }

        /* Calculator Styling */
        .calc-display {
            width: 100%;
            padding: 0.6rem;
            font-size: 1.2rem;
            text-align: right;
            border: 1px solid var(--border-color);
            border-radius: 6px;
            margin-bottom: 0.75rem;
            background: #f8fafc;
            font-family: monospace;
            font-weight: bold;
        }

        .calc-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 0.35rem;
        }

        .calc-btn {
            padding: 0.55rem 0.2rem;
            font-size: 0.85rem;
            font-weight: 600;
            border: 1px solid var(--border-color);
            border-radius: 4px;
            background: #fff;
            cursor: pointer;
        }

        .calc-btn:hover { background: #e2e8f0; }
        .calc-btn.op { background: #eff6ff; color: var(--primary-header); }
        .calc-btn.special { background: var(--skipped-bg); color: var(--accent-gold); }

        #desmos-calculator {
            width: 100%;
            height: 280px;
            border-radius: 8px;
            border: 1px solid var(--border-color);
        }

        .math-frac {
            display: inline-flex;
            flex-direction: column;
            vertical-align: middle;
            text-align: center;
            font-size: 0.9em;
            padding: 0 0.2em;
        }

        .math-num { border-bottom: 1px solid var(--text-dark); padding-bottom: 1px; }
        .math-den { padding-top: 1px; }

        .results-summary {
            background: var(--card-bg); border-radius: 12px; padding: 2rem;
            border: 1px solid var(--border-color); margin-bottom: 2rem; text-align: center;
        }

        .score-circle {
            width: 130px; height: 130px; border-radius: 50%; background: var(--header-gradient);
            color: white; display: flex; flex-direction: column; align-items: center;
            justify-content: center; margin: 1rem auto;
        }

        .score-num { font-size: 2.2rem; font-weight: 800; color: var(--accent-gold-light); }
        .review-list { display: flex; flex-direction: column; gap: 1.5rem; }
        .review-card { background: var(--card-bg); border-radius: 12px; padding: 1.5rem; border: 1px solid var(--border-color); }

        .status-tag {
            padding: 0.25rem 0.6rem; border-radius: 4px; font-size: 0.75rem;
            font-weight: 700; text-transform: uppercase;
        }

        .tag-correct { background: var(--correct-bg); color: #065f46; }
        .tag-incorrect { background: var(--incorrect-bg); color: #991b1b; }
        .tag-skipped { background: var(--skipped-bg); color: #92400e; }

        @media (max-width: 992px) {
            .quiz-container { grid-template-columns: 1fr; }
            .quiz-sidebar { position: static; }
        }
    </style>
</head>
<body>

    <header>
        <div>
            <div class="brand-title">BRAIN AND MIND ACADEMY</div>
            <div class="brand-subtitle">AP Calculus AB • Slope of the Tangent Line & Normal Line (Micro-Learning Sheet)</div>
        </div>
        <div class="user-info" id="user-header-info" style="display: none;">
            <span class="user-email" id="display-user-email"></span>
            <button class="btn btn-outline" style="color:white; border-color:rgba(255,255,255,0.3);" onclick="logout()">Switch User</button>
        </div>
    </header>

    <!-- Auth Screen -->
    <div id="auth-screen" class="screen active">
        <div class="auth-card">
            <h2>Student Portal</h2>
            <p>Enter your student email to access your step-by-step AP Calculus learning card sheet.</p>
            <form onsubmit="handleLogin(event)">
                <div class="form-group">
                    <label for="email-input">Email ID</label>
                    <input type="email" id="email-input" required placeholder="student@academy.edu">
                </div>
                <button type="submit" class="btn btn-primary" style="width: 100%;">Start Progressive Learning Sheet</button>
            </form>
        </div>
    </div>

    <!-- Quiz Screen -->
    <div id="quiz-screen" class="screen">
        <div class="quiz-container">
            <div class="quiz-card">
                <div class="quiz-header">
                    <span class="q-badge" id="q-number-badge">Card 1 of 12</span>
                    <span style="font-size: 0.85rem; color: var(--text-muted);">Guided Calculus Steps</span>
                </div>

                <div class="q-title" id="q-title-text"></div>
                <div class="problem-statement" id="q-problem-text"></div>

                <!-- STEP 1 BLOCK -->
                <div class="step-block active-step" id="step1-block">
                    <div class="step-header">
                        <span class="step-tag">Step 1: Formula & Definition Setup</span>
                        <span id="step1-status-tag" style="font-weight:700; font-size:0.8rem; color:var(--accent-gold);">In Progress</span>
                    </div>
                    <div class="step-prompt" id="step1-prompt">Choose the appropriate calculus definition or formula in full form:</div>
                    <div class="step-options-list" id="step1-options-container"></div>
                    <div class="step-actions" id="step1-actions">
                        <button class="btn btn-primary btn-sm" onclick="checkStep(1)">Check Step 1</button>
                        <button class="btn btn-gold btn-sm" onclick="skipStep(1)">Skip Step 1</button>
                    </div>
                </div>

                <!-- STEP 2 BLOCK -->
                <div class="step-block locked" id="step2-block">
                    <div class="step-header">
                        <span class="step-tag">Step 2: Substitution & Algebraic Simplification</span>
                        <span id="step2-status-tag" style="font-weight:700; font-size:0.8rem; color:var(--text-muted);">Locked</span>
                    </div>
                    <div class="step-prompt" id="step2-prompt">Formulate the simplified limit expression or substituted ratio:</div>
                    <div class="step-options-list" id="step2-options-container"></div>
                    <div class="step-actions" id="step2-actions" style="display:none;">
                        <button class="btn btn-primary btn-sm" onclick="checkStep(2)">Check Step 2</button>
                        <button class="btn btn-gold btn-sm" onclick="skipStep(2)">Skip Step 2</button>
                    </div>
                </div>

                <!-- STEP 3 BLOCK -->
                <div class="step-block locked" id="step3-block">
                    <div class="step-header">
                        <span class="step-tag">Step 3: Final Calculation & Evaluation</span>
                        <span id="step3-status-tag" style="font-weight:700; font-size:0.8rem; color:var(--text-muted);">Locked</span>
                    </div>
                    <div class="step-prompt" id="step3-prompt">Determine the final calculated rate, slope, or line equation in full form:</div>
                    <div class="step-options-list" id="step3-options-container"></div>
                    <div class="step-actions" id="step3-actions" style="display:none;">
                        <button class="btn btn-primary btn-sm" onclick="checkStep(3)">Check Step 3</button>
                        <button class="btn btn-gold btn-sm" onclick="skipStep(3)">Skip Step 3</button>
                    </div>
                </div>

                <div class="action-bar">
                    <button class="btn btn-danger" id="skip-card-btn" onclick="skipEntireCard()">Skip Entire Card</button>
                    <button class="btn btn-outline" id="next-btn" style="display: none;" onclick="nextQuestion()">Next Card &rarr;</button>
                </div>

                <div class="rationale-box" id="rationale-container" style="display: none;">
                    <div class="rationale-title">Step-by-Step Mathematical Solution</div>
                    <div id="rationale-text" style="font-size: 0.95rem; line-height: 1.6;"></div>
                </div>
            </div>

            <!-- Sidebar -->
            <div class="quiz-sidebar">
                <div class="sidebar-card">
                    <div class="sidebar-title">Card Palette (1–12)</div>
                    <div class="legend-grid">
                        <div class="legend-item"><div class="legend-dot dot-active"></div> Active</div>
                        <div class="legend-item"><div class="legend-dot dot-attempted"></div> Submitted</div>
                        <div class="legend-item"><div class="legend-dot dot-skipped"></div> Skipped</div>
                        <div class="legend-item"><div class="legend-dot dot-unvisited"></div> Unvisited</div>
                    </div>
                    <div class="question-grid" id="question-grid"></div>
                    <div style="margin-top: 1rem;">
                        <button class="btn btn-danger" style="width: 100%;" onclick="finishTest()">Finish & Submit Sheet</button>
                    </div>
                </div>

                <!-- Desmos Graphing Calculator Embed -->
                <div class="sidebar-card">
                    <div class="sidebar-title" style="margin-bottom:0.5rem;">Desmos Graph Plotter</div>
                    <div id="desmos-calculator"></div>
                </div>

                <!-- Scientific Calculator -->
                <div class="sidebar-card">
                    <div class="sidebar-title" style="margin-bottom:0.5rem;">Scientific Calculator</div>
                    <input type="text" class="calc-display" id="calc-disp" readonly value="0">
                    <div class="calc-grid">
                        <button class="calc-btn special" onclick="calcSqrt()">√x</button>
                        <button class="calc-btn special" onclick="calcInput('**2')">x²</button>
                        <button class="calc-btn special" onclick="calcInput('**3')">x³</button>
                        <button class="calc-btn op" onclick="calcClear()">C</button>

                        <button class="calc-btn" onclick="calcInput('7')">7</button>
                        <button class="calc-btn" onclick="calcInput('8')">8</button>
                        <button class="calc-btn" onclick="calcInput('9')">9</button>
                        <button class="calc-btn op" onclick="calcInput('/')">÷</button>
                        
                        <button class="calc-btn" onclick="calcInput('4')">4</button>
                        <button class="calc-btn" onclick="calcInput('5')">5</button>
                        <button class="calc-btn" onclick="calcInput('6')">6</button>
                        <button class="calc-btn op" onclick="calcInput('*')">×</button>
                        
                        <button class="calc-btn" onclick="calcInput('1')">1</button>
                        <button class="calc-btn" onclick="calcInput('2')">2</button>
                        <button class="calc-btn" onclick="calcInput('3')">3</button>
                        <button class="calc-btn op" onclick="calcInput('-')">-</button>
                        
                        <button class="calc-btn" onclick="calcInput('0')">0</button>
                        <button class="calc-btn" onclick="calcInput('.')">.</button>
                        <button class="calc-btn op" onclick="calcInput('+')">+</button>
                        <button class="calc-btn op" onclick="calcEval()">=</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Review Screen -->
    <div id="review-screen" class="screen">
        <div class="results-summary">
            <h2>Performance Summary</h2>
            <div class="score-circle">
                <span class="score-num" id="final-score">0 / 12</span>
                <span style="font-size: 0.8rem; opacity: 0.8;">Score</span>
            </div>
            <button class="btn btn-primary" onclick="restartQuiz()">Retake Learning Sheet</button>
        </div>

        <h3 style="margin-bottom: 1rem; color: var(--primary-header);">Step-by-Step Worksheet Review</h3>
        <div class="review-list" id="review-list"></div>
    </div>

    <script>
        const AudioFX = {
            ctx: null,
            init() {
                if (!this.ctx) {
                    this.ctx = new (window.AudioContext || window.webkitAudioContext)();
                }
                if (this.ctx.state === 'suspended') {
                    this.ctx.resume();
                }
            },
            playCorrectBell() {
                this.init();
                const now = this.ctx.currentTime;
                const playSingleBell = (freq, time, duration) => {
                    const osc = this.ctx.createOscillator();
                    const gain = this.ctx.createGain();

                    osc.type = 'sine';
                    osc.frequency.setValueAtTime(freq, time);

                    gain.gain.setValueAtTime(0, time);
                    gain.gain.linearRampToValueAtTime(0.3, time + 0.01);
                    gain.gain.exponentialRampToValueAtTime(0.001, time + duration);

                    osc.connect(gain);
                    gain.connect(this.ctx.destination);

                    osc.start(time);
                    osc.stop(time + duration);
                };

                playSingleBell(880, now, 0.8);        
                playSingleBell(1318.51, now + 0.12, 1.2); 
            },
            playIncorrectBell() {
                this.init();
                const now = this.ctx.currentTime;

                const osc = this.ctx.createOscillator();
                const gain = this.ctx.createGain();

                osc.type = 'triangle';
                osc.frequency.setValueAtTime(220, now); 

                gain.gain.setValueAtTime(0, now);
                gain.gain.linearRampToValueAtTime(0.35, now + 0.01);
                gain.gain.exponentialRampToValueAtTime(0.001, now + 0.6);

                osc.connect(gain);
                gain.connect(this.ctx.destination);

                osc.start(now);
                osc.stop(now + 0.6);
            },
            playSkipChime() {
                this.init();
                const now = this.ctx.currentTime;

                const osc = this.ctx.createOscillator();
                const gain = this.ctx.createGain();

                osc.type = 'sine';
                osc.frequency.setValueAtTime(523.25, now); 
                osc.frequency.exponentialRampToValueAtTime(392, now + 0.15); 

                gain.gain.setValueAtTime(0.15, now);
                gain.gain.exponentialRampToValueAtTime(0.001, now + 0.15);

                osc.connect(gain);
                gain.connect(this.ctx.destination);

                osc.start(now);
                osc.stop(now + 0.15);
            }
        };

        const CHAPTER_KEY = "AP_CALC_TANGENT_NORMAL_RANDOMIZED_FULLFORM";

        // ALL 4 Questions (12 parts total) with fully written terms & non-identical randomized correct answers across steps
        const questionsData = [
            // Card 1: 1a (Correct: B, D, A)
            {
                id: 1,
                desmosLatex: 'y=1/x',
                title: "Card 1 (Question 1a): Average Rate of Change of f(x) = 1/x over [-1, 4]",
                problem: "Consider the function f(x) = 1/x. Find the average rate of change of f(x) over the interval [-1, 4].",
                step1: {
                    prompt: "Select the formula for the Average Rate of Change on the closed interval [a, b]:",
                    options: [
                        "Average Rate of Change = lim (h -> 0) [f(a+h) - f(a)] / h",
                        "Average Rate of Change = [f(b) - f(a)] / (b - a)",
                        "Average Rate of Change = [f(b) + f(a)] / 2",
                        "Average Rate of Change = f'(b) - f'(a)"
                    ],
                    correct: 1 // Option B
                },
                step2: {
                    prompt: "Substitute the endpoint function values f(4) = 1/4 and f(-1) = -1 into the difference quotient:",
                    options: [
                        "(1/4 - 1) / (4 - (-1)) = -3/20",
                        "[4 - (-1)] / [1/4 - (-1)] = 5 / (5/4) = 4",
                        "(1/4 + 1) / 3 = (5/4) / 3",
                        "[f(4) - f(-1)] / [4 - (-1)] = [1/4 - (-1)] / [4 - (-1)] = (5/4) / 5"
                    ],
                    correct: 3 // Option D
                },
                step3: {
                    prompt: "Calculate the simplified average rate of change value: (5/4) / 5 = [ _____ ]:",
                    options: [
                        "Average Rate of Change = 1/4",
                        "Average Rate of Change = -1/4",
                        "Average Rate of Change = 5/4",
                        "Average Rate of Change = 1"
                    ],
                    correct: 0 // Option A
                },
                rationale: "<b>Step 1:</b> Average Rate of Change = [f(b) - f(a)] / (b - a).<br><b>Step 2:</b> f(4) = 1/4 and f(-1) = -1. Average Rate of Change = [1/4 - (-1)] / [4 - (-1)] = (5/4) / 5.<br><b>Step 3:</b> (5/4) / 5 = 1/4."
            },
            // Card 2: 1b (Correct: C, A, D)
            {
                id: 2,
                desmosLatex: 'y=1/x',
                title: "Card 2 (Question 1b): Tangent Slope of f(x) = 1/x at x = -3 (h -> 0 Definition)",
                problem: "Find the slope of the line tangent to f(x) = 1/x at x = -3 using the limit definition (h -> 0).",
                step1: {
                    prompt: "Select the limit definition of the slope of the tangent line at x = c as h approaches 0:",
                    options: [
                        "Slope of the tangent line = lim (x -> c) [f(x) - f(c)] / (x - c)",
                        "Slope of the tangent line = [f(c + h) - f(c)] / h",
                        "Slope of the tangent line = lim (h -> 0) [f(c + h) - f(c)] / h",
                        "Slope of the tangent line = lim (h -> 0) [f(c) - f(h)] / h"
                    ],
                    correct: 2 // Option C
                },
                step2: {
                    prompt: "Substitute c = -3: f(-3 + h) = 1/(-3 + h) and f(-3) = -1/3. Simplify the difference quotient:",
                    options: [
                        "lim (h -> 0) [1/(-3 + h) - (-1/3)] / h = lim (h -> 0) h / [3h(-3 + h)] = lim (h -> 0) 1 / [3(-3 + h)]",
                        "lim (h -> 0) [1/(-3 + h) - 1/3] / h = lim (h -> 0) (-6 - h) / [3h(-3 + h)]",
                        "lim (h -> 0) -h / [3h(-3 + h)] = lim (h -> 0) -1 / [3(-3 + h)]",
                        "lim (h -> 0) [3 - (-3 + h)] / h = (6 - h) / h"
                    ],
                    correct: 0 // Option A
                },
                step3: {
                    prompt: "Evaluate the limit by direct substitution of h = 0 into 1 / [3(-3 + h)]:",
                    options: [
                        "Slope of the tangent line = -1/3",
                        "Slope of the tangent line = 1/9",
                        "Slope of the tangent line = -1/6",
                        "Slope of the tangent line = -1/9"
                    ],
                    correct: 3 // Option D
                },
                rationale: "<b>Step 1:</b> Slope of the tangent line = lim (h -> 0) [f(-3+h) - f(-3)] / h.<br><b>Step 2:</b> [1/(-3+h) + 1/3] / h = [3 + (-3+h)] / [3h(-3+h)] = h / [3h(-3+h)] = 1 / [3(-3+h)].<br><b>Step 3:</b> As h -> 0, Slope = 1 / [3(-3)] = -1/9."
            },
            // Card 3: 1c (Correct: D, C, B)
            {
                id: 3,
                desmosLatex: 'y=1/x',
                title: "Card 3 (Question 1c): Tangent Slope of f(x) = 1/x at x = -3 (Alternative Definition)",
                problem: "Find the slope of the line tangent to f(x) = 1/x at x = -3 using the alternative definition.",
                step1: {
                    prompt: "Select the alternative definition of the slope of the tangent line at x = c:",
                    options: [
                        "Slope of the tangent line = lim (h -> 0) [f(x + h) - f(x)] / h",
                        "Slope of the tangent line = [f(x) - f(c)] / (x - c)",
                        "Slope of the tangent line = lim (x -> 0) [f(x) - f(c)] / x",
                        "Slope of the tangent line = lim (x -> c) [f(x) - f(c)] / (x - c)"
                    ],
                    correct: 3 // Option D
                },
                step2: {
                    prompt: "Substitute c = -3: f(x) = 1/x, f(-3) = -1/3. Simplify the expression [1/x - (-1/3)] / [x - (-3)]:",
                    options: [
                        "[ (3 - x) / (3x) ] / (x + 3) = (3 - x) / [3x(x + 3)]",
                        "[ (x - 3) / (3x) ] / (x + 3) = -1 / (3x)",
                        "[1/x - (-1/3)] / (x + 3) = [ (3 + x) / (3x) ] / (x + 3) = (x + 3) / [3x(x + 3)] = 1 / (3x)",
                        "(1/x + 1/3) / (x - 3)"
                    ],
                    correct: 2 // Option C
                },
                step3: {
                    prompt: "Evaluate the limit as x approaches -3: lim (x -> -3) 1 / (3x) = [ _____ ]:",
                    options: [
                        "Slope of the tangent line = 1/9",
                        "Slope of the tangent line = -1/9",
                        "Slope of the tangent line = -1/3",
                        "Slope of the tangent line = 1/3"
                    ],
                    correct: 1 // Option B
                },
                rationale: "<b>Step 1:</b> Slope of the tangent line = lim (x -> -3) [f(x) - f(-3)] / (x - (-3)).<br><b>Step 2:</b> [1/x + 1/3] / (x + 3) = [(3+x)/(3x)] / (x+3) = 1 / (3x).<br><b>Step 3:</b> Evaluate at x = -3: 1 / [3(-3)] = -1/9."
            },
            // Card 4: 2a (Correct: A, B, C)
            {
                id: 4,
                desmosLatex: 'y=x^3-2',
                title: "Card 4 (Question 2a): Average Rate of Change of f(x) = x^3 - 2 over [1, 3]",
                problem: "Consider the function f(x) = x^3 - 2. Find the average rate of change of f(x) over the interval [1, 3].",
                step1: {
                    prompt: "Select the setup for Average Rate of Change on the interval [1, 3]:",
                    options: [
                        "Average Rate of Change = [f(3) - f(1)] / (3 - 1)",
                        "Average Rate of Change = [f(1) - f(3)] / (3 - 1)",
                        "Average Rate of Change = lim (h -> 0) [f(1+h) - f(1)] / h",
                        "Average Rate of Change = [f(3) + f(1)] / 2"
                    ],
                    correct: 0 // Option A
                },
                step2: {
                    prompt: "Compute endpoint outputs f(3) = 3^3 - 2 = 25 and f(1) = 1^3 - 2 = -1, then substitute into the formula:",
                    options: [
                        "[25 - 1] / 2 = 24 / 2 = 12",
                        "[f(3) - f(1)] / (3 - 1) = [25 - (-1)] / 2 = 26 / 2",
                        "[27 - 1] / 2 = 26 / 2",
                        "[25 + 1] / 3 = 26 / 3"
                    ],
                    correct: 1 // Option B
                },
                step3: {
                    prompt: "Calculate the final simplified Average Rate of Change: 26 / 2 = [ _____ ]:",
                    options: [
                        "Average Rate of Change = 12",
                        "Average Rate of Change = 26",
                        "Average Rate of Change = 13",
                        "Average Rate of Change = 14"
                    ],
                    correct: 2 // Option C
                },
                rationale: "<b>Step 1:</b> Average Rate of Change = [f(3) - f(1)] / (3 - 1).<br><b>Step 2:</b> f(3) = 27 - 2 = 25, f(1) = 1 - 2 = -1. Quotient = [25 - (-1)] / 2 = 26 / 2.<br><b>Step 3:</b> 26 / 2 = 13."
            },
            // Card 5: 2b (Correct: C, A, D)
            {
                id: 5,
                desmosLatex: 'y=x^3-2',
                title: "Card 5 (Question 2b): Tangent Slope of f(x) = x^3 - 2 at x = 2 (h -> 0 Definition)",
                problem: "Find the slope of the line tangent to f(x) = x^3 - 2 at x = 2 using the limit definition (h -> 0).",
                step1: {
                    prompt: "Formulate the limit definition of the slope of the tangent line at x = 2:",
                    options: [
                        "Slope of the tangent line = lim (x -> 2) [f(x) - f(2)] / (x - 2)",
                        "Slope of the tangent line = lim (h -> 0) [f(2) - f(h)] / h",
                        "Slope of the tangent line = lim (h -> 0) [f(2 + h) - f(2)] / h",
                        "Slope of the tangent line = [f(2 + h) - f(2)] / h"
                    ],
                    correct: 2 // Option C
                },
                step2: {
                    prompt: "Expand f(2 + h) = (2 + h)^3 - 2 = 6 + 12h + 6h^2 + h^3 and f(2) = 6. Simplify the difference quotient:",
                    options: [
                        "[(6 + 12h + 6h^2 + h^3) - 6] / h = (12h + 6h^2 + h^3) / h = 12 + 6h + h^2",
                        "(6h + 12h^2 + h^3) / h = 6 + 12h + h^2",
                        "(12h + h^3) / h = 12 + h^2",
                        "(8 + 12h + 6h^2 + h^3) / h"
                    ],
                    correct: 0 // Option A
                },
                step3: {
                    prompt: "Evaluate the limit as h approaches 0: lim (h -> 0) (12 + 6h + h^2) = [ _____ ]:",
                    options: [
                        "Slope of the tangent line = 6",
                        "Slope of the tangent line = 8",
                        "Slope of the tangent line = 14",
                        "Slope of the tangent line = 12"
                    ],
                    correct: 3 // Option D
                },
                rationale: "<b>Step 1:</b> Slope of the tangent line = lim (h -> 0) [f(2+h) - f(2)] / h.<br><b>Step 2:</b> [6 + 12h + 6h^2 + h^3 - 6] / h = 12 + 6h + h^2.<br><b>Step 3:</b> Evaluate at h = 0: 12 + 0 + 0 = 12."
            },
            // Card 6: 2c (Correct: A, C, B)
            {
                id: 6,
                desmosLatex: 'y=x^3-2',
                title: "Card 6 (Question 2c): Tangent Slope of f(x) = x^3 - 2 at x = 2 (Alternative Definition)",
                problem: "Find the slope of the line tangent to f(x) = x^3 - 2 at x = 2 using the alternative definition.",
                step1: {
                    prompt: "Set up the alternative limit quotient at c = 2: lim (x -> 2) [f(x) - f(2)] / (x - 2):",
                    options: [
                        "lim (x -> 2) [(x^3 - 2) - 6] / (x - 2) = lim (x -> 2) (x^3 - 8) / (x - 2)",
                        "lim (x -> 2) (x^3 - 2) / (x - 2)",
                        "lim (x -> 2) (x^3 - 6) / (x - 2)",
                        "lim (x -> 2) (x^3 + 8) / (x + 2)"
                    ],
                    correct: 0 // Option A
                },
                step2: {
                    prompt: "Factor the difference of cubes x^3 - 8 = (x - 2)(x^2 + 2x + 4) and cancel the factor (x - 2):",
                    options: [
                        "(x - 2)(x^2 - 2x + 4) / (x - 2) = x^2 - 2x + 4",
                        "(x - 2)(x^2 + 4) / (x - 2) = x^2 + 4",
                        "(x - 2)(x^2 + 2x + 4) / (x - 2) = x^2 + 2x + 4",
                        "(x - 2)^3 / (x - 2) = (x - 2)^2"
                    ],
                    correct: 2 // Option C
                },
                step3: {
                    prompt: "Evaluate the limit as x approaches 2: 2^2 + 2(2) + 4 = 4 + 4 + 4 = [ _____ ]:",
                    options: [
                        "Slope of the tangent line = 8",
                        "Slope of the tangent line = 12",
                        "Slope of the tangent line = 16",
                        "Slope of the tangent line = 10"
                    ],
                    correct: 1 // Option B
                },
                rationale: "<b>Step 1:</b> lim (x -> 2) (x^3 - 8) / (x - 2).<br><b>Step 2:</b> Factoring gives (x - 2)(x^2 + 2x + 4) / (x - 2) = x^2 + 2x + 4.<br><b>Step 3:</b> Evaluate at x = 2: 4 + 4 + 4 = 12."
            },
            // Card 7: 3a (Correct: B, D, A)
            {
                id: 7,
                desmosLatex: 'y=\\sqrt{x}',
                title: "Card 7 (Question 3a): Tangent Slope of f(x) = √x at x = 9",
                problem: "Consider the function f(x) = √x. Find the slope of the line tangent to f(x) at x = 9 (Use either definition).",
                step1: {
                    prompt: "Set up the alternative limit formulation: lim (x -> 9) [f(x) - f(9)] / (x - 9):",
                    options: [
                        "lim (x -> 9) (√x - 9) / (x - 9)",
                        "lim (x -> 9) (√x - 3) / (x - 9)",
                        "lim (x -> 9) (x - 9) / (√x - 3)",
                        "lim (x -> 9) (√x + 3) / (x - 9)"
                    ],
                    correct: 1 // Option B
                },
                step2: {
                    prompt: "Factor the denominator x - 9 as (√x - 3)(√x + 3) and simplify the quotient:",
                    options: [
                        "(√x - 3) / [ (√x - 3)(√x - 3) ] = 1 / (√x - 3)",
                        "(√x + 3) / (x - 9)",
                        "1 / (√x - 3)",
                        "(√x - 3) / [ (√x - 3)(√x + 3) ] = 1 / (√x + 3)"
                    ],
                    correct: 3 // Option D
                },
                step3: {
                    prompt: "Evaluate the limit as x approaches 9: 1 / (√9 + 3) = 1 / (3 + 3) = [ _____ ]:",
                    options: [
                        "Slope of the tangent line = 1/6",
                        "Slope of the tangent line = 1/3",
                        "Slope of the tangent line = 1/9",
                        "Slope of the tangent line = 6"
                    ],
                    correct: 0 // Option A
                },
                rationale: "<b>Step 1:</b> Slope of the tangent line = lim (x -> 9) (√x - 3) / (x - 9).<br><b>Step 2:</b> Factoring or rationalizing yields 1 / (√x + 3).<br><b>Step 3:</b> At x = 9, 1 / (3 + 3) = 1/6."
            },
            // Card 8: 3b (Correct: C, A, B)
            {
                id: 8,
                desmosLatex: 'y=\\sqrt{x}',
                title: "Card 8 (Question 3b): Tangent Line Equation to f(x) = √x at x = 9",
                problem: "Find the equation of the line tangent to f(x) = √x at x = 9.",
                step1: {
                    prompt: "Determine the Point of tangency and the Slope of the tangent line:",
                    options: [
                        "Point of tangency = (9, 9), Slope of the tangent line = 1/6",
                        "Point of tangency = (3, 9), Slope of the tangent line = 1/6",
                        "Point of tangency = (9, 3), Slope of the tangent line = 1/6",
                        "Point of tangency = (9, 3), Slope of the tangent line = -6"
                    ],
                    correct: 2 // Option C
                },
                step2: {
                    prompt: "Substitute into point-slope equation form y - y_1 = m(x - x_1):",
                    options: [
                        "y - 3 = (1/6)(x - 9)",
                        "y - 9 = (1/6)(x - 3)",
                        "y - 3 = -6(x - 9)",
                        "y + 3 = (1/6)(x + 9)"
                    ],
                    correct: 0 // Option A
                },
                step3: {
                    prompt: "Express in slope-intercept form: y = (1/6)x - 9/6 + 3 = (1/6)x - 3/2 + 6/2 = [ _____ ]:",
                    options: [
                        "Equation of the tangent line: y = (1/6)x - 3/2",
                        "Equation of the tangent line: y = (1/6)x + 3/2",
                        "Equation of the tangent line: y = (1/6)x + 3",
                        "Equation of the tangent line: y = 6x - 51"
                    ],
                    correct: 1 // Option B
                },
                rationale: "<b>Step 1:</b> Point of tangency is (9, √9) = (9, 3), Slope of the tangent line = 1/6.<br><b>Step 2:</b> Point-slope form: y - 3 = (1/6)(x - 9).<br><b>Step 3:</b> y = (1/6)x - 3/2 + 3 = (1/6)x + 3/2."
            },
            // Card 9: 3c (Correct: D, B, A)
            {
                id: 9,
                desmosLatex: 'y=\\sqrt{x}',
                title: "Card 9 (Question 3c): Normal Line Equation to f(x) = √x at x = 9",
                problem: "Find the equation of the line normal to f(x) = √x at x = 9.",
                step1: {
                    prompt: "Calculate the Slope of the normal line as the negative reciprocal of the tangent slope (1/6):",
                    options: [
                        "Slope of the normal line = 1/6",
                        "Slope of the normal line = 6",
                        "Slope of the normal line = -1/6",
                        "Slope of the normal line = -1 / (Slope of the tangent line) = -1 / (1/6) = -6"
                    ],
                    correct: 3 // Option D
                },
                step2: {
                    prompt: "Substitute the point of tangency (9, 3) and normal slope -6 into point-slope form:",
                    options: [
                        "y - 9 = -6(x - 3)",
                        "y - 3 = -6(x - 9)",
                        "y - 3 = 6(x - 9)",
                        "y + 3 = -6(x + 9)"
                    ],
                    correct: 1 // Option B
                },
                step3: {
                    prompt: "Convert to slope-intercept form: y = -6x + 54 + 3 = [ _____ ]:",
                    options: [
                        "Equation of the normal line: y = -6x + 57",
                        "Equation of the normal line: y = -6x + 51",
                        "Equation of the normal line: y = -6x - 57",
                        "Equation of the normal line: y = 6x - 51"
                    ],
                    correct: 0 // Option A
                },
                rationale: "<b>Step 1:</b> Slope of the normal line is the negative reciprocal: -6.<br><b>Step 2:</b> Point-slope form: y - 3 = -6(x - 9).<br><b>Step 3:</b> y = -6x + 54 + 3 = -6x + 57."
            },
            // Card 10: 4a (Correct: B, C, D)
            {
                id: 10,
                desmosLatex: 'y=3x^2+x',
                title: "Card 10 (Question 4a): Tangent Slope of f(x) = 3x^2 + x at x = -1",
                problem: "Consider the function f(x) = 3x^2 + x. Find the slope of the line tangent to f(x) at x = -1 (Use either definition).",
                step1: {
                    prompt: "Evaluate f(-1) and set up the derivative limit as h approaches 0:",
                    options: [
                        "f(-1) = 4; Slope of the tangent line = lim (h -> 0) [f(-1+h) - 4] / h",
                        "f(-1) = 3(-1)^2 + (-1) = 2; Slope of the tangent line = lim (h -> 0) [f(-1+h) - 2] / h",
                        "f(-1) = -2; Slope of the tangent line = lim (h -> 0) [f(-1+h) + 2] / h",
                        "f(-1) = 0; Slope of the tangent line = lim (h -> 0) f(-1+h) / h"
                    ],
                    correct: 1 // Option B
                },
                step2: {
                    prompt: "Expand f(-1+h) = 3(-1+h)^2 + (-1+h) = 2 - 5h + 3h^2, and simplify the difference quotient:",
                    options: [
                        "[(2 - 5h + 3h^2) - 2] / h = (5h + 3h^2) / h = 5 + 3h",
                        "(-6h + 3h^2) / h = -6 + 3h",
                        "[(2 - 5h + 3h^2) - 2] / h = (-5h + 3h^2) / h = -5 + 3h",
                        "(-5h) / h = -5"
                    ],
                    correct: 2 // Option C
                },
                step3: {
                    prompt: "Evaluate the limit as h approaches 0: lim (h -> 0) (-5 + 3h) = [ _____ ]:",
                    options: [
                        "Slope of the tangent line = 5",
                        "Slope of the tangent line = -6",
                        "Slope of the tangent line = 2",
                        "Slope of the tangent line = -5"
                    ],
                    correct: 3 // Option D
                },
                rationale: "<b>Step 1:</b> f(-1) = 3(1) - 1 = 2.<br><b>Step 2:</b> f(-1+h) - f(-1) = (2 - 5h + 3h^2) - 2 = -5h + 3h^2. Dividing by h gives -5 + 3h.<br><b>Step 3:</b> Evaluate at h = 0: Slope of the tangent line = -5."
            },
            // Card 11: 4b (Correct: C, B, A)
            {
                id: 11,
                desmosLatex: 'y=3x^2+x',
                title: "Card 11 (Question 4b): Tangent Line Equation to f(x) = 3x^2 + x at x = -1",
                problem: "Find the equation of the line tangent to f(x) = 3x^2 + x at x = -1.",
                step1: {
                    prompt: "State the Point of tangency and the Slope of the tangent line:",
                    options: [
                        "Point of tangency = (-1, -2), Slope of the tangent line = -5",
                        "Point of tangency = (-1, 2), Slope of the tangent line = 1/5",
                        "Point of tangency = (-1, 2), Slope of the tangent line = -5",
                        "Point of tangency = (1, 4), Slope of the tangent line = -5"
                    ],
                    correct: 2 // Option C
                },
                step2: {
                    prompt: "Substitute into point-slope formula y - y_1 = m(x - x_1):",
                    options: [
                        "y + 2 = -5(x - 1)",
                        "y - 2 = -5(x - (-1))  =>  y - 2 = -5(x + 1)",
                        "y - 2 = 5(x + 1)",
                        "y - 2 = (1/5)(x + 1)"
                    ],
                    correct: 1 // Option B
                },
                step3: {
                    prompt: "Express in slope-intercept form: y = -5x - 5 + 2 = [ _____ ]:",
                    options: [
                        "Equation of the tangent line: y = -5x - 3",
                        "Equation of the tangent line: y = -5x + 3",
                        "Equation of the tangent line: y = -5x - 7",
                        "Equation of the tangent line: y = 5x + 7"
                    ],
                    correct: 0 // Option A
                },
                rationale: "<b>Step 1:</b> Point of tangency is (-1, 2), Slope of the tangent line = -5.<br><b>Step 2:</b> y - 2 = -5(x + 1).<br><b>Step 3:</b> y = -5x - 5 + 2 = -5x - 3."
            },
            // Card 12: 4c (Correct: B, D, C)
            {
                id: 12,
                desmosLatex: 'y=3x^2+x',
                title: "Card 12 (Question 4c): Normal Line Equation to f(x) = 3x^2 + x at x = -1",
                problem: "Find the equation of the line normal to f(x) = 3x^2 + x at x = -1.",
                step1: {
                    prompt: "Determine the Slope of the normal line given the tangent slope (-5):",
                    options: [
                        "Slope of the normal line = -5",
                        "Slope of the normal line = -1 / (Slope of the tangent line) = -1 / (-5) = 1/5",
                        "Slope of the normal line = 5",
                        "Slope of the normal line = -1/5"
                    ],
                    correct: 1 // Option B
                },
                step2: {
                    prompt: "Substitute point (-1, 2) and normal slope 1/5 into point-slope equation:",
                    options: [
                        "y - 2 = -(1/5)(x + 1)",
                        "y + 2 = (1/5)(x - 1)",
                        "y - 2 = 5(x + 1)",
                        "y - 2 = (1/5)(x - (-1))  =>  y - 2 = (1/5)(x + 1)"
                    ],
                    correct: 3 // Option D
                },
                step3: {
                    prompt: "Convert to slope-intercept form: y = (1/5)x + 1/5 + 2 = (1/5)x + 1/5 + 10/5 = [ _____ ]:",
                    options: [
                        "Equation of the normal line: y = (1/5)x + 9/5",
                        "Equation of the normal line: y = (1/5)x - 11/5",
                        "Equation of the normal line: y = (1/5)x + 11/5",
                        "Equation of the normal line: y = 5x + 7"
                    ],
                    correct: 2 // Option C
                },
                rationale: "<b>Step 1:</b> Slope of the normal line is the negative reciprocal: 1/5.<br><b>Step 2:</b> y - 2 = (1/5)(x + 1).<br><b>Step 3:</b> y = (1/5)x + 1/5 + 2 = (1/5)x + 11/5."
            }
        ];

        let currentUser = null;
        let currentQIndex = 0;
        let userState = { answers: {}, status: {}, cardSteps: {} };
        let desmosCalc = null;

        function initDesmos() {
            const elt = document.getElementById('desmos-calculator');
            if (elt && !desmosCalc && window.Desmos) {
                desmosCalc = Desmos.GraphingCalculator(elt, {
                    expressions: true,
                    keypad: false,
                    settingsMenu: false
                });
            }
            if (desmosCalc) {
                desmosCalc.setBlank();
                desmosCalc.setExpression({ id: 'fn', latex: questionsData[currentQIndex].desmosLatex });
            }
        }

        // Calculator Logic
        function calcInput(val) {
            const d = document.getElementById('calc-disp');
            if (d.value === '0' || d.value === 'Error') d.value = val;
            else d.value += val;
        }

        function calcClear() {
            document.getElementById('calc-disp').value = '0';
        }

        function calcEval() {
            const d = document.getElementById('calc-disp');
            try {
                d.value = eval(d.value);
            } catch(e) {
                d.value = 'Error';
            }
        }

        function calcSqrt() {
            const d = document.getElementById('calc-disp');
            try {
                const val = parseFloat(d.value) || 0;
                d.value = Number(Math.sqrt(val).toFixed(4));
            } catch(e) {
                d.value = 'Error';
            }
        }

        function handleLogin(e) {
            e.preventDefault();
            const email = document.getElementById('email-input').value.trim();
            if (email) {
                currentUser = email;
                localStorage.setItem('bm_calc_fullform_email', email);
                initSession();
            }
        }

        function initSession() {
            document.getElementById('display-user-email').innerText = currentUser;
            document.getElementById('user-header-info').style.display = 'flex';

            const savedData = localStorage.getItem(`${currentUser}_${CHAPTER_KEY}`);
            if (savedData) {
                userState = JSON.parse(savedData);
            } else {
                userState = { answers: {}, status: {}, cardSteps: {} };
            }

            switchScreen('quiz-screen');
            renderGrid();
            loadQuestion(0);
            setTimeout(initDesmos, 300);
        }

        function logout() {
            localStorage.removeItem('bm_calc_fullform_email');
            currentUser = null;
            document.getElementById('user-header-info').style.display = 'none';
            switchScreen('auth-screen');
        }

        function saveState() {
            if (currentUser) {
                localStorage.setItem(`${currentUser}_${CHAPTER_KEY}`, JSON.stringify(userState));
            }
        }

        function switchScreen(id) {
            document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
        }

        function renderGrid() {
            const grid = document.getElementById('question-grid');
            grid.innerHTML = '';
            questionsData.forEach((q, idx) => {
                const btn = document.createElement('button');
                btn.className = 'grid-btn';
                btn.innerText = idx + 1;

                if (idx === currentQIndex) btn.classList.add('active');
                if (userState.status[idx] === 'submitted') btn.classList.add('attempted');
                if (userState.status[idx] === 'skipped') btn.classList.add('skipped');

                btn.onclick = () => jumpToQuestion(idx);
                grid.appendChild(btn);
            });
        }

        function loadQuestion(index) {
            currentQIndex = index;
            const q = questionsData[index];

            document.getElementById('q-number-badge').innerText = `Card ${index + 1} of ${questionsData.length}`;
            document.getElementById('q-title-text').innerHTML = q.title;
            document.getElementById('q-problem-text').innerHTML = q.problem;

            if (!userState.cardSteps[index]) {
                userState.cardSteps[index] = {
                    s1Selection: null, s1Status: 'unattempted',
                    s2Selection: null, s2Status: 'unattempted',
                    s3Selection: null, s3Status: 'unattempted'
                };
            }

            const cState = userState.cardSteps[index];

            renderStepUI(1, q.step1, cState.s1Selection, cState.s1Status, true);
            const isStep1Passed = cState.s1Status === 'correct' || cState.s1Status === 'skipped';
            renderStepUI(2, q.step2, cState.s2Selection, cState.s2Status, isStep1Passed);
            const isStep2Passed = cState.s2Status === 'correct' || cState.s2Status === 'skipped';
            renderStepUI(3, q.step3, cState.s3Selection, cState.s3Status, isStep2Passed);

            const isCardFinished = userState.status[index] === 'submitted' || userState.status[index] === 'skipped';
            const ratBox = document.getElementById('rationale-container');

            if (isCardFinished) {
                ratBox.style.display = 'block';
                document.getElementById('rationale-text').innerHTML = q.rationale;
                document.getElementById('skip-card-btn').style.display = 'none';
                document.getElementById('next-btn').style.display = 'inline-flex';
            } else {
                ratBox.style.display = 'none';
                document.getElementById('skip-card-btn').style.display = 'inline-flex';
                document.getElementById('next-btn').style.display = 'none';
            }

            if (desmosCalc) {
                desmosCalc.setBlank();
                desmosCalc.setExpression({ id: 'fn', latex: q.desmosLatex });
            }

            renderGrid();
        }

        function renderStepUI(stepNum, stepData, currentSelection, currentStatus, isUnlocked) {
            const block = document.getElementById(`step${stepNum}-block`);
            const container = document.getElementById(`step${stepNum}-options-container`);
            const tag = document.getElementById(`step${stepNum}-status-tag`);
            const actions = document.getElementById(`step${stepNum}-actions`);
            container.innerHTML = '';

            if (!isUnlocked) {
                block.className = 'step-block locked';
                tag.innerText = 'Locked';
                tag.style.color = 'var(--text-muted)';
                actions.style.display = 'none';
                return;
            }

            if (currentStatus === 'correct') {
                block.className = 'step-block completed-step';
                tag.innerText = '✓ Correct';
                tag.style.color = 'var(--correct-green)';
                actions.style.display = 'none';
            } else if (currentStatus === 'skipped') {
                block.className = 'step-block skipped-step';
                tag.innerText = 'Skipped';
                tag.style.color = 'var(--skipped-orange)';
                actions.style.display = 'none';
            } else {
                block.className = 'step-block active-step';
                tag.innerText = 'In Progress';
                tag.style.color = 'var(--accent-gold)';
                actions.style.display = 'flex';
            }

            stepData.options.forEach((optText, idx) => {
                const item = document.createElement('div');
                item.className = 'step-option-item';

                if (currentSelection === idx) item.classList.add('selected');

                if (currentStatus === 'correct' || currentStatus === 'skipped') {
                    item.classList.add('disabled');
                    if (idx === stepData.correct) item.classList.add('correct');
                    else if (currentSelection === idx) item.classList.add('incorrect');
                } else if (currentStatus === 'incorrect' && currentSelection === idx) {
                    item.classList.add('incorrect');
                    item.onclick = () => selectStepOption(stepNum, idx);
                } else {
                    item.onclick = () => selectStepOption(stepNum, idx);
                }

                item.innerHTML = `<div class="step-opt-prefix">${String.fromCharCode(65 + idx)}</div><div>${optText}</div>`;
                container.appendChild(item);
            });
        }

        function selectStepOption(stepNum, idx) {
            const cState = userState.cardSteps[currentQIndex];
            if (stepNum === 1) {
                if (cState.s1Status === 'correct' || cState.s1Status === 'skipped') return;
                cState.s1Selection = idx;
                cState.s1Status = 'unattempted';
            } else if (stepNum === 2) {
                if (cState.s2Status === 'correct' || cState.s2Status === 'skipped') return;
                cState.s2Selection = idx;
                cState.s2Status = 'unattempted';
            } else if (stepNum === 3) {
                if (cState.s3Status === 'correct' || cState.s3Status === 'skipped') return;
                cState.s3Selection = idx;
                cState.s3Status = 'unattempted';
            }
            saveState();
            loadQuestion(currentQIndex);
        }

        function checkStep(stepNum) {
            const q = questionsData[currentQIndex];
            const cState = userState.cardSteps[currentQIndex];

            if (stepNum === 1) {
                if (cState.s1Selection === null) {
                    alert("Please select an option for Step 1 first!");
                    return;
                }
                if (cState.s1Selection === q.step1.correct) {
                    cState.s1Status = 'correct';
                    AudioFX.playCorrectBell();
                } else {
                    cState.s1Status = 'incorrect';
                    AudioFX.playIncorrectBell();
                }
            } else if (stepNum === 2) {
                if (cState.s2Selection === null) {
                    alert("Please select an option for Step 2 first!");
                    return;
                }
                if (cState.s2Selection === q.step2.correct) {
                    cState.s2Status = 'correct';
                    AudioFX.playCorrectBell();
                } else {
                    cState.s2Status = 'incorrect';
                    AudioFX.playIncorrectBell();
                }
            } else if (stepNum === 3) {
                if (cState.s3Selection === null) {
                    alert("Please select an option for Step 3 first!");
                    return;
                }
                if (cState.s3Selection === q.step3.correct) {
                    cState.s3Status = 'correct';
                    userState.status[currentQIndex] = 'submitted';
                    userState.answers[currentQIndex] = cState.s3Selection;
                    AudioFX.playCorrectBell();
                } else {
                    cState.s3Status = 'incorrect';
                    AudioFX.playIncorrectBell();
                }
            }
            saveState();
            loadQuestion(currentQIndex);
        }

        function skipStep(stepNum) {
            const cState = userState.cardSteps[currentQIndex];
            if (stepNum === 1) {
                cState.s1Status = 'skipped';
                AudioFX.playSkipChime();
            } else if (stepNum === 2) {
                cState.s2Status = 'skipped';
                AudioFX.playSkipChime();
            } else if (stepNum === 3) {
                cState.s3Status = 'skipped';
                userState.status[currentQIndex] = 'submitted';
                AudioFX.playSkipChime();
            }
            saveState();
            loadQuestion(currentQIndex);
        }

        function skipEntireCard() {
            const cState = userState.cardSteps[currentQIndex];
            cState.s1Status = 'skipped';
            cState.s2Status = 'skipped';
            cState.s3Status = 'skipped';
            userState.status[currentQIndex] = 'skipped';
            saveState();
            AudioFX.playSkipChime();
            nextQuestion();
        }

        function nextQuestion() {
            if (currentQIndex < questionsData.length - 1) {
                loadQuestion(currentQIndex + 1);
            } else {
                finishTest();
            }
        }

        function jumpToQuestion(idx) {
            loadQuestion(idx);
        }

        function finishTest() {
            switchScreen('review-screen');
            let score = 0;
            const reviewList = document.getElementById('review-list');
            reviewList.innerHTML = '';

            questionsData.forEach((q, idx) => {
                const status = userState.status[idx];
                const cState = userState.cardSteps[idx] || {};
                const isFullyCorrect = cState.s1Status === 'correct' && cState.s2Status === 'correct' && cState.s3Status === 'correct';

                if (isFullyCorrect) score++;

                const card = document.createElement('div');
                card.className = 'review-card';

                let tagHtml = '<span class="status-tag tag-skipped">Skipped</span>';
                if (status === 'submitted') {
                    tagHtml = isFullyCorrect 
                        ? '<span class="status-tag tag-correct">Fully Correct</span>' 
                        : '<span class="status-tag tag-incorrect">Completed with Help</span>';
                }

                const s3Answer = cState.s3Selection !== null ? q.step3.options[cState.s3Selection] : 'None';
                const s3Correct = q.step3.options[q.step3.correct];

                card.innerHTML = `
                    <div style="display:flex; justify-content:space-between; margin-bottom:0.5rem;">
                        <strong>${q.title}</strong>
                        ${tagHtml}
                    </div>
                    <p style="font-size:0.9rem; margin-bottom:0.5rem;">${q.problem}</p>
                    <p style="font-size:0.9rem; color:var(--text-muted);">
                        <strong>Your Step 3 Answer:</strong> ${s3Answer} | 
                        <strong>Correct Answer:</strong> ${s3Correct}
                    </p>
                    <div style="margin-top:0.5rem; font-size:0.85rem; background:#f8fafc; padding:0.5rem; border-radius:4px;">
                        <strong>Solution Rationale:</strong> ${q.rationale}
                    </div>
                `;
                reviewList.appendChild(card);
            });

            document.getElementById('final-score').innerText = `${score} / ${questionsData.length}`;
        }

        function restartQuiz() {
            userState = { answers: {}, status: {}, cardSteps: {} };
            saveState();
            startQuizScreen();
        }

        window.onload = function() {
            const savedUser = localStorage.getItem('bm_calc_fullform_email');
            if (savedUser) {
                currentUser = savedUser;
                initSession();
            }
        };
    </script>
</body>
</html>
