# ow

<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>節約能源大作戰 - 網頁版</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;500;700;900&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Noto Sans TC', sans-serif;
            background-color: #0d1a2e;
            background-image: linear-gradient(160deg, #0d1a2e 0%, #0f2c57 100%);
        }
        .btn {
            @apply py-3 px-6 rounded-lg text-lg font-bold shadow-lg transition-transform duration-200 ease-in-out transform hover:-translate-y-1;
        }
        .btn-primary {
            @apply bg-green-500 text-white hover:bg-green-600 active:scale-95;
        }
        .btn-secondary {
            @apply bg-gray-600 text-white hover:bg-gray-700 active:scale-95;
        }
        .option-btn {
            @apply w-full text-left p-4 my-2 border-2 border-gray-600 rounded-lg bg-gray-700/50 text-white hover:border-yellow-400 hover:bg-gray-700 transition-all duration-200;
        }
        .option-btn.selected {
             @apply border-yellow-500 bg-yellow-900/50 ring-2 ring-yellow-500;
        }
        .option-btn.correct {
            @apply border-green-500 bg-green-900/50 ring-2 ring-green-500 text-green-200;
        }
        .option-btn.incorrect {
            @apply border-red-500 bg-red-900/50 ring-2 ring-red-500 text-red-200;
        }
        .hidden {
            display: none;
        }
        .coin-icon {
            display: inline-block;
            width: 28px;
            height: 28px;
            background-color: #facc15;
            border-radius: 50%;
            color: #ca8a04;
            text-align: center;
            font-weight: bold;
            line-height: 28px;
            margin-right: 10px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.2);
            font-size: 16px;
        }
        .badge-icon {
            width: 90px;
            height: 90px;
        }
        .glass-panel {
            @apply bg-gray-800/50 backdrop-blur-md border border-gray-700/50 rounded-2xl shadow-2xl;
        }
    </style>
