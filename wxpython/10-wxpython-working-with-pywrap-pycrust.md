# wxPython

## Working with PyWrap and PyCrust

### Introduction

The idea of this section is to write very minimal wxPython applications 
that could be changed and inspected on-the-fly using PyWrap and PyCrust. 
Also, the purpose goes around exploring all your options interactively 
that would help you better understand wxPython, and provide you more 
confidence when it comes to writing your actual program code.

### Basic wxPython application

This is the most basic wxPython application:

```python
import wx
app = wx.App()
frame = wx.Frame(None, -1, "Hello World")
frame.Show()
app.MainLoop()
```

This version works with PyCrust:

```python
import wx

class Frame(wx.Frame):
    pass

class App(wx.App):

    def OnInit(self):
        self.frame = Frame(parent=None, id=-1, title="Title")
        self.frame.Show()
        self.SetTopWindow(self.frame)
        return True

if __name__ == '__main__':
    app = App()
    app.MainLoop()
```

Run it with PyWrap like this:

```
(py34wxpy4) $ pywrap34 buffer.py
```

Load these Python instructions in the PyCrust shell:

```python
>>> import wx
>>> app.frame.panel = wx.Panel(parent=app.frame)
>>> app.frame.panel.SetBackgroundColour('White')
>>> app.frame.panel.Refresh()
>>> app.frame.statusbar = app.frame.CreateStatusBar(number=3)
>>> app.frame.statusbar.SetStatusText("Left", 0)
>>> app.frame.statusbar.SetStatusText("Center", 1)
>>> app.frame.statusbar.SetStatusText("Right", 2)
>>> app.frame.menubar = wx.MenuBar()
>>> menu = wx.Menu()
>>> app.frame.menubar.Append(menu, "Primary")
>>> app.frame.SetMenuBar(app.frame.menubar)
>>> menu.Append(wx.NewId(), "One", "First menu item")
>>> menu.Append(wx.NewId(), "Two", "Second menu item")
```

### A longer but still simple version

Rewrite a version that allows methods definition with PyCrust:

```python
import wx

class Frame(wx.Frame):

    def OnMove(self, event):
        pos = event.GetPosition()
        self.posCtrl.SetValue("{0}, {1}".format(pos.x, pos.y))

class App(wx.App):

    def OnInit(self):
        self.frame = Frame(parent = None, 
                           id = -1, 
                           title = "My Frame", 
                           size = (300,300))
        self.frame.Show()
        self.SetTopWindow(self.frame)
        return True

if __name__ == '__main__':
    app = App()
    app.MainLoop()
```

Then, run it with PyWrap and load these Python instructions in the 
shell:

```python
>>> import wx
>>> app.frame.panel = wx.Panel(app.frame, -1)
>>> app.frame.panel.Bind(wx.EVT_MOTION,  app.frame.OnMove)
>>> wx.StaticText(app.frame.panel, -1, "Pos:", pos=(10,12))
>>> app.frame.posCtrl = wx.TextCtrl(app.frame.panel, -1, "", pos=(40,10))
```

Finally, resize the window just a bit and see the changes.

### Application that shows version and system information

A different but even longer basic version:

```python
import wx

class Frame(wx.Frame):
    pass

class App(wx.App):

    def OnInit(self):
        self.frame = Frame(parent = None, 
                           id = -1, 
                           title = "Version Info", 
                           size = (500,200))
        self.frame.Show()
        self.SetTopWindow(self.frame)
        return True

if __name__ == '__main__':
    app = App()
    app.MainLoop()
```

Then, run it with PyWrap and load these Python instructions in the 
shell:

```python
>>> import platform
>>> import wx
>>> py_version = "Python version: {}".format(platform.python_version())
>>> wx_version = "wxPython version: {}".format(wx.version())
>>> os_version = "Operating system: {}".format(platform.platform())
>>> app.frame.panel = wx.Panel(app.frame, -1)
>>> app.frame.panel.SetBackgroundColour('White')
>>> main_sizer = wx.BoxSizer(wx.VERTICAL)
>>> size = (20,-1)
>>> main_sizer.Add(wx.StaticText(app.frame.panel, label=py_version), 0, wx.ALL, 5)
>>> main_sizer.Add(wx.StaticText(app.frame.panel, label=wx_version), 0, wx.ALL, 5)
>>> main_sizer.Add(wx.StaticText(app.frame.panel, label=os_version), 0, wx.ALL, 5)
>>> app.frame.panel.SetSizer(main_sizer)
```

### Application that shows the size and position of a window

A "minimal" test version from the creator of wxPython:

```python
import wx

class Frame(wx.Frame):

    def OnSize(self, event):
        size = event.GetSize()
        self.sizeCtrl.SetValue("{0},{1}".format(size.width, size.height))

    def OnMove(self, event):
        pos = event.GetPosition()
        self.posCtrl.SetValue("{0},{1}".format(pos.x, pos.y))

class App(wx.App):

    def OnInit(self):
        self.frame = Frame(parent=None, id=-1, title="This is a test")
        self.frame.Show(True)
        self.SetTopWindow(self.frame)
        return True

def main():
    app = App(False)
    app.MainLoop()

if __name__ == '__main__':
    main()
```

