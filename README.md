# TKCTF

This is a template for your docker image that will be used to host
your CTF challenge.

## Overview

Download the template from the course website and unzip it.

~~~~{.sh}
    $ wget https://tc.gts3.org/cs6265/2026-fall/_static/ctf-template.zip
    $ unzip ctf-template.zip

    $ cd ctf-template
    $ make help
    prepare: prepare a docker image for compilation
    build  : build the target
    dist   : build the docker image
    release: build the target, docker image and release them
    run    : run the docker container
    exploit: launch the exploit
    test   : test the docker/exploit
    submit : zip for submission
~~~~

Keep in mind that the best challenge should be fun and educational. Please don't
design the challenge that requires any random/pure guessing (but well-designed
bruteforcing is fine).

You can replicate real security vulnerabilities, like `mini-sudo` or
`mini-heartbleed`. There are a few sources that you can refer:

- <https://ctftime.org/>
- <https://www.cvedetails.com/>
- <https://www.exploit-db.com/>

## Structure

~~~~{.sh}
    /NAME                : team-name:challenge-name (e.g., `staff:fmtstr`)
    /PORT                : a port number

    # all files to run your service
    /docker/Dockerfile   : Dockerfile
           /target       : target binary
           /flag         : follow this format: tkctf{please submit this flag!}

    # all files to be released to participants
    /release/README.md   : guideline
            /target      : target binary, if you want to release

    # source/exploit for your team and organizer
    /source/Dockerfile   : Dockerfile for the build environment
           /exploit.py   : exploit code
           /test.sh      : run docker, run exploit.py and print out flag
           /writeup.txt  : solution
           /src/         : source code
~~~~

## Workflow

1. Change the `NAME` file to your challenge name: `teamname:challenge`
   (e.g., `staff:fmtstr`)
2. Change the `docker/flag` file as you wish, but wrap it inside `tkctf{...}`
   (e.g., `tkctf{please submit this flag!}`)
3. `make prepare` to build a docker container for the build process
4. Design your challenge under `source/src/`
   - All code and Makefile go to `source/src/`
   - See `source/src/Makefile` to enable/disable mitigation
   - Put `README.md` under `release/README.md`
   - `make build` to build the challenge
5. `make dist` to prepare a docker image for exploitation
6. Put an exploit to `source/exploit.py`
   (e.g., `make run` and `make exploit`)
7. Make sure everything is ready with `make test`
8. `make release` to rebuild everything and copy the target to `release/`
   - Check what's included in `/release/`
9. `make submit` to zip your challenge to `../<NAME>.zip`, 
   upload it to a shareable link, 
   and submit the link through the form printed by `make submit`

The source code of the challenge locates in `source/src/`, which
contains its source (`fmtstr.c`) and makefile (`Makefile`).
The makefile includes various defense options you can enable
(e.g., `CFLAGS += -fstack-protector`). Please carefully enable them
as you'd like for your challenge.

## Checklist for submission

1) `/NAME`: Team/challenge name
2) `/release/README.md`: Description about the challenge
3) `/release/target`: the target binary to release
3) `/release/*`: anything else you would like to make public (e.g. libc)
5) `/docker/flag`: Flag!
6) `/source/writeup.txt`: Your description on the challenge and solution
7) `/source/exploit.py`: Your _working_ exploit
8) Make sure `make test` works!

## The game day
- The organizer will run `make dist` to prepare the docker image
- The organizer will release `/release/*` via CTFd
- Your docker image will be monitored with your exploit script
