<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">

<meta name="viewport"
content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">

<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="Iron Man OS">

<link rel="apple-touch-icon"
href="https://img.icons8.com/plasticine/200/iron-man.png">

<title>⚡ Iron Man OS</title>

<style>

@import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Rajdhani:wght@400;500;600;700&display=swap');

*{
margin:0;
padding:0;
box-sizing:border-box;
-webkit-tap-highlight-color:transparent;
}

:root{
--arc:#00d4ff;
--pink:#ff8cb4;
--glass:rgba(255,255,255,0.06);
--glass-b:rgba(0,212,255,0.18);
--text:#e8f4ff;
--muted:#7a9ab8;
}

body{
font-family:'Rajdhani',sans-serif;
background:#050c14;
min-height:100vh;
color:var(--text);
overflow-x:hidden;
overflow-y:auto;
width:100%;
}

#successOverlay{
position:fixed;
inset:0;
background:rgba(0,0,0,0.9);
z-index:9999;
display:none;
flex-direction:column;
align-items:center;
justify-content:center;
backdrop-filter:blur(10px);
text-align:center;
padding:20px;
}

.app{
max-width:440px;
margin:auto;
padding:18px 15px 120px;
min-height:100vh;
overflow-y:auto;
display:none;
-webkit-overflow-scrolling:touch;
}

.app.active{
display:block;
}

.header{
margin-top:18px;
margin-bottom:20px;
}

.header h1{
font-family:'Orbitron',sans-serif;
font-size:20px;
font-weight:900;
color:var(--arc);
text-shadow:0 0 18px rgba(0,212,255,0.45);
}

.pinned-banner{
background:linear-gradient(
135deg,
rgba(0,212,255,0.11),
rgba(0,80,130,0.16)
);

border:1px solid rgba(0,212,255,0.32);
border-left:4px solid var(--arc);

border-radius:16px;
padding:15px 16px;
margin-bottom:16px;

min-height:80px;

display:flex;
align-items:center;
justify-content:center;
}

#pinnedText{
font-weight:600;
text-align:center;
line-height:1.4;
font-size:16px;
}

.card{
background:var(--glass);
border:1px solid var(--glass-b);
border-radius:20px;
padding:18px;
margin-bottom:14px;
backdrop-filter:blur(12px);
}

.card h2{
font-family:'Orbitron',sans-serif;
font-size:11px;
color:var(--arc);
letter-spacing:1px;
margin-bottom:12px;
text-transform:uppercase;
}

input,
textarea,
select{
width:100%;
background:rgba(0,0,0,0.38);
border:1px solid var(--glass-b);
border-radius:12px;
color:var(--text);
padding:11px 13px;
font-family:'Rajdhani',sans-serif;
font-size:16px;
margin-bottom:10px;
outline:none;
}

.btn{
border:none;
border-radius:12px;
padding:12px 16px;
cursor:pointer;
font-family:'Rajdhani',sans-serif;
font-size:14px;
font-weight:700;
}

.btn-primary{
background:linear-gradient(
135deg,
var(--arc),
#0099bb
);

color:#000;
width:100%;
}

.btn-pink{
background:linear-gradient(
135deg,
var(--pink),
#ff5c93
);

color:#000;
width:100%;
}

.item-row{
background:rgba(0,0,0,0.28);
border:1px solid var(--glass-b);
border-radius:15px;
padding:14px;
margin-bottom:10px;
display:flex;
justify-content:space-between;
align-items:center;
}

.item-row.done{
opacity:.45;
text-decoration:line-through;
}

input[type="checkbox"]{
width:24px;
height:24px;
margin:0;
}

.history-entry{
border-bottom:1px solid var(--glass-b);
padding:15px 0;
}

.h-date{
color:var(--arc);
font-weight:700;
font-family:'Orbitron';
font-size:13px;
margin-bottom:5px;
}

.h-body{
font-size:13px;
color:var(--muted);
margin-top:8px;
line-height:1.4;
}

.bottom-nav{
position:fixed;
bottom:0;
left:0;
width:100%;
background:rgba(4,11,20,0.97);
border-top:1px solid var(--glass-b);
display:flex;
justify-content:space-around;
padding:12px 0 25px;
z-index:999;
}

