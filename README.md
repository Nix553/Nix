# Nix
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Das geheimnisvolle Schloss</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            margin: 0;
            padding: 0;
            height: 100vh;
            background-image: url('images/sessel.jpg'); /* Dein Bild */
            background-size: cover;
            background-position: center;
            color: #fff;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
        }

        #game-container {
            background-color: rgba(0, 0, 0, 0.6);
            border-radius: 10px;
            padding: 20px;
            max-width: 600px;
            width: 100%;
            text-align: center;
            transition: transform 0.3s ease-in-out;
        }

        h1 {
            color: #FFD700;
            animation: fadeIn 2s ease-in-out;
        }

        .choice {
            background-color: #4CAF50;
            color: white;
            padding: 12px;
            margin: 10px 0;
            border: none;
            cursor: pointer;
            font-size: 18px;
            border-radius: 5px;
            transition: background-color 0.3s;
        }

        .choice:hover {
            background-color: #45a049;
        }

        #story {
            font-size: 18px;
            margin-bottom: 20px;
        }

        .button-container {
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }
    </style>
</head>
<body>

    <div id="game-container">
        <h1>Das geheimnisvolle Schloss</h1>
        <div id="story">
            <!-- Story wird hier eingefügt -->
            <p>Du stehst vor den imposanten Toren des Schlosses...</p>
        </div>
        <div class="button-container">
            <button class="choice" onclick="makeChoice(1)">Eintreten und das Schloss erkunden</button>
            <button class="choice" onclick="makeChoice(2)">Zurückgehen und den Ort meiden</button>
            <button class="choice" onclick="makeChoice(3)">Laut klopfen, um herauszufinden, ob jemand da ist</button>
        </div>
    </div>

    <script>
        let currentState = 0;

        // Hier speichern wir den Fortschritt
        function saveProgress(state) {
            localStorage.setItem("gameState", state);
        }

        function loadProgress() {
            const savedState = localStorage.getItem("gameState");
            if (savedState) {
                currentState = parseInt(savedState);
                // Wieder die entsprechende Szene laden
                if (currentState === 1) {
                    showStory("Du betrittst das Schloss. Der Eingang ist dunkel und du kannst kaum etwas sehen.");
                    showChoices(["In den großen Saal gehen", "In einen kleinen Raum rechts abbiegen"]);
                } else if (currentState === 2) {
                    showStory("Du drehst dich um und gehst, das mulmige Gefühl lässt dich nicht los.");
                    showChoices(["Zu Hause entspannen", "Vielleicht doch zurückkehren?"]);
                } else if (currentState === 3) {
                    showStory("Du klopfst laut an die Tür. Ein unheimliches Geräusch antwortet aus dem Inneren.");
                    showChoices(["Weiter klopfen", "Weggehen"]);
                }
            }
        }

        function makeChoice(choice) {
            saveProgress(choice); // Fortschritt speichern

            if (choice === 1) {
                showStory("Du betrittst das Schloss. Der Eingang ist dunkel und du kannst kaum etwas sehen.");
                showChoices(["In den großen Saal gehen", "In einen kleinen Raum rechts abbiegen"]);
            } else if (choice === 2) {
                showStory("Du drehst dich um und gehst, das mulmige Gefühl lässt dich nicht los.");
                showChoices(["Zu Hause entspannen", "Vielleicht doch zurückkehren?"]);
            } else if (choice === 3) {
                showStory("Du klopfst laut an die Tür. Ein unheimliches Geräusch antwortet aus dem Inneren.");
                showChoices(["Weiter klopfen", "Weggehen"]);
            }
        }

        function showStory(storyText) {
            document.getElementById("story").innerHTML = "<p>" + storyText + "</p>";
        }

        function showChoices(choices) {
            const buttons = document.querySelectorAll('.choice');
            buttons.forEach(button => button.style.display = 'none');
            
            choices.forEach((choice, index) => {
                const button = document.createElement('button');
                button.classList.add('choice');
                button.textContent = choice;
                button.onclick = () => makeChoice(index + 1);
                document.querySelector('.button-container').appendChild(button);
            });
        }

        // Lädt den Fortschritt, wenn die Seite geladen wird
        window.onload = function() {
            loadProgress();
        };
    </script>
</body>
</html>
