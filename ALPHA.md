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
<!-- used https://tanod.dev/tools/markdown-table-generator/ for the table cuz having to edit tables with text files is miserable -->
| Component       |     Type |                                                          Function |
| :-------------- | -------: | ----------------------------------------------------------------: |
| PlasmaGraphics  |      Int |                                              Version? Is always 1 |
| Seal            |        ? | When used the other names are obfuscated using a custom algorithm |
| Texture         |  Complex |        Describes an image, the format, the wrapping and filtering |
| SmoothMeshShape |  Complex |                                                                 ? |
| TextShape       |  Complex |                                            Text string to display |
| Transformation  |  Complex |                                           Mostly arrays/matrices? |
| Display         |  Complex |                                 Seems to behave like a rectangle? |
| Widget          |  Complex |                                                                 ? |
| Button          |  Complex |              Derivate of Widget with extra info about button type |
| Edit            |  Complex |                    Derivate of Widget (what are the differences?) |
| Node            |  Complex |                                  ? can have many children or none |
| pageWidth       |    Float |                                                                   |
| pageHeight      |    Float |                                                                   |
| dpi             |    Float |                                                                   |
| unit            |      Int |                                                                   |
| pageColor       | 4 Floats |                                                        RBGA color |

All the complex types appear more than once and all have a unique identifier `wname`.

WIP Notes

A lot of assets seem to use Attribute.frame multiple times and the amount of Attribute.frame is the same, are they alternative version of the same asset?
<asset>.wname seems always original, might be the way to Uniquely identify assets within the file
Make an ALPHA/ subfolder where each Complex structure is described more in detail, inside also a BASICS.md where to explain common components like attributes and characteristics like .wname
All `?` is unconfirmed information, needs to be double checked and refined
