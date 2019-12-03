---
layout: post
title: Export/backup all Grafana dashboards at once
date: '2017-07-12 13:09:35'
---

Grafana is an awesome tool to create graphs from whatever data you have. It doesn't have an option to export all dashboards at once, though. You could select each dashboard and export it to JSON at a time, but that's toil.

There's a better way: Use [grafcli](https://github.com/m110/grafcli). It's a feature-rich Grafana command line tool written in Python. (Python3, of course.) Install it using pip3: 
`pip3 install grafcli`

Now create a config file `grafcli.conf`. As long as it's in your working directory, you're fine:

```
[grafcli]
editor = vim
verbose = off

[hosts]
$GRAFANA_URL = on

[$GRAFANA_URL]
type = api
url = https://$GRAFANA_URL:$PORT
ssl = on
user = admin
password = $GRAFANA_ADMIN_PASSWORD
#token = $GRAFANA_TOKEN

[resources]
data-dir = ~/.grafcli
```

If you have a `token`, you do not need `user`/`password` and vice versa.

To verify if your configuration file is valid, try `grafcli ls remote`. It should show the Grafana URL you have configured. 

To create a backup of all dashboards, use this command: 
`grafcli backup remote/$GRAFANA_URL/ backup.tgz`

Restoring from a backup is simple as well: 
`grafcli restore backup.tgz remote/$GRAFANA_URL/`

Check out the [docs](https://github.com/m110/grafcli#usage) for more options.