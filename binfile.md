# BIN file format

BINs are files used by the game client. They contain typed structured data.


## BIN header

The BIN file starts with the following header:

| Pos | Size | Format | Description                            |
| ---:| ----:| ------ | -------------------------------------- |
|   0 |    4 | `PROP` | magic code                             |
|   4 |    1 | u8     | version                                |

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
|   0 |     4 | u32    | length size (4)                        |
|   4 |     4 | u32    | entry length                           |
|   8 |     4 | u32    | entry hash                             |
|  12 |     4 | u16    | field count                            |

The header is followed by field data as defined [here](#field-format).


## Data types

BIN data is structured and each value is typed.
Some types are nested and can contain other values.

The following types are defined:

| Value | Format      | Size   | Nested | Nestable | Description                        |
| -----:| ----------- | ------ | ------ | -------- | ---------------------------------- |
|     0 | vec3(u16)   | 6      |        |          |                                    |
|     1 | bool        | 1      |        |          |                                    |
|     2 | s8          | 1      |        |          |                                    |
|     3 | u8          | 1      |        |          |                                    |
|     4 | s16         | 2      |        |          |                                    |
|     5 | u16         | 2      |        |          |                                    |
|     6 | s32         | 4      |        |          |                                    |
|     7 | u32         | 4      |        |          |                                    |
|     8 | s64         | 8      |        |          |                                    |
|     9 | u64         | 8      |        |          |                                    |
|    10 | float       | 4      |        |          |                                    |
|    11 | vec2(float) | 8      |        |          |                                    |
|    12 | vec3(float) | 12     |        |          |                                    |
|    13 | vec4(float) | 16     |        |          |                                    |
|    14 | matrix4x4   | 64     |        |          |                                    |
|    15 | rgba        | 4      |        |          | RGBA byte values                   |
|    16 | string      | 2+*n*  |        |          | 2-byte size followed by content    |
|    17 | hash        | 4      |        |          | [BIN hash](#bin-hash) value        |
|    18 | container   |        | ✓      | ✗        |                                    |
|    19 | struct      |        | ✓      |          | see [Structs and embeddeds](#structs-and-embeddeds)                                                                            |
|    20 | embedded    |        | ✓      |          | see [Structs and embeddeds](#structs-and-embeddeds)                                                                            |
|    21 | link        | 4      |        |          |                                    |
|    22 | array       |        | ✓      | ✗        | array of nestable values           |
|    23 | map         |        | ✓      | ✗        | key/value pairs (both nestable)    |
|    24 | padding     | 1      |        |          | 1-byte padding                     |

**Note:** non-nestable types can only be used as field values, they cannot be used in containers, arrays or maps.


## Structs and embeddeds

Structs and embeddeds store their values in fields.
Each field of is associated to a type and a hash (based on its human-readable
name). Fields are optional.

**Note:** Structs and embeddeds work the same. In general, structs are favored.
Embeddeds seem to be used to wrap types that would not be (e.g. to put a
container in another container).

Data starts with the following header:

| Pos | Size  | Format | Description                            |
| ---:| -----:| ------ | -------------------------------------- |
|   0 |     4 | u32    | struct/embedded name hash              |
|   4 |     4 | u32    | entry value                            |
|   8 |     2 | u16    | field count                            |

**Note:** if the name hash is 0, struct is void and ends right after the name hash.

Header is followed by field data.
Each field is introduced by a small header whose format depends on its type.


## Field format

All fields are introduced with the following header:

| Pos | Size  | Format | Description                            |
| ---:| -----:| ------ | -------------------------------------- |
|   0 |     4 | u32    | field name hash                        |
|   4 |     1 | u8     | field type                             |

Basic types are immediately followed by data.
Types with additonal header values are described below.

### Container field header

| Pos | Size  | Format | Description                            |
| ---:| -----:| ------ | -------------------------------------- |
|   5 |     1 | u8     | value type                             |
|   6 |     4 | u32    | field size (remaining bytes)           |
|  10 |     4 | u32    | value count                            |

Header is followed by value data.

### Array field header

| Pos | Size  | Format | Description                            |
| ---:| -----:| ------ | -------------------------------------- |
|   5 |     1 | u8     | value type                             |
|   6 |     1 | u8     | value count                            |

Header is followed by value data.

### Map field header

| Pos | Size  | Format | Description                            |
| ---:| -----:| ------ | -------------------------------------- |
|   5 |     1 | u8     | key type                               |
|   6 |     1 | u8     | value type                             |
|   7 |     4 | u32    | field size (remaining bytes)           |
|  11 |     4 | u32    | key/value count                        |

Header is followed by value data.

