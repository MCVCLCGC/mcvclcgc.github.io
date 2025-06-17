<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Only For My First Love 💌</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      height: 100vh;
      overflow: hidden;
      background: linear-gradient(135deg, #ffdde1, #fcb69f, #ffecd2, #fcbad3);
      background-size: 400% 400%;
      animation: gradient 15s ease infinite;
      font-family: 'Georgia', serif;
      display: flex;
      justify-content: center;
      align-items: center;
      text-align: center;
      color: #3c003c;
      position: relative;
      transition: background 0.5s ease;
    }
    @keyframes gradient {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }

    .container, .slideshow-container {
      max-width: 90%;
      background: rgba(255, 255, 255, 0.3);
      padding: 20px;
      border-radius: 20px;
      box-shadow: 0 0 25px #ffb3c6;
      backdrop-filter: blur(10px);
      animation: slideDown 1.8s ease-out forwards;
      opacity: 0;
      transform: translateY(-100vh);
      position: relative;
    }

    .hidden { display: none; }

    @keyframes slideDown {
      to {
        transform: translateY(0);
        opacity: 1;
      }
    }

    #heart {
      font-size: 3.5rem;
      animation: pulse 1.5s infinite;
      color: #ff4d6d;
      text-shadow: 0 0 15px #ff4d6d;
    }
    @keyframes pulse {
      0%,100% { transform: scale(1); }
      50% { transform: scale(1.3); }
    }

    #message {
      margin-top: 20px;
      font-size: 1.1rem;
      line-height: 1.6;
      white-space: pre-wrap;
      min-height: 140px;
    }

    #highlight {
      display: inline-block;
      margin-top: 15px;
      font-weight: bold;
      color: #ff3366;
      font-size: 1.3rem;
      background: rgba(255,255,255,0.6);
      padding: 6px 12px;
      border-radius: 12px;
      box-shadow: 0 0 8px #ffcce0;
      min-height: 30px;
    }

    .button-container {
      margin-top: 25px;
      display: flex;
      justify-content: center;
      gap: 15px;
      flex-wrap: wrap;
    }

    .btn {
      padding: 12px 24px;
      font-size: 1rem;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      position: relative;
      transition: background-color 0.3s;
    }

    .yes {
      background-color: #ff4d6d;
      color: white;
    }

    .yes:hover { background-color: #e8435f; }

    .no {
      background-color: #ff4d6d;
      color: #ffffff;
      position: relative;
      pointer-events: auto;
    }

    .no::after {
      content: "Please Don't 😭";
      position: absolute;
      bottom: -28px;
      left: 50%;
      transform: translateX(-50%);
      background: #ff4d6d;
      color: white;
      padding: 4px 10px;
      border-radius: 5px;
      font-size: 0.8rem;
      opacity: 0;
      transition: opacity 0.3s ease;
      white-space: nowrap;
      z-index: 3;
    }

    .no:hover::after,
    .no:active::after,
    .no:focus::after {
      opacity: 1;
    }

    .sad-overlay {
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background: rgba(30, 30, 50, 0.7);
      display: none;
      justify-content: center;
      align-items: center;
      text-align: center;
      font-size: 1.5rem;
      font-weight: bold;
      color: white;
      z-index: 1000;
      flex-direction: column;
    }

    .slideshow-container {
      display: none;
      flex-direction: column;
      align-items: center;
      text-align: center;
    }

    .slideshow-container img {
      width: 100%;
      max-height: 60vh;
      object-fit: contain;
      border-radius: 12px;
      margin-bottom: 15px;
      display: none;
    }

    .slideshow-container img.active {
      display: block;
    }

    .caption {
      font-weight: bold;
      color: #6d003c;
      font-size: 1.1rem;
    }

    .controls {
      margin-top: 15px;
      display: flex;
      justify-content: center;
      gap: 20px;
    }

    .controls button {
      background: rgba(255,255,255,0.3);
      border: none;
      padding: 10px 20px;
      border-radius: 8px;
      color: #3c003c;
      cursor: pointer;
    }

    .controls button:hover {
      background: rgba(255,255,255,0.5);
    }
  </style>
</head>
<body>

  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>

  <div class="sad-overlay" id="sadOverlay">
    <div>💔 I’ll always wait for you. 💖</div>
  </div>

  <div class="container" id="proposalBox">
    <div id="heart">❤️</div>
    <div id="message">Loading...</div>
    <div id="highlight"></div>

    <div class="button-container">
      <button class="btn yes" onclick="startSlideshow()">Yes 😳</button>
      <button class="btn no" onclick="disabled">No 😅</button>
    </div>
  </div>

  <div class="slideshow-container container hidden" id="slideshowBox">
    <img src="img1.jpg" />
    <img src="photo2.png" />
    <img src="Dpt46.png" />
    <div class="caption" id="caption">Your Smile 🌸</div>
    <div class="controls">
      <button onclick="prevSlide()">◀️ Prev</button>
      <button onclick="nextSlide()">Next ▶️</button>
    </div>
  </div>

  <script>
    const messageDiv = document.getElementById("message");
    const highlightDiv = document.getElementById("highlight");
    const sadOverlay = document.getElementById("sadOverlay");

    const poem = `Hey Dipsina 👀,
If stars could speak, they’d whisper your name—
the only word that sets my sky aflame.
I don’t need forever, just your hand in mine—
say yes, and turn this breath into rhyme. 💖`;

    const proposal = `Will you be mine forever? 💍`;

    let i = 0;
    function typeWriterMain(text, el, cb) {
      if (i < text.length) {
        el.innerHTML = text.slice(0, i + 1).replace(/\n/g, "<br>");
        i++;
        setTimeout(() => typeWriterMain(text, el, cb), 40);
      } else if (cb) {
        setTimeout(cb, 500);
      }
    }

    function startSlideshow() {
      confetti({ particleCount: 600, spread: 360, origin: { y: 0.5 } });

      document.getElementById("proposalBox").classList.add("hidden");
      const slideshow = document.getElementById("slideshowBox");
      slideshow.classList.remove("hidden");
      slideshow.style.display = "flex";

      showSlide(0);
    }

    function sadMode() {
      sadOverlay.style.display = "flex";
      document.body.style.background = "#444";
      setTimeout(() => {
        sadOverlay.style.display = "none";
        document.body.style.background = "";
      }, 3000);
    }

    const slides = document.querySelectorAll("#slideshowBox img");
    const captions = ["Your Smile 🌸", "My Life 😄", "Forever Begins Here 💍"];
    const caption = document.getElementById("caption");
    let current = 0;

    function showSlide(index) {
      slides.forEach((img, i) => {
        img.classList.toggle("active", i === index);
      });
      caption.textContent = captions[index];
    }

    function nextSlide() {
      current = (current + 1) % slides.length;
      showSlide(current);
    }

    function prevSlide() {
      current = (current - 1 + slides.length) % slides.length;
      showSlide(current);
    }

    setInterval(() => {
      if (!document.getElementById("slideshowBox").classList.contains("hidden")) {
        nextSlide();
      }
    }, 5000);

    window.onload = () => {
      typeWriterMain(poem, messageDiv, () => {
        i = 0;
        typeWriterMain(proposal, highlightDiv);
      });
    };
  </script>
</body>
</html>
