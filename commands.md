# Commands


## Help

python3 src/cli.py --h

Output:
```
usage: cli.py [-h] [-n NAME] [-ip IP] [-un USERNAME]

Digital Detective CLI Tool

options:
  -h, --help            show this help message and exit
  -n NAME, --name NAME  Performs a full-name search, "first last"
  -ip IP, --ip IP       Performs an IP search, 1.2.3.4
  -un USERNAME, --username USERNAME
                        Performs a username search, "@username"
```

## CLI Tool Commands

**"Full Name"**      
python3 src/cli.py -n "first last"    

**IP Address**       
python3 src/cli.py -ip 1.2.3.4       

**"Username"**     
python3 src/cli.py -un "@username""       

**Help Command**      
python3 src/cli.py --help         
                   



### Run CLI tool commands via Virtual Environment
```
source venv/bin/activate
```
Run different commands
```
deactivate
```

### Different commands and results

**Name search**
```
python3 src/cli.py -n "Dwight Schrute"
```

First time:
```
(venv) student@student-ThinkPad-T490s:~/digital-detective$ python3 src/cli.py -n "Dwight Schrute"
Request URL: https://serpapi.com/search?q=Dwight Schrute&location=Finland&hl=en&gl=fi&num=10&api_key=
Request completed in 2.96 seconds
No cached data found. Fetching new data from Fonecta.
New data saved to cache.
No results found in Fonecta JSON data.
      Name Search Results for Dwight Schrute       
┏━━━━━━━━━━━━━━━━┳━━━━━━━━━━━┳━━━━━━━━━━━┳━━━━━━━━┓
┃ Name           ┃ Location  ┃ Phone     ┃ source ┃
┡━━━━━━━━━━━━━━━━╇━━━━━━━━━━━╇━━━━━━━━━━━╇━━━━━━━━┩
│ Dwight Schrute │ Not found │ Not found │ Google │
└────────────────┴───────────┴───────────┴────────┘
Result written to file: results/n_dwight_schrute.txt
```

Second time using cached data:
```
(venv) student@student-ThinkPad-T490s:~/digital-detective$ python3 src/cli.py -n "Dwight Schrute"
Using cached data for google_search_dwight_schrute
Using cached data for fonecta_search_dwight_schrute
No results found in Fonecta JSON data.
      Name Search Results for Dwight Schrute       
┏━━━━━━━━━━━━━━━━┳━━━━━━━━━━━┳━━━━━━━━━━━┳━━━━━━━━┓
┃ Name           ┃ Location  ┃ Phone     ┃ source ┃
┡━━━━━━━━━━━━━━━━╇━━━━━━━━━━━╇━━━━━━━━━━━╇━━━━━━━━┩
│ Dwight Schrute │ Not found │ Not found │ Google │
└────────────────┴───────────┴───────────┴────────┘
Result written to file: results/n_dwight_schrute1.txt
(venv) student@student-ThinkPad-T490s:~/digital-detective$ 

```

My name:

```
(venv) student@student-ThinkPad-T490s:~/digital-detective$ python3 src/cli.py -n "Laura Levistö"
Using cached data for google_search_laura_levistö
Using cached data for fonecta_search_laura_levistö
                    Name Search Results for Laura Levistö                     
┏━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━┳━━━━━━━━━┓
┃ Name                  ┃ Location                    ┃ Phone      ┃ source  ┃
┡━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━╇━━━━━━━━━┩
│ Laura Levistö         │ Tampere, Pirkanmaa, Finland │ Not found  │ Google  │
│ Laura Anniina Levistö │ Tampere                     │ 040508●●●● │ Fonecta │
└───────────────────────┴─────────────────────────────┴────────────┴─────────┘
Result written to file: results/n_laura_levistö1.txt
(venv) student@student-ThinkPad-T490s:~/digital-detective$ 
```

