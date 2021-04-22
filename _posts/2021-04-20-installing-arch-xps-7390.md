---
layout: post
author: Ian 
title: Arch Installation on Dell XPS 13 (7390)
---
This post serves as an account of, as well as an instructional reference for,
the quirks of installing Arch GNU/Linux on the XPS 13 7390.

I recently purchased one of these machines new, and decided that I wanted Arch
to be the OS that I would install on it. Previously I had installed Arch on my
ThinkPad X220, but that machine's age and ubiquity meant that I didn't really
run into any hiccups - most things "just worked" thanks to native kernel
support. Since the 7390 revision of the popular XPS 13 is less than 2 years old
at the time of this writing, there were a few extra things to work through.

Firstly, the community wiki is the definitive reference for getting Arch running
on any compatible machine. In addition to the [installation
guide](https://wiki.archlinux.org/index.php/Installation_guide), there are also
many individual pages dedicated to device-specific issues and tips. See these
pages for the usual procedure for installation of the base system. I've also
found the wiki to be an excellent reference for other popular software, and for
Unix in general.

#### Disabling PSR
Panel Self Refresh is a power-saving measure that aims to cut
down on unnecessary display refreshes of static content. With Intel's i915
chipset, a kernel bug (?) causes the display to flicker on some machines. On
mine, the display would randomly corrupt completely. Adding `i915.enable_psr=0`
as a kernel option fixes this issue, at the cost of the battery life it would
otherwise save.

#### Fixing GTK3 Scaling
Although the configuration I purchased includes a 1080p
screen at 96 DPI, I found that I had scaling issues on Firefox. Initially I
believed this to be an issue with Wayland (I'm attempting to leave X behind),
but Firefox appeared incredibly tiny in both Sway and i3. The fix I landed on
was setting the environment variable `GDK_DPI_SCALE` to 1.3. This seemed to be
the best option, as Sway does support fractional scaling for the whole display,
but seems to discourage it in their documentation. A similar fix may be required
for apps running QT frontends; I haven't tried one yet.

#### Adjusting Display Brightness
The Arch wiki page for this machine advises installing the `acpilight` package,
and setting a udev rule, in addition to adding `acpi_backlight=vendor` as a
kernel parameter. However I found it was much easier to install `brightnessctl`
and add the keymap `bindsym XF86MonBrightnessUp exec brightnessctl set +2%` and
a similar mapping for lowering the brightness.

Overall, the installation went very smoothly, and there aren't too many gotchas
to be concerned about. I may do a followup to this post in the future if I run
into more unexpected and/or obscure issues, though.
