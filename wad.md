# WAD file format

WADs are archives used by the clients. They contain assets, game data (e.g.
item description), files for the LCU's interface and more.


## WAD header

The WAD file starts with the following header:

| Pos | Size | Format | Description                            |
| ---:| ----:| ------ | -------------------------------------- |
|   0 |    2 | `RW`   | magic code                             |
|   2 |    1 | u8     | major version                          |
|   3 |    1 | u8     | minor version                          |

Parsing of following data depends on the major version.
Latest known major version is 3.


## WAD version 1

Following the WAD header is the directory entry.

| Pos | Size | Format | Description                            |
| ---:| ----:| ------ | -------------------------------------- |
|   0 |    2 | u16    | entry header offset                    |
|   2 |    2 | u16    | entry header size                      |
|   4 |    4 | u32    | entry count                            |

This header provides the number and location of entries in the WAD archive.
[Entry headers](#entry-headers) start at the *entry header offset* and are
spaced by the *entry header size*. (In practice, they immediately follow the
directory header and are contiguous.)


## WAD version 2

Following the WAD header is the directory entry.

| Pos | Size | Format | Description                                       |
| ---:| ----:| ------ | ------------------------------------------------- |
|   0 |    1 | u8     | ECDSA signature length                            |
|   1 |   83 |        | ECDSA signature of entry headers, padded with `0` |
|  84 |    8 | u64    | xxHash checksum                                   |
|  92 |    2 | u16    | entry header offset                               |
|  94 |    2 | u16    | entry header size                                 |
|  96 |    4 | u32    | entry count                                       |

This header provides the number and location of entries in the WAD archive.
[Entry headers](#entry-headers) start at the *entry header offset* and are
spaced by the *entry header size*. (In practice, they immediately follow the
directory header and are contiguous.)


## WAD version 3

Following the WAD header is the directory entry.

| Pos | Size | Format | Description                            |
| ---:| ----:| ------ | -------------------------------------- |
|   0 |  264 |        | ECDSA signature                        |
| 264 |    4 | u32    | entry count                            |

This header provides the number of entries in the WAD archive.
[Entry headers](#entry-headers) immediately follow the directory header and are
contiguous.


## Entry headers

Entry header format is compatible with all WAD versions: new fields are added
to the end of the structure. Knowing the size of the entry header structure
allows to which fields are actually present.

WAD version 1 ends at the *data type* field, followed by 3 padding bytes (for alignement).
WAD versions 2 and 3 include all fields.

| Pos | Size | Format | Description                            |
| ---:| ----:| ------ | -------------------------------------- |
|   0 |    8 | u64    | [path hash](#path-hashes)              |
|   8 |    4 | u32    | data offset in the WAD archive         |
|  12 |    4 | u32    | compressed size                        |
|  16 |    4 | u32    | uncompressed size                      |
|  20 |    1 | u8     | data type                              |
|  21 |    1 | bool   | set for [duplicate entries](#entry-duplication) |
|  22 |    2 | u16    | padding                                |
|  24 |    8 | u64    | first 8 bytes of sha256 hash of data   |

The following *data types* are known:

 - `0` -- uncompressed data
 - `1` -- gzip
 - `2` -- [file redirection](#file-redirection)
 - `3` -- [Zstandard](http://facebook.github.io/zstd/)


## Path hashes

Paths of files in WAD archives are hashed using 64-bit
[xxHash](http://cyan4973.github.io/xxHash/) with seed 0.
Since paths are not stored in the archive in clear, they have to be guessed.

Hashed paths are all in lowercase. They usually use letters, digits and
characters from `._-/`. Rare occurrences also use spaces and `@`.

List of reversed hashes are available on CDTB:

 - [LCU hashes](https://raw.githubusercontent.com/CommunityDragon/CDTB/master/cdragontoolbox/hashes.lcu.txt)
 - [game client hashes](https://raw.githubusercontent.com/CommunityDragon/CDTB/master/cdragontoolbox/hashes.game.txt)


## Entry duplication

If an entry is duplicated, it's offset points to data of an another entry which is not duplicated.
This is a technique to lower file sizes.


## File redirection

For file redirection entries, the data offset points to an `u32` specifying the
length of the file redirection that follows it.

The file redirection is a string path. It tells the game to load the file
redirection file path instead of the one the xxHash specifies.

