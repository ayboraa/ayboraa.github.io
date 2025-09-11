---
title: "Whoami"
seo_title: Aybora Ünveren
description: "Who is Aybora Ünveren"
hide:
 - git-revision-date
---

<style>
.md-source-file {
    display: none;
}

.md-content {
    overflow: hidden !important;
}

.matrix-canvas {
    position: absolute !important;
    top: 0 !important;
    left: 0 !important;
    width: 100% !important;
    height: 100% !important;
    z-index: 1 !important;
    pointer-events: none !important;
    opacity: 0.15 !important;
}

.md-content h1,
.md-content #typeit-output,
.md-content button {
    position: relative !important;
    z-index: 10 !important;
    text-shadow: 2px 2px 4px rgba(0,0,0,0.8) !important;
}

.md-content button {
    margin: 0 30px;
    background: #000 !important;
    color: #fff !important;
    border: none !important;
    cursor: pointer !important;
    overflow: hidden;
    position: relative;
    padding: 15px 30px !important;
    font-size: 18px !important;
    border-radius: 8px !important;
    transition: transform 0.2s ease, opacity 0.8s ease;
    opacity: 0;
}

/* Gradient cam parlama efekti */
.md-content button::after {
    content: '';
    position: absolute;
    top: 0;
    left: -75%;
    width: 50%;
    height: 100%;
    background: linear-gradient(
        120deg,
        rgba(255,255,255,0) 0%,
        rgba(255,255,255,0.7) 50%,
        rgba(255,255,255,0) 100%
    );
    transform: skewX(-20deg);
    opacity: 0;
}

/* Hover: efekt ileri kayar */
.md-content button:hover::after {
    animation: shine-forward 1.2s forwards;
}

/* Mouse out: efekt geri kayar */
.md-content button::before {
    content: '';
    position: absolute;
    top: 0;
    left: -75%;
    width: 50%;
    height: 100%;
    background: linear-gradient(
        120deg,
        rgba(255,255,255,0) 0%,
        rgba(255,255,255,0.7) 50%,
        rgba(255,255,255,0) 100%
    );
    transform: skewX(-20deg);
    opacity: 0;
}

.md-content button:not(:hover)::before {
    animation: shine-back 1.2s forwards;
}

@keyframes shine-forward {
    0% { left: -75%; opacity: 0; }
    50% { left: 100%; opacity: 0.8; }
    90% { left: 100%; opacity: 0; } 
}

@keyframes shine-back {
    0% { left: 100%; opacity: 0; }
    50% { left: -75%; opacity: 0.8; }
    99% { left: -75%; opacity: 0; }
    100% { left: -75%; opacity: 0; }
}
</style>

<h1 style="text-align: center;">Aybora Ünveren</h1>
<div id="typeit-output" style="text-align: center;"></div>

<div id="button-container" style="text-align: center; margin-top: 20px; z-index: 10; position: relative;">
    <button data-target="./Mobile Security">📱 Mobile Security</button>
    <button data-target="./offensive">⚔️ Offensive Security</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/typeit@7.0.4/dist/typeit.min.js"></script>
<script>
function startEffects(instant=false) {
    document.querySelectorAll('.matrix-canvas').forEach(c => c.remove());
    
    const canvas = document.createElement('canvas');
    canvas.className = 'matrix-canvas';
    const ctx = canvas.getContext('2d');
    const mdContent = document.querySelector('.md-content');
    if (!mdContent) return;
    
    canvas.width = mdContent.offsetWidth;
    canvas.height = mdContent.offsetHeight || window.innerHeight;
    mdContent.appendChild(canvas);
    
    const chars = 'アイウエオカキクケコサシスセソタチツテトナニヌネノハヒフヘホマミムメモヤユヨラリルレロワヲン';
    const fontSize = 8;
    const columns = canvas.width / fontSize;
    const drops = [];
    
    for (let i = 0; i < columns; i++) {
        drops[i] = Math.random() * -100;
    }
    
    function draw() {
        ctx.fillStyle = 'rgba(0, 0, 0, 0.03)';
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        ctx.fillStyle = '#ffffff';
        ctx.font = fontSize + 'px Courier New';
        for (let i = 0; i < drops.length; i++) {
            const text = chars.charAt(Math.floor(Math.random() * chars.length));
            ctx.fillText(text, i * fontSize, drops[i] * fontSize);
            if (Math.random() < 0.66) drops[i]++;
            if (drops[i] * fontSize > canvas.height && Math.random() > 0.99) {
                drops[i] = -Math.random() * 100;
            }
        }
        setTimeout(() => requestAnimationFrame(draw), 33);
    }
    
    draw();
    
    const output = document.getElementById('typeit-output');
    if (output && typeof TypeIt !== 'undefined') {
        output.innerHTML = '';
        const typeitInstance = new TypeIt("#typeit-output", {
            strings: [
                "I'm a security researcher.",
                "I break things to understand them.", 
                "Currently focusing on mobile security."
            ],
            speed: 50,
            waitUntilVisible: true,
            afterComplete: () => {
                const buttons = document.querySelectorAll('#button-container button');
                buttons.forEach((btn, i) => {
                    setTimeout(() => {
                        btn.style.opacity = 1;
                    }, i * 200);
                });
            }
        });
        if(instant) {
            typeitInstance.destroy();
            output.innerHTML = "I'm a security researcher.<br> I break things to understand them.<br> Currently focusing on mobile security.";
            const buttons = document.querySelectorAll('#button-container button');
            buttons.forEach(btn => btn.style.opacity = 1);
        } else {
            typeitInstance.go();
        }
    }
}

// Check localStorage
const visited = localStorage.getItem('visitedBefore');
const instantLoad = visited === 'true';
setTimeout(() => startEffects(instantLoad), 100);

const buttons = document.querySelectorAll('#button-container button');
buttons.forEach(btn => {
    btn.addEventListener('click', () => {
        localStorage.setItem('visitedBefore', 'true');
        window.location.href = btn.dataset.target;
    });
});

setInterval(() => {
    if (document.getElementById('typeit-output') && !document.querySelector('.matrix-canvas')) {
        startEffects(localStorage.getItem('visitedBefore') === 'true');
    }
}, 1000);
</script>
