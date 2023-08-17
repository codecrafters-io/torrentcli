# torrentcli

`torrentcli` is a CLI bittorrent client.

`torrentcli` was built to serve as a reference implementation for learners of the [Build your own BitTorrent](https://app.codecrafters.io/courses/bittorrent/overview) challenge.

Its primary usage is to download a torrent given a `.torrent` file:

```bash
torrentcli download -o /tmp/ubuntu.iso ubuntu-iso.torrent
```

It also exposes some other lower-level commands to deal with `.torrent` files.

## List of commands

### `torrentcli decode <bencoded_string>`

Decodes a bencoded string and prints it as JSON

**Example:**

```bash
$ torrentcli decode d3:cow3:moo4:spam4:eggse
{ "cow": "moo", "spam": "eggs" }
```

### `torrentcli info <torrent_file>`

Extracts information from a torrent file.

**Example:**

```bash
$ torrentcli info ubuntu-iso.torrent
Tracker URL: http://torrent.ubuntu.com:6969/announce
Length: 4068474880
Info Hash: 6d4795dee70aeb88e03e5336ca7c9fcf0a1e206d
```

### `torrentcli peers <torrent_file>`

Lists the available peers for a torrent.

**Example:**

```bash
$ torrentcli peers ubuntu-iso.torrent
188.119.61.177:6881
71.224.0.29:51414
62.153.208.98:3652
```

### `torrentcli handshake <torrent_file> <peer>`

Performs a handshake with a peer.

Example:

```bash
$ torrentcli handshake ubuntu-iso.torrent 118.119.61.177:6882
Handshake succcessful.
```

### `torrentcli download_piece -o <download_location> <torrent_file> <peer> <piece_index>`

Download a piece of a file from a peer.

**Example:**

```bash
$ torrentcli download_piece -o /tmp/ubuntu-iso-piece-1 ubuntu-iso.torrent 118.119.61.117:6882 1
Piece 1 downloaded to /tmp/ubuntu-iso-piece-1.
```

### `torrentcli download -o <download_location> <torrent_file>`

Download a torrent.

**Example:**

```bash
$ torrentcli download -o /tmp/ubuntu-iso ubuntu-iso.torrent
Downloaded ubuntu-iso.torrent to /tmp/ubuntu-iso.
```
