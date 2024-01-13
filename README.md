This script generates a blacklist for nftables from various ip lists:

Let's have a look at that code:

```
feed=(
    https://www.spamhaus.org/drop/drop.txt
    https://www.spamhaus.org/drop/edrop.txt
    https://raw.githubusercontent.com/herrbischoff/country-ip-blocks/master/ipv4/cn.cidr
    https://raw.githubusercontent.com/SecOps-Institute/Tor-IP-Addresses/master/tor-exit-nodes.lst
)
```

So each file is downloaded and a new set is created and all ip addresses in
these files are added to the tables and are blocked from then on.

To set up and install it run the following:

Download the latet version
```
git clone https://github.com/hboetes/theblackguardscontrol.git
```

Copy it to /etc, there it will save the ip-lists as well.
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

Install a cronjob, so the rules are regularly updated.

```
sudo ln /etc/theblackguardscontrol_generator /etc/cron.weekly/
```
