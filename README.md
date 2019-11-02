# proxc

- Execute command with `proxychains` applied without having to edit `proxychains.conf` .
   - Useful when you just want to run some app behind a single proxy.
   - It generates and uses a `proxychains.conf` in memory.
- Configure DNS for one Linux process
    - Use bubblewrap to create a mount namespace, in which processes see the DNS you want in `/etc/resolv.conf`
    - Ban `/var/run/nscd` so processes can't use system's DNS cache

## Usage

    proxc [-p socks5|socks4|http <proxy_ip> <proxy_port>] [-d <dns-ip>] -c <command and args>
