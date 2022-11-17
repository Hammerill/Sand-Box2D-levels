# Sand-Box2D Index
In this document described how Sand-Box2D operates with its [index file](../levels/index.json).

Only purpose of index file existence is to help Sand-Box2D download levels locally in order to play them.

## Contents
- [Notes](#notes)
- [File structrure](#file-structrure)

## Notes
- It's important to update version in the index. If you don't do it, Sand-Box2D will consider your level
as actual and won't update it even if there's really some changes.
- Leave paths only to files relative to the "directory" field. Don't leave URLs or paths to files
you didn't upload.
- In level files you should use the same rules, but mostly files would be considered as relative of
the subject file itself (like main level file), not strictly to the "directory" field.
But in most cases you may prefer leaving main level file at the same path as "directory" field,
so there would be no difference.

## File structrure
Index has the following structure:
```json
  [
    {
      "directory": "default_level",
      "level": "default_level.json",
      "metadata": {
        "name": "Default level",
        "author": "Hammerill",
        "version": "v1.0.0",
        "date": "2022-10-29",
        "description": "Default level for Sand-Box2D that also used as tutorial example."
      },
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
- `metadata` - contains information about level, its author and other info that might be useful.
Its required fields (when publishing a level) are:
  * `name` - name of the level.
  * `author` - nickname of the level creator.
  * `version` - version of the level. Format like v1.0.0 is preferred.
  * `date` - date of the level publication in YYYY-MM-DD format.
- It can also support the following fields:
  * `description` - detailed description text of the level.
  * `thumbnail` - path to the image in PNG or JPG format with 16x9 aspect. 
It might be a screenshot from the level or some illustration describing it. 
When no thumbnail specified, in the level selector menu (doesn't exists yet though) is fallback image showed.
  * `"screenshots": ["...", "..."]` - list of screenshots from the level in the same format as `thumbnail`.
- `files` - list of other files that are used in the level. It's important to mark them here - 
if you don't, they won't be downloaded and be accessible from the level file.

You can add custom fields to metadata if you think you need to do it.
