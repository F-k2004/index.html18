<!DOCTYPE html>
<html lang="fa">
<head>
  <meta charset="UTF-8" />
  <title>🧠 بازی حافظه</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <style>
    body {
      margin: 0;
      direction: rtl;
      font-family: sans-serif;
      background: #222;
      olor: #fff;
      text-align: center;
      padding-top: 20px;
    }

    h1 {
      font-weight: 300;
    }

    #game {
      width: 90%;
      max-width: 480px;
      margin: 40px auto;
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 12px;
    }

    .card {
      width: 100%;
      aspect-ratio: 1/1;
      background: #444;
      border-radius: 10px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 32px;
      cursor: pointer;
      transition: transform 0.4s;
      user-select: none;
    }

    .card.revealed {
      background: #00e676;
      transform: rotateY(180deg);
    }

    .card.matched {
      background: #0091ea;
      opacity: 0.6;
      cursor: default;
    }
  </style>
</head>
<body>

  <h1>🧠 بازی تقویت حافظه</h1>
  <p>روی کارت‌ها کلیک کن و جفت‌ها را پیدا کن!</p>

  <div id="game"></div>

  <script>
    const emojis = ["🍎","🍌","🍇","🍓","🍒","🍉","🍍","🥝"];
    let cards = [...emojis, ...emojis].sort(() => Math.random() - 0.5);

    const game = document.getElementById("game");

    cards.forEach((e) => {
      const card = document.createElement("div");
      card.classList.add("card");
      card.dataset.emoji = e;
      card.addEventListener("click", reveal);
      game.appendChild(card);
    });

    let first = null;
    let lock = false;

    function reveal() {
      if (lock) return;
      if (this.classList.contains("revealed")) return;

      this.classList.add("revealed");
      this.textContent = this.dataset.emoji;

      if (!first) {
        first = this;
      } else {
        lock = true;
        if (first.dataset.emoji === this.dataset.emoji) {
          first.classList.add("matched");
          this.classList.add("matched");
          first = null;
          lock = false;
        } else {
          setTimeout(() => {
            first.classList.remove("revealed");
            first.textContent = "";
            this.classList.remove("revealed");
            this.textContent = "";
            first = null;
            lock = false;
          }, 700);
        }
      }
    }
  </script>

</body>
</html>
