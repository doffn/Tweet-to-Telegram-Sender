# 🐦 Twitter Telegram Bot

A Python bot that scrapes tweets from **Nitter**, stores them in **MongoDB**, and sends new tweet alerts to a **Telegram channel** — all without using the official Twitter API.


## 📸 Preview

![Twitter Telegram Bot Preview](assets/img.png)
*An overview of the bot’s scraping and alert process.*


## 🚀 Features

* 🧩 **Nitter Scraper** — Collects tweets and replies from public Nitter mirrors without authentication.
* 💾 **MongoDB Storage** — Keeps track of tweet IDs to avoid duplicate alerts.
* 📢 **Telegram Integration** — Sends formatted tweet notifications to your Telegram channel.
* 🧠 **Randomized Headers** — Generates unique HTTP headers and cookies on every request to bypass scraping restrictions.
* ⚙️ **Error Handling** — Manages connection and parsing errors per user gracefully.


## 🧰 Requirements

* Python **3.8+**
* A **MongoDB** instance (local or cloud)
* A **Telegram Bot API Key** (from [@BotFather](https://t.me/BotFather))


## 🔑 Environment Variables

Set these environment variables (or create a `.env` file):

```bash
API=<your_telegram_bot_api_key>
CHANNEL_ID=<your_telegram_channel_id>
MONGODB_URI=<your_mongodb_connection_uri>
```


## ⚙️ Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/yourusername/twitter-telegram-bot.git
   cd twitter-telegram-bot
   ```

2. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```


## 🧠 Header Randomization

Each request to Nitter uses **fresh randomized headers** to mimic legitimate traffic and reduce IP blocking risks:

* Generates a **random 32-character cookie token** (`tiekoetter.com-cookie-verification=<token>`).
* Refreshes the **HTTP date** each run.
* Adds realistic **security headers** (CSP, HSTS, Referrer-Policy, etc.).

Example snippet:

```python
def generate_headers(self):
    date_str = datetime.utcnow().strftime("%a, %d %b %Y %H:%M:%S GMT")
    token = secrets.token_hex(16)
    cookie = f"tiekoetter.com-cookie-verification={token}"
    ...
```



## 🧪 Usage Example

```python
from bot import TwitterTelegramBot

# Initialize the bot
bot = TwitterTelegramBot()

# Define usernames to track
usernames = ["elonmusk", "nasa"]

# Step 1: Fetch tweets (include replies if desired)
data = bot.get_tweet_by_userid(usernames, replies=True)

# Step 2: Send new tweets to Telegram and store IDs in MongoDB
bot.tg_sender(data)
```

### 💡 Workflow

1. Scrapes tweets from Nitter (`https://nitter.tiekoetter.com/`).
2. Parses tweet text, date, and URL.
3. Checks MongoDB for already-sent tweet IDs.
4. Sends only **new tweets** to Telegram with Markdown formatting.


## 📂 Project Structure

```
twitter-telegram-bot/
│
├── assets/img.png     # Image or flow diagram
├── main.py                 # Main bot logic
├── requirements.txt       # Dependencies
└── README.md              # Documentation
```


## 🛠️ Technologies Used

* 🐍 **Python** – Core language
* 🌐 **Requests** – HTTP requests
* 🍃 **MongoDB / PyMongo** – Data storage
* 🧭 **BeautifulSoup4** – HTML parsing
* 🤖 **Telebot (pyTelegramBotAPI)** – Telegram integration


## 🕒 Optional: Automate

You can schedule the bot to run periodically using **cron** or a background task:

## Support

If you want an update or a question feel free to dm. **DOFFNERI**