.nav-item{
color:var(--muted);
text-align:center;
font-size:10px;
cursor:pointer;
flex:1;
}

.nav-item.active{
color:var(--arc);
}

.nav-item.active-pink{
color:var(--pink);
}

.nav-item .icon{
display:block;
font-size:22px;
margin-bottom:4px;
}

</style>
</head>

<body>

<div id="successOverlay"
onclick="this.style.display='none'">

<h2 style="
font-family:'Orbitron';
color:var(--arc);
margin-bottom:15px;
letter-spacing:2px;
">
MISSION COMPLETE
</h2>

<div id="mediaContainer"
style="
width:100%;
display:flex;
justify-content:center;
">
</div>

</div>

<div id="homePage" class="app active">

<div class="header">
<h1>INITIATING PROTOCOL ⚡</h1>
</div>

<div class="pinned-banner">
<div id="pinnedText">
Ready for deployment...
</div>
</div>

<div class="card">

<h2>⚙️ CHOOSE PRESET VIBE</h2>

<select id="quoteSelector"
onchange="applyPresetQuote()">
</select>

</div>

<div class="card">

<h2>⚡ DAILY PROTOCOLS</h2>

<div id="habitList"></div>

<input
type="text"
id="habitInput"
placeholder="New Core Habit..."
>

<button
class="btn btn-primary"
onclick="addHabit()"
>
Add Protocol
</button>

</div>

</div>

<div id="studyPage" class="app">

<div class="header">
<h1>📚 STUDY HUD</h1>
</div>

<div class="card">

<h2>⏳ POMODORO</h2>

<div id="pomoTime"
style="
font-family:'Orbitron';
font-size:42px;
text-align:center;
color:var(--arc);
margin:10px 0;
">
25:00
</div>

<button
class="btn btn-primary"
id="pomoBtn"
onclick="togglePomo()"
>
START SEQUENCE
</button>

</div>

<div class="card">

<h2>📝 DAILY MISSIONS</h2>

<div id="dailyStudyList"></div>

<textarea
id="dailyStudyInput"
placeholder="New missions..."
></textarea>

<button
class="btn btn-primary"
onclick="addStudyTask()"
>
Deploy Missions
</button>

</div>

</div>

<div id="archivePage" class="app">

<div class="header">
<h1>📂 MASTER ARCHIVE</h1>
</div>

<div class="card">

<h2>📜 PERMANENT NOTES</h2>

<textarea
id="permanentNotes"
placeholder="General journal/notes..."
rows="4"
oninput="savePermanentNotes()"
></textarea>

</div>

<div class="card">

<h2>🕰️ CHRONOLOGICAL LOGS</h2>

<div id="masterArchiveList"></div>

</div>

</div>

<div id="periodPage" class="app">

<div class="header">
<h1 style="color:var(--pink)">
🩷 RED ROOM
</h1>
</div>

<div class="card">

<h2 style="color:var(--pink)">
📊 PREDICTIONS
</h2>

<div style="font-size:14px; margin-bottom:5px;">
Next Period:
<span id="nextPeriodDate"
style="color:var(--pink)">
--
</span>
</div>

<div style="font-size:14px;">
Power Window:
<span id="ovulationDate"
style="color:var(--pink)">
--
</span>
</div>

</div>

<div class="card">

<h2 style="color:var(--pink)">
📑 TODAY'S LOG
</h2>

<textarea
id="periodSymptoms"
placeholder="Symptoms, mood, meds..."
rows="4"
oninput="saveDailyPeriod()"
></textarea>

</div>

<div class="card">

<h2>🛠️ CALIBRATE</h2>

<input
type="date"
id="lastPeriodInput"
>

<button
class="btn btn-pink"
onclick="updatePeriodData()"
>
Update Cycle
</button>

</div>

</div>

<nav class="bottom-nav">

<div
class="nav-item active"
id="nav-home"
onclick="showPage('home')"
>
<span class="icon">🏠</span>
Home
</div>

