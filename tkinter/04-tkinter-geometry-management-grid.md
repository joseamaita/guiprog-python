# Tkinter

## Geometry management

### Simple Tkinter applications that shows the use of the grid manager

Let's see an initial authentication (login) interface:

```python
from tkinter import *
root = Tk()
Label(root, text="Username").grid(row=0, sticky=W)
Label(root, text="Password").grid(row=1, sticky=W)
Entry(root).grid(row=0, column=1, sticky=E)
Entry(root).grid(row=1, column=1, sticky=E)
Button(root, text="Login").grid(row=2, column=1, sticky=NSEW)
root.mainloop()
```

Let's have a look at an example of the `grid` manager (Find & Replace 
interface), where we use most of the common arguments to the `grid` 
method, such as `row`, `column`, `padx`, `pady`, `rowspan`, 
and `columnspan`:

```python
from tkinter import *
parent = Tk()
parent.title('Find & Replace')

Label(parent, text="Find:").grid(row = 0, 
                                 column = 0, 
                                 sticky = 'e')
Entry(parent, width=60).grid(row = 0, 
                             column = 1, 
                             padx = 2, 
                             pady = 2, 
                             sticky = 'we', 
                             columnspan = 9)
Label(parent, text="Replace:").grid(row = 1, 
                                    column = 0, 
                                    sticky = 'e')
Entry(parent).grid(row = 1, 
                   column = 1, 
                   padx = 2, 
                   pady = 2, 
                   sticky = 'we', 
                   columnspan = 9)
Button(parent, text="Find").grid(row = 0, 
                                 column = 10, 
                                 padx = 2, 
                                 pady = 2, 
                                 sticky = 'e'+'w')
Button(parent, text="Find All").grid(row = 1, 
                                     column = 10, 
                                     padx = 2, 
                                     sticky = 'e'+'w')
Button(parent, text="Replace").grid(row = 2, 
                                    column = 10, 
                                    padx = 2, 
                                    sticky = 'e'+'w')
Button(parent, text="Replace All").grid(row = 3, 
                                        column = 10, 
                                        padx = 2, 
                                        sticky = 'e'+'w')
Checkbutton(parent, text='Match whole word only ').grid(row = 2, 
                                                        column = 1, 
                                                        columnspan = 4,
                                                        sticky = 'w')
Checkbutton(parent, text='Match Case').grid(row = 3, 
                                            column = 1, 
                                            columnspan = 4, 
                                            sticky = 'w')
Checkbutton(parent, text='Wrap around').grid(row = 4, 
                                             column = 1, 
                                             columnspan = 4, 
                                             sticky = 'w')
Label(parent, text="Direction:").grid(row = 2, 
                                      column = 6, 
                                      sticky = 'w')
Radiobutton(parent, text='Up', value=1).grid(row = 3, 
                                             column = 6, 
                                             columnspan = 6, 
                                             sticky = 'w')
Radiobutton(parent, text='Down', value=2).grid(row = 3, 
                                               column = 7, 
                                               columnspan = 2, 
                                               sticky = 'e')

parent.mainloop()

```

For a complete `grid` reference, type the following command in the 
Python shell:

```
>>> import tkinter
>>> help(tkinter.Grid)
Help on class Grid in module tkinter:

class Grid(builtins.object)
 |  Geometry manager Grid.
 |  
 |  Base class to use the methods grid_* in every widget.
 |  
 |  Methods defined here:
 |  
 |  bbox = grid_bbox(self, column=None, row=None, col2=None, row2=None)
 |  
 |  columnconfigure = grid_columnconfigure(self, index, cnf={}, **kw)
 |  
 |  config = grid_configure(self, cnf={}, **kw)
 |  
 |  configure = grid_configure(self, cnf={}, **kw)
 |  
 |  forget = grid_forget(self)
 |  
 |  grid = grid_configure(self, cnf={}, **kw)
 |  
 |  grid_bbox(self, column=None, row=None, col2=None, row2=None)
 |      Return a tuple of integer coordinates for the bounding
:
```

The `grid` manager is a great tool for the development of complex 
layouts. Complex structures can be easily achieved by breaking the 
container widget into grids of rows and columns and then placing the 
widgets in grids where they are wanted. It is also commonly used to 
develop different kinds of dialog boxes.

To override the automatic sizing of the grid's columnn and rows, use the 
following code to configure the size of widgets:

```
w.columnconfigure(n, option=value, ...) AND
w.rowconfigure(N, option=value, ...)
```

Use these to configure the options for a given widget, `w`, in either 
the *nth* column or the *nth* row, specifying values for the 
options, `minsize`, `pad`, and `weight`. Note that the numbering of rows 
begins from `0` and not `1`.

The options available are as follows:

Option | Description
------------ | -------------
`minsize` | This is the minimum size of a column or row in pixels. If there is no widget in a given column or row, the cell does not appear in spite of this `minsize` specification.
`pad` | This is the external padding in pixels that will be added to the specified column or row over the size of the largest cell.
`weight` | This specifies the relative weight of a row or column and then distributes the extra space. This enables making the row or column stretchable.

For example, the following code distributes two-fifths of the extra 
space to the first column and three-fifths to the second column:

```python
w.columnconfigure(0, weight=2)
w.columnconfigure(1, weight=3)
```

The `columnconfigure()` and `rowconfigure()` methods are often used to 
implement the dynamic resizing of widgets, especially on resizing the 
root window.

Remember this: you cannot use the `grid` and `pack` methods together in 
the same container window. If you try doing that, your program will 
raise a `_tkinter.TclError` error.
