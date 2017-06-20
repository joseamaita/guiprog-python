# Tkinter

## Handling widget-specific variables

You need variables with a wide variety of widgets. You likely need a 
string variable to track what the user enters into the entry widget or 
text widget. You most probably need Boolean variables to track whether 
the user has checked off the Checkbox widget. You need integer variables 
to track the value entered in a Spinbox or Slider widget.

In order to respond to changes in widget-specific variables, Tkinter 
offers its own variable class. The variable that you can use to track 
widget-specific values must be subclassed from this Tkinter variable 
class. Tkinter offers some commonly used predefined variables. They 
are `StringVar`, `IntVar`, `BooleanVar`, and `DoubleVar`.

You can use these variables to capture and play with the changes in the 
values of variables from within your callback functions. You can also 
define your own variable type, if required.

Creating a Tkinter variable is simple. You simply have to call the 
constructor:

```python
my_string = StringVar()
ticked_yes = BooleanVar()
group_choice = IntVar()
volume = DoubleVar()
```

Once the variable is created, you can use it as a widget option, as 
follows:

```python
Entry(root, textvariable=my_string)
Checkbutton(root, text="Remember Me", variable=ticked_yes)
Radiobutton(root, text="Option1", variable=group_choice, value="option1")
Scale(root, label="Volume Control", variable=volume, from=0, to=10)
```

Additionally, Tkinter provides access to the values of variables via 
the `set()` and `get()` methods, as follows:

```python
my_var.set("FooBar")
my_var.get()
```

### Simple Tkinter application with variables for login screen

```python
#!/home/jose-alberto/.virtualenvs/py36tk86/bin/python
from tkinter import *
root = Tk()

def show():
    print( "You entered:")
    print( "Employee Number: {0}".format(employee_number.get()))
    print( "Login Password: {0}".format(password.get()))
    print( "Remember Me: {0}".format(remember_me.get()))
    print( '*'*30)


Label(root, text="Employee Number:").grid(row=1, column=1)
employee_number = IntVar()
Entry(root, 
      width = 40, 
      textvariable = employee_number)\
      .grid(row =1, column =2, columnspan = 2)
employee_number.set("120350")


Label(root, text="Login Password:").grid(row=2, column=1, sticky='w')
password = StringVar()
Entry(root, 
      width = 40, 
      show = "*", 
      textvariable = password)\
      .grid(row = 2, column = 2, columnspan = 2) 
password.set("mysecretpassword")

Button(root, text="Login", command=show).grid(row=3, column=3)

remember_me = BooleanVar()
Checkbutton(root, 
            text = "Remember Me", 
            variable = remember_me)\
            .grid(row = 3, column = 2)
remember_me.set(True)

root.mainloop()
```
