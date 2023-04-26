# Sand-Box2D Python Scripting
This is a documentation about Python scripting in Sand-Box2D Levels.

Sand-Box2D provides `sandbox2d` module to operate with its environment to Python 2.7 scripts which are called in Level runtime.
Below you'll see all the functions that this module provides.

## Contents
- [Function Log](#function-log)
- [Function Get](#function-get)
- [Function Set](#function-set)
- [Function Sound](#function-sound)

## Function Log
Syntax: `sandbox2d.log(to_log: str)`.

This function simply types some text to dev console. If Sand-Box2D gets full operating in-game console (like in this [concept](https://github.com/Hammerill/Sand-Box2D/blob/main/pics/console_concept.png)) you won't be forced to alt-tab to your real console to see output.

Example:
```python
from sandbox2d import log

log("Wow, this script was loaded somehow, yay!")
```

## Function Get
Syntax: `sandbox2d.get(id: int, param: str)`.

This function will get some parameter of some object from Sand-Box2D environment. Its return type is unknown, it can be string, int, float and etc. There are some [reserved IDs](./README-objects.md#reserved-ids) which can be useful to storage variables for example (see ID `1` in reserved IDs).

Example:
```python
import sandbox2d

OBJECT_ID = 10

x = sandbox2d.get(OBJECT_ID, "x")
y = sandbox2d.get(OBJECT_ID, "y")

sandbox2d.log("Current position of the object with ID {0} is {{{1}; {2}}}.".format(OBJECT_ID, x, y))
```

## Function Set
Syntax: `sandbox2d.set(id: int, param: str, value)`.

This function will set some parameter of some object from Sand-Box2D environment. Type of the argument `value` is unknown, it can be string, int, float and etc. There are some [reserved IDs](./README-objects.md#reserved-ids) which can be useful to storage variables for example (see ID `1` in reserved IDs).

Example (note: in this example we use a feature that sets variable to `0` when we access it for the first time via function get):
```python
import sandbox2d

i = sandbox2d.get(1, "i")
if i < 10:
    sandbox2d.log("nah ya too weak. try again")
    sandbox2d.set(1, "i", i + 1)
else:
    sandbox2d.log("Wow, you called this function 10 times or even more, as congratulations we will return your object ID 10 to center.")
    sandbox2d.set(10, "x", 0)
    sandbox2d.set(10, "y", 0)
```

## Function Sound
Syntax: `sandbox2d.sound(sfx_name: str)`.

This function will play some specific SFX from the default Sand-Box2D assets. You can view them all in `assets/sfx/index.json`.
In future it's planning that we'll have an ability to provide SFX and music with levels themselves and you will be able to play them through Python scripts, but now we have only this.

Example:
```python
import sandbox2d

sandbox2d.sound("menu_hit")
sandbox2d.log("This script executes only if you did something unlawful. You will receive punishment.")
```
