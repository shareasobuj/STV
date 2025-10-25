# STV 
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>STV</title>
<style>
body{font-family:'Poppins',sans-serif;background:#eef2f7;margin:0;}
header{background:#0074cc;color:white;text-align:center;padding:15px;}
nav{background:#1e90ff;display:flex;justify-content:center;flex-wrap:wrap;}
nav button{margin:5px;padding:10px 20px;border:none;border-radius:5px;background:white;color:#0074cc;font-weight:bold;cursor:pointer;transition:0.3s;}
nav button:hover{background:#0074cc;color:white;}
.container{padding:20px;}
.video-grid{display:flex;flex-wrap:wrap;justify-content:center;}
.video-card{background:white;margin:10px;padding:10px;width:300px;border-radius:10px;box-shadow:0 0 8px rgba(0,0,0,0.1);text-align:center;}
.video-card video{width:100%;border-radius:8px;}
.video-card h4{margin-top:5px;font-size:16px;}
.admin-panel{background:white;max-width:500px;margin:auto;padding:20px;border-radius:10px;box-shadow:0 0 10px rgba(0,0,0,0.1);}
input,button{width:100%;padding:10px;margin:8px 0;border-radius:5px;border:1px solid #ccc;}
button{background:#0074cc;color:white;border:none;}
button:hover{background:#005fa3;}
.hidden{display:none;}
</style>
</head>
<body>

<header>
  <h1>🎓 STV </h1>
</header>

<nav>
  <button onclick="showHome()">Home</button>
  <button onclick="showLogin()">Login</button>
  <button onclick="showSignup()">Sign Up</button>
  <button onclick="showAdmin()" id="adminBtn" style="display:none;">Admin Panel</button>
  <button onclick="logout()" id="logoutBtn" style="display:none;">Logout</button>
</nav>

<div class="container">

  <!-- Home -->
  <div id="homePage">
    <h2>📺 Educational Videos</h2>
    <div id="videoList" class="video-grid"></div>
  </div>

  <!-- Login -->
  <div id="loginPage" class="hidden">
    <div class="admin-panel">
      <h3>🔐 Login</h3>
      <input type="text" id="loginEmail" placeholder="Email">
      <input type="password" id="loginPassword" placeholder="Password">
      <button onclick="login()">Login</button>
    </div>
  </div>

  <!-- Signup -->
  <div id="signupPage" class="hidden">
    <div class="admin-panel">
      <h3>📝 Sign Up</h3>
      <input type="text" id="signupEmail" placeholder="Email">
      <input type="password" id="signupPassword" placeholder="Password">
      <button onclick="signup()">Sign Up</button>
    </div>
  </div>

  <!-- Admin Panel -->
  <div id="adminPage" class="hidden">
    <div class="admin-panel">
      <h3>⚙️ Admin Panel</h3>
      <input type="text" id="videoTitle" placeholder="Video Title">
      <input type="text" id="videoURL" placeholder="Video URL (MP4)">
      <button onclick="addVideo()">Add Video</button>
      <h4>🎞 Manage Videos</h4>
      <div id="adminVideoList"></div>
    </div>
  </div>

</div>

<script>
// === 20 Working Public Domain MP4 Videos ===
let videos = [
 {title:"Learn HTML in 5 Minutes", url:"https://samplelib.com/lib/preview/mp4/sample-5s.mp4"},
 {title:"Learn CSS Fast", url:"https://samplelib.com/lib/preview/mp4/sample-10s.mp4"},
 {title:"JavaScript Basics", url:"https://samplelib.com/lib/preview/mp4/sample-15s.mp4"},
 {title:"Python Tutorial", url:"https://samplelib.com/lib/preview/mp4/sample-20s.mp4"},
 {title:"Science Facts", url:"https://samplelib.com/lib/preview/mp4/sample-30s.mp4"},
 {title:"Solar System Explained", url:"https://samplelib.com/lib/preview/mp4/sample-5mb.mp4"},
 {title:"Geography for Kids", url:"https://samplelib.com/lib/preview/mp4/sample-10mb.mp4"},
 {title:"World History", url:"https://samplelib.com/lib/preview/mp4/sample-15mb.mp4"},
 {title:"Mathematics Basics", url:"https://samplelib.com/lib/preview/mp4/sample-20mb.mp4"},
 {title:"Grammar Lessons", url:"https://samplelib.com/lib/preview/mp4/sample-30mb.mp4"},
 {title:"Animal World", url:"https://samplelib.com/lib/preview/mp4/sample-40mb.mp4"},
 {title:"Technology Today", url:"https://samplelib.com/lib/preview/mp4/sample-50mb.mp4"},
 {title:"Coding for Kids", url:"https://samplelib.com/lib/preview/mp4/sample-1mb.mp4"},
 {title:"Art and Creativity", url:"https://samplelib.com/lib/preview/mp4/sample-3mb.mp4"},
 {title:"Physics in Daily Life", url:"https://samplelib.com/lib/preview/mp4/sample-7mb.mp4"},
 {title:"Healthy Habits", url:"https://samplelib.com/lib/preview/mp4/sample-12mb.mp4"},
 {title:"Environmental Studies", url:"https://samplelib.com/lib/preview/mp4/sample-9mb.mp4"},
 {title:"Space Discovery", url:"https://samplelib.com/lib/preview/mp4/sample-6mb.mp4"},
 {title:"Computer Basics", url:"https://samplelib.com/lib/preview/mp4/sample-2mb.mp4"},
 {title:"Global Culture", url:"https://samplelib.com/lib/preview/mp4/sample-8mb.mp4"}
];

if(localStorage.getItem('videos')) videos = JSON.parse(localStorage.getItem('videos'));
let users = JSON.parse(localStorage.getItem('users')) || [];
let currentUser = JSON.parse(localStorage.getItem('currentUser')) || null;

function showHome(){
  hideAll();
  document.getElementById('homePage').classList.remove('hidden');
  renderVideos();
}
function showLogin(){
  hideAll();
  document.getElementById('loginPage').classList.remove('hidden');
}
function showSignup(){
  hideAll();
  document.getElementById('signupPage').classList.remove('hidden');
}
function showAdmin(){
  hideAll();
  document.getElementById('adminPage').classList.remove('hidden');
  renderAdminVideos();
}
function hideAll(){
  document.getElementById('homePage').classList.add('hidden');
  document.getElementById('loginPage').classList.add('hidden');
  document.getElementById('signupPage').classList.add('hidden');
  document.getElementById('adminPage').classList.add('hidden');
}

function renderVideos(){
  const list=document.getElementById('videoList');
  list.innerHTML='';
  videos.forEach(v=>{
    list.innerHTML+=`
      <div class="video-card">
        <video controls preload="metadata" src="${v.url}"></video>
        <h4>${v.title}</h4>
      </div>`;
  });
}

function renderAdminVideos(){
  const list=document.getElementById('adminVideoList');
  list.innerHTML='';
  videos.forEach((v,i)=>{
    list.innerHTML+=`
      <div class="video-card">
        <video controls src="${v.url}"></video>
        <h4>${v.title}</h4>
        <button onclick="editVideo(${i})">Edit</button>
        <button onclick="deleteVideo(${i})">Delete</button>
      </div>`;
  });
}

function addVideo(){
  const title=document.getElementById('videoTitle').value;
  const url=document.getElementById('videoURL').value;
  if(title && url){
    videos.push({title,url});
    localStorage.setItem('videos',JSON.stringify(videos));
    renderAdminVideos();renderVideos();
    document.getElementById('videoTitle').value='';
    document.getElementById('videoURL').value='';
  }
}
function editVideo(i){
  const newTitle=prompt("Enter new title",videos[i].title);
  const newURL=prompt("Enter new URL",videos[i].url);
  if(newTitle&&newURL){
    videos[i]={title:newTitle,url:newURL};
    localStorage.setItem('videos',JSON.stringify(videos));
    renderAdminVideos();renderVideos();
  }
}
function deleteVideo(i){
  if(confirm("Are you sure?")){
    videos.splice(i,1);
    localStorage.setItem('videos',JSON.stringify(videos));
    renderAdminVideos();renderVideos();
  }
}

function signup(){
  const email=document.getElementById('signupEmail').value;
  const pass=document.getElementById('signupPassword').value;
  if(users.find(u=>u.email===email))return alert("User already exists");
  users.push({email,password:pass});
  localStorage.setItem('users',JSON.stringify(users));
  alert("Signup successful!");showLogin();
}
function login(){
  const email=document.getElementById('loginEmail').value;
  const pass=document.getElementById('loginPassword').value;
  const user=users.find(u=>u.email===email && u.password===pass);
  if(user){
    currentUser=user;
    localStorage.setItem('currentUser',JSON.stringify(user));
    document.getElementById('adminBtn').style.display='inline';
    document.getElementById('logoutBtn').style.display='inline';
    alert("Login successful!");
    showHome();
  } else alert("Invalid credentials");
}
function logout(){
  currentUser=null;
  localStorage.removeItem('currentUser');
  document.getElementById('adminBtn').style.display='none';
  document.getElementById('logoutBtn').style.display='none';
  showHome();
}

// init
showHome();
if(currentUser){
  document.getElementById('adminBtn').style.display='inline';
  document.getElementById('logoutBtn').style.display='inline';
}
</script>

