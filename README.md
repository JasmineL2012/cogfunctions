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

    // 互补功能：1和5、2和6、3和7、4和8
    function getComplement(key) {
        if (key.startsWith("Ni")) return "Ti+";
        if (key.startsWith("Ne")) return "Si+";
        if (key.startsWith("Si")) return "Ne+";
        if (key.startsWith("Se")) return "Fi+";
        if (key.startsWith("Ti")) return "Ni+";
        if (key.startsWith("Te")) return "Ti+";
        if (key.startsWith("Fi")) return "Se+";
        if (key.startsWith("Fe")) return "Te+";
        return "";
    }
    // 你的要求：如果第一功能是Te，第五必须为Ti，以此类推
    positions[4] = getComplement(main1);
    positions[5] = getComplement(main2);
    positions[6] = getComplement(positions[2]);
    positions[7] = getComplement(positions[3]);

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

    // 类型描述（可根据需要扩展更多类型描述）
    const typeDescriptions = {
        INTJ: "INTJ：富有远见、善于规划，喜欢独立思考和系统性分析，追求高效和创新。",
        INTP: "INTP：逻辑严密、思想开放，喜欢探索理论和原理，追求真理和独立见解。",
        ENTJ: "ENTJ：果断自信、善于领导，擅长制定战略和组织资源，追求目标和成就。",
        ENTP: "ENTP：机智灵活、善于创新，喜欢挑战常规和提出新观点，乐于辩论和探索。",
        INFJ: "INFJ：富有洞察力、关怀他人，注重价值观和意义，善于理解他人情感。",
        INFP: "INFP：理想主义、富有同情心，重视内心价值和独特性，追求和谐与自我实现。",
        ENFP: "ENFP：热情开放、富有创造力，喜欢探索新可能，重视人际关系和个人成长。",
        ENFJ: "ENFJ：善于沟通、关心他人，擅长激励和引导团队，重视集体和社会价值。",
        ISTJ: "ISTJ：务实可靠、注重细节，喜欢有序和规则，重视责任和承诺。",
        ISFJ: "ISFJ：体贴周到、乐于助人，注重传统和安全，善于照顾他人。",
        ESTJ: "ESTJ：组织能力强、注重效率，喜欢管理和执行，重视规则和秩序。",
        ESFJ: "ESFJ：友善合群、乐于服务，重视人际关系和团队合作，善于协调和支持。",
        ESTP: "ESTP：行动力强、适应力高，喜欢冒险和挑战，善于解决实际问题。",
        ESFP: "ESFP：热情外向、乐于体验，喜欢享受生活和与人互动，重视当下和感受。",
        ISTP: "ISTP：冷静理性、动手能力强，喜欢分析和解决实际问题，适应变化。",
        ISFP: "ISFP：温和敏感、追求自由，重视个人体验和美感，喜欢随性而为。"
    };
    let typeHtml = bestType
        ? `<div style="font-size:1.5em;color:#ffe7ba;font-weight:bold;">${bestType}</div>
           <div style="color:#fff;margin:1em 0 0.5em 0;">${typeDescriptions[bestType] || ""}</div>`
        : `<div style="color:#ffe7ba;">无法确定人格类型</div>`;

    document.getElementById('quiz-app').innerHTML = `
    <div class="center-card" style="max-width:700px;display:flex;flex-direction:column;align-items:center;">
        <div class="result-title">最有可能的人格类型</div>
        ${typeHtml}
        <div style="text-align:center;margin-top:32px;">
            <button class="start-btn" onclick="renderHome()">返回首页</button>
            <button class="nav-btn" onclick="showSignExplain()">正负号解释</button>
        </div>
    </div>
    `;
}

// 新页面：正负号解释
function showSignExplain() {
    document.getElementById('quiz-app').innerHTML = `
    <div class="center-card" style="max-width:700px;">
        <div class="result-title">正负号的含义与判断依据</div>
        <div style="color:#fff;text-align:left;line-height:1.8;font-size:1.08em;">
            <b>正号（+）</b>：表示该功能的典型、主流或积极表现。例如“Ni+”代表内倾直觉的主动、健康使用。<br>
            <b>负号（-）</b>：表示该功能的非典型、消极或受压抑表现。例如“Ni-”代表内倾直觉的回避、失衡或阴影面。<br>
            <br>
            <b>判断依据：</b><br>
            - 题目设计时，正号题目描述功能的健康、主动、典型用法，负号题目描述功能的回避、压抑、极端或阴影面。<br>
            - 你的答题分数越高，说明你在该功能的该极性上表现越明显。<br>
            <br>
            <b>举例：</b><br>
            - “Te+”高分：你倾向于用客观标准和逻辑管理外部世界。<br>
            - “Te-”高分：你可能在外部逻辑上有回避、压抑或极端表现。<br>
            <br>
            <button class="nav-btn" onclick="renderHome()">返回首页</button>
        </div>
    </div>
    `;
}
