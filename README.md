<html lang="de"><head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BOCU</title>
    <style>
        /* Grundlegendes Styling für die Seite */
        body {
            font-family: 'Arial', sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f9;
            overflow: hidden;
        }
        .navbar {
            display: flex;
            justify-content: space-between;
            background-color: #1e90ff;
            padding: 10px;
            color: white;
        }
        .navbar input {
            padding: 10px;
            width: 60%;
            border-radius: 5px;
            border: none;
        }
        .navbar button {
            padding: 10px 20px;
            margin-left: 10px;
            border-radius: 5px;
            border: none;
            background-color: #fff;
            color: #1e90ff;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        .navbar button:hover {
            background-color: #ddd;
        }
        #content {
            display: flex;
            flex-direction: row;
            height: calc(100vh - 50px);
        }
        #sidebar {
            width: 20%;
            background-color: #333;
            color: white;
            overflow-y: auto;
            padding: 10px;
        }
        #main {
            width: 80%;
            padding: 10px;
            overflow-y: auto;
        }
        .iframe {
            width: 100%;
            height: 100%;
            border: none;
        }
    </style>
</head>
<body class="">
<div class="navbar">
    <input type="text" id="nameInput" placeholder="Geben Sie einen Namen ein">
    <button onclick="search()">Suchen</button>
    <button onclick="showBookmarks()">Lesezeichen</button>
    <button onclick="toggleTheme()">Thema wechseln</button>
</div>

<div id="content">
    <div id="sidebar">
        <h2>Lesezeichen</h2>
        <ul id="bookmarkList">
            <!-- Lesezeichen werden hier eingefügt -->
        <li>Albert Einstein</li><li>Marie Curie</li><li>Isaac Newton</li><li>Albert Einstein</li><li>Marie Curie</li><li>Isaac Newton</li></ul>
    </div>
    <div id="main">
        <iframe id="resultFrame" class="iframe"></iframe>
    </div>
</div>

<script>
    // Funktion für die Suche
    function search() {
        const name = document.getElementById('nameInput').value.trim();
        if (name) {
            const googleSearchUrl = 'https://www.google.com/search?q=' + encodeURIComponent(name);
            document.getElementById('resultFrame').src = googleSearchUrl;
            addBookmark(name);
        } else {
            alert('Bitte geben Sie einen Namen ein.');
        }
    }
	    // Funktion, um ein Lesezeichen hinzuzufügen
    function addBookmark(name) {
        const bookmarkList = document.getElementById('bookmarkList');
        const listItem = document.createElement('li');
        listItem.textContent = name;
        listItem.onclick = () => loadBookmark(name);
        bookmarkList.appendChild(listItem);
    }

    // Funktion, um ein Lesezeichen zu laden
    function loadBookmark(name) {
        const googleSearchUrl = 'https://www.google.com/search?q=' + encodeURIComponent(name);
        document.getElementById('resultFrame').src = googleSearchUrl;
    }

    // Funktion, um die Sidebar mit Lesezeichen anzuzeigen
    function showBookmarks() {
        const sidebar = document.getElementById('sidebar');
        sidebar.style.display = sidebar.style.display === 'none' ? 'block' : 'none';
    }

    // Funktion, um das Thema zu wechseln
    function toggleTheme() {
        const body = document.body;
        body.style.backgroundColor = body.style.backgroundColor === 'white' ? '#333' : 'white';
        body.style.color = body.style.color === 'black' ? 'white' : 'black';
    }
</script>
<script>
    // Erweiterte Funktionen für besseren UX
    document.addEventListener('DOMContentLoaded', (event) => {
        // Initialisiere Standardthema
        toggleTheme(); // Diese Zeile schaltet das Thema beim Laden um, um die Funktion zu demonstrieren

        // Event-Listener für die Eingabetaste im Suchfeld
        document.getElementById('nameInput').addEventListener('keypress', function (e) {
            if (e.key === 'Enter') {
                search();
            }
        });

        // Beispielhafte Lesezeichen zur Demonstration
        const initialBookmarks = ['Albert Einstein', 'Marie Curie', 'Isaac Newton'];
        initialBookmarks.forEach(name => addBookmark(name));
    });

    // Funktion, um gespeicherte Lesezeichen zu erhalten
    function loadSavedBookmarks() {
        // Hier könnte man lokalen Speicher oder eine API-Verbindung verwenden, um Lesezeichen zu laden
        console.log("Lesezeichen werden geladen...");
    }

    // Funktion, um Lesezeichen zu speichern
    function saveBookmarks() {
        // Hier könnte man lokalen Speicher oder eine API-Verbindung verwenden, um Lesezeichen zu speichern
        console.log("Lesezeichen werden gespeichert...");
    }
</script>
<style>
    /* Zusätzliches Styling für eine bessere Benutzeroberfläche */
    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        padding: 8px;
        cursor: pointer;
        transition: background-color 0.3s;
    }

    li:hover {
        background-color: #575757;
    }

    h2 {
        font-size: 1.5em;
        margin: 0 0 10px 0;
        padding-bottom: 10px;
        border-bottom: 1px solid #444;
    }
    
    /* Responsive Design Anpassungen */
    @media (max-width: 768px) {
        #sidebar {
            display: none;
        }
        
        .navbar input {
            width: 50%;
        }
        
        #main {
            width: 100%;
        }
    }
</style>
<style>
    /* Weiteres Styling für eine verbesserte Benutzererfahrung */
    .navbar h1 {
        font-size: 1.8em;
        margin: 0;
    }

    .navbar button:focus {
        outline: none;
        box-shadow: 0 0 5px #1e90ff;
    }

    #sidebar h2 {
        color: #1e90ff;
    }

    #main h2 {
        color: #333;
    }

    /* Dark mode specific styles */
    .dark-mode {
        background-color: #222;
        color: #ddd;
    }

    .dark-mode .navbar {
        background-color: #111;
    }

    .dark-mode #sidebar {
        background-color: #333;
    }

    .dark-mode li:hover {
        background-color: #444;
    }
</style>
<script>
    // Funktion, um das Thema dauerhaft zu speichern
    function saveThemePreference(isDarkMode) {
        localStorage.setItem('darkMode', isDarkMode);
    }

    // Funktion, um das gespeicherte Thema zu laden
    function loadThemePreference() {
        const isDarkMode = localStorage.getItem('darkMode') === 'true';
        if (isDarkMode) {
            document.body.classList.add('dark-mode');
        }
    }

    // Aktualisierte Funktion, um das Thema zu wechseln und zu speichern
    function toggleTheme() {
        const body = document.body;
        body.classList.toggle('dark-mode');
        saveThemePreference(body.classList.contains('dark-mode'));
    }

    document.addEventListener('DOMContentLoaded', (event) => {
        loadThemePreference(); // Lade das gespeicherte Thema beim Laden der Seite
    });
</script>


</body></html>
