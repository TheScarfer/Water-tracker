<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title> Droplet-- Water Tracker 💧</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@500;700&display=swap');

        body {
            font-family: 'Playfair Display', serif;
            background: #dceef2;
            color: #000303;
            text-align: center;
            padding: 40px 20px;
            margin: 0;
        }

        .main-title {
            font-size: 3.2em;
            color: #00090d;
            font-weight: 700;
            letter-spacing: 1px;
            text-shadow: 1px 2px 3px rgba(0, 0, 0, 0.15);
            margin-bottom: 20px;
            transition: transform 0.2s ease;
        }

        .main-title:hover {
            transform: scale(1.02);
        }

        .dash {
            color: #7aaeb7;
            font-weight: 500;
        }

        form {
            margin: 20px auto;
            max-width: 400px;
            display: flex;
            gap: 10px;
            justify-content: center;
        }

        input[type="number"] {
            padding: 10px;
            font-size: 16px;
            border: 2px solid #a2cfe3;
            border-radius: 8px;
            width: 50%;
        }

        button {
            padding: 10px 20px;
            font-size: 16px;
            background-color: #246f91;
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: background 0.3s;
        }

        button:hover {
            background-color: #1b4e66;
        }

        .stats {
            margin-top: 30px;
        }

        .stats p {
            font-size: 18px;
            margin: 8px 0;
        }

        .log {
            margin-top: 30px;
            max-width: 400px;
            margin-left: auto;
            margin-right: auto;
            background: #ffffff;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.08);
        }

        .log-entry {
            font-size: 16px;
            margin: 4px 0;
            color: #555;
        }
    </style>
</head>
<body>
    <h1 class="main-title">Droplet <span class="dash">--</span> Water Tracker 💧</h1>

    <form method="POST" action="/">
        <input type="number" name="amount" placeholder="Amount in ml" required>
        <button type="submit">Add</button>
    </form>

    <h2>Daily Goal: {{ DAILY_GOAL }} ml</h2>
    <p><strong>Total Drunk:</strong> {{ total_intake }} ml</p>
    <p><strong>Remaining:</strong> {{ remaining }} ml</p>

    <div class="progress-bar" style="background: #e0e0e0; border-radius: 8px; height: 30px; width: 400px; margin: 20px auto;">
        <div class="progress" style="background: #7aaeb7; height: 100%; width: {{ progress }}%; border-radius: 8px; color: #fff; line-height: 30px;">
            {{ progress }}%
        </div>
    </div>

    <h2>Water Log:</h2>
    <ul style="list-style: none; padding: 0;">
        {% for entry in log %}
            <li class="log-entry">{{ entry.amount }} ml at {{ entry.time }}</li>
        {% endfor %}
    </ul>

    <p>Track your daily water intake effortlessly!</p>
</body>
</html>
