# proxc
Execute command with `proxychains` applied without having to edit `proxychains.conf` .

Useful when you just want to run some app behind a single proxy.

It generates and uses a `proxychains.conf` in memory.

## Usage

    proxc socks5|socks4|http <proxy_ip> <proxy_port> <command and args>
