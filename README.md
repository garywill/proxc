# proxc
Execute command with `proxychains` applied without having to edit `proxychains.conf` .

Useful when you just want to run some app behind a single proxy.

It automatically generates a `proxychains.conf` in temporary path.

## Usage

    proxc proxytype proxyip proxyport commands
