# HappyBirthday
<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="content-type" content="text/html; charset=utf-8" />
    <title>Happy Birthday</title>
    <style>
      /* Reset */
      * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
      }

      /* Background with lotus/snow theme */
      body {
        min-height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        background: linear-gradient(135deg, #f8e8ee 0%, #fdf6f9 50%, #e8f4f8 100%);
        font-family: "Georgia", serif;
        color: #444;
        position: relative;
        overflow-x: hidden;
      }

      /* Optional: Add background pattern */
      body::before {
        content: '';
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-image: 
          radial-gradient(circle at 20% 30%, rgba(255, 182, 193, 0.1) 0%, transparent 50%),
          radial-gradient(circle at 80% 70%, rgba(176, 224, 230, 0.1) 0%, transparent 50%);
        z-index: -1;
        pointer-events: none;
      }

      /* Book Cover Wrapper */
      .book-wrapper {
        perspective: 2000px;
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        z-index: 10000;
        transition: opacity 0.5s ease;
      }

      .book-wrapper.hidden {
        opacity: 0;
        pointer-events: none;
      }

      /* Book Container */
      .book {
        width: 400px;
        height: 550px;
        position: relative;
        transform-style: preserve-3d;
      }

      /* Book Cover (Front Page) */
      .book-cover {
        position: absolute;
        width: 100%;
        height: 100%;
        background: linear-gradient(135deg, #f8d7e8 0%, #e8c4d8 100%);
        border-radius: 0 15px 15px 0;
        transform-origin: left center;
        transition: transform 1.5s ease;
        cursor: pointer;
        box-shadow: 
          5px 5px 20px rgba(0, 0, 0, 0.3),
          inset -5px 0 15px rgba(0, 0, 0, 0.1);
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        padding: 40px;
        text-align: center;
        border-left: 8px solid #c97c98;
      }

      .book-cover.open {
        transform: rotateY(-180deg);
      }

      /* Book Cover Content */
      .book-cover h2 {
        font-size: 42px;
        color: #c97c98;
        margin-bottom: 20px;
        text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
      }

      .book-cover p {
        font-size: 18px;
        color: #888;
        margin-bottom: 40px;
        font-style: italic;
      }

      .book-cover .decorations {
        font-size: 50px;
        margin-bottom: 30px;
        animation: float 3s ease-in-out infinite;
      }

      .book-cover .tap-hint {
        font-size: 16px;
        color: #c97c98;
        margin-top: 30px;
        animation: pulse 2s ease-in-out infinite;
        background: rgba(255, 255, 255, 0.5);
        padding: 12px 25px;
        border-radius: 25px;
        border: 2px solid rgba(201, 124, 152, 0.3);
      }

      @keyframes float {
        0%, 100% {
          transform: translateY(0px);
        }
        50% {
          transform: translateY(-10px);
        }
      }

      @keyframes pulse {
        0%, 100% {
          transform: scale(1);
          opacity: 1;
        }
        50% {
          transform: scale(1.05);
          opacity: 0.8;
        }
      }

      /* Book Back (Base) */
      .book-back {
        position: absolute;
        width: 100%;
        height: 100%;
        background: linear-gradient(135deg, #e8c4d8 0%, #d4b4c8 100%);
        border-radius: 15px 0 0 15px;
        box-shadow: -5px 5px 20px rgba(0, 0, 0, 0.3);
        border-right: 8px solid #c97c98;
      }

      /* Book Spine */
      .book-spine {
        position: absolute;
        left: -8px;
        top: 0;
        width: 8px;
        height: 100%;
        background: linear-gradient(to bottom, #c97c98 0%, #b86b88 100%);
        border-radius: 3px 0 0 3px;
      }

      /* Main Card - Initially hidden */
      .container {
        text-align: center;
        background: rgba(255, 255, 255, 0.95);
        padding: 50px 40px;
        border-radius: 25px;
        box-shadow: 0 15px 50px rgba(0, 0, 0, 0.1);
        max-width: 600px;
        animation: fadeIn 1.5s ease;
        backdrop-filter: blur(10px);
        border: 1px solid rgba(255, 255, 255, 0.8);
        opacity: 0;
        transition: opacity 1s ease;
      }

      .container.visible {
        opacity: 1;
      }

      /* Name Title */
      h1 {
        font-size: 42px;
        margin-bottom: 10px;
        color: #c97c98;
        letter-spacing: 2px;
        text-shadow: 0 2px 4px rgba(201, 124, 152, 0.2);
      }

      /* Subtitle */
      .subtitle {
        font-size: 20px;
        color: #8aaab4;
        margin-bottom: 30px;
        font-weight: 300;
      }

      /* Message text */
      .message {
        font-size: 17px;
        line-height: 1.8;
        margin-bottom: 25px;
        color: #555;
      }

      /* Closing line */
      .closing {
        font-style: italic;
        color: #888;
        margin-top: 20px;
        margin-bottom: 30px;
        font-size: 15px;
      }

      /* Cake Container */
      .cake-container {
        margin: 30px auto 20px;
        animation: fadeInUp 2s ease;
      }

      .cake {
        width: 180px;
        height: 160px;
        margin: 0 auto 25px;
        position: relative;
      }

      /* Candle */
      .candle {
        width: 12px;
        height: 50px;
        background: linear-gradient(to bottom, #f8b4d0 0%, #e89bb8 50%, #d686a3 100%);
        margin: 0 auto;
        border-radius: 6px 6px 0 0;
        position: relative;
        box-shadow: 0 0 8px rgba(0, 0, 0, 0.15);
      }

      /* Wick */
      .wick {
        width: 2px;
        height: 10px;
        background: #555;
        margin: 0 auto;
        position: relative;
        top: -2px;
      }

      /* Flame */
      .flame {
        width: 18px;
        height: 28px;
        background: radial-gradient(ellipse at center, #fff 0%, #ffe4b3 20%, #ffb380 50%, #ff9a7a 80%);
        border-radius: 50% 50% 50% 50% / 60% 60% 40% 40%;
        position: absolute;
        top: -28px;
        left: 50%;
        transform: translateX(-50%);
        animation: flicker 0.2s infinite alternate;
        box-shadow: 0 0 15px #ffb380, 0 0 30px #ff9a7a;
        transition: opacity 0.5s ease, transform 0.5s ease;
      }

      .flame.blown {
        opacity: 0;
        transform: translateX(-50%) translateY(-20px) scale(0);
      }

      /* Smoke after blowing */
      .smoke {
        position: absolute;
        top: -10px;
        left: 50%;
        transform: translateX(-50%);
        opacity: 0;
      }

      .smoke.active {
        animation: smokeRise 2s ease-out forwards;
      }

      .smoke span {
        display: block;
        width: 8px;
        height: 8px;
        background: rgba(180, 180, 180, 0.6);
        border-radius: 50%;
        margin-bottom: 4px;
      }

      @keyframes smokeRise {
        0% {
          opacity: 0.7;
          transform: translateX(-50%) translateY(0);
        }
        100% {
          opacity: 0;
          transform: translateX(-50%) translateY(-50px) scale(1.8);
        }
      }

      @keyframes flicker {
        0% {
          transform: translateX(-50%) scaleY(1) scaleX(1);
        }
        100% {
          transform: translateX(-50%) scaleY(1.05) scaleX(0.95);
        }
      }

      /* Cake base - Lotus/Snow theme */
      .cake-base {
        width: 180px;
        height: 100px;
        background: linear-gradient(to bottom, #f8d7e8 0%, #f0c4d8 100%);
        border-radius: 15px 15px 35px 35px;
        position: relative;
        box-shadow: 0 8px 25px rgba(201, 124, 152, 0.3);
        margin-top: 10px;
      }

      .cake-base::before {
        content: '';
        position: absolute;
        top: 8px;
        left: 10%;
        width: 80%;
        height: 12px;
        background: rgba(255, 255, 255, 0.5);
        border-radius: 8px;
      }

      /* Cake decorations - snow/lotus dots */
      .cake-base::after {
        content: '✿ ❄ ✿';
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        color: rgba(255, 255, 255, 0.7);
        font-size: 20px;
        letter-spacing: 15px;
      }

      .frosting {
        position: absolute;
        bottom: -8px;
        left: 0;
        width: 100%;
        height: 18px;
        background: linear-gradient(to right, #b0dce8, #c8e4ec, #b0dce8);
        border-radius: 0 0 35px 35px;
      }

      /* Button with lotus/snow colors */
      button {
        margin-top: 15px;
        padding: 14px 35px;
        border: none;
        border-radius: 30px;
        background: linear-gradient(135deg, #f8d7e8 0%, #c8e4ec 100%);
        color: #666;
        font-size: 16px;
        cursor: pointer;
        transition: all 0.3s ease;
        font-weight: 600;
        box-shadow: 0 4px 15px rgba(201, 124, 152, 0.3);
        letter-spacing: 0.5px;
      }

      button:hover {
        transform: translateY(-2px);
        box-shadow: 0 6px 20px rgba(201, 124, 152, 0.4);
        background: linear-gradient(135deg, #f0c4d8 0%, #b0dce8 100%);
      }

      button:disabled {
        background: #ddd;
        cursor: not-allowed;
        box-shadow: none;
      }

      /* Party Popper */
      .confetti {
        position: fixed;
        width: 10px;
        height: 10px;
        pointer-events: none;
        z-index: 9999;
      }

      @keyframes confettiFall {
        0% {
          transform: translateY(0) rotate(0deg);
          opacity: 1;
        }
        100% {
          transform: translateY(100vh) rotate(720deg);
          opacity: 0;
        }
      }

      /* Modal styles - Lotus/Snow theme */
      .modal {
        display: none;
        position: fixed;
        z-index: 10001;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.6);
        backdrop-filter: blur(8px);
        animation: fadeIn 0.3s ease;
      }

      .modal-content {
        position: relative;
        background: linear-gradient(135deg, #f8d7e8 0%, #f0e8f8 50%, #c8e4ec 100%);
        color: #555;
        margin: 8% auto;
        padding: 45px 40px;
        border-radius: 25px;
        width: 85%;
        max-width: 500px;
        box-shadow: 0 15px 60px rgba(0, 0, 0, 0.3);
        animation: slideDown 0.5s ease;
        text-align: center;
        border: 2px solid rgba(255, 255, 255, 0.5);
      }

      .close {
        position: absolute;
        right: 20px;
        top: 15px;
        font-size: 32px;
        font-weight: 300;
        color: #888;
        cursor: pointer;
        transition: all 0.3s;
        line-height: 1;
      }

      .close:hover {
        transform: rotate(90deg);
        color: #c97c98;
      }

      .modal-message {
        font-size: 17px;
        line-height: 1.8;
        margin-top: 20px;
        color: #555;
      }

      .modal h2 {
        font-size: 2.2em;
        margin-bottom: 15px;
        color: #c97c98;
        text-shadow: 0 2px 4px rgba(201, 124, 152, 0.2);
      }

      /* Fade Animation */
      @keyframes fadeIn {
        from {
          opacity: 0;
        }
        to {
          opacity: 1;
        }
      }

      @keyframes fadeInUp {
        from {
          opacity: 0;
          transform: translateY(20px);
        }
        to {
          opacity: 1;
          transform: translateY(0);
        }
      }

      @keyframes slideDown {
        from {
          transform: translateY(-50px) scale(0.9);
          opacity: 0;
        }
        to {
          transform: translateY(0) scale(1);
          opacity: 1;
        }
      }

      /* Responsive */
      @media (max-width: 600px) {
        .book {
          width: 320px;
          height: 450px;
        }

        .book-cover h2 {
          font-size: 32px;
        }

        .book-cover p {
          font-size: 16px;
        }

        .container {
          padding: 35px 25px;
          margin: 20px;
        }

        h1 {
          font-size: 32px;
        }

        .subtitle {
          font-size: 16px;
        }

        .message {
          font-size: 15px;
        }

        .cake {
          width: 150px;
          height: 140px;
        }

        .cake-base {
          width: 150px;
          height: 90px;
        }
      }
    </style>
  </head>
  <body>
    <!-- Book Cover Animation -->
    <div class="book-wrapper" id="bookWrapper">
      <div class="book">
        <div class="book-back">
          <div class="book-spine"></div>
        </div>
        <div class="book-cover" id="bookCover" onclick="openBook()">
          <div class="decorations">✿ ❄ ✿</div>
          <h2>A Special Day</h2>
          <p>For Someone Special</p>
          <div class="tap-hint">👆 Tap to Open</div>
        </div>
      </div>
    </div>

    <!-- Main Birthday Card Content -->
    <div class="container" id="mainContent">
      <h1>Her Name</h1>
      <div class="subtitle">Happy Birthday ✨</div>
      <div class="message">
        Today is special — not just because it's your birthday, but because it's the day someone truly wonderful came into this world.
        I hope you realize how rare you are… the way you smile, the way you care, the way your presence can quietly brighten someone's day without you even trying.
        Even on ordinary days, you shine in ways you probably don't notice yourself. And honestly, I feel lucky just knowing you exist in the same world as me.
        So today, I wish you peace in your heart, warmth in your days, and dreams that come true gently, one by one.
        Happy Birthday — may life always be soft with you.🍓🍰💚
      </div>
      <div class="closing">
        — from someone who's really glad you exist
      </div>

      <!-- Cake with Candle -->
      <div class="cake-container">
        <div class="cake">
          <div class="candle">
            <div class="wick"></div>
            <div class="flame" id="flame"></div>
            <div class="smoke" id="smoke">
              <span></span>
              <span></span>
              <span></span>
            </div>
          </div>
          <div class="cake-base">
            <div class="frosting"></div>
          </div>
        </div>
        <button id="wishButton" onclick="makeWish()">Make a Wish 🕯️</button>
      </div>
    </div>

    <!-- Modal with Birthday Wish -->
    <div id="myModal" class="modal">
      <div class="modal-content">
        <span class="close" onclick="closeMessage()">&times;</span>
        <h2>✿ Your Wish ❄</h2>
        <div class="modal-message">
          <strong>May this year bring you...</strong><br><br>
          
          Moments of pure joy that take your breath away ✨<br>
          Laughter that makes your cheeks hurt 😊<br>
          Dreams that unfold gently, one by one 🌸<br>
          Peace in your heart, always 💕<br>
          Love that surrounds you like snowflakes ❄️<br>
          And the quiet knowledge that you are cherished 🍓<br><br>
          
          <em>Happy Birthday, beautiful soul.<br>
          The world is brighter with you in it.</em> 💚
        </div>
      </div>
    </div>

    <script>
      let wishMade = false;

      // Book opening function
      function openBook() {
        const bookCover = document.getElementById('bookCover');
        const bookWrapper = document.getElementById('bookWrapper');
        const mainContent = document.getElementById('mainContent');

        // Open the book cover
        bookCover.classList.add('open');

        // After animation, hide book and show content
        setTimeout(() => {
          bookWrapper.classList.add('hidden');
          mainContent.classList.add('visible');
        }, 1500);
      }

      function makeWish() {
        if (wishMade) return;
        
        wishMade = true;
        const flame = document.getElementById('flame');
        const smoke = document.getElementById('smoke');
        const button = document.getElementById('wishButton');
        
        // Blow out the candle
        flame.classList.add('blown');
        
        // Show smoke
        setTimeout(() => {
          smoke.classList.add('active');
        }, 300);
        
        // Create party popper effect
        setTimeout(() => {
          createConfetti();
          showMessage();
        }, 800);
        
        // Disable button
        button.disabled = true;
        button.textContent = 'Wish Made! ✿';
      }

      function createConfetti() {
        // Lotus & Snow color palette
        const colors = ['#f8d7e8', '#c8e4ec', '#f0c4d8', '#b0dce8', '#e8c4d8', '#d4e8f0', '#f8b4d0', '#a8d8e8'];
        const confettiCount = 80;
        
        for (let i = 0; i < confettiCount; i++) {
          setTimeout(() => {
            const confetti = document.createElement('div');
            confetti.className = 'confetti';
            confetti.style.left = Math.random() * 100 + '%';
            confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
            confetti.style.animation = `confettiFall ${2 + Math.random() * 2}s linear forwards`;
            confetti.style.animationDelay = Math.random() * 0.5 + 's';
            
            // Random shapes (circles and squares)
            if (Math.random() > 0.5) {
              confetti.style.borderRadius = '50%';
            }
            
            // Add some lotus flower symbols
            if (Math.random() > 0.8) {
              confetti.textContent = '✿';
              confetti.style.fontSize = '16px';
              confetti.style.width = 'auto';
              confetti.style.height = 'auto';
            }
            
            // Add some snowflakes
            if (Math.random() > 0.85) {
              confetti.textContent = '❄';
              confetti.style.fontSize = '14px';
              confetti.style.width = 'auto';
              confetti.style.height = 'auto';
            }
            
            document.body.appendChild(confetti);
            
            // Remove after animation
            setTimeout(() => {
              confetti.remove();
            }, 4500);
          }, i * 15);
        }
      }

      function showMessage() {
        document.getElementById('myModal').style.display = 'block';
      }

      function closeMessage() {
        document.getElementById('myModal').style.display = 'none';
      }

      // Close modal when clicking outside of it
      window.onclick = function(event) {
        const modal = document.getElementById('myModal');
        if (event.target == modal) {
          modal.style.display = 'none';
        }
      }
    </script>
  </body>
</html>
