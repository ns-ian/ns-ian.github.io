---
layout: post
author: Ian
---
Back in college, I took an elective on developing for the web, but found the
course to be too rudimentary. So, in the summer before my last semester, I
decided to make my own personal space on the web from the ground up.

Configuring the server and database, setting up deployment hooks, writing
the code⁠all of that. I ended up learning a lot of what I set out to learn,
and also some things that I hadn't thought about. (It was my first practical
exposure to Node, MVC architecture, MongoDB, and JavaScript in general). DNS
records, SSH, security certificates, and database auth started out as
roadblocks that I was impatient to move beyond, but now I look back on them
with some satisfaction.

Now, my needs have shifted. I'm employed as a software engineer for a large
company, so I don't feel that I have as much to prove when I find myself back
in the job market. It has become a nuisance to manage even a small website:
security vulerabilities creep up in dependencies, domains and certificates need
to be continually renewed, and I've even forgotten my credentials to some of
the security measures *I* set up. Just for context, this was an EC2 instance
running Ubuntu.

Static site generators seemed like an easy, but robust enough alternative. I
had previously flirted with [Hexo](https://hexo.io/), but GitHub Pages offers
better integration with [Jekyll](https://jekyllrb.com/), and their hosting is
free. So far, I'm pretty happy with the results; it was extremely easy to set
up, and my only headache stemmed from my own inexperience with Bootstrap and
building responsive layouts. The Liquid templating language feels just like
Embedded Ruby, and writing posts like this one in Markdown is already familiar.

I'm only saving a few bucks a month by switching, but it's nice to have a
clean, functional space online again. :)
