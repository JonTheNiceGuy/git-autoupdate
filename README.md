# git-autoupdate for remote repositories
This is a Bash script which checks the upstream server for your git repository, and, so long as it exists and is 
responsive to ping, it will do a git fetch, confirm there's a git merge (by checking the logs) and then performs a merge.

It has a simple "no response" test based on pings, and will parse the git config to find both SSH and HTTP(S) 
upstream repositories. Other upstreams are not detected, short of advising you they can't parse them for upstream 
detection.

You can also have it execute actions if a merge is performed (for example `jekyll build -d /path/to/tree` or `../bin/build_svc.sh`)

```
git-autoupdate - Check response of your git remote

-t <statefile> - where to place the statefile                        - default ~/.state_git_remote
-r <number>    - after how many checks to re-report upstream failure - default 30
-e <action>    - script to execute once the update is done           - default <none>
-s <path>      - location of the source tree to update               - default $PWD
```

## Examples
`git-autoupdate -s /var/www/source -e "jekyll build -d /var/www/site -s /var/www/source" -r 15`
Rebuild a Jekyll based site in /var/www/site based on the source in /var/www/source and alert if the upstream fails to respond after the 15th attempt.

## Notes
This script will "alarm" if there is no upstream (e.g. you've checked out a branch with no defined upstream) or if the upstream is in your filesystem (e.g. `git clone /home/user/test/.git /opt/test_service`). It will only signal this alarm once.

## Tips, Tricks, and other Suggestions welcome!
This script scratches a specific pair of itches for me.

1. It polls an upstream source (e.g. github) via a cronjob, and if that source isn't responding (perhaps a DDOS is underway), then it doesn't spam your mailbox about it.
2. It can optionally build, via "magic" (aka detecting when something has changed) the source into a built product... effectively turning this into a very simple CI system :)

If this script is _*NEARLY*_ enough for you, but you need it to do something else, please *LET ME KNOW* - there's an "issues" thingy up the top there, please use it! If you're not comfortable using Github issues (or you don't have an account on here!), please fire an [email to me](mailto:jon@sprig.gs), so I can raise it for you. If you see something on here that you want to fix, PLEASE DO! (I'd say I'll love you forever, but I have a wife and children who might disapprove ;) )
