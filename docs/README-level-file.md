# Sand-Box2D Level File
In this document described how Sand-Box2D operates with its levels files.

## Contents
- [Numbers input](#numbers-input)
- [File structure](#file-structure)
  * [Options sector](#options-sector)
  * [Camera sector](#camera-sector)
  * [Objects sector](#objects-sector)
  * [Cycles sector](#cycles-sector)
- [Samples](#samples)

## Numbers input
You can input numbers in default JSON format (`"number": 123` or `"number_float": 12.3`), 
but you can also input a string like that: `"random": "100:5000"`,
it means that you want to input a *random* number between 100 and 5000.
Float and negative numbers are also supported: `"random_float": "-1.5:5"`.

## File structure
Every level file is just a JSON with the structure below:
```json
  {
    "options": {"...": "..."},
    "camera": {"...": "..."},
    "objects": [{"...": "..."}, {"...": "..."}],
    "cycles": [{"...": "..."}, {"...": "..."}]
  }
```

### Options sector
Here are global world options located. If you want to keep settings by default, skip and don't write this sector in your file.

It has the following structure:
- No options yet. They'll appear here when they would be realized in the code.

### Camera sector
In this sector described how Sand-Box2D should place camera at the start, can player move it and etc.

It has the following structure (key `attached_id` is exceed intentionally):
```json
  "camera": {
    "type": "static",
    "attached_id": 15,
    "zoom": true,
    "move": true,
    "x": 6,
    "y": 3.5,
    "height": 8
  }
```
Where:
- `type` - type of the camera. It can be:
  * `static` - camera doesn't move by itself. Player can move it and change zoom if it's allowed below.
  * `attached` - camera is attached to some object and spectates them. Zooming is allowed, but not movement.
- `attached_id` - ID of the object to be spectated when camera type is attached 
(more [here](./README-objects.md/#id)). Ignored when `type` is not `attached`.
- `zoom` - can user change camera zoom in game (true/false)?
- `move` - can user move camera in game? Ignored when `type` is `attached`.
- `x` and `y` - starting position of the camera in Box2D meters
(point to which camera is centered). Ignored when `type` is `attached`.
- `height` - it used for setting zoom value at the beginning.
It describes how much Box2D meters should camera capture in altitude, i.e. from screen top to bottom.

### Objects sector
Read full [article](./README-objects.md) to understand how to create certain objects.

This sector describes which physics objects Sand-Box2D need to create once at the beginning.

It has the following structure:
```json
  "objects": [
    {
      "type": "platform",
      "x1": 2,
      "y1": 7,
      "x2": 10,
      "y2": 7,
      "r": 255,
      "g": 255,
      "b": 0
    },
    {
      "type": "platform",
      "x1": 1,
      "y1": 1,
      "x2": 2,
      "y2": 7,
      "r": 255,
      "g": 255,
      "b": 0
    },
    {
      "type": "platform",
      "x1": 10,
      "y1": 7,
      "x2": 11,
      "y2": 1,
      "r": 255,
      "g": 255,
      "b": 0
    }
  ]
```
In this example we just create 3 static [platforms](./README-objects.md/#platform).

### Cycles sector
Read full [article](./README-objects.md) to understand how to create certain objects.

This sector does the same thing as the [objects sector](#objects-sector), but periodically.
You can declare several cycles with different delays.

It has the following structure:
```json
  "cycles": [
    {
      "delay": "25:100",
      "objects": [
        {
          "type": "circle",
          "x": 5,
          "y": 0,
          "radius": "0.05:0.75",
          "vel_x": -10,
          "vel_y": 10,
          "r": "0:255",
          "g": "0:255",
          "b": "0:255",
          "r_angle": 0,
          "g_angle": 0,
          "b_angle": 0
        }
      ]
    },
    {
      "delay": "100:200",
      "objects": [
        {
          "type": "box",
          "x": 7,
          "y": 0,
          "w": "0.1:2.0",
          "h": "0.1:2.0",
          "angle": 0,
          "vel_x": 10,
          "vel_y": 10,
          "texture": "./box.png"
        }
      ]
    }
  ]
```
Where:
- `delay` - amount of frames between cycle steps. Why its value is a string read [here](#numbers-input).
- `objects` - should be filled with objects as [here](#objects-sector).

Here we declare two cycles with [box](./README-objects.md/#box) and [circle](./README-objects.md/#circle)
with random width/height and radius respectively.
Circles with random color will spawn continuously every 25-100 frames (0.5-2 seconds),
and boxes will do it every 100-200 frames (2-3 seconds, ~2 times slower).

## Samples
You can refer to the [default level](../levels/default_level/) for example built with this tutorial.

But you can also view other levels from theirs [directory](../levels/).
