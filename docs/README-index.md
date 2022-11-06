# Sand-Box2D Index
In this document described how Sand-Box2D operates with its [index file](../levels/index.json).

Only purpose of index file existence is to help Sand-Box2D download levels locally in order to play them.

## Contents
- [Notes](#notes)
- [File structrure](#file-structrure)

## Notes
- Level info (like its version) is stored in the
[metadata sector of its file](./README-level-file.md/#metadata-sector),
so index file only provides path to those files, not theirs info 
(when you just update your level, you shouldn't consider updating index file, only if it's new file(s) added).
- It's important to update version in your metadata. If you don't do it, Sand-Box2D will consider your level
as actual and won't update it even if there's really some changes.

## File structrure
Index has the following structure:
```json
[
    {
        "directory": "default_level",
        "level": "default_level.json",
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
- `files` - list of files that are used in the level. It's important to mark them here - 
if you don't, they won't be downloaded and be accessible from level file.
