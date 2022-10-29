# Sand-Box2D Levels
This is a documentation how Sand-Box2D operates with its levels files.

## File structure
Every level file is just a JSON with the structure below:

```json
  {
    "metadata": {"..."},
    "camera": {"..."},
    "objects": {"..."},
    "thread": {"..."},
    "thread": {"..."},
    "..."
  }
```

### Metadata sector
Metadata contains information about level, its author and other info that might be useful. It has the following structure:
```json
  "metadata": {
    "name": "Default level",
    "author": "Hammerill",
    "version": "v1.0.0",
    "date": "2022-10-29"
    "..."
  }
```
Where 4 required fields (when publishing a level) are:
- `name` - name of the level.
- `author` - nickname of the level creator.
- `version` - version of the level.
- `date` - date of the level publication in YYYY-MM-DD format.

It can also support the following fields:
- `preview` - link to the image in PNG or JPG format with 16x9 aspect. 
It's a thumbnail of the level, showing screenshot from the level itself or some illustration describing it. 
When no preview specified, in the level selector menu (doesn't exists yet though) is fallback image showed.
- `description` - detailed description text of the level.
- `screenshots: {"...", "..."}` - list of screenshots from the level in the same format as `preview`.

And you can add custom fields to metadata if you think you need to do it.

### Camera sector
In this sector described how Sand-Box2D should place camera at the start, can player move it and etc. It has the following structure:
```json
  "camera": {
    "type": "static",
    "ONGOING"
  }
```

