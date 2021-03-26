# Quote Bot

## Table of Contents

- [Quote Bot](#quote-bot)
  - [Table of Contents](#table-of-contents)
  - [1 description](#1-description)
    - [1.1 quote](#11-quote)
    - [1.2 command](#12-command)
  - [2 deploy](#2-deploy)
    - [2.1 distribute](#21-distribute)
    - [2.2 scp](#22-scp)
    - [2.3 unzip](#23-unzip)
    - [2.4 systemd setup](#24-systemd-setup)

## 1 description

### 1.1 quote

If send the Message Link to text channel, Quote Bot reply content of link.

### 1.2 command

`!quote`: prefix

|option|alias|description|
| ---- | --- | --------- |
|`--version`|`-v`|version|

e.g. `!quote -v`

## 2 deploy

These are all kobi32768's notebook, but it may be helpful.  
kobi32768 not support other environment.

`>` Windows  
`$` Ubuntu

### 2.1 distribute

`> gradle distZip`

### 2.2 scp

Move zipped distribute file on `~/quotebot` with WinSCP

### 2.3 unzip

`$ unzip quotebot-<version>,zip`

### 2.4 systemd setup

Automatically execute latest

Make shell script for bot starting

```bash:start-quotebot.sh
#!/bin/bash

latest=`ls -drt /home/<user>/quotebot/*/ | tail -n 1`
cd $latest
./bin/quotebot
```

Make service file  
`$ ~/micro /etc/systemd/system/quotebot.service`

```ini:quotebot.service
[Unit]
Description=QuoteBot
After=netwowrk.target

[Service]
Restart=always
ExecStart=/home/<user>/start-quotebot.sh

[Install]
WantedBy=multi-user.target
```

Reload systemctl  
`$ systemctl daemon-reload`

Check status  
`$ systemctl list-unit-files | grep quotebot`
