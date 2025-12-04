<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: Everyday Actions</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #3498db 0%, #2c3e50 100%);
            min-height: 100vh;
            padding: 20px;
            color: #2c3e50;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            max-width: 1000px;
            width: 100%;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #2980b9, #3498db);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #2980b9, #3498db);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(41, 128, 185, 0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 30px;
            min-height: 400px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #e8f4fc, #ecf0f1);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #3498db;
            box-shadow: 0 4px 15px rgba(52, 152, 219, 0.2);
        }

        .word-bank h3 {
            color: #2980b9;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #3498db, #2980b9);
            color: white;
            padding: 10px 18px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 3px 10px rgba(52, 152, 219, 0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(52, 152, 219, 0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid #3498db;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #2980b9;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #27ae60;
            background: #d5f4e6;
        }

        .fill-blank.incorrect {
            border-color: #e74c3c;
            background: #fadbd8;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .option {
            padding: 15px 20px;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .option:hover {
            border-color: #3498db;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(52, 152, 219, 0.2);
        }

        .option.selected {
            background: #3498db;
            color: white;
            border-color: #3498db;
        }

        .option.correct {
            background: #27ae60;
            color: white;
            border-color: #27ae60;
        }

        .option.incorrect {
            background: #e74c3c;
            color: white;
            border-color: #e74c3c;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #2980b9;
            font-size: 1.2em;
        }

        .match-item {
            padding: 15px;
            margin: 8px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .match-item:hover {
            border-color: #3498db;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(52, 152, 219, 0.2);
        }

        .match-item.selected {
            background: #e8f4fc;
            border-color: #3498db;
        }

        .match-item.matched {
            background: #27ae60;
            color: white;
            border-color: #27ae60;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #3498db, #2980b9);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 20px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(52, 152, 219, 0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(52, 152, 219, 0.4);
        }

        .reset-btn {
            background: linear-gradient(135deg, #e74c3c, #c0392b);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 10px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(231, 76, 60, 0.3);
        }

        .reset-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(231, 76, 60, 0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #3498db, #2980b9);
            color: white;
            padding: 15px 20px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(52, 152, 219, 0.3);
            z-index: 1000;
        }

        .icon {
            font-size: 24px;
            margin-right: 10px;
            vertical-align: middle;
        }

        /* Vocabulary List Styles */
        .vocabulary-list {
            padding: 20px;
        }

        .vocabulary-item {
            margin-bottom: 25px;
            padding: 20px;
            border-radius: 10px;
            background: #f8f9fa;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
        }

        .vocabulary-item h3 {
            color: #2980b9;
            margin-bottom: 10px;
            font-size: 1.4em;
            border-bottom: 2px solid #3498db;
            padding-bottom: 8px;
        }

        .vocabulary-item p {
            margin-bottom: 8px;
            line-height: 1.6;
        }

        .example {
            font-style: italic;
            color: #555;
            padding-left: 15px;
            border-left: 3px solid #3498db;
            margin-top: 10px;
        }

        .vocabulary-item strong {
            color: #2c3e50;
        }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 200px;
            }
            
            .score {
                position: static;
                margin: 20px auto;
                display: block;
                width: fit-content;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/15</div>
    
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-book icon"></i> Vocabulary Game: Everyday Actions</h1>
            <p>Practice these useful English words in different contexts!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('vocabulary')">Vocabulary List</button>
            <button class="nav-btn" onclick="showSection('fill-gaps')">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching')">Match Definitions</button>
            <button class="nav-btn" onclick="showSection('multiple-choice')">Multiple Choice</button>
        </div>

        <!-- Vocabulary List Section -->
        <div id="vocabulary" class="game-section active">
            <h2 style="text-align: center; margin-bottom: 20px; color: #2980b9;">Vocabulary Words and Meanings</h2>
            
            <div class="vocabulary-list">
                <div class="vocabulary-item">
                    <h3>upload</h3>
                    <p><strong>Definition:</strong> To transfer data or files from a local computer to a remote server or website.</p>
                    <p><strong>Usage:</strong> Commonly used in computing and digital contexts; opposite of "download."</p>
                    <p class="example"><strong>Example:</strong> "I need to upload these photos to my social media account."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>wear out</h3>
                    <p><strong>Definition:</strong> To become damaged or useless from prolonged use; to exhaust or tire someone.</p>
                    <p><strong>Usage:</strong> Can refer to objects becoming old or people becoming tired.</p>
                    <p class="example"><strong>Example:</strong> "My shoes have worn out after two years of daily use."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>waste</h3>
                    <p><strong>Definition:</strong> To use or expend carelessly, extravagantly, or to no purpose.</p>
                    <p><strong>Usage:</strong> Can refer to time, money, resources, or opportunities.</p>
                    <p class="example"><strong>Example:</strong> "Don't waste your time watching TV all day."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>weak</h3>
                    <p><strong>Definition:</strong> Lacking physical strength or energy; not strong.</p>
                    <p><strong>Usage:</strong> Can describe physical weakness, weak arguments, weak signals, etc.</p>
                    <p class="example"><strong>Example:</strong> "After being sick for a week, I still feel weak."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>show off</h3>
                    <p><strong>Definition:</strong> To display one's abilities or possessions in an obvious way to impress others.</p>
                    <p><strong>Usage:</strong> Often has a negative connotation of being boastful or arrogant.</p>
                    <p class="example"><strong>Example:</strong> "He likes to show off his new car to all his friends."</p>
                </div>
            </div>
        </div>

        <!-- Fill in the Gaps Section -->
        <div id="fill-gaps" class="game-section">
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Word Bank - Choose from these words:</h3>
                <div class="word-options">
                    <span class="word-option">upload</span>
                    <span class="word-option">wear out</span>
                    <span class="word-option">waste</span>
                    <span class="word-option">weak</span>
                    <span class="word-option">show off</span>
                </div>
            </div>

            <div id="fill-gaps-container">
                <!-- Sentences will be dynamically inserted here -->
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
            <button class="reset-btn" onclick="resetFillBlanks()">Reset Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #2980b9;">Match the words with their definitions</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Vocabulary Words</h4>
                    <div class="match-item" data-word="upload" onclick="selectMatch(this)">upload</div>
                    <div class="match-item" data-word="wear out" onclick="selectMatch(this)">wear out</div>
                    <div class="match-item" data-word="waste" onclick="selectMatch(this)">waste</div>
                    <div class="match-item" data-word="weak" onclick="selectMatch(this)">weak</div>
                    <div class="match-item" data-word="show off" onclick="selectMatch(this)">show off</div>
                </div>
                <div class="match-column">
                    <h4>Definitions</h4>
                    <div id="meanings-container">
                        <!-- Meanings will be dynamically inserted here -->
                    </div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
            <button class="check-btn" onclick="checkMatching()">Check Matching</button>
            <button class="reset-btn" onclick="resetMatching()">Reset Matching</button>
        </div>

        <!-- Multiple Choice Section -->
        <div id="multiple-choice" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #2980b9;">Multiple Choice Questions</h2>
            
            <div class="question">
                <h3>1. What does it mean to "upload" something?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To delete files from a computer</div>
                    <div class="option" onclick="selectOption(this, true)">To transfer files to a remote server</div>
                    <div class="option" onclick="selectOption(this, false)">To print documents on paper</div>
                    <div class="option" onclick="selectOption(this, false)">To organize files in folders</div>
                </div>
                <div class="feedback" id="mc-feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>2. When something "wears out," what happens to it?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">It becomes more valuable</div>
                    <div class="option" onclick="selectOption(this, true)">It becomes damaged from use</div>
                    <div class="option" onclick="selectOption(this, false)">It changes color</div>
                    <div class="option" onclick="selectOption(this, false)">It increases in size</div>
                </div>
                <div class="feedback" id="mc-feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>3. Which action is an example of "waste"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Saving money for the future</div>
                    <div class="option" onclick="selectOption(this, true)">Spending hours on social media instead of studying</div>
                    <div class="option" onclick="selectOption(this, false)">Recycling paper and plastic</div>
                    <div class="option" onclick="selectOption(this, false)">Using energy-efficient appliances</div>
                </div>
                <div class="feedback" id="mc-feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>4. What does "weak" typically mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Very strong and powerful</div>
                    <div class="option" onclick="selectOption(this, true)">Lacking strength or energy</div>
                    <div class="option" onclick="selectOption(this, false)">Extremely intelligent</div>
                    <div class="option" onclick="selectOption(this, false)">Highly motivated</div>
                </div>
                <div class="feedback" id="mc-feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>5. What does it mean to "show off"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To hide one's abilities</div>
                    <div class="option" onclick="selectOption(this, true)">To display abilities to impress others</div>
                    <div class="option" onclick="selectOption(this, false)">To work quietly without recognition</div>
                    <div class="option" onclick="selectOption(this, false)">To help others without expecting anything</div>
                </div>
                <div class="feedback" id="mc-feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>6. Which sentence uses "upload" correctly?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">I need to upload this document from the printer</div>
                    <div class="option" onclick="selectOption(this, true)">I will upload the photos to my cloud storage</div>
                    <div class="option" onclick="selectOption(this, false)">Please upload the coffee from the kitchen</div>
                    <div class="option" onclick="selectOption(this, false)">He uploaded his shoes before going out</div>
                </div>
                <div class="feedback" id="mc-feedback-6" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>7. What is a synonym for "wear out"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Repair</div>
                    <div class="option" onclick="selectOption(this, true)">Deteriorate</div>
                    <div class="option" onclick="selectOption(this, false)">Strengthen</div>
                    <div class="option" onclick="selectOption(this, false)">Renew</div>
                </div>
                <div class="feedback" id="mc-feedback-7" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>8. Which is NOT a form of waste?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Wasting time</div>
                    <div class="option" onclick="selectOption(this, false)">Wasting money</div>
                    <div class="option" onclick="selectOption(this, true)">Wasting by recycling</div>
                    <div class="option" onclick="selectOption(this, false)">Wasting opportunities</div>
                </div>
                <div class="feedback" id="mc-feedback-8" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>9. What is the opposite of "weak"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, true)">Strong</div>
                    <div class="option" onclick="selectOption(this, false)">Tired</div>
                    <div class="option" onclick="selectOption(this, false)">Slow</div>
                    <div class="option" onclick="selectOption(this, false)">Quiet</div>
                </div>
                <div class="feedback" id="mc-feedback-9" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>10. Why might someone "show off"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To help others learn</div>
                    <div class="option" onclick="selectOption(this, true)">To gain admiration from others</div>
                    <div class="option" onclick="selectOption(this, false)">To complete work efficiently</div>
                    <div class="option" onclick="selectOption(this, false)">To solve problems quietly</div>
                </div>
                <div class="feedback" id="mc-feedback-10" style="display: none;"></div>
            </div>
            
            <button class="reset-btn" onclick="resetMultipleChoice()">Reset Answers</button>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];
        
        // Track correct answers for each section
        let fillBlanksCorrect = 0;
        let matchingCorrect = 0;
        let multipleChoiceCorrect = 0;
        
        // Definitions for the matching game
        const definitions = [
            { meaning: "upload", text: "To transfer files to a remote server or website" },
            { meaning: "wear out", text: "To become damaged or useless from prolonged use" },
            { meaning: "waste", text: "To use or expend carelessly or to no purpose" },
            { meaning: "weak", text: "Lacking physical strength or energy" },
            { meaning: "show off", text: "To display abilities to impress others" }
        ];

        // Sentences for the fill-in-the-blanks game
        const sentences = [
            { text: "I need to <input type='text' class='fill-blank' data-answer='upload' placeholder='answer'> these photos to my social media account.", answer: "upload" },
            { text: "My shoes have <input type='text' class='fill-blank' data-answer='worn out' placeholder='answer'> after two years of daily use.", answer: "worn out" },
            { text: "Don't <input type='text' class='fill-blank' data-answer='waste' placeholder='answer'> your time watching TV all day.", answer: "waste" },
            { text: "After being sick for a week, I still feel <input type='text' class='fill-blank' data-answer='weak' placeholder='answer'>.", answer: "weak" },
            { text: "He likes to <input type='text' class='fill-blank' data-answer='show off' placeholder='answer'> his new car to all his friends.", answer: "show off" },
            { text: "Please <input type='text' class='fill-blank' data-answer='upload' placeholder='answer'> the document to the shared drive so everyone can access it.", answer: "upload" },
            { text: "These old batteries have <input type='text' class='fill-blank' data-answer='worn out' placeholder='answer'> and need to be replaced.", answer: "worn out" },
            { text: "It's a <input type='text' class='fill-blank' data-answer='waste' placeholder='answer'> of money to buy things you don't need.", answer: "waste" },
            { text: "The signal is too <input type='text' class='fill-blank' data-answer='weak' placeholder='answer'> to make a phone call here.", answer: "weak" },
            { text: "She always tries to <input type='text' class='fill-blank' data-answer='show off' placeholder='answer'> her piano skills at parties.", answer: "show off" }
        ];

        // Function to shuffle array (Fisher-Yates algorithm)
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        // Initialize the fill-in-the-blanks game with shuffled sentences
        function initFillBlanks() {
            const container = document.getElementById('fill-gaps-container');
            container.innerHTML = '';
            
            // Shuffle the sentences
            const shuffledSentences = shuffleArray([...sentences]);
            
            // Create and append the sentence elements
            shuffledSentences.forEach((sentence, index) => {
                const div = document.createElement('div');
                div.className = 'question';
                div.innerHTML = `
                    <h3>Fill in the blank ${index + 1}:</h3>
                    <p>${sentence.text}</p>
                    <div class="feedback" id="feedback-${index + 1}" style="display: none;"></div>
                `;
                container.appendChild(div);
            });
        }

        // Initialize the matching game with shuffled definitions
        function initMatchingGame() {
            const meaningsContainer = document.getElementById('meanings-container');
            meaningsContainer.innerHTML = '';
            
            // Shuffle the definitions
            const shuffledDefinitions = shuffleArray([...definitions]);
            
            // Create and append the definition elements
            shuffledDefinitions.forEach(def => {
                const div = document.createElement('div');
                div.className = 'match-item';
                div.setAttribute('data-meaning', def.meaning);
                div.onclick = function() { selectMatch(this); };
                div.textContent = def.text;
                meaningsContainer.appendChild(div);
            });
        }

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
            
            // If showing fill-in-the-blanks section, reinitialize with shuffled sentences
            if (sectionId === 'fill-gaps') {
                initFillBlanks();
            }
            
            // If showing matching section, reinitialize with shuffled definitions
            if (sectionId === 'matching') {
                initMatchingGame();
                // Reset matching game state
                document.querySelectorAll('.match-item').forEach(item => {
                    item.classList.remove('selected', 'matched');
                });
                selectedWord = null;
                selectedMeaning = null;
                matchedPairs = [];
                document.getElementById('matching-feedback').style.display = 'none';
            }
            
            // Update score display
            updateScore();
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Show feedback for each question
                const feedback = document.getElementById(`feedback-${index+1}`);
                if (userAnswer === correctAnswer) {
                    feedback.textContent = '✅ Correct!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            fillBlanksCorrect = correctCount;
            updateScore();
        }

        function resetFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            blanks.forEach(blank => {
                blank.value = '';
                blank.classList.remove('correct', 'incorrect');
            });
            
            const feedbacks = document.querySelectorAll('#fill-gaps .feedback');
            feedbacks.forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            fillBlanksCorrect = 0;
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === definitions.length) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            matchingCorrect = matchedPairs.length;
            updateScore();
        }

        function checkMatching() {
            const allMatches = document.querySelectorAll('.match-item[data-word]');
            let allCorrect = true;
            
            allMatches.forEach(item => {
                if (!item.classList.contains('matched')) {
                    allCorrect = false;
                }
            });
            
            const feedback = document.getElementById('matching-feedback');
            if (allCorrect) {
                feedback.textContent = '🎉 Excellent! All matches are correct!';
                feedback.className = 'feedback correct';
            } else {
                const unmatchedCount = definitions.length - matchedPairs.length;
                feedback.textContent = `You have ${unmatchedCount} unmatched pair${unmatchedCount !== 1 ? 's' : ''}. Keep trying!`;
                feedback.className = 'feedback incorrect';
            }
            feedback.style.display = 'block';
        }

        function resetMatching() {
            document.querySelectorAll('.match-item').forEach(item => {
                item.classList.remove('selected', 'matched');
            });
            
            initMatchingGame();
            
            selectedWord = null;
            selectedMeaning = null;
            matchedPairs = [];
            
            document.getElementById('matching-feedback').style.display = 'none';
            
            matchingCorrect = 0;
            updateScore();
        }

        function selectOption(element, isCorrect) {
            // Remove selection from all options in this question
            const options = element.parentElement.querySelectorAll('.option');
            options.forEach(opt => {
                opt.classList.remove('selected');
                opt.classList.remove('correct');
                opt.classList.remove('incorrect');
            });
            
            // Mark the selected option
            element.classList.add('selected');
            
            const questionNumber = element.closest('.question').querySelector('h3').textContent.match(/\d+/)[0];
            const feedback = document.getElementById(`mc-feedback-${questionNumber}`);
            
            if (isCorrect) {
                element.classList.add('correct');
                feedback.textContent = '✅ Correct!';
                feedback.className = 'feedback correct';
            } else {
                element.classList.add('incorrect');
                feedback.textContent = '❌ Incorrect. Try again.';
                feedback.className = 'feedback incorrect';
                
                // Show the correct answer
                options.forEach(opt => {
                    if (opt.onclick.toString().includes('true')) {
                        opt.classList.add('correct');
                    }
                });
            }
            
            feedback.style.display = 'block';
            
            // Count correct answers in multiple choice
            multipleChoiceCorrect = document.querySelectorAll('#multiple-choice .option.correct.selected').length;
            updateScore();
        }

        function resetMultipleChoice() {
            document.querySelectorAll('#multiple-choice .option').forEach(option => {
                option.classList.remove('selected', 'correct', 'incorrect');
            });
            
            document.querySelectorAll('#multiple-choice .feedback').forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            multipleChoiceCorrect = 0;
            updateScore();
        }

        function updateScore() {
            // Total score from all sections
            score = fillBlanksCorrect + matchingCorrect + multipleChoiceCorrect;
            document.getElementById('score').textContent = score;
        }
        
        // Initialize the page
        window.onload = function() {
            initFillBlanks();
            initMatchingGame();
        }
    </script>
</body>
</html>
