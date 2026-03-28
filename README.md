<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes">
    <title>Kojano – byggspråket</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(145deg, #e6dcc8 0%, #cdc2a4 100%);
            font-family: 'Inter', system-ui, -apple-system, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            color: #2d3e2b;
            padding: 20px 16px 60px;
        }

        /* container */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: #fffef7;
            border-radius: 48px 48px 40px 40px;
            box-shadow: 0 20px 35px -12px rgba(0,0,0,0.2), 0 1px 2px rgba(0,0,0,0.05);
            overflow: hidden;
            backdrop-filter: blur(0px);
            transition: all 0.2s ease;
        }

        /* header */
        header {
            background: #3e6b3a;
            padding: 28px 20px;
            text-align: center;
            color: #fff8e7;
            position: relative;
            border-bottom: 4px solid #ffdf8c;
        }
        header h1 {
            font-size: 2.3rem;
            letter-spacing: -0.5px;
            font-weight: 800;
            text-shadow: 2px 2px 0 #2a4a24;
        }
        header p {
            font-size: 1rem;
            opacity: 0.9;
            margin-top: 6px;
        }
        .admin-toggle {
            position: absolute;
            top: 20px;
            right: 20px;
            background: #ffefc0;
            border: none;
            border-radius: 60px;
            padding: 8px 18px;
            font-weight: 700;
            font-size: 0.85rem;
            color: #3e6b3a;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
            cursor: pointer;
            transition: 0.1s;
        }
        .admin-toggle:active { transform: scale(0.96); }
        .admin-badge {
            background: #f4c542;
            color: #2d3e2b;
            padding: 6px 14px;
            border-radius: 40px;
            font-size: 0.75rem;
            display: inline-block;
            margin-top: 10px;
            font-weight: 600;
        }

        /* navigation */
        nav {
            background: #f5efe2;
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 8px;
            padding: 14px 12px;
            border-bottom: 1px solid #e2d8c2;
        }
        nav button {
            background: #ffffffcc;
            border: none;
            padding: 10px 20px;
            font-weight: 600;
            border-radius: 50px;
            color: #3b5a2b;
            font-size: 0.9rem;
            cursor: pointer;
            transition: 0.2s;
            box-shadow: 0 1px 3px rgba(0,0,0,0.05);
        }
        nav button.active {
            background: #3e6b3a;
            color: white;
            box-shadow: 0 6px 12px rgba(60,90,40,0.25);
        }

        /* tab content */
        .tab-content {
            display: none;
            padding: 28px 24px 36px;
            animation: fade 0.25s ease;
        }
        .tab-content.active {
            display: block;
        }
        @keyframes fade {
            from { opacity: 0; transform: translateY(6px);}
            to { opacity: 1; transform: translateY(0);}
        }

        h2 {
            font-size: 1.8rem;
            border-left: 6px solid #5f9e4a;
            padding-left: 18px;
            margin-bottom: 24px;
            font-weight: 700;
            color: #2c5a2a;
        }
        h3 {
            font-size: 1.3rem;
            margin: 24px 0 12px 0;
            color: #4b6e3e;
            font-weight: 600;
        }
        .card {
            background: #fefae9;
            border-radius: 36px;
            padding: 20px 24px;
            margin-bottom: 28px;
            border: 1px solid #e7ddc4;
            box-shadow: 0 6px 12px rgba(0,0,0,0.04);
        }

        /* alfabet */
        .alphabet-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            margin: 20px 0;
        }
        .letter {
            background: #e9e2cf;
            padding: 10px 18px;
            border-radius: 60px;
            font-weight: bold;
            font-size: 1.2rem;
            box-shadow: inset 0 1px 1px white, 0 2px 4px rgba(0,0,0,0.05);
        }

        /* ordlistor (grid) */
        .word-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
            gap: 10px;
            margin-bottom: 28px;
        }
        .word-card {
            background: #fffaf0;
            border-radius: 28px;
            padding: 10px 16px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border: 1px solid #e6dbbc;
            transition: 0.1s;
        }
        .word-sv {
            font-weight: 700;
            color: #3b5a2b;
        }
        .word-ko {
            font-family: 'Fira Mono', monospace;
            background: #e9e0cb;
            padding: 4px 14px;
            border-radius: 40px;
            font-size: 0.9rem;
            font-weight: 500;
        }

        /* ordbokstabell */
        .dict-table {
            width: 100%;
            border-collapse: collapse;
            background: #fffcf2;
            border-radius: 32px;
            overflow: hidden;
            margin-top: 20px;
        }
        .dict-table th, .dict-table td {
            padding: 12px 12px;
            text-align: left;
            border-bottom: 1px solid #ece0c8;
        }
        .dict-table th {
            background: #e6dbbc;
            color: #3b5a2b;
            font-weight: 700;
        }

        .search-input {
            width: 100%;
            padding: 14px 20px;
            border-radius: 60px;
            border: 1px solid #cfc3a2;
            background: white;
            font-size: 1rem;
            margin-bottom: 16px;
        }

        /* quiz & översätt */
        .quiz-card {
            background: #eef3e3;
            border-radius: 48px;
            padding: 28px 20px;
            text-align: center;
        }
        .quiz-question {
            font-size: 1.8rem;
            font-weight: 800;
            background: white;
            display: inline-block;
            padding: 12px 30px;
            border-radius: 60px;
            margin: 10px 0;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
        }
        .quiz-input {
            width: 80%;
            padding: 14px 20px;
            border-radius: 60px;
            border: 1px solid #cfc3a2;
            text-align: center;
            font-size: 1.1rem;
        }
        button {
            background: #6f9e4f;
            border: none;
            border-radius: 60px;
            padding: 12px 28px;
            color: white;
            font-weight: bold;
            font-size: 0.95rem;
            cursor: pointer;
            transition: 0.1s;
            margin: 6px;
            box-shadow: 0 3px 6px rgba(0,0,0,0.1);
        }
        button:active { transform: scale(0.96); background: #55833b; }
        .result-box {
            background: white;
            border-radius: 60px;
            padding: 18px;
            text-align: center;
            font-size: 1.2rem;
            border: 1px solid #dacfaf;
        }
        footer {
            text-align: center;
            font-size: 0.7rem;
            padding: 24px;
            color: #7f8f6a;
            background: #f8f3e6;
            border-top: 1px solid #e2d8c2;
        }
        .flex-row {
            display: flex;
            flex-wrap: wrap;
            gap: 16px;
            align-items: center;
        }
        @media (max-width: 600px) {
            .container { border-radius: 32px; }
            nav button { padding: 6px 14px; font-size: 0.8rem; }
            h2 { font-size: 1.5rem; }
        }
    </style>
</head>
<body>
<div class="container">
    <header>
        <h1>🏕️ KOJANO</h1>
        <p>byggspråket – lär dig, skapa egna ord</p>
        <button id="adminLoginBtn" class="admin-toggle">👑 Admin</button>
        <div id="adminStatus"></div>
    </header>
    <nav>
        <button data-tab="learn">📘 Lär dig</button>
        <button data-tab="categories">📂 Kategorier</button>
        <button data-tab="dictionary">📖 Ordbok</button>
        <button data-tab="quiz">🎯 Quiz</button>
        <button data-tab="translate">🔍 Översätt</button>
        <button data-tab="adminPanel" id="adminTabBtn" style="display:none;">⚙️ Admin</button>
    </nav>

    <!-- LÄR DIG -->
    <div id="learn" class="tab-content">
        <h2>🔤 Alfabet (29 bokstäver)</h2>
        <div class="alphabet-grid" id="alphabetGrid"></div>
        <div class="card">
            <strong>📐 9 grammatikregler</strong><br>
            1. Ordföljd: VEM – GÖR – VAD (<em>Mi konstru koj</em>)<br>
            2. Tid: -ar (nu), -de (då), -er (framtid)<br>
            3. Flera: +s (<em>pin → pins</em>)<br>
            4. Bestämd: +en/-et (<em>kojen, taktet</em>)<br>
            5. Adjektiv före substantiv (<em>grand koj</em>)<br>
            6. Fråga: börja med <em>We</em> (<em>We tu bygg?</em>)<br>
            7. Negation: <em>no</em> före verb (<em>Mi no bygg</em>)<br>
            8. Uppmaning: verb + -a! (<em>Bygga!</em>)<br>
            9. Ägande: min, din, lis, las, nosar, vosar, lesar
        </div>
    </div>

    <!-- KATEGORIER -->
    <div id="categories" class="tab-content">
        <h2>📚 Ordlistor efter kategori</h2>
        <div id="categoryContainer"></div>
    </div>

    <!-- ORDBOK (alla ord) -->
    <div id="dictionary" class="tab-content">
        <h2>📖 Alla ord (svenska → kojano)</h2>
        <input type="text" id="dictSearch" class="search-input" placeholder="🔍 Filtrera ord...">
        <div id="dictTableContainer" style="max-height: 500px; overflow-y: auto;"></div>
        <p style="margin-top: 12px;">✨ Totalt <span id="wordCount">0</span> ord</p>
    </div>

    <!-- QUIZ -->
    <div id="quiz" class="tab-content">
        <h2>🎯 Träna glosor</h2>
        <div class="quiz-card">
            <div class="quiz-question" id="quizWord">laddar...</div>
            <input type="text" id="quizAnswer" class="quiz-input" placeholder="Skriv på Kojano">
            <div><button id="checkQuizBtn">Kontrollera</button> <button id="newQuizBtn">🎲 Nytt ord</button></div>
            <div id="quizFeedback" class="feedback" style="margin-top: 16px; font-weight: bold;"></div>
        </div>
    </div>

    <!-- ÖVERSÄTT -->
    <div id="translate" class="tab-content">
        <h2>🔍 Sök ord (svenska ↔ kojano)</h2>
        <div class="flex-row" style="margin-bottom: 16px;">
            <input type="text" id="searchInput" class="search-input" placeholder="Skriv ord...">
            <button id="searchBtn">Översätt</button>
        </div>
        <div id="translateResult" class="result-box">⭐ Skriv ett ord</div>
    </div>

    <!-- ADMINPANEL -->
    <div id="adminPanel" class="tab-content">
        <h2>⚙️ Admin – lägg till ord & ändra lösenord</h2>
        <div class="card">
            <h3>🔎 Slå upp ord</h3>
            <div class="flex-row">
                <input type="text" id="adminLookupInput" class="search-input" placeholder="Svenska ord...">
                <button id="adminLookupBtn">Sök</button>
            </div>
            <div id="adminLookupResult" class="result-box" style="margin-top: 10px;"></div>
            <hr style="margin: 20px 0;">
            <h3>➕ Lägg till nytt ord</h3>
            <div class="flex-row" style="flex-direction: column; align-items: stretch;">
                <input type="text" id="newSvWord" placeholder="Svenska ord">
                <input type="text" id="newKoWord" placeholder="Kojano-översättning">
                <button id="addWordBtn">Lägg till</button>
            </div>
            <hr>
            <h3>🔐 Ändra admin-lösenord</h3>
            <div class="flex-row">
                <input type="password" id="newAdminPwd" placeholder="Nytt lösenord">
                <button id="changePwdBtn">Ändra</button>
            </div>
            <hr>
            <h3>📋 Mina tillagda ord</h3>
            <div id="customWordList" style="max-height: 260px; overflow-y: auto;"></div>
            <button id="resetCustomWords" style="background:#b97f48; margin-top: 12px;">🗑️ Radera alla egna ord</button>
        </div>
        <p>💡 Grundord kan inte tas bort, egna ord sparas i webbläsaren.</p>
    </div>
    <footer>🏕️ Kojano – byggspråket | Adminläge sparas lokalt</footer>
</div>

<script>
    // ---------- GRUNDORDBOK ----------
    const baseDict = new Map();
    function addBase(sv, ko) { baseDict.set(sv.toLowerCase(), ko); baseDict.set(ko.toLowerCase(), sv); }
    // stort urval (exakt samma som tidigare)
    addBase("vatten","aku"); addBase("mjölk","lakt"); addBase("juice","saft"); addBase("bröd","pan");
    addBase("smör","butir"); addBase("ost","kaz"); addBase("ägg","ägg"); addBase("kött","köt");
    addBase("fisk","fisk"); addBase("grönsaker","grön-sak"); addBase("frukt","söt-sak"); addBase("äpple","epl");
    addBase("banan","banan"); addBase("glass","glac"); addBase("kaka","tort"); addBase("godis","söt");
    addBase("hund","kan"); addBase("katt","kat"); addBase("kanin","hopp"); addBase("hamster","hamstr");
    addBase("fågel","bird"); addBase("häst","ekv"); addBase("ko","bov"); addBase("gris","pork");
    addBase("ekorre","skvir"); addBase("räv","vulp"); addBase("uggla","strig");
    addBase("måndag","lun-di"); addBase("tisdag","mar-di"); addBase("onsdag","merk-di");
    addBase("torsdag","jov-di"); addBase("fredag","ven-di"); addBase("lördag","sat-di");
    addBase("söndag","sol-di"); addBase("idag","hodie"); addBase("igår","heri"); addBase("imorgon","kras");
    addBase("vecka","sept"); addBase("månad","lun"); addBase("år","an");
    addBase("noll","nul"); addBase("ett","un"); addBase("två","du"); addBase("tre","tri"); addBase("fyra","kvar");
    addBase("fem","kvin"); addBase("sex","ses"); addBase("sju","sep"); addBase("åtta","okt"); addBase("nio","nov");
    addBase("tio","dek"); addBase("tjugo","du-dek"); addBase("trettio","tri-dek"); addBase("fyrtio","kvar-dek");
    addBase("femtio","kvin-dek"); addBase("sextio","ses-dek"); addBase("sjuttio","sep-dek");
    addBase("åttio","okt-dek"); addBase("nittio","nov-dek"); addBase("hundra","cent"); addBase("tusen","mil");
    addBase("röd","red"); addBase("blå","blå"); addBase("grön","verd"); addBase("gul","gelb");
    addBase("svart","svart"); addBase("vit","vit"); addBase("orange","oran"); addBase("rosa","ros");
    addBase("lila","lila"); addBase("brun","brun"); addBase("grå","grå");
    addBase("glad","felic"); addBase("ledsen","tris"); addBase("arg","arg"); addBase("rädd","tim");
    addBase("lugn","kalm"); addBase("kär","amor"); addBase("trött","fatig"); addBase("pigg","energ");
    addBase("förvånad","surp"); addBase("orolig","anx"); addBase("ensam","sol"); addBase("modig","kuraĝ");
    addBase("huvud","kap"); addBase("hår","har"); addBase("öga","ok"); addBase("öra","or"); addBase("näsa","naz");
    addBase("mun","munt"); addBase("tand","dent"); addBase("arm","arm"); addBase("hand","man"); addBase("finger","fing");
    addBase("ben","gamb"); addBase("fot","ped"); addBase("hjärta","kord"); addBase("mage","venter"); addBase("rygg","dors");
    addBase("hus","hus"); addBase("lägenhet","flat"); addBase("rum","rum"); addBase("kök","kök");
    addBase("sovrum","dorm-rum"); addBase("badrum","toa-rum"); addBase("vardagsrum","stor-rum");
    addBase("dörr","dor"); addBase("fönster","fen"); addBase("vägg","val"); addBase("golv","grund");
    addBase("tak","takt"); addBase("säng","säng"); addBase("bord","bord"); addBase("stol","sit");
    addBase("lampa","lamp"); addBase("nyckel","klav");

    // Alfabet
    const letters = ["A","AO","E","EJ","I","O","U","Y","AJ","B","CH","D","F","G","H","J","K","L","M","N","NG","P","R","S","SH","T","V","W","Z"];
    const alphabetDiv = document.getElementById("alphabetGrid");
    letters.forEach(l => { let span = document.createElement("span"); span.className = "letter"; span.innerText = l; alphabetDiv.appendChild(span); });

    // ---------- ADMIN-LÖSENORD ----------
    let ADMIN_PASSWORD = "koja123";
    function loadAdminPassword() { let s = localStorage.getItem("absolut_ingenting_admin_pwd"); if(s) ADMIN_PASSWORD = s; else localStorage.setItem("absolut_ingenting_admin_pwd", ADMIN_PASSWORD); }
    function setAdminPassword(p) { ADMIN_PASSWORD = p; localStorage.setItem("absolut_ingenting_admin_pwd", p); }

    // ---------- ADMIN-ORD ----------
    let customWords = [];
    function loadCustomWords() { let s = localStorage.getItem("absolut_ingenting_custom"); customWords = s ? JSON.parse(s) : []; }
    function saveCustomWords() { localStorage.setItem("absolut_ingenting_custom", JSON.stringify(customWords)); refreshCustomList(); rebuildFullDict(); updateAll(); }

    let fullDict = new Map();
    function rebuildFullDict() {
        fullDict.clear();
        for(let [k,v] of baseDict.entries()) fullDict.set(k,v);
        for(let w of customWords) { fullDict.set(w.sv.toLowerCase(), w.ko); fullDict.set(w.ko.toLowerCase(), w.sv); }
    }

    function refreshCustomList() {
        const container = document.getElementById("customWordList");
        if(!container) return;
        container.innerHTML = "";
        if(customWords.length===0) { container.innerHTML = "<p>Inga egna ord än.</p>"; return; }
        customWords.forEach((item, idx) => {
            let div = document.createElement("div"); div.className = "word-card"; div.style.marginBottom="6px";
            div.innerHTML = `<span><strong>${item.sv}</strong> → ${item.ko}</span><button class="delete-btn" data-idx="${idx}" style="background:#b97f48; padding:4px 12px;">🗑️</button>`;
            container.appendChild(div);
        });
        document.querySelectorAll(".delete-btn").forEach(btn => {
            btn.addEventListener("click", (e) => { let i = parseInt(btn.getAttribute("data-idx")); customWords.splice(i,1); saveCustomWords(); });
        });
    }

    function addCustomWord(sv, ko) {
        sv = sv.trim().toLowerCase(); ko = ko.trim().toLowerCase();
        if(!sv||!ko) return false;
        if(customWords.some(w=>w.sv===sv)) return false;
        if(baseDict.has(sv) && !confirm("Grundord finns redan. Ändå lägga till egen variant?")) return false;
        customWords.push({sv,ko}); saveCustomWords(); return true;
    }
    function resetCustomWords() { if(confirm("Radera ALLA egna ord?")) { customWords = []; saveCustomWords(); } }

    // ---------- ADMIN INLOGG ----------
    let isAdmin = false;
    function setAdminMode(admin) {
        isAdmin = admin;
        let adminTab = document.getElementById("adminTabBtn");
        let statusDiv = document.getElementById("adminStatus");
        if(isAdmin) { adminTab.style.display = "inline-block"; statusDiv.innerHTML = '<div class="admin-badge">🔓 ADMINLÄGE</div>'; }
        else { adminTab.style.display = "none"; statusDiv.innerHTML = ''; if(document.getElementById("adminPanel").classList.contains("active")) switchTab("learn"); }
    }
    function promptAdminLogin() { let pwd = prompt("Ange admin-lösenord:"); if(pwd===ADMIN_PASSWORD) setAdminMode(true); else alert("Fel lösenord"); }
    function changeAdminPassword() { if(!isAdmin){ alert("Endast inloggad admin"); return; } let newPwd = document.getElementById("newAdminPwd").value.trim(); if(!newPwd) return; setAdminPassword(newPwd); alert("Lösenord ändrat! Logga in igen."); setAdminMode(false); document.getElementById("newAdminPwd").value=""; }

    // ---------- KATEGORIER ----------
    const categories = {
        mat: ["vatten","mjölk","juice","bröd","smör","ost","ägg","kött","fisk","grönsaker","frukt","äpple","banan","glass","kaka","godis"],
        djur: ["hund","katt","kanin","hamster","fågel","häst","ko","gris","ekorre","räv","uggla"],
        tid: ["måndag","tisdag","onsdag","torsdag","fredag","lördag","söndag","idag","igår","imorgon","vecka","månad","år"],
        siffror: ["noll","ett","två","tre","fyra","fem","sex","sju","åtta","nio","tio","tjugo","trettio","fyrtio","femtio","sextio","sjuttio","åttio","nittio","hundra","tusen"],
        färger: ["röd","blå","grön","gul","svart","vit","orange","rosa","lila","brun","grå"],
        känslor: ["glad","ledsen","arg","rädd","lugn","kär","trött","pigg","förvånad","orolig","ensam","modig"],
        kropp: ["huvud","hår","öga","öra","näsa","mun","tand","arm","hand","finger","ben","fot","hjärta","mage","rygg"],
        hem: ["hus","lägenhet","rum","kök","sovrum","badrum","vardagsrum","dörr","fönster","vägg","golv","tak","säng","bord","stol","lampa","nyckel"]
    };
    const icons = { mat:"🍎", djur:"🐾", tid:"📅", siffror:"🔢", färger:"🎨", känslor:"😊", kropp:"🦵", hem:"🏠" };
    function buildCategories() {
        const container = document.getElementById("categoryContainer");
        container.innerHTML = "";
        for(let [cat, words] of Object.entries(categories)) {
            let section = document.createElement("div");
            section.innerHTML = `<h3>${icons[cat] || "📖"} ${cat.charAt(0).toUpperCase()+cat.slice(1)}</h3><div class="word-grid" id="grid-${cat}"></div>`;
            container.appendChild(section);
            let grid = section.querySelector(`.word-grid`);
            for(let sw of words) {
                let ko = fullDict.get(sw.toLowerCase());
                if(ko) {
                    let card = document.createElement("div"); card.className = "word-card";
                    card.innerHTML = `<span class="word-sv">${sw}</span> <span class="word-ko">${ko}</span>`;
                    grid.appendChild(card);
                }
            }
        }
        if(customWords.length) {
            let customSec = document.createElement("div");
            customSec.innerHTML = `<h3>✨ Mina egna ord</h3><div class="word-grid" id="custom-grid"></div>`;
            container.appendChild(customSec);
            let grid = customSec.querySelector(".word-grid");
            for(let w of customWords) {
                let card = document.createElement("div"); card.className = "word-card";
                card.innerHTML = `<span class="word-sv">${w.sv}</span> <span class="word-ko">${w.ko}</span>`;
                grid.appendChild(card);
            }
        }
    }

    // ORDBOK (filtrering)
    function buildDictionary() {
        let filter = document.getElementById("dictSearch").value.trim().toLowerCase();
        let entries = [];
        for(let [sv,ko] of fullDict.entries()) {
            if(sv === ko) continue;
            if(!fullDict.has(ko) || sv < ko) entries.push({sv,ko});
        }
        let unique = new Map();
        for(let e of entries) if(!unique.has(e.sv)) unique.set(e.sv, e);
        let list = Array.from(unique.values());
        if(filter) list = list.filter(e => e.sv.includes(filter) || e.ko.includes(filter));
        list.sort((a,b)=>a.sv.localeCompare(b.sv));
        document.getElementById("wordCount").innerText = list.length;
        let container = document.getElementById("dictTableContainer");
        container.innerHTML = "";
        let table = document.createElement("table"); table.className = "dict-table";
        table.innerHTML = `<thead><tr><th>Svenska</th><th>Kojano</th></tr></thead><tbody></tbody>`;
        let tbody = table.querySelector("tbody");
        for(let e of list) {
            let row = tbody.insertRow();
            row.insertCell(0).innerText = e.sv;
            row.insertCell(1).innerText = e.ko;
        }
        container.appendChild(table);
    }

    // QUIZ
    let currentQuizSv="", currentQuizKo="";
    function randomQuizWord() {
        let svWords = [];
        for(let [key,val] of fullDict.entries()) if(key.length>1 && !key.includes(' ') && !fullDict.has(val)) svWords.push(key);
        if(!svWords.length) svWords = ["koja","bygga","pinne"];
        let rand = svWords[Math.floor(Math.random()*svWords.length)];
        currentQuizSv = rand;
        currentQuizKo = fullDict.get(rand);
        document.getElementById("quizWord").innerText = currentQuizSv;
    }
    function checkQuiz() {
        let ans = document.getElementById("quizAnswer").value.trim().toLowerCase();
        let fb = document.getElementById("quizFeedback");
        if(!ans) { fb.innerHTML = "❓ Skriv ett svar"; return; }
        if(ans === currentQuizKo) fb.innerHTML = "✅ Rätt! 🏕️";
        else fb.innerHTML = `❌ Fel! Rätt svar: ${currentQuizKo}`;
    }

    // ÖVERSÄTT
    function translate() {
        let inp = document.getElementById("searchInput").value.trim().toLowerCase();
        let res = document.getElementById("translateResult");
        if(!inp) { res.innerHTML = "⭐ Skriv ett ord"; return; }
        if(fullDict.has(inp)) res.innerHTML = `<strong>${inp}</strong> → <strong style="background:#e9e2cd; padding:4px 12px; border-radius:40px;">${fullDict.get(inp)}</strong>`;
        else res.innerHTML = `❓ "${inp}" finns inte i ordboken`;
    }

    function adminLookup() {
        let inp = document.getElementById("adminLookupInput").value.trim().toLowerCase();
        let out = document.getElementById("adminLookupResult");
        if(!inp) { out.innerHTML = "⭐ Skriv ett svenskt ord"; return; }
        if(fullDict.has(inp)) out.innerHTML = `<strong>${inp}</strong> → ${fullDict.get(inp)}`;
        else out.innerHTML = `❓ "${inp}" saknas`;
    }

    function updateAll() { buildCategories(); buildDictionary(); if(document.getElementById("dictionary").classList.contains("active")) buildDictionary(); }

    // FLIKHANTERING
    function switchTab(tabId) {
        document.querySelectorAll('.tab-content').forEach(t => t.classList.remove('active'));
        document.getElementById(tabId).classList.add('active');
        document.querySelectorAll('nav button').forEach(btn => btn.classList.remove('active'));
        let activeBtn = document.querySelector(`nav button[data-tab="${tabId}"]`);
        if(activeBtn) activeBtn.classList.add('active');
        if(tabId === "adminPanel" && !isAdmin) { alert("Logga in som admin först"); switchTab("learn"); }
        if(tabId === "quiz") randomQuizWord();
        if(tabId === "categories") buildCategories();
        if(tabId === "dictionary") buildDictionary();
    }

    // INIT
    loadAdminPassword(); loadCustomWords(); rebuildFullDict(); refreshCustomList(); updateAll(); setAdminMode(false);
    document.getElementById("adminLoginBtn").onclick = () => { if(isAdmin) setAdminMode(false); else promptAdminLogin(); };
    document.getElementById("addWordBtn").onclick = () => { let sv=document.getElementById("newSvWord").value, ko=document.getElementById("newKoWord").value; if(addCustomWord(sv,ko)){ alert("Ord tillagt!"); document.getElementById("newSvWord").value=""; document.getElementById("newKoWord").value=""; updateAll(); } else alert("Kunde inte lägga till"); };
    document.getElementById("resetCustomWords").onclick = resetCustomWords;
    document.getElementById("searchBtn").onclick = translate;
    document.getElementById("checkQuizBtn").onclick = checkQuiz;
    document.getElementById("newQuizBtn").onclick = () => { randomQuizWord(); document.getElementById("quizAnswer").value=""; document.getElementById("quizFeedback").innerHTML=""; };
    document.getElementById("changePwdBtn").onclick = changeAdminPassword;
    document.getElementById("adminLookupBtn").onclick = adminLookup;
    document.getElementById("dictSearch").addEventListener("input", buildDictionary);
    document.getElementById("searchInput").addEventListener("keypress", e => { if(e.key==='Enter') translate(); });
    document.getElementById("quizAnswer").addEventListener("keypress", e => { if(e.key==='Enter') checkQuiz(); });
    document.querySelectorAll("nav button[data-tab]").forEach(btn => btn.addEventListener("click", () => switchTab(btn.getAttribute("data-tab"))));
    switchTab("learn");
</script>
</body>
</html>
