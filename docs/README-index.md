# Sand-Box2D Index
In this document described how Sand-Box2D operates with its [index file](../levels/index.json).

Only purpose of index file existence is to help Sand-Box2D download levels locally in order to play them.

## Contents
- [Notes](#notes)
- [File structrure](#file-structrure)

## Notes
- It's important to update version in the index. If you don't do it, Sand-Box2D will consider your level
as actual and won't update it even if there's really some changes.
- Other metadata of the level are stored in its [main file](./README-level-file.md).

## File structrure
Index has the following structure:
```json
[
  {
    "directory": "default_level",
    "level": "default_level.json",
    "version": "v1.0.0",
    "files": [
      "img/box.png"
    ]
  }
]
```
Where:
- `directory` - path to the directory (relatively to the [levels directory](../levels/)) where level is located.
Note that all the next paths will be considered as relative to it.
- `level` - path to the [main level file](./README-level-file.md).
- `version` - version of the level. Should be the same as in metadata sector of the level's file. 
- `files` - list of other files that are used in the level. It's important to mark them here - 
if you don't, they won't be downloaded and be accessible from level file.
