# wxPython

## Initial setup

### Create virtual environment (version A)

```
$ mkvirtualenv --python=/usr/bin/python3.4 py34wxpy4
```

### Create virtual environment (version B)

```
$ python3.6 -m venv /home/jose-alberto/.virtualenvs/py36wxpy4
```

### Activate virtual environment

```
$ workon py34wxpy4
```

### Install the wxPython toolkit

```
(py34wxpy4) $ pip install wxpython
```

### Test if the wxPython toolkit is correctly installed

```
(py34wxpy4) $ python
>>> import wx
>>> (no error is shown)
```

### Check the wxPython version

```
(py34wxpy4) $ python
>>> import wx
>>> wx.version()
```

### Test a wxPython application with Python

```
(py34wxpy4) $ python name_of_wxpython_application.py
```

### Run a Python script from the console

```
-> (within name_of_wxpython_application.py), add this line at the top:
#!/home/jose-alberto/.virtualenvs/py34wxpy4/bin/python

(py34wxpy4) $ chmod +x name_of_wxpython_application.py
(py34wxpy4) $ ./name_of_wxpython_application.py
```

### Basic wxPython applications

This is the most basic wxPython application:

```python
import wx
app = wx.App()
frame = wx.Frame(None, -1, "Hello World")
frame.Show()
app.MainLoop()
```

This is another version of the same application:

```python
import wx
app = wx.App(False)    # Create a new app, don't redirect stdout/stderr 
                       # to a window.
frame = wx.Frame(None, wx.ID_ANY, "Hello World") # A Frame is a 
                                                 # top-level window.
frame.Show(True)    # Show the frame.
app.MainLoop()
```

![initial-setup-img](files/01-wxpython-initial-setup-a.png)
