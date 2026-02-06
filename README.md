Your Companion To A DSHS Life! 
<html lang="en">
<head>
<meta charset="UTF-8">
<title>School System</title>
<style>
body {
  margin: 0;
  font-family: "Arial", sans-serif;
  background-color: #fff;
  background-image:
    repeating-linear-gradient(to bottom, transparent 0px, transparent 26px, rgba(0,0,0,0.08) 27px),
    url('https://www.transparenttextures.com/patterns/pencil-paper.png');
  background-size: 100% 28px, auto;
  color: #222;
}

input, button, select, textarea { width: 100%; padding: 8px; margin-top: 8px; box-sizing: border-box; }
button { background: #007bff; color: white; border: none; cursor: pointer; font-size: 14px; }
button:hover { background: #0056b3; }
.signup-link { color: #007bff; font-weight: bold; cursor: pointer; }
.signup-link:hover { text-decoration: underline; }

.login, #signup { height: 100vh; display: flex; justify-content: center; align-items: center; }
.box { background: rgba(255,255,255,0.95); padding: 20px; width: 280px; border-radius: 8px; box-shadow: 0 8px 15px rgba(0,0,0,0.3); text-align: center; }

.dashboard { display: none; height: 100vh; }
.header { background: rgba(0,51,102,0.95); color: white; padding: 15px; text-align: center; font-size: 18px; }
.container { display: flex; height: calc(100vh - 60px); }

.menu { width: 180px; background: rgba(255,255,255,0.95); padding: 5px; box-shadow: 2px 0 10px rgba(0,0,0,0.2); display: flex; flex-direction: column; }
.menu button { margin: 5px 0; padding: 8px; text-align: left; font-size: 14px; border: 1px solid black; border-radius: 4px; background: #eee; }
.menu button.toggle-btn { background: #003366; color: white; font-size: 16px; border: none; }
.menu button.logout { margin-top: auto; background: #d9534f; color: white; font-size: 14px; }

.content { flex: 1; padding: 15px; display: flex; flex-direction: column; align-items: center; overflow-y: auto; }
.section { background: rgba(255,255,255,0.9); padding: 10px; border-radius: 5px; width: 95%; margin-top: 10px; }
img.school { max-width: 90%; border-radius: 10px; margin-bottom: 15px; }
table { border-collapse: collapse; width: 100%; }
table, th, td { border: 1px solid #000; text-align: center; padding: 5px; }
.edit { border: 1px solid #ccc; }
.view-only { background: #f9f9f9; pointer-events: none; }
.subsection { background: rgba(245,245,245,0.8); padding: 8px; margin-top: 8px; border-radius: 5px; text-align: left; }

@media screen and (max-width: 768px){
  .container { flex-direction: column; }
  .menu { width: 100%; display: flex; flex-direction: row; flex-wrap: wrap; }
  .menu button { flex: 1 1 45%; margin: 3px; }
  .content { width: 100%; padding: 10px; }
}
</style>
</head>

<body>

<div class="login" id="login">
  <div class="box">
    <h2>Login</h2>
    <input type="text" id="username" placeholder="Username">
    <input type="password" id="password" placeholder="Enter password">
    <button onclick="login()">Login</button>
    <p style="font-size:13px; margin-top:10px;">
      Don’t have an account yet? 
      <span class="signup-link" onclick="showSignup()">Sign up!</span>
    </p>
    <p id="msg"></p>
  </div>
</div>

<div class="login" id="signup" style="display:none;">
  <div class="box">
    <h2>Student Sign Up</h2>
    <input type="text" id="su_name" placeholder="Full Name">
    <input type="text" id="su_id" placeholder="Student I.D">
    <input type="text" id="su_section" placeholder="Section">
    <input type="text" id="su_track" placeholder="Track">
    <input type="text" id="su_strand" placeholder="Strand">
    <input type="text" id="su_grade" placeholder="Grade Level">
    <button onclick="submitSignup()">Create Account</button>
    <p style="font-size:13px; margin-top:10px;">
      Already have an account? 
      <span class="signup-link" onclick="showLogin()">Login</span>
    </p>
  </div>
</div>

<div class="dashboard" id="dashboard">
  <div class="header" id="roleTitle"></div>
  <div class="container">
    <div class="menu" id="menu"></div>
    <div class="content" id="content">
      <img src="https://source.unsplash.com/800x400/?school" alt="School" class="school">
      <div class="section">
        <h3>Welcome</h3>
        <p>Select an option from the menu.</p>
      </div>
    </div>
  </div>
</div>

<script>
// ---------- LOAD DATA ----------
let students=JSON.parse(localStorage.getItem("students")) || [
  {name:"Jibdel", id:"ST001", section:"7A", track:"Academic", strand:"STEM", gradeLevel:"7"},
  {name:"Viennes", id:"ST002", section:"7A", track:"Academic", strand:"ABM", gradeLevel:"7"},
  {name:"Jurl", id:"ST003", section:"7B", track:"Academic", strand:"STEM", gradeLevel:"7"},
  {name:"Sam", id:"ST004", section:"7B", track:"Academic", strand:"ABM", gradeLevel:"7"},
  {name:"Justine", id:"ST005", section:"7C", track:"Academic", strand:"STEM", gradeLevel:"7"},
  {name:"Ashley", id:"ST006", section:"7C", track:"Academic", strand:"ABM", gradeLevel:"7"},
  {name:"Gerlie", id:"ST007", section:"7D", track:"Academic", strand:"STEM", gradeLevel:"7"},
  {name:"Meriem", id:"ST008", section:"7D", track:"Academic", strand:"ABM", gradeLevel:"7"}
];

let subjects=["Math","Science","Filipino","English","MAPEH","AP"];
let currentUser=null;

// ---------- LOGIN ----------
function login(){
  const username=document.getElementById("username").value;
  const password=document.getElementById("password").value;
  
  if(username==="teacher" && password==="teacher123"){ 
    role="teacher"; 
    currentUser={name:"Mr. Santos", id:"T001", position:"Teacher III", sectionHandled:"7A-7D"}; 
  }
  else{
    let found=students.find(s=>s.id===username && password==="student123");
    if(found){ role="student"; currentUser=found; }
    else{ document.getElementById("msg").innerText="Invalid login"; return; }
  }
  
  document.getElementById("login").style.display="none";
  document.getElementById("signup").style.display="none";
  document.getElementById("dashboard").style.display="block";
  loadDashboard();
}

// ---------- SIGNUP ----------
function showSignup(){ document.getElementById("login").style.display="none"; document.getElementById("signup").style.display="flex"; }
function showLogin(){ document.getElementById("signup").style.display="none"; document.getElementById("login").style.display="flex"; }
function submitSignup(){
  let newStudent={
    name: document.getElementById("su_name").value,
    id: document.getElementById("su_id").value,
    section: document.getElementById("su_section").value,
    track: document.getElementById("su_track").value,
    strand: document.getElementById("su_strand").value,
    gradeLevel: document.getElementById("su_grade").value
  };
  students.push(newStudent);
  localStorage.setItem("students", JSON.stringify(students));
  alert("Signup successful! You can now log in.");
  showLogin();
}

// ---------- DASHBOARD ----------
function loadDashboard(){
  document.getElementById("roleTitle").innerText=role.toUpperCase()+" DASHBOARD";
  
  const menu=document.getElementById("menu");
  menu.innerHTML="";
  
  const toggle=document.createElement("button");
  toggle.innerText="☰"; toggle.className="toggle-btn"; toggle.onclick=toggleMenu;
  menu.appendChild(toggle);
  
  let items=[];
  if(role==="teacher"){ items=["Attendance","Grades","Student Files","Parents","My Info","Planner","Bulletin Board"]; }
  else if(role==="student"){ items=["Attendance","Grades","AI Chat","My Info","Planner","Bulletin Board"]; }
  
  items.forEach(it=>{
    const btn=document.createElement("button");
    btn.innerText=it;
    btn.onclick=()=>loadSection(it);
    menu.appendChild(btn);
  });
  
  const logoutBtn=document.createElement("button");
  logoutBtn.innerText="Logout"; logoutBtn.className="logout"; logoutBtn.onclick=logout;
  menu.appendChild(logoutBtn);
  
  showWelcome();
}

function toggleMenu(){ document.getElementById("menu").classList.toggle("collapsed"); }
function logout(){ role=""; currentUser=null; document.getElementById("dashboard").style.display="none"; document.getElementById("login").style.display="flex"; }

// ---------- CONTENT ----------
function showWelcome(){
  const content=document.getElementById("content");
  content.innerHTML=`<img src="https://source.unsplash.com/800x400/?school" class="school">
  <div class="section"><h3>Welcome</h3><p>Select an option from the menu.</p></div>`;
}

function loadSection(name){
  const content=document.getElementById("content");
  content.innerHTML="";
  
  const img=document.createElement("img");
  img.src="https://source.unsplash.com/800x400/?school";
  img.className="school";
  content.appendChild(img);
  
  if(name==="Attendance"){
    const section=document.createElement("div"); section.className="section";
    let html="<h3>Attendance</h3><table><tr><th>Name</th>";
    for(let i=1;i<=5;i++) html+=`<th>Day ${i}</th>`; html+="</tr>";
    students.forEach((s,index)=>{
      html+=`<tr><td>${s.name}</td>`;
      for(let i=0;i<5;i++){
        let checked=localStorage.getItem(`${s.id}_day${i}`)=="true" ? "checked" : "";
        html+=`<td><input type="checkbox" onchange="saveAttendance('${s.id}',${i},this.checked)" ${checked}></td>`;
      }
      html+="</tr>";
    });
    section.innerHTML=html+"</table>"; content.appendChild(section);
  }
  
  if(name==="Grades"){
    const section=document.createElement("div"); section.className="section";
    let html="<h3>Grades</h3><table><tr><th>Subject</th>";
    students.forEach(s=>{ html+=`<th>${s.name}</th>`; });
    html+="</tr>";
    subjects.forEach((sub,i)=>{
      html+=`<tr><td>${sub}</td>`;
      students.forEach(s=>{
        let g=localStorage.getItem(`${s.id}_${sub}`) || Math.floor(Math.random()*21)+80;
        html+=`<td><input type="text" value="${g}" onchange="saveGrade('${s.id}','${sub}',this.value)"></td>`;
      });
      html+="</tr>";
    });
    section.innerHTML=html+"</table>"; content.appendChild(section);
  }
  
  if(name==="My Info"){
    const section=document.createElement("div"); section.className="section";
    if(role==="teacher"){
      section.innerHTML=`<h3>My Info</h3>
      <p><strong>Name:</strong> ${currentUser.name}</p>
      <p><strong>Teacher I.D:</strong> ${currentUser.id}</p>
      <p><strong>Position:</strong> ${currentUser.position}</p>
      <p><strong>Section Handled:</strong> ${currentUser.sectionHandled}</p>`;
    } else if(role==="student"){
      section.innerHTML=`<h3>My Info</h3>
      <p><strong>Name:</strong> ${currentUser.name}</p>
      <p><strong>Student I.D:</strong> ${currentUser.id}</p>
      <p><strong>Section:</strong> ${currentUser.section}</p>
      <p><strong>Track:</strong> ${currentUser.track}</p>
      <p><strong>Strand:</strong> ${currentUser.strand}</p>
      <p><strong>Grade Level:</strong> ${currentUser.gradeLevel}</p>`;
    }
    content.appendChild(section);
  }
  
  if(name==="Planner" || name==="Bulletin Board" || name==="Student Files" || name==="AI Chat"){
    const section=document.createElement("div"); section.className="section";
    section.innerHTML=`<h3>${name}</h3><p>Sample content for ${name}...</p>`;
    content.appendChild(section);
  }
}

// ---------- SAVE DATA ----------
function saveAttendance(id,day,value){
  localStorage.setItem(`${id}_day${day}`, value);
}

function saveGrade(id,sub,value){
  localStorage.setItem(`${id}_${sub}`, value);
}

</script>
</body>
</html>
