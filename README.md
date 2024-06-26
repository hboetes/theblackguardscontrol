# About
This script generates a blacklist for nftables from various ip lists:

## The name
It's a song from the legendary band VoiVod.

## What you might want to change:
These are the lists I currently use, all reputable sources:
 - The spamhaus drop lists: https://www.spamhaus.org/drop/
 - A blacklist dropping all traffic from China. For each legitimate visit to my server I get a 1000 illegal ones, enough is enough.
 - tor exit nodes, they are always trying to bruteforce my ssh-server.
 - https://www.blocklist.de

Blocking the ips from these list will save you a lot of useless traffic.

Whilst running the script each file is downloaded and a new set is created and all
ip-addresses in these files are added to a table and are blocked from then on.

## Installation
To set up and install it run the following:

Download the latest version:
```
git clone https://github.com/hboetes/theblackguardscontrol.git
```

Copy it to /etc, there it will save the ip-lists.
```
sudo cp -r theblackguardscontrol/ /etc
```

Run it for the first time
```
sudo /etc/theblackguardscontrol/theblackguardscontrol_generator
```

Check the firewall rules:
```
sudo nft list ruleset | less
```

Install a cronjob, so the rules are updated regularly.
```
sudo ln /etc/theblackguardscontrol_generator /etc/cron.daily/
```

## TODO
Since I don't have ipv6 I have no way to check it, therefore it's currently not supported. PRs are welcome!
Add automatic reports? https://www.blocklist.de/en/download.html#ohnefail2ban
