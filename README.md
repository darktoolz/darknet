# darknet auto proxy .i2p + .onion linux docker
Usage:
- install docker
- `git clone https://github.com/darktoolz/darknet.git` and `cd darknet`
- `docker compose -f docker-compose.yml up -d` for everything up & running
- set `127.0.0.1:8118` HTTP/HTTPS proxy in system/browser

## defaults
- service should start at system startup
- using `darknet` as docker compose project name
- no `ipv6`
- docker images try to be `read_only: true` except for data volumes

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

## use proxy as default by GNOME and browsers
- open `settings` / `network` / `network proxy`
- set `127.0.0.1` and `8118` for both `HTTP` and `HTTPS` proxy
- adjust `NO_PROXY` settings

## use proxy as default by linux tools
To allow most linux tools to use proxy by default (note on `http://` for both protocols) add similar to shell config (something like `.bashrc`, `.profile`):
```bash
export http_proxy=http://127.0.0.1:8118
export https_proxy=http://127.0.0.1:8118
export HTTP_PROXY=http://127.0.0.1:8118
export HTTPS_PROXY=http://127.0.0.1:8118
export no_proxy=localhost,127.0.0.0/8
export NO_PROXY=localhost,127.0.0.0/8
```

## .gitconfig
```
[http]
  proxy = http://127.0.0.1:8118
[https]
  proxy = http://127.0.0.1:8118
```

## how to use tor bridges
To configure usage of tor bridges add `BRIDGES` env var to `.env` file in same dir using format like this:
```
BRIDGES="
Bridge obfs4 1.2.3.4:1234 1FB788ACEFB2............A0F3CAFC35CC6203 cert=... iat-mode=0
Bridge obfs4 2.3.4.5:2345 ... cert=... iat-mode=0
"
```

## potential conflicts
- stop other tor/i2p services before install/run
