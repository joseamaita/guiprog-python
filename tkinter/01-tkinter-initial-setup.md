# Tkinter

## Initial setup

### Create virtual environment

```
$ python3.6 -m venv /home/jose-alberto/.virtualenvs/py36tk86
```

### Activate virtual environment

```
$ workon py36tk86
```

### Test if the Tkinter module is installed on your Python distribution

```
(py36tk86) $ python
>>> import tkinter
>>> (no error is shown)
```

### Check the Tkinter version

```
(py36tk86) $ python
>>> import tkinter
>>> tkinter._test()
```

### Install Pmw (Python MegaWidgets)

```
(py36tk86) $ pip install Pmw

```

### Test a Tkinter application with Python

```
(py36tk86) $ python name_of_tkinter_application.py
```

### Run a Python script from the console

```
-> (within name_of_tkinter_application.py), add this line at the top:
#!/home/jose-alberto/.virtualenvs/py36tk86/bin/python

(py36tk86) $ chmod +x name_of_tkinter_application.py
(py36tk86) $ ./name_of_tkinter_application.py
```

### Basic Tkinter applications

This is the most basic Tkinter application:

```python
from tkinter import *
root = Tk()
root.mainloop()
```

This is another basic application:

```python
from tkinter import Label, mainloop
Label(text='This has to be the\nsimplest bit of code').pack()
mainloop()
```

Another version:

```python
from tkinter import *
root = Tk()
my_label = Label(root,text="I am a label widget")
my_button = Button(root,text="I am a button")
my_label.pack()
my_button.pack()
root.mainloop()
```
