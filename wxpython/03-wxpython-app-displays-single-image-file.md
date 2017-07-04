# wxPython

## Application that displays a single image file

The bare minimum required for this working wxPython program is:

```python
# bare.py
import wx

class App(wx.App):
    def OnInit(self):
        frame = wx.Frame(parent=None, title='Bare')
        frame.Show()
        return True

app = App()
app.MainLoop()
```

Now, let's extend our minimal wxPython program:

```python
#!/usr/bin/env python
"""spare.py is a starting point for simple wxPython programs."""
import wx

class Frame(wx.Frame):
    pass


class App(wx.App):
    def OnInit(self):
        self.frame = Frame(parent=None, title='Spare')
        self.frame.Show()
        self.SetTopWindow(self.frame)
        return True

if __name__ == '__main__':
    app = App()
    app.MainLoop()
```

Next, let's create our final version (make sure to have 
the *wxPython.jpg* image file within the *files* folder):

```python
#!/usr/bin/env python
"""Hello, wxPython! program."""

import wx

class Frame(wx.Frame):
    """Frame class that displays an image."""

    def __init__(self, image, parent=None, id=-1,
                 pos=wx.DefaultPosition, title='Hello, wxPython!'):
        """Create a Frame instance and display image."""
        temp = image.ConvertToBitmap()
        size = temp.GetWidth(), temp.GetHeight()
        wx.Frame.__init__(self, parent, id, title, pos, size)
        self.bmp = wx.StaticBitmap(parent=self, label=temp)
        self.SetClientSize(size)

class App(wx.App):
    """Application class."""

    def OnInit(self):
        image = wx.Image('files/wxPython.jpg', wx.BITMAP_TYPE_JPEG)
        self.frame = Frame(image)
        self.frame.Show()
        self.SetTopWindow(self.frame)
        return True

def main():
    app = App()
    app.MainLoop()

if __name__ == '__main__':
    main()
```

![single-image-img](files/03-wxpython-app-displays-single-image-file-a.png)
