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

        header {
            background: linear-gradient(135deg, #111827, #1f2937);
            padding: 25px 30px;
            border-bottom: 2px solid var(--accent-gold);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        header h1 {
            margin: 0;
            font-size: 24px;
            color: var(--accent-gold);
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .content {
            padding: 30px;
        }

        .btn {
            background-color: var(--accent-gold);
            color: #000;
            font-weight: bold;
            border: none;
            padding: 12px 20px;
            border-radius: 6px;
            cursor: pointer;
            transition: background 0.2s;
        }

        .btn:hover {
            background-color: var(--accent-gold-hover);
        }

        .btn-danger {
            background-color: var(--danger);
            color: #fff;
        }

        input, select {
            width: 100%;
            padding: 12px;
            background: var(--bg-input);
            border: 1px solid var(--border);
            border-radius: 6px;
            color: var(--text-light);
            margin-bottom: 15px;
            box-sizing: border-box;
        }

        .hidden {
            display: none !important;
        }

        .admin-badge {
            background: var(--danger);
            color: white;
            padding: 4px 10px;
            border-radius: 4px;
            font-size: 12px;
            font-weight: bold;
        }

        .card {
            background: rgba(26, 38, 64, 0.5);
            border: 1px solid var(--border);
            padding: 20px;
            border-radius: 8px;
            margin-bottom: 20px;
        }

        .question-box {
            margin-bottom: 25px;
            padding-bottom: 15px;
            border-bottom: 1px solid var(--border);
        }

        .modal {
            max-width: 400px;
            margin: 30px auto;
            background: var(--bg-card);
            padding: 20px;
            border-radius: 8px;
            border: 1px solid var(--border);
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 15px;
        }

        th, td {
            border: 1px solid var(--border);
            padding: 10px;
            text-align: left;
        }

        th {
            background: var(--bg-input);
            color: var(--accent-gold);
        }
    </style>
</head>
<body>

    <div class="container">
        <header>
            <div>
                <h1>DOJ Grande City</h1>
                <p style="margin: 5px 0 0 0; color: var(--text-muted); font-size: 14px;">Department of Justice – Prüfungssystem</p>
            </div>
            <div id="header-status">
                <button class="btn" onclick="openLoginModal()">Admin Portal</button>
            </div>
        </header>

        <div class="content">
            <!-- Öffentlicher Bereich / Prüfung -->
            <div id="user-view">
                <div class="card" id="start-screen">
                    <h2>Offizielle DOJ Einstellungsprüfung</h2>
                    <p>Willkommen beim Prüfungsportal von Grande City. Dir werden zufällig 15 Fragen aus unserem Fragenkatalog gestellt. Zum Bestehen sind mindestens 80% (12 von 15 Punkten) erforderlich.</p>
                    <input type="text" id="applicant-name" placeholder="Dein vollständiger Name / Ingame-Name" style="max-width: 400px;">
                    <br>
                    <button class="btn" onclick="startExam()">Prüfung starten</button>
                </div>

                <div id="exam-screen" class="hidden">
                    <h3 id="exam-title">Prüfung läuft...</h3>
                    <div id="questions-container"></div>
                    <button class="btn" onclick="submitExam()">Prüfung abgeben & auswerten</button>
                </div>

                <div id="result-screen" class="hidden">
                    <div class="card" id="result-card">
                        <h2>Prüfungsergebnis</h2>
                        <p id="result-text" style="font-size: 18px; font-weight: bold;"></p>
                        <button class="btn" onclick="location.reload()">Zurück zur Startseite</button>
                    </div>
                </div>
            </div>

            <!-- Admin-Dashboard -->
            <div id="admin-view" class="hidden">
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px;">
                    <h2>Admin-Dashboard</h2>
                    <span class="admin-badge">ADMIN AKTIV</span>
                </div>
                <div class="card">
                    <h3>Fragenkatalog verwalten (Gesamt: <span id="question-count">0</span>)</h3>
                    <p>Hier kannst du Fragen hinzufügen oder löschen. Die Änderungen werden direkt im Browser gespeichert.</p>
                    
                    <div style="background: var(--bg-input); padding: 15px; border-radius: 6px; margin-bottom: 20px;">
                        <h4>Neue Frage hinzufügen</h4>
                        <input type="text" id="new-q-text" placeholder="Fragetext eingeben...">
                        <input type="text" id="new-q-opt1" placeholder="Antwortmöglichkeit A">
                        <input type="text" id="new-q-opt2" placeholder="Antwortmöglichkeit B">
                        <input type="text" id="new-q-opt3" placeholder="Antwortmöglichkeit C">
                        <select id="new-q-correct">
                            <option value="0">Richtige Antwort: A</option>
                            <option value="1">Richtige Antwort: B</option>
                            <option value="2">Richtige Antwort: C</option>
                        </select>
                        <button class="btn" onclick="addNewQuestion()">Frage hinzufügen</button>
                    </div>

                    <h4>Vorhandene Fragen</h4>
                    <div id="admin-question-list" style="max-height: 400px; overflow-y: auto;"></div>

                    <br>
                    <button class="btn btn-danger" onclick="adminLogout()">Admin abmelden</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Login Modal -->
    <div id="login-section" class="modal hidden" style="margin-top: 20px;">
        <h3>Admin Login</h3>
        <input type="text" id="username" placeholder="Benutzername (Doj1)">
        <input type="password" id="password" placeholder="Passwort (starko)">
        <button class="btn" onclick="performLogin()">Einloggen</button>
        <button class="btn" style="background: transparent; color: var(--text-muted); margin-top: 10px;" onclick="closeLoginModal()">Abbrechen</button>
    </div>

    <script>
        // Standard-Fragenkatalog (über 60 Fragen als Basis)
        const defaultQuestions = [
            { q: "Was ist die Hauptaufgabe des Department of Justice?", options: ["Polizeistreifen fahren", "Die Einhaltung von Gesetzen und Vertretung der Justiz", "Fahrzeugtuning verkaufen"], correct: 1 },
            { q: "Wann darf von der Schusswaffe gebrauch gemacht werden?", options: ["Immer bei Flucht", "Nur bei unmittelbarer Eigen- oder Fremdgefährdung", "Gar nicht"], correct: 1 },
            { q: "Wer ist der oberste Dienstherr im Justizministerium?", options: ["Der Chief of Police", "Der Minister / Attorney General / Richter", "Der Autohändler"], correct: 1 },
            { q: "Was bedeutet die Unschuldsvermutung?", options: ["Jeder ist schuldig bis zum Beweis des Gegenteils", "Jeder gilt solange als unschuldig, bis die Schuld bewiesen ist", "Es gibt keine Gesetze"], correct: 1 },
            { q: "Wie ist bei einer Festnahme vorzugehen?", options: ["Direkt wegsperren", "Rights verlesen (Miranda Warnings) und Grund nennen", "Erst fragen, dann schlagen"], correct: 1 },
            { q: "Was versteht man unter einer Durchsuchung ohne Durchsuchungsbefehl?", options: ["Ist grundsätzlich immer verboten", "Nur in akuten Gefahr-im-Verzug-Situationen zulässig", "Erlaubt bei jedem Verdacht"], correct: 1 },
            { q: "Welche Strafe droht bei Meineid vor Gericht?", options: ["Eine mündliche Verwarnung", "Harte Freiheitsstrafe / Justizstrafe", "Gar nichts"], correct: 1 },
            { q: "Was ist ein Haftbefehl?", options: ["Ein Einkaufszettel", "Eine richterliche Anordnung zur Festnahme", "Ein Strafzettel fürs Parken"], correct: 1 },
            { q: "Wie verhält man sich im Gerichtssaal gegenüber dem Richter?", options: ["Respektvoll und auf Anweisung aufstehen", "Rauchen und reinrufen", "Laut Musik hören"], correct: 0 },
            { q: "Darf Beweismaterial gefälscht werden?", options: ["Ja, wenn man den Täter unbedingt will", "Nein, niemals, das ist Amtsmissbrauch", "Nur am Wochenende"], correct: 1 },
            { q: "Was ist die Aufgabe eines Anwalts?", options: ["Den Mandanten bestmöglich vor Gericht zu verteidigen", "Polizeiarbeit behindern", "Strafen selbst festlegen"], correct: 0 },
            { q: "Was bedeutet 'Gefahr im Verzug'?", options: ["Es eilt so sehr, dass auf richterliche Erlaubnis nicht gewartet werden kann", "Es ist Feierabend", "Niemand ist in Gefahr"], correct: 0 },
            { q: "Wer darf Urteile fällen?", options: ["Jeder Polizist", "Ausschließlich der zuständige Richter", "Der Bürgermeister allein"], correct: 1 },
            { q: "Wie lange darf eine Person maximal vorläufig festgehalten werden ohne Anhörung (Standard)?", options: ["1 Woche", "Bis zu einem gesetzlich festgelegten Zeitraum laut Serverregeln", "Einen Monat"], correct: 1 },
            { q: "Was ist Bestechlichkeit im Amt?", options: ["Geld oder Vorteile für Amtshandlungen anzunehmen", "Trinkgeld im Restaurant", "Gute Arbeit leisten"], correct: 0 },
            { q: "Darf ein Zeuge zur Aussage gezwungen werden?", options: ["Ja, rechtlich vorgeschrieben", "Nein, niemals", "Nur wenn er Lust hat"], correct: 0 },
            { q: "Was versteht man unter Notwehr?",options: ["Angriff auf andere", "Abwehr eines gegenwärtigen, rechtswidrigen Angriffs", "Streit auf der Straße"], correct: 1 },
            { q: "Welche Sprache wird im Gerichtssaal primär gesprochen?", options: ["Fiktive Zeichensprache", "Deutsch / Amtssprache", "Englisch ausschließlich"], correct: 1 },
            { q: "Was ist ein Präzedenzfall?", options: ["Ein Unfall", "Ein früheres Gerichtsurteil als Richtlinie", "Ein Autotyp"], correct: 1 },
            { q: "Wer vertritt den Staat bei Straftaten?", options: ["Der Angeklagte", "Die Staatsanwaltschaft (Prosecution)", "Der Abschleppdienst"], correct: 1 },
            { q: "Was ist Amtsmissbrauch?", options: ["Befugnisse der Position illegal auszunutzen", "Zu spät zur Arbeit kommen", "Kaffee verschütten"], correct: 0 },
            { q: "Was bedeutet 'In dubio pro reo'?", options: ["Im Zweifel für den Angeklagten", "Im Zweifel für den Staat", "Es gibt keine Zweifel"], correct: 0 },
            { q: "Darf man während einer Verhandlung telefonieren?", options: ["Ja, laut laut", "Nein, striktes Verbot im Gerichtssaal", "Nur mit Kopfhörern"], correct: 1 },
            { q: "Was ist ein Beweismittel?", options: ["Jedes Objekt oder Zeugnis zur Tataufklärung", "Ein privates Foto", "Eine Meinung"], correct: 0 },
            { q: "Wer stellt den Gerichtsschutz (Bailiff / Security)?", options: ["Der Richter selbst", "Autorisierte Sicherheitskräfte / Justizwache", "Niemand"], correct: 1 },
            { q: "Was ist eine Geldstrafe?", options: ["Ein Geschenk", "Eine finanzielle Sanktion bei Vergehen", "Steuergeld"], correct: 1 },
            { q: "Was ist eine Bewährungsstrafe?", options: ["Freiheitsstrafe, die zur Bewährung ausgesetzt wird", "Sofortiger Gefängnisaufenthalt", "Freispruch"], correct: 0 },
            { q: "Darf Beweismittel unterschlagen werden?", options: ["Ja", "Nein, das ist Beweismittelvernichtung", "Manchmal"], correct: 1 },
            { q: "Wer ernennt neue Richter?", options: ["Die Regierung / Justizleitung", "Jeder Bürger", "Die Polizei"], correct: 0 },
            { q: "Was ist eine Klage?", options: ["Ein offizieller Rechtsanspruch vor Gericht", "Ein Beschwerdebrief", "Ein Autokauf"], correct: 0 },
            { q: "Was bedeutet Vertraulichkeit im Justizdienst?", options: ["Geheimhaltung von internen Akten", "Alles auf Twitter posten", "Mit Freunden teilen"], correct: 0 },
            { q: "Was ist ein Geständnis?", options: ["Das Einräumen der Tat", "Eine Lüge", "Eine Ausrede"], correct: 0 },
            { q: "Darf ein Polizist als Richter fungieren?", options: ["Ja", "Nein, Gewaltenteilung muss gewahrt werden", "Wenn kein Richter da ist"], correct: 1 },
            { q: "Was ist Korruption?", options: ["Illegale Vorteilsnahme", "Gute Teamarbeit", "Überstunden"], correct: 0 },
            { q: "Was bedeutet Gewaltenteilung?", options: ["Trennung von Legislative, Exekutive und Judikative", "Alles wird von einer Person gemacht", "Kampfsport im Dienst"], correct: 0 },
            { q: "Wie verhält man sich bei einer Dienstbesprechung?", options: ["Aufmerksam zuhören und Anweisungen befolgen", "Schlafen", "Weggehen"], correct: 0 },
            { q: "Was ist ein Freispruch?", options: ["Verurteilung", "Gerichtliche Feststellung der Unschuld", "Geldstrafe"], correct: 1 },
            { q: "Darf man Beweise erpressen?", options: ["Ja", "Nein, illegal erlangte Beweise sind ungültig", "Nur bei schweren Fällen"], correct: 1 },
            { q: "Was ist ein Zeuge?", options: ["Eine Person, die das Geschehen beobachtet hat", "Der Täter", "Der Richter"], correct: 0 },
            { q: "Was ist ein Tatort?", options: ["Der Ort, an dem die Straftat begangen wurde", "Ein Kino", "Eine Werkstatt"], correct: 0 },
            { q: "Was bedeutet Dienstgeheimnis?", options: ["Interne Infos dürfen nicht nach außen", "Jeder darf alles wissen", "Öffentliche News"], correct: 0 },
            { q: "Was ist ein Urteil?", options: ["Die offizielle Entscheidung des Gerichts", "Eine Idee", "Ein Vorschlag"], correct: 0 },
            { q: "Darf man Waffen im Gerichtssaal tragen (als Zivilist)?", options: ["Ja, immer", "Nein, striktes Waffenverbot", "Nur kleine Pistolen"], correct: 1 },
            { q: "Was ist eine Berufung?", options: ["Ein Rechtsmittel gegen ein Urteil", "Ein Anruf", "Ein Jobwechsel"], correct: 0 },
            { q: "Wer führt Protokoll bei Gerichtsverhandlungen?", options: ["Der Protokollant / Schreiber", "Der Verdächtige", "Niemand"], correct: 0 },
            { q: "Was ist ein Verbrechen?", options: ["Eine schwerwiegende Straftat", "Zu schnelles Gehen", "Falsch parken"], correct: 0 },
            { q: "Was ist ein Vergehen?", options: ["Eine leichtere Straftat", "Mord", "Raubüberfall"], correct: 0 },
            { q: "Darf ein Richter befangen sein?", options: ["Ja", "Nein, Richter müssen unparteiisch sein", "Egal"], correct: 1 },
            { q: "Was ist das Strafregister?", options: ["Sammlung von Vorstrafen", "Ein Kochbuch", "Telefonliste"], correct: 0 },
            { q: "Was bedeutet Akteneinsicht?", options: ["Das Recht, Falldokumente einzusehen", "Akte verbrennen", "Akte verstecken"], correct: 0 },
            { q: "Wer überwacht die Einhaltung der Menschenrechte?", options: ["Das DOJ und internationale Standards", "Niemand", "Autohändler"], correct: 0 },
            { q: "Was ist eine Vernehmung?",options: ["Befragung durch Behörden", "Ein Verhör mit Gewalt", "Ein Kaffeekränzchen"], correct: 0 },
            { q: "Darf ein Beschuldigter schweigen?", options: ["Nein, er muss reden", "Ja, das Recht auf Schweigen (Right to remain silent)", "Nur wenn er müde ist"], correct: 1 },
            { q: "Was ist Justizvollzug?", options: ["Der Vollzug von Freiheitsstrafen", "Freizeitpark", "Polizeiarbeit"], correct: 0 },
            { q: "Was ist ein Durchsuchungsbefehl?", options: ["Richterliche Erlaubnis zur Durchsuchung", "Einkaufszettel", "Führerschein"], correct: 0 },
            { q: "Wer unterschreibt offizielle Haftbefehle?", options: ["Ein Richter", "Ein Praktikant", "Der Verdächtige"], correct: 0 },
            { q: "Was ist eine Zeugenaussage?", options: ["Aussage unter Wahrheitspflicht", "Eine Vermutung", "Ein Gerücht"], correct: 0 },
            { q: "Darf man im Gericht essen?", options: ["Ja, ganze Menüs", "Nein, untersagt", "Nur Süßigkeiten"], correct: 1 },
            { q: "Was ist ein Justiziar?", options: ["Ein Rechtsberater", "Ein Polizist", "Ein Mechaniker"], correct: 0 },
            { q: "Was bedeutet Gesetzeshilfe?", options: ["Unterstützung der Justiz", "Gesetze brechen", "Gesetze ignorieren"], correct: 0 },
            { q: "Wie ist die Kleiderordnung im Gericht?", options: ["Formell / Anzug", "Badekleidung", "Jogginghose"], correct: 0 }
        ];

        let questions = JSON.parse(localStorage.getItem('doj_questions')) || defaultQuestions;
        let activeExamQuestions = [];

        // Admin Session beim Laden prüfen
        window.addEventListener('DOMContentLoaded', () => {
            const isAdmin = sessionStorage.getItem('doj_admin_logged_in');
            if (isAdmin === 'true') {
                showAdminView();
            }
        });

        function openLoginModal() {
            document.getElementById('login-section').classList.remove('hidden');
        }

        function closeLoginModal() {
            document.getElementById('login-section').classList.add('hidden');
        }

        function performLogin() {
            const user = document.getElementById('username').value;
            const pass = document.getElementById('password').value;

            if (user === 'Doj1' && pass === 'starko') {
                sessionStorage.setItem('doj_admin_logged_in', 'true');
                closeLoginModal();
                showAdminView();
            } else {
                alert('Falsche Anmeldedaten!');
            }
        }

        function showAdminView() {
            document.getElementById('user-view').classList.add('hidden');
            document.getElementById('admin-view').classList.remove('hidden');
            document.getElementById('login-section').classList.add('hidden');
            document.getElementById('header-status').innerHTML = '<span class="admin-badge">Admin Modus</span>';
            renderAdminQuestions();
        }

        function adminLogout() {
            sessionStorage.removeItem('doj_admin_logged_in');
            document.getElementById('admin-view').classList.add('hidden');
            document.getElementById('user-view').classList.remove('hidden');
            document.getElementById('header-status').innerHTML = '<button class="btn" onclick="openLoginModal()">Admin Portal</button>';
        }

        function startExam() {
            const name = document.getElementById('applicant-name').value.trim();
            if (!name) {
                alert('Bitte gib deinen Namen ein!');
                return;
            }

            // 15 zufällige Fragen auswählen
            let shuffled = [...questions].sort(() => 0.5 - Math.random());
            activeExamQuestions = shuffled.slice(0, 15);

            let container = document.getElementById('questions-container');
            container.innerHTML = '';

            activeExamQuestions.forEach((item, index) => {
                let box = document.createElement('div');
                box.className = 'question-box';
                box.innerHTML = `
                    <label><strong>${index + 1}. ${item.q}</strong></label><br>
                    <select id="question-${index}">
                        <option value="">Bitte wählen...</option>
                        <option value="0">${item.options[0]}</option>
                        <option value="1">${item.options[1]}</option>
                        <option value="2">${item.options[2]}</option>
                    </select>
                `;
                container.appendChild(box);
            });

            document.getElementById('start-screen').classList.add('hidden');
            document.getElementById('exam-screen').classList.remove('hidden');
            document.getElementById('exam-title').innerText = `Prüfung für: ${name}`;
        }

        function submitExam() {
            let score = 0;
            let total = activeExamQuestions.length;

            for (let i = 0; i < total; i++) {
                let val = document.getElementById(`question-${i}`).value;
                if (val === "") {
                    alert(`Bitte beantworte alle Fragen! Frage ${i + 1} ist noch offen.`);
                    return;
                }
                if (parseInt(val) === activeExamQuestions[i].correct) {
                    score++;
                }
            }

            let percentage = (score / total) * 100;
            let passed = percentage >= 80;

            document.getElementById('exam-screen').classList.add('hidden');
            document.getElementById('result-screen').classList.remove('hidden');

            let resText = document.getElementById('result-text');
            let resCard = document.getElementById('result-card');

            if (passed) {
                resCard.style.borderColor = 'var(--success)';
                resText.style.color = 'var(--success)';
                resText.innerHTML = `Bestanden! Du hast ${score} von ${total} Punkten erreicht (${percentage.toFixed(1)}%). Glückwunsch!`;
            } else {
                resCard.style.borderColor = 'var(--danger)';
                resText.style.color = 'var(--danger)';
                resText.innerHTML = `Nicht bestanden. Du hast ${score} von ${total} Punkten erreicht (${percentage.toFixed(1)}%). Benötigt werden mindestens 80%.`;
            }
        }

        function renderAdminQuestions() {
            document.getElementById('question-count').innerText = questions.length;
            let list = document.getElementById('admin-question-list');
            list.innerHTML = '';

            questions.forEach((item, index) => {
                let div = document.createElement('div');
                div.style.cssText = "background: var(--bg-main); padding: 10px; margin-bottom: 8px; border-radius: 4px; display: flex; justify-content: space-between; align-items: center;";
                div.innerHTML = `
                    <div><strong>#${index + 1}</strong> ${item.q}</div>
                    <button class="btn btn-danger" style="padding: 6px 12px; font-size: 12px;" onclick="deleteQuestion(${index})">Löschen</button>
                `;
                list.appendChild(div);
            });
        }

        function addNewQuestion() {
            let qText = document.getElementById('new-q-text').value.trim();
            let opt1 = document.getElementById('new-q-opt1').value.trim();
            let opt2 = document.getElementById('new-q-opt2').value.trim();
            let opt3 = document.getElementById('new-q-opt3').value.trim();
            let correct = parseInt(document.getElementById('new-q-correct').value);

            if (!qText || !opt1 || !opt2 || !opt3) {
                alert('Bitte alle Felder für die Frage ausfüllen!');
                return;
            }

            questions.push({
                q: qText,
                options: [opt1, opt2, opt3],
                correct: correct
            });

            localStorage.setItem('doj_questions', JSON.stringify(questions));
            renderAdminQuestions();

            document.getElementById('new-q-text').value = '';
            document.getElementById('new-q-opt1').value = '';
            document.getElementById('new-q-opt2').value = '';
            document.getElementById('new-q-opt3').value = '';
            alert('Frage erfolgreich hinzugefügt!');
        }

        function deleteQuestion(index) {
            if (confirm('Mist du sicher, dass du diese Frage löschen möchtest?')) {
                questions.splice(index, 1);
                localStorage.setItem('doj_questions', JSON.stringify(questions));
                renderAdminQuestions();
            }
        }
    </script>
</body>
</html>
