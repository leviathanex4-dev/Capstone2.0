Your Comanion To A DSHS Life! 
<html lang="en">
<head>
<meta charset="UTF-8">
<title>School System</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
/* ---------- NOTES PAPER BACKGROUND ---------- */
body {
  margin: 0;
  font-family: "Allassy Caps", serif;
  background-color: #fff;
  background-image:
    repeating-linear-gradient(to bottom, transparent 0px, transparent 26px, rgba(0,0,0,0.1) 27px),
    radial-gradient(circle at 20% 30%, rgba(0,0,0,0.03) 2px, transparent 2px),
    radial-gradient(circle at 80% 70%, rgba(0,0,0,0.03) 2px, transparent 2px);
  background-size: 100% 28px, 50px 50px, 50px 50px;
  color: #222;
}

/* ---------- GENERAL ---------- */
input, button, select, textarea {
  width: 100%;
  padding: 8px;
  margin-top: 8px;
  box-sizing: border-box;
  font-family: inherit;
  font-size: 14px;
}

button {
  background: #007bff;
  color: #fff;
  border: none;
  cursor: pointer;
}

button:hover { opacity: 0.9; }

.signup-link {
  color: #007bff;
  font-weight: bold;
  cursor: pointer;
}

.signup-link:hover {
  text-decoration: underline;
}

/* ---------- LOGIN / SIGNUP ---------- */
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
  box-shadow: 0 5px 15px rgba(0,0,0,0.3);
  text-align: center;
}

