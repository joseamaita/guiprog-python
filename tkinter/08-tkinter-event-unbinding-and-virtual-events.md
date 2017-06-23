# Tkinter

## Event unbinding and virtual events

In addition to the `bind` method, you might find the following two 
event-related options useful in certain cases:

**unbind**

Tkinter provides the `unbind` option to undo the effect of an earlier 
binding. The syntax is as follows:

```python
widget.unbind(event)
```

The following are some examples of its usage:

```python
entry.unbind('<Alt-Shift-5>')
root.unbind_all('<F1>')
root.unbind_class('Entry', '<KeyPress-Del>')
```

**Virtual events**

Tkinter also lets you create your own events. You can give these virtual 
events any name that you want.

For example, let's suppose that you want to create a new event 
called `<<commit>>`, which is triggered by the `F9` key. To create this 
virtual event on a given widget, use the following syntax:

```python
widget.event_add('<<commit>>', '<KeyRelease-F9>')
```

You can then bind `<<commit>>` to a callback by using a normal `bind()` 
method, as follows:

```python
widget.bind('<<commit>>', callback)
```

Other event-related methods can be accessed by typing the following line 
in the Python terminal:

```python
>>> import tkinter
>>> help(tkinter.Event)
Help on class Event in module tkinter:

class Event(builtins.object)
 |  Container for the properties of an event.
 |  
 |  Instances of this type are generated if one of the following events occurs:
 |  
 |  KeyPress, KeyRelease - for keyboard events
 |  ButtonPress, ButtonRelease, Motion, Enter, Leave, MouseWheel - for mouse events
 |  Visibility, Unmap, Map, Expose, FocusIn, FocusOut, Circulate,
 |  Colormap, Gravity, Reparent, Property, Destroy, Activate,
 |  Deactivate - for window events.
 |  
 |  If a callback function for one of these events is registered
 |  using bind, bind_all, bind_class, or tag_bind, the callback is
 |  called with an Event as first argument. It will have the
 |  following attributes (in braces are the event types for which
 |  the attribute is valid):
 |  
 |      serial - serial number of event
 |  num - mouse button pressed (ButtonPress, ButtonRelease)
:
```
