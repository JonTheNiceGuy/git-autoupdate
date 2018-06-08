# simple-git-autoupdate-for-jekyll

This is a simple Bash script which checks the upstream server for your jekyll git repository, and, so long as
it exists and is responsive to ping, it will do a git fetch, confirm there's a git merge (by checking the logs)
and then performs the merge.

It has a simple "no response" test based on pings, and will parse the git config to find both SSH and HTTP(S) 
upstream repositories. Other upstreams are not detected, short of advising you they can't parse them for upstream 
detection.