**IP search**
```
python3 src/cli.py -ip 8.8.8.8
```
First time:
```
(venv) student@student-ThinkPad-T490s:~/digital-detective$ python3 src/cli.py -ip 8.8.8.8
Request URL: http://ip-api.com/json/8.8.8.8
Request completed in 0.49 seconds
Request URL: https://api.iplocation.net/?ip=8.8.8.8&format=json
Request completed in 0.43 seconds
                                      IP Search Results                                       
┏━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ Field                    ┃ Value                                                           ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┩
│ IP Address               │ 8.8.8.8                                                         │
│ ISP                      │ Google LLC                                                      │
│ Location (Lat, Lon)      │ 39.03, -77.5                                                    │
│ City                     │ Ashburn                                                         │
│ Country                  │ United States                                                   │
│ Cross-Reference          │ Accurate: Both APIs returned matching or complementary results. │
│ ISP Result Was Different │ ISPs match.                                                     │
└──────────────────────────┴─────────────────────────────────────────────────────────────────┘
Result written to file: results/ip_8_8_8_8.txt
(venv) student@student-ThinkPad-T490s:~/digital-detective$ 
```
Second time using cached data:
```
(venv) student@student-ThinkPad-T490s:~/digital-detective$ python3 src/cli.py -ip 8.8.8.8
Using cached data for ipapi_8.8.8.8
Using cached data for iplocation_8.8.8.8
                                      IP Search Results                                       
┏━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ Field                    ┃ Value                                                           ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┩
│ IP Address               │ 8.8.8.8                                                         │
│ ISP                      │ Google LLC                                                      │
│ Location (Lat, Lon)      │ 39.03, -77.5                                                    │
│ City                     │ Ashburn                                                         │
│ Country                  │ United States                                                   │
│ Cross-Reference          │ Accurate: Both APIs returned matching or complementary results. │
│ ISP Result Was Different │ ISPs match.                                                     │
└──────────────────────────┴─────────────────────────────────────────────────────────────────┘
Result written to file: results/ip_8_8_8_81.txt
(venv) student@student-ThinkPad-T490s:~/digital-detective$ 
```
Different IP:
```
python3 src/cli.py -ip 185.199.108.153
```
```
(venv) student@student-ThinkPad-T490s:~/digital-detective$ python3 src/cli.py -ip 185.199.108.153
Using cached data for ipapi_185.199.108.153
Using cached data for iplocation_185.199.108.153
                                  IP Search Results                                  
┏━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ Field                    ┃ Value                                                  ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┩
│ IP Address               │ 185.199.108.153                                        │
│ ISP                      │ Fastly, Inc.                                           │
│ Location (Lat, Lon)      │ 37.7823, -122.391                                      │
│ City                     │ San Francisco                                          │
│ Country                  │ United States                                          │
│ Cross-Reference          │ Incomplete result: some fields are different.          │
│ ISP Result Was Different │ IP-API ISP: Fastly, Inc., IP-Location ISP: GitHub Inc. │
└──────────────────────────┴────────────────────────────────────────────────────────┘
Result written to file: results/ip_185_199_108_1531.txt
(venv) student@student-ThinkPad-T490s:~/digital-detective$
```

**Username search**
```
python3 src/cli.py -un "@recyclops"
```
First time:

