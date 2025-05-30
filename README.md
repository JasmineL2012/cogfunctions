<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <title>荣格八维认知功能测试</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- 示例用 Unsplash 星空海面静图，建议你换成真实动图 GIF/MP4/WEBM 背景 -->
    <style>
        html, body {
            height: 100%;
            margin: 0;
            padding: 0;
        }
        body {
            min-height: 100vh;
            min-width: 100vw;
            overflow-x: hidden;
            background: #0a1833;
            /* 用真实动图替换下方URL即可 */
            background-image: url('[https://images.unsplash.com/photo-1506744038136-46273834b3fb?auto=format&fit=crop&w=1500&q=80](https://cdn.pixabay.com/photo/2023/10/10/11/28/star-trails-8306233_1280.jpg)');
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
            animation: bgmove 30s linear infinite alternate;
        }
        @keyframes bgmove {
            0% { background-position: 50% 60%; }
            100% { background-position: 50% 40%; }
        }
        .overlay {
            position: fixed;
            inset: 0;
            background: rgba(10,24,51,0.55);
            z-index: 0;
        }
        .center-card {
            position: absolute;
            left: 50%;
            top: 50%;
            transform: translate(-50%,-50%);
            background: rgba(255,255,255,0.13);
            box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
            border-radius: 18px;
            padding: 38px 32px 32px 32px;
            max-width: 480px;
            width: 90vw;
            text-align: center;
            z-index: 1;
            backdrop-filter: blur(8px);
        }
        .title {
            font-size: 2.1em;
            font-weight: bold;
            color: #f8f8ff;
            letter-spacing: 2px;
            margin-bottom: 1.2em;
            text-shadow: 0 2px 12px #222a;
        }
        .start-btn, .option-btn, .nav-btn {
            font-family: inherit;
            font-size: 1.15em;
            border: none;
            border-radius: 12px;
            padding: 12px 32px;
            margin: 18px 0 0 0;
            background: linear-gradient(90deg, #fff 0%, #e0e0e0 100%);
            color: #0a1833;
            font-weight: bold;
            box-shadow: 0 2px 12px rgba(10,24,51,0.10);
            cursor: pointer;
            transition: background 0.18s, color 0.18s, transform 0.12s;
        }
        .start-btn:hover, .nav-btn:hover {
            background: linear-gradient(90deg, #e0e0e0 0%, #fff 100%);
            transform: translateY(-2px) scale(1.04);
        }
        .question-title {
            font-size: 1.3em;
            color: #fff;
            margin-bottom: 1.2em;
            text-shadow: 0 2px 8px #222a;
        }
        .options-row {
            display: flex;
            justify-content: space-between;
            gap: 12px;
            margin: 28px 0 18px 0;
        }
        .option-btn {
            flex: 1 1 0;
            margin: 0;
            padding: 16px 0;
            font-size: 1.08em;
            border-radius: 14px;
            border: none;
            color: #fff;
            font-weight: 500;
            box-shadow: 0 2px 8px rgba(10,24,51,0.10);
            transition: background 0.18s, transform 0.12s, box-shadow 0.18s;
            outline: none;
        }
        .option-btn.selected, .option-btn:active {
            box-shadow: 0 4px 18px 0 rgba(127,83,172,0.18);
            transform: scale(1.06);
            border: 2px solid #fff;
        }
        .option-btn.red    { background: #ff4e50; }
        .option-btn.orange { background: #ffb347; color: #222; }
        .option-btn.gray   { background: #e0e0e0; color: #222; }
        .option-btn.blue   { background: #00b894; }
        .option-btn.green  { background: #00c853; }
        .option-btn:hover:not(:disabled) {
            filter: brightness(1.08) saturate(1.2);
            transform: scale(1.08);
        }
        .option-btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
        }
        .nav-btn {
            margin: 0 8px;
            padding: 10px 28px;
            background: linear-gradient(90deg, #fff 0%, #e0e0e0 100%);
            color: #0a1833;
        }
        .nav-btn:disabled {
            background: #bdbdbd;
            color: #fff;
            cursor: not-allowed;
        }
        .progress-bar {
            width: 100%;
            background: rgba(255,255,255,0.18);
            border-radius: 6px;
            height: 10px;
            margin-bottom: 18px;
            overflow: hidden;
        }
        .progress {
            height: 100%;
            background: linear-gradient(90deg, #ffe7ba 0%, #7f53ac 100%);
            border-radius: 6px;
            transition: width 0.3s;
        }
        .error {
            color: #ffe066;
            margin-top: 10px;
            min-height: 24px;
        }
        ul {
            text-align: left;
            padding-left: 1.2em;
            color: #fff;
        }
        .result-title {
            color: #ffe7ba;
            margin-bottom: 1em;
        }
        @media (max-width: 600px) {
            .center-card { padding: 18px 4vw 18px 4vw; }
            .title { font-size: 1.2em; }
            .question-title { font-size: 1em; }
            .option-btn { font-size: 0.95em; padding: 12px 0; }
        }
    </style>
</head>
<body>
    <div class="overlay"></div>
    <div id="quiz-app"></div>
    <script>
        // 题目与变量
        const questions = [
            "1. 你相信很多行为、事情都可以分为符合标准、不符合标准的，而那些符合标准的是好的",
            "2. 你总是在追求公正客观的判断。比如你不在乎一个人偷东西是否迫不得已，他事实上就是做错了",
            "3. 你经常感知到一个物体、一件事在未来某个时刻的样子",
            "4. 你产生的想象和你有着独一无二的联系，你的经历和自身导致你产生这些想象，这些想象也是你自身的重要组成部分",
            "5. 当你有一个想法时，你想让它在现实中产生最大效益",
            "6. 你的感受经常和别人的不同。比如有时别人觉得B在阴阳你但你不这么觉得, 你觉得A在讨好你时别人又不这么觉得",
            "7. 你总结出一个人的性格（比如甜美的、帅气的、温柔的）并发现他们的行为大部分时候符合你的印象",
            "8. 如果一个人说了伤害你的话，你受伤害的感受会随着不断感受它而加深, 你意识到这种感受在蒙蔽你并想摆脱，但你总忍不住去想它和它相关的事",
            "9. 当感官刺激足够强时，你会想沉浸其中，不去思考你为什么会有这样的感受、这样的感受好不好、有什么意义和影响",
            "10. 你总是在想我怎么做、别人怎么做可以让事情变得更好",
            "11. 你不到不得已不做出确定的选择，这不是因为选择困难症, 而是你觉得前面总有更好的选择等着你",
            "12. 你喜欢听不同的方案和想法，并思考他们是否合理或他们的可行性"
        ];
        const questionVars = [
            "Te+", "Te+", "Ni+", "Ni+", "Ni+", "Si+", "Si+", "Si-", "Se+", "Ne+", "Ne+", "Ne+"
        ];
        const varNames = [
            "Ne+", "Ne-", "Ni+", "Ni-", "Fe+", "Fe-", "Fi+", "Fi-", "Ti+", "Ti-", "Te+", "Te-", "Si+", "Si-", "Se+", "Se-"
        ];
        let varScores = {};
        varNames.forEach(name => varScores[name] = 0);

        const options = [
            { text: "非常不同意", value: -5, color: "red" },
            { text: "不同意", value: -3, color: "orange" },
            { text: "中立", value: 0, color: "gray" },
            { text: "同意", value: 3, color: "blue" },
            { text: "非常同意", value: 5, color: "green" }
        ];

        let answers = new Array(questions.length).fill(null);
        let current = 0;

        // 首页
        function renderHome() {
            document.getElementById('quiz-app').innerHTML = `
                <div class="center-card">
                    <div class="title">荣格八维认知功能测试</div>
                    <p style="color:#f8f8ff;opacity:0.92;">探索你的认知风格，发现自我潜能</p>
                    <button class="start-btn" onclick="startTest()">开始测试</button>
                </div>
            `;
        }

        // 题目页
        function showQuestion(errorMsg = '') {
            let progress = Math.round((current + 1) / questions.length * 100);
            let optionsHtml = options.map((opt, idx) => `
                <button
                    class="option-btn ${opt.color} ${answers[current] === opt.value ? 'selected' : ''}"
                    onclick="selectOption(${opt.value})"
                    type="button"
                >${opt.text}</button>
            `).join('');
            document.getElementById('quiz-app').innerHTML = `
                <div class="center-card">
                    <div class="progress-bar"><div class="progress" style="width:${progress}%;"></div></div>
                    <div class="question-title">${questions[current]}</div>
                    <div class="options-row">${optionsHtml}</div>
                    <div class="btn-group" style="margin-top:24px;">
                        <button class="nav-btn" onclick="prevQuestion()" ${current === 0 ? 'disabled' : ''}>上一题</button>
                        <button class="nav-btn" onclick="nextQuestion()">${current === questions.length - 1 ? '提交' : '下一题'}</button>
                    </div>
                    <div class="error">${errorMsg}</div>
                </div>
            `;
        }

        // 自动跳下一题
        function selectOption(val) {
            answers[current] = val;
            if (current < questions.length - 1) {
                current++;
                showQuestion();
            } else {
                submitQuiz();
            }
        }

        function prevQuestion() {
            if (current > 0) {
                current--;
                showQuestion();
            }
        }

        function nextQuestion() {
            if (answers[current] === null) {
                showQuestion('请先选择一个选项');
                return;
            }
            if (current < questions.length - 1) {
                current++;
                showQuestion();
            } else {
                submitQuiz();
            }
        }

        function startTest() {
            current = 0;
            answers = new Array(questions.length).fill(null);
            showQuestion();
        }

        // 结果页
        function submitQuiz() {
            // 统计分数
            varNames.forEach(name => varScores[name] = 0);
            answers.forEach((score, idx) => {
                if (score !== null) {
                    varScores[questionVars[idx]] += score;
                }
            });
            document.getElementById('quiz-app').innerHTML = `
                <div class="center-card">
                    <div class="result-title">测试完成！</div>
                    <p style="margin-bottom:1em;">各变量得分：</p>
                    <ul>
                        ${Object.entries(varScores).map(([k, v]) => `<li><b>${k}</b>：${v}</li>`).join('')}
                    </ul>
                    <button class="start-btn" onclick="renderHome()">返回首页</button>
                </div>
            `;
        }

        // 初始化
        renderHome();
    </script>
</body>
</html>

