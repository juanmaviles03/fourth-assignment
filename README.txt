<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Quiz App</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap" rel="stylesheet">
  <style>
    :root {
      --brand: #2563eb;
      --brand-hover: #1e40af;
      --correct: #16a34a;
      --wrong: #dc2626;
      --text: #1f2937;
      --muted: #6b7280;
      --card-bg: #ffffff;
      --bg: #f3f4f6;
    }
    * { box-sizing: border-box; }

    body {
      font-family: 'Inter', system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
      background: var(--bg);
      color: var(--text);
      margin: 0;
      padding: 24px;
      display: grid;
      place-items: center;
      min-height: 100dvh;
    }

    #quiz-box {
      width: 100%;
      max-width: 560px;
      background: var(--card-bg);
      border-radius: 14px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.07);
      padding: 24px;
    }

    #question {
      font-size: 1.25rem;
      line-height: 1.4;
      margin: 0 0 18px 0;
      font-weight: 600;
    }

    #answer-buttons {
      text-align: left;          /* left-align the group */
      padding-left: 4px;         /* slight indent */
      margin-bottom: 16px;
    }

    .btn {
      display: block;
      width: 100%;               /* equal width buttons */
      max-width: 340px;          /* limit width */
      margin: 10px 0;
      padding: 12px 16px;
      border: 1px solid #e5e7eb;
      border-radius: 10px;
      background: #fff;
      text-align: left;          /* left-align label */
      cursor: pointer;
      font-size: 1rem;
      transition:
        background-color .2s ease,
        border-color .2s ease,
        transform .06s ease;
    }
    .btn:hover:not(:disabled) {
      border-color: var(--brand);
      background: #f8fafc;
    }
    .btn:active:not(:disabled) { transform: scale(0.99); }
    .btn:disabled { cursor: not-allowed; opacity: .9; }

    /* Correct/Wrong states added via classList */
    .correct {
      background: #ecfdf5;
      border-color: var(--correct);
      color: #065f46;
    }
    .wrong {
      background: #fef2f2;
      border-color: var(--wrong);
      color: #7f1d1d;
    }

    /* Focus visibility for keyboard users */
    .btn:focus-visible,
    #next-btn:focus-visible {
      outline: 3px solid var(--brand);
      outline-offset: 2px;
    }

    #next-btn {
      display: none; /* shown dynamically */
      padding: 12px 18px;
      background: var(--brand);
      color: #fff;
      border: none;
      border-radius: 10px;
      font-size: 1rem;
      cursor: pointer;
      transition: background-color .2s ease;
    }
    #next-btn:hover { background: var(--brand-hover); }

    .muted {
      color: var(--muted);
      margin-top: 8px;
      font-size: .95rem;
    }
  </style>
</head>
<body>
  <div id="quiz-box" role="region" aria-labelledby="question">
    <h2 id="question">Question text</h2>
    <div id="answer-buttons" aria-live="polite"></div>
    <button id="next-btn" type="button" data-action="next">Next</button>
    <div class="muted" id="progress"></div>
  </div>

  <script src="script.js"></script>
</body>
</html>