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
|  84 |    8 |        | XXH64 checksum                                    |
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
|   0 |  256 |        | ECDSA signature                        |
| 256 |    8 |        | XXH64 checksum                         |
| 264 |    4 | u32    | entry count                            |

This header provides the number of entries in the WAD archive.
[Entry headers](#entry-headers) immediately follow the directory header and are
contiguous.


## Entry headers

Entry header format is somewhat compatible with all WAD versions: new fields are added
to the end of the structure.

WAD version 1 ends at the *data type* field, followed by 3 padding bytes (for alignement).
WAD versions 2 and 3 include all fields.

| Pos   | Size | Format | Description                            |
| ---:  | ----:| ------ | -------------------------------------- |
|   0   |    8 | u64    | [path hash](#path-hashes)              |
|   8   |    4 | u32    | data offset in the WAD archive         |
|  12   |    4 | u32    | compressed size                        |
|  16   |    4 | u32    | uncompressed size                      |
|  20:0 |  0:4 | u4     | data type                              |
|  20:4 |  0:4 | u4     | count of [subbchunks](#entry-subchunks) |
|  21   |    1 | bool   | set for [duplicate entries](#entry-duplication) |
|  22   |    2 | u16    | index of first [subbchunk](#entry-subchunks) |
|  24   |    8 |        | [entry checksum](#entry-checksum)      |

The following *data types* are known:

 - `0` -- uncompressed data
 - `1` -- gzip
 - `2` -- [file redirection](#file-redirection)
 - `3` -- [Zstandard](https://facebook.github.io/zstd/)
 - `4` -- [Zstandard with subchunks](#entry-subchunks)

## Entry subchunks

Introduced in 3.3.
Subchunked entries consist of multiple ZStandard compressed frames.
Subchunk headers are packed as an array inside dedicated entry.
Name of dedicated entry is derived by swaping extension 
of ``.wad.client`` to ``wad.SubchunkTOC``.
This allows the client to skip decompressing unecessary parts of file (example: unused mipmaps).

| Pos | Size | Format | Description                            |
| ---:| ----:| ------ | -------------------------------------- |
|   0 |    4 |    u32 | compressed size                        |
|   4 |    4 |    u32 | uncompressed size                      |
|   8 |    8 |        | [subbchunk checksum](#entry-checksum)  |


## Path hashes

Paths of files in WAD archives are hashed using 64-bit
[XXH64](https://cyan4973.github.io/xxHash/) with seed 0.
Since paths are not stored in the archive in clear, they have to be guessed.

Hashed paths are all in lowercase. They usually use letters, digits and
characters from `._-/`. Rare occurrences also use spaces and `@`.

List of reversed hashes are available in [Data repository](https://github.com/CommunityDragon/Data).


## Entry duplication

If an entry is duplicated, it's offset points to data of first entry which is not duplicated.
Pointed entry does not have duplicated flag set, only subsequent entries have it.
This is a technique to lower file sizes.

## Entry checksum

Not present for entry headers before wad version 3.
For version 3.0 this is first 8 bytes of sha256 hash.
Starting with version 3.1 this is xxh3_64bits hash.

## File redirection

For file redirection entries, the data offset points to an `u32` specifying the
length of the file redirection that follows it.

The file redirection is a string path. It tells the game to load the file
redirection file path instead of the one the xxHash specifies.

