<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DOJ Grande City - Department of Justice</title>
    <style>
        :root {
            --bg-main: #070a12;
            --bg-card: #0f172a;
            --bg-input: #151e36;
            --accent-gold: #d4af37;
            --accent-gold-hover: #f3c653;
            --text-light: #f3f4f6;
            --text-muted: #9ca3af;
            --success: #059669;
            --danger: #dc2626;
            --border: #1e293b;
            --border-glow: rgba(212, 175, 55, 0.4)
        }

        body {
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
            background-color: var(--bg-main);
            color: var(--text-light);
            margin: 0;
            padding: 30px;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }

        .container {
            max-width: 950px;
            width: 100%;
            margin: 0 auto;
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 16px;
            box-shadow: 0 20px 50px rgba(0,0,0,0.8), 0 0 20px rgba(212, 175, 55, 0.05);
            overflow: hidden;
            position: relative;
        }

        header {
            background: linear-gradient(135deg, #090d16, #131c2e);
            padding: 25px 35px;
            border-bottom: 2px solid var(--accent-gold);
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 20px;
        }

        header h1 {
            margin: 0;
            font-size: 26px;
            color: var(--accent-gold);
            text-transform: uppercase;
            letter-spacing: 1.5px;
            text-shadow: 0 2px 4px rgba(0,0,0,0.5);
        }

        .header-clock-container {
            display: flex;
            align-items: center;
            gap: 15px;
            background: rgba(11, 15, 25, 0.6);
            padding: 8px 15px;
            border-radius: 10px;
            border: 1px solid var(--border);
        }

        .analog-clock {
            width: 46px;
            height: 46px;
            border: 2px solid var(--accent-gold);
            border-radius: 50%;
            position: relative;
            background: #0b0f19;
            box-shadow: inset 0 0 8px rgba(0,0,0,0.8);
        }

        .clock-center {
            width: 6px;
            height: 6px;
            background: var(--accent-gold);
            border-radius: 50%;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 4;
        }

        .hand {
            position: absolute;
            bottom: 50%;
            left: 50%;
            transform-origin: bottom;
            border-radius: 4px;
            z-index: 3;
        }

        .hour-hand {
            width: 3px;
            height: 12px;
            background: var(--text-light);
            transform: translate(-50%, 0);
        }

        .minute-hand {
            width: 2px;
            height: 17px;
            background: var(--accent-gold);
            transform: translate(-50%, 0);
        }

        .second-hand {
            width: 1px;
            height: 19px;
            background: var(--danger);
            transform: translate(-50%, 0);
            z-index: 5;
        }

        .date-display {
            text-align: left;
        }

        .date-display .date-text {
            font-size: 13px;
            font-weight: bold;
            color: var(--text-light);
            letter-spacing: 0.5px;
        }

        .date-display .time-text {
            font-size: 11px;
            color: var(--accent-gold);
            font-family: monospace;
        }

        .content {
            padding: 35px;
        }

        .btn {
            background: linear-gradient(135deg, var(--accent-gold), #b89230);
            color: #000;
            font-weight: bold;
            border: none;
            padding: 12px 24px;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.2s ease;
            box-shadow: 0 4px 12px rgba(212, 175, 55, 0.2);
            text-transform: uppercase;
            font-size: 13px;
            letter-spacing: 0.5px;
        }

        .btn:hover {
            background: linear-gradient(135deg, var(--accent-gold-hover), var(--accent-gold));
            box-shadow: 0 6px 18px var(--border-glow);
            transform: translateY(-1px);
        }

        .btn-danger {
            background: linear-gradient(135deg, var(--danger), #b91c1c);
            color: #fff;
            box-shadow: 0 4px 12px rgba(220, 38, 38, 0.3);
        }

        .btn-danger:hover {
            background: linear-gradient(135deg, #ef4444, var(--danger));
            box-shadow: 0 6px 18px rgba(220, 38, 38, 0.5);
        }

        input, select {
            width: 100%;
            padding: 14px;
            background: var(--bg-input);
            border: 1px solid var(--border);
            border-radius: 8px;
            color: var(--text-light);
            margin-bottom: 18px;
            box-sizing: border-box;
            font-size: 14px;
            transition: border-color 0.2s, box-shadow 0.2s;
        }

        input:focus, select:focus {
            outline: none;
            border-color: var(--accent-gold);
            box-shadow: 0 0 0 3px rgba(212, 175, 55, 0.15);
        }

        input::placeholder {
            color: #64748b;
            opacity: 1;
        }

        .hidden {
            display: none !important;
        }

        .admin-badge {
            background: var(--danger);
            color: white;
            padding: 5px 12px;
            border-radius: 6px;
            font-size: 11px;
            font-weight: bold;
            letter-spacing: 1px;
            box-shadow: 0 2px 8px rgba(220, 38, 38, 0.4);
        }

        .card {
            background: rgba(21, 30, 54, 0.4);
            border: 1px solid var(--border);
            padding: 25px;
            border-radius: 12px;
            margin-bottom: 20px;
            backdrop-filter: blur(10px);
        }

        .question-box {
            margin-bottom: 25px;
            padding-bottom: 20px;
            border-bottom: 1px solid var(--border);
        }

        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            background: rgba(5, 8, 15, 0.85);
            backdrop-filter: blur(8px);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.3s ease;
        }

        .modal-overlay.active {
            opacity: 1;
            pointer-events: auto;
        }

        .modal-box {
            background: var(--bg-card);
            border: 1px solid var(--accent-gold);
            padding: 35px;
            border-radius: 16px;
            width: 100%;
            max-width: 420px;
            box-shadow: 0 25px 60px rgba(0,0,0,0.9), 0 0 30px rgba(212, 175, 55, 0.2);
            transform: translateY(20px);
            transition: transform 0.3s cubic-bezier(0.16, 1, 0.3, 1);
        }

        .modal-overlay.active .modal-box {
            transform: translateY(0);
        }

        .modal-box h3 {
            margin-top: 0;
            color: var(--accent-gold);
            text-transform: uppercase;
            letter-spacing: 1px;
            font-size: 20px;
            margin-bottom: 20px;
            border-bottom: 1px solid var(--border);
            padding-bottom: 10px;
        }

        .modal-actions {
            display: flex;
            gap: 10px;
            margin-top: 10px;
        }

        .modal-actions .btn {
            flex: 1;
        }

        .btn-secondary {
            background: transparent;
            border: 1px solid var(--border);
            color: var(--text-muted);
            box-shadow: none;
        }

        .btn-secondary:hover {
            background: rgba(255,255,255,0.05);
            color: var(--text-light);
            border-color: var(--text-muted);
            box-shadow: none;
        }

        @media print {
            body {
                background: #ffffff !important;
                color: #000000 !important;
                padding: 0;
            }
            header, .modal-overlay, button, .admin-badge {
                display: none !important;
            }
            .container {
                border: none !important;
                box-shadow: none !important;
                background: #ffffff !important;
                max-width: 100% !important;
                width: 100% !important;
            }
            .card {
                background: #ffffff !important;
                border: 2px solid #000000 !important;
                color: #000000 !important;
                box-shadow: none !important;
            }
            #result-text {
                color: #000000 !important;
            }
        }
    </style>
</head>
<body>

    <div class="container">
        <header>
            <div>
                <h1>DOJ Grande City</h1>
                <p style="margin: 5px 0 0 0; color: var(--text-muted); font-size: 14px;">Department of Justice – Prüfungsportal</p>
            </div>
            
            <div style="display: flex; align-items: center; gap: 20px;">
                <div class="header-clock-container">
                    <div class="analog-clock">
                        <div class="clock-center"></div>
                        <div class="hand hour-hand" id="hour-hand"></div>
                        <div class="hand minute-hand" id="minute-hand"></div>
                        <div class="hand second-hand" id="second-hand"></div>
                    </div>
                    <div class="date-display">
                        <div class="date-text" id="header-date">--. --. ----</div>
                        <div class="time-text" id="header-time">00:00:00</div>
                    </div>
                </div>

                <div id="header-status">
                    <button class="btn" onclick="openLoginModal()">Admin Portal</button>
                </div>
            </div>
        </header>

        <div class="content">
            <div id="user-view">
                <div class="card" id="start-screen">
                    <h2>Offizielle DOJ Einstellungsprüfung</h2>
                    <p>Willkommen beim Prüfungsportal von Grande City. Dir werden per Zufallsgenerator 15 Fragen aus unserem über 60 Fragen starken Katalog zugewiesen. Zum Bestehen sind mindestens 80% (12 von 15 Punkten) erforderlich.</p>
                    <br>
                    <input type="text" id="applicant-name" placeholder="Vollständiger Name / Ingame-Name eingeben..." style="max-width: 450px;">
                    <br>
                    <button class="btn" onclick="startExam()">Prüfung starten</button>
                </div>

                <div id="exam-screen" class="hidden">
                    <h3 id="exam-title" style="color: var(--accent-gold); margin-bottom: 25px;">Prüfung läuft...</h3>
                    <div id="questions-container"></div>
                    <button class="btn" onclick="submitExam()">Prüfung abgeben & auswerten</button>
                </div>

                <div id="result-screen" class="hidden">
                    <div class="card" id="result-card" style="text-align: center; padding: 40px;">
                        <h2>Offizielles Prüfungsergebnis</h2>
                        <p id="applicant-display-name" style="color: var(--accent-gold); font-size: 16px; font-weight: bold; margin-top: 5px;"></p>
                        <p id="result-text" style="font-size: 20px; font-weight: bold; margin: 25px 0;"></p>
                        
                        <div style="display: flex; justify-content: center; gap: 15px; margin-top: 30px;">
                            <button class="btn" onclick="printResultPDF()" style="background: linear-gradient(135deg, #3b82f6, #1d4ed8); color: #fff;">🖨️ Als PDF speichern / Drucken</button>
                            <button class="btn btn-secondary" onclick="location.reload()">Zurück zur Startseite</button>
                        </div>
                    </div>
                </div>
            </div>

            <div id="admin-view" class="hidden">
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 25px;">
                    <h2>Admin-Dashboard</h2>
                    <span class="admin-badge">ADMIN MODUS AKTIV</span>
                </div>
                <div class="card">
                    <h3>Fragenkatalog verwalten (Gesamt im System: <span id="question-count" style="color: var(--accent-gold);">0</span>)</h3>
                    <p style="color: var(--text-muted); margin-bottom: 25px;">Füge neue Fragen hinzu oder entferne bestehende. Änderungen werden sofort dauerhaft im Browser gesichert.</p>
                    
                    <div style="background: rgba(11, 15, 25, 0.6); padding: 20px; border-radius: 10px; border: 1px solid var(--border); margin-bottom: 30px;">
                        <h4 style="margin-top: 0; color: var(--accent-gold);">Neue Frage hinzufügen</h4>
                        <input type="text" id="new-q-text" placeholder="Fragetext eingeben...">
                        <div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 10px;">
                            <input type="text" id="new-q-opt1" placeholder="Antwort A" style="margin-bottom: 10px;">
                            <input type="text" id="new-q-opt2" placeholder="Antwort B" style="margin-bottom: 10px;">
                            <input type="text" id="new-q-opt3" placeholder="Antwort C" style="margin-bottom: 10px;">
                        </div>
                        <select id="new-q-correct">
                            <option value="0">Richtige Antwort: A</option>
                            <option value="1">Richtige Antwort: B</option>
                            <option value="2">Richtige Antwort: C</option>
                        </select>
                        <button class="btn" onclick="addNewQuestion()">Frage speichern</button>
                    </div>

                    <h4 style="margin-bottom: 15px;">Vorhandene Fragen</h4>
                    <div id="admin-question-list" style="max-height: 450px; overflow-y: auto; padding-right: 5px;"></div>

                    <br>
                    <button class="btn btn-danger" onclick="adminLogout()">Admin abmelden</button>
                </div>
            </div>
        </div>
    </div>

    <div id="login-modal" class="modal-overlay">
        <div class="modal-box">
            <h3>Admin Portal Login</h3>
            <p style="color: var(--text-muted); font-size: 13px; margin-bottom: 20px;">Bitte gib deine Administrator-Zugangsdaten ein, um den Fragenkatalog zu verwalten.</p>
            <input type="text" id="username" placeholder="Benutzername">
            <input type="password" id="password" placeholder="Passwort">
            <div class="modal-actions">
                <button class="btn btn-secondary" onclick="closeLoginModal()">Abbrechen</button>
                <button class="btn" onclick="performLogin()">Einloggen</button>
            </div>
        </div>
    </div>

    <script>
        function updateClock() {
            const now = new Date();
            const seconds = now.getSeconds();
            const minutes = now.getMinutes();
            const hours = now.getHours();

            const secondDegrees = (seconds / 60) * 360;
            const minuteDegrees = ((minutes + seconds / 60) / 60) * 360;
            const hourDegrees = ((hours % 12 + minutes / 60) / 12) * 360;

            const secEl = document.getElementById('second-hand');
            const minEl = document.getElementById('minute-hand');
            const hrEl = document.getElementById('hour-hand');

            if(secEl) secEl.style.transform = `translate(-50%, 0) rotate(${secondDegrees}deg)`;
            if(minEl) minEl.style.transform = `translate(-50%, 0) rotate(${minuteDegrees}deg)`;
            if(hrEl) hrEl.style.transform = `translate(-50%, 0) rotate(${hourDegrees}deg)`;

            const optionsDate = { weekday: 'short', day: '2-digit', month: '2-digit', year: 'numeric' };
            const dateEl = document.getElementById('header-date');
            const timeEl = document.getElementById('header-time');

            if(dateEl) dateEl.innerText = now.toLocaleDateString('de-DE', optionsDate);
            if(timeEl) timeEl.innerText = now.toLocaleTimeString('de-DE');
        }
        setInterval(updateClock, 1000);
        updateClock();

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
            { q: "Was versteht man unter Notwehr?", options: ["Angriff auf andere", "Abwehr eines gegenwärtigen, rechtswidrigen Angriffs", "Streit auf der Straße"], correct: 1 },
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
            { q: "Was ist eine Vernehmung?", options: ["Befragung durch Behörden", "Ein Verhör mit Gewalt", "Ein Kaffeekränzchen"], correct: 0 },
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

        window.addEventListener('DOMContentLoaded', () => {
            const isAdmin = sessionStorage.getItem('doj_admin_logged_in');
            if (isAdmin === 'true') {
                showAdminView();
            }
        });

        function openLoginModal() {
            document.getElementById('login-modal').classList.add('active');
            document.getElementById('username').focus();
        }

        function closeLoginModal() {
            document.getElementById('login-modal').classList.remove('active');
            document.getElementById('username').value = '';
            document.getElementById('password').value = '';
        }

        function performLogin() {
            const user = document.getElementById('username').value.trim();
            const pass = document.getElementById('password').value.trim();

            if (user === 'Doj1' && pass === 'starko') {
                sessionStorage.setItem('doj_admin_logged_in', 'true');
                closeLoginModal();
                showAdminView();
            } else {
                alert('Falscher Benutzername oder falsches Passwort!');
            }
        }

        function showAdminView() {
            document.getElementById('user-view').classList.add('hidden');
            document.getElementById('admin-view').classList.remove('hidden');
            document.getElementById('header-status').innerHTML = '<span class="admin-badge">ADMIN AKTIV</span>';
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

            let shuffled = [...questions].sort(() => 0.5 - Math.random());
            activeExamQuestions = shuffled.slice(0, 15);

            let container = document.getElementById('questions-container');
            container.innerHTML = '';

            activeExamQuestions.forEach((item, index) => {
                let box = document.createElement('div');
                box.className = 'question-box';
                box.innerHTML = `
                    <label style="font-size: 16px; display: block; margin-bottom: 12px;"><strong>${index + 1}. ${item.q}</strong></label>
                    <select id="question-${index}">
                        <option value="">Bitte Antwort auswählen...</option>
                        <option value="0">${item.options[0]}</option>
                        <option value="1">${item.options[1]}</option>
                        <option value="2">${item.options[2]}</option>
                    </select>
                `;
                container.appendChild(box);
            });

            document.getElementById('start-screen').classList.add('hidden');
            document.getElementById('exam-screen').classList.remove('hidden');
            document.getElementById('exam-title').innerText = `Prüfung für Anwärter: ${name}`;
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function submitExam() {
            let score = 0;
            let total = activeExamQuestions.length;
            const name = document.getElementById('applicant-name').value.trim();

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

            document.getElementById('applicant-display-name').innerText = `Prüfling: ${name}`;
            let resText = document.getElementById('result-text');
            let resCard = document.getElementById('result-card');

            if (passed) {
                resCard.style.borderColor = 'var(--success)';
                resText.style.color = 'var(--success)';
                resText.innerHTML = `🎉 BESTANDEN!<br><span style="font-size: 16px; color: var(--text-light);">Du hast ${score} von ${total} Punkten erreicht (${percentage.toFixed(1)}%). Glückwunsch zur bestandenen Prüfung!</span>`;
            } else {
                resCard.style.borderColor = 'var(--danger)';
                resText.style.color = 'var(--danger)';
                resText.innerHTML = `❌ LEIDER NICHT BESTANDEN<br><span style="font-size: 16px; color: var(--text-light);">Du hast ${score} von ${total} Punkten erreicht (${percentage.toFixed(1)}%). Benötigt werden mindestens 80% (12 Punkte).</span>`;
            }
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function printResultPDF() {
            window.print();
        }

        function renderAdminQuestions() {
            document.getElementById('question-count').innerText = questions.length;
            let list = document.getElementById('admin-question-list');
            list.innerHTML = '';

            questions.forEach((item, index) => {
                let div = document.createElement('div');
                div.style.cssText = "background: rgba(7, 10, 18, 0.6); padding: 12px 15px; margin-bottom: 10px; border-radius: 8px; border: 1px solid var(--border); display: flex; justify-content: space-between; align-items: center; gap: 15px;";
                div.innerHTML = `
                    <div style="font-size: 14px;"><strong style="color: var(--accent-gold);">#${index + 1}</strong> ${item.q}</div>
                    <button class="btn btn-danger" style="padding: 6px 14px; font-size: 11px; white-space: nowrap;" onclick="deleteQuestion(${index})">Löschen</button>
                `;
                list.appendChild(div);
            });
        }

        function addNewQuestion() {
            let qText = document.getElementById('new-q-text').value.trim();
            let opt1 = document.getElementById('new-q-opt1').value.trim();
            let opt2 = document.getElementById('new-q-opt2').value.trim();
            let opt3 = document.getElementById('new-q-opt3').value.trim(); // <-- Hier korrigiert!
            let correct = parseInt(document.getElementById('new-q-correct').value);

            if (!qText || !opt1 || !opt2 || !opt3) {
                alert('Bitte den Fragetext und alle drei Antwortmöglichkeiten ausfüllen!');
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
            document.getElementById('new-q-correct').value = '0';
            alert('Frage wurde erfolgreich dem Katalog hinzugefügt!');
        }

        function deleteQuestion(index) {
            if (confirm('Bist du sicher, dass du diese Frage unwiderruflich löschen möchtest?')) {
                questions.splice(index, 1);
                localStorage.setItem('doj_questions', JSON.stringify(questions));
                renderAdminQuestions();
            }
        }
    </script>
</body>
</html>
