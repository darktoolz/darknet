# darknet auto proxy .i2p + .onion linux docker
Usage:
- install docker
- `git clone https://github.com/darktoolz/darknet.git` and `cd darknet`
- `docker compose -f docker-compose.yml up -d` for everything up & running
- set `127.0.0.1:8118` HTTP/HTTPS proxy in system/browser

Defaults:
- service should start at system startup
- is uses `darknet` as docker compose project name

## actions (run in the same dir where docker-compose.yml located)
- to update images: `docker compose pull --ignore-pull-failures --policy always`
- to stop or start: `docker compose stop` or `docker compose start`
- destroy completely: `docker compose down -v --remove-orphans`

## other actions
- `ps`: `docker compose -p darknet ps`: check status
- `logs`: `docker compose -p darknet logs`: logs

Full list of commands: `docker compose -h`

## depends on
- `https://github.com/darktoolz/privoxy`
- `https://github.com/darktoolz/tor`
- `https://github.com/darktoolz/i2p`

## to allow linux tools to use proxy by default (note on `http://` for both protocols):
```bash
export http_proxy=http://127.0.0.1:8118
export https_proxy=http://127.0.0.1:8118
export HTTP_PROXY=http://127.0.0.1:8118
export HTTPS_PROXY=http://127.0.0.1:8118
export no_proxy=localhost,127.0.0.0/8
export NO_PROXY=localhost,127.0.0.0/8
```

## notes
- stop other tor/i2p services before install/run
- if you set env vars in `.bashrc` / `.profile`:
  - `unset http_proxy https_proxy HTTP_PROXY HTTPS_PROXY` before running update/stop/start/up action
