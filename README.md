### Prolog

This is a file which I collect some useful for me tips and tricks.

See list: 

1. [increase upload max limit in Wordpress, PHP8.0-fpm and Nginx](#increase-upload-max-limit-in-wordpress-php80-fpm-and-nginx)
2. [some hosts in Zabbix aren't visible](#some-hosts-in-zabbix-arent-visible)
3. [how to cut a last X characters from various size of strings input](#how-to-cut-a-last-x-characters-from-various-size-of-strings-input)
4. [how to make bash history stick and searchable](#how-to-make-bash-history-stick-and-searchable)
5. [notification isn't send to all members in Zabbix groups](#notification-isnt-send-to-all-members-in-zabbix-groups)
6. [how to check size of Docker images](#how-to-check-size-of-docker-images)
7. [some useful commands of using Docker software](#some-useful-commands-of-using-docker-software)
8. [convert video files to audio files](#convert-video-files-to-audio-files)
9. [how to return to the previous directory](#how-to-return-to-the-previous-directory)
10. [how to copy variables during PHPStorm debug session](#how-to-copy-variables-during-phpstorm-debug-session)
11. [how to delete git branch](#how-to-delete-git-branch)
12. [how to force GPG use expired key](#how-to-force-gpg-use-expired-key)
13. [how to detect file character encoding](#how-to-detect-file-character-encoding)
14. [how to check php language syntax from the command line](#how-to-check-php-language-syntax-from-the-command-line)
15. [how to replace voice to text](#how-to-replace-voice-to-text)
16. [how to extract one dir from large tar archive](#how-to-extract-one-dir-from-large-tar-archive)
17. [how to renew an expired encryption subkey with gpg](#how-to-renew-an-expired-encryption-subkey-with-gpg)
18. [how to trim spaces in string](#how-to-trim-spaces-in-string)
19. [how to start Firefox web browser in safe mode](#how-to-start-firefox-web-browser-in-safe-mode)
20. [print only digits using grep](#print-only-digits-using-grep)
21. [simple access to website with secret cookie](#simple-access-to-website-with-secret-cookie)
22. [escape spaces in bash](#escape-spaces-in-bash)
23. [how to setup global gitignore rules](#how-to-setup-global-gitignore-rules)
24. [how to make bash for loop](#how-to-make-bash-for-loop)
25. [how to "normalize" caller id in Asterisk](#how-to-normalize-caller-id-in-asterisk)
26. [an infinite loop in single-line bash](#an-infinite-loop-in-single-line-bash)
27. [how to get a file directory path from file path](#how-to-get-a-file-directory-path-from-file-path)
28. [how to use htmlq software](#how-to-use-htmlq-software)
29. [how to replace spaces with underscore in file names using a bash](#how-to-replace-spaces-with-underscore-in-file-names-using-a-bash)
30. [how to concatenating several .mp3 files into one .mp3](#how-to-concatenating-several-mp3-files-into-one-mp3)
31. [how to escape spaces in path for scp copy](#how-to-escape-spaces-in-path-for-scp-copy)
32. [how to get destination number from SIP datagram](#how-to-get-destination-number-from-sip-datagram)
33. [pretty print json](#pretty-print-json)
34. [useful bash script settings](#useful-bash-script-settings)
35. [some useful curl flags](#some-useful-curl-flags)
36. [ssh reverse tunnel](#ssh-reverse-tunnel)
37. [phpstorm debugging browser's add-on](#phpstorm-debugging-browsers-add-on)
38. [remove ^M carriage return](#remove-m-carriage-return)
39. [git how to push to all remotes](#git-how-to-push-to-all-remotes)
40. [git how to recover dropped stashes](#git-how-to-recover-dropped-stashes)
41. [how to distinguish null from empty string in psql](#how-to-distinguish-null-from-empty-string-in-psql)
42. [how to download files parallel](#how-to-download-files-parallel)
43. [how to see PWD of the process](#how-to-see-pwd-of-the-process)
44. [how to unzip a multipart spanned zip on linux](#how-to-unzip-a-multipart-spanned-zip-on-linux)
45. [how to see differenct between two text file](#how-to-see-differenct-between-two-text-file)
46. [find and delete all empty directories](##find-and-delete-all-empty-directories)

### increase upload max limit in Wordpress, PHP8.0-fpm and Nginx

Settings form `location /` and `location /wp-admin` there aren't cascading and nginx
processes them separately.

[top](#prolog)

### some hosts in Zabbix aren't visible

If you have a monitored host try "Full clone" instead of create a new one.

[top](#prolog)

### how to cut a last X characters from various size of strings input

If you want cut, for example, an extension of files, try `rev` twice, i.e.

```bash
ls *.mp4 | rev | cut -c 5- | rev
```

[top](#prolog)

### how to make bash history stick and searchable

First, make a directory `mkdir ~/.logs`

Second, add to `~/.bashrc` this entry 
```bash
export PROMPT_COMMAND='if [ "$(id -u)" -ne 0 ]; then echo "$(date "+%Y-%m-%d.%H:%M:%S") $(pwd) $(history 1)" >> ~/.logs/bash-history-$(date "+%Y-%m-%d").log; fi'
```

After restart bash shell, you will have a daily log of all shell commands like this:

```bash
$ cat ~/.logs/bash-history-2021-06-20.log
(...)
2021-06-20.11:28:52 /home/tom   500  cat ~/.bashrc
(...)
```

[top](#prolog)

### notification isn't send to all members in Zabbix groups

If you have a proper configuration and despite this, notifications aren't sent check and set properly user's permissions.

[top](#prolog)

### how to check size of Docker images

```bash
$ docker images --format "{{.ID}}\t{{.Size}}\t{{.Repository}}" | sort -k 2 -h | grep postgres
```

[top](#prolog)

### some useful commands of using Docker software

#### how to mount volume and bind port

```bash
$ docker run -v /<path_on_host>:/<path_inside_container> -p <external_port_on_host>:<internal_port_on_container> -it --entrypoint <command_to_run_on_container> <image>
```
#### how to copy file/directory from container to host

```bash
$ docker cp <container_id>:/<path_inside_container> <path_on_host>
```
#### how to copy file/directory from host to container

```bash
$ docker cp <path_on_host> <container_id>:/<path_inside_container>
```

#### how to log into running container

```bash
$ docker exec -it <container_name> <shell>
```

#### how to expose range of ports

```bash
$ docker run --expose=7000-8000 -p 7000-8000:7000-8000
```

#### how to removing all unused docker objects

```bash
$ docker system prune
```

#### how to set restart automatically

See how to [start containers automatically](https://docs.docker.com/config/containers/start-containers-automatically/).

[top](#prolog)

### convert video files to audio files

```bash
$ ls *.mp4 | rev | cut -c 5- | rev | xargs -n 1 -I %  sh -c 'ffmpeg -i "%.mp4" "%.mp3"'
```
[top](#prolog)

### how to return to the previous directory

```bash
$ cd -
```

[top](#prolog)

### how to copy variables during PHPStorm debug session

See the linked answer

[Is there a way to copy a data structure from the 'Variables' window in the debugger?](https://stackoverflow.com/a/28487879)

[top](#prolog)

### how to delete git branch

delete locally branch

```bash
$ git branch -d <localBranch>
```

delete remote branch

```bash
$ git push origin --delete <remoteBranch>
```

[top](#prolog)

### how to force GPG use expired key

Use `--faked-system-time` option, for example

```bash
$ gpg2 --faked-system-time 20100101T000000 -e -r keyid
```

[top](#prolog)

### how to detect file character encoding

```bash
$ enca -L <language> <file>
``` 

[top](#prolog)

### how to check php language syntax from the command line

Simply, type

```bash
$ php -l <filename>
```

If the syntax in the file is correct you will see this:

`No syntax errors detected in <filename>`

[top](#prolog)

### how to replace voice to text

1. Download [voice2json](https://voice2json.org) command-line tool.

2. Train for defined phrases in sentences.ini (see docs how)

3. Record audio to wav file

4. Replace using this tool command
	```bash
	$ voice2json --profile <language> transcribe-wav < ~/path/to/file.wav | jq .text
	```
[top](#prolog)

### how to extract one dir from large tar archive

```bash
$ tar -xvf foo.tar home/foo/bar # Note: no leading slash
```

[top](#prolog)

### how to renew an expired encryption subkey with gpg

See [how to renew an expired encryption subkey with gpg](https://unix.stackexchange.com/questions/552707/how-to-renew-an-expired-encryption-subkey-with-gpg).

After edit key send it to hkp(s) server

```bash
$ gpg --send-keys --keyserver keyserver.ubuntu.com <your-key-id>
```

[top](#prolog)

### how to trim spaces in string

```bash
$ echo "  Text with spaces   " | sed -e 's/^[ \t]*//'
```

[top](#prolog)

### how to start Firefox web browser in safe mode

This command starts Firefox with all Add-on's disabled.

```bash
$ firefox --safe-mode
```

[top](#prolog)

### print only digits using grep

```bash
$ echo <string> | grep -o '[0-9]\+'
```

[top](#prolog)

### simple access to website with secret cookie

```bash
$ cat fy_LONG_UNIQUE_STRING_g3ufyg3uyfg3487ftu.php
<?php
 
setcookie('secret', 'fr3iufhr3i_HERE_IS_MY_SECRET_PHRASE_hr3ugi3rug');
header('Location: /?'.rand());
 
$ head .htaccess
RewriteEngine on
 
SetEnvIf Cookie "secret=fr3iufhr3i_HERE_IS_MY_SECRET_PHRASE_hr3ugi3rug" secret-cave=open
RewriteCond %{REQUEST_URI} !^/fy_LONG_UNIQUE_STRING_g3ufyg3uyfg3487ftu.php$
RewriteCond %{ENV:secret-cave} !open
RewriteRule (.*) https://google.com
```
 
if you visit: https://example.com/fy_LONG_UNIQUE_STRING_g3ufyg3uyfg3487ftu.php 
then you unlock access to website, otherwise you will be redirect to Google site.

[top](#prolog)

### escape spaces in bash

```bash
$ echo <string with spaces> | tr " " "\ "
```

[top](#prolog)

### how to setup global gitignore rules

```bash
$ git config --global core.excludesFile '~/.gitignore'
```

[top](#prolog)

### how to make bash for loop

use `seq` command to generate data for loop

```bash
for i in $(seq 1 250)
```

[top](#prolog)

### how to "normalize" caller id in Asterisk

below code save the last 9 digit of `CALLERID(num)` in variable foo

```
same => n,Set(foo=${FILTER(0-9,${SHELL(echo ${CALLERID(num)} | grep -o '[0-9]\+' | rev | cut -c -9 | rev)})})
```

[top](#prolog)

### an infinite loop in single-line bash

```bash
$ while :; do echo 'Hit CTRL+C'; sleep 1; done
```

[top](#prolog)

### how to get a file directory path from file path

```bash
$ DIR=$(dirname <file>)
```

[top](#prolog)

### how to use htmlq software

[htmlq](https://github.com/mgdm/htmlq) is like jq, but for HTML. See project page at GitHub.

Example how to extract all links urls from site (from project's [README](https://github.com/mgdm/htmlq/blob/master/README.md)).

```bash
$ curl --silent https://www.rust-lang.org/ | htmlq --attribute href a
/
/tools/install
/learn
/tools
/governance
/community
https://blog.rust-lang.org/
/learn/get-started
https://blog.rust-lang.org/2019/04/25/Rust-1.34.1.html
https://blog.rust-lang.org/2018/12/06/Rust-1.31-and-rust-2018.html
[...]
```

[top](#prolog)

### how to replace spaces with underscore in file names using a bash

```bash
$ for f in *\ *; do mv "$f" "${f// /_}"; done
```

[top](#prolog)

### how to concatenating several .mp3 files into one .mp3

```bash
$ sudo apt-get install mp3wrap
$ mp3wrap output.mp3 *.mp3
```

[top](#prolog)

### how to escape spaces in path for scp copy

See [StackOverflow answer](https://stackoverflow.com/questions/19858176/how-do-i-escape-spaces-in-path-for-scp-copy-in-linux)

[top](#prolog)

### how to get destination number from SIP datagram

in file `/etc/asterisk/extension.conf` put

```bash
(...)
same => n,Set(VALTO=${SIP_HEADER(To)})
same => n,Set(VALTO=${CUT(VALTO,:,2)})
same => n,Set(NORMDST=${CUT(VALTO,@,1)})
(...)
```
`NORMDST` variable will include destination number

[top](#prolog)

### pretty print json

```bash
cat example.json | python -m json.tool
```

[top](#prolog)

### useful bash script settings

in short use this setting in bash script (see help to explanation)

```bash
#!/bin/bash
set -euxo pipefail
```

[top](#prolog)

### some useful curl flags

in short use some of this flags (see help)

```bash
curl --fail --silent --show-error --location --insecure
```

[top](#prolog)

### ssh reverse tunnel

[forward ports with a reverse SSH tunnel](https://github.com/openoms/bitcoin-tutorials/blob/master/ssh_tunnel.md)

[top](#prolog)

### phpstorm debugging browser's add-on

if you use some browser's extension in extension's tab, for example to graphql
query and you want debug them, you have to open another tab with normal view
(frontend or admin) of debugging web aplication and set it in debug mode to
set properly cookie with debug on and allow to debug code in PHP Storm IDE.

[top](#prolog)

### remove ^M carriage return

[sed Delete / Remove ^M Carriage Return (Line Feed / CRLF) on Linux or Unix](https://www.cyberciti.biz/faq/sed-remove-m-and-line-feeds-under-unix-linux-bsd-appleosx/)

[top](#prolog)

### git how to push to all remotes

[Able to push to all git remotes with the one command?](https://stackoverflow.com/questions/5785549/able-to-push-to-all-git-remotes-with-the-one-command)

[top](#prolog)

### git how to recover dropped stashes

List hash of all dropped stashes and make a separate branch of each:

`git fsck --no-reflog | awk '/dangling commit/ {print $3}' | xargs -L1 -I R git branch dropped-R R`

Next, checkout of every branch (named `dropped-{sha1 hash}`) and find your dropped changes.

Based on [this SO answer](https://stackoverflow.com/questions/89332/how-to-recover-a-dropped-stash-in-git).

[top](#prolog)

### how to distinguish null from empty string in psql

When you have a record with empty string or null value
is not easy to distinguish each other in standard
psql settings.

Execution of below command replaces display of null
value with the given string.

`\pset null '<null>'`

[top](#prolog)

### how to download files parallel

We can call wget for each line in files.txt with a maximum of two processes `-P` in parallel

`cat files.txt | xargs -n 1 -P 2 wget -qc`

[top](#prolog)

### how to see PWD of the process

Simply find the process id `PID` and run

`pwdx $PID`

[top](#prolog)

### how to unzip a multipart spanned zip on linux

`cat test.zip.* >test.zip`
`zip -FF test.zip --out test-full.zip`
`unzip test-full.zip`

[top](#prolog)

### how to see differenct between two text file

Use `comm` command with two sorted files (see manpage how to do it)

[top](#prolog)

### find and delete all empty directories

Follow this [SO answer](https://stackoverflow.com/questions/2810838/finding-empty-directories).

[top](#prolog)
