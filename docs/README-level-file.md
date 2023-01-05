# Sand-Box2D Level File
In this document described how Sand-Box2D operates with its levels files.

## Contents
- [Numbers input](#numbers-input)
- [File structure](#file-structure)
  * [Options sector](#options-sector)
  * [Camera sector](#camera-sector)
  * [Actions sector](#actions-sector)
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
    "actions": {"...": "..."},
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

It has the following structure (keys `attached_id` and `attached_remain` are exceed intentionally):
```json
  "camera": {
    "type": "static",
    "attached_id": 15,
    "attached_remain": 75,
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
- `attached_remain` - value that shows how many percents are left each frame when spectating object.
If you leave 0, camera will spectate object strictly, without smooth effect (it encounters object by 100% each frame).
When you set 75, it means that camera is going to encounter object by 25% each frame, which means that you're gonna see smooth effect.
If you set 100, camera won't move at all (it encounters object by 0% each frame, i.e. it's just static).
If you set >100, camera will fly away from object (no sense to do that).
Ignored when `type` is not `attached`.
- `zoom` - can user change camera zoom in game (true/false)?
- `move` - can user move camera in game? Ignored when `type` is `attached`.
- `x` and `y` - starting position of the camera in Box2D meters
(point to which camera is centered). Ignored when `type` is `attached`.
- `height` - it used for setting zoom value at the beginning.
It describes how much Box2D meters should camera capture in altitude, i.e. from screen top to bottom.

### Actions sector
In this sector you can add some actions (move objects or something) that will perform when user press special buttons.

With this thing you can change (set or add) any value of any object in-game.

Here's example:
```json
  "actions": {
    "up": {
      "keydown_hold": [
        {
          "id": 10,
          "type": "add",
          "param": "vel_y",
          "value": -0.75
        }
      ]
    },
    "right": {
      "keydown_hold": [
        {
          "id": 10,
          "type": "add",
          "param": "vel_x",
          "value": 0.75
        },
        {
          "id": 10,
          "type": "add",
          "param": "vel_ang",
          "value": 0.25
        }
      ]
    },
    "down": {
      "keydown_hold": [
        {
          "id": 10,
          "type": "add",
          "param": "vel_y",
          "value": 0.75
        }
      ]
    },
    "left": {
      "keydown_hold": [
        {
          "id": 10,
          "type": "add",
          "param": "vel_x",
          "value": -0.75
        },
        {
          "id": 10,
          "type": "add",
          "param": "vel_ang",
          "value": -0.25
        }
      ]
    },
    "enter": {
      "keydown_once": [
        {
          "id": 10,
          "type": "set",
          "param": "vel_x",
          "value": 0
        },
        {
          "id": 10,
          "type": "set",
          "param": "vel_y",
          "value": 0
        },
        {
          "id": 10,
          "type": "set",
          "param": "angle",
          "value": 0
        },
        {
          "id": 10,
          "type": "set",
          "param": "vel_ang",
          "value": 0
        }
      ],
      "keydown_hold": [
        {
          "id": 10,
          "type": "set",
          "param": "vel_x",
          "value": 0
        },
        {
          "id": 10,
          "type": "set",
          "param": "vel_y",
          "value": -0.2
        }
      ],
      "keyup": [
        {
          "id": 10,
          "type": "set",
          "param": "vel_x",
          "value": "-100:100"
        },
        {
          "id": 10,
          "type": "set",
          "param": "vel_y",
          "value": "-100:100"
        }
      ]
    }
  }
```
Where:
- `up`, `right`, `down`, `left` and `enter` - corresponding buttons to call actions.
Each game platform can have different buttons for this. They all can contain following keys:
  * `keydown_hold` is called every frame when corresponding button is hold.
  * `keydown_once` is called only once when user just pressed this button.
  * `keyup` is called only once when user stopped holding this button.

And all these keys are containing list of actions, one of them look like this:
```json
  {
    "id": 10,
    "type": "add",
    "param": "vel_y",
    "value": -0.75
  }
```
Where:
- `id` - [ID](./README-objects.md#id) of the object to be involved in this action.
- `type` - type of the action:
  * `set` - you want to set some object parameter to some value (`param = value`);
  * `add` - you want to add something to the param of the object (`param += value`).
- `param` - name of the object parameter to be modified.
- `value` - value to be setted-added to object parameter.

In this example we added move controls for the box with ID `10`. When we press directional
buttons it starts to move in this direction. When we press `enter` button it stops, but
if we stop pressing it, box will fly in random direction.

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
    },
    {
      "type": "box",
      "id": 10,
      "x": 6,
      "y": 5,
      "w": 2,
      "h": 2,
      "texture": "./box.png"
    }
  ]
```
In this example we just create 3 static [platforms](./README-objects.md/#platform)
and [box](./README-objects.md/#box) with ID `10` (to which will point our [action](#actions-sector)).

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
          "b": "0:255"
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
