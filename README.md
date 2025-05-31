<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <title>荣格八维认知功能测试</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- ...样式同你原有... -->
    <style>
        /* ...省略，与你原有一致... */
    </style>
</head>
<body>
    <div class="overlay"></div>
    <div id="quiz-app"></div>
    <script>
        // ===================== 你可以自定义的部分 =====================
        const questions = [
            // ...你的题库...
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
        // ===================== 你可以自定义的部分结束 =====================
        let userScores = {};
        functions.forEach(f => userScores[f] = [0,0,0,0,0,0,0,0]);
        let answers = new Array(questions.length).fill(null);
        let current = 0;
        let positions = Array(8).fill(""); // 关键：全局声明

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
            let leftLabel = `<div class="slider-label">完全不符合</div>`;
            let rightLabel = `<div class="slider-label right">非常同意</div>`;
            let optionHtml = options.map((opt, idx) => `
                <button
                    class="option-card${answers[current] === opt.value ? ' selected' : ''}"
                    onclick="selectOption(${opt.value})"
                    type="button"
                    aria-label="${opt.text}"
                >
                    <div class="option-dot"></div>
                    <span>${opt.text}</span>
                </button>
            `).join('');
            document.getElementById('quiz-app').innerHTML = `
                <div class="center-card">
                    <div class="progress-bar"><div class="progress" style="width:${progress}%;"></div></div>
                    <div class="question-title">${questions[current].text}</div>
                    <div class="options-slider">
                        ${leftLabel}
                        <div class="option-card-group">${optionHtml}</div>
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
        function startTest() {
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
            // 关键：不要再 let positions = ...，直接用全局 positions
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
            if (!bestType) bestType = "（无法判断）";
            let top3 = typeScores.slice(0, 3);

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
        renderHome();
    </script>
</body>
</html>
