[TOC]


## Launching Applications
The launching of applications in Mac OS is confusing to many, espcially when you have to change global settings, say environment variables, to the application. Here are some tips and todos to the topic.


### Environment Varaibles


#### Maverick
When `bash` is invoked as an interactive login shell, or as a non-interactive shell with the `--login` option, it reads and executes commands, from the first of these files, that exists and is readable, in the listed order:

1. /etc/profile
2. ~/.bash_profile
3. ~/.bash_login
4. ~/.profile

If bash is invoked with the name `sh`, it tries to mimic the startup behavior of historical versions of sh as closely as possible, while conforming to the POSIX standard as well. When invoked as an interactive login shell, or a non-interactive shell with the --login option, it first attempts to read and execute commands from /etc/profile and ~/.profile, in that order.

The above said, there is no need to go through all those manually. One can run the following to achieve the goal, in terminal:
```bash
launchctl setenv PATH $PATH
```
Some said that one can modify the file
```text
/etc/launchd.conf
```
for the purpose. However, I've found that not all (at least not mine) boxes have this file. So it seems the `launchctl` approach is much safer to do.

#### prior to Mavericks
Besides the aforementioned list of files, there was also the
```text
~/.MacOSX/environment.plist
```
and the (on Mountain Lion)
```text
/etc/environment
```
All these files, except `launchctl`, I haven't tried, because some of them doesn't exist in my box, and some seems not safe in my case.
