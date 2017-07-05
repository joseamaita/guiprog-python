# wxPython

## Basics of inserting objects and subwindows

A version that adds widgets to a frame is:

```python
#!/usr/bin/env python
import wx

class InsertFrame(wx.Frame):
    def __init__(self, parent, id):
        wx.Frame.__init__(self, 
                          parent, 
                          id, 
                          'Frame With Button', 
                          size = (300, 100))
        panel = wx.Panel(self)
        button = wx.Button(panel, 
                           label = "Close", 
                           pos=(125, 10), 
                           size=(50, 50))
        self.Bind(wx.EVT_BUTTON, self.OnCloseMe, button)
        self.Bind(wx.EVT_CLOSE, self.OnCloseWindow)

    def OnCloseMe(self, event):
        self.Close(True)

    def OnCloseWindow(self, event):
        self.Destroy()

if __name__ == '__main__':
    app = wx.App()
    frame = InsertFrame(parent=None, id=-1)
    frame.Show()
    app.MainLoop()
```

![insert-obj-img](files/05-wxpython-basics-of-inserting-objects-and-subwindows-a.png)

Several versions that add a menubar, toolbar, or status bar to a frame 
are presented (make sure to have the *images* module in the same 
location as the script). This is the first one:

```python
#!/usr/bin/env python
# this version uses deprecated method "AddSimpleTool"
import wx
from files import images

class ToolbarFrame(wx.Frame):
    def __init__(self, parent, id):
        wx.Frame.__init__(self, 
                          parent, 
                          id, 
                          'Toolbars', 
                          size=(300, 200))
        panel = wx.Panel(self)
        panel.SetBackgroundColour('White')
        statusBar = self.CreateStatusBar()
        toolbar = self.CreateToolBar()
        toolbar.AddSimpleTool(wx.NewId(), 
                              images.getNewBitmap(), 
                              "New", 
                              "Long help for 'New'")
        toolbar.Realize()
        menuBar = wx.MenuBar()
        menu1 = wx.Menu()
        menuBar.Append(menu1, "&File")
        menu2 = wx.Menu()
        menu2.Append(wx.NewId(), "&Copy", "Copy in status bar")
        menu2.Append(wx.NewId(), "C&ut", "")
        menu2.Append(wx.NewId(), "Paste", "")
        menu2.AppendSeparator()
        menu2.Append(wx.NewId(), "&Options...", "Display Options")
        menuBar.Append(menu2, "&Edit")
        self.SetMenuBar(menuBar)

    def OnCloseMe(self, event):
        self.Close(True)

    def OnCloseWindow(self, event):
        self.Destroy()

if __name__ == '__main__':
    app = wx.App()
    frame = ToolbarFrame(parent=None, id=-1)
    frame.Show()
    app.MainLoop()
```

A newer version:

```python
#!/usr/bin/env python
# this version uses newer method "AddTool"
import wx
from files import images

class ToolbarFrame(wx.Frame):
    def __init__(self, parent, id):
        wx.Frame.__init__(self, 
                          parent, 
                          id, 
                          'Toolbars', 
                          size=(300, 200))
        panel = wx.Panel(self)
        panel.SetBackgroundColour('White')
        statusBar = self.CreateStatusBar()
        toolbar = self.CreateToolBar()
        toolbar.AddTool(wx.NewId(), 
                        "New", 
                        images.getNewBitmap(), 
                        wx.NullBitmap, 
                        wx.ITEM_NORMAL, 
                        "New", 
                        "Long help for 'New'", 
                        None)
        toolbar.Realize()
        menuBar = wx.MenuBar()
        menu1 = wx.Menu()
        menuBar.Append(menu1, "&File")
        menu2 = wx.Menu()
        menu2.Append(wx.NewId(), "&Copy", "Copy in status bar")
        menu2.Append(wx.NewId(), "C&ut", "")
        menu2.Append(wx.NewId(), "Paste", "")
        menu2.AppendSeparator()
        menu2.Append(wx.NewId(), "&Options...", "Display Options")
        menuBar.Append(menu2, "&Edit")
        self.SetMenuBar(menuBar)

    def OnCloseMe(self, event):
        self.Close(True)

    def OnCloseWindow(self, event):
        self.Destroy()

if __name__ == '__main__':
    app = wx.App()
    frame = ToolbarFrame(parent=None, id=-1)
    frame.Show()
    app.MainLoop()
```

