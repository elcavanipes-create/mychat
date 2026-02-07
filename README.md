# mychat
MY chat - social app
<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MY chat</title>

<style>
*{box-sizing:border-box;font-family:sans-serif}
body{margin:0;background:#0b0b0b;color:#fff}
header{padding:15px;text-align:center;font-size:22px;
background:linear-gradient(45deg,#ff0055,#00aaff)}
section{padding:10px}

#login input,#chat input{
width:100%;padding:12px;border-radius:12px;
border:none;background:#1c1c1c;color:#fff;margin-bottom:10px
}
button{
width:100%;padding:12px;border:none;
border-radius:12px;background:#00aaff;
color:#fff;font-weight:bold
}

#stories{display:flex;overflow-x:auto;gap:10px}
.story{
min-width:70px;height:70px;border-radius:50%;
background:linear-gradient(45deg,#ff0055,#ffaa00);
display:flex;align-items:center;justify-content:center;
font-size:12px;font-weight:bold
}

#messages{height:50vh;overflow-y:auto;margin:10px 0}
.msg{
background:#1c1c1c;padding:10px;border-radius:12px;
margin-bottom:8px
}

.msg img{max-width:100%;border-radius:10px;margin-top:5px}
.like{color:#ff4d6d;cursor:pointer}
footer{
position:fixed;bottom:0;width:100%;padding:10px;
background:#111
}
</style>
</head>

<body>

<header>💬 MY chat</header>

<section id="login">
<input id="username" placeholder="اسم المستخدم">
<button onclick="login()">دخول</button>
</section>

<section id="chat" style="display:none">

<div id="stories">
<div class="story">+</div>
</div>

<div id="messages"></div>

<input id="text" placeholder="اكتب رسالة">
<input type="file" id="img">
<button onclick="send()">إرسال</button>

</section>

<footer>📱 MY chat - HTML App</footer>

<script>
let user = localStorage.user;
let msgs = JSON.parse(localStorage.msgs||"[]");

if(user) show();

function login(){
user = username.value;
localStorage.user=user;
show();
}

function show(){
login.style.display="none";
chat.style.display="block";
render();
}

function send(){
let t=text.value;
let f=img.files[0];
let r=new FileReader();
r.onload=()=>{
msgs.push({u:user,t, i:r.result, l:0});
save();
}
if(f) r.readAsDataURL(f);
else {msgs.push({u:user,t,i:null,l:0});save();}
text.value="";img.value="";
}

function save(){
localStorage.msgs=JSON.stringify(msgs);
render();
}

function like(i){
msgs[i].l++;save();
}

function render(){
messages.innerHTML="";
msgs.forEach((m,i)=>{
messages.innerHTML+=`
<div class="msg">
<b>${m.u}</b><br>${m.t||""}
${m.i?`<img src="${m.i}">`:""}
<br><span class="like" onclick="like(${i})">❤️ ${m.l}</span>
</div>`;
});
}
</script>

</body>
</html>