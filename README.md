## My custom instructions:

1. Clone to `/opt/mailcow-dockerized`
2. Create the Btrfs subvolume `/var/lib/mailcow-dockerized`
3. Add original repo as upstream:
  ```bash
  git remote add upstream https://github.com/mailcow/mailcow-dockerized.git
  ```

## Every time u wanna update, don't use their script, just:

1. Run:
```bash
git fetch upstream
git merge upstream/master
```
2. Manage the conflicts in the compose
3. Run:
```bash
docker compose pull && \
docker compose up -d --remove-orphans && \
docker image prune -f
```

## Comments:

- I'd love to move all confs (mainly `data/conf`) to `/etc/mailcow-dockerized` on top of all the data moved to `/var/lib/mailcow-dockerized`, but I can't: they change stuff from time to time. Pulling from upstream is useful to be in control, but I'll just let them manage the confs after a quick check everytime
- Remember not to set to `restart: unless-stopped` cuz u need max uptime possible
- For todo stuff, see the [issues](https://github.com/xX-MrN0b0dy-Xx/mailcow-dockerized/issues)
