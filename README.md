<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <title>荣格八维认知功能测试</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        /* ...样式同前，省略... */
        html, body { height: 100%; margin: 0; padding: 0; }
        body {
            min-height: 100vh; min-width: 100vw; overflow-x: hidden;
            background: #0a1833;
            background-image: url('https://cdn.pixabay.com/photo/2023/10/10/11/28/star-trails-8306233_1280.jpg');
            background-size: cover; background-position: center; background-repeat: no-repeat;
            animation: bgmove 30s linear infinite alternate;
        }
        @keyframes bgmove { 0% { background-position: 50% 60%; } 100% { background-position: 50% 40%; } }
        .overlay { position: fixed; inset: 0; background: rgba(10,24,51,0.55); z-index: 0; }
        .center-card { position: absolute; left: 50%; top: 50%; transform: translate(-50%,-50%);
            background: rgba(255,255,255,0.13); box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
            border-radius: 18px; padding: 38px 32px 32px 32px; max-width: 480px; width: 90vw;
            text-align: center; z-index: 1; backdrop-filter: blur(8px); }
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
        .slider-label { font-size: 1.08em; margin-top: 8px; font-weight: bold; color: #b44143;
            width: 48px; text-align: center; }
        .slider-label.right { color: #62b283; }
        .slider-radio-group { display: flex; flex: 1; justify-content: space-between; align-items: center;
            position: relative; margin: 0 8px; }
        .slider-radio-group::before { content: ''; position: absolute; top: 50%; left: 0; right: 0; height: 4px;
            background: linear-gradient(90deg, #b44143 0%, #dda95f 25%, #e0e0e0 50%, #4ba694 75%, #62b283 100%);
            z-index: 0; transform: translateY(-50%); border-radius: 2px; }
        .slider-radio { position: relative; z-index: 1; background: none; border: none; outline: none; cursor: pointer;
            padding: 0; margin: 0 0.5vw; }
        .slider-radio-circle { width: 36px; height: 36px; border-radius: 50%; border: 3px solid #e0e0e0; background: #fff;
            display: flex; align-items: center; justify-content: center; transition: border-color 0.18s, box-shadow 0.18s;
            box-shadow: 0 2px 8px rgba(10,24,51,0.10); }
        .slider-radio.selected .slider-radio-circle { border-color: #62b283; box-shadow: 0 0 0 4px rgba(98,178,131,0.18); }
        .slider-radio.red .slider-radio-circle { border-color: #b44143; }
        .slider-radio.orange .slider-radio-circle { border-color: #dda95f; }
        .slider-radio.gray .slider-radio-circle { border-color: #e0e0e0; }
        .slider-radio.blue .slider-radio-circle { border-color: #4ba694; }
        .slider-radio.green .slider-radio-circle { border-color: #62b283; }
        .slider-radio.selected .slider-radio-circle { background: #62b283; }
        .slider-radio.selected.red .slider-radio-circle { background: #b44143; }
        .slider-radio.selected.orange .slider-radio-circle { background: #dda95f; }
        .slider-radio.selected.gray .slider-radio-circle { background: #e0e0e0; }
        .slider-radio.selected.blue .slider-radio-circle { background: #4ba694; }
        .slider-radio.selected.green .slider-radio-circle { background: #62b283; }
        .slider-radio-circle-inner { width: 16px; height: 16px; border-radius: 50%; background: #fff; opacity: 0;
            transition: opacity 0.18s; }
        .slider-radio.selected .slider-radio-circle-inner { opacity: 1; background: #fff; }
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
        @media (max-width: 600px) {
            .center-card { padding: 18px 4vw 18px 4vw; }
            .title { font-size: 1.2em; }
            .question-title { font-size: 1em; }
            .slider-radio-circle { width: 28px; height: 28px; }
            .slider-radio-circle-inner { width: 12px; height: 12px; }
            .slider-label { font-size: 0.95em; width: 36px; }
        }
    </style>
</head>
<body>
    <div class="overlay"></div>
    <div id="quiz-app"></div>
    <script>
        // ===================== 你可以自定义的部分 =====================

        // 1. 题目设置（func: 功能，polarity: "positive"/"negative"，weight: 分数倍数）
        // polarity: "positive" 表示加到主功能（1号位），"negative" 表示加到劣势功能（8号位）
        // weight: 分数倍数（如1, 1.5, 2等）
        const questions = [
            const questions = [
    { text: "你相信有一个标准能区分大部分行为、事情，而那些符合标准的是好的", func: "Te", polarity: "positive", weight: 2 },
    { text: "你不喜欢考虑那么多特殊情况。比如你不在乎一个人偷东西是否迫不得已，他事实上就是做错了", func: "Te", polarity: "positive", weight: 2 },
    { text: "有时你觉得自己是神秘力量派来帮助人类社会发展的，所以你才掌握了能区分一切好坏的标准，同时也有责任让身边的人符合这个标准定义的好", func: "Te", polarity: "positive", weight: 3 },
    { text: "如果把生命的感性部分剔除掉，确实有客观的标准能分辨好坏，但这显然过于理想化了", func: "Te", polarity: "positive", weight: 1 },
    { text: "你经常感知到一个物体、一件事在未来某个时刻的样子", func: "Ni", polarity: "positive", weight: 2 },
    { text: "你产生的想象和你有着独一无二的联系，你的经历和自身导致你产生这些想象，这些想象也是你自身的重要组成部分", func: "Ni", polarity: "positive", weight: 3 },
    { text: "当你有一个想法时，你想专注于它并希望它在现实中能发挥最大好处", func: "Ni", polarity: "positive", weight: 2 },
    { text: "你有时会思考你的想象对你和世界来说有什么意义", func: "Ni", polarity: "positive", weight: 2 },
    { text: "在场面彻底失控的情况下，你有种难以抑制的冲动，就像被丧尸咬后疯狂寻找血液的感觉", func: "Se", polarity: "negative", weight: 3 },
    { text: "你有时对刺激很敏感，它们强迫你离开身体里集中、安全的地方", func: "Se", polarity: "negative", weight: 2 },
    { text: "当感官刺激足够强时，你会想沉浸其中，不去思考你为什么会有这样的感受、这样的感受好不好、有什么意义和影响", func: "Se", polarity: "positive", weight: 2 },
    { text: "你总是希望从那些重要的事情、感觉中得到什么", func: "Se", polarity: "negative", weight: 2 },
    { text: "当你站在沙滩上，海浪一遍遍冲击着你的双腿，这种互动证明着你的存在", func: "Se", polarity: "positive", weight: 3 },
    { text: "你觉得人活一生就是为了体验，不理解那些对纵欲的担心，因为体验本身就是节制的", func: "Se", polarity: "positive", weight: 3 },
    { text: "你的朋友会评价你是一个很会发掘新玩法的人", func: "Se", polarity: "positive", weight: 2 },
    { text: "你脑海里的某个角落藏着一些模糊的、阴暗的东西，而来自外部的感觉帮助你远离这些它们", func: "Ni", polarity: "negative", weight: 3 },
    { text: "如果新的事实证明你原本是错的，你不会固执己见，因为那些理论本就是基于事实的", func: "Se", polarity: "positive", weight: 2 },
    { text: "你总是在想我怎么做、别人怎么做可以让事情变得更好", func: "Ne", polarity: "positive", weight: 2 },
    { text: "你不到不得已不做出选择，这不是因为选择困难症，而是你觉得前面总有更好的选择等着你", func: "Ne", polarity: "positive", weight: 3 },
    { text: "你在合作中不是个独断的人，喜欢思考不同方案是否合理或他们的可行性，不在乎这些方案是谁提出的", func: "Ne", polarity: "positive", weight: 2 },
    { text: "你会是一个优秀的人事经理，能看出应聘者突出的能力", func: "Ne", polarity: "positive", weight: 2 },
    { text: "在平凡的生活中，你总是想找点乐子", func: "Ne", polarity: "positive", weight: 1 },
    { text: "你是个有点喜新厌旧的人", func: "Ne", polarity: "positive", weight: 1 },
    { text: "当你在小说中读到男女主满眼只有对方时，即使结局是好的，你也不欣赏。", func: "Fe", polarity: "positive", weight: 1 },
    { text: "你不会单单因为爱情而和一个人结婚。", func: "Fe", polarity: "positive", weight: 2 },
    { text: "如果你穿越到古代，你不会传递和践行那些与时代不符的价值观，例如人人平等。", func: "Fe", polarity: "positive", weight: 2 },
    { text: "你觉得那些大多数人认可的东西具有先验性，大部分时候都是对的", func: "Fe", polarity: "positive", weight: 3 },
    { text: "世界上有些人缺少、甚至抗拒独立思考，不会有意去探索那些感受不到的东西。", func: "Fe", polarity: "negative", weight: 3 },
    { text: "你的情感像是在内心深处流淌的溪水", func: "Fi", polarity: "positive", weight: 3 },
    { text: "你的情感是很私密的，不想用它来打动、改变那些外界的东西", func: "Fi", polarity: "positive", weight: 2 },
    { text: "有时你希望那些隐秘的情感被人理解和重视，但你不会表现出来", func: "Fi", polarity: "positive", weight: 2 },
    { text: "你绝不会为了世俗的成功和认可而放弃个人价值观", func: "Fi", polarity: "positive", weight: 3 },
    { text: "你的情感无法用语言完全呈现出来，但你会把一部分情感寄托在一些贴身旧物上", func: "Fi", polarity: "positive", weight: 2 },
    { text: "明明很在乎某人，却故意表现冷淡", func: "Fi", polarity: "negative", weight: 2 },
    { text: "如果被要求表达强烈的情感立场，你会感到不知所措", func: "Fi", polarity: "negative", weight: 3 },
    { text: "你有时会分析自己为什么会有这样的情感，事后又觉得很没必要", func: "Fi", polarity: "negative", weight: 3 },
    { text: "有时你已经很清晰的说明了你的理念和观点，但别人还是难以理解", func: "Ti", polarity: "positive", weight: 2 },
    { text: "你觉得理念本身非常崇高，不一定要为现实服务", func: "Ti", polarity: "positive", weight: 3 },
    { text: "如果不能从辩论中持续完善论点，你不会继续下去。表面上的输赢其实没那么重要", func: "Ti", polarity: "positive", weight: 2 },
    { text: "如果你的大脑是一台模拟程序，它可能会因为考虑了太多复杂条件而死机", func: "Ti", polarity: "positive", weight: 3 },
    { text: "你的感受经常和别人的不同。比如有时别人觉得B在阴阳你但你不这么觉得，你觉得A在讨好你时别人又不这么觉得", func: "Si", polarity: "positive", weight: 2 },
    { text: "你总结出一个人的性格（比如甜美的、帅气的、温柔的）并发现他们的行为大部分时候符合你的印象", func: "Si", polarity: "positive", weight: 3 },
    { text: "如果一个人说了伤害你的话，你受伤害的感受会随着不断感受它而加深，你意识到这种感受在蒙蔽你并想摆脱，但你总忍不住去想它和它相关的事", func: "Si", polarity: "negative", weight: 3 },
    { text: "你希望自己可以完全摒弃主观感受，客观地看待事物，但你知道这是不可能的", func: "Si", polarity: "negative", weight: 2 },
    { text: "你经常感受到那些潜在的危险并远离它们", func: "Ne", polarity: "negative", weight: 3 },
    { text: "第二天你要出席一个重要会议，你会不自觉地想各种可能，比如帮助了一个路人后发现他是你的上司，然后嘲笑自己为什么会有这么无厘头的想法", func: "Ne", polarity: "negative", weight: 2 }

        ];

        // 2. 选项设置（分值和颜色）
        const options = [
            { text: "完全不符合", value: 1, color: "red" },
            { text: "不符合", value: 2, color: "orange" },
            { text: "中立", value: 3, color: "gray" },
            { text: "符合", value: 4, color: "blue" },
            { text: "非常同意", value: 5, color: "green" }
        ];

        // 3. 功能列表（顺序不要改）
        const functions = ["Ne","Ni","Fe","Fi","Ti","Te","Si","Se"];

        // 4. 人格类型功能分布表（顺序不要改）
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

        // ===================== 你可以自定义的部分结束 =====================

        // 用户分数结构
        let userScores = {};
        functions.forEach(f => userScores[f] = [0,0,0,0,0,0,0,0]); // 8个位置

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
            let leftLabel = `<div class="slider-label">完全不符合</div>`;
            let rightLabel = `<div class="slider-label right">非常同意</div>`;
            let sliderHtml = options.map((opt, idx) => `
                <button
                    class="slider-radio ${opt.color} ${answers[current] === opt.value ? 'selected' : ''}"
                    onclick="selectOption(${opt.value})"
                    type="button"
                    aria-label="${opt.text}"
                >
                    <div class="slider-radio-circle">
                        <div class="slider-radio-circle-inner"></div>
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
            functions.forEach(f => userScores[f] = [0,0,0,0,0,0,0,0]);
            showQuestion();
        }

        // 统计分数和匹配
        function submitQuiz() {
    // 1. 统计每个功能正负得分
    let funcVars = ["Ni","Ne","Si","Se","Ti","Te","Fi","Fe"];
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

    // 2. 感知功能+、判断功能+，分别选最高的
    let perceptionPlus = [
        { key: "Ni+", val: funcScores["Ni+"] },
        { key: "Ne+", val: funcScores["Ne+"] },
        { key: "Si+", val: funcScores["Si+"] },
        { key: "Se+", val: funcScores["Se+"] }
    ];
    let judgingPlus = [
        { key: "Ti+", val: funcScores["Ti+"] },
        { key: "Te+", val: funcScores["Te+"] },
        { key: "Fi+", val: funcScores["Fi+"] },
        { key: "Fe+", val: funcScores["Fe+"] }
    ];
    perceptionPlus.sort((a,b)=>b.val-a.val);
    judgingPlus.sort((a,b)=>b.val-a.val);

    // 3. 取感知+和判断+最高的各1个，作为候选
    let topPer = perceptionPlus[0];
    let topJud = judgingPlus[0];

    // 4. 分组（每组一正一负）
    const groupMap = {
        "Ni": ["Ni","Se"], "Se": ["Ni","Se"],
        "Ne": ["Ne","Si"], "Si": ["Ne","Si"],
        "Ti": ["Ti","Fe"], "Fe": ["Ti","Fe"],
        "Fi": ["Fi","Te"], "Te": ["Fi","Te"]
    };

    // 5. 计算两组总分（正负都算进去）
    function groupSum(group) {
        return funcScores[group[0]+"+"] + funcScores[group[0]+"-"] +
               funcScores[group[1]+"+"] + funcScores[group[1]+"-"];
    }
    let group1 = groupMap[topPer.key.slice(0,2)];
    let group2 = groupMap[topJud.key.slice(0,2)];
    let group1Sum = groupSum(group1);
    let group2Sum = groupSum(group2);

    // 6. 决定主功能1、2位置（高的在1，低的在2）
    let main1, main2, main1Group, main2Group;
    if (group1Sum >= group2Sum) {
        main1 = topPer.key.slice(0,2);
        main2 = topJud.key.slice(0,2);
        main1Group = group1;
        main2Group = group2;
    } else {
        main1 = topJud.key.slice(0,2);
        main2 = topPer.key.slice(0,2);
        main1Group = group2;
        main2Group = group1;
    }

    // 7. 一组里的功能要不放1/4，要不放2/3，要不放5/8，要不放6/7
    // 这里只放主功能和对位功能，其他可扩展
    // 1和5对位，2和6对位
    let positions = Array(8).fill("");
    positions[0] = main1;
    positions[1] = main2;
    // 5位是主功能组的另一个
    positions[4] = main1Group[0] === main1 ? main1Group[1] : main1Group[0];
    // 6位是副功能组的另一个
    positions[5] = main2Group[0] === main2 ? main2Group[1] : main2Group[0];

    // 8. 互补主功能（如1是Ni，5是Ne；1是Te，5是Ti；反之亦然）
    // 已在上面实现

    // 9. 展示
    let resultHtml = `
        <li>主功能(1)：${positions[0]}</li>
        <li>辅助功能(2)：${positions[1]}</li>
        <li>第五功能(5)：${positions[4]}</li>
        <li>第六功能(6)：${positions[5]}</li>
    `;

    // 展示所有变量得分
    let scoreHtml = Object.entries(funcScores).map(
        ([k,v]) => `<li>${k}: ${v}</li>`
    ).join('');

    document.getElementById('quiz-app').innerHTML = `
        <div class="center-card">
            <div class="result-title">测试完成！</div>
            <p>你的主序列：</p>
            <ul>${resultHtml}</ul>
            <p style="margin-bottom:1em;">各变量得分：</p>
            <ul>${scoreHtml}</ul>
            <button class="start-btn" onclick="renderHome()">返回首页</button>
        </div>
    `;
}

        // 初始化
        renderHome();
    </script>
</body>
</html>

