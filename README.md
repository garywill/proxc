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

> **Notice:** If network status change, NetworkManager or other program may delete `/etc/resolv.conf` and create a new one. That makes bubblewrap's file binding lost, causing DNS fallback to original system's DNS
> 
> So, not suitable for long-time running. If you want long-time running, it's recommend to use static DNS configuration using the following variables in the `/etc/sysconfig/network/config`:
> 
> -  `NETCONFIG_DNS_STATIC_SEARCHLIST` 
> - `NETCONFIG_DNS_STATIC_SERVERS` 
> - `NETCONFIG_DNS_FORWARDER` 
> 
> or disable DNS configuration updates via netconfig by setting: `NETCONFIG_DNS_POLICY=''`

## Configure proxy for Linux command execution

```
proxc -p socks5|socks4|http <proxy_ip> <proxy_port> -c <command and args>
```

Execute command with `proxychains` applied without having to edit `proxychains.conf` . Useful when you just want to run some app temporarily behind a single proxy.

It generates and uses a `proxychains.conf` in memory.

> **Notice:** proxychains doesn't ensure process must go through the proxy. There can be leaks.

## Configure both DNS & proxy

    proxc [-d <dns-ip>] [-p socks5|socks4|http <proxy_ip> <proxy_port>]  -c <command and args>