```
(venv) student@student-ThinkPad-T490s:~/digital-detective$ python3 src/cli.py -un "@recyclops"
Running Sherlock for username: recyclops
[*] Checking username recyclops on:

[+] 7Cups: https://www.7cups.com/@recyclops
[+] 9GAG: https://www.9gag.com/u/recyclops
[+] Anilist: https://anilist.co/user/recyclops/
[+] Apple Discussions: https://discussions.apple.com/profile/recyclops
[+] Audiojungle: https://audiojungle.net/user/recyclops
[+] Behance: https://www.behance.net/recyclops
[+] Blogger: https://recyclops.blogspot.com
[+] BoardGameGeek: https://boardgamegeek.com/user/recyclops
[+] CGTrader: https://www.cgtrader.com/recyclops
[+] Chess: https://www.chess.com/member/recyclops
[+] Clubhouse: https://www.clubhouse.com/@recyclops
[+] Codecademy: https://www.codecademy.com/profiles/recyclops
[+] Codeforces: https://codeforces.com/profile/recyclops
[+] DeviantART: https://recyclops.deviantart.com
[+] Discord: https://discord.com
[+] Disqus: https://disqus.com/recyclops
[+] Duolingo: https://www.duolingo.com/profile/recyclops
[+] Flipboard: https://flipboard.com/@recyclops
[+] Freelance.habr: https://freelance.habr.com/freelancers/recyclops
[+] Freesound: https://freesound.org/people/recyclops/
[+] GNOME VCS: https://gitlab.gnome.org/recyclops
[+] GaiaOnline: https://www.gaiaonline.com/profiles/recyclops
[+] Genius (Users): https://genius.com/recyclops
[+] Giant Bomb: https://www.giantbomb.com/profile/recyclops/
[+] Giphy: https://giphy.com/recyclops
[+] GitHub: https://www.github.com/recyclops
[+] HackerOne: https://hackerone.com/recyclops
[+] HackerRank: https://hackerrank.com/recyclops
[+] HudsonRock: https://cavalier.hudsonrock.com/api/json/v2/osint-tools/search-by-username?username=recyclops
[+] Hugging Face: https://huggingface.co/recyclops
[+] IFTTT: https://www.ifttt.com/p/recyclops
[+] Imgur: https://imgur.com/user/recyclops
[+] Instructables: https://www.instructables.com/member/recyclops
[+] Issuu: https://issuu.com/recyclops
[+] Itch.io: https://recyclops.itch.io/
[+] Kongregate: https://www.kongregate.com/accounts/recyclops
[+] Letterboxd: https://letterboxd.com/recyclops
[+] Lichess: https://lichess.org/@/recyclops
[+] Linktree: https://linktr.ee/recyclops
[+] Memrise: https://www.memrise.com/user/recyclops/
[+] MixCloud: https://www.mixcloud.com/recyclops/
[+] Monkeytype: https://monkeytype.com/profile/recyclops
[+] MyAnimeList: https://myanimelist.net/profile/recyclops
[+] Myspace: https://myspace.com/recyclops
[+] Newgrounds: https://recyclops.newgrounds.com
[+] NitroType: https://www.nitrotype.com/racer/recyclops
[+] OpenStreetMap: https://www.openstreetmap.org/user/recyclops
[+] Pastebin: https://pastebin.com/u/recyclops
[+] Periscope: https://www.periscope.tv/recyclops/
[+] Pokemon Showdown: https://pokemonshowdown.com/users/recyclops
[+] Reddit: https://www.reddit.com/user/recyclops
[+] Replit.com: https://replit.com/@recyclops
[+] Roblox: https://www.roblox.com/user.aspx?username=recyclops
[+] Scratch: https://scratch.mit.edu/users/recyclops
[+] Scribd: https://www.scribd.com/recyclops
[+] Sketchfab: https://sketchfab.com/recyclops
[+] Slack: https://recyclops.slack.com
[+] Smule: https://www.smule.com/recyclops
[+] Snapchat: https://www.snapchat.com/add/recyclops
[+] SoundCloud: https://soundcloud.com/recyclops
[+] Sporcle: https://www.sporcle.com/user/recyclops/people
[+] Spotify: https://open.spotify.com/user/recyclops
[+] Star Citizen: https://robertsspaceindustries.com/citizens/recyclops
[+] Steam Community (User): https://steamcommunity.com/id/recyclops/
[+] Telegram: https://t.me/recyclops
[+] Tenor: https://tenor.com/users/recyclops
[+] ThemeForest: https://themeforest.net/user/recyclops
[+] TorrentGalaxy: https://torrentgalaxy.to/profile/recyclops
[+] TradingView: https://www.tradingview.com/u/recyclops/
[+] Trakt: https://www.trakt.tv/users/recyclops
[+] Trello: https://trello.com/recyclops
[+] TryHackMe: https://tryhackme.com/p/recyclops
[+] Twitter: https://x.com/recyclops
[+] Typeracer: https://data.typeracer.com/pit/profile?user=recyclops
[+] Ultimate-Guitar: https://ultimate-guitar.com/u/recyclops
[+] Untappd: https://untappd.com/user/recyclops
[+] VSCO: https://vsco.co/recyclops
[+] Venmo: https://account.venmo.com/u/recyclops
[+] Weblate: https://hosted.weblate.org/user/recyclops/
[+] Weebly: https://recyclops.weebly.com/
[+] Wikipedia: https://en.wikipedia.org/wiki/Special:CentralAuth/recyclops?uselang=qqx
[+] Xbox Gamertag: https://xboxgamertag.com/search/recyclops
[+] YouTube: https://www.youtube.com/@recyclops
[+] eGPU: https://egpu.io/forums/profile/recyclops/
[+] geocaching: https://www.geocaching.com/p/default.aspx?u=recyclops
[+] last.fm: https://last.fm/user/recyclops
[+] livelib: https://www.livelib.ru/reader/recyclops
[+] mastodon.social: https://mastodon.social/@recyclops
[+] osu!: https://osu.ppy.sh/users/recyclops
[+] Bluesky: https://bsky.app/profile/recyclops.bsky.social

[*] Search completed with 90 results
Running Social Analyzer for username: @recyclops
                           Cross-Referenced Results for @recyclops                           
┏━━━━━┳━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ No. ┃ Platform      ┃           Status           ┃ Link                                   ┃
┡━━━━━╇━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┩
│ 1   │ Github        │    Found with Sherlock     │ https://www.github.com/recyclops       │
│ 2   │ Twitter       │         Not Found          │ Not Found                              │
│ 3   │ Instagram     │         Not Found          │ Not Found                              │
│ 4   │ Facebook      │ Found with Social Analyzer │ https://facebook.com/@recyclops        │
│ 5   │ Linkedin      │         Not Found          │ Not Found                              │
│ 6   │ Youtube       │    Found with Sherlock     │ https://www.youtube.com/@recyclops     │
│ 7   │ Reddit        │    Found with Sherlock     │ https://www.reddit.com/user/recyclops  │
│ 8   │ Tiktok        │         Not Found          │ Not Found                              │
│ 9   │ Pinterest     │         Not Found          │ Not Found                              │
│ 10  │ Tumblr        │         Not Found          │ Not Found                              │
│ 11  │ Snapchat      │    Found with Sherlock     │ https://www.snapchat.com/add/recyclops │
│ 12  │ Medium        │         Not Found          │ Not Found                              │
│ 13  │ Quora         │         Not Found          │ Not Found                              │
│ 14  │ Vimeo         │         Not Found          │ Not Found                              │
│ 15  │ Flickr        │         Not Found          │ Not Found                              │
│ 16  │ Soundcloud    │    Found with Sherlock     │ https://soundcloud.com/recyclops       │
│ 17  │ Dribbble      │         Not Found          │ Not Found                              │
│ 18  │ Behance       │    Found with Sherlock     │ https://www.behance.net/recyclops      │
│ 19  │ Deviantart    │       Found in both        │ https://recyclops.deviantart.com       │
│ 20  │ Stackoverflow │         Not Found          │ Not Found                              │
└─────┴───────────────┴────────────────────────────┴────────────────────────────────────────┘
Result written to file: results/un_recyclops.txt
(venv) student@student-ThinkPad-T490s:~/digital-detective$
```
Second time using cached data:

