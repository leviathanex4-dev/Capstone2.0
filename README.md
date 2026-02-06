YOUR COMPANION TO A DSHS LIFE! 
<html lang="en">  
<head>  
<meta charset="UTF-8">  
<title>DSHS School System</title>  
<style>  
body {  
  margin: 0;  
  font-family: Algerian;  
  background-color: #fff;  
  background-image:  
    repeating-linear-gradient(to bottom, transparent 0px, transparent 26px, rgba(0,0,0,0.08) 27px),  
    url('https://source.unsplash.com/1600x900/?school,classroom'),  
    url('https://i.ibb.co/4m7KgXg/scribbles.png');  
  background-size: 100% 28px, cover, 100px 100px;  
  background-blend-mode: lighten;  
  color: #222;  
}  
.signup-link { color: #007bff; font-weight: bold; cursor: pointer; }  
.signup-link:hover { text-decoration: underline; }  
input, button, textarea, select { width: 100%; padding: 8px; margin-top: 6px; box-sizing: border-box; }  
button { cursor: pointer; }  
.edit { border: 1px solid #ccc; }  
.view-only { background: #f9f9f9; pointer-events: none; }  
.login { height: 100vh; display: flex; justify-content: center; align-items: center; }  
.box { background: rgba(255,255,255,0.95); padding: 25px; width: 320px; border-radius: 8px; box-shadow: 0 10px 20px rgba(0,0,0,0.3); text-align: center; }  
.pass-wrapper { position: relative; }  
.pass-wrapper span { position: absolute; right: 10px; top: 10px; cursor: pointer; }  
.dashboard { display: none; height: 100vh; }  
.header { background: rgba(0,51,102,0.95); color: white; padding: 15px; text-align: center; font-size: 18px; position: relative; z-index:1; }  
.container { display: flex; height: calc(100vh - 60px); position:relative; }  .menu {
width: 220px;
background: rgba(255,255,255,0.95);
padding: 10px;
box-shadow: 2px 0 10px rgba(0,0,0,0.2);
display: flex;
flex-direction: column;
position:absolute;
top:0;
left:0;
height:100%;
z-index:2;
transition: transform 0.3s;
transform: translateX(-100%);
}
.menu.show { transform: translateX(0); }
.menu button {
background: #eee;
color: black;
margin-top: 6px;
font-size: 14px;
white-space: nowrap;
overflow: hidden;
border:1px solid black;
border-radius:4px;
padding:6px;
}

.toggle-btn { background: #003366; color: white; font-size: 18px; border:none; position:absolute; top:10px; left:10px; z-index:3; padding:4px 8px; border-radius:4px; }
.logout { margin-top:auto; background:#d9534f; color:white; font-size:14px !important; }

.content { flex: 1; padding: 20px; display: flex; flex-direction: column; align-items: center; overflow-y:auto; }
.section { background: rgba(255,255,255,0.9); padding:15px; border-radius:5px; width:90%; margin-top:15px; }
.subsection { background: rgba(245,245,245,0.8); padding:10px; margin-top:10px; border-radius:5px; text-align:left; }
img.school { max-width: 80%; border-radius:10px; margin-bottom:20px; }

table { border-collapse: collapse; width: 100%; margin-top:10px; }
table, th, td { border: 1px solid #ccc; text-align:center; padding:5px; cursor: pointer; }
.schedule-box { display:flex; flex-wrap:wrap; gap:10px; margin-top:10px; }
.schedule-box div { flex:1 1 120px; background:#f0f0f0; border:1px solid #ccc; padding:10px; border-radius:5px; text-align:center; }

.chatbox { border:1px solid #ccc; padding:10px; height:200px; width:100%; overflow-y:auto; margin-top:5px; }
</style>

</head>  
<body>  <!-- LOGIN -->  <div class="login" id="login">  
  <div class="box">  
    <h2>Login</h2>  
    <input type="text" id="loginUsername" placeholder="Username">  
    <div class="pass-wrapper">  
      <input type="password" id="loginPassword" placeholder="Password">  
      <span onclick="togglePassword()">👁️</span>  
    </div>  
    <button onclick="login()">Login</button>  
    <p id="msg"></p>  
    <p style="font-size:13px; margin-top:10px;">Don’t have an account yet? <span class="signup-link" onclick="showSignup()">Sign up!</span></p>  
  </div>  
</div>  <!-- SIGN UP -->  <div class="login" id="signup" style="display:none;">  
  <div class="box">  
    <h2>Student Sign Up</h2>  
    <input type="text" id="signupName" placeholder="Full Name">  
    <input type="text" id="signupID" placeholder="Student I.D">  
    <input type="text" id="signupSection" placeholder="Section">  
    <input type="text" id="signupTrack" placeholder="Track">  
    <input type="text" id="signupStrand" placeholder="Strand">  
    <input type="text" id="signupGradeLevel" placeholder="Grade Level">  
    <input type="text" id="signupUsername" placeholder="Username">  
    <input type="password" id="signupPass" placeholder="Password">  
    <button onclick="submitSignup()">Create Account</button>  
    <p style="font-size:13px; margin-top:10px;">Already have an account? <span class="signup-link" onclick="showLogin()">Login</span></p>  
  </div>  
</div>  <!-- DASHBOARD -->  <div class="dashboard" id="dashboard">  
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
</div>  <script>  
// ---------- DATA ----------  
let role="", currentUser="";  
let students=[  
{name:"Jibdel",id:"ST001",section:"12-A",track:"Academic",strand:"STEM",gradeLevel:"12",username:"jibdel",password:"1234"},  
{name:"Viennes",id:"ST002",section:"12-B",track:"Academic",strand:"ABM",gradeLevel:"12",username:"viennes",password:"5678"},  
{name:"Jurl",id:"ST003",section:"12-C",track:"Academic",strand:"STEM",gradeLevel:"12",username:"jurl",password:"abcd"},  
{name:"Sam",id:"ST004",section:"12-D",track:"Academic",strand:"HUMSS",gradeLevel:"12",username:"sam",password:"efgh"},  
{name:"Justine",id:"ST005",section:"12-A",track:"Academic",strand:"STEM",gradeLevel:"12",username:"justine",password:"ijkl"},  
{name:"Ashley",id:"ST006",section:"12-B",track:"Academic",strand:"ABM",gradeLevel:"12",username:"ashley",password:"mnop"},  
{name:"Gerlie",id:"ST007",section:"12-C",track:"Academic",strand:"STEM",gradeLevel:"12",username:"gerlie",password:"qrst"},  
{name:"Meriem",id:"ST008",section:"12-D",track:"Academic",strand:"HUMSS",gradeLevel:"12",username:"meriem",password:"uvwx"}];  
  
let teachers=[{name:"Mr. Smith",id:"TE001",position:"Teacher III",sectionHandled:"12-A",username:"teacher1",password:"teach123"}];  
let parents=[{name:"Parent of Jibdel",child:"Jibdel",username:"parentSt001",password:"par123"}];  
  
let subjects=["3I's","Genchem 2","P6 2","🧢 🗿","Perdev","CPAR","Entrepreneurship"];  
let scheduleTimes={"3I's":"8:00-9:00","Genchem 2":"9:00-10:00","P6 2":"10:00-11:00","🧢 🗿":"11:00-11:45","Perdev":"11:45-12:30","CPAR":"12:30-1:00","Entrepreneurship":"1:00-2:00"};  
  
let gradesData={};  
students.forEach(s=>{  
  gradesData[s.name]={};  
  subjects.forEach(subj=>{  
    gradesData[s.name][subj]=Math.floor(Math.random()*21)+80; // 80-100  
  });  
});  
  
// ---------- ATTENDANCE ----------  
let attendanceData = {};  
students.forEach(s=>{  
  attendanceData[s.name] = {};  
  for(let d=1; d<=5; d++){  
    attendanceData[s.name]["Day "+d] = "P"; // default Present  
  }  
});  
  
// ---------- PASSWORD TOGGLE ----------  
function togglePassword(){  
  const p=document.getElementById("loginPassword");  
  p.type=(p.type==="password")?"text":"password";  
}  
  
// ---------- LOGIN ----------  
function login(){  
  const username=document.getElementById("loginUsername").value;  
  const pass=document.getElementById("loginPassword").value;  
  let found=false;  
  
  teachers.forEach(t=>{if(username===t.username && pass===t.password){role="teacher"; currentUser=t.name; found=true;}});  
  students.forEach(s=>{if(username===s.username && pass===s.password){role="student"; currentUser=s.name; found=true;}});  
  parents.forEach(p=>{if(username===p.username && pass===p.password){role="parent"; currentUser=p.child; found=true;}});  
  
  if(!found){document.getElementById("msg").innerText="Invalid login"; return;}  
  document.getElementById("login").style.display="none";  
  document.getElementById("signup").style.display="none";  
  document.getElementById("dashboard").style.display="block";  
  loadDashboard();  
}  
  
// ---------- DASHBOARD ----------  
function loadDashboard(){  
  document.getElementById("roleTitle").innerText = role.toUpperCase()+" DASHBOARD";  
  const menu=document.getElementById("menu"); menu.innerHTML="";  
  const toggle=document.createElement("button"); toggle.innerText="☰"; toggle.className="toggle-btn"; toggle.onclick=()=>menu.classList.toggle("show"); menu.appendChild(toggle);  
  let items=[];  
  if(role==="teacher"){items=["Attendance","Grades","Schedule Planner","Planner","My Info","Parent Chat," Attendance"];}  
  else if(role==="student"){items=["Attendance","Grades","Schedule","Planner","My Info","E-Motion"];}  
  else if(role==="parent"){items=["Child Attendance","Child Grades","Child Schedule","Teacher Chat"];}  
  createMenu(items);  
  const logoutBtn=document.createElement("button"); logoutBtn.innerText="⬅ Logout"; logoutBtn.className="logout"; logoutBtn.onclick=logout; menu.appendChild(logoutBtn);  
}  
  
function createMenu(items){  
  const menu=document.getElementById("menu");  
  items.forEach(item=>{  
    const btn=document.createElement("button");  
    btn.innerText=item;  
    btn.onclick=()=>loadSection(item);  
    menu.appendChild(btn);  
  });  
}  
  
// ---------- LOGOUT ----------  
function logout(){   
  role=""; currentUser="";   
  document.getElementById("dashboard").style.display="none";   
  document.getElementById("login").style.display="flex";   
}  
  
// ---------- SIGNUP ----------  
function showSignup(){ document.getElementById("login").style.display="none"; document.getElementById("signup").style.display="flex"; }  
function showLogin(){ document.getElementById("signup").style.display="none"; document.getElementById("login").style.display="flex"; }  
function submitSignup(){  
  let name=document.getElementById("signupName").value;  
  let id=document.getElementById("signupID").value;  
  let section=document.getElementById("signupSection").value;  
  let track=document.getElementById("signupTrack").value;  
  let strand=document.getElementById("signupStrand").value;  
  let gradeLevel=document.getElementById("signupGradeLevel").value;  
  let username=document.getElementById("signupUsername").value;  
  let password=document.getElementById("signupPass").value;  
  students.push({name,id,section,track,strand,gradeLevel,username,password});  
  gradesData[name]={}; subjects.forEach(sub=>gradesData[name][sub]=0);  
  attendanceData[name]={}; for(let d=1; d<=5; d++){attendanceData[name]["Day "+d]="P";}  
  alert("Signup successful! You can now log in."); showLogin();  
}  
  
// ---------- LOAD SECTION ----------  
function loadSection(tab){  
  const content = document.getElementById("content");  
  content.innerHTML = "";  
  const section = document.createElement("div");  
  section.className = "section";  
    
  const today = new Date().getDay(); // Sunday=0 ... Saturday=6  
  const dayIndex = today>=1 && today<=5 ? today : 1; // highlight only Mon-Fri  
  
  // ---------- TEACHER ----------  
  if(role==="teacher"){  
    if(tab==="Attendance"){  
      section.innerHTML="<h3>Attendance</h3>";  
      let table="<table><tr><th>Student</th>";  
      for(let d=1; d<=5; d++){  
        table+="<th>Day "+d+"</th>";  
      }  
      table+="</tr>";  
      students.forEach(s=>{  
        table+="<tr><td>"+s.name+"</td>";  
        for(let d=1; d<=5; d++){  
          table+=`<td contenteditable="true" onclick="toggleStatus('${s.name}','Day ${d}',this)">${attendanceData[s.name]["Day "+d]}</td>`;  
        }  
        table+="</tr>";  
      });  
      table+="</table>";  
      section.innerHTML+=table;  
    }  
  
    // GRADES  
    if(tab==="Grades"){  
      section.innerHTML="<h3>Grades</h3><p>Select a student:</p>";  
      students.forEach(s=>{  
        let btn=document.createElement("button");  
        btn.innerText=s.name;  
        btn.onclick=()=>{  
          section.innerHTML="<h3>"+s.name+"'s Grades</h3>";  
          subjects.forEach(sub=>{  
            section.innerHTML+=`<div class="subsection">${sub} - <span contenteditable="true">${gradesData[s.name][sub]}</span></div>`;  
          });  
        };  
        section.appendChild(btn);  
      });  
    }  
  
    // SCHEDULE PLANNER  
    if(tab==="Schedule Planner"){  
      section.innerHTML="<h3>Schedule Planner</h3>";  
      let box="<div class='schedule-box'>";  
      subjects.forEach(sub=>{  
        box+=`<div><strong>${sub}</strong><br>${scheduleTimes[sub]}</div>`;  
      });  
      box+="<div><strong>Recess</strong><br>9:45–10:00</div>";  
      box+="<div><strong>Lunch</strong><br>12:00–1:00</div>";  
      box+="</div>";  
      section.innerHTML+=box;  
    }  
  
    // PLANNER  
    if(tab==="Planner"){  
      section.innerHTML="<h3>Teacher Planner</h3>";  
      section.innerHTML+=`<textarea rows="6" placeholder="Plans..."></textarea>`;  }  

// MY INFO  
if(tab==="My Info"){  
  const t=teachers[0];  
  section.innerHTML=`<h3>My Info</h3>  
    <p>Name: ${t.name}</p>  
    <p>ID: ${t.id}</p>  
    <p>Position: ${t.position}</p>  
    <p>Section Handled: ${t.sectionHandled}</p>`;  
}  

// PARENT CHAT  
if(tab==="Parent Chat"){  
  section.innerHTML=`<h3>Parent Conversations</h3>  
    <div class="subsection">Parent of Jibdel</div>  
    <div class="chatbox">Hello Teacher 👋</div>  
    <input placeholder="Reply...">`;  
}

}

// ---------- STUDENT ----------
if(role==="student"){
const s = students.find(st=>st.name===currentUser);

if(tab==="Attendance"){  
  section.innerHTML="<h3>My Attendance</h3>";  
  let t="<table><tr><th>Day</th><th>Status</th></tr>";  
  for(let d=1; d<=5; d++){  
    let highlight = (d===dayIndex) ? " style='background:#fffa90;'" : "";  
    t+=`<tr${highlight}><td>Day ${d}</td><td>${attendanceData[s.name]["Day "+d]}</td></tr>`;  
  }  
  t+="</table>";  
  section.innerHTML+=t;  
}  

if(tab==="Grades"){  
  section.innerHTML="<h3>My Grades</h3>";  
  subjects.forEach(sub=>{  
    section.innerHTML+=`<div class="subsection">${sub} - ${gradesData[s.name][sub]}</div>`;  
  });  
}  

if(tab==="Schedule"){  
  section.innerHTML="<h3>My Schedule</h3>";  
  let box="<div class='schedule-box'>";  
  subjects.forEach(sub=>{  
    box+=`<div><strong>${sub}</strong><br>${scheduleTimes[sub]}</div>`;  
  });  
  box+="<div><strong>Recess</strong><br>9:45–10:00</div>";  
  box+="<div><strong>Lunch</strong><br>12:00–1:00</div>";  
  box+="</div>";  
  section.innerHTML+=box;  
}  

if(tab==="Planner"){  
  section.innerHTML="<h3>Student Planner</h3>";  
  section.innerHTML+=`<h4>Daily</h4><textarea rows="3"></textarea>  
    <h4>Weekly</h4><textarea rows="3"></textarea>  
    <h4>Goals</h4><textarea rows="3"></textarea>`;  
}  

if(tab==="E-Motion"){  
  section.innerHTML="<h3>E-Motion</h3>";  
  section.innerHTML+=`<div class="chatbox">How are you feeling today?</div>  
    <input placeholder="Type your thoughts...">`;  
}  

if(tab==="My Info"){  
  section.innerHTML=`<h3>My Info</h3>  
    <p>Name: ${s.name}</p>  
    <p>ID: ${s.id}</p>  
    <p>Grade Level: ${s.gradeLevel}</p>  
    <p>Section: ${s.section}</p>  
    <p>Strand: ${s.strand}</p>`;  
}

}

// ---------- PARENT ----------
if(role==="parent"){
const child=currentUser;

if(tab==="Child Attendance"){  
  section.innerHTML="<h3>Attendance</h3>";  
  let t="<table><tr><th>Day</th><th>Status</th></tr>";  
  for(let d=1; d<=5; d++){  
    let highlight = (d===dayIndex) ? " style='background:#fffa90;'" : "";  
    t+=`<tr${highlight}><td>Day ${d}</td><td>${attendanceData[child]["Day "+d]}</td></tr>`;  
  }  
  t+="</table>";  
  section.innerHTML+=t;  
}  

if(tab==="Child Grades"){  
  section.innerHTML="<h3>Grades</h3>";  
  subjects.forEach(sub=>{  
    section.innerHTML+=`<div class="subsection">${sub} - ${gradesData[child][sub]}</div>`;  
  });  
}  

if(tab==="Child Schedule"){  
  section.innerHTML="<h3>Schedule</h3>";  
  let box="<div class='schedule-box'>";  
  subjects.forEach(sub=>{  
    box+=`<div><strong>${sub}</strong><br>${scheduleTimes[sub]}</div>`;  
  });  
  box+="</div>";  
  section.innerHTML+=box;  
}  

if(tab==="Teacher Chat"){  
  section.innerHTML="<h3>Chat Teacher</h3>";  
  section.innerHTML+=`<div class="chatbox">Good afternoon teacher.</div>  
    <input placeholder="Message...">`;  
}

}

content.appendChild(section);
}

// ---------- TOGGLE ATTENDANCE STATUS ----------
function toggleStatus(student, day, td){
td.innerText = td.innerText==="P" ? "A" : "P";
attendanceData[student][day] = td.innerText;
}
</script>

</body>  
</html>  
