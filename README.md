```html
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no, viewport-fit=cover">

<title>🍀 Luckify Pro</title>

<!-- ============================================================
   META ETIQUETAS PARA COMPATIBILIDAD CON IPHONE (iOS PWA)
   ============================================================ */ -->
<!-- Indica a iOS que puede instalarse en la pantalla de inicio -->
<meta name="apple-mobile-web-app-capable" content="yes">
<!-- Define el título de la app debajo del icono en el iPhone -->
<meta name="apple-mobile-web-app-title" content="Luckify">
<!-- Controla el estilo de la barra de estado (traslúcida para diseño moderno) -->
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">

<!-- Icono de la App para la pantalla de inicio del iPhone -->
<link rel="apple-touch-icon" href="https://fav.farm/🍀">

<style>
/* ============================================================
   VARIABLES (Estilos limpios con CSS Variables)
   ============================================================ */

:root {
  /* Colores principales */
  --color-indigo:     #6366f1;
  --color-indigo-dark:#4f46e5;
  --color-pink:       #ec4899;
  --color-red-start:  #ff3c3c;
  --color-red-end:    #ff6b6b;
  --color-bg:         #09090f;

  /* Superficies con transparencia */
  --surface-card:     rgba(255, 255, 255, 0.08);
  --surface-player:   rgba(255, 255, 255, 0.05);
  --border-color:     rgba(255, 255, 255, 0.10);
  --border-player:    rgba(255, 255, 255, 0.08);

  /* Sombras */
  --shadow-card:      0 10px 30px rgba(0, 0, 0, 0.30);
  --shadow-card-hover:0 15px 35px rgba(0, 0, 0, 0.40);

  /* Tipografía */
  --font-base:        -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
  --fs-title:         42px;
  --fs-result:        26px;
  --fs-final:         24px;
  --fs-score:         18px;
  --fs-emoji:         60px;
  --fs-button:        16px;

  /* Espaciado y bordes */
  --radius-card:      28px;
  --radius-player:    22px;
  --radius-button:    18px;
  --padding-card:     20px;
  --padding-button:   15px;

  /* Transiciones */
  --transition-card:  transform 0.25s ease, box-shadow 0.25s ease;
  --transition-btn:   transform 0.2s ease, filter 0.2s ease;
}


/* ============================================================
   RESET & BASE
   ============================================================ */

*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  -webkit-tap-highlight-color: transparent; /* Elimina el flash azul al tocar botones en iOS */
}

body {
  min-height: 100vh;
  font-family: var(--font-base);
  color: white;

  background:
    radial-gradient(circle at top left,    var(--color-indigo-dark), transparent 30%),
    radial-gradient(circle at bottom right, var(--color-pink),        transparent 30%),
    var(--color-bg);

  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
  /* Espaciado seguro para dispositivos con Notch o Dynamic Island */
  padding-top: env(safe-area-inset-top, 20px);
  padding-bottom: env(safe-area-inset-bottom, 20px);
}


/* ============================================================
   LAYOUT PRINCIPAL
   ============================================================ */

.app {
  width: 100%;
  max-width: 500px;
  animation: fadeIn 0.7s ease both;
}


/* ============================================================
   TÍTULO
   ============================================================ */

.title {
  text-align: center;
  margin-bottom: 25px;
}

.title h1 {
  font-size: var(--fs-title);
  text-shadow: 0 0 20px rgba(255, 255, 255, 0.15);
}

.title p {
  margin-top: 5px;
  opacity: 0.7;
}


/* ============================================================
   TARJETA
   ============================================================ */

.card {
  background:        var(--surface-card);
  backdrop-filter:   blur(18px);
  -webkit-backdrop-filter: blur(18px);
  border:            1px solid var(--border-color);
  border-radius:     var(--radius-card);
  padding:           var(--padding-card);
  margin-bottom:     20px;
  box-shadow:        var(--shadow-card);
  transition:        var(--transition-card);
}

.card:hover {
  transform:   translateY(-3px);
  box-shadow:  var(--shadow-card-hover);
}

.card h2 {
  margin-bottom: 15px;
}


/* ============================================================
   BOTONES
   ============================================================ */

button {
  display: block;
  width: 100%;
  padding: var(--padding-button);
  margin-top: 10px;
  border: none;
  border-radius: var(--radius-button);
  background: linear-gradient(45deg, var(--color-indigo), var(--color-pink));
  color: white;
  font-family: inherit;
  font-size: var(--fs-button);
  font-weight: bold;
  cursor: pointer;
  transition: var(--transition-btn);
}

button:hover {
  transform: scale(1.03);
  filter: brightness(1.1);
}

button:active {
  transform: scale(0.96);
}

/* Variante: reset / peligro */
.reset {
  background: linear-gradient(45deg, var(--color-red-start), var(--color-red-end));
}


/* ============================================================
   RESULTADO
   ============================================================ */

.resultado {
  margin-top: 18px;
  text-align: center;
  font-size: var(--fs-result);
  font-weight: bold;
  min-height: 40px;
}


/* ============================================================
   PIEDRA-PAPEL-TIJERAS — Arena
   ============================================================ */

.arena {
  display: flex;
  gap: 15px;
  justify-content: center;
  flex-wrap: wrap;
  margin-top: 10px;
}

.jugador {
  flex: 1;
  min-width: 150px;
  padding: 18px;
  text-align: center;
  background:    var(--surface-player);
  border:        1px solid var(--border-player);
  border-radius: var(--radius-player);
  transition:    transform 0.25s ease;
}

.jugador:hover {
  transform: translateY(-4px);
}

.jugador h3 {
  margin-bottom: 15px;
}

.eleccion {
  font-size:  var(--fs-emoji);
  margin:     15px 0;
  min-height: 70px;
  display: inline-block;
  transition: transform 0.2s ease;
}

.final {
  margin-top:  20px;
  text-align:  center;
  font-size:   var(--fs-final);
  font-weight: bold;
  min-height:  70px;
}

.scoreboard {
  display:         flex;
  justify-content: center;
  gap:             30px;
  margin-top:      20px;
  font-size:       var(--fs-score);
}


/* ============================================================
   ANIMACIONES CLASIFICADAS
   ============================================================ */

@keyframes fadeIn {
  from {
    opacity:   0;
    transform: translateY(20px);
  }
  to {
    opacity:   1;
    transform: translateY(0);
  }
}

@keyframes pop {
  0% {
    opacity:   0.3;
    transform: scale(0.6);
  }
  100% {
    opacity:   1;
    transform: scale(1);
  }
}

@keyframes spin {
  0% { transform: rotate(0deg) scale(0.8); }
  100% { transform: rotate(360deg) scale(1); }
}

@keyframes flip {
  0% { transform: rotateY(0deg) scale(1); }
  50% { transform: rotateY(360deg) scale(1.3); }
  100% { transform: rotateY(720deg) scale(1); }
}

/* Clases de activación de animación dinámicas */
.anim-pop {
  animation: pop 0.25s cubic-bezier(0.175, 0.885, 0.32, 1.2) both;
}

.anim-spin {
  animation: spin 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.1) both;
}

.anim-flip {
  animation: flip 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.2) both;
}

/* Movimiento de puños de Piedra, Papel o Tijera */
.shake-left {
  animation: shakeLeft 0.4s ease infinite;
}

.shake-right {
  animation: shakeRight 0.4s ease infinite;
}

@keyframes shakeLeft {
  0%, 100% { transform: translateY(0) rotate(10deg); }
  50% { transform: translateY(-15px) rotate(-5deg); }
}

@keyframes shakeRight {
  0%, 100% { transform: scaleX(-1) translateY(0) rotate(10deg); }
  50% { transform: scaleX(-1) translateY(-15px) rotate(-5deg); }
}


/* ============================================================
   RESPONSIVE
   ============================================================ */

@media (max-width: 600px) {
  .title h1 {
    font-size: 34px;
  }

  .arena {
    flex-direction: column;
  }
}
</style>
</head>

<body>

<div class="app">

  <div class="title">
    <h1>🍀 Luckify</h1>
    <p>Decisiones completamente al azar</p>
  </div>

  <!-- VOLADO -->
  <div class="card">
    <h2>🪙 Cara o Cruz</h2>
    <button onclick="volado()">Lanzar moneda</button>
    <div class="resultado" id="coinResult">?</div>
  </div>

  <!-- DADO -->
  <div class="card">
    <h2>🎲 Dado</h2>
    <button onclick="dado()">Lanzar dado</button>
    <div class="resultado" id="diceResult">?</div>
  </div>

  <!-- PPT -->
  <div class="card">
    <h2>⚔️ Piedra Papel Tijera</h2>
    
    <div class="arena">
      <div class="jugador">
        <h3>Jugador 1</h3>
        <div class="eleccion" id="e1">❔</div>
        <button class="ppt-btn" onclick="lanzar(1)">Lanzar</button>
      </div>

      <div class="jugador">
        <h3>Jugador 2</h3>
        <div class="eleccion" id="e2">❔</div>
        <button class="ppt-btn" onclick="lanzar(2)">Lanzar</button>
      </div>
    </div>

    <div class="final" id="pptResult">Esperando jugadores...</div>

    <div class="scoreboard">
      <div>🏆 J1: <span id="score1">0</span></div>
      <div>🏆 J2: <span id="score2">0</span></div>
    </div>

    <button class="reset" onclick="reiniciarPPT()">Reiniciar marcador</button>
  </div>

</div>

<!-- LÓGICA DE INTERACCIÓN, ANIMACIÓN REUTILIZABLE Y AUDIO SINTETIZADO -->
<script>
/* ==========================================================================
   SINTETIZADOR DE AUDIO (Web Audio API)
   ========================================================================== */
const audioCtx = new (window.AudioContext || window.webkitAudioContext)();

function playSound(type) {
    if (audioCtx.state === 'suspended') {
        audioCtx.resume();
    }
    const now = audioCtx.currentTime;

    switch (type) {
        case 'coin-spin':
            {
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = 'sine';
                osc.frequency.setValueAtTime(587.33, now); 
                osc.frequency.exponentialRampToValueAtTime(1174.66, now + 0.15); 
                osc.frequency.exponentialRampToValueAtTime(880, now + 0.3); 
                
                gain.gain.setValueAtTime(0.25, now);
                gain.gain.exponentialRampToValueAtTime(0.01, now + 0.4);

                osc.connect(gain);
                gain.connect(audioCtx.destination);
                osc.start(now);
                osc.stop(now + 0.4);
            }
            break;

        case 'coin-land':
            {
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = 'triangle';
                osc.frequency.setValueAtTime(987.77, now); 
                osc.frequency.setValueAtTime(1318.51, now + 0.08); 
                
                gain.gain.setValueAtTime(0.3, now);
                gain.gain.exponentialRampToValueAtTime(0.01, now + 0.5);

                osc.connect(gain);
                gain.connect(audioCtx.destination);
                osc.start(now);
                osc.stop(now + 0.5);
            }
            break;

        case 'dice-roll':
            {
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = 'triangle';
                osc.frequency.setValueAtTime(130 + Math.random() * 70, now);
                
                gain.gain.setValueAtTime(0.12, now);
                gain.gain.exponentialRampToValueAtTime(0.01, now + 0.05);

                osc.connect(gain);
                gain.connect(audioCtx.destination);
                osc.start(now);
                osc.stop(now + 0.06);
            }
            break;

        case 'dice-stop':
            {
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = 'sine';
                osc.frequency.setValueAtTime(329.63, now); 
                osc.frequency.exponentialRampToValueAtTime(523.25, now + 0.1); 
                
                gain.gain.setValueAtTime(0.3, now);
                gain.gain.exponentialRampToValueAtTime(0.01, now + 0.3);

                osc.connect(gain);
                gain.connect(audioCtx.destination);
                osc.start(now);
                osc.stop(now + 0.3);
            }
            break;

        case 'click':
            {
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = 'sine';
                osc.frequency.setValueAtTime(450, now);
                osc.frequency.exponentialRampToValueAtTime(200, now + 0.1);
                
                gain.gain.setValueAtTime(0.15, now);
                gain.gain.exponentialRampToValueAtTime(0.01, now + 0.1);

                osc.connect(gain);
                gain.connect(audioCtx.destination);
                osc.start(now);
                osc.stop(now + 0.1);
            }
            break;

        case 'swing':
            {
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = 'sawtooth';
                osc.frequency.setValueAtTime(120, now);
                osc.frequency.exponentialRampToValueAtTime(40, now + 0.08);
                
                gain.gain.setValueAtTime(0.2, now);
                gain.gain.exponentialRampToValueAtTime(0.01, now + 0.1);

                osc.connect(gain);
                gain.connect(audioCtx.destination);
                osc.start(now);
                osc.stop(now + 0.1);
            }
            break;

        case 'win-jingle':
            {
                const notes = [523.25, 659.25, 783.99, 1046.50]; 
                notes.forEach((freq, idx) => {
                    const osc = audioCtx.createOscillator();
                    const gain = audioCtx.createGain();
                    osc.type = 'triangle';
                    osc.frequency.value = freq;
                    
                    gain.gain.setValueAtTime(0, now);
                    gain.gain.linearRampToValueAtTime(0.2, now + (idx * 0.08) + 0.01);
                    gain.gain.exponentialRampToValueAtTime(0.001, now + 0.4 + (idx * 0.08));
                    
                    osc.connect(gain);
                    gain.connect(audioCtx.destination);
                    osc.start(now + (idx * 0.08));
                    osc.stop(now + 0.5 + (idx * 0.08));
                });
            }
            break;

        case 'draw-jingle':
            {
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.type = 'sine';
                osc.frequency.setValueAtTime(440, now);
                osc.frequency.setValueAtTime(349.23, now + 0.15); 
                
                gain.gain.setValueAtTime(0.2, now);
                gain.gain.exponentialRampToValueAtTime(0.01, now + 0.35);

                osc.connect(gain);
                gain.connect(audioCtx.destination);
                osc.start(now);
                osc.stop(now + 0.35);
            }
            break;
    }
}

/* ==========================================================================
   LÓGICA: VOLADO (CARA O CRUZ)
   ========================================================================== */
let isFlipping = false;

function volado(){
    if (isFlipping) return;
    isFlipping = true;

    playSound('coin-spin');
    const container = document.getElementById("coinResult");
    
    container.classList.remove("anim-flip", "anim-pop");
    void container.offsetWidth; 
    
    container.innerText = "🪙";
    container.classList.add("anim-flip");

    setTimeout(() => {
        const result = Math.random() < 0.5 ? "🪙 Cara" : "🪙 Cruz";
        
        container.classList.remove("anim-flip");
        void container.offsetWidth;
        
        container.innerText = result;
        container.classList.add("anim-pop");
        
        playSound('coin-land');
        isFlipping = false;
    }, 600);
}

/* ==========================================================================
   LÓGICA: DADO
   ========================================================================== */
let isRolling = false;
const diceSymbols = ["⚀", "⚁", "⚂", "⚃", "⚄", "⚅"];

function dado(){
    if (isRolling) return;
    isRolling = true;

    const container = document.getElementById("diceResult");
    
    container.classList.remove("anim-spin", "anim-pop");
    void container.offsetWidth;
    container.classList.add("anim-spin");

    let speed = 50;
    const playRollTick = () => {
        if (speed < 400) {
            playSound('dice-roll');
            const randomFace = diceSymbols[Math.floor(Math.random() * 6)];
            container.innerText = randomFace;
            speed += 60;
            setTimeout(playRollTick, speed);
        }
    };
    playRollTick();

    setTimeout(() => {
        const num = Math.floor(Math.random() * 6) + 1;
        
        container.classList.remove("anim-spin");
        void container.offsetWidth;
        
        container.innerText = diceSymbols[num - 1] + " (" + num + ")";
        container.classList.add("anim-pop");

        playSound('dice-stop');
        isRolling = false;
    }, 500);
}

/* ==========================================================================
   LÓGICA: PIEDRA, PAPEL O TIJERA (PPT)
   ========================================================================== */
const opcionesPPT = [
    { nombre:"Piedra", emoji:"✊" },
    { nombre:"Papel", emoji:"✋" },
    { nombre:"Tijera", emoji:"✌️" }
];

let jugadas = { 1:null, 2:null };
let puntuacion = { 1:0, 2:0 };
let pptState = "idle"; // "idle", "shaking", "result"

function lanzar(jugador){
    if (pptState === "shaking") return;

    if (pptState === "result") {
        const e1 = document.getElementById("e1");
        const e2 = document.getElementById("e2");
        
        e1.innerText = "❔";
        e2.innerText = "❔";
        e1.classList.remove("anim-pop");
        e2.classList.remove("anim-pop");
        e1.style.transform = "none";
        e2.style.transform = "none";
        
        document.getElementById("pptResult").innerText = "Esperando jugadores...";
        jugadas = { 1:null, 2:null };
        pptState = "idle";
    }

    const opcion = opcionesPPT[Math.floor(Math.random() * opcionesPPT.length)];
    jugadas[jugador] = opcion;

    playSound('click');
    document.getElementById(`e${jugador}`).innerText = "✅";

    if(jugadas[1] && jugadas[2]){
        ejecutarCoreografiaPPT();
    } else {
        document.getElementById("pptResult").innerText = "Esperando al otro jugador...";
    }
}

function ejecutarCoreografiaPPT() {
    pptState = "shaking";
    const e1 = document.getElementById("e1");
    const e2 = document.getElementById("e2");
    const pptResult = document.getElementById("pptResult");

    e1.classList.remove("anim-pop");
    e2.classList.remove("anim-pop");

    e1.innerText = "✊";
    e2.innerText = "✊";
    e1.classList.add("shake-left");
    e2.classList.add("shake-right");

    let tick = 0;
    pptResult.innerText = "¡Piedra!";
    playSound('swing');

    const interval = setInterval(() => {
        tick++;
        if (tick === 1) {
            pptResult.innerText = "¡Papel!";
            playSound('swing');
        } else if (tick === 2) {
            pptResult.innerText = "¡O Tijera!";
            playSound('swing');
        } else if (tick === 3) {
            clearInterval(interval);
            e1.classList.remove("shake-left");
            e2.classList.remove("shake-right");
            determinarGanador();
        }
    }, 450);
}

function determinarGanador(){
    const j1 = jugadas[1].nombre;
    const j2 = jugadas[2].nombre;
    let resultado = "";
    let isDraw = false;

    if(j1 === j2){
        resultado = "🤝 ¡EMPATE!";
        isDraw = true;
    } else if(
        (j1==="Piedra" && j2==="Tijera") ||
        (j1==="Papel" && j2==="Piedra") ||
        (j1==="Tijera" && j2==="Papel")
    ){
        resultado = "🔥 ¡GANA JUGADOR 1!";
        puntuacion[1]++;
    } else {
        resultado = "⚡ ¡GANA JUGADOR 2!";
        puntuacion[2]++;
    }

    const e1 = document.getElementById("e1");
    const e2 = document.getElementById("e2");
    
    e1.innerText = jugadas[1].emoji;
    e2.innerText = jugadas[2].emoji;
    
    e2.style.transform = "scaleX(-1)";

    e1.classList.remove("anim-pop");
    e2.classList.remove("anim-pop");
    void e1.offsetWidth;
    void e2.offsetWidth;
    e1.classList.add("anim-pop");
    e2.classList.add("anim-pop");

    if (isDraw) {
        playSound('draw-jingle');
    } else {
        playSound('win-jingle');
    }

    document.getElementById("pptResult").innerHTML = `
        ${jugadas[1].emoji} ⚔️ <span style="display:inline-block; transform: scaleX(-1);">${jugadas[2].emoji}</span>
        <br><br>
        ${resultado}
    `;

    document.getElementById("score1").innerText = puntuacion[1];
    document.getElementById("score2").innerText = puntuacion[2];

    pptState = "result";
}

function reiniciarPPT(){
    puntuacion = { 1:0, 2:0 };
    jugadas = { 1:null, 2:null };
    pptState = "idle";

    playSound('click');

    document.getElementById("score1").innerText = "0";
    document.getElementById("score2").innerText = "0";
    document.getElementById("pptResult").innerText = "Marcador reiniciado";
    
    const e1 = document.getElementById("e1");
    const e2 = document.getElementById("e2");
    
    e1.innerText = "❔";
    e2.innerText = "❔";
    
    e1.classList.remove("anim-pop");
    e2.classList.remove("anim-pop");
    e1.style.transform = "none";
    e2.style.transform = "none";
}
</script>

</body>
</html>

```

