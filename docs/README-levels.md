# Sand-Box2D Levels
This is a documentation how Sand-Box2D operates with its levels files.

## File structure
Every level file is just a JSON with the structure below:
```json
  {
    "metadata": {"..."},
    "options": {"..."},
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
    "date": "2022-10-29",
    "..."
  }
```
Where 4 required fields (when publishing a level) are:
- `name` - name of the level.
- `author` - nickname of the level creator.
- `version` - version of the level. Format like v1.0.0 is preferred.
- `date` - date of the level publication in YYYY-MM-DD format.

It can also support the following fields:
- `thumbnail` - link to the image in PNG or JPG format with 16x9 aspect. 
It might be a screenshot from the level or some illustration describing it. 
When no thumbnail specified, in the level selector menu (doesn't exists yet though) is fallback image showed.
- `description` - detailed description text of the level.
- `screenshots: {"...", "..."}` - list of screenshots from the level in the same format as `thumbnail`.

And you can add custom fields to metadata if you think you need to do it.

### Options sector
Here are global world options located. If you want to keep settings by default, skip and don't write this sector in your file.
It has the following structure:
- No options yet. They'll appear here when they would be realized in the code.

### Camera sector
In this sector described how Sand-Box2D should place camera at the start, can player move it and etc. It has the following structure:
```json
  "camera": {
    "type": "static",
    "zoom": true,
    "move": true,
    "x": 5,
    "y": 4,
    "height": 8
  }
```
Where:
- `type` - type of the camera. It can be:
  * `static` - camera doesn't move by itself. Player can move it and change zoom if it's allowed below.
  * `attached` - camera is attached to some object and spectates them. Zooming is allowed, but not movement.
- `zoom` - can user change camera zoom in game (true/false)?
- `move` - can user move camera in game? Ignored when `type` is `attached`.
- `x` and `y` - starting position of the camera in Box2D meters. Ignored when `type` is `attached`.
- `height` - it used for setting zoom value at start.
It describes how much Box2D meters should camera capture in altitude, i.e. from screen top to bottom.

ONGOING
