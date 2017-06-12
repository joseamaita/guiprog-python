# Tkinter

## Geometry management

### Simple Tkinter application that shows the use of the place manager

Let's see an example that presents absolute and relative positioning:

```python
from tkinter import *
root = Tk()

# Absolute positioning
Button(root, text="Absolute Placement").place(x = 20, 
                                              y = 10)

# Relative positioning
Button(root, text="Relative").place(relx = 0.8, 
                                    rely=0.2, 
                                    relwidth = 0.5, 
                                    width = 10, 
                                    anchor = NE)

root.mainloop()
```

For a complete `place` reference, type the following command in the 
Python shell:

```
>>> import tkinter
>>> help(tkinter.Place)
Help on class Place in module tkinter:

class Place(builtins.object)
 |  Geometry manager Place.
 |  
 |  Base class to use the methods place_* in every widget.
 |  
 |  Methods defined here:
 |  
 |  config = place_configure(self, cnf={}, **kw)
 |  
 |  configure = place_configure(self, cnf={}, **kw)
 |  
 |  forget = place_forget(self)
 |  
 |  info = place_info(self)
 |  
 |  place = place_configure(self, cnf={}, **kw)
 |  
 |  place_configure(self, cnf={}, **kw)
 |      Place a widget in the parent widget. Use as options:
 |      in=master - master relative to which the widget is placed
 |      in_=master - see 'in' option description
:
```

The `place` manager is useful in situations where you have to implement 
the custom geometry managers, where the widget placement is decided
by the end user.

While the `pack` and `grid` managers cannot be used together in the same 
frame, the `place` manager can be used with any geometry manager within 
the same container frame.
