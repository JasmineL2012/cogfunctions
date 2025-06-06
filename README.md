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
            margin: 36px 0 18px 0; gap: 10px; }
        .slider-label {
            font-size: 1.08em; margin-top: 8px; font-weight: bold;
            width: 48px; text-align: center; letter-spacing: 2px;
            background: rgba(255,255,255,0.13);
            border-radius: 10px;
            padding: 4px 0;
            box-shadow: 0 2px 8px 0 rgba(31,38,135,0.07);
        }
        .slider-label.right { color: #7cdda4; }
        .slider-label { color: #e26567; }
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
            background: transparent;
            border-radius: 50%;
            min-width: 25px;
            min-height: 25px;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 2px 12px 0 rgba(31,38,135,0.10);
            transition: background transparent;
            border: 10px solid rgba(255,255,255,0.18);
        }

        .slider-radio-group {
           display: flex; flex: 1; justify-content: space-between; align-items: center;
           position: relative; margin: 0 8px;
           gap: 50px;
        }
        
        .slider-radio.selected .slider-radio-inner {
            background: rgb(219, 219, 125);
            box-shadow: 0 0 0 4px rgba(98, 127, 178, 0.18);
            border: 5px solid #ffe7ba;
        }

        .slider-radio .slider-radio-circle-inner {
            width: 14px; height: 14px; border-radius: 50%; background: #fff; opacity: 0;
            transition: opacity 0.18s;
        }
        .slider-radio.selected .slider-radio-circle-inner {
            opacity: 1; background: #d5d4b5;
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
        .progress { height: 100%; background: white;
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
        const questions = [
    // 外倾思维Te
    { text: "我相信有一个标准能区分大部分行为、事情，而那些符合标准的是好的", func: "Te", polarity: "positive", weight: 2 },
    { text: "我不在乎一个人偷东西是否迫不得已，他事实上就是做错了", func: "Te", polarity: "positive", weight: 2 },
    { text: "我有种使命感让身边的人符合客观标准定义的好", func: "Te", polarity: "positive", weight: 2 },
    { text: "我想从大量事实中得到具有普适性的规律", func: "Te", polarity: "positive", weight: 2 },
    { text: "我会选择成果稳定可以量化的，而不是机会大风险也大的", func: "Te", polarity: "positive", weight: 2 },
    
    { text: "我从不用统一准则来评判别人的生活方式，因为萝卜青菜各有所爱", func: "Te", polarity: "negative", weight: 2 },
    { text: "如果把生命的感性部分剔除掉，可能有客观的标准能分辨好坏，但这显然不太可能", func: "Te", polarity: "negative", weight: 2 },
    { text: "我的创造不需要用外部标准来衡量，但有时我会用外部标准衡量别人产生的价值", func: "Te", polarity: "negative", weight: 2 },
    { text: "我觉得有些人过于执着于客观标准，忽略了人性和情感的复杂性", func: "Te", polarity: "negative", weight: 2 },
    { text: "我不喜欢外界标准的限制，但有时希望我的选择能得到它的认可", func: "Te", polarity: "negative", weight: 2 },

    // 内倾直觉Ni
    { text: "我经常感知到一个物体、一件事在未来某个时刻的样子", func: "Ni", polarity: "positive", weight: 2 },
    { text: "我和我的想象有着独一无二的联系，我的经历导致这些想象的产生，这些想象也是我自身的重要组成部分", func: "Ni", polarity: "positive", weight: 2 },
    { text: "我有时会思考我的想象对我和世界来说有什么意义", func: "Ni", polarity: "positive", weight: 2 },
    { text: "当我有一个想法时，我想专注于它并希望它在现实中能发挥最大好处", func: "Ni", polarity: "positive", weight: 2 },
    { text: "我经常在零碎的细节中感知到一些趋势", func: "Ni", polarity: "positive", weight: 2 },

    { text: "我有过一种强烈的“预感”某件坏事会发生，并因此提前作出了规避行为", func: "Ni", polarity: "negative", weight: 2 },
    { text: "有时我会因为感知自己的失败而提前放弃努力", func: "Ni", polarity: "negative", weight: 2 },
    { text: "我觉得人生已注定走向特定的结局，选择改变不了什么", func: "Ni", polarity: "negative", weight: 2 },
    { text: "有时我会快速下结论否定一个人或群体，抗拒进一步了解和交流", func: "Ni", polarity: "negative", weight: 2 },
    { text: "我坚信眼见为实，很少耗费精力思考事物的发展趋势", func: "Ni", polarity: "negative", weight: 2 },

    // 内倾感觉Si
    { text: "我的感受经常和别人的不同，比如有时别人觉得一个人在阴阳你但我不这么觉得", func: "Si", polarity: "positive", weight: 2 },
    { text: "我发现一个人的行为大部分时候符合你的印象", func: "Si", polarity: "positive", weight: 2 },
    { text: "我去某些从未去过的地方有种莫名的熟悉感，可能因为我经常读类似背景的小说", func: "Si", polarity: "positive", weight: 2 },
    { text: "生活环境决定了人看待事物的角度", func: "Si", polarity: "positive", weight: 2 },
    { text: "我可以很容易说出什么颜色、什么动物能代表一个朋友", func: "Si", polarity: "positive", weight: 2 },

    { text: "如果一个人说了伤害我的话，我受伤害的感受会随着不断感受它而加深，这种感受在蒙蔽我，但我总忍不住去想和它相关的事", func: "Si", polarity: "negative", weight: 2 },
    { text: "我希望自己可以完全摒弃主观感受，客观地感受事物的存在，但这不太可能", func: "Si", polarity: "negative", weight: 2 },
    { text: "我有一些难以解释的偏好或排斥，比如讨厌某种颜色组合。说不上来理由但很坚持", func: "Si", polarity: "negative", weight: 2 },
    { text: "我觉得别人描述的感受太主观了，只有亲身经历过才真实", func: "Si", polarity: "negative", weight: 2 },

    // 外倾感觉Se
    { text: "我觉得人活一生就是为了体验，很少担心过度纵欲", func: "Se", polarity: "positive", weight: 2 },
    { text: "我的朋友会评价我是一个很会发掘新玩法的人", func: "Se", polarity: "positive", weight: 2 },
    { text: "如果无法想通一件事，我会很快投入到新刺激中转移注意力", func: "Se", polarity: "positive", weight: 2 },
    { text: "我喜欢沉浸在感官刺激中，不去想我的感受是什么", func: "Se", polarity: "positive", weight: 2 },
    { text: "实实在在的感受是我内在体系的重要组成部分", func: "Se", polarity: "positive", weight: 2 },

    { text: "在场面彻底失控的情况下，我有种破罐子破摔的冲动", func: "Se", polarity: "negative", weight: 2 },
    { text: "在嘈杂的环境中工作，我会感到难以集中注意力", func: "Se", polarity: "negative", weight: 2 },
    { text: "我经常想自己是不是错过了一些关键信息", func: "Se", polarity: "negative", weight: 2 },
    { text: "那些只接收信息而不主动思考的人太肤浅了", func: "Se", polarity: "negative", weight: 2 },
    { text: "有时我很想永远停留在此时此刻，不去面对将来的未知数", func: "Se", polarity: "negative", weight: 2 },

    // 外倾直觉Ne
    { text: "我不到不得已不做出选择，这不是因为选择困难症，而是前面总有更好的选择", func: "Ne", polarity: "positive", weight: 2 },
    { text: "在合作中有人提出了新方案，我总是认真考虑，不在乎方案由谁提出", func: "Ne", polarity: "positive", weight: 2 },
    { text: "我会是一个优秀的人事经理，能看出应聘者的潜能", func: "Ne", polarity: "positive", weight: 2 },
    { text: "我不满足于平凡的生活，总想找点乐子", func: "Ne", polarity: "positive", weight: 2 },
    { text: "我脑海里有很多疯狂的想法，但不会真的这么做", func: "Ne", polarity: "positive", weight: 2 },

    { text: "我经常感受到那些潜在的危险并远离它们", func: "Ne", polarity: "negative", weight: 2 },
    { text: "第二天我出席一个重要会议，我会不自觉地想各种可能，然后嘲笑自己为什么会有这么无厘头的想法", func: "Ne", polarity: "negative", weight: 2 },
    { text: "面对太多可能时我会感到不知所措，会想选错了会怎么样", func: "Ne", polarity: "negative", weight: 2 },
    { text: "我有很多想法但不会贸然把它们带到现实中", func: "Ne", polarity: "negative", weight: 2 },
    { text: "我总觉得还有很多更好的可能性，但不知道具体是什么", func: "Ne", polarity: "negative", weight: 2 },

    // 外倾情感Fe
{ text: "我常以温和的态度示人，也希望人们能互相理解和尊重", func: "Fe", polarity: "positive", weight: 3 },
{ text: "如果我穿越到古代，我不会传递那些与时代不符的价值观，例如人人平等。", func: "Fe", polarity: "positive", weight: 1 },
{ text: "我觉得那些大多数人认可的东西具有先验性，大部分时候都是对的", func: "Fe", polarity: "positive", weight: 3 },
{ text: "我认为要在恰当的时候表达恰当的情感，比如葬礼应该肃穆", func: "Fe", polarity: "positive", weight: 2 },
{ text: "帮助他人是我实现自我的方式", func: "Fe", polarity: "positive", weight: 2 },
{ text: "我对感知自己在群体中的位置、人与人之间的亲密程度比较敏感", func: "Fe", polarity: "positive", weight: 2 },
{ text: "世界上有些人缺少、甚至抗拒独立思考，不会有意去探索那些感受不到的东西。", func: "Fe", polarity: "negative", weight: 3 },
{ text: "我有时会梦到和身边的人产生冲突，并发觉现实中确实有这样的倾向", func: "Fe", polarity: "negative", weight: 2 },
{ text: "我觉得“我是谁”和“我应该成为谁”之间的界限很模糊", func: "Fe", polarity: "negative", weight: 2 },
{ text: "我融入不了群体可能是我哪里出了问题", func: "Fe", polarity: "negative", weight: 2 },
{ text: "有人说我在自己在意的群体里会表现得不太自然", func: "Fe", polarity: "negative", weight: 2 },

    // 内倾情感Fi
    // ...existing code...

    // 内倾情感Fi
    { text: "我的情感是很私密的，不想用它来打动、改变那些外界的东西", func: "Fi", polarity: "positive", weight: 2 },
    { text: "我不会为了世俗的成功和认可而放弃个人价值观", func: "Fi", polarity: "positive", weight: 3 },
    { text: "我的理智会选择情感，但我的情感不会选择理智", func: "Fi", polarity: "positive", weight: 2 },
    { text: "我最想要的是具备自己认可的价值", func: "Fi", polarity: "positive", weight: 2 },
    { text: "看电影时我会把自己代入到角色中思考", func: "Fi", polarity: "positive", weight: 2 },
    { text: "有时我希望那些隐秘的情感被人理解和重视", func: "Fi", polarity: "positive", weight: 1 },

    { text: "有时我明明很在乎某人，却故意表现冷淡", func: "Fi", polarity: "negative", weight: 2 },
    { text: "如果被要求表达强烈的情感立场，我会感到不知所措", func: "Fi", polarity: "negative", weight: 3 },
    { text: "我有时会分析自己为什么会有这样的情感，事后又觉得很没必要", func: "Fi", polarity: "negative", weight: 2 },
    { text: "我理解某些选择的思考过程，但我不想尊重它们", func: "Fi", polarity: "negative", weight: 2 },

// ...existing code...

    // 内倾思维Ti
    // ...existing code...

    // 内倾思维Ti
    { text: "我认为理念本身非常崇高，不一定要为现实服务", func: "Ti", polarity: "positive", weight: 3 },
    { text: "如果不能从辩论中持续完善论点，我不会继续浪费时间", func: "Ti", polarity: "positive", weight: 2 },
    { text: "和别人辩论时，我经常问“你对a的理解是xxx吗？”", func: "Ti", polarity: "positive", weight: 2 },
    { text: "学习新知识时，我总是自己想很多问题并觉得自己已经想通了", func: "Ti", polarity: "positive", weight: 2 },
    { text: "看到别人的反常行为会忍不住想“他为什么这么说/做”", func: "Ti", polarity: "positive", weight: 2 },

    { text: "我对理念有清晰的了解，但有条理地向外界展示自己的推理过程有点困难", func: "Ti", polarity: "negative", weight: 2 },
    { text: "我对自己的理念缺乏确定性，经常觉得考虑的还不够完善", func: "Ti", polarity: "negative", weight: 3 },
    { text: "我知道别人的逻辑漏洞在哪，但我不想指出让气氛变差，所以我不想了", func: "Ti", polarity: "negative", weight: 2 },
    { text: "在思考问题时，我会因为考虑了太多复杂情况而觉得很混乱", func: "Ti", polarity: "negative", weight: 2 },
    { text: "有时和朋友聊天时会各说各话，得出结论才发现逻辑起点竟然不一样", func: "Ti", polarity: "negative", weight: 2 },

// ...existing code...
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
    // 不要自动提交，最后一题也只是刷新选中状态
    if (current < questions.length - 1) {
        current++;
        showQuestion();
    } else {
        // 只是刷新选中状态，不自动提交
        showQuestion();
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

    // 匹配人格类型
    let mainSeq = [positions[0], positions[1], positions[2], positions[3]].map(f => f.replace(/[+-]/g, ''));
    let typeScores = [];
    for (let type in typeTable) {
        let typeFuncs = typeTable[type].slice(0, 4);
        let score = mainSeq.reduce((acc, f, i) => acc + (f === typeFuncs[i] ? 1 : 0), 0);
        typeScores.push({type, score});
    }
    typeScores.sort((a, b) => b.score - a.score);
    let bestType = typeScores[0]?.type;

    // 类型描述
    const typeDescriptions = {
        INTJ: "富有远见、善于规划，喜欢独立思考和系统性分析，追求高效和创新。",
        INTP: "逻辑严密、思想开放，喜欢探索理论和原理，追求真理和独立见解。",
        ENTJ: "果断自信、善于领导，擅长制定战略和组织资源，追求目标和成就。",
        ENTP: "机智灵活、善于创新，喜欢挑战常规和提出新观点，乐于辩论和探索。",
        INFJ: "富有洞察力、关怀他人，注重价值观和意义，善于理解他人情感。",
        INFP: "理想主义、富有同情心，重视内心价值和独特性，追求和谐与自我实现。",
        ENFP: "热情开放、富有创造力，喜欢探索新可能，重视人际关系和个人成长。",
        ENFJ: "善于沟通、关心他人，擅长激励和引导团队，重视集体和社会价值。",
        ISTJ: "务实可靠、注重细节，喜欢有序和规则，重视责任和承诺。",
        ISFJ: "体贴周到、乐于助人，注重传统和安全，善于照顾他人。",
        ESTJ: "组织能力强、注重效率，喜欢管理和执行，重视规则和秩序。",
        ESFJ: "友善合群、乐于服务，重视人际关系和团队合作，善于协调和支持。",
        ESTP: "行动力强、适应力高，喜欢冒险和挑战，善于解决实际问题。",
        ESFP: "热情外向、乐于体验，喜欢享受生活和与人互动，重视当下和感受。",
        ISTP: "冷静理性、动手能力强，喜欢分析和解决实际问题，适应变化。",
        ISFP: "温和敏感、追求自由，重视个人体验和美感，喜欢随性而为。"
    };

let typeFuncs = bestType ? typeTable[bestType] : [];

// 感知功能和判断功能分组
const perceptionFuncs = ["Se", "Si", "Ni", "Ne"];
const judgingFuncs = ["Te", "Ti", "Fe", "Fi"];

// 计算所有正负极的最大绝对值，用于统一比例
const allFuncs = [...perceptionFuncs, ...judgingFuncs];
const maxAbs = Math.max(
    ...allFuncs.map(f => Math.abs(funcScores[f + "+"])),
    ...allFuncs.map(f => Math.abs(funcScores[f + "-"])),
    1
);

function renderFuncBar(func) {
    const neg = funcScores[func + "-"];
    const pos = funcScores[func + "+"];
    const negWidth = Math.round((Math.abs(neg) / maxAbs) * 140);
    const posWidth = Math.round((Math.abs(pos) / maxAbs) * 140);
    return `
        <div style="display:flex;align-items:center;margin:6px 0;">
            <div style="width:48px;min-width:48px;max-width:48px;text-align:right;font-weight:bold;color:#ffe7ba;font-size:1.12em;letter-spacing:1px;">
                ${func}
            </div>
            <div style="display:flex;flex-direction:column;align-items:flex-start;flex:1;margin-left:12px;">
                <div style="display:flex;align-items:center;margin-bottom:2px;">
                    <div style="width:${posWidth}px;height:18px;background:#7cdda4;border-radius:9px;transition:width 0.3s;"></div>
                    <span style="margin-left:10px;color:#7cdda4;font-weight:bold;font-size:1.08em;">
                        ${pos !== 0 ? '+' + pos : ''}
                    </span>
                </div>
                <div style="display:flex;align-items:center;">
                    <div style="width:${negWidth}px;height:18px;background:#e26567;border-radius:9px;transition:width 0.3s;"></div>
                    <span style="margin-left:10px;color:#e26567;font-weight:bold;font-size:1.08em;">
                        ${neg !== 0 ? '-' + Math.abs(neg) : ''}
                    </span>
                </div>
            </div>
        </div>
    `;
}

let funcScoreHtml = `
    <div style="margin:1.5em 0 1em 0;">
        <div style="color:#ffe7ba;font-weight:bold;margin-bottom:0.5em;">感知功能</div>
        <div style="display:flex;align-items:center;font-size:0.98em;color:#ffe7ba;margin-bottom:4px;">
            <div style="width:54px;min-width:54px;max-width:54px;text-align:right;"></div>
            <div style="flex:1;display:flex;justify-content:center;align-items:center;">
                <span style="flex:0 0 200px;text-align:center;"></span>
            </div>
        </div>
        <div style="background:rgba(255,255,255,0.08);border-radius:10px;padding:12px 8px;">
            ${perceptionFuncs.map(f => renderFuncBar(f)).join('')}
        </div>
        <div style="color:#ffe7ba;font-weight:bold;margin:1.2em 0 0.5em 0;">判断功能</div>
        <div style="display:flex;align-items:center;font-size:0.98em;color:#ffe7ba;margin-bottom:4px;">
            <div style="width:54px;min-width:54px;max-width:54px;text-align:right;"></div>
            <div style="flex:1;display:flex;justify-content:center;align-items:center;">
                <span style="flex:0 0 200px;text-align:center;"></span>
            </div>
        </div>
        <div style="background:rgba(255,255,255,0.08);border-radius:10px;padding:12px 8px;">
            ${judgingFuncs.map(f => renderFuncBar(f)).join('')}
        </div>
    </div>
`;
    // 替换 funcOrderHtml 相关部分

// 计算每个功能的总和（正+负）
let funcTotals = {};
funcVars.forEach(f => {
    funcTotals[f] = (funcScores[f + "+"] || 0) + (funcScores[f + "-"] || 0);
});
const maxTotal = Math.max(...Object.values(funcTotals).map(Math.abs), 1);

// 生成功能方框
// 替换 funcOrderHtml 相关部分
function renderFuncBox(func, idx) {
    // 颜色深浅，正负都用同一色系，数值越大越深
    const total = funcTotals[func] ?? 0;
    const baseColor = "#E6E6FA";
    const deepColor = "#4B0082";
    const percent = Math.min(Math.abs(total) / maxTotal, 1);
    function lerpColor(a, b, t) {
        function hex2rgb(hex) {
            hex = hex.replace("#", "");
            return [0, 2, 4].map(i => parseInt(hex.substr(i, 2), 16));
        }
        function rgb2hex(rgb) {
            return "#" + rgb.map(x => x.toString(16).padStart(2, "0")).join("");
        }
        const rgbA = hex2rgb(a), rgbB = hex2rgb(b);
        const rgb = rgbA.map((x, i) => Math.round(x + (rgbB[i] - x) * t));
        return rgb2hex(rgb);
    }
    const bgColor = lerpColor(baseColor, deepColor, percent);
    const labelArr = ["主导功能", "辅助功能", "第三功能", "劣势功能", "替补功能", "批判功能", "盲点功能", "魔鬼功能"];
    return `
        <div style="
            display:flex;flex-direction:column;align-items:center;justify-content:center;
            width:84px;height:64px;margin:8px;
            background:${bgColor};
            border-radius:12px;
            box-shadow:0 2px 8px 0 rgba(31,38,135,0.10);
            font-weight:bold;
            color:#0a1833;
            font-size:1.12em;
            border:2px solid #ffe7ba;
            position:relative;
        ">
            <div style="font-size:0.98em;opacity:0.7;position:absolute;top:7px;left:0;right:0;text-align:center;pointer-events:none;">${labelArr[idx]}</div>
            <div style="font-size:1.18em;margin-top:28px;z-index:1;position:relative;">${func}</div>
        </div>
    `;
}

// 可信度校验
let credibilityLow = false;
let warningMsg = "";

// 主导/辅助功能负面得分大于正面
const mainFuncIdx = [0, 1];
mainFuncIdx.forEach(idx => {
    const func = typeFuncs[idx];
    if (func) {
        if ((funcScores[func + "-"] || 0) > (funcScores[func + "+"] || 0)) {
            credibilityLow = true;
            warningMsg += `主导/辅助功能 ${func} 负面得分大于正面, 可能当下状态不佳或结果误测；`;
        }
    }
});

// 7-8功能正向大于负向
let posCount = 0, negCount = 0;
typeFuncs.forEach(func => {
    const pos = funcScores[func + "+"] || 0;
    const neg = funcScores[func + "-"] || 0;
    if (pos > neg) posCount++;
    if (neg > pos) negCount++;
});
if (posCount >= 7) {
    credibilityLow = true;
    warningMsg += `8个功能中有${posCount}个正向得分大于负向；`;
}
if (negCount >= 7) {
    credibilityLow = true;
    warningMsg += `8个功能中有${negCount}个负向得分大于正向；`;
}

// 获取当前类型功能顺序（如 INTJ: ["Ni","Te","Fi","Se",...])
document.getElementById('quiz-app').innerHTML = `
    <div class="center-card" style="flex-direction:row;justify-content:center;align-items:flex-start;gap:36px;max-width:1200px;">
        <!-- 人格类型 -->
        <div style="flex:1;min-width:220px;max-width:320px;display:flex;flex-direction:column;align-items:center;">
            <div class="result-title" style="font-size:1.5em;font-weight:bold;">你的类型：${bestType || "未识别"}</div>
            ${credibilityLow ? `<div style="color:#e26567;font-weight:bold;margin-bottom:0.5em;">可信度低</div>` : ""}
            <div style="color:#ffe7ba;margin-bottom:1em;">${typeDescriptions[bestType] || ""}</div>
            <button class="start-btn" onclick="renderHome()" style="margin-top:2em;">返回首页</button>
        </div>
        <!-- 柱状图 -->
        <div style="flex:1;min-width:260px;max-width:340px;">
            <div style="color:#ffe7ba;font-weight:bold;margin-bottom:0.5em;text-align:center;">感知功能得分</div>
            <div style="background:rgba(255,255,255,0.08);border-radius:10px;padding:12px 8px;margin-bottom:1.2em;">
                ${perceptionFuncs.map(f => renderFuncBar(f)).join('')}
            </div>
            <div style="color:#ffe7ba;font-weight:bold;margin-bottom:0.5em;text-align:center;">判断功能得分</div>
            <div style="background:rgba(255,255,255,0.08);border-radius:10px;padding:12px 8px;">
                ${judgingFuncs.map(f => renderFuncBar(f)).join('')}
            </div>
        </div>
        <!-- 功能排序 -->
        <div style="flex:1;min-width:220px;max-width:320px;display:flex;flex-direction:column;align-items:center;">
            <div style="color:#ffe7ba;font-weight:bold;margin-bottom:0.5em;text-align:center;">${bestType} 功能顺序</div>
            <div style="display:grid;grid-template-columns:repeat(2,1fr);grid-template-rows:repeat(4,1fr);gap:12px;">
                ${typeFuncs.map((f,i)=>renderFuncBox(f,i)).join('')}
            </div>
        </div>
    </div>
`;
}

        renderHome();
    </script>
</body>
</html>
