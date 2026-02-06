Your Companion To A DSHS Life! 
<html lang="en">
<head>
<meta charset="UTF-8">
<title>School System</title>
<style>
/* ---------- NOTES PAPER BACKGROUND ---------- */
body {
  margin: 0;
  font-family: "Allassy Caps", serif;
  background-color: #fff;
  background-image:
    repeating-linear-gradient(to bottom, transparent 0px, transparent 26px, rgba(0,0,0,0.1) 27px),
    radial-gradient(circle, rgba(200,200,200,0.05) 1px, transparent 1px);
  background-size: 100% 28px, 30px 30px;
  color: #222;
}

/* ---------- LINKS ---------- */
.signup-link {
  color: #007bff;
  font-weight: bold;
  cursor: pointer;
}
.signup-link:hover {
  text-decoration: underline;
}

/* ---------- LOGIN & SIGNUP BOX ---------- */
.login, #signup {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.box {
  background: rgba(255,255,255,0.95);
  padding: 25px;
  width: 320px;
  border-radius: 8px;
  box-shadow: 0 10px 20px rgba(0,0,0,0.3);
  text-align: center;
  border: 1px solid #000; /* add black border like notebook box */
}

input, button, textarea, select {
  width: 100%;
  padding: 10px;
  margin-top: 10px;
  border-radius: 4px;
}

button {
  background: #007bff;
  color: white;
  border: none;
  cursor: pointer;
}

button:hover {
  opacity: 0.9;
}

/* ---------- DASHBOARD ---------- */
.dashboard {
  display: none;
  height: 100vh;
  display: flex;
  flex-direction: column;
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
  overflow: hidden;
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
  border-right: 1px solid #000;
}

.menu button {
  background: #fff;
  color: black;
  margin-top: 6px;
  font-size: 14px;
  padding: 10px;
  text-align: left;
  border: 1px solid #000;
  border-radius: 4px;
  cursor: pointer;
}

.menu button:hover {
  background: #e0e0e0;
}

.menu.collapsed {
  width: 60px;
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
  border: 1px solid #000; /* add notebook style border */
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
  border: 1px solid #000;
  text-align: center;
  padding: 5px;
}

.edit {
  border: 1px solid #000;
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
  border: 1px solid #000;
}

/* ---------- MOBILE RESPONSIVE ---------- */
@media screen and (max-width: 768px){
  .container {flex-direction: column;}
  .menu {width: 100%; display: flex; flex-direction: row; overflow-x: auto;}
  .menu button {flex: 1; margin: 4px;}
}
</style>
</head>
<body>

<!-- LOGIN -->
<div class="login" id="login">
  <div class="box">
    <h2>Login</h2>
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
    <input type="text" placeholder="Full Name" id="signupName">
    <input type="text" placeholder="Student I.D" id="signupID">
    <input type="text" placeholder="Section" id="signupSection">
    <input type="text" placeholder="Track" id="signupTrack">
    <input type="text" placeholder="Strand" id="signupStrand">
    <input type="text" placeholder="Grade Level" id="signupGrade">
    <button onclick="submitSignup()">Create Account</button>
    <p style="font-size:13px; margin-top:10px;">
      Already have an account? <span class="signup-link" onclick="showLogin()">Login</span>
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
let role = "";
let studentsData = [];
let teachersData = [
  {name:"Mr. Smith", id:"T001", position:"Teacher III", section:"Math 10"}
];
let currentStudent = null;
let currentTeacher = teachersData[0];

// ---------- LOGIN ----------
function login() {
  const pass = document.getElementById("password").value;
  if(pass==="teacher"){ role="teacher"; currentStudent=null;}
  else if(pass==="student"){ role="student"; currentStudent=studentsData[0]||null;}
  else{ document.getElementById("msg").innerText="Invalid password"; return; }

  document.getElementById("login").style.display="none";
  document.getElementById("signup").style.display="none";
  document.getElementById("dashboard").style.display="flex";
  loadDashboard();
}

// ---------- DASHBOARD ----------
function loadDashboard(){
  document.getElementById("roleTitle").innerText = role.toUpperCase()+" DASHBOARD";
  const menu = document.getElementById("menu");
  menu.innerHTML="";
  const toggle=document.createElement("button");
  toggle.innerText="☰"; toggle.className="toggle-btn"; toggle.onclick=toggleMenu;
  menu.appendChild(toggle);

  let items=[];
  if(role==="teacher"){ items=["My Info","Attendance","Grades","Student Files","Parents","Subjects","Schedule","Bulletin Board"]; }
  else if(role==="student"){ items=["My Info","Attendance","Grades","Schedule","AI Chat","Bulletin Board","Planner"]; }

  createMenu(items);

  const logoutBtn=document.createElement("button");
  logoutBtn.innerText="⬅ Back"; logoutBtn.className="logout"; logoutBtn.onclick=logout;
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

// ---------- SHOW / HIDE ----------
function showSignup(){ document.getElementById("login").style.display="none"; document.getElementById("signup").style.display="flex";}
function showLogin(){ document.getElementById("signup").style.display="none"; document.getElementById("login").style.display="flex";}

// ---------- SIGNUP ----------
function submitSignup(){
  const student={ 
    name: document.getElementById("signupName").value,
    id: document.getElementById("signupID").value,
    section: document.getElementById("signupSection").value,
    track: document.getElementById("signupTrack").value,
    strand: document.getElementById("signupStrand").value,
    grade: document.getElementById("signupGrade").value
  };
  studentsData.push(student);
  alert("Signup successful!");
  showLogin();
}

// ---------- LOGOUT ----------
function logout(){ role=""; document.getElementById("dashboard").style.display="none"; document.getElementById("login").style.display="flex"; }

// ---------- TOGGLE MENU ----------
function toggleMenu(){ document.getElementById("menu").classList.toggle("collapsed"); }

// ---------- LOAD SECTION ----------
function loadSection(name){
  const content=document.getElementById("content");
  content.innerHTML="";

  const img=document.createElement("img");
  img.src="https://source.unsplash.com/800x400/?school";
  img.className="school";
  content.appendChild(img);

  if(name==="My Info"){
    const section=document.createElement("div"); section.className="section";
    let html="";
    if(role==="teacher"){
      html=`<h3>Teacher Info</h3>
      <p><strong>Name:</strong> ${currentTeacher.name}</p>
      <p><strong>ID:</strong> ${currentTeacher.id}</p>
      <p><strong>Position:</strong> ${currentTeacher.position}</p>
      <p><strong>Section Handled:</strong> ${currentTeacher.section}</p>`;
    } else if(role==="student" && currentStudent){
      html=`<h3>Student Info</h3>
      <p><strong>Name:</strong> ${currentStudent.name}</p>
      <p><strong>ID:</strong> ${currentStudent.id}</p>
      <p><strong>Section:</strong> ${currentStudent.section}</p>
      <p><strong>Track:</strong> ${currentStudent.track}</p>
      <p><strong>Strand:</strong> ${currentStudent.strand}</p>
      <p><strong>Grade:</strong> ${currentStudent.grade}</p>`;
    }
    section.innerHTML=html;
    content.appendChild(section);
    return;
  }

  /* ---------- OLD SECTIONS (Attendance, Grades, etc.) ---------- */
  const section=document.createElement("div"); section.className="section";
  section.innerHTML=`<h3>${name}</h3><p>Old content placeholder (attendance, grades, etc.)</p>`;
  content.appendChild(section);
}
</script>

</body>
</html>
