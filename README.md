Your Companion To A DSHS Life! 
<html lang="en">
<head>
<meta charset="UTF-8">
<title>DSHS School System</title>
<style>
  /* ---------- NOTES PAPER BACKGROUND ---------- */
body {
  margin: 0;
  font-family: "Allassy Caps", serif;
  background-color: #fff;

  /* dotted lines + subtle scribbles */
  background-image:
    repeating-linear-gradient(to bottom, transparent 0px, transparent 26px, rgba(0,0,0,0.1) 27px),
    url('data:image/svg+xml,%3Csvg width="100" height="100" xmlns="http://www.w3.org/2000/svg"%3E%3Cpath d="M10 10 q5 5 10 0" stroke="rgba(0,0,0,0.05)" stroke-width="1" fill="none"/%3E%3C/svg%3E');
  background-size: 100% 28px, 50px 50px;
  color: #222;
}

/* ---------- LOGIN & SIGNUP ---------- */
.login {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.box {
  background: rgba(255,255,255,0.95);
  padding: 25px;
  width: 300px;
  border-radius: 8px;
  box-shadow: 0 10px 20px rgba(0,0,0,0.3);
  text-align: center;
}

input, button, select, textarea {
  width: 100%;
  padding: 10px;
  margin-top: 10px;
}

button {
  background: #007bff;
  color: white;
  border: none;
  cursor: pointer;
}

.signup-link {
  color: #007bff;
  font-weight: bold;
  cursor: pointer;
}

.signup-link:hover {
  text-decoration: underline;
}

/* ---------- DASHBOARD ---------- */
.dashboard {
  display: none;
  height: 100vh;
}

.header {
  background: rgba(0,51,102,0.95);
  color: white;
  padding: 15px;
  text-align: center;
  font-size: 18px;
}

.container {
  display: flex;
  height: calc(100vh - 60px);
}

/* ---------- MENU ---------- */
.menu {
  width: 220px;
  background: rgba(255,255,255,0.95);
  padding: 10px;
  box-shadow: 2px 0 10px rgba(0,0,0,0.2);
  display: flex;
  flex-direction: column;
  transition: width 0.3s;
}

.menu.collapsed {
  width: 60px;
}

.menu button {
  background: #eee;
  color: black;
  margin-top: 6px;
  font-size: 14px;
  white-space: nowrap;
  overflow: hidden;
  border: 1px solid #000; /* black border for menu buttons */
  border-radius: 4px;
  padding: 8px;
}

.menu.collapsed button {
  font-size: 0;
}

.menu.collapsed button::before {
  content: "•";
  font-size: 18px;
}

.toggle-btn {
  background: #003366;
  color: white;
  font-size: 18px;
}

.logout {
  margin-top: auto;
  background: #d9534f !important;
  color: white !important;
  font-size: 14px !important;
}

/* ---------- CONTENT ---------- */
.content {
  flex: 1;
  padding: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  overflow-y: auto;
}

.section {
  background: rgba(255,255,255,0.9);
  padding: 15px;
  border-radius: 5px;
  width: 90%;
  margin-top: 15px;
}

img.school {
  max-width: 80%;
  border-radius: 10px;
  margin-bottom: 20px;
}

table {
  border-collapse: collapse;
  width: 100%;
  margin-bottom: 15px;
}

table, th, td {
  border: 1px solid #ccc;
  text-align: center;
  padding: 5px;
}

.edit {
  border: 1px solid #ccc;
}

.view-only {
  background: #f9f9f9;
  pointer-events: none;
}

.subsection {
  background: rgba(245,245,245,0.8);
  padding: 10px;
  margin-top: 10px;
  border-radius: 5px;
  text-align: left;
}

/* ---------- MOBILE ---------- */
@media screen and (max-width: 768px) {
  .container { flex-direction: column; }
  .menu { width: 100%; display: flex; flex-wrap: wrap; }
  .menu button { flex: 1 1 48%; margin: 5px; }
  .content { width: 100%; padding: 10px; }
}
</style>
</head>

<body>

<!-- LOGIN -->
<div class="login" id="login">
  <div class="box">
    <h2>Login</h2>
    <input type="text" id="username" placeholder="Enter username">
    <input type="password" id="password" placeholder="Enter password">
    <button onclick="login()">Login</button>

    <p style="font-size:13px; margin-top:15px;">
      Don’t have an account yet?
      <span class="signup-link" onclick="showSignup()">Sign up!</span>
    </p>

    <p id="msg"></p>
  </div>
</div>

<!-- SIGN UP -->
<div class="login" id="signup" style="display:none;">
  <div class="box">
    <h2>Student Sign Up</h2>
    <input type="text" id="suName" placeholder="Full Name">
    <input type="text" id="suID" placeholder="Student I.D">
    <input type="text" id="suSection" placeholder="Section">
    <input type="text" id="suTrack" placeholder="Track">
    <input type="text" id="suStrand" placeholder="Strand">
    <input type="text" id="suGrade" placeholder="Grade Level">
    <button onclick="submitSignup()">Create Account</button>
    <p style="font-size:13px; margin-top:10px;">
      Already have an account?
      <span class="signup-link" onclick="showLogin()">Login</span>
    </p>
  </div>
</div>

<!-- DASHBOARD -->
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
// ---------- PREDEFINED DATA ----------
let role = "";
let students = [
  {name:"Jibdel", id:"S001", section:"10A", track:"STEM", strand:"Science", grade:"10"},
  {name:"Viennes", id:"S002", section:"10B", track:"ABM", strand:"Business", grade:"10"},
  {name:"Jurl", id:"S003", section:"10C", track:"GAS", strand:"Arts", grade:"10"},
  {name:"Sam", id:"S004", section:"10A", track:"STEM", strand:"Science", grade:"10"},
  {name:"Justine", id:"S005", section:"10B", track:"ABM", strand:"Business", grade:"10"},
  {name:"Ashley", id:"S006", section:"10C", track:"GAS", strand:"Arts", grade:"10"},
  {name:"Gerlie", id:"S007", section:"10A", track:"STEM", strand:"Science", grade:"10"},
  {name:"Meriem", id:"S008", section:"10B", track:"ABM", strand:"Business", grade:"10"}
];

let subjects = ["Entrepreneurship","Three eyes","🧢 🗿","Math","Pi6","P ey"];
let gradesData = {
  "1st": {"Entrepreneurship":"A","Three eyes":"B+","🧢 🗿":"C","Math":"A-","Pi6":"B","P ey":"B+"},
  "2nd": {"Entrepreneurship":"A-","Three eyes":"A","🧢 🗿":"B+","Math":"A","Pi6":"B+","P ey":"A-"}
};

let teachers = [
  {username:"mrsmith", password:"teacher", name:"Mr. Smith", id:"T001", position:"Teacher III", sectionHandled:"10A"}
];

// ---------- LOGIN ----------
function login() {
  let user = document.getElementById("username").value;
  let pass = document.getElementById("password").value;

  // check teacher
  let t = teachers.find(t => t.username===user && t.password===pass);
  if(t){ role="teacher"; currentUser=t; showDashboard(); return;}

  // check student
  let s = students.find(s => s.id===user);
  if(s){ role="student"; currentUser=s; showDashboard(); return;}

  document.getElementById("msg").innerText="Invalid username/password";
}

// ---------- DASHBOARD ----------
let currentUser = null;
function showDashboard(){
  document.getElementById("login").style.display="none";
  document.getElementById("signup").style.display="none";
  document.getElementById("dashboard").style.display="block";

  document.getElementById("roleTitle").innerText = role.toUpperCase()+" DASHBOARD";

  const menu = document.getElementById("menu");
  menu.innerHTML="";

  const toggle = document.createElement("button");
  toggle.innerText="☰"; toggle.className="toggle-btn"; toggle.onclick=toggleMenu;
  menu.appendChild(toggle);

  let items=[];
  if(role==="teacher"){
    items=["Attendance","Grades","Student Files","Parents","Subjects","Schedule","Bulletin Board","My Info"];
  } else if(role==="student"){
    items=["Attendance","Grades","Schedule","AI Chat","Bulletin Board","Planner","My Info"];
  }

  createMenu(items);

  const logoutBtn=document.createElement("button");
  logoutBtn.innerText="⬅ Logout"; logoutBtn.className="logout"; logoutBtn.onclick=logout;
  menu.appendChild(logoutBtn);
}

// ---------- MENU ----------
function createMenu(items){
  const menu=document.getElementById("menu");
  items.forEach(item=>{
    const btn=document.createElement("button");
    btn.innerText=item;
    btn.onclick=()=>loadSection(item);
    menu.appendChild(btn);
  });
}

function toggleMenu(){ document.getElementById("menu").classList.toggle("collapsed"); }
function logout(){ 
  role=""; 
  currentUser=null;
  document.getElementById("dashboard").style.display="none"; 
  document.getElementById("login").style.display="flex"; 
}

// ---------- SIGNUP ----------
function showSignup() { document.getElementById("login").style.display="none"; document.getElementById("signup").style.display="flex"; }
function showLogin() { document.getElementById("signup").style.display="none"; document.getElementById("login").style.display="flex"; }

function submitSignup() {
  let newStudent = {
    name: document.getElementById("suName").value,
    id: document.getElementById("suID").value,
    section: document.getElementById("suSection").value,
    track: document.getElementById("suTrack").value,
    strand: document.getElementById("suStrand").value,
    grade: document.getElementById("suGrade").value
  };
  students.push(newStudent);
  alert("Signup successful! You can now log in with your Student ID.");
  showLogin();
}

// ---------- LOAD SECTIONS ----------
function loadSection(name){
  const content=document.getElementById("content");
  content.innerHTML="";
  const img=document.createElement("img");
  img.src="https://source.unsplash.com/800x400/?school";
  img.className="school";
  content.appendChild(img);

  let editable=(role==="teacher");
  let editClass=editable?"edit":"view-only";

  // ---------- MY INFO ----------
  if(name==="My Info"){
    const section = document.createElement("div");
    section.className="section";
    let html = "<h3>My Info</h3>";
    if(role==="teacher"){
      html += `<p>Name: ${currentUser.name}</p>`;
      html += `<p>Teacher I.D: ${currentUser.id}</p>`;
      html += `<p>Position: ${currentUser.position}</p>`;
      html += `<p>Section Handled: ${currentUser.sectionHandled}</p>`;
    } else if(role==="student"){
      html += `<p>Name: ${currentUser.name}</p>`;
      html += `<p>Student I.D: ${currentUser.id}</p>`;
      html += `<p>Section: ${currentUser.section}</p>`;
      html += `<p>Track: ${currentUser.track}</p>`;
      html += `<p>Strand: ${currentUser.strand}</p>`;
      html += `<p>Grade Level: ${currentUser.grade}</p>`;
    }
    section.innerHTML = html;
    content.appendChild(section);
    return;
  }

  // ---------- ATTENDANCE ----------
  if(name==="Attendance"){
    const section=document.createElement("div"); section.className="section";
    const dates=["2026-02-01","2026-02-02","2026-02-03"];
    let tableHTML="<h3>Attendance Table</h3><table><tr><th>Name</th>";    
    dates.forEach(d=>tableHTML+=`<th>${d}</th>`); tableHTML+="</tr>";    
    students.forEach(s=>{
      tableHTML+=`<tr><td>${s.name}</td>`;
      dates.forEach(()=>tableHTML+=`<td><input type="checkbox" ${editable?"":"disabled"}></td>`);
      tableHTML+="</tr>";
    });
    tableHTML+="</table>";    
    section.innerHTML=tableHTML;    
    content.appendChild(section);    
    return;
  }

  // ---------- GRADES ----------
  if(name==="Grades"){
    const section=document.createElement("div"); section.className="section";
    section.innerHTML=`<h3>Grades</h3>
      <label for="semesterSelect">Select Semester: </label>
      <select id="semesterSelect">
        <option value="1st">1st Semester</option>
        <option value="2nd">2nd Semester</option>
      </select>
      <div id="gradesContent" style="margin-top:15px;"></div>`;
    content.appendChild(section);

    const gradesContent=section.querySelector("#gradesContent");
    const semesterSelect=section.querySelector("#semesterSelect");

    function renderGrades(sem){
      let html=`<table><tr><th>Subject</th><th>Grade</th></tr>`;
      subjects.forEach(subj=>{
        html+=`<tr><td>${subj}</td><td><input type="text" value="${gradesData[sem][subj]}" class="${editable?"edit":"view-only"}" ${editable?"":"disabled"}></td></tr>`;
      });
      gradesContent.innerHTML = html;
    }
    renderGrades("1st");
    semesterSelect.addEventListener("change",()=>{renderGrades(semesterSelect.value);});
    return;
  }

  // ---------- OTHER SECTIONS ----------
  const section=document.createElement("div"); section.className="section";
  section.innerHTML=`<h3>${name}</h3><p>Section content placeholder...</p>`;
  content.appendChild(section);
}
</script>

</body>
</html>
