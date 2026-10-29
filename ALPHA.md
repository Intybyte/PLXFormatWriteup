Contains the PLX version used in Cube World Alpha

The PLX format is subdivided in `Chunks` which have this structure:

UI = Unsigned Integer, 4 bytes

```text

+--------+----------+-----------------------+
| id: UI | size: UI | data: byteArray[size] |
+--------+----------+-----------------------+

```

There are 2 types of chunks:
- Data Definition Chunks (I will call them `DDChunks` for now)
- Real Data Chunks (I will call them `RDChunks`)

`DDChunks` have `id` equal to 0, and `data` will contain a `RDChunk` with a set `id` and an UTF-8 string in data with its name:

```text
+--------+----------+--------+---------------+-------------------+
| id = 0 | size: UI | id: UI | name_size: UI | name[size]: UTF-8 |
+--------+----------+--------+---------------+-------------------+
```

These chunks specify the data layout.

`RDChunks` have `id` equal to the data type specified by `DDChunks`.

Here we have the list of root components in order of appearances:
