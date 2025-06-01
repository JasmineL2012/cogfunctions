<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <title>荣格八维认知功能测试</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        html, body { height: 100%; margin: 0; padding: 0; font-family: 'Segoe UI', 'PingFang SC', 'Hiragino Sans GB', 'Arial', sans-serif; }
        body {
            min-height: 100vh; min-width: 100vw; overflow-x: hidden;
            background: #0a1833;
            background-image: url('https://cdn.pixabay.com/photo/2023/10/10/11/28/star-trails-8306233_1280.jpg');
            background-size: cover; background-position: center; background-repeat: no-repeat;
            animation: bgmove 30s linear infinite alternate;
        }
        @keyframes bgmove { 0% { background-position: 50% 60%; } 100% { background-position: 50% 40%; } }
        .overlay { position: fixed; inset: 0; background: rgba(10,24,51,0.55); z-index: 0; }
        .center-card {
            position: absolute;
            left: 50%; top: 50%;
            transform: translate(-50%,-50%);
            background: rgba(255,255,255,0.13);
            box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
            border-radius: 18px;
            padding: 38px 32px 32px 32px;
            max-width: 1100px;
            width: 92vw;
            text-align: center;
            z-index: 1;
            backdrop-filter: blur(8px);
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .title { font-size: 2.1em; font-weight: bold; color: #f8f8ff; letter-spacing: 2px;
            margin-bottom: 1.2em; text-shadow: 0 2px 12px #222a; }
        .start-btn, .nav-btn { font-family: inherit; font-size: 1.15em; border: none; border-radius: 12px;
            padding: 12px 32px; margin: 18px 0 0 0; background: linear-gradient(90deg, #fff 0%, #e0e0e0 100%);
            color: #0a1833; font-weight: bold; box-shadow: 0 2px 12px rgba(10,24,51,0.10); cursor: pointer;
            transition: background 0.18s, color 0.18s, transform 0.12s; }
        .start-btn:hover, .nav-btn:hover { background: linear-gradient(90deg, #e0e0e0 0%, #fff 100%);
            transform: translateY(-2px) scale(1.04); }
        .question-title { font-size: 1.3em; color: #fff; margin-bottom: 1.2em; text-shadow: 0 2px 8px #222a; }
        .options-slider { display: flex; align-items: center; justify-content: space-between;
            margin: 36px 0 18px 0; gap: 0; }
        .slider-label {
            font-size: 1.08em; margin-top: 8px; font-weight: bold;
            width: 48px; text-align: center; letter-spacing: 2px;
            background: rgba(255,255,255,0.10);
            border-radius: 10px;
            padding: 4px 0;
            box-shadow: 0 2px 8px 0 rgba(31,38,135,0.07);
        }
        .slider-label.right { color: #62b283; }
        .slider-label { color: #b44143; }
        .slider-radio-group {
            display: flex; flex: 1; justify-content: space-between; align-items: center;
            position: relative; margin: 0 8px;
            gap: 18px;
        }
        .slider-radio-group::before { content: ''; position: absolute; top: 50%; left: 0; right: 0; height: 4px;
            background: linear-gradient(90deg, #b44143 0%, #dda95f 25%, #e0e0e0 50%, #4ba694 75%, #62b283 100%);
            z-index: 0; transform: translateY(-50%); border-radius: 2px; }
        .slider-radio {
            background: none;
            border: none;
            outline: none;
            cursor: pointer;
            padding: 0;
            margin: 0;
            transition: transform 0.18s;
        }
        .slider-radio .slider-radio-inner {
            background: linear-gradient(180deg, rgba(255,255,255,0.18) 0%, rgba(98,178,131,0.09) 100%);
            border-radius: 50%;
            min-width: 48px;
            min-height: 48px;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 2px 12px 0 rgba(31,38,135,0.10);
            transition: background 0.18s, box-shadow 0.18s;
            border: 2px solid rgba(255,255,255,0.18);
        }
        .slider-radio.selected .slider-radio-inner {
            background: linear-gradient(180deg, #62b283 0%, #ffe7ba 100%);
            box-shadow: 0 0 0 4px rgba(98,178,131,0.18);
            border: 2.5px solid #ffe7ba;
        }
        .slider-radio .slider-radio-circle {
            width: 28px; height: 28px; border-radius: 50%;
            border: 2.5px solid #e0e0e0; background: #f8f8ff;
            display: flex; align-items: center; justify-content: center;
            transition: border-color 0.18s, box-shadow 0.18s;
        }
        .slider-radio.selected .slider-radio-circle {
            border-color: #62b283;
            background: #ffe7ba;
        }
        .slider-radio .slider-radio-circle-inner {
            width: 14px; height: 14px; border-radius: 50%; background: #fff; opacity: 0;
            transition: opacity 0.18s;
        }
        .slider-radio.selected .slider-radio-circle-inner {
            opacity: 1; background: #62b283;
        }
        .slider-radio-text {
            margin-top: 6px;
            font-size: 1.08em;
            color: #f8f8ff;
            letter-spacing: 1px;
            text-shadow: 0 1px 6px #222a;
            font-weight: 500;
            transition: color 0.18s;
        }
        .slider-radio.selected .slider-radio-text {
            color: #ffe7ba;
            font-weight: bold;
            text-shadow: 0 2px 10px #222a;
        }
        .nav-btn { margin: 0 8px; padding: 10px 28px; background: linear-gradient(90deg, #fff 0%, #e0e0e0 100%);
            color: #0a1833; }
        .nav-btn:disabled { background: #bdbdbd; color: #fff; cursor: not-allowed; }
        .progress-bar { width: 100%; background: rgba(255,255,255,0.18); border-radius: 6px; height: 10px;
            margin-bottom: 18px; overflow: hidden; }
        .progress { height: 100%; background: linear-gradient(90deg, #ffe7ba 0%, #7f53ac 100%);
            border-radius: 6px; transition: width 0.3s; }
        .error { color: #ffe066; margin-top: 10px; min-height: 24px; }
        ul { text-align: left; padding-left: 1.2em; color: #fff; }
        .result-title { color: #ffe7ba; margin-bottom: 1em; }
        .bar-chart-row {
            display: flex; align-items: center; margin-bottom: 8px;
        }
        .bar-label {
            display: inline-block; width: 48px; color: #ffe7ba; font-weight: bold; font-size: 1.08em;
        }
        .bar-bg {
            background: rgba(255,255,255,0.12);
            border-radius: 6px;
            height: 18px;
            width: 240px;
            margin: 0 8px;
            position: relative;
            overflow: hidden;
        }
        .bar-inner {
            background: linear-gradient(90deg, #62b283 0%, #ffe7ba 100%);
            height: 100%;
            border-radius: 6px;
            transition: width 0.3s;
        }
        .bar-value {
            margin-left: 8px; color: #ffe7ba; font-size: 1.08em;
        }
        @media (max-width: 600px) {
            .center-card { padding: 18px 4vw 18px 4vw; }
            .title { font-size: 1.2em; }
            .question-title { font-size: 1em; }
            .slider-radio-circle { width: 24px; height: 24px; }
            .slider-radio-circle-inner { width: 10px; height: 10px; }
            .slider-label { font-size: 0.95em; width: 36px; }
            .bar-bg { width: 120px; }
        }
        @media (max-width: 900px) {
            .center-card { flex-direction: column !important; max-width: 98vw !important; }
        }
    </style>
</head>
<body>
    <div class="overlay"></div>
    <div id="quiz-app"></div>
    <script>
        // ===================== 你可以自定义的部分 =====================
        const questions = [
    // 外倾思维Te
    { text: "你相信有一个标准能区分大部分行为、事情，而那些符合标准的是好的", func: "Te", polarity: "positive", weight: 1 },
    { text: "你不喜欢考虑那么多特殊情况。比如你不在乎一个人偷东西是否迫不得已，他事实上就是做错了", func: "Te", polarity: "positive", weight: 2 },
    { text: "你有种使命感让身边的人符合客观标准定义的好", func: "Te", polarity: "positive", weight: 4 },
    { text: "如果把生命的感性部分剔除掉，可能有客观的标准能分辨好坏，但这显然不太可能", func: "Te", polarity: "negative", weight: 1 },
    { text: "难以接受生活在标准划分下的世界里，那些艺术的、感性的事物都不复存在了", func: "Te", polarity: "negative", weight: 3 },
    { text: "你从不用统一准则来评判别人的生活方式，因为萝卜青菜各有所爱", func: "Te", polarity: "negative", weight: 3 },

    // 内倾直觉Ni
    { text: "你经常感知到一个物体、一件事在未来某个时刻的样子", func: "Ni", polarity: "positive", weight: 2 },
    { text: "你产生的想象和你有着独一无二的联系，你的经历和自身导致你产生这些想象，这些想象也是你自身的重要组成部分", func: "Ni", polarity: "positive", weight: 4 },
    { text: "你有时会思考你的想象对你和世界来说有什么意义", func: "Ni", polarity: "positive", weight: 1 },
    { text: "你有过一种强烈的“预感”某件坏事会发生，并因此提前作出了规避或抵触行为", func: "Ni", polarity: "negative", weight: 3 },
    { text: "有时你会感知自己的失败而提前放弃努力", func: "Ni", polarity: "negative", weight: 2 },
    { text: "你曾觉得自己应该选择某个专业，即使现实因素告诉你这并不合适，但你仍很执着", func: "Ni", polarity: "negative", weight: 2 },

    // 内倾感觉Si
    { text: "你的感受经常和别人的不同。比如有时别人觉得B在阴阳你但你不这么觉得，你觉得A在讨好你时别人又不这么觉得", func: "Si", polarity: "positive", weight: 1 },
    { text: "你总结出一个人的性格（比如甜美的、帅气的、温柔的）并发现他们的行为大部分时候符合你的印象", func: "Si", polarity: "positive", weight: 3 },
    { text: "你去某些从未去过的地方有种莫名的熟悉感，可能因为你经常读类似背景的小说", func: "Si", polarity: "positive", weight: 3 },
    { text: "如果一个人说了伤害你的话，你受伤害的感受会随着不断感受它而加深，你意识到这种感受在蒙蔽你并想摆脱，但你总忍不住去想它和它相关的事", func: "Si", polarity: "negative", weight: 3 },
    { text: "你希望自己可以完全摒弃主观感受，客观地感受事物的存在，但你知道这是不可能的", func: "Si", polarity: "negative", weight: 2 },
    { text: "你有一些难以解释的偏好或排斥，比如讨厌某种颜色组合。你说不上来理由但很坚持", func: "Si", polarity: "negative", weight: 2 },

    // 外倾感觉Se
    { text: "你觉得人活一生就是为了体验，很少担心过度纵欲", func: "Se", polarity: "positive", weight: 3 },
    { text: "你的朋友会评价你是一个很会发掘新玩法的人", func: "Se", polarity: "positive", weight: 2 },
    { text: "如果无法想通一件事，你会很快投入到新刺激中转移注意力", func: "Se", polarity: "positive", weight: 2 },
    { text: "在场面彻底失控的情况下，你有种破罐子破摔的冲动", func: "Se", polarity: "negative", weight: 4 },
    { text: "如果在嘈杂的环境中工作，你会感到难以集中注意力", func: "Se", polarity: "negative", weight: 2 },
    { text: "被打断后，你需要一点时间才能回到原本的工作状态", func: "Se", polarity: "negative", weight: 1 },

    // 外倾直觉Ne
    { text: "你不到不得已不做出选择，这不是因为选择困难症，而是你觉得前面总有更好的选择等着你", func: "Ne", polarity: "positive", weight: 4 },
    { text: "在合作中有人提出了新方案，你总是认真考虑，不在乎方案由谁提出", func: "Ne", polarity: "positive", weight: 2 },
    { text: "你会是一个优秀的人事经理，能看出应聘者的潜能", func: "Ne", polarity: "positive", weight: 1 },
    { text: "你经常感受到那些潜在的危险并远离它们", func: "Ne", polarity: "negative", weight: 3 },
    { text: "第二天你要出席一个重要会议，你会不自觉地想各种可能，然后嘲笑自己为什么会有这么无厘头的想法", func: "Ne", polarity: "negative", weight: 3 },
    { text: "面对太多可能时你会感到不知所措，会想选错了会怎么样", func: "Ne", polarity: "negative", weight: 1 },

    // 外倾情感Fe
    { text: "你常以温和的态度示人，也希望人们能互相理解和尊重", func: "Fe", polarity: "positive", weight: 3 },
    { text: "如果你穿越到古代，你不会传递那些与时代不符的价值观，例如人人平等。", func: "Fe", polarity: "positive", weight: 1 },
    { text: "你觉得那些大多数人认可的东西具有先验性，大部分时候都是对的", func: "Fe", polarity: "positive", weight: 3 },
    { text: "世界上有些人缺少、甚至抗拒独立思考，不会有意去探索那些感受不到的东西。", func: "Fe", polarity: "negative", weight: 3 },
    { text: "你有时会梦到和身边的人产生冲突，并发觉现实中确实有这样的倾向", func: "Fe", polarity: "negative", weight: 2 },
    { text: "你觉得“我是谁”和“我应该成为谁”之间的界限很模糊", func: "Fe", polarity: "negative", weight: 2 },

    // 内倾情感Fi
    { text: "你的情感是很私密的，不想用它来打动、改变那些外界的东西", func: "Fi", polarity: "positive", weight: 1 },
    { text: "有时你希望那些隐秘的情感被人理解和重视，但你不会表现出来", func: "Fi", polarity: "positive", weight: 1 },
    { text: "你绝不会为了世俗的成功和认可而放弃个人价值观", func: "Fi", polarity: "positive", weight: 4 },
    { text: "明明很在乎某人，却故意表现冷淡", func: "Fi", polarity: "negative", weight: 2 },
    { text: "如果被要求表达强烈的情感立场，你会感到不知所措", func: "Fi", polarity: "negative", weight: 3 },
    { text: "你有时会分析自己为什么会有这样的情感，事后又觉得很没必要", func: "Fi", polarity: "negative", weight: 2 },

    // 内倾思维Ti
    { text: "你觉得理念本身非常崇高，不一定要为现实服务", func: "Ti", polarity: "positive", weight: 3 },
    { text: "如果不能从辩论中持续完善论点，你不会继续下去。表面上的输赢其实没那么重要", func: "Ti", polarity: "positive", weight: 2 },
    { text: "在思考问题时，你喜欢把尽可能多的复杂情况考虑进去", func: "Ti", polarity: "positive", weight: 2 },
    { text: "有时你已经很清晰的说明了你的理念和观点，但别人还是难以理解", func: "Ti", polarity: "negative", weight: 2 },
    { text: "你对自己的理念缺乏确定性，经常觉得考虑的还不够完善", func: "Ti", polarity: "negative", weight: 3 },
    { text: "如果他人逻辑混乱，你总忍不住打断而惹他们不高兴", func: "Ti", polarity: "negative", weight: 2 }
];
        const options = [
            { text: "完全不符合", value: 1, color: "red" },
            { text: "不符合", value: 2, color: "orange" },
            { text: "中立", value: 3, color: "gray" },
            { text: "符合", value: 4, color: "blue" },
            { text: "非常同意", value: 5, color: "green" }
        ];
        const functions = ["Ne","Ni","Fe","Fi","Ti","Te","Si","Se"];
        const typeTable = {
            INTJ: ["Ni","Te","Fi","Se","Ne","Ti","Fe","Si"],
            INTP: ["Ti","Ne","Si","Fe","Te","Ni","Se","Fi"],
            ENTJ: ["Te","Ni","Se","Fi","Fe","Ne","Si","Ti"],
            ENTP: ["Ne","Ti","Fe","Si","Ni","Te","Fi","Se"],
            INFJ: ["Ni","Fe","Ti","Se","Ne","Fi","Te","Si"],
            INFP: ["Fi","Ne","Si","Te","Fe","Ni","Se","Ti"],
            ENFP: ["Ne","Fi","Te","Si","Ni","Fe","Ti","Se"],
            ENFJ: ["Fe","Ni","Se","Ti","Fi","Ne","Si","Te"],
            ISTJ: ["Si","Te","Fi","Ne","Se","Ti","Fe","Ni"],
            ISFJ: ["Si","Fe","Ti","Ne","Se","Fi","Te","Ni"],
            ESTJ: ["Te","Si","Ne","Fi","Fe","Se","Ni","Ti"],
            ESFJ: ["Fe","Si","Ne","Ti","Fi","Se","Ni","Te"],
            ESTP: ["Se","Ti","Fe","Ni","Si","Te","Fi","Ne"],
            ESFP: ["Se","Fi","Te","Ni","Si","Fe","Ti","Ne"],
            ISTP: ["Ti","Se","Ni","Fe","Te","Si","Ne","Fi"],
            ISFP: ["Fi","Se","Ni","Te","Fe","Si","Ne","Ti"]
        };
        let userScores = {};
        functions.forEach(f => userScores[f] = [0,0,0,0,0,0,0,0]);
        let answers = new Array(questions.length).fill(null);
        let current = 0;

        function showStartDialog() {
            if (document.getElementById('start-dialog')) return;
            const dialog = document.createElement('div');
            dialog.id = 'start-dialog';
            dialog.style.position = 'fixed';
            dialog.style.left = '0'; dialog.style.top = '0'; dialog.style.width = '100vw'; dialog.style.height = '100vh';
            dialog.style.background = 'rgba(10,24,51,0.55)';
            dialog.style.zIndex = '9999';
            dialog.innerHTML = `
                <div style="
                    position:absolute;left:50%;top:50%;transform:translate(-50%,-50%);
                    background:rgba(255,255,255,0.13);backdrop-filter:blur(8px);
                    border-radius:18px;box-shadow:0 8px 32px 0 rgba(31,38,135,0.37);
                    padding:38px 32px 32px 32px;max-width:420px;width:90vw;text-align:left;
                ">
                    <div style="color:#ffe7ba;font-size:1.18em;font-weight:bold;margin-bottom:1em;">测试须知</div>
                    <div style="color:#fff;line-height:1.8;font-size:1.08em;">
                        1. 部分测试题为深刻了解荣格八维的用户服务，旨在防止用户猜测题目意图。<br>
                        2. 为保证测试准确性，请以你大多数情况下的做法为准答题，而不是“应该这么做”或“我也可以这么做”。
                    </div>
                    <div style="text-align:center;margin-top:2em;">
                        <button class="start-btn" onclick="closeStartDialogAndBegin()">确认</button>
                    </div>
                </div>
            `;
            document.body.appendChild(dialog);
        }
        function closeStartDialogAndBegin() {
            const dialog = document.getElementById('start-dialog');
            if (dialog) dialog.remove();
            actuallyStartTest();
        }
        function renderHome() {
            document.getElementById('quiz-app').innerHTML = `
                <div class="center-card">
                    <div class="title">荣格八维认知功能测试</div>
                    <p style="color:#f8f8ff;opacity:0.92;">探索你的认知风格，发现自我潜能</p>
                    <button class="start-btn" onclick="startTest()">开始测试</button>
                </div>
            `;
        }
        function showQuestion(errorMsg = '') {
            let progress = Math.round((current + 1) / questions.length * 100);
            let leftLabel = `<div class="slider-label">否</div>`;
            let rightLabel = `<div class="slider-label right">是</div>`;
            let sliderHtml = options.map((opt, idx) => `
                <button
                    class="slider-radio ${opt.color} ${answers[current] === opt.value ? 'selected' : ''}"
                    onclick="selectOption(${opt.value})"
                    type="button"
                    aria-label="${opt.text}"
                >
                    <div class="slider-radio-inner">
                        <div class="slider-radio-circle">
                            <div class="slider-radio-circle-inner"></div>
                        </div>
                    </div>
                </button>
            `).join('');
            document.getElementById('quiz-app').innerHTML = `
                <div class="center-card">
                    <div class="progress-bar"><div class="progress" style="width:${progress}%;"></div></div>
                    <div class="question-title">${questions[current].text}</div>
                    <div class="options-slider">
                        ${leftLabel}
                        <div class="slider-radio-group">${sliderHtml}</div>
                        ${rightLabel}
                    </div>
                    <div class="btn-group" style="margin-top:24px;">
                        <button class="nav-btn" onclick="prevQuestion()" ${current === 0 ? 'disabled' : ''}>上一题</button>
                        <button class="nav-btn" onclick="nextQuestion()">${current === questions.length - 1 ? '提交' : '下一题'}</button>
                    </div>
                    <div class="error">${errorMsg}</div>
                </div>
            `;
        }
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
        function shuffleQuestions() {
    for (let i = questions.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [questions[i], questions[j]] = [questions[j], questions[i]];
    }
}
        function startTest() {
            shuffleQuestions();
            current = 0;
            answers = new Array(questions.length).fill(null);
            functions.forEach(f => userScores[f] = [0,0,0,0,0,0,0,0]);
            showQuestion();
        }
        function actuallyStartTest() {
            current = 0;
            answers = new Array(questions.length).fill(null);
            functions.forEach(f => userScores[f] = [0,0,0,0,0,0,0,0]);
            showQuestion();
        }
        function submitQuiz() {
            const funcVars = ["Ni","Ne","Si","Se","Ti","Te","Fi","Fe"];
            let funcScores = {};
            funcVars.forEach(f => {
                funcScores[f + "+"] = 0;
                funcScores[f + "-"] = 0;
            });
            answers.forEach((score, idx) => {
                if (score !== null) {
                    const q = questions[idx];
                    let key = q.func + (q.polarity === "positive" ? "+" : "-");
                    funcScores[key] += score * (q.weight || 1);
                }
            });
            const attitude = {
                "Ni+": "i", "Ni-": "i", "Ne+": "e", "Ne-": "e",
                "Si+": "i", "Si-": "i", "Se+": "e", "Se-": "e",
                "Ti+": "i", "Ti-": "i", "Te+": "e", "Te-": "e",
                "Fi+": "i", "Fi-": "i", "Fe+": "e", "Fe-": "e"
            };
            let perceptionPlus = [
                { key: "Ni+", val: funcScores["Ni+"] },
                { key: "Ne+", val: funcScores["Ne+"] },
                { key: "Si+", val: funcScores["Si+"] },
                { key: "Se+", val: funcScores["Se+"] }
            ].sort((a,b)=>b.val-a.val);
            let judgingPlus = [
                { key: "Ti+", val: funcScores["Ti+"] },
                { key: "Te+", val: funcScores["Te+"] },
                { key: "Fi+", val: funcScores["Fi+"] },
                { key: "Fe+", val: funcScores["Fe+"] }
            ].sort((a,b)=>b.val-a.val);
            let mainPer = null, mainJud = null;
            for (let p of perceptionPlus) {
                for (let j of judgingPlus) {
                    if (attitude[p.key] !== attitude[j.key]) {
                        mainPer = p;
                        mainJud = j;
                        break;
                    }
                }
                if (mainPer && mainJud) break;
            }
            if (!mainPer || !mainJud) {
                alert("无法确定主功能和辅助功能的内外倾，请检查题目设置或答题分布。");
                return;
            }
            const groupPairs = {
                "Ni+": ["Ni+","Se-"], "Se+": ["Se+","Ni-"],
                "Ne+": ["Ne+","Si-"], "Si+": ["Si+","Ne-"],
                "Ti+": ["Ti+","Fe-"], "Fe+": ["Fe+","Ti-"],
                "Fi+": ["Fi+","Te-"], "Te+": ["Te+","Fi-"]
            };
            function groupSum(pair) {
                return (funcScores[pair[0]] || 0) + (funcScores[pair[1]] || 0);
            }
            let perPair = groupPairs[mainPer.key];
            let judPair = groupPairs[mainJud.key];
            let perSum = groupSum(perPair);
            let judSum = groupSum(judPair);
            let main1, main2, main1Pair, main2Pair;
            if (perSum >= judSum) {
                main1 = mainPer.key;
                main2 = mainJud.key;
                main1Pair = perPair;
                main2Pair = judPair;
            } else {
                main1 = mainJud.key;
                main2 = mainPer.key;
                main1Pair = judPair;
                main2Pair = perPair;
            }
            let positions = Array(8).fill("");
            positions[0] = main1;
            positions[1] = main2;
            positions[3] = main1Pair[0] === main1 ? main1Pair[1] : main1Pair[0];
            positions[2] = main2Pair[0] === main2 ? main2Pair[1] : main2Pair[0];
            function getComplement(key) {
                if (key.startsWith("Ni")) return "Ne+";
                if (key.startsWith("Ne")) return "Ni+";
                if (key.startsWith("Si")) return "Se+";
                if (key.startsWith("Se")) return "Si+";
                if (key.startsWith("Ti")) return "Te+";
                if (key.startsWith("Te")) return "Ti+";
                if (key.startsWith("Fi")) return "Fe+";
                if (key.startsWith("Fe")) return "Fi+";
                return "";
            }
            positions[4] = getComplement(main1);
            positions[7] = getComplement(main2);

            // 匹配人格类型，补全5-8功能
            let mainSeq = [positions[0], positions[1], positions[2], positions[3]].map(f => f.replace(/[+-]/g, ''));
            let typeScores = [];
            for (let type in typeTable) {
                let typeFuncs = typeTable[type].slice(0, 4);
                let score = mainSeq.reduce((acc, f, i) => acc + (f === typeFuncs[i] ? 1 : 0), 0);
                typeScores.push({type, score});
            }
            typeScores.sort((a, b) => b.score - a.score);
            let top3 = typeScores.slice(0, 3);
            let bestType = top3[0]?.type;
            if (bestType) {
                let bestFuncs = typeTable[bestType];
                positions[4] = bestFuncs[4] || positions[4];
                positions[5] = bestFuncs[5] || "";
                positions[6] = bestFuncs[6] || "";
                positions[7] = bestFuncs[7] || positions[7];
            }

            let resultHtml = `
                <li>主导功能(1)：${positions[0]}</li>
                <li>辅助功能(2)：${positions[1]}</li>
                <li>第三功能(3)：${positions[2]}</li>
                <li>劣势功能(4)：${positions[3]}</li>
                <li>替补功能(5)：${positions[4]}</li>
                <li>批判功能(6)：${positions[5]}</li>
                <li>盲点功能(7)：${positions[6]}</li>
                <li>魔鬼功能(8)：${positions[7]}</li>
            `;
            let maxScore = Math.max(...Object.values(funcScores));
            let scoreHtml = Object.entries(funcScores).map(([k, v]) => {
                let barWidth = maxScore > 0 ? Math.round((v / maxScore) * 240) : 0;
                return `
                    <div class="bar-chart-row">
                        <span class="bar-label">${k}</span>
                        <div class="bar-bg">
                            <div class="bar-inner" style="width:${barWidth}px"></div>
                        </div>
                        <span class="bar-value">${v}</span>
                    </div>
                `;
            }).join('');
            let typeHtml = `<p style="color:#ffe7ba;">最有可能的人格类型：</p><ul>${top3.map(t=>`<li><b>${t.type}</b> 匹配分：${t.score}/4</li>`).join('')}</ul>`;
            document.getElementById('quiz-app').innerHTML = `
    <div class="center-card" style="max-width:1100px;display:flex;flex-direction:row;justify-content:space-between;gap:32px;">
        <div style="flex:1;min-width:220px;">
            <div class="result-title">人格类型</div>
            ${typeHtml}
        </div>
        <div style="flex:1.1;min-width:220px;">
            <div class="result-title">主序列</div>
            <ul>${resultHtml}</ul>
        </div>
        <div style="flex:1.5;min-width:260px;">
            <div class="result-title">各变量得分</div>
            <div>${scoreHtml}</div>
        </div>
    </div>
    <div style="text-align:center;margin-top:32px;">
        <button class="start-btn" onclick="renderHome()">返回首页</button>
    </div>
`;
        }
        renderHome();
    </script>
</body>
</html>
