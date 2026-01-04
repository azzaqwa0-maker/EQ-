<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Bass EQ</title>
<style>
body{background:#020617;color:#fff;font-family:sans-serif;text-align:center}
input,button{width:80%;margin:8px}
button{padding:8px;border:0;border-radius:8px;background:#38bdf8;font-weight:bold}
</style>
</head>
<body>

<h3>🔊 Bass EQ</h3>
<audio id="a" controls src="music.mp3"></audio>

<p>Sub Bass (60Hz)</p>
<input type="range" min="-20" max="30" value="0" id="sub">

<p>Bass (120Hz)</p>
<input type="range" min="-20" max="30" value="0" id="bass">

<p>Treble</p>
<input type="range" min="-20" max="20" value="0" id="treble">

<button onclick="preset()">🔥 Bass Boost</button>

<script>
const ctx = new AudioContext();
const a = document.getElementById("a");
const src = ctx.createMediaElementSource(a);

const sub = ctx.createBiquadFilter();
sub.type="lowshelf"; sub.frequency.value=60;

const bass = ctx.createBiquadFilter();
bass.type="lowshelf"; bass.frequency.value=120;

const treble = ctx.createBiquadFilter();
treble.type="highshelf"; treble.frequency.value=4000;

src.connect(sub); sub.connect(bass); bass.connect(treble); treble.connect(ctx.destination);

sub.oninput=bass.oninput=treble.oninput=()=>{};
document.getElementById("sub").oninput=e=>sub.gain.value=e.target.value;
document.getElementById("bass").oninput=e=>bass.gain.value=e.target.value;
document.getElementById("treble").oninput=e=>treble.gain.value=e.target.value;

function preset(){
  sub.gain.value=20;
  bass.gain.value=15;
  treble.gain.value=5;
  document.getElementById("sub").value=20;
  document.getElementById("bass").value=15;
  document.getElementById("treble").value=5;
}
a.onplay=()=>ctx.resume();
</script>

</body>
</html>
