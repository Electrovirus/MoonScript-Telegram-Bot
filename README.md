#Moonscript telegram bot

Multi purpose telegram bot written in MoonScript/lua and licenced under the GNU General Public License.


Table of Contents

* [Setup](#setup)
* [Telegram Cli](#telegram-cli)
* [Database](#database)
* [Plugins](#plugins)
* [Support and development](#support-and-development)
* [Special thanks to](#special-thanks-to)
* [Collaborators](#collaborators)
* [Other projects](#other-projects)

#Setup

You should have lua,luarocks,redis-server,moonscript,lua-socket,lua-sec,oauth,redis-lua,lua-cjson and ansicolors installed

You can install them by:

```bash
sudo apt-get update; sudo apt-get install lua5.1 luarocks lua-socket lua-sec redis-server ; sudo luarocks install moonscript ; sudo luarocks install oauth ; sudo luarocks install redis-lua ; sudo luarocks install lua-cjson ; sudo luarocks install ansicolors;sudo luarocks install serpent
```

Clone the bot

```bash
cd $HOME
git clone https://github.com/electrovirus/MoonScript-Telegram-Bot.git
cd MoonScript-Telegram-Bot
```
Set telegram_api_key in config.moon file to the token you received from the Botfather.

```moonscript
telegram_api_key: ""--Your telegram bot api key
```

Run it!

```
sh run.sh
```


If you get this error from moonscript
```
/usr/bin/lua: /usr/share/lua/5.1//luarocks/loader.lua:113: error loading module 'lfs' from file '/usr/local/lib/lua/5.1/lfs.so':
    /usr/local/lib/lua/5.1/lfs.so: undefined symbol: luaL_register
```



Make sure you are using the lua5.1 package instead of the lua5.2 package. Try:

```
sudo apt-get install lua5.1
sudo apt-get remove lua5.2
```


# Telegram cli

First clone and configure telegram cli

```
git clone https://github.com/Rondoozle/tg.git
cd tg
git submodule update --init --recursive
./configure
make
```
Run it with -P and --json options

```
./bin/telegram-cli -k ./tg/tg-server.pub -P 7731 --json
```
Enter your number and conformation code

And uncomment plugin `telegramCli` in config.moon

You can send command to telegram-cli using your api bot

```
#tg msg user#id123456789 <text>
#tg msg channel#id123456789 <text>
#tg msg chat#id123456789 <text>

#tg chat_del_user chat#id123456789 user#id12345678 <text>
```

Press `TAB` key twice in telegram for all of the methods

You should have serpent installed

```
sudo luarocks install serpent
```


#Database
bot is using redis as database
We use perfix/folder `bot`

Here are the datas

**Chats**

`bot:chats` > List of all chats(groups,supergroups,privates)

`bot:privates` > List of all private chats

`bot:groups` > List of all groups

`bot:supergroups` > List of all supergroups

`bot:inline_users` > List of all inline users

**chat_id info**

`bot:chats:chat_id`

1. title
2. type

**user_id info**

`bot:users:user_id`

1. first_name
2. last_name
3. username

These info will be updated on each msg

`bot:total_inline_from_user:msg.from.id` >  

**bot statistics**

`bot:total_messages` > Number of total msgs bot received

`bot:total_inlines` > Number of total inline requests

**chat_id msg statistics**

`bot:total_chat_msgs:chat_id` > Number of total msgs bot received in chat_id

`"bot:total_users_msgs_in_chat:chat_id:user_id"` > Number of total msgs bot received in chat_id from user_id

**chat_id members**

`bot:chatchat_id` > list of chat_id members


[How to backup,restore,secure,stablize redis DB](https://github.com/SEEDTEAM/TeleSeed/wiki/Redis)

# Plugins

Plugins list
* [9gag](#9gag)
* [Admin](#admin)
* [Anime](#anime)
* [Calculator](#calculator)
* [Cat](#cat)
* [Chatter](#chatter)
* [Code](#code)
* [Dogify](#dogify)
* [Echo](#echo)
* [Giphy](#giphy)
* [Github](#github)
* [Google](#google-search)
* [Help](#help)
* [Imdb](#imdb)
* [Ipinfo](#ip-info)
* [Lastfm](#lastfm)
* [Linkshortener](#link-shortener)
* [Location](#location)
* [Meme](#meme)
* [Moon](#moon)
* [Qrcode](#qrcode)
* [Reddit](#reddit)
* [Remind](#remind)
* [Spotify](#spotify)
* [Stats](#stats)
* [Sticker](#sticker)
* [Talk](#talk)
* [Telegram-Cli](#telegramcli)
* [Time](#time)
* [Translate](#Translate)
* [Urbandictionary](#urban-dictionary)
* [Weather](#weather)
* [Webshot](#webshot)
* [Who](#who)
* [Wikipedia](#wikipedia)
* [youtube](#youtube)



### Admin

Plugin for admins

Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  N    |        N         |         Y          |    N

**Commands**

`/bot`

>Returns Bot status

`/admin reload`

>Reloads bot

`/plugins <Plugin_name> <chat_id> <true|false>`

>True will disable plugin `<Plugin_name>` on chat `<chat_id>`

`/blacklist <user_id>`

>This command will blacklist <user_id>
>>Can also be used by reply

`/bc <chat_id> <text>`

>this command will send `<text>` to `<chat_id>`
>>Markdown is enabled

>>use @channel_username for sending msgs to channels

`/broadcast <msg>`
>This command will send msg to all chats

### Calculator

Returns solutions to math expressions


Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  Y    |        N         |         Y          |    N

**Commands**

`/calc <expression>`

### Cat

Returns a cat

Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  Y    |        O         |         Y          |    N

**Commands**

`/cat`

### Chatter

Talk to bot in English !

Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  Y    |        N         |         Y          |    N

**Commands**

`bot_first_name, <text>`
`bot_username, <text>`
>jack, How are you ?
>@imandabot, How are you ?
>>you can also trigger chatter plugin by talking to bot in private or replying on of its messages in groups

### Code

Send the code in image format with support for highlighter.

Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  Y    |        Y         |         N          |    N


**Commands**

`/code [language] [code]`


### Dogify

Create a doge image with you words


Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  Y    |        N         |         Y          |    N

**Commands**

`/dogify <your/words/with/slashes>`

### Echo

Returns text

Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  Y    |        N         |         Y          |    Y

**Commands**

`/echo <text>`

>Markdown is enabled

**Inline**

`@bot_username /echo <text>`


### Giphy

Returns a GIF from giphycom!

Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  Y    |        Y         |         Y          |    N

**Commands**

`/giphy`

>Returns a random GIF

`/giphy [query]`

>Returns a GIF about [query]

### Github

Returns info about GitHub repo

Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  Y    |       N          |         Y          |    N


**Commands**

`/github <repo>`

>/gitrepo SEEDTEAM/TeleSeed

### Google search

Google search

Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  Y    |        N         |         Y          |    N


**Commands**

`/google <terms>`

`/g <terms>`

### 10 - Help

Returns info about other plugins

Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  N    |        N         |         Y          |    N


**Commands**

`/help`

>Will return a short list of plugins

`/help all`

>Will return full list of plugins with their commands

`/help [plugin_name]`

>Will return info about that plugin



### IMDB

Returns Info about movie from IMDB and its poster

Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  Y    |        N         |         Y          |    N


**Commands**



### IP info

Returns Given IP or domain info

Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  Y    |        Y         |         Y          |    N


**Commands**

`/ip <IP|domain>`


### Link shortener

Returns Shorten link

Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  Y    |        Y         |         Y          |    N


**Commands**

`/shorten <url>`

>/shorten https://github.com/SEEDTEAM


### Location

Sends location data

Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  Y    |        N         |         Y          |    N


**Commands**

`/loc <query>`

`/location <query>`


### Remind

Reminder

Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  Y    |        N         |         Y          |    N


**Commands**

`/remind <delay (value|mh)>  <text>`

>/remind 1h test

>/remind 1m test

>/remind 1h30m test

>>This plugin will save data in Redis(database) So It even works after Bot crashed or anything happen


### Spotify

Spotify plugin

Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  Y    |        O         |         Y          |    Y


**Commands**

`/spotify get [track name(for search)]`

Returns preview of that song (only 30 sec)

`/spotify track [track name(for search)]`

Returns track info and picture

`/spotify album [album name(for search)]`

Returns album info and picture

`/spotify artist [artist name(for search)]`

Returns artist info and picture

`/spotify playlist [playlist name(for search)]`

Returns playlist info and picture

**Inline**

`@bot_username /spotify album [album name(for search)]`

`@bot_username /spotify album [album name(for search)]`

`@bot_username /spotify artist [artist name(for search)]`

`@bot_username /spotify playlist [playlist name(for search)]`


### Stats

Chat msg statistics

Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  Y    |        N         |         Y          |    N


**Commands**


### Talk

Returns voice

Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  Y    |        N         |         Y          |    N


**Commands**

`/tts <text>`


### Time

Returns the time, date, and timezone for the given location

Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  Y    |        N         |         Y          |    N


**Commands**

`/time <location>`



### Urban dictionary

Returns the top definition from Urban Dictionary.

Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  Y    |        N         |         Y          |    N


**Commands**

`/ud <query>`


### Webshot

Returns screen shot from given website

Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  Y    |        Y         |         Y          |    N


**Commands**

`/webshot <url>`


### Who

Returns info about user and chat

Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  Y    |        N         |         Y          |    N


**Commands**

`/who`

### Wikipedia

Returns results from wikipedia.com

Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  Y    |        N         |         Y          |    N


**Commands**

`/wiki <query>`
`/wikipedia <query>`


### Youtube

Returns results from youtube.com

Listed | Requires API KEY | Enabled by default | inline
------ | ---------------- | ------------------ | ------
  Y    |        Y         |         N          |    Y


**Commands**

`/youtube get [video name(for search)]`
`/youtube dl [video name(for download)]`

**Inline**

`/youtube dl [video name(for download)]`



#This source is just edited by Electrovirus