Then, run it with PyWrap and load these Python instructions in the 
shell:

```python
>>> import wx
>>> app.frame.panel = wx.Panel(app.frame, -1)
>>> wx.StaticText(app.frame.panel, -1, "Pos:", pos=(10,12))
>>> app.frame.posCtrl = wx.TextCtrl(app.frame.panel, -1, "", pos=(40,10))
>>> app.frame.Bind(wx.EVT_MOVE, app.frame.OnMove)
# Move the window and see the position information on the text control
>>> wx.StaticText(app.frame.panel, -1, "Size:", pos=(10,52))
>>> app.frame.sizeCtrl = wx.TextCtrl(app.frame.panel, -1, "", pos=(40,52))
>>> app.frame.Bind(wx.EVT_SIZE, app.frame.OnSize)
# Resize the window and see the size information on the text control
```

### Application that shows the size and position of a window (updated)

An updated version of the previous application:

```python
import wx

class Frame(wx.Frame):

    def OnSize(self, event):
        size = event.GetSize()
        self.sizeCtrl.SetValue("{0},{1}".format(size.width, size.height))
        event.Skip()

    def OnMove(self, event):
        pos = event.GetPosition()
        self.posCtrl.SetValue("{0},{1}".format(pos.x, pos.y))

class App(wx.App):

    def OnInit(self):
        self.frame = Frame(parent=None, id=-1, title="This is a test")
        self.frame.Show(True)
        self.SetTopWindow(self.frame)
        return True

def main():
    app = App(False)
    app.MainLoop()

if __name__ == '__main__':
    main()
```

Then, run it with PyWrap and load these Python instructions in the 
shell:

```python
>>> import wx
>>> app.frame.panel = wx.Panel(app.frame, -1)
>>> app.frame.label1 = wx.StaticText(app.frame.panel, -1, "Size:")
>>> app.frame.label2 = wx.StaticText(app.frame.panel, -1, "Pos:")
>>> app.frame.sizeCtrl = wx.TextCtrl(app.frame.panel, -1, "", style=wx.TE_READONLY)
>>> app.frame.posCtrl = wx.TextCtrl(app.frame.panel, -1, "", style=wx.TE_READONLY)
>>> sizer = wx.FlexGridSizer(2, 2, 5, 5)
>>> sizer.Add(app.frame.label1)
>>> sizer.Add(app.frame.sizeCtrl)
>>> sizer.Add(app.frame.label2)
>>> sizer.Add(app.frame.posCtrl)
>>> border = wx.BoxSizer()
>>> border.Add(sizer, 0, wx.ALL, 15)
>>> app.frame.panel.SetSizerAndFit(border)
>>> app.frame.Fit()
>>> app.frame.Bind(wx.EVT_SIZE, app.frame.OnSize)
>>> app.frame.Bind(wx.EVT_MOVE, app.frame.OnMove)
```

### A "Hello World" example with a menu and a message box

The code is this:

```python
import wx

class Frame(wx.Frame):

    def OnQuit(self, event):
        self.Close()

    def OnAbout(self, event):
        wx.MessageBox("This is a wxPython Hello world sample", 
                      "About Hello World", 
                      wx.OK | wx.ICON_INFORMATION, 
                      self)

class App(wx.App):

    def OnInit(self):
        self.frame = Frame(parent = None, 
                           id = -1, 
                           title = "Hello World", 
                           pos = (50,60), 
                           size = (450,340))
        self.frame.Show()
        self.SetTopWindow(self.frame)
        return True

def main():
    app = App(False)
    app.MainLoop()

if __name__ == '__main__':
    main()
```

Then, run it with PyWrap and load these Python instructions in the 
shell:

```python
>>> import wx
>>> menuFile = wx.Menu()
>>> menuBar = wx.MenuBar()
>>> menuBar.Append(menuFile, "&File")
>>> menuFile.Append(1, "&About...")
>>> menuFile.AppendSeparator()
>>> menuFile.Append(2, "E&xit")
>>> app.frame.SetMenuBar(menuBar)
>>> app.frame.CreateStatusBar()
>>> app.frame.SetStatusText("Welcome to wxPython!")
>>> app.frame.Bind(wx.EVT_MENU, app.frame.OnAbout, id=1)
>>> app.frame.Bind(wx.EVT_MENU, app.frame.OnQuit, id=2)
```

### Application that displays a single image file

To run this application successfully, make sure to have 
the *wxPython.jpg* image file within the *files* folder:

```python
import wx

class Frame(wx.Frame):
    pass

class App(wx.App):

    def OnInit(self):
        self.frame = Frame(parent=None, id=-1, title="Hello, wxPython!")
        self.frame.Show()
        self.SetTopWindow(self.frame)
        return True

def main():
    app = App(False)
    app.MainLoop()

if __name__ == '__main__':
    main()
```

Then, run it with PyWrap and load these Python instructions in the 
shell:

```python
>>> import wx
>>> image = wx.Image('files/wxPython.jpg', wx.BITMAP_TYPE_JPEG)
>>> temp = image.ConvertToBitmap()
>>> size = temp.GetWidth(), temp.GetHeight()
>>> app.frame.bmp = wx.StaticBitmap(parent=app.frame, label=temp)
>>> app.frame.SetClientSize(size)
```
