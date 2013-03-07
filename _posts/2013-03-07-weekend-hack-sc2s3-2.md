---
layout: post
title: Weekend Hacks 1
author: Whit Morris
comments: true
---

# Streaming around: part 2

This week we'll take a look at streaming the files found via the
soundcloud api last month and stream them into an s3 bucket.

## Gotta have an interface

For hacks, I like CLIDD, command line driven development.  I'll build
a program up a several small pieces that each do something succint and
useful and use the command line to test each.  When I was prototyping [qubota](https://github.com/whitmo/qubota), I used this approach.  In the end I had a

Here I'm going to use
[cliff](https://cliff.readthedocs.org/en/latest/) to create a multi
command set similar to something like `git` or `svn`.  Cliff uses a
class to represent the "app" (the collection of all commands) and then
a class for each "command".  Cliff also offers some formatters for
making nice output.

First we'll edit our setup.py to add a cliff as a dep and register a
couple endpoints that will point to our code.  This will tell python
installation to create an executable script called `sc2s3` and
register a command our app can look for in the `sc2s3.cli` entry point
group.

Afterwards, we'll put some code in `sc2s3.cli` so the script will
execute and cliff will be able to find the sub command.

<script src="https://gist.github.com/whitmo/5112734.js"></script>

Now if we run:

  (hacknight)$ pip install -e ./
  
It will install the new dependencies we added and create the script.

Try it out by running the command.  You should get a prompt:

  (hacknight)$ sc2s3
  (sc2s3) help
  Shell commands (type help <topic>):
  ===================================
  cmdenvironment  edit  hi       l   list  pause  r    save  shell      show
  ed              help  history  li  load  py     run  set   shortcuts

  Undocumented commands:
  ======================
  EOF  eof  exit  q  quit

  Application commands (type help <topic>):
  =========================================
  help  urls   
   
  (sc2s3) urls
  urls
  usage: urls [-h] [-f {csv,html,json,table,yaml}] [-c COLUMN]
              [--quote {all,minimal,none,nonnumeric}]
              clientid username
  urls: error: too few arguments


## Code to execute

Now we have a running cli, we can start populating it with code and testing it (as well as using pdb to explore our code).

  





