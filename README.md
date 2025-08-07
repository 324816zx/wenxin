<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>雯芯生日快乐</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdn.jsdelivr.net/npm/font-awesome@4.7.0/css/font-awesome.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.8/dist/chart.umd.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Ma+Shan+Zheng&family=Noto+Serif+SC:wght@400;700&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/maplibre-gl@3.3.1/dist/maplibre-gl.js"></script>
    <link href="https://cdn.jsdelivr.net/npm/maplibre-gl@3.3.1/dist/maplibre-gl.css" rel="stylesheet" />
    <style>
        :root {
            --primary: #ff6b8b;
            --secondary: #74b9ff;
            --accent: #feca57;
            --dark: #2d3436;
            --light: #f5f6fa;
        }

        body {
            font-family: 'Noto Serif SC', serif;
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            overflow-x: hidden;
        }

        .title-font {
            font-family: 'Ma Shan Zheng', cursive;
        }

        .password-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, #1a2a6c 0%, #b21f1f 50%, #fdbb2d 100%);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            transition: opacity 1s ease-out;
        }

        .password-input {
            background: rgba(255, 255, 255, 0.2);
            border: none;
            border-radius: 10px;
            padding: 1rem;
            margin: 1rem;
            width: 200px;
            text-align: center;
            font-size: 1.5rem;
            color: white;
            backdrop-filter: blur(5px);
            box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
        }

        .password-input:focus {
            outline: none;
            box-shadow: 0 0 15px rgba(255, 255, 255, 0.5);
        }

        .hidden {
            display: none;
        }

        .opacity-0 {
            opacity: 0;
            pointer-events: none;
        }

        .slide-up {
            animation: slideUp 1s ease forwards;
        }

        @keyframes slideUp {
            from {
                transform: translateY(100px);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }

        .fade-in {
            animation: fadeIn 1.5s ease forwards;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }

        .pulse {
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% {
                transform: scale(1);
            }
            50% {
                transform: scale(1.05);
            }
            100% {
                transform: scale(1);
            }
        }

        .float {
            animation: float 3s ease-in-out infinite;
        }

        @keyframes float {
            0% {
                transform: translateY(0px);
            }
            50% {
                transform: translateY(-20px);
            }
            100% {
                transform: translateY(0px);
            }
        }

        .counter {
            font-family: monospace;
            background: linear-gradient(90deg, #ff9966, #ff5e62);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }

        .section {
            opacity: 0;
            transform: translateY(50px);
            transition: opacity 1s ease, transform 1s ease;
        }

        .section.visible {
            opacity: 1;
            transform: translateY(0);
        }

        .image-container {
            overflow: hidden;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .image-container img {
            transition: transform 0.5s ease;
        }

        .image-container:hover img {
            transform: scale(1.05);
        }

        .heart {
            position: absolute;
            width: 20px;
            height: 20px;
            background-color: var(--primary);
            transform: rotate(45deg);
            animation: float-heart 3s ease-in-out infinite;
            opacity: 0;
        }

        .heart:before, .heart:after {
            content: '';
            position: absolute;
            width: 20px;
            height: 20px;
            background-color: var(--primary);
            border-radius: 50%;
        }

        .heart:before {
            top: -10px;
            left: 0;
        }

        .heart:after {
            top: 0;
            left: -10px;
        }

        @keyframes float-heart {
            0% {
                transform: rotate(45deg) translateY(0) scale(1);
                opacity: 0;
            }
            50% {
                opacity: 1;
            }
            100% {
                transform: rotate(45deg) translateY(-100px) scale(1.5);
                opacity: 0;
            }
        }

        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 10px;
        }

        ::-webkit-scrollbar-track {
            background: #f1f1f1;
        }

        ::-webkit-scrollbar-thumb {
            background: var(--primary);
            border-radius: 5px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: #ff4767;
        }
    </style>
</head>
<body class="bg-light text-dark">
    <!-- Password Screen -->
    <div id="password-screen" class="password-screen">
        <h1 class="text-4xl md:text-5xl text-white font-bold mb-6 title-font fade-in">输入密码解锁祝福</h1>
        <div class="text-white text-xl mb-8 fade-in">她的生日...</div>
        <input type="password" id="password" class="password-input fade-in" maxlength="4" placeholder="****">
        <div id="error-message" class="text-white text-lg mt-4 hidden fade-in">密码错误，请重试</div>
    </div>

    <!-- Main Content -->
    <div id="main-content" class="hidden">
        <!-- Hero Section -->
        <section class="relative min-h-screen flex flex-col justify-center items-center text-center px-4 py-20 overflow-hidden">
            <div class="absolute inset-0 z-0">
                <div id="hearts-container"></div>
            </div>
            <h1 class="text-5xl md:text-7xl font-bold mb-6 title-font z-10 text-primary animate-[pulse_3s_ease-in-out_infinite]">雯芯生日快乐</h1>
            <p class="text-xl md:text-2xl mb-10 z-10 max-w-2xl mx-auto">16岁的天空，愿你自由翱翔，所有梦想都能实现</p>
            <div class="image-container w-48 h-48 md:w-64 md:h-64 rounded-full overflow-hidden border-4 border-accent shadow-lg mb-10 float z-10">
                <img src="wenxin1.jpg" alt="雯芯" class="w-full h-full object-cover">
            </div>
            <div class="flex flex-col items-center z-10">
                <p class="text-lg mb-2">点击下方开始探索</p>
                <a href="#counter" class="text-4xl text-primary animate-bounce">
                    <i class="fa fa-angle-down"></i>
                </a>
            </div>
        </section>

        <!-- Counter Section -->
        <section id="counter" class="py-20 px-4 bg-white section">
            <div class="max-w-4xl mx-auto text-center">
                <h2 class="text-4xl font-bold mb-10 title-font">我们相识的日子</h2>
                <div class="bg-gradient-to-r from-secondary to-primary p-1 rounded-xl mb-8 shadow-lg">
                    <div class="bg-white p-6 rounded-lg">
                        <div id="days-counter" class="text-3xl md:text-5xl font-bold counter mb-4"></div>
                        <div class="text-sm md:text-base opacity-70">从 2025年4月25日 23:24 开始</div>
                    </div>
                </div>
                <div class="grid grid-cols-2 md:grid-cols-4 gap-4 mt-10">
                    <div class="bg-light p-4 rounded-lg shadow-md transform transition-transform hover:scale-105">
                        <div id="days" class="text-3xl font-bold text-primary mb-2"></div>
                        <div class="text-sm opacity-70">天</div>
                    </div>
                    <div class="bg-light p-4 rounded-lg shadow-md transform transition-transform hover:scale-105">
                        <div id="hours" class="text-3xl font-bold text-primary mb-2"></div>
                        <div class="text-sm opacity-70">时</div>
                    </div>
                    <div class="bg-light p-4 rounded-lg shadow-md transform transition-transform hover:scale-105">
                        <div id="minutes" class="text-3xl font-bold text-primary mb-2"></div>
                        <div class="text-sm opacity-70">分</div>
                    </div>
                    <div class="bg-light p-4 rounded-lg shadow-md transform transition-transform hover:scale-105">
                        <div id="seconds" class="text-3xl font-bold text-primary mb-2"></div>
                        <div class="text-sm opacity-70">秒</div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Map Section -->
        <section id="map" class="py-20 px-4 bg-gray-50 section">
            <div class="max-w-4xl mx-auto text-center">
                <h2 class="text-4xl font-bold mb-10 title-font">我们的城市</h2>
                <p class="text-lg mb-8">山东曲阜 ❤️ 河南光山</p>
                <div id="map-container" class="w-full h-80 md:h-96 rounded-xl shadow-lg overflow-hidden"></div>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mt-8">
                    <div class="bg-white p-6 rounded-lg shadow-md">
                        <h3 class="text-xl font-bold mb-2 text-secondary">她的城市 - 山东曲阜</h3>
                        <p class="opacity-70">孔子故里，文化名城</p>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-md">
                        <h3 class="text-xl font-bold mb-2 text-primary">我的城市 - 河南光山</h3>
                        <p class="opacity-70">人杰地灵，美丽家乡</p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Personal Info Section -->
        <section id="personal-info" class="py-20 px-4 bg-white section">
            <div class="max-w-5xl mx-auto">
                <h2 class="text-4xl font-bold mb-16 text-center title-font">我们的故事</h2>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-10 mb-16">
                    <div class="text-center">
                        <div class="image-container w-48 h-48 mx-auto mb-6 rounded-full overflow-hidden border-4 border-primary shadow-lg">
                            <img src="wenxin1.jpg" alt="雯芯" class="w-full h-full object-cover">
                        </div>
                        <h3 class="text-2xl font-bold mb-2">张雯芯</h3>
                        <p class="text-gray-500 mb-4">2009年8月29日 (七夕节)</p>
                        <div class="bg-light p-4 rounded-lg shadow-sm">
                            <p class="italic text-gray-600">"讨厌对谁都温柔的人"</p>
                        </div>
                    </div>
                    <div class="text-center">
                        <div class="image-container w-48 h-48 mx-auto mb-6 rounded-full overflow-hidden border-4 border-secondary shadow-lg">
                            <img src="wenxin2.jpg" alt="张翔" class="w-full h-full object-cover">
                        </div>
                        <h3 class="text-2xl font-bold mb-2">张翔</h3>
                        <p class="text-gray-500 mb-4">2007年1月23日</p>
                        <div class="bg-light p-4 rounded-lg shadow-sm">
                            <p class="italic text-gray-600">"你个不懂事的东西"</p>
                        </div>
                    </div>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8">
                    <div class="bg-light p-6 rounded-xl shadow-md transition-transform hover:scale-105">
                        <h3 class="text-xl font-bold mb-4 flex items-center"><i class="fa fa-heart text-primary mr-2"></i> 她喜欢的</h3>
                        <div class="space-y-4">
                            <div class="flex items-center">
                                <div class="image-container w-16 h-16 mr-4 rounded-lg overflow-hidden">
                                    <img src="wenxin3.jpg" alt="古河渚" class="w-full h-full object-cover">
                                </div>
                                <div>
                                    <h4 class="font-bold">古河渚</h4>
                                    <p class="text-sm text-gray-500">《CLANNAD》女主角</p>
                                </div>
                            </div>
                            <div class="flex items-center">
                                <div class="image-container w-16 h-16 mr-4 rounded-lg overflow-hidden">
                                    <img src="wenxin4.jpg" alt="冈崎朋也" class="w-full h-full object-cover">
                                </div>
                                <div>
                                    <h4 class="font-bold">冈崎朋也</h4>
                                    <p class="text-sm text-gray-500">《CLANNAD》男主角</p>
                                </div>
                            </div>
                            <div class="flex items-center">
                                <div class="image-container w-16 h-16 mr-4 rounded-lg overflow-hidden">
                                    <img src="wenxin5.jpg" alt="毛泽东" class="w-full h-full object-cover">
                                </div>
                                <div>
                                    <h4 class="font-bold">毛泽东</h4>
                                    <p class="text-sm text-gray-500">伟大领袖</p>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="bg-light p-6 rounded-xl shadow-md transition-transform hover:scale-105">
                        <h3 class="text-xl font-bold mb-4 flex items-center"><i class="fa fa-star text-secondary mr-2"></i> 我喜欢的</h3>
                        <div class="space-y-4">
                            <div class="flex items-center">
                                <div class="image-container w-16 h-16 mr-4 rounded-lg overflow-hidden">
                                    <img src="wenxin6.jpg" alt="铠甲勇士" class="w-full h-full object-cover">
                                </div>
                                <div>
                                    <h4 class="font-bold">铠甲勇士</h4>
                                    <p class="text-sm text-gray-500">经典特摄剧</p>
                                </div>
                            </div>
                            <div class="flex items-center">
                                <div class="image-container w-16 h-16 mr-4 rounded-lg overflow-hidden">
                                    <img src="wenxin7.jpg" alt="李小龙" class="w-full h-full object-cover">
                                </div>
                                <div>
                                    <h4 class="font-bold">李小龙</h4>
                                    <p class="text-sm text-gray-500">功夫巨星</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Astrology Section -->
        <section id="astrology" class="py-20 px-4 bg-gray-50 section">
            <div class="max-w-5xl mx-auto text-center">
                <h2 class="text-4xl font-bold mb-10 title-font">我们的缘分</h2>
                <div class="mb-12">
                    <img src="wenxin镜映缘.jpg" alt="镜映缘分析" class="mx-auto rounded-lg shadow-lg max-w-full h-auto">
                    <p class="mt-4 text-lg italic text-gray-600">紫薇斗数：镜映缘 - 你们像镜子般照见彼此最深层的特质</p>
                </div>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mb-12">
                    <div class="bg-white p-6 rounded-xl shadow-md">
                        <h3 class="text-2xl font-bold mb-6 title-font text-primary">雯芯的五行</h3>
                        <div class="h-64 mb-6">
                            <canvas id="wenxin-chart"></canvas>
                        </div>
                        <div class="space-y-2 text-left">
                            <p><strong>日主：</strong>火 (丙火属阳火)</p>
                            <p><strong>喜用神：</strong>火、木</p>
                        </div>
                    </div>
                    <div class="bg-white p-6 rounded-xl shadow-md">
                        <h3 class="text-2xl font-bold mb-6 title-font text-secondary">张翔的五行</h3>
                        <div class="h-64 mb-6">
                            <canvas id="zhangxiang-chart"></canvas>
                        </div>
                        <div class="space-y-2 text-left">
                            <p><strong>日主：</strong>火 (丁火属阴火)</p>
                            <p><strong>喜用神：</strong>金、水、土</p>
                        </div>
                    </div>
                </div>
                <div class="bg-white p-6 rounded-xl shadow-md max-w-2xl mx-auto">
                    <h3 class="text-xl font-bold mb-4">八字命理</h3>
                    <p class="mb-4">我们两人八字均为偏财格，均为火日主</p>
                    <p>丁火属阴火，丙火属阳火，阴阳互补，缘分深厚</p>
                </div>
            </div>
        </section>

        <!-- Birthday Wish Section -->
        <section id="birthday-wish" class="py-20 px-4 bg-gradient-to-b from-white to-light section">
            <div class="max-w-3xl mx-auto text-center">
                <h2 class="text-4xl font-bold mb-10 title-font">生日祝福</h2>
                <div class="flex justify-center mb-10">
                    <div class="w-40 h-40 md:w-48 md:h-48 float">
                        <img src="wenxin6.jpg" alt="生日蛋糕" class="w-full h-full object-contain">
                    </div>
                </div>
                <div class="bg-white p-8 rounded-xl shadow-lg mb-10 text-left relative overflow-hidden">
                    <div class="absolute -top-10 -right-10 w-32 h-32 bg-primary opacity-10 rounded-full"></div>
                    <div class="absolute -bottom-10 -left-10 w-40 h-40 bg-secondary opacity-10 rounded-full"></div>
                    <h3 class="text-2xl font-bold mb-4 title-font text-center">致雯芯</h3>
                    <p class="mb-4 leading-relaxed">亲爱的雯芯：</p>
                    <p class="mb-4 leading-relaxed">今天是你的16岁生日，首先要祝你生日快乐！时间过得真快，我们相识已经有这么多天了。虽然我们不是男女朋友，但我很珍惜我们之间的友谊。</p>
                    <p class="mb-4 leading-relaxed">记得我们第一次聊天，第一次吵架，每一次的互动都让我更加了解你。你是一个特别的女孩，有着自己的想法和坚持，这也是我最欣赏你的地方。</p>
                    <p class="mb-4 leading-relaxed">16岁是一个美丽的年纪，充满了无限可能。希望你在未来的日子里，能够保持这份纯真和热情，勇敢地追求自己的梦想。无论遇到什么困难，都要记得你不是一个人，我会一直在你身边支持你。</p>
                    <p class="mb-4 leading-relaxed">知道你喜欢《CLANNAD》，喜欢古河渚和冈崎朋也，喜欢毛泽东；也知道你讨厌对谁都温柔的人。这些点点滴滴，都让我觉得你是一个真实、可爱的女孩。</p>
                    <p class="mb-4 leading-relaxed">最后，再次祝你生日快乐！愿你的16岁充满阳光和欢笑，所有的愿望都能实现。</p>
                    <p class="text-right font-bold mt-6">张翔</p>
                </div>
                <div class="text-6xl md:text-8xl font-bold title-font text-primary mb-2 pulse" style="letter-spacing: 10px;">16</div>
                <p class="text-lg text-gray-500">美好的16岁</p>
            </div>
        </section>

        <!-- Footer -->
        <footer class="bg-dark text-white py-10 px-4 text-center">
            <p class="mb-4">雯芯生日快乐 | 2025.08.29</p>
            <div class="flex justify-center space-x-4 mb-6">
                <button id="play-music" class="bg-primary hover:bg-primary/80 text-white p-2 rounded-full transition-colors">
                    <i class="fa fa-music"></i>
                </button>
                <button id="pause-music" class="bg-gray-600 hover:bg-gray-500 text-white p-2 rounded-full transition-colors hidden">
                    <i class="fa fa-pause"></i>
                </button>
                <button id="next-song" class="bg-secondary hover:bg-secondary/80 text-white p-2 rounded-full transition-colors">
                    <i class="fa fa-step-forward"></i>
                </button>
            </div>
            <p class="text-sm opacity-70">用❤️制作的生日祝福</p>
        </footer>
    </div>

    <!-- Music Elements -->
    <audio id="music" loop>Your browser does not support the audio element.</audio>

    <script>
        // Password Protection
        const passwordScreen = document.getElementById('password-screen');
        const mainContent = document.getElementById('main-content');
        const passwordInput = document.getElementById('password');
        const errorMessage = document.getElementById('error-message');

        passwordInput.addEventListener('input', function() {
            if (this.value.length === 4) {
                if (this.value === '0829') {
                    passwordScreen.classList.add('opacity-0');
                    setTimeout(() => {
                        passwordScreen.classList.add('hidden');
                        mainContent.classList.remove('hidden');
                        initCounter();
                        initMap();
                        initCharts();
                        initScrollAnimation();
                        createHearts();
                        playRandomSong();
                    }, 1000);
                } else {
                    errorMessage.classList.remove('hidden');
                    setTimeout(() => {
                        errorMessage.classList.add('hidden');
                        this.value = '';
                    }, 1500);
                }
            }
        });

        // Counter Function
        function initCounter() {
            const startDate = new Date(2025, 3, 25, 23, 24, 0); // April 25, 2025 23:24
            const daysCounter = document.getElementById('days-counter');
            const daysElement = document.getElementById('days');
            const hoursElement = document.getElementById('hours');
            const minutesElement = document.getElementById('minutes');
            const secondsElement = document.getElementById('seconds');

            function updateCounter() {
                const now = new Date();
                const diff = now - startDate;

                const days = Math.floor(diff / (1000 * 60 * 60 * 24));
                const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
                const seconds = Math.floor((diff % (1000 * 60)) / 1000);

                daysCounter.textContent = `${days}天 ${hours}时 ${minutes}分 ${seconds}秒`;
                daysElement.textContent = days;
                hoursElement.textContent = hours;
                minutesElement.textContent = minutes;
                secondsElement.textContent = seconds;
            }

            updateCounter();
            setInterval(updateCounter, 1000);
        }

        // Map Function
        function initMap() {
            // 使用简单的地图实现，避免复杂的API依赖
            const mapContainer = document.getElementById('map-container');

            // 创建一个简单的地图表示
            mapContainer.innerHTML = `
                <div class="relative w-full h-full bg-blue-50 rounded-lg overflow-hidden">
                    <div class="absolute top-1/4 left-1/4 w-3 h-3 bg-primary rounded-full animate-ping"></div>
                    <div class="absolute top-1/4 left-1/4 w-3 h-3 bg-primary rounded-full"></div>
                    <div class="absolute top-1/4 left-1/4 text-xs font-bold mt-4 -ml-12">山东曲阜</div>
                    
                    <div class="absolute top-1/2 right-1/4 w-3 h-3 bg-secondary rounded-full animate-ping"></div>
                    <div class="absolute top-1/2 right-1/4 w-3 h-3 bg-secondary rounded-full"></div>
                    <div class="absolute top-1/2 right-1/4 text-xs font-bold mt-4 -ml-12">河南光山</div>
                    
                    <svg class="absolute inset-0 w-full h-full" viewBox="0 0 100 100" preserveAspectRatio="none">
                        <path d="M25,25 Q50,50 75,50" stroke="#ff6b8b" stroke-width="0.5" fill="none" stroke-dasharray="5,5" animate="dash 5s linear infinite"/>
                    </svg>
                    
                    <div class="absolute inset-0 bg-[url('https://picsum.photos/id/101/800/400')] bg-cover bg-center opacity-40"></div>
                </div>
            `;
        }

        // Charts Function
        function initCharts() {
            // 雯芯的五行图表
            const wenxinCtx = document.getElementById('wenxin-chart').getContext('2d');
            new Chart(wenxinCtx, {
                type: 'doughnut',
                data: {
                    labels: ['木', '火', '土', '金', '水'],
                    datasets: [{
                        data: [3, 22, 22, 11, 38],
                        backgroundColor: [
                            '#2ecc71',  // 木-绿色
                            '#e74c3c',  // 火-红色
                            '#f39c12',  // 土-橙色
                            '#3498db',  // 金-蓝色
                            '#9b59b6'   // 水-紫色
                        ],
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            position: 'bottom',
                        },
                        title: {
                            display: true,
                            text: '五行分布',
                            font: {
                                size: 16
                            }
                        }
                    }
                }
            });

            // 张翔的五行图表
            const zhangxiangCtx = document.getElementById('zhangxiang-chart').getContext('2d');
            new Chart(zhangxiangCtx, {
                type: 'doughnut',
                data: {
                    labels: ['木', '火', '土', '金', '水'],
                    datasets: [{
                        data: [2, 49, 19, 24, 3],
                        backgroundColor: [
                            '#2ecc71',  // 木-绿色
                            '#e74c3c',  // 火-红色
                            '#f39c12',  // 土-橙色
                            '#3498db',  // 金-蓝色
                            '#9b59b6'   // 水-紫色
                        ],
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            position: 'bottom',
                        },
                        title: {
                            display: true,
                            text: '五行分布',
                            font: {
                                size: 16
                            }
                        }
                    }
                }
            });
        }

        // Scroll Animation
        function initScrollAnimation() {
            const sections = document.querySelectorAll('.section');

            function checkVisibility() {
                sections.forEach(section => {
                    const rect = section.getBoundingClientRect();
                    const windowHeight = window.innerHeight;

                    if (rect.top < windowHeight * 0.75) {
                        section.classList.add('visible');
                    }
                });
            }

            window.addEventListener('scroll', checkVisibility);
            checkVisibility(); // 初始检查
        }

        // Create Hearts Animation
        function createHearts() {
            const heartsContainer = document.getElementById('hearts-container');
            const colors = ['#ff6b8b', '#ff8fa3', '#ffb3c1', '#ffccd5'];

            function createHeart() {
                const heart = document.createElement('div');
                heart.classList.add('heart');
                heart.style.left = Math.random() * 100 + 'vw';
                heart.style.top = Math.random() * 100 + 'vh';
                heart.style.animationDelay = Math.random() * 5 + 's';
                heart.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                heart.style.width = Math.random() * 15 + 10 + 'px';
                heart.style.height = heart.style.width;

                heartsContainer.appendChild(heart);

                // 移除动画结束的爱心
                setTimeout(() => {
                    heart.remove();
                }, 5000);
            }

            // 持续创建爱心
            setInterval(createHeart, 300);
        }

        // Music Player
        const music = document.getElementById('music');
        const playButton = document.getElementById('play-music');
        const pauseButton = document.getElementById('pause-music');
        const nextButton = document.getElementById('next-song');
        const songs = [
            'wenxin疑心病.aac',
            'wenxin说好的幸福呢.aac',
            'wenxinAs long as you love.aac'
        ];
        let currentSongIndex = 0;

        function playRandomSong() {
            currentSongIndex = Math.floor(Math.random() * songs.length);
            music.src = songs[currentSongIndex];
            music.play().catch(error => {
                console.log('音乐播放失败:', error);
                // 如果自动播放失败，显示播放按钮
                playButton.classList.remove('hidden');
                pauseButton.classList.add('hidden');
            });
            playButton.classList.add('hidden');
            pauseButton.classList.remove('hidden');
        }

        playButton.addEventListener('click', () => {
            music.play();
            playButton.classList.add('hidden');
            pauseButton.classList.remove('hidden');
        });

        pauseButton.addEventListener('click', () => {
            music.pause();
            pauseButton.classList.add('hidden');
            playButton.classList.remove('hidden');
        });

        nextButton.addEventListener('click', () => {
            currentSongIndex = (currentSongIndex + 1) % songs.length;
            music.src = songs[currentSongIndex];
            music.play();
            playButton.classList.add('hidden');
            pauseButton.classList.remove('hidden');
        });
    </script>
</body>
</html>
