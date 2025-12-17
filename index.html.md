#   
<!DOCTYPE html>  
<html lang="tr">  
<head>  
  <meta charset="UTF-8" />  
  <title>Okul Projesi | Bilgi Yarışması</title>  
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />  
  
  <style>  
    *{box-sizing:border-box}  
    body{  
      margin:0;  
      font-family:Arial, Helvetica, sans-serif;  
      background:#111;  
      color:#fff;  
    }  
  
    /* ANA SAYFA */  
    #hero{  
      position:relative;  
      width:100vw;  
      height:100vh;  
      overflow:hidden;  
    }  
    #hero img{  
      width:100%;  
      height:100%;  
      object-fit:cover;  
      filter:brightness(0.55);  
    }  
    #hero-content{  
      position:absolute;  
      top:50%;  
      left:50%;  
      transform:translate(-50%,-50%);  
      text-align:center;  
    }  
    #hero-content h1{  
      font-size:48px;  
      margin-bottom:25px;  
      text-shadow:2px 2px 15px #000;  
    }  
    .btn{  
      padding:15px 35px;  
      font-size:20px;  
      border:none;  
      border-radius:10px;  
      cursor:pointer;  
      background:#fff;  
      color:#000;  
      transition:.3s;  
    }  
    .btn:hover{transform:scale(1.05)}  
  
    /* ÜST MENÜ */  
    #topbar{  
      position:fixed;  
      top:15px;  
      left:15px;  
      right:15px;  
      display:flex;  
      justify-content:space-between;  
      z-index:10;  
    }  
    #topbar button{  
      margin-left:10px;  
      background:#000;  
      color:#fff;  
      border:1px solid #fff;  
      padding:8px 15px;  
      border-radius:8px;  
    }  
  
    /* MENÜ */  
    #menu, #quiz, #admin{  
      display:none;  
      padding:40px;  
      text-align:center;  
    }  
  
    /* QUIZ */  
    .answer{  
      display:block;  
      width:60%;  
      margin:15px auto;  
      padding:15px;  
      font-size:18px;  
      border-radius:10px;  
      border:none;  
      cursor:pointer;  
      transition:.3s;  
    }  
    .answer:hover{background:#ddd;color:#000}  
  
    /* ADMIN */  
    input, textarea, select{  
      padding:10px;  
      margin:5px;  
      width:70%;  
      border-radius:8px;  
      border:none;  
    }  
  
  </style>  
</head>  
<body>  
  
<!-- MÜZİK -->  
<iframe id="music" width="0" height="0" src="https://www.youtube.com/embed/Fcd9O5jLRB8?autoplay=1&loop=1&playlist=Fcd9O5jLRB8" allow="autoplay"></iframe>  
  
<!-- ÜST BAR -->  
<div id="topbar">  
  <div>  
    <button onclick="toggleMusic()">🎵 Müzik</button>  
  </div>  
  <div>  
    <button onclick="showAdmin()">Yönetici</button>  
  </div>  
</div>  
  
<!-- ANA SAYFA -->  
<div id="hero">  
  <img src="https://www.ithakiyayingrubu.com/dosyalar/2022/02/Sabahattin-Ali.jpg" />  
  <div id="hero-content">  
    <h1>Sabahattin Ali</h1>  
    <button class="btn" onclick="enterSite()">Giriş Yap</button>  
  </div>  
</div>  
  
<!-- MENÜ -->  
<div id="menu">  
  <h2>Ana Menü</h2>  
  <button class="btn" onclick="startQuiz()">Bilgi Yarışması</button><br><br>  
  <button class="btn" onclick="openPresentation()">Sunumu Aç</button>  
</div>  
  
<!-- QUIZ -->  
<div id="quiz">  
  <h2 id="timer">40</h2>  
  <h2 id="question"></h2>  
  <div id="answers"></div>  
</div>  
  
<!-- ADMIN -->  
<div id="admin">  
  <h2>Yönetim Paneli</h2>  
  <input id="apass" type="password" placeholder="Şifre"><br>  
  <button onclick="adminLogin()">Giriş</button><hr>  
  <h3>Soru Ekle</h3>  
  <input id="q" placeholder="Soru"><br>  
  <input id="a1" placeholder="A"><br>  
  <input id="a2" placeholder="B"><br>  
  <input id="a3" placeholder="C"><br>  
  <input id="a4" placeholder="D"><br>  
  <input id="correct" placeholder="Doğru (0-3)"><br>  
  <button onclick="addQuestion()">Ekle</button>  
</div>  
  
<script>  
let playing=true;  
let adminPass="1234";  
let questions=JSON.parse(localStorage.getItem("questions")||"[]");  
let index=0, time=40, timer;  
  
function toggleMusic(){  
  const m=document.getElementById("music");  
  playing=!playing;  
  m.src= playing ? "https://www.youtube.com/embed/Fcd9O5jLRB8?autoplay=1&loop=1&playlist=Fcd9O5jLRB8" : "";  
}  
  
function enterSite(){  
  hero.style.display="none";  
  menu.style.display="block";  
}  
  
function startQuiz(){  
  menu.style.display="none";  
  quiz.style.display="block";  
  index=0;  
  loadQuestion();  
}  
  
function loadQuestion(){  
  if(index>=questions.length){alert("Bitti!");return}  
  time=40;  
  timer=setInterval(()=>{  
    timerDisplay.innerText=time--;  
    if(time<0){clearInterval(timer);index++;loadQuestion()}  
  },1000);  
  question.innerText=questions[index].q;  
  answers.innerHTML="";  
  questions[index].a.forEach((x,i)=>{  
    let b=document.createElement("button");  
    b.className="answer";  
    b.innerText=x;  
    b.onclick=()=>{clearInterval(timer);index++;loadQuestion()};  
    answers.appendChild(b);  
  });  
}  
  
function openPresentation(){  
  let p=localStorage.getItem("presentation");  
  if(p) window.open(p);  
  else alert("Sunum yok");  
}  
  
function showAdmin(){admin.style.display="block"}  
  
function adminLogin(){  
  if(apass.value===adminPass) alert("Giriş başarılı");  
  else alert("Hatalı şifre");  
}  
  
function addQuestion(){  
  questions.push({q:q.value,a:[a1.value,a2.value,a3.value,a4.value]});  
  localStorage.setItem("questions",JSON.stringify(questions));  
  alert("Eklendi");  
}  
</script>  
  
</body>  
</html>  
