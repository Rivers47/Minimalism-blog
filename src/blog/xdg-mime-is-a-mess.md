---
title:  Default application is a mess without Desktop Environment
description: A rant on XDG
tags: ["post", "linux"]
date: 2022-11-02
location: 迷いの竹林
layout: article.njk
permalink: "blog/{{ title | slugify }}.html"
---

[XDG MIME Applications](https://wiki.archlinux.org/title/XDG_MIME_Applications)

[desktop entries](https://wiki.archlinux.org/title/desktop_entries)

In addition to XDG, pcmanfm-qt attempts to manage file association on its own, which creates .desktop files in `~/.local/share/applications` I believe. .desktop files in this dir have precedence over those in `/usr/share/applications/` or `/usr/local/share/applications/`, but the way it creates these files is not that useful.


Had to deal with these because I'm using feh as the default image viewer but it doesn't support reading config files so everything has to be read from command line (well it does support changing key bindings but nothing more)

 

 

Useful debug:

```
export XDG_UTILS_DEBUG_LEVEL=10
xdg-mime query filetype /tmp/foobar.png
xdg-mime query default major/minor
```
let's you to see which mimeapps.list is scanned 

It's also possible that you are using `gio` from `glib2` which completely ignores `.config/mimeapp.list`, use it instead when xdg-mime isn't working.