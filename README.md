<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>До нашей даты</title>
  <style>
    :root {
      --background: #170d25;
      --background-light: #2b1640;
      --pink: #ff78bd;
      --pink-light: #ffd0e7;
      --text: #fff8fc;
      --muted: #d9bfd0;
      --gold: #ffd166;
    }

    * {
      box-sizing: border-box;
    }

    body {
      min-height: 100vh;
      margin: 0;
      display: grid;
      place-items: center;
      padding: 24px;
      overflow: hidden;
      color: var(--text);
      font-family: Georgia, "Times New Roman", serif;
      background:
        radial-gradient(circle at 15% 20%, rgba(255, 120, 189, 0.2), transparent 30%),
        radial-gradient(circle at 85% 80%, rgba(255, 209, 102, 0.12), transparent 28%),
        linear-gradient(145deg, var(--background), var(--background-light));
    }

    .page {
      width: min(900px, 100%);
      text-align: center;
      position: relative;
      z-index: 1;
    }

    .heart {
      color: var(--pink);
      font-size: 2rem;
      animation: pulse 1.8s ease-in-out infinite;
    }

    h1 {
      margin: 16px 0 10px;
      font-size: clamp(2.4rem, 8vw, 5.8rem);
      line-height: 0.98;
      font-weight: 400;
    }

    .subtitle {
      max-width: 600px;
      margin: 0 auto 42px;
      color: var(--muted);
      font-size: clamp(1rem, 2.5vw, 1.35rem);
      line-height: 1.6;
    }

    .countdown {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 14px;
    }

    .unit {
      min-width: 0;
      padding: 24px 12px;
      border: 1px solid rgba(255, 255, 255, 0.16);
      border-radius: 18px;
      background: rgba(255, 255, 255, 0.08);
      box-shadow: 0 18px 45px rgba(0, 0, 0, 0.22);
      backdrop-filter: blur(8px);
    }

    .number {
      display: block;
      color: var(--pink-light);
      font-family: Georgia, "Times New Roman", serif;
      font-size: clamp(2.2rem, 8vw, 5rem);
      line-height: 1;
    }

    .label {
      display: block;
      margin-top: 10px;
      color: var(--muted);
      font-size: 0.9rem;
      text-transform: uppercase;
      letter-spacing: 0.12em;
    }

    .date {
      margin-top: 34px;
      color: var(--gold);
      font-size: 1.05rem;
      letter-spacing: 0.08em;
    }

    .finished {
      display: none;
      color: var(--pink-light);
      font-size: clamp(1.8rem, 5vw, 3.5rem);
    }

    @keyframes pulse {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.15); }
    }

    @media (max-width: 560px) {
      .countdown {
        grid-template-columns: repeat(2, 1fr);
      }

      .subtitle {
        margin-bottom: 30px;
      }
    }
  </style>
</head>
<body>
  <main class="page">
    <div class="heart">♥</div>
    <h1>Денис и Лерочка</h1>
    <p class="subtitle">До нашей особенной даты осталось совсем немного</p>

    <div class="countdown" id="countdown">
      <div class="unit">
        <span class="number" id="days">00</span>
        <span class="label">дней</span>
      </div>
      <div class="unit">
        <span class="number" id="hours">00</span>
        <span class="label">часов</span>
      </div>
      <div class="unit">
        <span class="number" id="minutes">00</span>
        <span class="label">минут</span>
      </div>
      <div class="unit">
        <span class="number" id="seconds">00</span>
        <span class="label">секунд</span>
      </div>
    </div>

    <div class="finished" id="finished">С нашей датой, любимая Лерочка! ♥</div>
    <div class="date">14 октября 2026 года</div>
  </main>

  <script>
    // Отсчёт до начала 14 октября 2026 года по московскому времени.
    const targetDate = new Date("2026-10-14T00:00:00+03:00").getTime();
    const countdown = document.getElementById("countdown");
    const finished = document.getElementById("finished");

    function updateCountdown() {
      const difference = targetDate - Date.now();

      if (difference <= 0) {
        countdown.style.display = "none";
        finished.style.display = "block";
        return;
      }

      const days = Math.floor(difference / (1000 * 60 * 60 * 24));
      const hours = Math.floor((difference / (1000 * 60 * 60)) % 24);
      const minutes = Math.floor((difference / (1000 * 60)) % 60);
      const seconds = Math.floor((difference / 1000) % 60);

      document.getElementById("days").textContent = String(days).padStart(2, "0");
      document.getElementById("hours").textContent = String(hours).padStart(2, "0");
      document.getElementById("minutes").textContent = String(minutes).padStart(2, "0");
      document.getElementById("seconds").textContent = String(seconds).padStart(2, "0");
    }

    updateCountdown();
    setInterval(updateCountdown, 1000);
  </script>
</body>
</html>