/* ---------- DASHBOARD ---------- */
.dashboard { display: none; height: 100vh; }
.header { background: rgba(0,51,102,0.95); color: #fff; padding: 15px; text-align: center; font-size: 18px; }
.container { display: flex; height: calc(100vh - 60px); flex-wrap: wrap; }

/* ---------- MENU ---------- */
.menu {
  width: 180px;
  background: rgba(255,255,255,0.95);
  padding: 10px;
  box-shadow: 2px 0 10px rgba(0,0,0,0.2);
  display: flex;
  flex-direction: column;
  transition: width 0.3s;
}

.menu button {
  background: #eee;
  color: black;
  margin-top: 6px;
  font-size: 14px;
  white-space: nowrap;
  border: 1px solid black;
  padding: 8px;
}

.menu .toggle-btn { background: #003366; color: #fff; font-size: 18px; }
.menu .logout { margin-top: auto; background: #d9534f !important; color: #fff !important; }

/* ---------- CONTENT ---------- */
.content {
  flex: 1;
  padding: 15px;
  display: flex;
  flex-direction: column;
  align-items: center;
  overflow-y: auto;
}

.section {
  background: rgba(255,255,255,0.9);
  padding: 10px;
  border-radius: 5px;
  width: 95%;
  margin-top: 15px;
}

img.school {
  max-width: 80%;
  border-radius: 10px;
  margin-bottom: 15px;
}

table { border-collapse: collapse; width: 100%; margin-bottom: 15px; }
table, th, td { border: 1px solid #000; text-align: center; padding: 5px; }

.edit { border: 1px solid #ccc; }
.view-only { background: #f9f9f9; pointer-events: none; }
.subsection { background: rgba(245,245,245,0.8); padding: 10px; margin-top: 10px; border-radius: 5px; text-align: left; }

/* ---------- MOBILE ---------- */
@media screen and (max-width: 600px) {
  .container { flex-direction: column; }
  .menu { width: 100%; display: flex; flex-wrap: wrap; }
  .menu button { flex: 1 1 45%; margin: 5px; }
}
</style>
</head>
<body>

<!-- LOGIN -->
<div class="login" id="login">
  <div class="box">
    <h2>Login</h2>
    <input type="text" id="username" placeholder="Username or ID">
    <input type="password" id="password" placeholder="Password">
    <button onclick="login()">Login</button>
    <p style="font-size:13px; margin-top:15px;">
      Don’t have an account yet?
      <span class="signup-link" onclick="showSignup()">Sign up!</span>
    </p>
    <p id="msg" style="color:red;"></p>
  </div>
</div>

<!-- SIGN UP -->
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
/* ---------- USERS ---------- */
let users = [
  { role:"teacher", username:"teacher", password:"teacher123", name:"Mr. Santos", position:"Teacher III", sectionHandled:"Math" },
  { role:"student", username:"ST001", password:"student123", name:"Jibdel", studentID:"ST001", section:"7A", track:"Academic", strand:"STEM", gradeLevel:7 },
  { role:"student", username:"ST002", password:"student123", name:"Viennes", studentID:"ST002", section:"7B", track:"Academic", strand:"ABM", gradeLevel:7 }
];

/* ---------- LOGIN ---------- */
let role = "", currentStudent = "";

function login(){
  const username = document.getElementById("username").value.trim();
  const password = document.getElementById("password").value.trim();
  const user = users.find(u=>u.username===username && u.password===password);
  if(!user){ document.getElementById("msg").innerText="Invalid login"; return; }
  role = user.role;
  currentStudent = role==="student" ? user.name : "";
  document.getElementById("login").style.display="none";
  document.getElementById("dashboard").style.display="block";
  loadDashboard();
}

function showSignup(){
  document.getElementById("login").style.display="none";
  document.getElementById("signup").style.display="flex";
}
function showLogin(){
  document.getElementById("signup").style.display="none";
  document.getElementById("login").style.display="flex";
}
function submitSignup(){
  const newUser = {
    role:"student",
    username:document.getElementById("su_id").value.trim(),
    password:"student123",
    name:document.getElementById("su_name").value.trim(),
    studentID:document.getElementById("su_id").value.trim(),
    section:document.getElementById("su_section").value.trim(),
    track:document.getElementById("su_track").value.trim(),
    strand:document.getElementById("su_strand").value.trim(),
    gradeLevel:document.getElementById("su_grade").value.trim()
  };
  users.push(newUser);
  alert("Signup successful! Use your ID and password to login.");
  showLogin();
}

/* ---------- DASHBOARD ---------- */
function loadDashboard(){
  document.getElementById("roleTitle").innerText = role.toUpperCase()+" DASHBOARD";
  const menu = document.getElementById("menu");
  menu.innerHTML="";

  const toggle = document.createElement("button");
  toggle.innerText="☰"; toggle.className="toggle-btn"; toggle.onclick=toggleMenu;
  menu.appendChild(toggle);

  let items=[];
  if(role==="teacher"){
    items=["Attendance","Grades","Student Files","Parents","My Info","Subjects","Schedule","Bulletin Board"];
  } else if(role==="student"){
    items=["Attendance","Grades","Schedule","AI Chat","Bulletin Board","Planner","My Info"];
  }

  items.forEach(item=>{
    const btn=document.createElement("button");
    btn.innerText=item;
    btn.onclick=()=>loadSection(item);
    menu.appendChild(btn);
  });

  const logoutBtn=document.createElement("button");
  logoutBtn.innerText="⬅ Logout"; logoutBtn.className="logout"; logoutBtn.onclick=logout;
  menu.appendChild(logoutBtn);
}

function toggleMenu(){ document.getElementById("menu").classList.toggle("collapsed"); }
function logout(){ role=""; currentStudent=""; document.getElementById("dashboard").style.display="none"; document.getElementById("login").style.display="flex"; }

/* ---------- SAMPLE DATA ---------- */
const students=["Jibdel","Viennes"];
const subjects=["Filipino","Math","Science","English","AP","MSEP"];

const gradesData = {
  "Jibdel":{"Filipino":85,"Math":90,"Science":88,"English":91,"AP":87,"MSEP":89},
  "Viennes":{"Filipino":80,"Math":82,"Science":85,"English":83,"AP":88,"MSEP":90}
};

/* ---------- CONTENT ---------- */
function loadSection(name){
  const content=document.getElementById("content");
  content.innerHTML="";
  const img=document.createElement("img");
  img.src="https://source.unsplash.com/800x400/?school";
  img.className="school";
  content.appendChild(img);

  if(name==="My Info"){
    const section=document.createElement("div"); section.className="section";
    if(role==="teacher"){
      const t = users.find(u=>u.role==="teacher");
      section.innerHTML=`<h3>My Info</h3>
        Name: ${t.name}<br>
        Teacher I.D: teacher<br>
        Position: ${t.position}<br>
        Section handled: ${t.sectionHandled}`;
    } else {
      const s = users.find(u=>u.name===currentStudent);
      section.innerHTML=`<h3>My Info</h3>
        Name: ${s.name}<br>
        Student I.D: ${s.studentID}<br>
        Section: ${s.section}<br>
        Track: ${s.track}<br>
        Strand: ${s.strand}<br>
        Grade Level: ${s.gradeLevel}`;
    }
    content.appendChild(section);
    return;
  }

  if(name==="Attendance"){
    const section=document.createElement("div"); section.className="section";
    let html=`<h3>Attendance Table</h3><table><tr><th>Name</th>`;
    ["Feb 1","Feb 2","Feb 3","Feb 4","Feb 5"].forEach(d=>html+=`<th>${d}</th>`); html+="</tr>";
    students.forEach(s=>{
      if(role==="student" && s!==currentStudent) return;
      html+=`<tr><td>${s}</td>`; ["","","","",""].forEach(()=>html+=`<td><input type="checkbox"></td>`); html+="</tr>";
    });
    html+="</table>"; section.innerHTML=html;
    content.appendChild(section); return;
  }

  if(name==="Grades"){
    const section=document.createElement("div"); section.className="section";
    let html=`<h3>Grades</h3><table><tr><th>Subject</th>`;
    ["Filipino","Math","Science","English","AP","MSEP"].forEach(s=>html+=`<th>${s}</th>`); html+="</tr>";
    students.forEach(s=>{
      if(role==="student" && s!==currentStudent) return;
      html+=`<tr><td>${s}</td>`;
      subjects.forEach(sub=>html+=`<td><input type="text" value="${gradesData[s][sub]}"></td>`);
      html+="</tr>";
    });
    html+="</table>"; section.innerHTML=html;
    content.appendChild(section); return;
  }

  const section=document.createElement("div"); section.className="section";
  section.innerHTML=`<h3>${name}</h3><p>Sample content for ${name} section.</p>`;
  content.appendChild(section);
}
</script>
</body>
</html>
