<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>荣格八维认知功能测试</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: blueviolet;
            color: antiquewhite;
            text-align: center;
            padding: 50px;
            margin: 0;
        }
        h1 {
            font-size: 2em;
            color: bisque;
        }
        </style>
    </head>
    <body>
      <div id="quiz-container">
        <p>请点击下方按钮开始测试</p>
        <button onclick="startTest()">开始测试</button>
      </div>
    </body>

    <script>
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
            { text: "非常同意", value: 5},
            { text: "同意", value: 3},
            { text: "中立", value: 0},
            { text: "不同意", value: -3},
            { text: "非常不同意", value: -5}
        ];
                let answers = new Array(questions.length).fill(null);
        let current = 0;

        function startTest() {
            showQuestion();
        }

        function showQuestion(errorMsg = '') {
            let optionsHtml = options.map((opt, idx) => `
                <label>
                    <input type="radio" name="answer" value="${opt.value}" ${answers[current] == opt.value ? 'checked' : ''}>
                    ${opt.text}
                </label>
            `).join('<br>');
            document.getElementById('quiz-container').innerHTML = `
                <h1>第${current + 1}题</h1>
                <p>${questions[current]}</p>
                <div>${optionsHtml}</div>
                <div class="btn-group">
                    <button onclick="prevQuestion()" ${current === 0 ? 'disabled' : ''}>上一题</button>
                    <button onclick="nextQuestion()">${current === questions.length - 1 ? '提交' : '下一题'}</button>
                </div>
                <div class="error" style="color:yellow;">${errorMsg}</div>
            `;
        }
        function prevQuestion() {
            saveAnswer();
            if (current > 0) {
                current--;
                showQuestion();
            }
        }

        function nextQuestion() {
            const selected = document.querySelector('input[name="answer"]:checked');
            if (!selected) {
                showQuestion('请先选择一个选项');
                return;
            }
            saveAnswer();
            if (current < questions.length - 1) {
                current++;
                showQuestion();
            } else {
                submitQuiz();
            }
        }

        function saveAnswer() {
            const selected = document.querySelector('input[name="answer"]:checked');
            if (selected) {
                answers[current] = Number(selected.value);
            }
        }

        // 统计分数
function submitQuiz() {
    // 先清零
    varNames.forEach(name => varScores[name] = 0);
    // 累加每题分数到对应变量
    answers.forEach((score, idx) => {
        if (score !== null) {
            varScores[questionVars[idx]] += score;
        }
    });
    // 展示结果
    document.getElementById('quiz-container').innerHTML = `
        <h1>测试完成！</h1>
        <p>各变量得分：</p>
        <ul>
            ${Object.entries(varScores).map(([k, v]) => `<li>${k}: ${v}</li>`).join('')}
        </ul>
    `;
}

    </script>
</html>