```
(venv) student@student-ThinkPad-T490s:~/digital-detective$ python3 src/cli.py -un "@recyclops"
Using cached data for Sherlock: recyclops
Using cached data for Social Analyzer: @recyclops
                           Cross-Referenced Results for @recyclops                           
┏━━━━━┳━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ No. ┃ Platform      ┃           Status           ┃ Link                                   ┃
┡━━━━━╇━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┩
│ 1   │ Github        │    Found with Sherlock     │ https://www.github.com/recyclops       │
│ 2   │ Twitter       │         Not Found          │ Not Found                              │
│ 3   │ Instagram     │         Not Found          │ Not Found                              │
│ 4   │ Facebook      │ Found with Social Analyzer │ https://facebook.com/@recyclops        │
│ 5   │ Linkedin      │         Not Found          │ Not Found                              │
│ 6   │ Youtube       │    Found with Sherlock     │ https://www.youtube.com/@recyclops     │
│ 7   │ Reddit        │    Found with Sherlock     │ https://www.reddit.com/user/recyclops  │
│ 8   │ Tiktok        │         Not Found          │ Not Found                              │
│ 9   │ Pinterest     │         Not Found          │ Not Found                              │
│ 10  │ Tumblr        │         Not Found          │ Not Found                              │
│ 11  │ Snapchat      │    Found with Sherlock     │ https://www.snapchat.com/add/recyclops │
│ 12  │ Medium        │         Not Found          │ Not Found                              │
│ 13  │ Quora         │         Not Found          │ Not Found                              │
│ 14  │ Vimeo         │         Not Found          │ Not Found                              │
│ 15  │ Flickr        │         Not Found          │ Not Found                              │
│ 16  │ Soundcloud    │    Found with Sherlock     │ https://soundcloud.com/recyclops       │
│ 17  │ Dribbble      │         Not Found          │ Not Found                              │
│ 18  │ Behance       │    Found with Sherlock     │ https://www.behance.net/recyclops      │
│ 19  │ Deviantart    │       Found in both        │ https://recyclops.deviantart.com       │
│ 20  │ Stackoverflow │         Not Found          │ Not Found                              │
└─────┴───────────────┴────────────────────────────┴────────────────────────────────────────┘
Result written to file: results/un_recyclops1.txt
(venv) student@student-ThinkPad-T490s:~/digital-detective$ 
```

### Run run_tests.sh via Virtual Environment

```
chmod +x run_tests.sh

./run_tests.sh
```
Video of running the tests:

---

<video controls src="testcases_digital_detective.mp4" title="Title"></video>

---

First it uses 
- get_ip_info_ipapi, ("http://ip-api.com/json/{ip_address}")
- get_personal_info, ("https://serpapi.com/search?q={full_name}&location=Finland&hl=en&gl=fi&num=10&api_key={SERPAPI_KEY}")
- get_username_mentions_sherlock

Second time it uses cached data.