A different but also newer version (with keyword arguments):

```python
#!/usr/bin/env python
# this version uses newer method "AddTool" with keyword arguments
import wx
from files import images

class ToolbarFrame(wx.Frame):
    def __init__(self, parent, id):
        wx.Frame.__init__(self, 
                          parent, 
                          id, 
                          'Toolbars', 
                          size=(300, 200))
        panel = wx.Panel(self)
        panel.SetBackgroundColour('White')
        statusBar = self.CreateStatusBar()
        toolbar = self.CreateToolBar()
        toolbar.AddTool(wx.NewId(), 
                        "New", 
                        images.getNewBitmap(), 
                        wx.NullBitmap, 
                        kind = wx.ITEM_NORMAL, 
                        shortHelpString = "New", 
                        longHelpString = "Long help for 'New'", 
                        clientData = None)
        toolbar.Realize()
        menuBar = wx.MenuBar()
        menu1 = wx.Menu()
        menuBar.Append(menu1, "&File")
        menu2 = wx.Menu()
        menuBar.Append(menu2, "&Edit")
        menu2.Append(wx.NewId(), "&Copy", "Copy in status bar")
        menu2.Append(wx.NewId(), "C&ut", "")
        menu2.Append(wx.NewId(), "Paste", "")
        menu2.AppendSeparator()
        menu2.Append(wx.NewId(), "&Options...", "Display Options")
        self.SetMenuBar(menuBar)

    def OnCloseMe(self, event):
        self.Close(True)

    def OnCloseWindow(self, event):
        self.Destroy()

if __name__ == '__main__':
    app = wx.App()
    frame = ToolbarFrame(parent=None, id=-1)
    frame.Show()
    app.MainLoop()
```

![insert-obj-img](files/05-wxpython-basics-of-inserting-objects-and-subwindows-b.png)

![insert-obj-img](files/05-wxpython-basics-of-inserting-objects-and-subwindows-c.png)

![insert-obj-img](files/05-wxpython-basics-of-inserting-objects-and-subwindows-d.png)

![insert-obj-img](files/05-wxpython-basics-of-inserting-objects-and-subwindows-e.png)

![insert-obj-img](files/05-wxpython-basics-of-inserting-objects-and-subwindows-f.png)

![insert-obj-img](files/05-wxpython-basics-of-inserting-objects-and-subwindows-g.png)

The *images* module is:

```python
# images.py
from wx import Image, Bitmap
from wx import EmptyIcon
import io

def getNewData():
    return \
b'\x89PNG\r\n\x1a\n\x00\x00\x00\rIHDR\x00\x00\x00\x10\x00\x00\x00\x0f\x08\x06\
\x00\x00\x00\xedsO/\x00\x00\x00\x04sBIT\x08\x08\x08\x08|\x08d\x88\x00\x00\
\x00YIDATx\x9c\xed\xd31\n@!\x0c\x03\xd0\xa4\xfe\xfb\xdfX\xe3\xf0\x97R\xa5(.\
\x0ef\x13\xe45\xa2\x92Vp\x92\xcf/\xd4\xaa\xb2\xcd\xb4\xc2\x14\x00\x00in\x90\
\x84ZUDl\xa9\xa7\xc3c\xcb-\x80\xfc\x87{d8B6=B\xdb\rfy\xc0\r\xc0\xf0\x0e\xfc\
\x1d\xaf\x84\xa7\xbf\xb1\x03\xe1,\x19&\x93\x9a\xd2\x97\x00\x00\x00\x00IEND\
\xaeB`\x82' 

def getNewBitmap():
    return Bitmap(getNewImage())

def getNewImage():
    stream = io.BytesIO(getNewData())
    return Image(stream)
```
