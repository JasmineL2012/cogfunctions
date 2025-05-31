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
            .slider-label { font-size: 0.95em; width: 36px; }
            .bar-bg { width: 120px; }
        }
        /* 新选项卡片样式 */
        .option-card-group {
            display: flex; flex: 1; justify-content: space-between; align-items: stretch; gap: 12px;
            margin: 0 8px;
        }
        .option-card {
            flex: 1 1 0; display: flex; flex-direction: column; align-items: center; justify-content: center;
            background: linear-gradient(135deg, rgba(20,32,60,0.22) 60%, rgba(98,178,131,0.10) 100%);
            border-radius: 18px;
            min-width: 0;
            min-height: 72px;
            padding: 12px 6px 10px 6px;
            margin: 0;
            border: 2.5px solid transparent;
            box-shadow: 0 2px 12px 0 rgba(31,38,135,0.10);
            cursor: pointer;
            transition: border-color 0.18s, box-shadow 0.18s, background 0.18s, transform 0.12s;
            font-size: 1.14em;
            color: #f8f8ff;
            font-weight: 500;
            letter-spacing: 1px;
            text-shadow: 0 1px 6px #222a;
            outline: none;
            position: relative;
        }
        .option-card.selected {
            border-color: #62b283;
            background: linear-gradient(135deg, rgba(98,178,131,0.22) 60%, rgba(255,231,186,0.18) 100%);
            color: #ffe7ba;
            font-weight: bold;
            box-shadow: 0 4px 18px 0 rgba(98,178,131,0.18);
            transform: scale(1.04);
        }
        .option-card:active {
            transform: scale(0.98);
        }
        .option-card .option-dot {
            width: 18px; height: 18px; border-radius: 50%; margin-bottom: 8px;
            border: 2.5px solid #e0e0e0; background: #fff; box-shadow: 0 1px 6px #222a22;
            transition: border-color 0.18s, background 0.18s;
        }
        .option-card.selected .option-dot {
            background: #62b283;
            border-color: #62b283;
        }
        @media (max-width: 600px) {
            .option-card-group { gap: 4px; }
            .option-card { min-height: 48px; font-size: 0.98em; padding: 8px 2px 8px 2px; }
            .option-card .option-dot { width: 12px; height: 12px; }
        }
    </style>
</head>
<body>
    <div class="overlay"></div>
    <div id="quiz-app"></div>
    <script>
        // ...题库、options、functions、typeTable 省略，与你现有一致...

        // 省略题库部分，直接看 submitQuiz
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
            let top3 = typeScores.slice(0, 3);
            // 防止类型为空
            if (!bestType) bestType = "（无法判断）";

            // === 自动补全第5~8位功能 ===
            if (bestType && typeTable[bestType]) {
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
                <li>互补功能(5)：${positions[4]}</li>
                <li>批判功能(6)：${positions[5]}</li>
                <li>盲点功能(7)：${positions[6]}</li>
                <li>魔鬼功能(8)：${positions[7]}</li>
            `;
            // 柱状图
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
            let typeHtml = `
                <p style="color:#ffe7ba;font-size:1.2em;">
                    你的类型：<b style="font-size:1.5em;color:#62b283;">${bestType}</b>
                </p>
                <ul>${top3.map(t=>`<li><b>${t.type}</b> 匹配分：${t.score}/4</li>`).join('')}</ul>
            `;
            document.getElementById('quiz-app').innerHTML = `
                <div class="center-card">
                    <div class="result-title">测试完成！</div>
                    ${typeHtml}
                    <p>你的主序列：</p>
                    <ul>${resultHtml}</ul>
                    <p style="margin-bottom:1em;">各变量得分：</p>
                    <div>${scoreHtml}</div>
                    <button class="start-btn" onclick="renderHome()">返回首页</button>
                </div>
            `;
        }
        // ...renderHome、showQuestion、selectOption等函数与你现有一致...
        renderHome();
    </script>
</body>
</html>
