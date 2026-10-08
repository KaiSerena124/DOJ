<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DOJ Grande City - Department of Justice</title>
    <style>
        :root {
            --bg-main: #0b0f19;
            --bg-card: #131c2e;
            --bg-input: #1a2640;
            --accent-gold: #c5a059;
            --accent-gold-hover: #d4af37;
            --text-light: #f3f4f6;
            --text-muted: #9ca3af;
            --success: #059669;
            --danger: #dc2626;
            --border: #2a3b5c;
        }

        body {
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
            background-color: var(--bg-main);
            color: var(--text-light);
            margin: 0;
            padding: 30px;
        }

        .container {
            max-width: 950px;
            margin: 0 auto;
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 12px;
            box-shadow: 0 12px 32px rgba(0,0,0,0.7);
            overflow: hidden;
        }

        .top-bar {
            background: linear-gradient(135deg, #0f172a, #1e293b);
            border-bottom: 2px solid var(--accent-gold);
            padding: 20px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .brand-title {
            margin: 0;
            font-size: 22px;
            font-weight: 700;
            letter-spacing: 1px;
            color: var(--text-light);
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .brand-title span {
            color: var(--accent-gold);
        }

        .nav-buttons {
            display: flex;
            gap: 12px;
        }

        button {
            background-color: var(--accent-gold);
            color: #000;
            border: none;
            padding: 10px 18px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 14px;
            font-weight: 600;
            transition: all 0.2s ease;
        }

        button:hover {
            background-color: var(--accent-gold-hover);
            transform: translateY(-1px);
        }

        .btn-secondary {
            background-color: transparent;
            color: var(--text-light);
            border: 1px solid var(--border);
        }

        .btn-secondary:hover {
            background-color: rgba(255,255,255,0.05);
            border-color: var(--accent-gold);
        }

        .btn-danger {
            background-color: var(--danger);
            color: white;
        }

        .btn-danger:hover {
            background-color: #b91c1c;
        }

        .content-body {
            padding: 30px;
        }

        h2, h3 {
            color: var(--text-light);
            border-bottom: 1px solid var(--border);
            padding-bottom: 12px;
            margin-top: 0;
        }

        input, textarea, select {
            width: 100%;
            padding: 12px;
            margin: 8px 0 20px 0;
            background: var(--bg-input);
            border: 1px solid var(--border);
            color: var(--text-light);
            border-radius: 6px;
            box-sizing: border-box;
            font-size: 14px;
        }

        input:focus, textarea:focus, select:focus {
            outline: none;
            border-color: var(--accent-gold);
        }

        .hidden {
            display: none !important;
        }

        .question-card {
            background: rgba(26, 38, 64, 0.4);
            border: 1px solid var(--border);
            padding: 24px;
            border-radius: 8px;
            margin-bottom: 20px;
        }

        .options-list label {
            display: flex;
            align-items: center;
            background: var(--bg-input);
            border: 1px solid var(--border);
            padding: 12px 16px;
            margin: 8px 0;
            border-radius: 6px;
            cursor: pointer;
            transition: border-color 0.2s;
        }

        .options-list label:hover {
            border-color: var(--accent-gold);
        }

        .options-list input[type="radio"] {
            width: auto;
            margin: 0 12px 0 0;
            accent-color: var(--accent-gold);
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 15px;
        }

        th, td {
            border: 1px solid var(--border);
            padding: 12px;
            text-align: left;
            font-size: 14px;
        }

        th {
            background-color: var(--bg-input);
            color: var(--accent-gold);
        }

        .badge {
            padding: 5px 10px;
            border-radius: 4px;
            font-weight: 600;
            font-size: 12px;
        }
        .badge-success { background: var(--success); color: white; }
        .badge-danger { background: var(--danger); color: white; }

        .info-box {
            background: rgba(197, 160, 89, 0.1);
            border-left: 4px solid var(--accent-gold);
            padding: 15px;
            border-radius: 4px;
            margin-bottom: 20px;
            color: var(--text-muted);
            font-size: 14px;
        }
    </style>
</head>
<body>

<div class="container">
    <div class="top-bar">
        <h1 class="brand-title">🏛️ DOJ <span>GRANDE CITY</span></h1>
        <div class="nav-buttons">
            <button class="btn-secondary" onclick="switchView('userView')">Prüfung ablegen</button>
            <button class="btn-secondary" onclick="switchView('loginView')">Admin Portal</button>
        </div>
    </div>

    <div class="content-body">
        <!-- ANSICHT 1: BENUTZER / PRÜFUNG -->
        <div id="userView" class="view">
            <h2>Staatliche Prüfung – Department of Justice</h2>
            <div id="userStartScreen">
                <div class="info-box">
                    Willkommen beim offiziellen Rekrutierungs- und Prüfungssystem von DOJ Grande City. 
                    Dir werden zufällig <strong>15 Fragen</strong> aus unserem Archiv vorgelegt. 
                    Zum Bestehen der Prüfung sind mindestens <strong>80%</strong> (12 von 15 richtige Antworten) erforderlich.
                </div>
                <label>Vollständiger Name (IC):</label>
                <input type="text" id="candidateName" placeholder="Geben Sie Ihren Vor- und Nachnamen ein...">
                <button onclick="startTest()">Prüfung starten</button>
            </div>

            <div id="userTestScreen" class="hidden">
                <div id="quizContainer"></div>
                <button onclick="submitTest()">Prüfung einreichen</button>
            </div>

            <div id="userResultScreen" class="hidden">
                <h3>Prüfungsauswertung</h3>
                <div id="resultText" style="margin: 20px 0; font-size: 16px; line-height: 1.6;"></div>
                <button onclick="resetUserView()">Zurück zum Hauptmenü</button>
            </div>
        </div>

        <!-- ANSICHT 2: ADMIN LOGIN -->
        <div id="loginView" class="view hidden">
            <h2>Admin Authentifizierung</h2>
            <div class="info-box">Bitte geben Sie Ihre Administrator-Zugangsdaten ein, um fortzufahren.</div>
            
            <label>Benutzername:</label>
            <input type="text" id="adminUser" placeholder="Benutzername eingeben..." autocomplete="off" value="">
            
            <label>Passwort:</label>
            <input type="password" id="adminPass" placeholder="Passwort eingeben..." autocomplete="new-password" value="">
            
            <button onclick="checkLogin()">Einloggen</button>
        </div>

        <!-- ANSICHT 3: ADMIN DASHBOARD -->
        <div id="adminView" class="view hidden">
            <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px;">
                <h2>Admin Management-Konsole</h2>
                <button class="btn-danger" onclick="logoutAdmin()">Abmelden</button>
            </div>
            
            <div style="background: rgba(26, 38, 64, 0.4); border: 1px solid var(--border); padding: 20px; border-radius: 8px; margin-bottom: 30px;">
                <h3>Frage zum Archiv hinzufügen (Über 60 möglich)</h3>
                <label>Fragetext:</label>
                <textarea id="newQuestionText" rows="2" placeholder="Geben Sie hier den Gesetzestext oder die Situation ein..."></textarea>
                
                <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px;">
                    <div>
                        <label>Option A:</label>
                        <input type="text" id="optA" placeholder="Antwortmöglichkeit A">
                        <label>Option B:</label>
                        <input type="text" id="optB" placeholder="Antwortmöglichkeit B">
                    </div>
                    <div>
                        <label>Option C:</label>
                        <input type="text" id="optC" placeholder="Antwortmöglichkeit C">
                        <label>Option D:</label>
                        <input type="text" id="optD" placeholder="Antwortmöglichkeit D">
                    </div>
                </div>

                <label>Richtige Antwort:</label>
                <select id="correctOpt">
                    <option value="0">Option A</option>
                    <option value="1">Option B</option>
                    <option value="2">Option C</option>
                    <option value="3">Option D</option>
                </select>
                <button onclick="addQuestion()">Frage speichern</button>
            </div>

            <h3>Aktive Fragen im DOJ-Archiv (<span id="questionCount">0</span>)</h3>
            <table>
                <thead>
                    <tr>
                        <th style="width: 50px;">#</th>
                        <th>Fragetext</th>
                        <th style="width: 100px;">Aktion</th>
                    </tr>
                </thead>
                <tbody id="adminQuestionTable">
                    <!-- Wird dynamisch gefüllt -->
                </tbody>
            </table>
        </div>
    </div>
</div>

<script>
    // Initialisiere Standard-Fragen beim ersten Start (über 60 Fragen für optimalen Pool)
    if (!localStorage.getItem('doj_questions') || JSON.parse(localStorage.getItem('doj_questions')).length < 60) {
        const initialQuestions = [];
        for(let i = 1; i <= 65; i++) {
            initialQuestions.push({
                text: `[DOJ Gesetzbuch] Frage ${i}: Welches Vorgehen ist in dieser rechtlichen Situation korrekt?`,
                options: [
                    `Korrekte rechtliche Handlungsweise für Frage ${i}`,
                    `Unzulässige Vorgehensweise B`,
                    `Fehlerhafte Maßnahme C`,
                    `Nicht rechtmäßige Option D`
                ],
                correct: 0
            });
        }
        localStorage.setItem('doj_questions', JSON.stringify(initialQuestions));
    }

    let activeTestQuestions = [];
    let candidateAnswers = {};

    function switchView(viewId) {
        document.querySelectorAll('.view').forEach(v => v.classList.add('hidden'));
        document.getElementById(viewId).classList.remove('hidden');
        
        if(viewId === 'loginView') {
            document.getElementById('adminUser').value = '';
            document.getElementById('adminPass').value = '';
        }
        if(viewId === 'adminView') {
            loadAdminQuestions();
        }
    }

    // --- ADMIN LOGIK ---
    function checkLogin() {
        const user = document.getElementById('adminUser').value.trim();
        const pass = document.getElementById('adminPass').value.trim();

        if(user === "Doj1" && pass === "starko") {
            switchView('adminView');
        } else {
            alert("Zugriff verweigert: Ungültige Anmeldedaten.");
            document.getElementById('adminPass').value = '';
        }
    }

    function logoutAdmin() {
        switchView('userView');
    }

    function loadAdminQuestions() {
        const questions = JSON.parse(localStorage.getItem('doj_questions')) || [];
        document.getElementById('questionCount').innerText = questions.length;
        const tbody = document.getElementById('adminQuestionTable');
        tbody.innerHTML = '';

        questions.forEach((q, index) => {
            let tr = document.createElement('tr');
            tr.innerHTML = `
                <td>${index + 1}</td>
                <td>${q.text}</td>
                <td><button class="btn-danger" style="padding: 6px 12px; font-size: 12px;" onclick="deleteQuestion(${index})">Löschen</button></td>
            `;
            tbody.appendChild(tr);
        });
    }

    function addQuestion() {
        const text = document.getElementById('newQuestionText').value;
        const optA = document.getElementById('optA').value;
        const optB = document.getElementById('optB').value;
        const optC = document.getElementById('optC').value;
        const optD = document.getElementById('optD').value;
        const correct = parseInt(document.getElementById('correctOpt').value);

        if(!text.trim() || !optA.trim() || !optB.trim() || !optC.trim() || !optD.trim()) {
            alert("Bitte füllen Sie alle erforderlichen Felder aus.");
            return;
        }

        let questions = JSON.parse(localStorage.getItem('doj_questions')) || [];
        questions.push({
            text: text,
            options: [optA, optB, optC, optD],
            correct: correct
        });

        localStorage.setItem('doj_questions', JSON.stringify(questions));
        
        document.getElementById('newQuestionText').value = '';
        document.getElementById('optA').value = '';
        document.getElementById('optB').value = '';
        document.getElementById('optC').value = '';
        document.getElementById('optD').value = '';

        loadAdminQuestions();
        alert("Frage erfolgreich im DOJ-Archiv gespeichert.");
    }

    function deleteQuestion(index) {
        let questions = JSON.parse(localStorage.getItem('doj_questions')) || [];
        if(questions.length <= 15) {
            alert("Das Archiv muss mindestens 15 Fragen enthalten!");
            return;
        }
        if(confirm("Möchten Sie diese Frage permanent aus dem Archiv löschen?")) {
            questions.splice(index, 1);
            localStorage.setItem('doj_questions', JSON.stringify(questions));
            loadAdminQuestions();
        }
    }

    // --- BENUTZER / PRÜFUNGS-LOGIK ---
    function startTest() {
        const name = document.getElementById('candidateName').value;
        if(!name.trim()) {
            alert("Bitte tragen Sie Ihren Namen ein.");
            return;
        }

        let questions = JSON.parse(localStorage.getItem('doj_questions')) || [];
        if(questions.length < 15) {
            alert(`Das Archiv enthält zur Zeit erst ${questions.length} Fragen. Der Admin muss mindestens 15 Fragen hinterlegen.`);
            return;
        }

        let shuffled = [...questions].sort(() => 0.5 - Math.random());
        activeTestQuestions = shuffled.slice(0, 15);
        candidateAnswers = {};

        document.getElementById('userStartScreen').classList.add('hidden');
        document.getElementById('userTestScreen').classList.remove('hidden');

        let container = document.getElementById('quizContainer');
        container.innerHTML = '';

        activeTestQuestions.forEach((q, qIndex) => {
            let card = document.createElement('div');
            card.className = 'question-card';
            
            let optionsHtml = '';
            q.options.forEach((opt, oIndex) => {
                optionsHtml += `
                    <label>
                        <input type="radio" name="question_${qIndex}" value="${oIndex}" onchange="saveAnswer(${qIndex}, ${oIndex})">
                        ${opt}
                    </label>
                `;
            });

            card.innerHTML = `
                <p style="color: var(--accent-gold); margin-top:0;"><strong>Frage ${qIndex + 1} von 15</strong></p>
                <p style="font-size: 16px; font-weight: 500;">${q.text}</p>
                <div class="options-list">${optionsHtml}</div>
            `;
            container.appendChild(card);
        });
    }

    function saveAnswer(qIndex, optionIndex) {
        candidateAnswers[qIndex] = optionIndex;
    }

    function submitTest() {
        if(Object.keys(candidateAnswers).length < 15) {
            if(!confirm("Sie haben noch nicht alle Fragen beantwortet. Möchten Sie die Prüfung dennoch einreichen?")) {
                return;
            }
        }

        let correctCount = 0;
        activeTestQuestions.forEach((q, index) => {
            if(candidateAnswers[index] === q.correct) {
                correctCount++;
            }
        });

        let percentage = (correctCount / 15) * 100;
        let passed = percentage >= 80;

        document.getElementById('userTestScreen').classList.add('hidden');
        document.getElementById('userResultScreen').classList.remove('hidden');

        let resultHTML = `
            <p><strong>Kandidat:</strong> ${document.getElementById('candidateName').value}</p>
            <p><strong>Ergebnis:</strong> ${correctCount} von 15 Fragen korrekt (${percentage.toFixed(1)}%)</p>
            <p><strong>Status:</strong> <span class="badge ${passed ? 'badge-success' : 'badge-danger'}">${passed ? 'BESTANDEN' : 'NICHT BESTANDEN'}</span></p>
            <p style="color: var(--text-muted); font-size: 13px; margin-top: 15px;">Hinweis: Zum Bestehen waren mindestens 80% (12 korrekte Antworten) erforderlich.</p>
        `;
        document.getElementById('resultText').innerHTML = resultHTML;
    }

    function resetUserView() {
        document.getElementById('userResultScreen').classList.add('hidden');
        document.getElementById('userStartScreen').classList.remove('hidden');
        document.getElementById('candidateName').value = '';
    }
</script>

</body>
</html>
