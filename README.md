# Utopia-<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Vocabulario</title>
<style>
body { margin:0; font-family: 'Segoe UI', sans-serif; background:#1b1b1b; color:#fff; display:flex; flex-direction:column; align-items:center; min-height:100vh;}
header { width:100%; background:linear-gradient(90deg,#0b76ef,#0056b3); padding:15px; text-align:center; font-size:2em; font-weight:bold; box-shadow:0 4px 8px rgba(0,0,0,0.3);}
.container { margin-top:30px; width:95%; max-width:900px; display:flex; flex-direction:column; align-items:center;}
.panel { background:#2b2b2b; padding:20px; border-radius:10px; box-shadow:0 6px 12px rgba(0,0,0,0.4); width:100%; margin-bottom:20px;}
input[type="text"] { width:70%; padding:12px; margin:8px 0; border-radius:6px; border:none; font-size:1em;}
button { padding:12px 20px; margin:8px; border:none; border-radius:6px; background-color:#0b76ef; color:white; font-weight:bold; cursor:pointer;}
button:hover { background-color:#0056b3;}
#word-list { list-style:none; padding:0; width:100%;}
li { background:#3b3b3b; margin:10px 0; padding:12px; border-radius:6px;}
.word-title { font-weight:bold; font-size:1.1em; }
.word-definition { margin-top:5px; color:#ccc; font-size:0.95em;}
</style>
</head>
<body>

<header>Vocabulario</header>

<div class="container">

<div class="panel">
    <input type="text" id="search-query" placeholder="Busca en Google o DuckDuckGo...">
    <button onclick="search()">🔍 Buscar</button>
</div>

<div class="panel">
    <input type="text" id="word-input" placeholder="Nueva palabra">
    <input type="text" id="definition-input" placeholder="Definición">
    <button onclick="addWord()">Añadir palabra</button>
    <button onclick="clearWords()">Borrar todas</button>
    <ul id="word-list"></ul>
</div>

</div>

<script>
function search() {
    const q = document.getElementById('search-query').value.trim();
    if(!q) return;
    const url = 'https://duckduckgo.com/?q=' + encodeURIComponent(q);
    window.open(url,'_blank','width=1000,height=700,noopener,noreferrer');
}

const words = [];
function addWord() {
    const w = document.getElementById('word-input').value.trim();
    const d = document.getElementById('definition-input').value.trim();
    if(!w || !d) return;
    words.push({w,d});
    renderWords();
    document.getElementById('word-input').value='';
    document.getElementById('definition-input').value='';
}
function clearWords() {
    if(confirm("¿Borrar todas las palabras temporales?")) {
        words.length=0;
        renderWords();
    }
}
function renderWords() {
    const list=document.getElementById('word-list');
    list.innerHTML='';
    words.forEach(item=>{
        const li=document.createElement('li');
        const title=document.createElement('div');
        title.className='word-title';
        title.textContent=item.w;
        const def=document.createElement('div');
        def.className='word-definition';
        def.textContent=item.d;
        li.appendChild(title);
        li.appendChild(def);
        list.appendChild(li);
    });
}
</script>

</body>
</html>
