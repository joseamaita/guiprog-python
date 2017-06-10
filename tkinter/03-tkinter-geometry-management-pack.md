# Tkinter

## Geometry management

### Simple Tkinter applications that shows the use of the pack manager

In our first version, we see the use of the 'side' and 'fill' options, 
and then, the use of the 'expand' and 'fill' options:

```python
from tkinter import *
root = Tk()

frame = Frame(root)
# demo of side and fill options
Label (frame, text="Pack Demo of side and fill").pack()
Button(frame, text="A").pack(side=LEFT, fill=Y)
Button(frame, text="B").pack(side=TOP,  fill=X)
Button(frame, text="C").pack(side=RIGHT, fill=NONE)
Button(frame, text="D").pack(side=TOP, fill=BOTH)
frame.pack() 
# note the top frame does not expand nor does it fill in 
#X or Y directions

# demo of expand options - best understood by expanding the root widget
# and seeing the effect on all the three buttons below.
Label (root, text="Pack Demo of expand").pack()
Button(root, text="I do not expand").pack()
Button(root, text="I do not fill x but I expand").pack(expand=1)
Button(root, text="I fill x and expand").pack(fill=X, expand=1)

root.mainloop()
```

The pack manager is ideally suited for the following two kinds of 
situation:

* Placing widgets in a top-down manner
* Placing widgets side by side

Let's see:

```python
from tkinter import *
root = Tk()
parent = Frame(root)

# placing widgets top-down
Button(parent, text='ALL IS WELL').pack(fill=X)
Button(parent, text='BACK TO BASICS').pack(fill=X)
Button(parent, text='CATCH ME IF U CAN').pack(fill=X)

# placing widgets side by side
Button(parent, text='LEFT').pack(side=LEFT)
Button(parent, text='CENTER').pack(side=LEFT)
Button(parent, text='RIGHT').pack(side=LEFT)
parent.pack()
root.mainloop()
```

For a complete `pack` reference, type the following command in the 
Python shell:

```
>>> import tkinter
>>> help(tkinter.Pack)
Help on class Pack in module tkinter:

class Pack(builtins.object)
 |  Geometry manager Pack.
 |  
 |  Base class to use the methods pack_* in every widget.
 |  
 |  Methods defined here:
 |  
 |  config = pack_configure(self, cnf={}, **kw)
 |  
 |  configure = pack_configure(self, cnf={}, **kw)
 |  
 |  forget = pack_forget(self)
 |  
 |  info = pack_info(self)
 |  
 |  pack = pack_configure(self, cnf={}, **kw)
 |  
 |  pack_configure(self, cnf={}, **kw)
 |      Pack a widget in the parent widget. Use as options:
 |      after=widget - pack it after you have packed widget
 |      anchor=NSEW (or subset) - position widget according to
:
```

Using the `pack` manager is somewhat complicated as compared to 
the `grid` method, but it is a great choice in situations such as the 
following ones:

* Having a widget fill the complete container frame.
* Placing several widgets on top of each other or side by side.

Although you can create complicated layouts by nesting widgets in 
multiple frames, you will find the `grid` geometry manager more suitable 
for most of the complex layouts.
