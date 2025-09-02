# tess-website-kontolll
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Kenzo | Ethical Hacker</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    body {
      margin: 0;
      background: linear-gradient(180deg, #0c0c1d, #05050a, #000);
      color: #cbd5e1; /* lebih soft */
      font-family: 'JetBrains Mono', monospace;
    }

    .container {
      max-width: 420px;
      margin: auto;
      padding: 1rem;
      position: relative;
      z-index: 10;
    }

    /* Glitch Text */
    .glitch {
      position: relative;
      font-weight: bold;
      color: #00e0d6; /* cyan lebih soft */
      text-transform: uppercase;
    }
    .glitch::before,
    .glitch::after {
      content: attr(data-text);
      position: absolute;
      left: 0;
      width: 100%;
      overflow: hidden;
      clip: rect(0, 900px, 0, 0);
    }
    .glitch::before {
      animation: glitchTop 2s infinite linear alternate-reverse;
      color: #ff4dc8; /* pink redup */
    }
    .glitch::after {
      animation: glitchBottom 1.5s infinite linear alternate-reverse;
      color: #3cff3c; /* hijau lebih kalem */
    }
    @keyframes glitchTop {
      0% { clip: rect(0, 9999px, 0, 0); }
      25% { clip: rect(0, 9999px, 5px, 0); transform: translate(-2px, -2px);}
      50% { clip: rect(0, 9999px, 0, 0); }
      75% { clip: rect(0, 9999px, 3px, 0); transform: translate(1px, -1px);}
      100% { clip: rect(0, 9999px, 0, 0); }
    }
    @keyframes glitchBottom {
      0% { clip: rect(0, 9999px, 0, 0); }
      25% { clip: rect(5px, 9999px, 9999px, 0); transform: translate(1px, 1px);}
      50% { clip: rect(0, 9999px, 0, 0); }
      75% { clip: rect(3px, 9999px, 9999px, 0); transform: translate(-1px, 1px);}
      100% { clip: rect(0, 9999px, 0, 0); }
    }

    /* Card */
    .card {
      border: 1px solid #00e0d6; /* cyan lembut */
      border-radius: 0.5rem;
      padding: 1rem;
      background: rgba(17, 25, 40, 0.85);
      transition: all 0.3s ease-in-out;
    }
    .card:hover {
      transform: scale(1.02);
      box-shadow: 0 0 8px #00e0d6; /* glow halus */
    }

    /* Matrix Rain */
    canvas#matrix {
      position: fixed;
      top: 0;
      left: 0;
      z-index: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      opacity: 0.15; /* lebih redup */
    }
  </style>
</head>
<body>
  <canvas id="matrix"></canvas>

  <div class="container">
    <header class="text-center mb-6">
      <h1 class="glitch text-xl" data-text="Kenzo — Ethical Hacker">Kenzo — Ethical Hacker</h1>
      <p class="text-sm text-cyan-400">Security Researcher & Pentester</p>
    </header>

    <section class="card mb-4">
      <h2 class="text-base mb-2">About Me</h2>
      <p class="text-sm">Saya Kenzo, fokus dalam ethical hacking & keamanan siber. Misi saya adalah mengamankan sistem, memburu celah, & berbagi ilmu.</p>
    </section>

    <section class="mb-4">
      <h2 class="text-base mb-2">Skills</h2>
      <div class="space-y-2">
        <div class="card">Web App Pentesting ⭐⭐⭐⭐⭐</div>
        <div class="card">API Security ⭐⭐⭐⭐☆</div>
        <div class="card">Network Hardening ⭐⭐⭐⭐☆</div>
        <div class="card">Reverse Engineering ⭐⭐⭐☆☆</div>
        <div class="card">OSINT & Threat Intel ⭐⭐⭐⭐⭐</div>
      </div>
    </section>

    <section class="mb-4">
      <h2 class="text-base mb-2">Projects</h2>
      <div class="space-y-2">
        <div class="card">Enterprise Audit ⭐⭐⭐⭐⭐</div>
        <div class="card">Cloud Infra Review ⭐⭐⭐⭐☆</div>
        <div class="card">Bug Bounty Findings ⭐⭐⭐⭐⭐</div>
        <div class="card">API Security Hardening ⭐⭐⭐⭐☆</div>
      </div>
    </section>

    <footer class="mt-6 text-center text-[12px] text-cyan-400">
      <p class="mb-2">📧 <a href="mailto:pykcyber@gmail.com" class="underline">pykcyber@gmail.com</a></p>
      <p class="mb-2">📱 <a href="https://wa.me/6283143490913" target="_blank" class="underline">+62 831-4349-0913</a></p>
      <p class="text-[10px] mt-4">© 2025 Kenzo — Semua hak cipta dilindungi.</p>
    </footer>
  </div>

  <script>
    // MATRIX RAIN
    const canvas = document.getElementById("matrix");
    const ctx = canvas.getContext("2d");

    canvas.height = window.innerHeight;
    canvas.width = window.innerWidth;

    const chars = "01";
    const fontSize = 14;
    const columns = canvas.width / fontSize;
    const drops = [];

    for (let x = 0; x < columns; x++) drops[x] = 1;

    function draw() {
      ctx.fillStyle = "rgba(0, 0, 0, 0.05)";
      ctx.fillRect(0, 0, canvas.width, canvas.height);

      ctx.fillStyle = "#3cff3c"; // hijau lebih kalem
      ctx.font = fontSize + "px monospace";

      for (let i = 0; i < drops.length; i++) {
        const text = chars.charAt(Math.floor(Math.random() * chars.length));
        ctx.fillText(text, i * fontSize, drops[i] * fontSize);

        if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) {
          drops[i] = 0;
        }
        drops[i]++;
      }
    }

    setInterval(draw, 40);

    window.addEventListener("resize", () => {
      canvas.height = window.innerHeight;
      canvas.width = window.innerWidth;
    });
  </script>
</body>
</html>
