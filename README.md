# proxc

- Execute command with `proxychains` applied without having to edit `proxychains.conf` .
   - Useful when you just want to run some app behind a single proxy.
   - It generates and uses a `proxychains.conf` in memory.
- Configure DNS for one Linux process
    - Use bubblewrap to create a mount namespace, in which processes see the DNS you want in `/etc/resolv.conf`
    - Ban `/var/run/nscd` so processes can't use system's DNS cache
    > If network status change, NetworkManager or other program may delete `/etc/resolv.conf` and create a new one. That makes bubblewrap's file binding lost. So it's recommend to use static DNS configuration using the following variables in the `/etc/sysconfig/network/config`:   `NETCONFIG_DNS_STATIC_SEARCHLIST`  `NETCONFIG_DNS_STATIC_SERVERS`  `NETCONFIG_DNS_FORWARDER`     or disable DNS configuration updates via netconfig by setting: `NETCONFIG_DNS_POLICY=''`
    
## Usage

    proxc [-p socks5|socks4|http <proxy_ip> <proxy_port>] [-d <dns-ip>] -c <command and args>
