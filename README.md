# STV 
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>EduTV - Online Learning</title>
<style>
body {font-family: Arial, sans-serif; margin:0; background:#f0f2f5;}
header {background:#1e90ff; color:white; padding:15px; text-align:center;}
nav {display:flex; justify-content:center; background:#0074cc;}
nav button {margin:5px; padding:10px 20px; background:white; border:none; cursor:pointer; border-radius:5px;}
nav button:hover {background:#ddd;}
.container {padding:20px;}
.video-card {background:white; padding:10px; margin:10px; display:inline-block; vertical-align:top; width:300px; border-radius:8px; box-shadow:0 0 5px rgba(0,0,0,0.2);}
.video-card video {width:100%; border-radius:5px;}
.video-card h4 {margin:5px 0;}
.admin-panel {background:#fff; padding:20px; border-radius:10px; box-shadow:0 0 10px rgba(0,0,0,0.2); max-width:600px; margin:auto;}
input, button {padding:10px; margin:5px 0; width:100%; box-sizing:border-box;}
button {background:#1e90ff; color:white; border:none; border-radius:5px; cursor:pointer;}
button:hover {background:#0074cc;}
.hidden {display:none;}
</style>
</head>
<body>

<header>
  <h1>EduTV - Online Learning</h1>
</header>

<nav>
  <button onclick="showHome()">Home</button>
  <button onclick="showLogin()">Login</button>
  <button onclick="showSignup()">Sign Up</button>
  <button onclick="showAdmin()" id="adminBtn" style="display:none;">Admin Panel</button>
  <button onclick="logout()" id="logoutBtn" style="display:none;">Logout</button>
</nav>

<div class="container">

  <!-- Home Page -->
  <div id="homePage">
    <h2>Educational Videos</h2>
    <div id="videoList"></div>
  </div>

  <!-- Login Page -->
  <div id="loginPage" class="hidden">
    <div class="admin-panel">
      <h3>Login</h3>
      <input type="text" id="loginEmail" placeholder="Email">
      <input type="password" id="loginPassword" placeholder="Password">
      <button onclick="login()">Login</button>
    </div>
  </div>

  <!-- Signup Page -->
  <div id="signupPage" class="hidden">
    <div class="admin-panel">
      <h3>Sign Up</h3>
      <input type="text" id="signupEmail" placeholder="Email">
      <input type="password" id="signupPassword" placeholder="Password">
      <button onclick="signup()">Sign Up</button>
    </div>
  </div>

  <!-- Admin Panel -->
  <div id="adminPage" class="hidden">
    <div class="admin-panel">
      <h3>Admin Panel</h3>
      <input type="text" id="videoTitle" placeholder="Video Title">
      <input type="text" id="videoURL" placeholder="Video URL (MP4)">
      <button onclick="addVideo()">Add Video</button>
      <h4>Existing Videos</h4>
      <div id="adminVideoList"></div>
    </div>
  </div>

</div>

<script>
// Initialize 20 copyright-free educational videos
let videos = [
  {title:"Learn HTML Basics", url:"https://www.w3schools.com/html/mov_bbb.mp4"},
  {title:"Learn CSS Basics", url:"https://www.w3schools.com/html/movie.mp4"},
  {title:"Learn JavaScript", url:"https://www.w3schools.com/html/mov_bbb.mp4"},
  {title:"Python Programming Intro", url:"https://www.w3schools.com/html/movie.mp4"},
  {title:"Science for Kids", url:"https://archive.org/download/educational_science/educational_science.mp4"},
  {title:"Math Basics", url:"https://archive.org/download/educational_math/educational_math.mp4"},
  {title:"English Alphabets", url:"https://archive.org/download/abc_alphabet/abc_alphabet.mp4"},
  {title:"Learn Shapes", url:"https://archive.org/download/learn_shapes/learn_shapes.mp4"},
  {title:"Animals and Nature", url:"https://archive.org/download/animals_and_nature/animals_and_nature.mp4"},
  {title:"Solar System", url:"https://archive.org/download/solar_system/solar_system.mp4"},
  {title:"History Basics", url:"https://archive.org/download/history_basics/history_basics.mp4"},
  {title:"Music for Kids", url:"https://archive.org/download/music_for_kids/music_for_kids.mp4"},
  {title:"Art & Craft", url:"https://archive.org/download/art_and_craft/art_and_craft.mp4"},
  {title:"Learn Colors", url:"https://archive.org/download/learn_colors/learn_colors.mp4"},
  {title:"Geography Basics", url:"https://archive.org/download/geography_basics/geography_basics.mp4"},
  {title:"Fun Science Experiments", url:"https://archive.org/download/fun_science/fun_science.mp4"},
  {title:"Storytelling for Kids", url:"https://archive.org/download/storytelling/storytelling.mp4"},
  {title:"Basic Computer Skills", url:"https://archive.org/download/computer_skills/computer_skills.mp4"},
  {title:"Healthy Habits", url:"https://archive.org/download/healthy_habits/healthy_habits.mp4"},
  {title:"Environmental Awareness", url:"https://archive.org/download/environmental_awareness/environmental_awareness.mp4"}
];

// Load from LocalStorage
if(localStorage.getItem('videos')) videos = JSON.parse(localStorage.getItem('videos'));

// Load users
let users = JSON.parse(localStorage.getItem('users')) || [];
let currentUser = JSON.parse(localStorage.getItem('currentUser')) || null;

// Functions to show pages
function showHome(){document.getElementById('homePage').classList.remove('hidden');document.getElementById('loginPage').classList.add('hidden');document.getElementById('signupPage').classList.add('hidden');document.getElementById('adminPage').classList.add('hidden');renderVideos();}
function showLogin(){document.getElementById('homePage').classList.add('hidden');document.getElementById('loginPage').classList.remove('hidden');document.getElementById('signupPage').classList.add('hidden');document.getElementById('adminPage').classList.add('hidden');}
function showSignup(){document.getElementById('homePage').classList.add('hidden');document.getElementById('loginPage').classList.add('hidden');document.getElementById('signupPage').classList.remove('hidden');document.getElementById('adminPage').classList.add('hidden');}
function showAdmin(){document.getElementById('homePage').classList.add('hidden');document.getElementById('loginPage').classList.add('hidden');document.getElementById('signupPage').classList.add('hidden');document.getElementById('adminPage').classList.remove('hidden');renderAdminVideos();}

// Render video list
function renderVideos(){
  const list = document.getElementById('videoList');
  list.innerHTML = '';
  videos.forEach((v,i)=>{
    list.innerHTML += `<div class="video-card"><video controls src="${v.url}"></video><h4>${v.title}</h4></div>`;
  });
}

// Render admin video list
function renderAdminVideos(){
  const list = document.getElementById('adminVideoList');
  list.innerHTML = '';
  videos.forEach((v,i)=>{
    list.innerHTML += `<div class="video-card">
      <video controls src="${v.url}"></video>
      <h4>${v.title}</h4>
      <button onclick="editVideo(${i})">Edit</button>
      <button onclick="deleteVideo(${i})">Delete</button>
    </div>`;
  });
}

// Add video
function addVideo(){
  const title = document.getElementById('videoTitle').value;
  const url = document.getElementById('videoURL').value;
  if(title && url){ videos.push({title,url}); localStorage.setItem('videos',JSON.stringify(videos)); renderAdminVideos(); document.getElementById('videoTitle').value=''; document.getElementById('videoURL').value=''; renderVideos();}
}

// Edit video
function editVideo(index){
  const newTitle = prompt("Enter new title", videos[index].title);
  const newURL = prompt("Enter new URL", videos[index].url);
  if(newTitle && newURL){videos[index]={title:newTitle,url:newURL}; localStorage.setItem('videos',JSON.stringify(videos)); renderAdminVideos(); renderVideos();}
}

// Delete video
function deleteVideo(index){ if(confirm("Are you sure?")){ videos.splice(index,1); localStorage.setItem('videos',JSON.stringify(videos)); renderAdminVideos(); renderVideos();}}

// Signup
function signup(){
  const email = document.getElementById('signupEmail').value;
  const pass = document.getElementById('signupPassword').value;
  if(users.find(u=>u.email===email)){alert("User exists"); return;}
  users.push({email,password:pass,role:'admin'});
  localStorage.setItem('users',JSON.stringify(users));
  alert("Signup successful"); showLogin();
}

// Login
function login(){
  const email = document.getElementById('loginEmail').value;
  const pass = document.getElementById('loginPassword').value;
  const user = users.find(u=>u.email===email && u.password===pass);
  if(user){ currentUser=user; localStorage.setItem('currentUser',JSON.stringify(currentUser)); alert("Login successful"); document.getElementById('adminBtn').style.display='inline'; document.getElementById('logoutBtn').style.display='inline'; showHome();}
  else alert("Invalid credentials");
}

// Logout
function logout(){currentUser=null; localStorage.removeItem('currentUser'); document.getElementById('adminBtn').style.display='none'; document.getElementById('logoutBtn').style.display='none'; showHome();}

// Initialize page
showHome();
if(currentUser){document.getElementById('adminBtn').style.display='inline'; document.getElementById('logoutBtn').style.display='inline';}
</script>
