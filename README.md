# torrentcli

`torrentcli` is a CLI bittorrent client.

`torrentcli` was built to serve as a reference implementation for learners of the [Build your own BitTorrent](https://app.codecrafters.io/courses/bittorrent/overview) challenge.

Its primary usage is to download a torrent given a `.torrent` file:

```bash
torrentcli download -o /tmp/ubuntu.iso ubuntu-iso.torrent
```

It also exposes some other lower-level commands to deal with `.torrent` files.

## List of commands

### decode

Decodes a bencoded string and prints it as JSON

**Interface**: `torrentcli decode <bencoded_string>`

**Example:**

```bash
$ torrentcli decode d3:cow3:moo4:spam4:eggse
{ "cow": "moo", "spam": "eggs" }
```

### info

Extracts information from a torrent file.

**Interface**: `torrentcli info <torrent_file>`

**Example:**

```bash
$ torrentcli info ubuntu-iso.torrent
Tracker URL: http://torrent.ubuntu.com:6969/announce
Length: 4068474880
Info Hash: 6d4795dee70aeb88e03e5336ca7c9fcf0a1e206d
Piece Length: 262144
Piece Hashes:
ddf33172599fda84f0a209a3034f79f0b8aa5e22
795a618a1ee5275e952843b01a56ae4e142752ef
```

### peers

Lists the available peers for a torrent.

**Interface**: `torrentcli peers <torrent_file>`

**Example:**

```bash
$ torrentcli peers ubuntu-iso.torrent
188.119.61.177:6881
71.224.0.29:51414
62.153.208.98:3652
```

### handshake

Performs a handshake with a peer.

**Interface**: `torrentcli handshake <torrent_file> <peer>`

Example:

```bash
$ torrentcli handshake ubuntu-iso.torrent 118.119.61.177:6882
Peer ID: 0102030405060708090a0b0c0d0e0f1011121314
```

### download_piece

Download a piece of a file from a peer.

**Interface**: `torrentcli download_piece -o <download_location> <torrent_file> <peer> <piece_index>`

**Example:**

```bash
$ torrentcli download_piece -o /tmp/ubuntu-iso-piece-0 ubuntu-iso.torrent 118.119.61.117:6882 0
Piece 0 downloaded to /tmp/ubuntu-iso-piece-0.
```

### download

Download a torrent.

**Interface**: `torrentcli download -o <download_location> <torrent_file>`

**Example:**

```bash
$ torrentcli download -o /tmp/ubuntu-iso ubuntu-iso.torrent
Downloaded ubuntu-iso.torrent to /tmp/ubuntu-iso.
```
