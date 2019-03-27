# iptables-raw-POSTROUTING
Add POSTROUTING chain to iptables raw table

## Why this patch?
In order to match packets after SNAT.  
Originally, there's no chain after the nat POSTROUTING chain  
![Netfilter packet flow](https://upload.wikimedia.org/wikipedia/commons/3/37/Netfilter-packet-flow.svg)
In some cases we want to match packets (e.g. `-j LOG`) after being SNAT'ed, but we cannot add rules to the nat POSTROUTING chain because it only matches `--ctstate NEW` packets.  
So I created this patch. I didn't introduce a new table because it requires modification to netns (`struct net`) as well.
