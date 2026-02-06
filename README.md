<!DOCTYPE html>
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
    background-color: #ffffff;

    /* dotted horizontal note lines */
    background-image:
      repeating-linear-gradient(
        to bottom,
        transparent 0px,
        transparent 26px,
        rgba(0,0,0,0.15) 27px
      );

    background-size: 100% 28px;
    color: #222;
  }

  .signup-link {
    color: #007bff;
    font-weight: bold;
    cursor: pointer;
  }

  .signup-link:hover {
    text-decoration: underline;
  }

  /* ---------- LOGIN & SIGNUP ---------- */
  .login {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }

  .box {
    background: rgba(255,255,255,0.95);
    padding: 25px;
    width: 300px;
    border-radius: 8px;
    box-shadow: 0 10px 20px rgba(0,0,0,0.3);
    text-align: center;
  }

  input, button, textarea, select {
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
    overflow-y: auto;
  }

  .menu.collapsed {
    width: 60px;
  }

  /* ---------- MENU BUTTONS ---------- */
  .menu button {
    background: #fff;
    color: black;
    margin: 6px 0;
    font-size: 14px;
    padding: 10px;
    border: 2px solid black;
    border-radius: 5px;
    text-align: left;
    transition: transform 0.2s, box-shadow 0.2s, background 0.2s;
  }

  .menu button:hover {
    background: #f0f0f0;
    transform: translateY(-3px);
    box-shadow: 0 5px 10px rgba(0,0,0,0.2);
  }

  .menu.collapsed button:hover {
    transform: none;
    box-shadow: none;
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

  /* ---------- MOBILE RESPONSIVE ---------- */
  @media (max-width: 768px){
    .container {
      flex-direction: column;
      height: auto;
    }

    .menu {
      width: 100%;
      display: flex;
      flex-direction: row;
      overflow-x: auto;
      box-shadow: none;
    }

    .menu button {
      flex: 0 0 auto;
      margin: 5px;
      white-space: nowrap;
    }

    .menu.collapsed {
      width: 100%;
    }

    .content {
      width: 100%;
      padding: 10px;
    }

    img.school {
      max-width: 100%;
    }
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
    <input type="text" placeholder="Full Name">
    <input type="text" placeholder="Student I.D">
    <input type="text" placeholder="Section">
    <input type="text" placeholder="Track">
    <input type="text" placeholder="Strand">
    <input type="text" placeholder="Grade Level">
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
let role = "";
let currentStudent = "Jibdel"; // For student login
let currentParentChild = "Jibdel"; // For parent login

/* ---------- LOGIN ---------- */
function login() {
  const pass = document.getElementById("password").value;
  if (pass === "teacher") role = "teacher";
  else if (pass === "student") role = "student";
  else if (pass === "parent") role = "parent";
  else { document.getElementById("msg").innerText="Invalid password"; return; }

  document.getElementById("login").style.display="none";
  document.getElementById("dashboard").style.display="block";
  loadDashboard();
}

/* ---------- DASHBOARD ---------- */
function loadDashboard() {
  document.getElementById("roleTitle").innerText = role.toUpperCase()+" DASHBOARD";

  const menu = document.getElementById("menu");
  menu.innerHTML="";

  const toggle = document.createElement("button");
  toggle.innerText="☰"; toggle.className="toggle-btn"; toggle.onclick=toggleMenu;
  menu.appendChild(toggle);

  let items=[];
  if(role==="teacher"){
    items=["Attendance","Grades","Student Files","Parents","Subjects","Schedule","Bulletin Board"];
  } else if(role==="student"){
    items=["Attendance","Grades","Schedule","AI Chat","Bulletin Board","Planner"];
  } else if(role==="parent"){
    items=["Child Attendance","Child Grades","Child Schedule","Teacher Chat","Bulletin Board"];
  }

  createMenu(items);

  const logoutBtn=document.createElement("button");
  logoutBtn.innerText="⬅ Back"; logoutBtn.className="logout"; logoutBtn.onclick=logout;
  menu.appendChild(logoutBtn);

}
/* ---------- MENU ---------- */
function createMenu(items){
  const menu=document.getElementById("menu");
  items.forEach(item=>{
    const btn=document.createElement("button");
    btn.innerText=item;
    btn.onclick=()=>loadSection(item);
    menu.appendChild(btn);
  });
}

/* ---------- SHOW/HIDE SIGNUP ---------- */
function showSignup() {
  document.getElementById("login").style.display = "none";
  document.getElementById("signup").style.display = "flex";
}

function showLogin() {
  document.getElementById("signup").style.display = "none";
  document.getElementById("login").style.display = "flex";
}

function submitSignup() {
  alert("Signup successful! You can now log in.");
  showLogin();
}

/* ---------- LOGOUT ---------- */
function logout(){ 
  role=""; 
  document.getElementById("dashboard").style.display="none"; 
  document.getElementById("login").style.display="flex"; 
}

/* ---------- TOGGLE MENU ---------- */
function toggleMenu(){ document.getElementById("menu").classList.toggle("collapsed"); }

/* ---------- The rest of your old dashboard functions (attendance, grades, planner etc.) can remain as-is ---------- */
</script>
</body>
</html>
