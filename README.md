![Logo](https://i.imgur.com/PyKLAe7.png)

[![License](https://img.shields.io/badge/license-Public_domain-red.svg)](https://wiki.creativecommons.org/wiki/Public_domain)

About
----

**IPsum** is a threat intelligence feed based on 30+ different publicly available [lists](https://github.com/stamparm/maltrail) of suspicious and/or malicious IP addresses. All lists are automatically retrieved and parsed on a daily (24h) basis and the final result is pushed to this repository. List is made of IP addresses together with a total number of (black)list occurrence (for each). Greater the number, lesser the chance of false positive detection and/or dropping in (inbound) monitored traffic. Also, list is sorted from most (problematic) to least occurent IP addresses.

As an example, to get a fresh and ready-to-deploy auto-ban list of "bad IPs" that appear on at least 3 (black)lists you can run:

```
curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1
```

If you want to try it with `ipset`, you can do the following:

```
sudo su
apt-get -qq install iptables ipset
ipset -q flush ipsum
ipset -q create ipsum hash:net
for ip in $(curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1); do ipset add ipsum $ip; done
iptables -I INPUT -m set --match-set ipsum src -j DROP
```

In directory [levels](levels) you can find preprocessed raw IP lists based on number of blacklist occurrences (e.g. [levels/3.txt](levels/3.txt) holds IP addresses that can be found on 3 or more blacklists).

Wall of shame (2020-02-20)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
89.234.157.254|marylou.nos-oignons.net|11
195.206.105.217|zrh-exit.privateinternetaccess.com|11
18.27.197.252|wholesomeserver.media.mit.edu|10
185.220.102.8|-|10
178.165.72.177|178-165-72-177-kh.maxnet.ua|10
46.165.230.5|tor-exit.dhalgren.org|10
162.247.74.74|wiebe.tor-exit.calyxinstitute.org|10
171.25.193.78|tor-exit4-readme.dfri.se|9
185.107.47.171|tor-exit.r2.darknet.dev|9
46.165.245.154|-|9
162.247.74.27|turing.tor-exit.calyxinstitute.org|9
66.230.230.230|-|9
62.102.148.69|-|9
144.217.255.89|ns542132.ip-144-217-255.net|9
62.102.148.68|-|9
77.247.181.163|lumumba.torservers.net|9
109.70.100.20|tor-exit-anonymizer.appliedprivacy.net|8
195.154.179.3|195-154-179-3.rev.poneytelecom.eu|8
118.70.216.153|-|8
162.247.74.204|billsf.tor-exit.calyxinstitute.org|8
185.220.101.33|-|8
171.25.193.77|tor-exit1-readme.dfri.se|8
176.10.104.240|tor1e1.digitale-gesellschaft.ch|8
185.220.101.28|-|8
185.220.101.27|-|8
185.220.101.24|-|8
192.42.116.16|tor-exit.hartvoorinternetvrijheid.nl|8
92.63.194.104|-|8
104.244.76.245|zarathustra.tor.k0nsl.org|8
77.247.181.162|chomsky.torservers.net|8
167.88.7.134|the-windy-onion.tor-exits.alec.ninja|8
185.220.102.7|-|8
162.247.74.216|phoolandevi.tor-exit.calyxinstitute.org|8
162.247.74.213|snowden.tor-exit.calyxinstitute.org|8
171.25.193.235|tor-exit3-readme.dfri.se|8
176.10.99.200|accessnow.org|8
95.211.230.211|-|8
199.195.254.80|bvm.cybermilitia.net|8
45.148.10.143|-|8
77.247.181.165|politkovskaja.torservers.net|8
158.174.122.199|h-122-199.A357.priv.bahnhof.se|8
62.210.105.116|62-210-105-116.rev.poneytelecom.eu|8