</head>
<body class="text-white flex items-center justify-center min-h-screen p-4">

    <div id="app" class="w-full max-w-5xl mx-auto flex flex-col relative">

        <!-- Header -->
        <header id="game-header" class="hidden p-4 mb-6 glass-panel">
            <div class="flex justify-between items-center">
                <div class="flex items-center">
                    <span class="coin-icon">E</span>
                    <span id="energy-coins" class="text-3xl font-bold">100</span>
                </div>
                <div class="flex items-center space-x-4">
                     <span class="text-lg">關卡 <span id="question-number-header">1</span> / 4</span>
                    <button id="achievements-btn" class="text-yellow-400 hover:text-yellow-300 transition-colors">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10" viewBox="0 0 20 20" fill="currentColor">
                            <path fill-rule="evenodd" d="M10 2a.75.75 0 01.75.75v.518a3.746 3.746 0 012.83 1.352l.382.381.52.026a.75.75 0 01.738.902l-.285 1.708a3.746 3.746 0 010 2.83l.285 1.708a.75.75 0 01-.738.902l-.52.026-.382.381a3.746 3.746 0 01-2.83 1.352v.518a.75.75 0 01-1.5 0v-.518a3.746 3.746 0 01-2.83-1.352l-.382-.381-.52-.026a.75.75 0 01-.738-.902l.285-1.708a3.746 3.746 0 010-2.83l-.285-1.708a.75.75 0 01.738-.902l.52.026.382-.381a3.746 3.746 0 012.83-1.352V2.75A.75.75 0 0110 2zM8.5 10a1.5 1.5 0 113 0 1.5 1.5 0 01-3 0z" clip-rule="evenodd" />
                        </svg>
                    </button>
                </div>
            </div>
        </header>

        <!-- Start Screen -->
        <div id="start-screen" class="flex flex-col justify-center items-center text-center p-8 glass-panel">
            <h1 class="text-7xl font-black text-transparent bg-clip-text bg-gradient-to-r from-green-300 via-cyan-300 to-green-300 mb-4">節約能源大作戰</h1>
            <p class="text-gray-300 text-xl mb-10 max-w-2xl">投入100元啟動資金，開始你的節能挑戰，贏取能源幣，為地球和社會盡一份力！</p>
            <div class="w-full max-w-xs">
                <button id="start-game-btn" class="btn btn-primary w-full text-2xl py-4">支付100元，開始遊戲</button>
            </div>
            <p class="text-xs text-gray-500 mt-4">這是一個模擬過程</p>
        </div>
        
        <!-- Intro Animation Screen -->
        <div id="intro-screen" class="hidden flex-col justify-center items-center text-center p-8 h-96 glass-panel">
             <h2 class="text-4xl font-bold text-blue-300 mb-6">能源現狀小動畫</h2>
             <div class="w-28 h-28 bg-blue-900/50 rounded-full flex items-center justify-center mb-6 ring-4 ring-blue-500/50">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-16 w-16 text-blue-300" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M14.752 11.168l-3.197-2.132A1 1 0 0010 9.87v4.263a1 1 0 001.555.832l3.197-2.132a1 1 0 000-1.664z" />
                  <path stroke-linecap="round" stroke-linejoin="round" d="M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
             </div>
             <p class="text-gray-300 text-lg">地球的能源正在快速消耗...<br>一個小小的動作，就能帶來巨大的改變。</p>
        </div>

        <!-- Quiz Screen -->
        <main id="quiz-screen" class="hidden flex-grow p-8 glass-panel">
             <div id="timer" class="w-full bg-gray-900 rounded-full h-3.5 mb-6 border border-gray-700">
                <div id="timer-bar" class="bg-yellow-400 h-full rounded-full" style="width: 100%"></div>
            </div>
            <div class="grid md:grid-cols-2 gap-8 items-center">
                <div class="md:pr-8">
                    <p class="text-lg font-bold text-green-400 mb-2">挑戰題目</p>
                    <h2 id="question-text" class="text-4xl font-bold leading-tight">問題文字</h2>
                </div>
                <div>
                    <div id="options-container" class="flex flex-col space-y-3">
                        <!-- Options will be generated here -->
                    </div>
                    <button id="submit-answer-btn" class="btn btn-primary w-full mt-6 opacity-50" disabled>確定答案</button>
                </div>
            </div>
        </main>
        
        <!-- Donation Screen -->
        <div id="donation-screen" class="hidden flex-grow p-8 flex flex-col items-center glass-panel">
            <div class="text-center mb-8">
                <h2 class="text-5xl font-bold text-yellow-300">挑戰結束！</h2>
                <p class="text-gray-300 text-xl mt-2">恭喜你完成所有關卡！</p>
                <p class="text-lg mt-6">你最後的能源幣：</p>
                <div class="flex items-center justify-center mt-2">
                    <span class="coin-icon text-3xl w-12 h-12 leading-10">E</span>
                    <span id="final-coins" class="text-7xl font-bold">0</span>
                </div>
                 <p class="text-gray-400 mt-2 text-lg">可兌換成 <span id="cash-amount" class="font-bold text-green-400">0</span> 元現金</p>
            </div>

            <div class="w-full max-w-3xl">
                <h3 class="font-bold text-center text-2xl mb-6">選擇一個單位，將愛心捐出去</h3>
                <div id="donation-options" class="grid md:grid-cols-2 gap-4">
                    <!-- Donation options will be generated here -->
                </div>
            </div>
             <div class="mt-8">
                 <button id="restart-game-btn" class="btn btn-secondary text-xl">重新挑戰</button>
            </div>
        </div>

        <!-- Achievements & Modal Overlays -->
        <div id="overlay-container" class="absolute inset-0 bg-black/70 flex items-center justify-center z-20 hidden">
            <!-- Achievements Screen -->
            <div id="achievements-screen" class="hidden glass-panel p-8 max-w-lg w-full mx-4 relative">
                <button id="close-achievements-btn" class="absolute top-4 right-4 text-gray-400 hover:text-gray-300">
                     <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                    </svg>
                </button>
                <h2 class="text-3xl font-bold text-center mb-8 text-yellow-300">我的成就</h2>
                <div id="badges-container" class="grid grid-cols-2 sm:grid-cols-4 gap-6 text-center">
                    <!-- Badges will be generated here -->
                </div>
            </div>
        
            <!-- Result/Tip Modal -->
            <div id="modal" class="hidden glass-panel p-8 max-w-md w-full mx-4 text-center">
                <div id="modal-result-icon" class="w-20 h-20 mx-auto mb-4 rounded-full flex items-center justify-center">
                    <!-- Icon here -->
                </div>
                <h2 id="modal-title" class="text-3xl font-bold mb-2"></h2>
                <p id="modal-text" class="text-xl text-gray-300 mb-6"></p>
                <div id="modal-tip-section" class="bg-yellow-900/50 border-l-4 border-yellow-400 text-yellow-200 p-4 rounded-lg mb-8 text-left">
                    <p class="font-bold">節能小知識</p>
                    <p id="modal-tip-text"></p>
                </div>
                <button id="modal-next-btn" class="btn btn-primary w-full">下一關</button>
            </div>
        </div>
    </div>

    <script>
    document.addEventListener('DOMContentLoaded', () => {
        // --- DOM Elements ---
        const screens = {
            start: document.getElementById('start-screen'),
            intro: document.getElementById('intro-screen'),
            quiz: document.getElementById('quiz-screen'),
            donation: document.getElementById('donation-screen'),
        };
        const overlayContainer = document.getElementById('overlay-container');
        const achievementsScreen = document.getElementById('achievements-screen');
        const modalEl = document.getElementById('modal');
        const gameHeader = document.getElementById('game-header');
        const energyCoinsEl = document.getElementById('energy-coins');
        const finalCoinsEl = document.getElementById('final-coins');
        const cashAmountEl = document.getElementById('cash-amount');
        const questionNumberHeaderEl = document.getElementById('question-number-header');
        const questionTextEl = document.getElementById('question-text');
        const optionsContainer = document.getElementById('options-container');
        const submitAnswerBtn = document.getElementById('submit-answer-btn');
        const donationOptionsContainer = document.getElementById('donation-options');
        const badgesContainer = document.getElementById('badges-container');

        const modal = {
            icon: document.getElementById('modal-result-icon'),
            title: document.getElementById('modal-title'),
            text: document.getElementById('modal-text'),
            tipSection: document.getElementById('modal-tip-section'),
            tipText: document.getElementById('modal-tip-text'),
            nextBtn: document.getElementById('modal-next-btn'),
        };
        
        const timerBar = document.getElementById('timer-bar');

        // --- Game Data ---
        const questions = [
            { question: "為了舒適又省電，夏天冷氣最建議設定在幾度？", options: ["20-22度", "23-25度", "26-28度", "30度以上"], answer: 2, reward: 15, penalty: 5, tip: "冷氣溫度每調高1度，就能省下約6%的電力消耗。" },
            { question: "以下哪種電器在待機時最耗電，建議優先拔掉插頭？", options: ["手機充電器", "數位機上盒", "電風扇", "檯燈"], answer: 1, reward: 10, penalty: 5, tip: "數位機上盒、音響等有遙控功能的家電，待機時耗電量相當可觀。" },
            { question: "在AR場景中，你走到插座前。你應該做什麼來節能？", options: ["用一個延長線插滿所有電器", "將不用的電器插頭拔掉", "把插座擦乾淨", "確認電壓是否穩定"], answer: 1, reward: 20, penalty: 10, tip: "養成隨手拔插頭的習慣，是節能最直接有效的方法之一。" },
            { question: "更換家中燈具時，哪種選擇最節能環保？", options: ["傳統白熾燈泡", "省電燈泡(CFL)", "LED燈泡", "鹵素燈"], answer: 2, reward: 15, penalty: 5, tip: "LED燈泡的發光效率是傳統燈泡的數倍，且壽命更長、更省電。" }
        ];
        const charities = [
            { name: "兒童福利院", icon: "👧" }, { name: "長者照護中心", icon: "👵" },
            { name: "偏鄉教育基金", icon: "📚" }, { name: "流浪動物之家", icon: "🐶" }
        ];
        const achievements = [
            { id: 'rookie', name: '節能新秀', condition: (gs) => gs.correctAnswers >= 1, unlocked: false, icon: '🌱' },
            { id: 'expert', name: '節能達人', condition: (gs) => gs.correctAnswers >= 3, unlocked: false, icon: '💡' },
            { id: 'master', name: '環保大師', condition: (gs) => gs.correctAnswers >= questions.length, unlocked: false, icon: '🌍' },
            { id: 'donor', name: '慈善家', condition: (gs) => gs.donated, unlocked: false, icon: '💖' },
        ];

        // --- Game State ---
        let gameState;
        let timerInterval;
        let selectedOption = null;

        function init() {
            gameState = { energyCoins: 100, currentQuestionIndex: 0, correctAnswers: 0, donated: false };
            achievements.forEach(a => a.unlocked = false);
            updateCoinsDisplay();
            showScreen('start');
        }

        function showScreen(screenName) {
            Object.values(screens).forEach(screen => screen.classList.add('hidden'));
            if(screens[screenName]) screens[screenName].classList.remove('hidden');
            gameHeader.classList.toggle('hidden', screenName === 'start' || screenName === 'intro');
        }

        function startGame() {
            showScreen('intro');
            setTimeout(() => {
                showScreen('quiz');
                loadQuestion();
            }, 2500);
        }
        
        function updateCoinsDisplay() {
            energyCoinsEl.textContent = gameState.energyCoins;
        }

        function loadQuestion() {
            if (gameState.currentQuestionIndex >= questions.length) {
                endGame();
                return;
            }
            
            selectedOption = null;
            resetOptionsStyle();
            submitAnswerBtn.disabled = true;
            submitAnswerBtn.classList.add('opacity-50');

            const q = questions[gameState.currentQuestionIndex];
            questionNumberHeaderEl.textContent = `${gameState.currentQuestionIndex + 1}`;
            questionTextEl.textContent = q.question;
            optionsContainer.innerHTML = '';
            
            q.options.forEach((option, index) => {
                const button = document.createElement('button');
                button.className = 'option-btn text-lg';
                button.textContent = option;
                button.dataset.index = index;
                button.addEventListener('click', () => selectOption(button, index));
                optionsContainer.appendChild(button);
            });
            
            startTimer();
        }
        
        function selectOption(button, index) {
            selectedOption = index;
            resetOptionsStyle();
            button.classList.add('selected');
            submitAnswerBtn.disabled = false;
            submitAnswerBtn.classList.remove('opacity-50');
        }

        function resetOptionsStyle() {
            document.querySelectorAll('.option-btn').forEach(btn => {
                btn.classList.remove('selected', 'correct', 'incorrect');
            });
        }
        
        function startTimer() {
            clearInterval(timerInterval);
            timerBar.style.transition = 'none';
            timerBar.style.width = '100%';
            // Force reflow to restart animation
            void timerBar.offsetWidth; 
            timerBar.style.transition = 'width 15s linear';
            timerBar.style.width = '0%';

            timerInterval = setTimeout(handleTimeout, 15000);
        }
        
        function handleTimeout() {
            clearInterval(timerInterval);
            timerBar.style.transition = 'none';
            checkAnswer(null);
        }

        function checkAnswer(selectedIndex) {
            clearInterval(timerInterval);
            timerBar.style.transition = 'none';

            const q = questions[gameState.currentQuestionIndex];
            const isCorrect = selectedIndex === q.answer;

            const options = optionsContainer.querySelectorAll('.option-btn');
            options.forEach(btn => btn.disabled = true);
            
            if (selectedIndex !== null) {
                options[selectedIndex].classList.add(isCorrect ? 'correct' : 'incorrect');
            }
            if (!isCorrect) {
                options[q.answer].classList.add('correct');
            }

            if (isCorrect) {
                gameState.energyCoins += q.reward;
                gameState.correctAnswers++;
                showModal(true, `+${q.reward} 能源幣`, q.tip);
            } else {
                gameState.energyCoins -= q.penalty;
                showModal(false, `-${q.penalty} 能源幣`, q.tip);
            }

            updateCoinsDisplay();
            checkAchievements();
        }

        function showModal(isCorrect, text, tip) {
            overlayContainer.classList.remove('hidden');
            achievementsScreen.classList.add('hidden');
            modalEl.classList.remove('hidden');
            
            modal.title.textContent = isCorrect ? '答對了！' : '答錯了！';
            modal.text.textContent = text;
            modal.tipText.textContent = tip;
            
            modal.icon.innerHTML = isCorrect ? 
                `<svg xmlns="http://www.w3.org/2000/svg" class="h-12 w-12 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" /></svg>` :
                `<svg xmlns="http://www.w3.org/2000/svg" class="h-12 w-12 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" /></svg>`;
            modal.icon.className = `w-20 h-20 mx-auto mb-4 rounded-full flex items-center justify-center ${isCorrect ? 'bg-green-500' : 'bg-red-500'}`;
        }
        
        function nextQuestion() {
            overlayContainer.classList.add('hidden');
            modalEl.classList.add('hidden');
            gameState.currentQuestionIndex++;
            loadQuestion();
        }

        function endGame() {
            showScreen('donation');
            finalCoinsEl.textContent = gameState.energyCoins;
            const cash = Math.floor(gameState.energyCoins / 10);
            cashAmountEl.textContent = cash;
            
            donationOptionsContainer.innerHTML = '';
            charities.forEach(charity => {
                const button = document.createElement('button');
                button.className = 'flex items-center p-4 my-2 border-2 border-gray-600 rounded-lg bg-gray-700/50 text-white hover:border-sky-400 hover:bg-gray-700 transition-all duration-200';
                button.innerHTML = `
                    <span class="text-4xl mr-4">${charity.icon}</span>
                    <span class="font-bold text-lg">${charity.name}</span>
                    <span class="ml-auto text-sky-300 font-bold text-lg">捐出 ${cash} 元</span>
                `;
                button.addEventListener('click', () => donate(charity.name, cash));
                donationOptionsContainer.appendChild(button);
            });
        }
        
        function donate(charityName, amount) {
            gameState.donated = true;
            checkAchievements();
            
            overlayContainer.classList.remove('hidden');
            achievementsScreen.classList.add('hidden');
            modalEl.classList.remove('hidden');

            modal.title.textContent = "感謝您的愛心！";
            modal.text.innerHTML = `您已成功將 <span class="font-bold text-green-400">${amount}</span> 元捐贈給<br><span class="font-bold text-sky-400">${charityName}</span>`;
            modal.icon.innerHTML = `<svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10 text-white" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M3.172 5.172a4 4 0 015.656 0L10 6.343l1.172-1.171a4 4 0 115.656 5.656L10 17.657l-6.828-6.829a4 4 0 010-5.656z" clip-rule="evenodd" /></svg>`;
            modal.icon.className = 'w-20 h-20 mx-auto mb-4 rounded-full flex items-center justify-center bg-pink-500';
            modal.tipSection.classList.add('hidden');
            modal.nextBtn.textContent = "關閉";
            modal.nextBtn.onclick = () => {
                overlayContainer.classList.add('hidden');
                modalEl.classList.add('hidden');
                modal.tipSection.classList.remove('hidden');
                modal.nextBtn.textContent = "下一關";
                modal.nextBtn.onclick = nextQuestion;
            };
            
            donationOptionsContainer.querySelectorAll('button').forEach(btn => {
                btn.disabled = true;
                btn.classList.add('opacity-50', 'cursor-not-allowed');
            });
        }
        
        function checkAchievements() {
            achievements.forEach(ach => {
                if (!ach.unlocked && ach.condition(gameState)) {
                    ach.unlocked = true;
                }
            });
        }

        function showAchievements() {
            badgesContainer.innerHTML = '';
            achievements.forEach(ach => {
                const badgeEl = document.createElement('div');
                badgeEl.className = 'flex flex-col items-center';
                const isUnlocked = ach.unlocked;
                
                badgeEl.innerHTML = `
                    <div class="badge-icon rounded-full flex items-center justify-center transition-all duration-300 ${isUnlocked ? 'bg-yellow-400' : 'bg-gray-700'}">
                        <span class="text-5xl transition-transform duration-300 ${isUnlocked ? 'scale-100' : 'scale-90'}">${ach.icon}</span>
                    </div>
                    <p class="font-bold mt-3 ${isUnlocked ? 'text-yellow-200' : 'text-gray-400'}">${ach.name}</p>
                `;
                if (!isUnlocked) {
                   badgeEl.classList.add('opacity-60');
                }
                badgesContainer.appendChild(badgeEl);
            });
            overlayContainer.classList.remove('hidden');
            modalEl.classList.add('hidden');
            achievementsScreen.classList.remove('hidden');
        }
        
        function closeOverlay() {
            overlayContainer.classList.add('hidden');
            achievementsScreen.classList.add('hidden');
            modalEl.classList.add('hidden');
        }

        // --- Event Listeners ---
        document.getElementById('start-game-btn').addEventListener('click', startGame);
        submitAnswerBtn.addEventListener('click', () => { if (selectedOption !== null) { checkAnswer(selectedOption); }});
        modal.nextBtn.addEventListener('click', nextQuestion);
        document.getElementById('restart-game-btn').addEventListener('click', init);
        document.getElementById('achievements-btn').addEventListener('click', showAchievements);
        document.getElementById('close-achievements-btn').addEventListener('click', closeOverlay);

        // --- Initial Load ---
        init();
    });
    </script>

</body>
</html>
