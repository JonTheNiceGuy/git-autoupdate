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

`git-autoupdate -r 5`
Report an issue with the upstream every 5 checks
