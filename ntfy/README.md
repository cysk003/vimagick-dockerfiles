ntfy
====

[ntfy][1] (pronounced "_notify_") is a simple HTTP-based pub-sub notification service.
With ntfy, you can **send notifications to your phone or desktop via scripts** from
any computer, **without having to sign up or pay any fees**.

## up and running

```bash
$ mkdir -p data/{etc,log,var}
$ docker compose up -d
$ docker compose exec nify sh
>>> ntfy user add pi
>>> ntfy user add --role=admin kev
>>> ntfy user list
>>> ntfy access pi test rw
>>> ntfy access '*' test ro
>>> ntfy access
>>> ntfy token add --expires=30d --label=pi5 pi
>>> ntfy token add --expires=90d --label=win kev
>>> ntfy token list
>>> exit
$ curl http://127.0.0.1:2586
```

## client setup

- Linux: ~/.config/ntfy/client.yml
- MacOS: ~/Library/Application Support/ntfy/client.yml

```yaml
default-host: http://127.0.0.1:2586
default-user: kev
default-password: "******"
#default-token: "******"
```

```bash
$ ntfy sub test
$ ntfy pub -T fire -t WARNING test "Fire in the Hole"
```

```bash
$ websocat --basic-auth "kev:******" ws://127.0.0.1:2586/test/ws
$ curl -u "kev:******" -H 'Tags: fire' -H 'Title: WARNING' -d 'Fire in the Hole' http://127.0.0.1:2586/test
```

[1]: https://docs.ntfy.sh/config/
