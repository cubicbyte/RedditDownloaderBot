# Reddit Downloader Bot

A Telegram bot for downloading Reddit posts.

Table of Contents
=================
  * [What this bot can do](#what-this-bot-can-do)
  * [What this bot cannot do](#what-this-bot-cannot-do)
    * [List of non x.redd.it hosts from which this bot *can* download](#list-of-non-xreddit-hosts-from-which-this-bot-can-download)
  * [Setup](#setup)
    * [Build](#build)
    * [Obtain Reddit Token](#obtain-reddit-token)
    * [Obtain Telegram Token](#obtain-telegram-token)
    * [Run](#run)
  * [Optional Settings](#optional-settings)
    * [Allowed Users](#allowed-users)  
    * [Disable NSFW Content](disable-nsfw-content)

# What this bot can do

* Send Reddit posts and coments as text on Telegram
* Send images and image galleries hosted on `i.redd.it`
* Send videos hosted on `v.redd.it`
* Convert videos to audio only
* Send GIFs hosted on Reddit
* Let users choose the quality of images and videos
* Limit the users who can use it

# What this bot cannot do

* Send polls
* Send deleted posts
* Upload files larger than 50 MB
* Send text posts with over 4,096 characters or complex markdown (for example, tables)
* Download images or videos that are not hosted on `x.redd.it` (for example, YouTube videos)

## List of non `x.redd.it` hosts from which this bot *can* download

1. Imgur
2. Gfycat
3. Streamable
4. Red GIFs (although currently not working)

# Setup

## Build

First, install [FFmpeg](https://www.ffmpeg.org). On Debian or Ubuntu, simply run `apt install ffmpeg`. Then, clone and build the project using the following steps.

```bash
git clone https://github.com/mcsaeid/RedditDownloaderBot
cd RedditDownloaderBot
go build ./cmd/RedditDownloaderBot/
```

## Obtain Reddit Token

To use the bot, you will need Reddit and Telegram tokens. Start by creating a Reddit application. Go to https://www.reddit.com/prefs/apps and click on “are you a developer? create an app...” Choose a name, select `script` as the type of application, input something in the redirect URI field, and click on “create app.”

<p align="center">
  <img src="https://user-images.githubusercontent.com/63400670/215763728-f4242f17-46bd-421b-ab1c-493d1ec49f3b.png" alt="Creating a Reddit application"/>
</p>

You will be given two tokens: a client ID and a client secret—as shown in the image below.

<p align="center">
  <img src="https://user-images.githubusercontent.com/63400670/215763740-7e4e771e-1c40-47a8-95fb-3227dd130a82.png" alt="Reddit tokens"/>
</p>

## Obtain Telegram Token

Interact with [BotFather](https://t.me/BotFather) to create a bot and obtain its token. Additionally, you can use this [guide](https://core.telegram.org/bots/tutorial#obtain-your-bot-token).

Your token will look something like this:

```bash
4839574812:AAFD39kkdpWt3ywyRZergyOLMaJhac60qc
```

## Run

Now that you have the necessary tokens, edit the docker-compose.yml file and set the environment variables as such:

```bash
CLIENT_ID: "Reddit client ID"
CLIENT_SECRET: "Reddit client secret"
BOT_TOKEN: "Telegram bot token"
```

You can run the bot using docker-compose. In case you don’t have docker-compose installed, follow the steps below.

```bash
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-linux-x86_64" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

Lastly, run `docker-compose up --build` inside the RedditDownloaderBot directory to build and run the bot.

# Optional Settings

## Allowed Users

You can configure the bot to allow access to only a group of users. This is useful for deploying private bots. To do so, you need to create a whitelist that consists of Telegram user IDs. You can obtain user IDs using [GetIDs Bot](https://t.me/getidsbot). Next, create the environment variable `ALLOWED_USERS` and set its value to user IDs, separated by a comma.

```bash
ALLOWED_USERS: "1,2,3"
```

## Disable NSFW Content

You can keep the bot from downloading NSFW posts by setting the following environment variable:

```bash
DENY_NSFW: "true"
```

##### Disable Link to Post

You can disable the link to posts which is automatically added to each message by setting this:

```bash
export DISABLE_LINK_IN_CAPTION=true
```
