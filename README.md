# -<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>اختبار الذرة التفاعلي</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f5f5f5;
            margin: 0;
            padding: 20px;
            color: #333;
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        
        h1, h2 {
            text-align: center;
            color: #2c3e50;
        }
        
        .form-group {
            margin-bottom: 15px;
        }
        
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        
        input, select {
            width: 100%;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
            box-sizing: border-box;
        }
        
        .btn {
            background-color: #3498db;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
            display: block;
            margin: 20px auto;
        }
        
        .btn:hover {
            background-color: #2980b9;
        }
        
        .question {
            margin-bottom: 20px;
            padding: 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            background-color: #f9f9f9;
        }
        
        .question-number {
            font-weight: bold;
            margin-bottom: 10px;
        }
        
        .options {
            margin-left: 20px;
        }
        
        .option {
            margin-bottom: 8px;
        }
        
        .hidden {
            display: none;
        }
        
        .result {
            text-align: center;
            padding: 20px;
            background-color: #ecf0f1;
            border-radius: 5px;
            margin-top: 20px;
        }
        
        .score {
            font-size: 24px;
            font-weight: bold;
            color: #e74c3c;
        }
        
        .correct {
            color: #27ae60;
        }
        
        .incorrect {
            color: #e74c3c;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>اختبار الذرة التفاعلي</h1>
        
        <div id="start-section">
            <h2>بيانات الطالب</h2>
            <div class="form-group">
                <label for="student-name">اسم الطالب:</label>
                <input type="text" id="student-name" required>
            </div>
            <div class="form-group">
                <label for="student-class">الشعبة:</label>
                <select id="student-class" required>
                    <option value="">اختر الشعبة</option>
                    <option value="1">1</option>
                    <option value="2">2</option>
                    <option value="3">3</option>
                    <option value="4">4</option>
                    <option value="5">5</option>
                    <option value="6">6</option>
                    <option value="7">7</option>
                </select>
            </div>
            <button class="btn" id="start-btn">بدء الاختبار</button>
        </div>
        
        <div id="quiz-section" class="hidden">
            <form id="quiz-form">
                <!-- سيتم إضافة الأسئلة هنا ديناميكيًا -->
            </form>
            <button class="btn" id="submit-btn">إنهاء الاختبار</button>
        </div>
        
        <div id="result-section" class="hidden">
            <!-- سيتم عرض النتائج هنا -->
        </div>
    </div>

    <script>
        // بيانات الأسئلة
        const questions = [
            {
                question: "من الذي اقترح أن المادة تتكون من دقائق صغيرة غير قابلة للتجزئة؟",
                options: ["طومسون", "دالتون", "رذرفورد", "بور"],
                correct: 1
            },
            {
                question: "ما الجسم الذي يحمل شحنة موجبة في الذرة؟",
                options: ["النيوترون", "الإلكترون", "البروتون", "النواة"],
                correct: 2
            },
            {
                question: "أي مما يلي جسم متعادل الشحنة؟",
                options: ["البروتون", "النيوترون", "الإلكترون", "النواة"],
                correct: 1
            },
            {
                question: "الإلكترونات تدور حول النواة في",
                options: ["مستويات طاقة ثابتة فقط", "داخل النواة", "سحابة موجبة", "مدارات"],
                correct: 3
            },
            {
                question: "من اكتشف الإلكترون؟",
                options: ["رذرفورد", "بور", "طومسون", "شادويك"],
                correct: 2
            },
            {
                question: "ما موقع البروتونات في الذرة؟",
                options: ["في النواة", "في السحابة الإلكترونية", "في المدار الخارجي", "في الغلاف النووي"],
                correct: 0
            },
            {
                question: "عدد البروتونات يساوي",
                options: ["عدد النيوترونات", "العدد الذري", "عدد الإلكترونات", "عدد الكتلة"],
                correct: 1
            },
            {
                question: "ما الذي يحدد نوع العنصر؟",
                options: ["عدد النيوترونات", "عدد الإلكترونات", "عدد البروتونات", "عدد الكتلة"],
                correct: 2
            },
            {
                question: "ماذا تمثل كتلة الذرة تقريباً؟",
                options: ["مجموع البروتونات والإلكترونات", "مجموع البروتونات والنيوترونات", "عدد البروتونات فقط", "عدد الإلكترونات فقط"],
                correct: 1
            },
            {
                question: "الإلكترونات تحمل شحنة",
                options: ["موجبة", "سالبة", "متعادلة", "لا شيء"],
                correct: 1
            },
            {
                question: "الإلكترونات توجد في",
                options: ["النواة", "السحابة الإلكترونية", "مركز الذرة", "البروتونات"],
                correct: 1
            },
            {
                question: "ماذا يمثل العدد الكتلي؟",
                options: ["عدد البروتونات فقط", "عدد الإلكترونات", "عدد البروتونات + عدد النيوترونات", "عدد النيوترونات فقط"],
                correct: 2
            },
            {
                question: "النموذج الذي يصف الذرة كنواة صغيرة كثيفة موجبة الشحنة هو نموذج",
                options: ["بور", "طومسون", "رذرفورد", "دالتون"],
                correct: 2
            },
            {
                question: "نموذج 'المعجن مع الزبيب' من اقترحه؟",
                options: ["رذرفورد", "طومسون", "بور", "شادويك"],
                correct: 1
            },
            {
                question: "إكتشف النيوترون العالم",
                options: ["دالتون", "بور", "شادويك", "طومسون"],
                correct: 2
            },
            {
                question: "ما شحنة النواة الكلية؟",
                options: ["سالبة", "موجبة", "متعادلة", "لا توجد شحنة"],
                correct: 1
            },
            {
                question: "في الذرة المتعادلة، عدد الإلكترونات يساوي",
                options: ["عدد النيوترونات", "عدد البروتونات", "عدد الكتلة", "المستويات"],
                correct: 1
            },
            {
                question: "الإلكترونات الأقرب للنواة تمتلك",
                options: ["أكبر طاقة", "أقل طاقة", "نفس الطاقة", "لا طاقة"],
                correct: 1
            },
            {
                question: "من الذي وضع نموذج المستويات الطاقية للذرة؟",
                options: ["رذرفورد", "طومسون", "بور", "شادويك"],
                correct: 2
            },
            {
                question: "أي مما يلي لا يوجد في النواة؟",
                options: ["البروتون", "النيوترون", "الإلكترون", "جميعها توجد"],
                correct: 2
            },
            {
                question: "(العدد الذري للأكسجين 8) يعني أن لديه:",
                options: ["8 بروتونات", "8 نيوترونات", "8 إلكترونات فقط", "4 بروتونات و4 نيوترونات"],
                correct: 0
            },
            {
                question: "مجموع عدد البروتونات والنيوترونات في الذرة يسمى:",
                options: ["العدد الكتلي", "العدد الذري", "عدد الإلكترونات", "رقم المدار"],
                correct: 0
            },
            {
                question: "الإلكترونات تدور حول النواة بسبب:",
                options: ["قوى الجذب الكهربائي", "طاقة الضوء", "قوى الطرد", "الضغط"],
                correct: 0
            },
            {
                question: "من الذي قال إن الذرة تحتوي على فراغات كبيرة؟",
                options: ["رذرفورد", "بور", "دالتون", "طومسون"],
                correct: 0
            },
            {
                question: "الإلكترونات تتحرك بسرعة عالية حول النواة في",
                options: ["مدارات محددة", "مسار مستقيم", "اتجاه ثابت", "خط واحد"],
                correct: 0
            },
            {
                question: "عدد مستويات الطاقة في ذرة الصوديوم هو",
                options: ["1", "2", "3", "4"],
                correct: 2
            },
            {
                question: "المستوى الأول في الذرة يمكن أن يحتوي على",
                options: ["إلكترونين", "أربعة", "ثمانية", "عشرة"],
                correct: 0
            },
            {
                question: "المستوى الثاني يمكن أن يحتوي على أقصى",
                options: ["4", "6", "8", "10"],
                correct: 2
            },
            {
                question: "ما العنصر الذي يحتوي على بروتون واحد؟",
                options: ["الهيليوم", "الهيدروجين", "الأكسجين", "الكربون"],
                correct: 1
            },
            {
                question: "الذرة المتعادلة كهربائيًا تكون إذا",
                options: ["عدد البروتونات = عدد الإلكترونات", "عدد النيوترونات = عدد الإلكترونات", "عدد الكتلة = عدد البروتونات", "جميعها صحيحة"],
                correct: 0
            },
            {
                question: "الإلكترون أخف من البروتون بـ",
                options: ["مرتين", "100 مرة", "1800 مرة", "نفس الكتلة"],
                correct: 2
            },
            {
                question: "النواة تحتوي على",
                options: ["بروتونات فقط", "نيوترونات فقط", "بروتونات ونيوترونات", "إلكترونات فقط"],
                correct: 2
            },
            {
                question: "الإلكترونات الخارجية تحدد",
                options: ["نوع العنصر", "تفاعله الكيميائي", "لونه", "كتلته"],
                correct: 1
            },
            {
                question: "جسيمات تحمل الشحنة الموجبة تسمى",
                options: ["الإلكترونات", "النيوترونات", "البروتونات", "الفوتونات"],
                correct: 2
            },
            {
                question: "من صاحب أول نظرية علمية لتركيب الذرة؟",
                options: ["رذرفورد", "بور", "دالتون", "طومسون"],
                correct: 2
            },
            {
                question: "ما الذي يمثل العدد الكتلي؟",
                options: ["مجموع البروتونات والنيوترونات", "عدد البروتونات فقط", "عدد الإلكترونات", "عدد المستويات"],
                correct: 0
            },
            {
                question: "الإلكترون يوجد في",
                options: ["النواة", "السحابة الإلكترونية", "البروتون", "داخل النيوترون"],
                correct: 1
            },
            {
                question: "الذرة في الأصل تتكون من",
                options: ["نواة وسحابة إلكترونية", "نواة فقط", "إلكترونات فقط", "فراغ فقط"],
                correct: 0
            },
            {
                question: "الذي يحدد موقع الإلكترون هو",
                options: ["رقم المدار", "عدد البروتونات", "طاقته", "عدد الكتلة"],
                correct: 2
            }
        ];

        // عناصر DOM
        const startSection = document.getElementById('start-section');
        const quizSection = document.getElementById('quiz-section');
        const resultSection = document.getElementById('result-section');
        const startBtn = document.getElementById('start-btn');
        const submitBtn = document.getElementById('submit-btn');
        const quizForm = document.getElementById('quiz-form');
        const studentNameInput = document.getElementById('student-name');
        const studentClassSelect = document.getElementById('student-class');

        // بدء الاختبار
        startBtn.addEventListener('click', function() {
            if (studentNameInput.value && studentClassSelect.value) {
                startSection.classList.add('hidden');
                quizSection.classList.remove('hidden');
                renderQuestions();
            } else {
                alert('يرجى إدخال الاسم واختيار الشعبة');
            }
        });

        // عرض الأسئلة
        function renderQuestions() {
            quizForm.innerHTML = '';
            
            questions.forEach((q, index) => {
                const questionDiv = document.createElement('div');
                questionDiv.className = 'question';
                
                const questionNumber = document.createElement('div');
                questionNumber.className = 'question-number';
                questionNumber.textContent = `سؤال ${index + 1}: ${q.question}`;
                
                const optionsDiv = document.createElement('div');
                optionsDiv.className = 'options';
                
                q.options.forEach((option, optIndex) => {
                    const optionDiv = document.createElement('div');
                    optionDiv.className = 'option';
                    
                    const input = document.createElement('input');
                    input.type = 'radio';
                    input.name = `question-${index}`;
                    input.value = optIndex;
                    input.id = `q${index}-opt${optIndex}`;
                    
                    const label = document.createElement('label');
                    label.htmlFor = `q${index}-opt${optIndex}`;
                    label.textContent = option;
                    
                    optionDiv.appendChild(input);
                    optionDiv.appendChild(label);
                    optionsDiv.appendChild(optionDiv);
                });
                
                questionDiv.appendChild(questionNumber);
                questionDiv.appendChild(optionsDiv);
                quizForm.appendChild(questionDiv);
            });
        }

        // تقديم الإجابات
        submitBtn.addEventListener('click', function() {
            const studentName = studentNameInput.value;
            const studentClass = studentClassSelect.value;
            let score = 0;
            const results = [];
            
            questions.forEach((q, index) => {
                const selectedOption = document.querySelector(`input[name="question-${index}"]:checked`);
                
                if (selectedOption) {
                    const userAnswer = parseInt(selectedOption.value);
                    const isCorrect = userAnswer === q.correct;
                    
                    if (isCorrect) {
                        score++;
                    }
                    
                    results.push({
                        question: q.question,
                        userAnswer: q.options[userAnswer],
                        correctAnswer: q.options[q.correct],
                        isCorrect: isCorrect
                    });
                } else {
                    results.push({
                        question: q.question,
                        userAnswer: "لم يتم الإجابة",
                        correctAnswer: q.options[q.correct],
                        isCorrect: false
                    });
                }
            });
            
            showResults(studentName, studentClass, score, results);
        });

        // عرض النتائج
        function showResults(name, className, score, results) {
            quizSection.classList.add('hidden');
            resultSection.classList.remove('hidden');
            
            const percentage = (score / questions.length) * 100;
            
            resultSection.innerHTML = `
                <h2>نتيجة الاختبار</h2>
                <p><strong>اسم الطالب:</strong> ${name}</p>
                <p><strong>الشعبة:</strong> ${className}</p>
                <div class="score">${score} / ${questions.length} (${percentage.toFixed(1)}%)</div>
                
                <h3>تفاصيل الإجابات:</h3>
                <div id="detailed-results">
                    ${results.map((result, index) => `
                        <div class="question-result">
                            <p><strong>سؤال ${index + 1}:</strong> ${result.question}</p>
                            <p class="${result.isCorrect ? 'correct' : 'incorrect'}">
                                <strong>إجابتك:</strong> ${result.userAnswer}
                                ${!result.isCorrect ? `<br><strong>الإجابة الصحيحة:</strong> ${result.correctAnswer}` : ''}
                            </p>
                        </div>
                    `).join('')}
                </div>
                
                <button class="btn" id="retry-btn">إعادة الاختبار</button>
            `;
            
            document.getElementById('retry-btn').addEventListener('click', function() {
                resultSection.classList.add('hidden');
                startSection.classList.remove('hidden');
                studentNameInput.value = '';
                studentClassSelect.value = '';
                quizForm.reset();
            });
        }
    </script>
</body>
</html>
