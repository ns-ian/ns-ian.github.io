---
layout: post
author: Ian
title: Headless Pi-hole Setup With DietPi
---
Here's a quick account of my experience deploying the Pi-hole application with
a minimal image over SSH.

Pi-hole is a DNS sinkhole that has risen to popularity within the last year or
two. By running the app on your local network (be it on a SBC or a Docker
container), it will filter DNS lookup requests through a block list, before
passing the query on to an upstream provider (Google, Cloudflare, etc). This
allows ad-blocking for any device connected to the network, including those
that don't have an easy solution for blocking advertisements, like smart TVs.
As it blocks ads at the network level, it's less superficial than using a
browser extension, which will simply hide the content.

### Hardware
To get started, I purchased a Raspberri Pi Zero W from
[CanaKit](https://www.canakit.com/raspberry-pi-zero-wireless.html), which came
with the usual accessories: a case, some adapters, a power supply, and a 16 GB
microSD. The W model isn't required, as the same setup can be achieved with a
micro USB to RJ45 adapter, but I figured wireless wouldn't be a big deal for
doing DNS lookups.

### OS
A lot of people seem to be fine with using the default Raspbian OS for this,
which is fine, but I opted to install a minimal image with
[DietPi](https://dietpi.com/), since I don't need a desktop environment. (And I
definitely don't need LibreOffice.)

The image can be flashed to the microSD via
[Etcher](https://www.balena.io/etcher/) or another such tool for creating
bootable media. Although I haven't tried, I don't see why Rufus or plain old
`dd` wouldn't work.

### Setup
I wanted to do a headless installation, which required a couple changes to
2 files in the root directory of the newly flashed image:
* In `dietpi.txt`, set `AUTO_SETUP_AUTOMATED=1` (I also changed my keyboard
layout and locale here)
* In `dietpi-wifi.txt` set `aWIFI_SSID[0]` to the network SSID (in single
quotes), and `aWIFI_KEY[0]` to the password (also in single quotes)

This allowed DietPi to connect to WiFi and go through its setup without any
direct input.

Once I had slotted the microSD into the Pi and connected it to a power supply,
I grabbed a snack and let it go through its automated setup. I'm guessing it
had a setup of 10-15 minutes. Next, I opened my router's DHCP client list, and
looked for the device, which was connected with the hostname DietPi. Since I
was on my Windows machine, I opened up PuTTY and connected to the local IP it
had been assigned, via SSH. The login is `root` with the password `dietpi`.

At this point, the Pi needed a static IP rule in my router's DHCP settings, so
I went ahead and did that. This step will vary from router to router, but it's
usually pretty straightforward (map the Pi's MAC address to whatever local IP
you prefer). I power cycled the Pi after this step to ensure it would connect
to the expected IP.

With that out of the way, I logged back into the Pi and ran the Pi-hole install
script:
```
$ curl -sSL https://install.pi-hole.net | bash
```
There's really nothing worth noting about this step -- it's fully automated,
save for a few choices which require your input (what blocklists you want,
what upstream DNS, etc). Once it finished, I was provided with a password for
logging into the admin web interface, which I saved for reference.

### And..?
The best litmus test I could think of was to open up Edge on my Windows machine
and search for a chili recipe. For some reason, recipe websites are the biggest
offenders for inundating users with disruptive ads. I'm happy to say that I was
able to surf a few of these sites comfortably without a browser extension, so
it's a tentative success! I've done a little more testing with our TV, and I'm
still being served ads via our Internet TV service, but I believe this can be
mitigated by finding the right domain to add to the blocklist.

I have also noticed that a couple of my devices take a tad longer to get a DNS
resolution, but it's still perfectly usable.

Now, anyone who visits and connects their phone to our WiFi will appreciate a
more pleasant web browsing experience. :)
