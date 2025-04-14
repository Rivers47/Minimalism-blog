---
title:  Change SwayWM wallpaper with a user systemd service
description: Randomly change wallpaper with swaybg using systemd service however you want
tags: ["post", "linux"]
date: 2025-04-12
location: 迷いの竹林
layout: article.njk
permalink: "blog/{{ title | slugify }}.html"
---

This post is inspired by [this blog post](https://sylvaindurand.org/dynamic-wallpapers-with-sway/)
with a few modifications. 

This is my script. 
```
#!/bin/bash
echo start wallpaper service
pkill swaybg
while :; do
	path=$(find '/home/rivers/Pictures/WallPaper' -type f | shuf -n1)
	echo "$path"
	swaybg -i "$path" --mode fill & 
	if [ $PID ]; then
		sleep 1
		kill $PID
	fi
	PID=$!

	#custom logic on wait time before changing wallpaper again
	sleep $(expr $RANDOM / 100 + 300 )
done
```
The `pkill` at the beginning of the script might be unncessary, but it's
there just in case. I am not sure if a process can kill processes outside
of its cgroup to be honest. The `sleep 1` is necessary because the 
new swaybg process needs sometime to load the image file. If the old process
is killed instantly there will still be a black screen in between.
The 1 second interval may need to be larger if you are reading big files
from a network mounted drive, for instance.

Initially I tried to use systemd timers to achieve this, but it does 
not work well with the requirement that you need to start a new 
process before killing the old one. Also systemd timers don't allow
setting more complicated logic of delay times.

So, to make this a systemd (user) unit that start automatically on
your login, create this in `~/.config/systemd/user`

```
[Unit]
Description=change wall paper
#ConditionEnvironment=WAYLAND_DISPLAY
Wants=sway-session.target
After=sway-session.target

[Service]
ExecStart=%h/.config/systemd/user/changeWallpaper.sh
Restart=always

[Install]
WantedBy=default.target
```
The `ConditionEnvironment` should needed because the service needs to start after the wayland compositor
is up, but I haven't found a way to make the unit start reliably after wayland.
