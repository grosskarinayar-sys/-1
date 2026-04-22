<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Тест: Исполнение наказания несовершеннолетних</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }
        .container {
            max-width: 900px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            overflow: hidden;
            animation: fadeIn 0.5s ease;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .header {
            background: linear-gradient(135deg, #4a5568 0%, #2d3748 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }
        .header h1 {
            font-size: 1.8rem;
            margin-bottom: 10px;
        }
        .header p {
            opacity: 0.9;
            font-size: 1rem;
        }
        .variant-badge {
            background: #e53e3e;
            display: inline-block;
            padding: 8px 20px;
            border-radius: 30px;
            font-weight: bold;
            margin-top: 15px;
            font-size: 1.2rem;
        }
        .content {
            padding: 30px;
        }
        .question {
            margin-bottom: 25px;
            padding: 15px;
            background: #f7fafc;
            border-radius: 12px;
            border-left: 4px solid #667eea;
        }
        .question-text {
            font-weight: 600;
            margin-bottom: 12px;
            color: #2d3748;
            font-size: 1.05rem;
        }
        .options {
            padding-left: 20px;
        }
        .options label {
            display: block;
            margin: 8px 0;
            cursor: pointer;
            color: #4a5568;
        }
        .options input {
            margin-right: 10px;
            cursor: pointer;
        }
        .task {
            margin-top: 30px;
            padding: 20px;
            background: #fef5e7;
            border-radius: 12px;
            border-left: 4px solid #ed8936;
        }
        .task h3 {
            color: #c05621;
            margin-bottom: 15px;
        }
        .task textarea {
            width: 100%;
            padding: 12px;
            border: 1px solid #e2e8f0;
            border-radius: 8px;
            font-family: inherit;
            resize: vertical;
            margin-top: 10px;
        }
        .email-input {
            margin: 20px 0;
            padding: 15px;
            background: #e6fffa;
            border-radius: 12px;
        }
        .email-input label {
            font-weight: 600;
            color: #234e52;
        }
        .email-input input {
            width: 100%;
            padding: 10px;
            margin-top: 8px;
            border: 1px solid #b2f5ea;
            border-radius: 8px;
            font-size: 1rem;
        }
        .btn-submit {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 14px 30px;
            font-size: 1.1rem;
            font-weight: bold;
            border-radius: 40px;
            cursor: pointer;
            width: 100%;
            transition: transform 0.2s, box-shadow 0.2s;
        }
        .btn-submit:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(0,0,0,0.2);
        }
        .result {
            margin-top: 20px;
            padding: 15px;
            border-radius: 12px;
            display: none;
        }
        .result.success {
            background: #c6f6d5;
            color: #22543d;
            display: block;
        }
        .result.error {
            background: #fed7d7;
            color: #742a2a;
            display: block;
        }
        footer {
            background: #edf2f7;
            padding: 15px;
            text-align: center;
            font-size: 0.8rem;
            color: #718096;
        }
        @media (max-width: 600px) {
            .content {
                padding: 20px;
            }
            .question-text {
                font-size: 0.95rem;
            }
        }
    </style>
</head>
<body>
<div class="container" id="app">
    <div class="header">
        <h1>📚 Контроль знаний</h1>
        <p>Институт исполнения наказания в виде лишения свободы<br>в отношении несовершеннолетних</p>
        <div class="variant-badge" id="variantBadge">Загрузка...</div>
    </div>
    <div class="content">
        <form id="testForm">
            <div id="questionsContainer"></div>
            
            <div class="task">
                <h3>📝 Задача с открытым ответом</h3>
                <div id="taskText"></div>
                <textarea id="openAnswer" rows="5" placeholder="Введите ваш развернутый ответ здесь..."></textarea>
            </div>
            
            <div class="email-input">
                <label>📧 Email для получения результатов:</label>
                <input type="email" id="studentEmail" placeholder="example@mail.ru" required>
                <small style="color: #718096;">Результаты будут отправлены на этот адрес</small>
            </div>
            
            <button type="button" class="btn-submit" onclick="submitTest()">✅ Отправить ответы</button>
            <div id="resultMessage" class="result"></div>
        </form>
    </div>
    <footer>
        Тест состоит из 10 вопросов и задачи. Выбран вариант случайным образом.
    </footer>
</div>

<script>
    // ========== МАТЕРИАЛЫ ТЕСТОВ ==========
    
    // ВАРИАНТ 1
    const variant1 = {
        name: "ВАРИАНТ 1",
        questions: [
            { text: "1. В каком учреждении несовершеннолетние отбывают наказание в виде лишения свободы?", options: ["а) Исправительная колония общего режима", "б) Тюрьма", "в) Воспитательная колония", "г) Колония-поселение"], correct: 2 },
            { text: "2. Какова максимальная цель наказания в отношении несовершеннолетних?", options: ["а) Изоляция от общества", "б) Исправление и предотвращение новых преступлений", "в) Возмездие за содеянное", "г) Физическое наказание"], correct: 1 },
            { text: "3. В каком возрасте несовершеннолетние могут быть переведены из воспитательной колонии в исправительную колонию общего режима?", options: ["а) По достижении 16 лет", "б) По достижении 18 лет", "в) По достижении 21 года", "г) Не переводятся"], correct: 1 },
            { text: "4. Какие виды наказаний НЕ применяются к несовершеннолетним?", options: ["а) Штраф", "б) Обязательные работы", "в) Лишение свободы", "г) Пожизненное лишение свободы"], correct: 3 },
            { text: "5. Основные средства исправления несовершеннолетних, отбывающих лишение свободы, включают:", options: ["а) Только строгий режим", "б) Режим, воспитательную работу, общественно полезный труд, обучение", "в) Исключительно физическую подготовку", "г) Трудотерапию без права обучения"], correct: 1 },
            { text: "6. Социально-правовое значение исполнения лишения свободы в отношении несовершеннолетних заключается в:", options: ["а) Усилении карательной функции", "б) Обеспечении социальной реабилитации и ресоциализации", "в) Демонстрации силы государства", "г) Исключении права на образование"], correct: 1 },
            { text: "7. В каком нормативно-правовом акте закреплен перечень видов наказаний, назначаемых несовершеннолетним, включая лишение свободы?", options: ["а) Уголовно-процессуальный кодекс РФ", "б) Уголовный кодекс РФ (ст. 88)", "в) Уголовно-исполнительный кодекс РФ", "г) Конституция РФ"], correct: 1 },
            { text: "8. Разрешено ли в воспитательных колониях использование мер физического воздействия?", options: ["а) Категорически запрещено", "б) Только в исключительных случаях (пресечение преступления, самооборона)", "в) Только для поддержания дисциплины"], correct: 1 },
            { text: "9. Какой основной НПА регулирует порядок и условия исполнения наказаний в виде лишения свободы?", options: ["а) УК РФ", "б) УПК РФ", "в) Конституция", "г) УИК РФ"], correct: 3 },
            { text: "10. Особенностью режима в воспитательных колониях является:", options: ["а) Свободное выезд домой", "б) Ограничение общения с другими осужденными", "в) Создание условий для получения общего и профессионального образования"], correct: 2 }
        ],
        task: "Задача: Администрация воспитательной колонии полностью заменила общеобразовательное обучение несовершеннолетних производственным трудом, аргументируя это необходимостью возмещения ущерба от преступлений.\n\nВопрос: Законны ли действия администрации? Назовите основные средства исправления несовершеннолетних."
    };
    
    // ВАРИАНТ 2
    const variant2 = {
        name: "ВАРИАНТ 2",
        questions: [
            { text: "1. Какой документ составляет международно-правовую основу института исполнения наказания несовершеннолетних, закрепляя принцип раздельного содержания со взрослыми?", options: ["а) Манифест об образовании", "б) Конвенция ООН о правах ребенка (1989 г.)", "в) Женевские конвенции 1949 г."], correct: 1 },
            { text: "2. Какая из перечисленных целей наказания, согласно ст. 43 УК РФ, является приоритетной при применении лишения свободы к несовершеннолетним?", options: ["а) Возмездие за совершенное преступление", "б) Восстановление социальной справедливости", "в) Устрашение населения", "г) Изоляция от общества на максимальный срок"], correct: 1 },
            { text: "3. В чем заключается социально-правовое значение института лишения свободы для несовершеннолетних?", options: ["а) В ужесточении ответственности до уровня взрослых", "б) В обеспечении приоритета воспитания, образования и подготовки к жизни в обществе", "в) В полном освобождении от ответственности", "г) В ликвидации ответственности"], correct: 1 },
            { text: "4. Какое из перечисленных средств исправления НЕ применяется к несовершеннолетним в колониях?", options: ["а) Режим", "б) Получение основного общего образования", "в) Общественно полезный труд", "г) Участие в боевых действиях"], correct: 3 },
            { text: "5. В чем заключается социально-правовое значение воспитательных колоний?", options: ["а) В создании условий для социальной адаптации и обучения", "б) В максимальной изоляции осужденных", "в) В организации жесткого физического труда", "г) В полном освобождении от ответственности"], correct: 0 },
            { text: "6. В каком учреждении несовершеннолетние отбывают наказание в виде лишения свободы?", options: ["а) Исправительная колония общего режима", "б) Тюрьма", "в) Воспитательная колония", "г) Колония-поселение"], correct: 2 },
            { text: "7. Особенностью режима в воспитательных колониях является:", options: ["а) Свободное посещение школы", "б) Создание условий для получения общего и профессионального образования", "в) Отсутствие ограничений в общении"], correct: 1 },
            { text: "8. Обязательно ли получение общего образования в воспитательной колонии?", options: ["а) Да, до 18 лет", "б) Нет, по желанию", "в) Только для тех, кто не умеет читать"], correct: 0 },
            { text: "9. До какого возраста осужденные могут оставаться в воспитательной колонии?", options: ["а) До 18 лет", "б) До 19 лет", "в) До 21 года"], correct: 1 },
            { text: "10. Какой основной НПА регулирует порядок и условия исполнения наказаний в виде лишения свободы?", options: ["а) УК РФ", "б) УИК РФ", "в) Приказы ФСИН", "г) УПК РФ"], correct: 1 }
        ],
        task: "Задача: В воспитательной колонии к осужденному, нарушившему режим, применили физическую силу для наказания.\n\nВопрос: Соответствует ли это целям наказания несовершеннолетних? Обоснуйте ответ."
    };
    
    // Рандомный выбор варианта
    const variants = [variant1, variant2];
    const selectedVariant = variants[Math.floor(Math.random() * 2)];
    
    // Отображение варианта
    document.getElementById('variantBadge').innerText = selectedVariant.name;
    
    // Генерация вопросов
    function renderQuestions() {
        const container = document.getElementById('questionsContainer');
        let html = '';
        selectedVariant.questions.forEach((q, idx) => {
            html += `
                <div class="question">
                    <div class="question-text">${q.text}</div>
                    <div class="options">
            `;
            q.options.forEach((opt, optIdx) => {
                html += `
                    <label>
                        <input type="radio" name="q${idx}" value="${optIdx}">
                        ${opt}
                    </label>
                `;
            });
            html += `</div></div>`;
        });
        container.innerHTML = html;
        document.getElementById('taskText').innerHTML = `<p style="white-space: pre-line;">${selectedVariant.task}</p>`;
    }
    
    // Сбор ответов
    function collectAnswers() {
        let score = 0;
        let answers = [];
        for (let i = 0; i < selectedVariant.questions.length; i++) {
            const radios = document.getElementsByName(`q${i}`);
            let selectedValue = null;
            for (let j = 0; j < radios.length; j++) {
                if (radios[j].checked) {
                    selectedValue = parseInt(radios[j].value);
                    break;
                }
            }
            const isCorrect = (selectedValue === selectedVariant.questions[i].correct);
            if (isCorrect) score++;
            answers.push({
                question: selectedVariant.questions[i].text,
                userAnswer: selectedValue !== null ? selectedVariant.questions[i].options[selectedValue] : "Не выбран",
                correctAnswer: selectedVariant.questions[i].options[selectedVariant.questions[i].correct],
                isCorrect: isCorrect
            });
        }
        return { score, answers, total: selectedVariant.questions.length };
    }
    
    // Отправка на email через FormSubmit.co (бесплатный сервис)
    async function submitTest() {
        const studentEmail = document.getElementById('studentEmail').value;
        const openAnswer = document.getElementById('openAnswer').value;
        const resultDiv = document.getElementById('resultMessage');
        
        if (!studentEmail) {
            resultDiv.className = 'result error';
            resultDiv.innerHTML = '❌ Пожалуйста, введите ваш email для получения результатов.';
            return;
        }
        
        const { score, answers, total } = collectAnswers();
        const percent = Math.round((score / total) * 100);
        
        // Формируем тело письма
        let emailBody = `Результаты тестирования\n`;
        emailBody += `Вариант: ${selectedVariant.name}\n`;
        emailBody += `Студент: ${studentEmail}\n`;
        emailBody += `Результат: ${score} из ${total} (${percent}%)\n\n`;
        emailBody += `=== Детальные ответы ===\n`;
        answers.forEach((a, idx) => {
            emailBody += `${idx+1}. ${a.question}\n`;
            emailBody += `   Ответ: ${a.userAnswer}\n`;
            emailBody += `   Правильный: ${a.correctAnswer}\n`;
            emailBody += `   Верно: ${a.isCorrect ? '✅' : '❌'}\n\n`;
        });
        emailBody += `=== Открытая задача ===\n`;
        emailBody += `${selectedVariant.task}\n\n`;
        emailBody += `Ответ студента:\n${openAnswer || '(ответ не дан)'}\n`;
        emailBody += `\n---\nОтправлено автоматически из системы тестирования.`;
        
        // Отправка через FormSubmit (прокси-сервис)
        try {
            const formData = new FormData();
            formData.append('email', 'carina.gross@yandex.ru');
            formData.append('subject', `Результаты теста - ${selectedVariant.name} - ${studentEmail}`);
            formData.append('message', emailBody);
            formData.append('_replyto', studentEmail);
            
            const response = await fetch('https://formsubmit.co/ajax/carina.gross@yandex.ru', {
                method: 'POST',
                body: formData
            });
            
            if (response.ok) {
                resultDiv.className = 'result success';
                resultDiv.innerHTML = `✅ Результаты отправлены! Ваш результат: ${score}/${total} (${percent}%). Проверьте почту ${studentEmail} (возможно, папку Спам).`;
                // Не очищаем форму, чтобы студент мог сохранить результат
            } else {
                throw new Error('Ошибка отправки');
            }
        } catch (error) {
            resultDiv.className = 'result error';
            resultDiv.innerHTML = `⚠️ Не удалось отправить результаты автоматически. Скопируйте результат: ${score}/${total} (${percent}%) и отправьте преподавателю вручную.`;
            console.error('Submit error:', error);
        }
    }
    
    renderQuestions();
</script>
</body>
</html>
