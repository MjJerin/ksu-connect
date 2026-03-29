# KsUnited ⚡

A Q&A platform we built for Kent State students during our hackathon. Think Reddit but just for KSU — you can ask questions, get AI answers, reply with GIFs, and see who's the most helpful person on campus.

---

## what it does

- you sign in with your @kent.edu email (no outsiders)
- post questions with flairs like Housing, Dining, Academic, Rant, etc.
- **FlashAI** is a chatbot that actually knows KSU stuff — dining hours, tuition, dorms, advising — powered by AWS Bedrock
- every post gets auto-tagged positive/negative/neutral by the AI in the background
- replies support GIFs via Giphy
- there's a leaderboard that scores users based on upvotes, posts, replies, and how positive their posts are
- admin panel to monitor everything

## the leaderboard (data science part)

we calculate a "Flash Score" for each user:

```
score = (upvotes × 3) + (posts × 2) + (replies × 1) + sentiment bonus
```

then we normalize it 0–100 using min-max normalization so it stays competitive no matter how many people join. sentiment bonus is +10 if most of your posts are positive, -5 if they're mostly negative.

## stack

- Python + Flask for the backend
- SQLite for the database
- AWS Bedrock (Claude 3 Haiku) for the AI features
- Gmail SMTP for password reset emails
- Giphy API for GIF search in replies
- Chart.js for the leaderboard chart
- plain HTML/CSS/JS for the frontend, no frameworks

## run it locally

```bash
pip install flask flask-login werkzeug requests
```

make a `.env` file:
```
AWS_BEARER_TOKEN_BEDROCK=...
MAIL_EMAIL=...
MAIL_PASSWORD=...
GIPHY_API_KEY=...
```

then just:
```bash
python app.py
```

admin panel is at `/admin`

---

made at KSU hackathon 2026 ⚡
