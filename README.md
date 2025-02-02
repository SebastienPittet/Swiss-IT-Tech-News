# Telegram-RSS-bot
Bot for telegram channel, example with: [Swiss-IT-News](https://t.me/SwissITNews)

# How to use this bot

## Quick Start with Docker

1. Clone or Download the content of this repository.

2. Optional: Ensure Docker is installed on your system.

3. Configuration options:

   You have two options for configuring the bot: using a `.env` file or a TOML file named `configuration.toml`. You can use one of them, but remember that settings in the TOML file will take precedence over the ENV variables.

   - **Using a `.env` file:**

     Create a `.env` file in the directory `./bot` with the following content, replacing the placeholders with your actual data:

     ```
     # Development settings
     TIME_INTERVAL_MIN=20
     ENTRY_MAX_TIME_OLD=1200
     BOT_TOKEN=yourBotToken
     CHANNEL_ID=@yourChannel
     RSS_URLS="https://korben.info/feed
     https://www.ictjournal.ch/taxonomy/term/404/feed
     https://www.ictjournal.ch/taxonomy/term/31/feed
     https://www.ictjournal.ch/taxonomy/term/406/feed
     https://www.newsd.admin.ch/newsd/feeds/rss?lang=fr&org-nr=1&offer-nr=308
     https://feeds.feedburner.com/TheHackersNews
     https://www.xavierstuder.com/feed
     https://www.thelazyadministrator.com/feed
     https://4sysops.com/feed
     https://www.thomasmaurer.ch/feed
     https://www.cyberciti.biz/atom/atom.xml
     https://blog.codinghorror.com/rss
     https://www.schneier.com/feed/atom"
     
     # Docker container settings
     TZ=Europe/Zurich
     
     ```

   - **Using a `configuration.toml` file:**

     Alternatively, you can create a `configuration.toml` file in the directory `./bot` with the necessary configuration. Here's a template for the TOML file:

     ```toml
     # configuration.toml

     # General settings
     TIME_INTERVAL_MIN = 20  # Run the feedparser every n minutes
     ENTRY_MAX_TIME_OLD = 1200  # 1200 seconds = 20 minutes

     # Bot Configuration
     BOT_TOKEN = "YOUR BOT TOKEN"
     CHANNEL_ID = "@YourChannel"

     # News, RSS feeds
     RSS_URLS = [
       "https://korben.info/feed",
       "https://www.ictjournal.ch/taxonomy/term/404/feed",
       "https://www.ictjournal.ch/taxonomy/term/31/feed",
       "https://www.ictjournal.ch/taxonomy/term/406/feed",
       "https://www.newsd.admin.ch/newsd/feeds/rss?lang=fr&org-nr=1&offer-nr=308",
       "https://feeds.feedburner.com/TheHackersNews",
       "https://redmondmag.com/rss-feeds/columns.aspx",
       "https://redmondmag.com/rss-feeds/in-depth.aspx",
       "https://redmondmag.com/rss-feeds/news.aspx",
       "https://redmondmag.com/rss-feeds/tech-library.aspx",
       "https://www.xavierstuder.com/feed",
       "https://www.thelazyadministrator.com/feed",
       "https://4sysops.com/feed",
       "https://www.thomasmaurer.ch/feed",
       "https://www.cyberciti.biz/atom/atom.xml",
       "https://blog.codinghorror.com/rss",
       "https://www.schneier.com/feed/atom",
     ]
     ```

     This file allows you to easily manage your bot's configuration in a structured format. Remember to replace the placeholders with your actual configuration details.

4. Build the Docker image:

    ```bash
    docker build -t telegram-rss-bot:latest .
    ```

5. Run the Docker container:

    ```bash
    docker run -d --name telegram-rss-bot:latest --env-file /path/to/your/.env
    ```

    Replace `/path/to/your/.env` with the actual path to your `.env` file.

## Traditional Setup

If you prefer not using Docker, follow these steps:

1. First, download or clone the repository containing the script to your local machine or server.

2. Get a Raspberry Pi (or any computer with Python 3) and install the needed libraries: 

    ```bash
    virtualenv .venv -p python3
    source .venv/bin/activate
    pip install -r requirements.txt
    ```

3. Create a `configuration.toml` file or an `.env` file to set up your bot token, channel ID, and RSS feeds. Below are the templates for each file type:

    **configuration.toml:**
    ```toml
    # Configuration file for Telegram Bot
    
    # General settings
    TIME_INTERVAL_MIN = 20  # Run the feedparser every n minutes
    ENTRY_MAX_TIME_OLD = 1200  # 1200 seconds = 20 min
    
    # Bot Configuration
    BOT_TOKEN = "YOUR BOT TOKEN"
    CHANNEL_ID = "@YourChannel"
    
    # News, RSS feeds
    RSS_URLS = [
        "https://korben.info/feed",
        "https://www.ictjournal.ch/taxonomy/term/404/feed",
        "https://www.ictjournal.ch/taxonomy/term/31/feed",
        "https://www.ictjournal.ch/taxonomy/term/406/feed",
        "https://www.newsd.admin.ch/newsd/feeds/rss?lang=fr&org-nr=1&offer-nr=308",
        "https://feeds.feedburner.com/TheHackersNews",
        "https://mspoweruser.com/feed/",
        "https://www.numerama.com/feed/",
    ]
    ```

    **.env:**
    ```
    # Development settings
    TIME_INTERVAL_MIN=20
    ENTRY_MAX_TIME_OLD=1200
    BOT_TOKEN="YOUR BOT TOKEN"
    CHANNEL_ID="@YourChannel"
    RSS_URLS="https://korben.info/feed
    https://www.ictjournal.ch/taxonomy/term/404/feed
    https://www.ictjournal.ch/taxonomy/term/31/feed
    https://www.ictjournal.ch/taxonomy/term/406/feed
    https://www.newsd.admin.ch/newsd/feeds/rss?lang=fr&org-nr=1&offer-nr=308
    https://feeds.feedburner.com/TheHackersNews
    https://redmondmag.com/rss-feeds/columns.aspx
    https://redmondmag.com/rss-feeds/in-depth.aspx
    https://redmondmag.com/rss-feeds/news.aspx
    https://redmondmag.com/rss-feeds/tech-library.aspx
    https://www.xavierstuder.com/feed
    https://www.thelazyadministrator.com/feed
    https://4sysops.com/feed
    https://www.thomasmaurer.ch/feed
    https://www.cyberciti.biz/atom/atom.xml
    https://blog.codinghorror.com/rss
    https://www.schneier.com/feed/atom"
    ```

4. The script will continuously run and execute an update at the time interval specified in your configuration file.

# Setting Up Telegram Channel and Bot

This chapter guides you through creating your Telegram channel and setting up a bot using BotFather, which will be used by your script to post updates.

## Creating Your Telegram Channel

1. Open Telegram and search for the "New Message" button, usually found at the bottom right corner. Click on it and select "New Channel".
2. Set your channel name and description. For example, "Swiss IT News" for IT-related updates in Switzerland.
3. Choose your channel's privacy setting. For public channels, set a unique link, such as `https://t.me/SwissITNews`.
4. Add any desired users to your channel or skip this step to proceed to channel creation.

## Creating a Bot with BotFather

1. In Telegram, search for the `@BotFather` user or access directly via [https://telegram.me/BotFather](https://telegram.me/BotFather).
2. Start a chat with BotFather and use the `/newbot` command to create a new bot.
3. Follow the instructions from BotFather to set up your bot's name and username. BotFather will then provide you with a token to access the Telegram API, which looks something like this: `123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11`.
4. Note down your bot's token; you'll need it for the script configuration.

![Bot Father](https://telegrambots.github.io/book/1/docs/logo-bot-father.jpg)

## Adding Your Bot to Your Channel

1. Add your bot to your channel as an administrator. To do this, go to your channel's "Info" section, select "Administrators", "Add Administrator", and then search for your bot by the username you gave it.
2. Give your bot permissions to post messages.


# Configuration
This code supports a TOML formatted configuration file:
```toml
$ cat configuration.toml

# Configuration file for Telegram Bot

# General settings
TIME_INTERVAL_MIN = 20  # Run the feedparser every n minutes
ENTRY_MAX_TIME_OLD = 1200  # 1200 seconds = 20 min

# Bot Configuration
BOT_TOKEN = "YOUR BOT TOKEN"
CHANNEL_ID = "@YourChannel"

# News, RSS feeds
RSS_URLS = [
    "https://korben.info/feed",
    "https://www.ictjournal.ch/taxonomy/term/404/feed",
    "https://www.ictjournal.ch/taxonomy/term/31/feed",
    "https://www.ictjournal.ch/taxonomy/term/406/feed",
    "https://www.newsd.admin.ch/newsd/feeds/rss?lang=fr&org-nr=1&offer-nr=308",
    "https://feeds.feedburner.com/TheHackersNews",
    "https://mspoweruser.com/feed/",
    "https://www.numerama.com/feed/",
    ]
```

If the configuration file fails (doesn't exist or incorrect synthax), it will default to `ENV VARs`. This last approach is highly recommended, to follow the [Twelve Factor App](https://12factor.net).

To ease the development work, you can rely on a .env file with:

```
# Development settings
TIME_INTERVAL_MIN=20
ENTRY_MAX_TIME_OLD=1200
BOT_TOKEN="YOUR BOT TOKEN"
CHANNEL_ID="@YourChannel"
RSS_URLS="https://korben.info/feed
https://www.ictjournal.ch/taxonomy/term/404/feed
https://www.ictjournal.ch/taxonomy/term/31/feed
https://www.ictjournal.ch/taxonomy/term/406/feed
https://www.newsd.admin.ch/newsd/feeds/rss?lang=fr&org-nr=1&offer-nr=308
https://feeds.feedburner.com/TheHackersNews
https://redmondmag.com/rss-feeds/columns.aspx
https://redmondmag.com/rss-feeds/in-depth.aspx
https://redmondmag.com/rss-feeds/news.aspx
https://redmondmag.com/rss-feeds/tech-library.aspx
https://www.xavierstuder.com/feed
https://www.thelazyadministrator.com/feed
https://4sysops.com/feed
https://www.thomasmaurer.ch/feed
https://www.cyberciti.biz/atom/atom.xml
https://blog.codinghorror.com/rss
https://www.schneier.com/feed/atom"
```

Env Variables can be set/intjected via Dockerfile or a Kubernetes manifest.