<div
class="nav-item"
id="nav-study"
onclick="showPage('study')"
>
<span class="icon">📚</span>
Study
</div>

<div
class="nav-item"
id="nav-archive"
onclick="showPage('archive')"
>
<span class="icon">📂</span>
History
</div>

<div
class="nav-item"
id="nav-period"
onclick="showPage('period')"
>
<span class="icon">🩷</span>
Period
</div>

</nav>

<script>

const quotes = [

"Hot people finish their tasks 💅",

"Delulu but still productive ✨",

"Romanticize the grind, bestie 🌸",

"Locked in… kinda 🔒",

"Your future self is side-eyeing you 👀",

"Productivity looks good on you 😌",

"Do it for the plot 🎬",

"Tiny habits. Huge slay 💖",

"Focus, babe. Chaos later 🧠",

"Locked in era activated ⚡",

"Your comeback starts with one checkbox ☑️",

"Future millionaire behavior starts now 💸",

"Go make today less embarrassing 💀",

"✨ Custom Motivation"

];

const successMedia = [
"treats.mp4",
"cat.mp4",
"outfit.gif"
];

let habits =
JSON.parse(localStorage.getItem('habits')) || [];

let dailyTasks =
JSON.parse(localStorage.getItem('dailyTasks')) || [];

let masterArchive =
JSON.parse(localStorage.getItem('masterArchive')) || [];

let pomoTimer;

function save(){

localStorage.setItem(
'habits',
JSON.stringify(habits)
);

localStorage.setItem(
'dailyTasks',
JSON.stringify(dailyTasks)
);

}

function checkDailyReset(){

const today =
new Date().toDateString();

const lastDate =
localStorage.getItem('lastOpenDate');

if(lastDate && lastDate !== today){

const logEntry = {

date:lastDate,

habits:[...habits],

study:[...dailyTasks],

period:
localStorage.getItem('periodLogs_today')
|| "No notes logged.",

permanentNotes:
localStorage.getItem('permanentNotes')
|| ""

};

masterArchive.unshift(logEntry);

localStorage.setItem(
'masterArchive',
JSON.stringify(masterArchive)
);

habits.forEach(h=>h.done=false);

dailyTasks.forEach(t=>t.done=false);

localStorage.removeItem(
'periodLogs_today'
);

save();

renderHome();

renderStudy();
}

localStorage.setItem(
'lastOpenDate',
today
);

}

function startDayWatcher(){

setInterval(()=>{

checkDailyReset();

},60000);

document.addEventListener(
"visibilitychange",
()=>{

if(!document.hidden){
checkDailyReset();
}
});
}

function triggerSuccess(){

const overlay =
document.getElementById('successOverlay');

overlay.style.display='flex';

setTimeout(()=>{

overlay.style.display='none';

},3000);

}

function showPage(page){

document
.querySelectorAll('.app')
.forEach(p=>p.classList.remove('active'));

document
.querySelectorAll('.nav-item')
.forEach(n=>
n.classList.remove(
'active',
'active-pink'
)
);

document
.getElementById(page+'Page')
.classList.add('active');

const nav =
document.getElementById(
'nav-'+page
);

if(page === 'period'){

nav.classList.add('active-pink');

}else{

nav.classList.add('active');
}

if(page === 'archive'){
renderArchive();
}
}

function addHabit(){

const input =
document.getElementById('habitInput');

if(!input.value.trim()) return;

habits.push({
name:input.value,
done:false
});

input.value="";

save();

renderHome();
}

function toggleHabit(i){

habits[i].done =
!habits[i].done;

if(habits[i].done){
triggerSuccess();
}

save();

renderHome();
}

function renderHome(){

const hList =
document.getElementById('habitList');

hList.innerHTML="";

habits.forEach((h,i)=>{

hList.innerHTML += `
<div class="item-row ${h.done?'done':''}">

<span>${h.name}</span>

<input
type="checkbox"
${h.done?'checked':''}
onchange="toggleHabit(${i})">

</div>
`;
});
}

function addStudyTask(){

const input =
document.getElementById(
'dailyStudyInput'
);

input.value
.split('\n')
.forEach(t=>{

if(t.trim()){

dailyTasks.push({
text:t,
done:false
});
}
});

input.value="";

save();

renderStudy();
}

