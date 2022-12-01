# Sand-Box2D Objects
This is a documentation about certain objects in the Sand-Box2D world, how to declare them and etc.

All the objects classes are childs of the abstract class `BasePObj` in the code.
So, Sand-Box2D operates with objects as pointers to `BasePObj` realizations (`BasePObj*`).
Object cannot operate right after creation, it have to be registered (call `Register()` giving link to world),
because this was obvious option to make objects more portable.

## Contents
- [ID](#id)
- [Platform](#platform)
- [Box](#box)
- [Circle](#circle)

## ID
Each object _can_ have unique ID (integer). It means that you don't have to set it when you don't need it.
In this case (when you don't manually set ID), it will be considered as `-1`.

Setting ID will help us later with pointing to object which would be spectated by camera in attached mode, 
making joints between objects and involving them in "actions".

To set ID (in this example `1337`) you just have to set its value like that:
```json
  {
    "type": "...",
    "id": 1337,
    "...": "..."
  }
```

# Platform
Platform is a static line which represents Box2D's `b2EdgeShape` with start & end points.

It has the following structure:
```json
  {
    "type": "platform",
    "x1": 2,
    "y1": 7,
    "x2": 10,
    "y2": 7,
    "r": 255,
    "g": 255,
    "b": 0
  }
```
Where:
- `x1` and `y1` - position of the start point in Box2D meters.
- `x2` and `y2` - position of the end point in Box2D meters.
- `r`, `g`, `b` - color of the platform.

# Box
Box is a dynamic rectangle which represents Box2D's `b2PolygonShape` with position of center; width, height and angle.

It has the following structure:
```json
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
```
Where:
- `x` and `y` - position of the center of the box in Box2D meters.
- `w` and `h` - width and height of the box in Box2D meters.
Why its value is a string read [here](./README-level-file.md#numbers-input).
- `angle` - angle of the box in degrees.
- `vel_x` and `vel_y` - starting linear velocity of the box (its speed).
- `texture` - path to the texture of the box. 
If several objects are using the same file, Sand-Box2D won't load them every time - 
it will use the same already loaded texture in the memory.

# Circle
Circle is a dynamic object which represents Box2D's `b2CircleShape` with position of the center and radius.

It has the following structure:
```json
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
```
Where:
- `x` and `y` - position of the center of the circle in Box2D meters.
- `radius` - radius of the circle in Box2D meters.
- `vel_x` and `vel_y` - starting linear velocity of the circle (its speed).
- `r`, `g`, `b` - color of the circle.
- `r_angle`, `g_angle`, `b_angle` - color of the angle renderer of the circle
(line from circle center to border which shows how much circle is rotated).
