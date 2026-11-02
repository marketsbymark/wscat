# wscat

A Node.js command-line tool for sending and receiving WebSocket messages, either as a client or as a simple listener.

This is a fork of [websockets/wscat](https://github.com/websockets/wscat). The checked-in [package.json](package.json) identifies this snapshot as version `5.1.0`.

## Installation

Node.js and npm are required. To install the published package globally:

```
npm install -g wscat
```

To run this fork from source instead:

```sh
git clone https://github.com/marketsbymark/wscat.git
cd wscat
npm install
node bin/wscat --help
```

Use `node bin/wscat` in place of `wscat` in the examples when running from this checkout. Installing the published package does not necessarily install this fork's version.

## Usage

```
Usage: wscat [options] (--listen <port> | --connect <url>)

Options:
  -V, --version                       output the version number
  --auth <username:password>          add basic HTTP authentication header (--connect only)
  --ca <ca>                           specify a Certificate Authority (--connect only)
  --cert <cert>                       specify a Client SSL Certificate (--connect only)
  --host <host>                       optional host
  --key <key>                         specify a Client SSL Certificate's key (--connect only)
  --max-redirects [num]               maximum number of redirects allowed (--connect only) (default: 10)
  --no-color                          run without color
  --passphrase [passphrase]           specify a Client SSL Certificate Key's passphrase (--connect only). If you don't
                                      provide a value, it will be prompted for
  --proxy <[protocol://]host[:port]>  connect via a proxy. Proxy must support CONNECT method
  --slash                             enable slash commands for control frames (/ping, /pong, /close [code [, reason]])
  -c, --connect <url>                 connect to a WebSocket server
  -H, --header <header:value>         set an HTTP header. Repeat to set multiple (--connect only) (default: [])
  -L, --location                      follow redirects (--connect only)
  -l, --listen <port>                 listen on port
  -n, --no-check                      do not check for unauthorized certificates
  -o, --origin <origin>               optional origin
  -p, --protocol <version>            optional protocol version
  -P, --show-ping-pong                print a notification when a ping or pong is received
  -s, --subprotocol <protocol>        optional subprotocol (default: [])
  -w, --wait <seconds>                wait given seconds after executing command
  -x, --execute <command>             execute command after connecting
  -h, --help                          display help for command
```

## Local example

In one terminal, start a listener:

```sh
wscat --listen 8765
```

In a second terminal, connect to it:

```sh
wscat --connect ws://127.0.0.1:8765
```

Type a message and press Enter in either terminal; it appears in the other terminal. The listener is not an automatic echo server. Press Ctrl+C to stop each process.

**Listener safety:** This version's listener does not explicitly bind to loopback and may be reachable from other interfaces. Use a trusted development environment and restrict access with your firewall. The `--host` option sets the client Host header; it does not restrict the listener's bind address.

For remote connections, use a server you control or are authorized to test. Keep TLS verification enabled; `--no-check` disables certificate validation.

## Development checks

The `npm test` script in this snapshot only prints “No test specified”; it does not run an automated test suite. A manual two-terminal exchange can be used as a basic smoke check.

## License

[MIT](LICENSE)
