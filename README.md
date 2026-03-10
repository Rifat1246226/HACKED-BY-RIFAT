<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Hacker Prank</title>
<style>
body {
    margin: 0;
    background: black;
    color: #0f0;
    font-family: monospace;
    overflow: hidden;
}
#matrix {
    position: absolute;
    width: 100%;
    height: 100%;
}
.alert {
    position: absolute;
    left: 50px;
    color: red;
    font-size: 60px; /* বড় Warning text */
    font-weight: bold;
    animation: blink 1s infinite;
}
@keyframes blink {
    0%, 50%, 100% {opacity:1;}
    25%, 75% {opacity:0;}
}
#logo {
    position: absolute;
    top: 20px;
    right: 50px;
    width: 150px;
}
</style>
</head>
<body>
<img id="logo" src="https://upload.wikimedia.org/wikipedia/commons/2/2c/Anonymous_emblem.svg" alt="Hacker Logo">
<canvas id="matrix"></canvas>

<script>
// Matrix effect
const canvas = document.getElementById('matrix');
const ctx = canvas.getContext('2d');
canvas.height = window.innerHeight;
canvas.width = window.innerWidth;

const letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789@#$%^&*()*&^%";
const fontSize = 16;
const columns = canvas.width / fontSize;
const drops = [];
for(let x = 0; x < columns; x++) drops[x] = 1;

function draw() {
    ctx.fillStyle = "rgba(0, 0, 0, 0.05)";
    ctx.fillRect(0, 0, canvas.width, canvas.height);
    ctx.fillStyle = "#0F0";
    ctx.font = fontSize + "px monospace";
    for(let i = 0; i < drops.length; i++){
        const text = letters.charAt(Math.floor(Math.random()*letters.length));
        ctx.fillText(text, i*fontSize, drops[i]*fontSize);
        if(drops[i]*fontSize > canvas.height && Math.random() > 0.975) drops[i] = 0;
        drops[i]++;
    }
}

setInterval(draw, 50);

// Typing fake hacking messages
let messages = [
    "ACCESS GRANTED ✔",
    "SCANNING DEVICE...",
    "READING FACEBOOK DATA...",
    "READING GMAIL DATA...",
    "UPLOADING TO SERVER...",
    "",
    "⚠ WARNING: JUST A PRANK! 😄"
];

let i = 0;
setTimeout(function typeMsg(){
    if(i < messages.length){
        const div = document.createElement('div');
        div.className = 'alert';
        div.style.top = `${100 + i*70}px`;
        div.innerText = messages[i];
        document.body.appendChild(div);
        i++;
        setTimeout(typeMsg, 1500);
    }
}, 2000);

// Click alert + sound effect
document.body.addEventListener('click', () => {
    alert("SYSTEM ALERT! 😎 Just a prank!");
    const audio = new Audio('https://www.soundjay.com/buttons/sounds/beep-07.mp3');
    audio.play();
});
</script>
</body>
</html>
