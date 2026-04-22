<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Parsel Translator | TheCraft Industrys</title>
<style>
:root{--bg:#020617;--accent:#22c55e;--card:#0f172a}
body{margin:0;font-family:Segoe UI,Arial;background:var(--bg);color:#e2e8f0}
header{padding:15px 30px;display:flex;justify-content:space-between;align-items:center;background:#020617;border-bottom:1px solid #134e4a}
header h1{color:var(--accent)}
nav a{margin-left:15px;color:#e2e8f0;text-decoration:none;cursor:pointer}
.hero{height:300px;display:flex;flex-direction:column;justify-content:center;align-items:center;background:linear-gradient(#020617, #000)}
.hero h2{font-size:32px;color:var(--accent)}
.container{max-width:1000px;margin:auto;padding:20px}
.flex{display:flex;gap:15px}
textarea{flex:1;height:120px;background:#000;border:none;color:var(--accent);padding:10px;border-radius:10px}
button{padding:10px;border:none;border-radius:10px;background:var(--accent);cursor:pointer}
.footer{margin-top:40px;padding:20px;text-align:center;border-top:1px solid #134e4a;font-size:13px}
.cookie{position:fixed;bottom:0;width:100%;background:#111;padding:10px;text-align:center}
.hidden{display:none}
.controls{margin-top:10px;display:flex;gap:10px}
</style>
</head>
<body>

<header>
<h1>🐍 Parsel</h1>
<nav>
<a id="navHome">Home</a>
<a id="navTranslator">Translator</a>
<a id="navSettings">Settings</a>
<a id="navSources">Sources</a>
</nav>
</header>

<div id="home" class="hero">
<h2>Speak the Language of Serpents</h2>
<p>Professional Parsel Translator</p>
<button id="startBtn">Start Translating</button>
</div>

<div id="translator" class="container hidden">
<h2>Translator</h2>
<div class="flex">
<textarea id="input" placeholder="Input..."></textarea>
<textarea id="output" placeholder="Output..." readonly></textarea>
</div>
<div class="controls">
<button id="translateBtn">Translate</button>
<button id="swapBtn">⇄ Swap</button>
<button id="backBtn">← Back</button>
</div>
</div>

<div id="settings" class="container hidden">
<h2>Settings</h2>
<p>• Smart Mode: Enabled</p>
<p>• Language Detection: Auto</p>
<p>• Version: 3.0 Pro</p>
</div>

<div class="footer">
<p>© 2026 TheCraft Industrys</p>
<p>Contact | Development | Legal</p>
</div>

<div id="cookie" class="cookie">
This site uses cookies to improve your experience.
<button id="cookieBtn">Accept</button>
</div>

<script>
document.addEventListener("DOMContentLoaded",()=>{

const map={a:"Haa",b:"Eetha",c:"Hass",d:"Sssha",e:"ssss",f:"Hassay",g:"Eeth",h:"Seetha",i:"Aya",j:"Sheay",k:"ayath",l:"hatehh",m:"sshhhh",n:"hathh",o:"Ayeeh",p:"Aah",q:"Atheya",r:"Hassey",s:"Sshei",t:"sseya",u:"Essehie",v:"Sshatay",w:"Hahheey",x:"Seeh",y:"Haaah",z:"Ssseth"};

const tokens=Object.entries(map).map(([k,v])=>({char:k,token:v.toLowerCase()}));

let mode="auto";

function toParsel(text){
let out="";
for(let c of text){out+=map[c]?map[c]+" ":c}
return out.trim();
}

function smartDecode(text){
text=text.toLowerCase().replace(/\s+/g,'');
let results=[];

function dfs(i,str){
if(i===text.length){results.push(str);return}
for(let t of tokens){
if(text.startsWith(t.token,i)) dfs(i+t.token.length,str+t.char);
}
}

dfs(0,"");
return results[0] || "?";
}

function translate(){
let text=document.getElementById('input').value.toLowerCase();
let out="";

if(mode==='toParsel'){
out=toParsel(text);
}else if(mode==='fromParsel'){
out=smartDecode(text);
}else{
// auto
if(/[a-z]{2,}/.test(text)) out=toParsel(text);
else out=smartDecode(text);
}

document.getElementById('output').value=out;
}

function swap(){
mode = mode==='toParsel'?'fromParsel':'toParsel';
}

function showPage(id){
['home','translator','settings'].forEach(p=>document.getElementById(p).classList.add('hidden'));
document.getElementById(id).classList.remove('hidden');
}

function acceptCookies(){
document.getElementById('cookie').style.display='none';
}

function rickroll(){
window.open('https://www.youtube.com/watch?v=dQw4w9WgXcQ','_blank');
}

// bindings

document.getElementById('translateBtn').addEventListener('click',translate);
document.getElementById('swapBtn').addEventListener('click',swap);
document.getElementById('backBtn').addEventListener('click',()=>showPage('home'));

document.getElementById('startBtn').addEventListener('click',()=>showPage('translator'));
document.getElementById('navHome').addEventListener('click',()=>showPage('home'));
document.getElementById('navTranslator').addEventListener('click',()=>showPage('translator'));
document.getElementById('navSettings').addEventListener('click',()=>showPage('settings'));
document.getElementById('navSources').addEventListener('click',rickroll);
document.getElementById('cookieBtn').addEventListener('click',acceptCookies);

// TESTS
console.log("Encode test:", toParsel("abc"));
console.log("Decode test:", smartDecode("haaeethahass"));

});
</script>

</body>
</html>
