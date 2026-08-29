# docker-tun AppArmor profile

Install this on any host whose kernel mediates AF_UNIX through AppArmor.
Check first:

```sh
cat /sys/kernel/security/apparmor/features/network/af_unix
```

If that prints `yes` (Proxmox 9, Debian 13, recent Ubuntu), the `docker-default`
profile Docker generates will deny every AF_UNIX socket a container opens, and
`internetIncome.sh --start` fails in two places at once:

- the tun2socks containers die with `[ENGINE] failed to start: get mtu:
  permission denied`, restart-loop, and leave every app container sharing their
  netns stuck in `Created`
- the app containers fail every DNS lookup with
  `curl: (6) getaddrinfo() thread failed to start`, so earnapp never downloads
  its installer and never mints a node id

If the file is missing or prints `no`, you do not need this profile, and
`internetIncome.sh` behaves exactly as it did before.

## Install

```sh
sudo cp apparmor/docker-tun /etc/apparmor.d/docker-tun
sudo apparmor_parser -r -W /etc/apparmor.d/docker-tun
grep -c '^docker-tun ' /sys/kernel/security/apparmor/profiles   # expect 1
```

`internetIncome.sh` detects the loaded profile and adds
`--security-opt apparmor=docker-tun` to every container it starts. Nothing else
to configure. Living in `/etc/apparmor.d` means `apparmor.service` reloads it at
boot, so it survives reboots.

## Remove

```sh
sudo apparmor_parser -R /etc/apparmor.d/docker-tun
sudo rm /etc/apparmor.d/docker-tun
```

## What it is

Docker's own `docker-default` profile with `abi <abi/4.0>,` declared, which is
the actual fix — adding `unix,` alone does not work, because the denial happens
in the `net` class and the legacy ABI emits no rule matching AF_UNIX there. It
also names the `runc` peer in its signal and ptrace rules, since ABI 4.0
mediates those more tightly. Every other `docker-default` restriction is kept:
`deny mount`, the `/proc` and `/sys` write denials, and ptrace/signal scoping.
This is narrower than `--security-opt apparmor=unconfined`, which is the usual
advice for this error and drops confinement entirely.