function renderStudy(){

const dList =
document.getElementById(
'dailyStudyList'
);

dList.innerHTML="";

dailyTasks.forEach((t,i)=>{

dList.innerHTML += `
<div class="item-row ${t.done?'done':''}">

<span>${t.text}</span>

<input
type="checkbox"
${t.done?'checked':''}

onchange="
dailyTasks[${i}].done=
!dailyTasks[${i}].done;

save();

renderStudy();
">

</div>
`;
});
}

function renderArchive(){

const list =
document.getElementById(
'masterArchiveList'
);

list.innerHTML="";

masterArchive.forEach(item=>{

list.innerHTML += `
<div class="history-entry">

<div class="h-date">
${item.date}
</div>

<div class="h-body">

<b>Tasks:</b><br>

${item.study.map(
t=>`${t.text}
${t.done?'✅':'❌'}`
).join('<br>')}

</div>

</div>
`;
});
}

function saveDailyPeriod(){

localStorage.setItem(
'periodLogs_today',

document.getElementById(
'periodSymptoms'
).value
);

}

function savePermanentNotes(){

localStorage.setItem(
'permanentNotes',

document.getElementById(
'permanentNotes'
).value
);

}

function updatePeriodData(){

const lastDate =
document.getElementById(
'lastPeriodInput'
).value;

if(!lastDate) return;

localStorage.setItem(
'lastPeriod',
lastDate
);

const start =
new Date(lastDate);

const next =
new Date(start);

next.setDate(
start.getDate()+28
);

const ovu =
new Date(start);

ovu.setDate(
start.getDate()+14
);

document.getElementById(
'nextPeriodDate'
).innerText =
next.toDateString();

document.getElementById(
'ovulationDate'
).innerText =
ovu.toDateString();
}

function togglePomo(){

if(pomoTimer){

clearInterval(pomoTimer);

pomoTimer=null;

document.getElementById(
'pomoBtn'
).innerText=
"START SEQUENCE";

}else{

let s=1500;

document.getElementById(
'pomoBtn'
).innerText=
"STOP SEQUENCE";

pomoTimer=setInterval(()=>{

s--;

let m=Math.floor(s/60);

let sec=s%60;

document.getElementById(
'pomoTime'
).innerText=
`${m}:${sec<10?'0'+sec:sec}`;

if(s<=0){

clearInterval(pomoTimer);

triggerSuccess();
}

},1000);
}
}

function applyPresetQuote(){

const val =
document.getElementById(
'quoteSelector'
).value;

if(val ===
"✨ Custom Motivation"){

const custom =
prompt(
"Enter your motivation ✨"
);

if(!custom) return;

document.getElementById(
'pinnedText'
).innerText =
custom;

localStorage.setItem(
'customQuote',
custom
);

}else{

document.getElementById(
'pinnedText'
).innerText =
val;
}

localStorage.setItem(
'activeQuote',
val
);
}

window.onload = ()=>{

checkDailyReset();

startDayWatcher();

const sel =
document.getElementById(
'quoteSelector'
);

quotes.forEach(q=>{

let opt =
document.createElement('option');

opt.value=q;

opt.innerText=q;

sel.appendChild(opt);
});

const activeQuote =
localStorage.getItem(
'activeQuote'
) || quotes[0];

if(activeQuote ===
"✨ Custom Motivation"){

document.getElementById(
'pinnedText'
).innerText =

localStorage.getItem(
'customQuote'
) ||

"Your custom motivation ✨";

}else{

document.getElementById(
'pinnedText'
).innerText =
activeQuote;
}

document.getElementById(
'permanentNotes'
).value =

localStorage.getItem(
'permanentNotes'
) || "";

document.getElementById(
'periodSymptoms'
).value =

localStorage.getItem(
'periodLogs_today'
) || "";

document.getElementById(
'lastPeriodInput'
).value =

localStorage.getItem(
'lastPeriod'
) || "";

updatePeriodData();

renderHome();

renderStudy();

};

</script>

</body>
</html>
