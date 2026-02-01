# Cleaner-Tracker
The cleaning app that gets you. ADHD-friendly task tracker with satisfying checkboxes, a laundry timer (because we all forget), and a ‘I’m struggling’ mode for those days. No judgment, just progress. Your house won’t clean itself, but at least now you’ll remember what needs doing.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>Cleaning Tracker</title>
    <link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;700&family=Fraunces:wght@600;700;900&display=swap" rel="stylesheet">
    <style>
        :root {
            --daily: #60A5FA;
            --kitchen: #FCD34D;
            --bathrooms: #67E8F9;
            --master: #EC4899;
            --boys: #F9A8D4;
            --living: #60A5FA;
            --basement: #A78BFA;
            --bg: #0F172A;
            --surface: #1E293B;
            --text: #F1F5F9;
            --text-dim: #94A3B8;
            --success: #10B981;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'DM Sans', sans-serif;
            background: linear-gradient(135deg, #0F172A 0%, #1E293B 100%);
            color: var(--text);
            min-height: 100vh;
            padding: 20px;
            padding-bottom: 100px;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
        }
        
        h1 {
            font-family: 'Fraunces', serif;
            font-size: 2.5rem;
            font-weight: 900;
            background: linear-gradient(135deg, #60A5FA 0%, #A78BFA 50%, #EC4899 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 10px;
        }
        
        .tagline {
            color: var(--text-dim);
            font-size: 1rem;
            margin-bottom: 30px;
        }
        
        .streak-hero {
            background: var(--surface);
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 30px;
            text-align: center;
        }
        
        .streak-number {
            font-size: 4rem;
            font-weight: 900;
            color: #FCD34D;
        }
        
        .streak-info h2 {
            font-size: 1.5rem;
            margin: 10px 0;
        }
        
        .mode-toggle {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }
        
        .mode-btn {
            flex: 1;
            padding: 15px;
            background: var(--surface);
            border: 2px solid transparent;
            border-radius: 12px;
            color: var(--text);
            font-weight: 600;
            cursor: pointer;
        }
        
        .mode-btn.active {
            background: var(--daily);
            color: var(--bg);
        }
        
        .task-grid {
            display: grid;
            gap: 20px;
        }
        
        .task-card {
            background: var(--surface);
            border-radius: 15px;
            padding: 20px;
            border-top: 4px solid;
        }
        
        .task-card.kitchen { border-top-color: var(--kitchen); }
        .task-card.bathrooms { border-top-color: var(--bathrooms); }
        .task-card.master { border-top-color: var(--master); }
        .task-card.boys { border-top-color: var(--boys); }
        .task-card.living { border-top-color: var(--living); }
        .task-card.basement { border-top-color: var(--basement); }
        
        .task-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }
        
        .task-title {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .task-icon {
            font-size: 1.5rem;
        }
        
        .task-title h3 {
            font-size: 1.25rem;
        }
        
        .task-badge {
            padding: 5px 12px;
            border-radius: 15px;
            font-size: 0.75rem;
            background: var(--daily);
            color: var(--bg);
        }
        
        .task-list {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        
        .task-item {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 10px;
            background: rgba(255,255,255,0.05);
            border-radius: 10px;
            cursor: pointer;
        }
        
        .task-item:active {
            background: rgba(255,255,255,0.1);
        }
        
        .checkbox {
            width: 24px;
            height: 24px;
            border: 2px solid var(--text-dim);
            border-radius: 6px;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-shrink: 0;
        }
        
        .task-item.completed .checkbox {
            background: var(--success);
            border-color: var(--success);
        }
        
        .task-item.completed .checkbox::after {
            content: '✓';
            color: white;
            font-weight: bold;
        }
        
        .task-item.completed .task-text {
            text-decoration: line-through;
            opacity: 0.6;
        }
        
        .task-text {
            flex: 1;
            font-size: 0.95rem;
        }
        
        .progress-section {
            margin-top: 15px;
            padding-top: 15px;
            border-top: 1px solid rgba(255,255,255,0.1);
        }
        
        .progress-label {
            display: flex;
            justify-content: space-between;
            margin-bottom: 8px;
            font-size: 0.85rem;
            color: var(--text-dim);
        }
        
        .progress-bar {
            height: 10px;
            background: rgba(255,255,255,0.1);
            border-radius: 10px;
            overflow: hidden;
        }
        
        .progress-fill {
            height: 100%;
            background: var(--success);
            border-radius: 10px;
            transition: width 0.3s ease;
        }
        
        .laundry-timer {
            background: var(--basement);
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 20px;
        }
        
        .timer-display {
            font-size: 2.5rem;
            font-weight: 900;
            text-align: center;
            margin: 15px 0;
        }
        
        .timer-buttons {
            display: flex;
            gap: 10px;
        }
        
        .timer-btn {
            flex: 1;
            padding: 12px;
            background: rgba(255,255,255,0.2);
            border: none;
            border-radius: 10px;
            color: white;
            font-weight: 600;
            cursor: pointer;
        }
        
        .timer-btn:active {
            background: rgba(255,255,255,0.3);
        }
        
        .reset-btn {
            margin-top: 10px;
            padding: 8px 16px;
            background: #EF4444;
            border: none;
            border-radius: 8px;
            color: white;
            cursor: pointer;
        }
        
        @media (max-width: 768px) {
            h1 { font-size: 2rem; }
            .mode-toggle { flex-direction: column; }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>✨ Clean House, Clear Mind</h1>
            <p class="tagline">Your ADHD-friendly cleaning companion</p>
        </header>
        
        <div class="streak-hero">
            <div class="streak-number" id="streakNumber">0</div>
            <div class="streak-info">
                <h2>Day Streak! 🎉</h2>
                <p>Keep that momentum going!</p>
                <button class="reset-btn" onclick="resetStreak()">Reset Streak</button>
            </div>
        </div>
        
        <div class="mode-toggle">
            <button class="mode-btn active" onclick="setMode('regular')">✨ Regular Mode</button>
            <button class="mode-btn" onclick="setMode('struggling')">💙 Bare Minimum</button>
        </div>
        
        <div class="laundry-timer">
            <h3>🧺 Laundry Timer</h3>
            <div class="timer-display" id="timerDisplay">--:--</div>
            <div class="timer-buttons">
                <button class="timer-btn" onclick="startTimer(45)">Washer 45m</button>
                <button class="timer-btn" onclick="startTimer(60)">Dryer 60m</button>
                <button class="timer-btn" onclick="stopTimer()">Stop</button>
            </div>
        </div>
        
        <div class="task-grid" id="taskGrid"></div>
    </div>
    
    <script>
        var TASKS = {
            regular: {
                kitchen: {
                    name: 'Kitchen',
                    icon: '🍳',
                    color: 'kitchen',
                    tasks: [
                        'Wipe down counters and stove',
                        'Load/run dishwasher',
                        'Take out trash if full',
                        'Wipe down table'
                    ]
                },
                living: {
                    name: 'Living Areas',
                    icon: '🛋️',
                    color: 'living',
                    tasks: [
                        '5-minute pickup',
                        'Fluff couch pillows',
                        'Clear coffee table',
                        'Change main floor litter box bag'
                    ]
                },
                master: {
                    name: 'Master Suite',
                    icon: '👑',
                    color: 'master',
                    tasks: [
                        'Make bed',
                        'Dirty clothes in hamper',
                        'Clear nightstands',
                        'Tidy dressing room'
                    ]
                },
                boys: {
                    name: "Boys' Rooms",
                    icon: '🚀',
                    color: 'boys',
                    tasks: [
                        "Make Freddie's bed",
                        "Make Henry's bed",
                        'Clothes in hampers',
                        'Quick pickup'
                    ]
                },
                bathrooms: {
                    name: 'Bathrooms',
                    icon: '🛁',
                    color: 'bathrooms',
                    tasks: [
                        'Wipe down counters',
                        'Quick toilet swish',
                        'Hang up towels'
                    ]
                },
                laundry: {
                    name: 'Laundry',
                    icon: '🧺',
                    color: 'basement',
                    tasks: [
                        'One load in washer',
                        'Move washer to dryer',
                        'Fold one load',
                        'Change basement litter box bag'
                    ]
                }
            },
            struggling: {
                essential: {
                    name: 'Bare Minimum',
                    icon: '💙',
                    color: 'living',
                    tasks: [
                        'Dishes in dishwasher',
                        'Laundry in hamper',
                        'Bed somewhat made',
                        'Change litter box bags',
                        'STOP. Rest.'
                    ]
                }
            }
        };
        
        var currentMode = 'regular';
        var timerInterval = null;
        var timerEndTime = null;
        
        function loadData() {
            try {
                var saved = localStorage.getItem('cleaningTasks');
                var streak = localStorage.getItem('cleaningStreak');
                if (streak) {
                    document.getElementById('streakNumber').textContent = streak;
                }
                return saved ? JSON.parse(saved) : {};
            } catch(e) {
                return {};
            }
        }
        
        function saveData(data) {
            try {
                localStorage.setItem('cleaningTasks', JSON.stringify(data));
            } catch(e) {}
        }
        
        function saveStreak(streak) {
            try {
                localStorage.setItem('cleaningStreak', streak);
                document.getElementById('streakNumber').textContent = streak;
            } catch(e) {}
        }
        
        function resetStreak() {
            if (confirm('Reset your streak?')) {
                saveStreak(0);
            }
        }
        
        function isTaskCompleted(category, taskIndex) {
            var data = loadData();
            var today = new Date().toDateString();
            return data[today] && data[today][category] && data[today][category][taskIndex];
        }
        
        function toggleTask(category, taskIndex) {
            var data = loadData();
            var today = new Date().toDateString();
            
            if (!data[today]) data[today] = {};
            if (!data[today][category]) data[today][category] = {};
            
            data[today][category][taskIndex] = !data[today][category][taskIndex];
            saveData(data);
            
            renderTasks();
        }
        
        function setMode(mode) {
            currentMode = mode;
            var buttons = document.querySelectorAll('.mode-btn');
            buttons.forEach(function(btn) {
                btn.classList.remove('active');
            });
            if (mode === 'regular') {
                buttons[0].classList.add('active');
            } else {
                buttons[1].classList.add('active');
            }
            renderTasks();
        }
        
        function renderTasks() {
            var grid = document.getElementById('taskGrid');
            grid.innerHTML = '';
            
            var taskSet = TASKS[currentMode];
            
            Object.keys(taskSet).forEach(function(category) {
                var cardData = taskSet[category];
                var card = createTaskCard(category, cardData);
                grid.appendChild(card);
            });
        }
        
        function createTaskCard(category, data) {
            var card = document.createElement('div');
            card.className = 'task-card ' + data.color;
            
            var tasksHtml = '';
            data.tasks.forEach(function(task, index) {
                var completed = isTaskCompleted(category, index) ? 'completed​​​​​​​​​​​​​​​​
