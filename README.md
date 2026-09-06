# Mini-robot
<!DOCTYPE html><html lang="te"><head><meta charset="UTF-8"><meta name="viewport" content="width=device-width,initial-scale=1"><meta name="theme-color" content="#000"><title>Mini Robot</title><style>body{background:#000;color:#fff;text-align:center;font-family:sans-serif;padding:20px}#r{font-size:90px;animation:p 2s infinite}@keyframes p{0%,100%{transform:scale(1)}50%{transform:scale(1.1)}}button{padding:14px 26px;margin:8px;border-radius:30px;border:0;background:#FF0066;color:#fff;font-size:17px}#off{display:none;position:fixed;inset:0;background:#000;z-index:9999;padding-top:40vh;font-size:24px}</style><link rel="manifest" href="data:application/json;base64,eyJuYW1lIjoiTWluaSBSb2JvdCIsInNob3J0X25hbWUiOiJNaW5pUm9ib3QiLCJzdGFydF91cmwiOiIuIiwiZGlzcGxheSI6InN0YW5kYWxvbmUiLCJiYWNrZ3JvdW5kX2NvbG9yIjoiIzAwMDAwMCIsInRoZW1lX2NvbG9yIjoiI0ZGMDA2NiJ9"></head><body>
<div id="off" onclick="wake()">Tap to Wake Up<br><small>Say: "On Chey"</small></div>
<div id="r">🤖</div><h2>Mini Robot - Sweet Voice</h2><p id="s">Hi Parveen! Nenu ready!</p><p id="h" style="color:#FF99CC"></p>
<button onclick="listen()">🎤 Matladu</button><button onclick="photo()">📸 Photo</button><button onclick="sOff()">🌙 Screen Off</button>
<video id="v" autoplay playsinline style="width:90%;border-radius:15px;margin-top:12px"></video><canvas id="c" style="display:none"></canvas>
<script>
let voice;function loadV(){let vs=speechSynthesis.getVoices();voice=vs.find(x=>x.name.includes("Female"))||vs[0]}speechSynthesis.onvoiceschanged=loadV;loadV();
function sp(t){let u=new SpeechSynthesisUtterance(t);if(voice)u.voice=voice;u.pitch=1.35;u.rate=0.9;speechSynthesis.speak(u);s.innerText=t}
function listen(){let R=window.SpeechRecognition||window.webkitSpeechRecognition;if(!R){alert("Chrome lo open chey");return}let r=new R();r.lang='te-IN';r.start();s.innerText="Vintunna...🎧";r.onresult=e=>{let cmd=e.results[0][0].transcript.toLowerCase();h.innerText="Nuvvu: "+cmd;doCmd(cmd)}}
function doCmd(c){
 if(c.includes("screen off")||c.includes("nidra")||c.includes("sleep")){sOff();sp("Good night Parveen, screen off chestunna");return}
 if(c.includes("on chey")||c.includes("wake")){wake();sp("Welcome back boss!");return}
 if(c.includes("photo")||c.includes("camera")){photo();return}
 if(c.includes("youtube")){let q=c.replace("youtube","").trim();sp(q+" YouTube lo chupistunna");open("https://www.youtube.com/results?search_query="+q);return}
 if(c.includes("search")||c.includes("google")){let q=c.replace("search","").replace("google","").trim();sp(q+" search chestunna");open("https://www.google.com/search?q="+q);return}
 if(c.includes("call")){let n=c.replace(/\D/g,'');if(n.length>=10){sp(n+" ki call chestunna");location.href="tel:"+n}else sp("Number cheppu Parveen");return}
 sp("Ok Parveen, "+c+" ani annav, nenu gurtunchukunna!")
}
async function photo(){try{let st=await navigator.mediaDevices.getUserMedia({video:true});v.srcObject=st;setTimeout(()=>{c.width=640;c.height=480;c.getContext('2d').drawImage(v,0,0);let a=document.createElement('a');a.download='robot-photo.png';a.href=c.toDataURL();a.click();sp("Photo teesa!")},1800)}catch{sp("Camera permission ivvu")}}
function sOff(){off.style.display="block"}function wake(){off.style.display="none";sp("Screen on chesa!")}
window.onload=()=>{setTimeout(()=>sp("Hi Parveen! Nenu nee Mini Robot ni, matladu!"),500)}
</script></body></html>
