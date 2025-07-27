from flask import Flask, request

app = Flask(__name__)

# Set your daily goal in ml
DAILY_GOAL = 2000

# In-memory storage
water_log = []
total_intake = 0

@app.route("/", methods=["GET", "POST"])
def home():
    global total_intake

    if request.method == "POST":
        amount = request.form.get("amount")
        if amount:
            try:
                ml = int(amount)
                water_log.append(f"{ml} ml")
                total_intake += ml
            except ValueError:
                pass

    log_html = "<br>".join(water_log)
    remaining = max(0, DAILY_GOAL - total_intake)
    progress = min(100, int((total_intake / DAILY_GOAL) * 100))

    return f"""
        <html>
        <head>
            <title>Water Tracker</title>
            <style>
                .progress-bar {{
                    width: 100%;
                    background-color: #ddd;
                    border-radius: 10px;
                    overflow: hidden;
                    height: 30px;
                    margin-bottom: 10px;
                }}
                .progress {{
                    height: 100%;
                    background-color: #4CAF50;
                    width: {progress}%;
                    text-align: center;
                    color: white;
                    line-height: 30px;
                    font-weight: bold;
                }}
            </style>
        </head>
        <body>
            <h1>Water Tracker 💧</h1>
            <form method="POST">
                <input type="number" name="amount" placeholder="Amount in ml" required>
                <button type="submit">Add</button>
            </form>

            <h2>Daily Goal: {DAILY_GOAL} ml</h2>
            <p><strong>Total Drunk:</strong> {total_intake} ml</p>
            <p><strong>Remaining:</strong> {remaining} ml</p>

            <div class="progress-bar">
                <div class="progress">{progress}%</div>
            </div>

            <h2>Water Log:</h2>
            {log_html}
        </body>
        </html>
    """

if __name__ == "__main__":
    app.run(debug=True)
