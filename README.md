# proxc

1. per-process DNS configuration on Linux
2. per-process proxy configuration on Linux

## Configure DNS for Linux command execution

```
proxc -d <dns-ip> [-d <dns-ip_2>] -c <command and args>
```

Execute command with the DNS you specify.

It uses bubblewrap to create a mount namespace, in which processes see the DNS you want in a fake `/etc/resolv.conf`.

It bans in the namespace `/var/run/nscd` so processes can't use system's DNS cache

> Now it requires bubblewrap >= 0.11.0 . If you're using older bubblewrap, please use old proxc 1.0

## Configure proxy for Linux command execution

```
proxc -p socks5|socks4|http <proxy_ip> <proxy_port> -c <command and args>
```

Execute command with `proxychains` applied without having to edit `proxychains.conf` . Useful when you just want to run some app temporarily behind a single proxy.

It generates and uses a `proxychains.conf` in memory.

> **Notice:** proxychains doesn't ensure process must go through the proxy. There can be leaks.

## Configure both DNS & proxy

    proxc [-d <dns-ip>] [-p socks5|socks4|http <proxy_ip> <proxy_port>]  -c <command and args>
