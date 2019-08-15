# BIN file format

BINs are files used by the game client. They contain typed structured data.


## BIN header

The BIN file starts with the following header:

| Pos | Size | Format | Description                            |
| ---:| ----:| ------ | -------------------------------------- |
|   0 |    4 | `PROP` | magic code                             |
|   4 |    4 | u32    | version                                |

Parsing of following data depends on the version.

Starting from version 2, the header is followed by links to other BIN files (a
list of their path):

| Pos | Size  | Format | Description                            |
| ---:| -----:| ------ | -------------------------------------- |
|   0 |     4 | u32    | linked files count                     |
|   4 | ?×*n* | string | linked files paths                     |

After linked files (or version for older BIN files) are the entry types:

| Pos | Size  | Format | Description                            |
| ---:| -----:| ------ | -------------------------------------- |
|   0 |     4 | u32    | entry count                            |
|   4 | 4×*n* | u32    | entry types                            |


## BIN entries

Entry header:

| Pos | Size  | Format | Description                            |
| ---:| -----:| ------ | -------------------------------------- |
|   0 |     4 | u32    | entry length                           |
|   4 |     4 | u32    | entry hash                             |
|   8 |     4 | u16    | field count                            |

The header is followed by field data as defined [here](#field-format).


## Data types

BIN data is structured and each value is typed.
Some types are nested and can contain other values.

The following types are defined:

| Value | Format      | Size  | Nested | Description                        |
| -----:| ----------- | -----:|:------:| ---------------------------------- |
|     0 | empty       | 6     |        |                                    |
|     1 | bool        | 1     |        |                                    |
|     2 | s8          | 1     |        |                                    |
|     3 | u8          | 1     |        |                                    |
|     4 | s16         | 2     |        |                                    |
|     5 | u16         | 2     |        |                                    |
|     6 | s32         | 4     |        |                                    |
|     7 | u32         | 4     |        |                                    |
|     8 | s64         | 8     |        |                                    |
|     9 | u64         | 8     |        |                                    |
|    10 | float       | 4     |        |                                    |
|    11 | vec2(float) | 8     |        |                                    |
|    12 | vec3(float) | 12    |        |                                    |
|    13 | vec4(float) | 16    |        |                                    |
|    14 | matrix4x4   | 64    |        |                                    |
|    15 | rgba        | 4     |        | RGBA byte values                   |
|    16 | string      | 2+*n* |        | 2-byte size followed by content    |
|    17 | hash        | 4     |        | [BIN hash](#bin-hash) value        |
|    18 | container   | > 9   | ✓      | array of values of the same type   |
|    19 | struct      | > 10  | ✓      | [structure with named fields](#structs-and-embeddeds) |
|    20 | embedded    | > 10  | ✓      | [structure with named fields](#structs-and-embeddeds) |
|    21 | link        | 4     |        |                                    |
|    22 | option      | 2+*n* | ✓      | an optional value                  |
|    23 | map         | > 10  | ✓      | key/value pairs                    |
|    24 | flag        | 1     |        | boolean used as a flag              |

**Note:** Value size is either fixed (e.g. numeric types) or provided in the
header (e.g. structs). The only exceptions are nested strings whose size cannot
be inferred from the header.


## Structs and embeddeds

Structs and embeddeds store their values in fields.
Each field of is associated to a type and a hash (based on its human-readable
name). Fields are optional.

**Note:** Structs and embeddeds work the same. The difference is internal:
structs are stored as fields and embeddeds are pointers to static data.

Data starts with the following header:

| Pos | Size  | Format | Description                            |
| ---:| -----:| ------ | -------------------------------------- |
|   0 |     4 | u32    | struct/embedded name hash              |
|   4 |     4 | u32    | data size (remaining bytes)            |
|   8 |     2 | u16    | field count                            |

**Note:** if the name hash is 0, struct is void and ends right after the name hash.

Header is followed by field data.
Each field is introduced by a small header followed by field value data.
Field header format is describe below:

| Pos | Size  | Format | Description                            |
| ---:| -----:| ------ | -------------------------------------- |
|   0 |     4 | u32    | field name hash                        |
|   4 |     1 | u8     | field type                             |


## Other nested types

Containers, options and maps are nested types for which all elements are
sequenced and have the same type (provided in the header).

### Container

| Pos | Size  | Format | Description                            |
| ---:| -----:| ------ | -------------------------------------- |
|   0 |     1 | u8     | value type                             |
|   1 |     4 | u32    | data size (remaining bytes)            |
|   5 |     4 | u32    | value count                            |

### Option

| Pos | Size  | Format | Description                            |
| ---:| -----:| ------ | -------------------------------------- |
|   0 |     1 | u8     | value type                             |
|   1 |     1 | u8     | 1 if option has a value, 0 otherwise   |

### Map

| Pos | Size  | Format | Description                            |
| ---:| -----:| ------ | -------------------------------------- |
|   0 |     1 | u8     | key type                               |
|   1 |     1 | u8     | value type                             |
|   2 |     4 | u32    | data size (remaining bytes)            |
|   6 |     4 | u32    | key/value count                        |


## BIN hashes

BIN files use 32-bit hashes to identify fields and reference some data instances.

An [FNV-1a hash](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function#FNV-1a_hash)
is applied to the lowercased string value.

