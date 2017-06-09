# wxPython

## Basic sample applications

### Simple wxPython applications

A longer but still simple version:

```python
import wx

class MyFrame(wx.Frame):

    def __init__(self):
        wx.Frame.__init__(self, None, -1, "My Frame", size=(300, 300))
        panel = wx.Panel(self, -1)
        panel.Bind(wx.EVT_MOTION,  self.OnMove)
        wx.StaticText(panel, -1, "Pos:", pos=(10, 12))
        self.posCtrl = wx.TextCtrl(panel, -1, "", pos=(40, 10))

    def OnMove(self, event):
        pos = event.GetPosition()
        self.posCtrl.SetValue("{0}, {1}".format(pos.x, pos.y))

if __name__ == '__main__':
    app = wx.App()
    frame = MyFrame()
    frame.Show(True)
    app.MainLoop()
```

A different but even longer basic version:

```python
import platform
import wx


class MyFrame(wx.Frame):
    """"""
    
    def __init__(self):
        """Constructor"""
        wx.Frame.__init__(self, 
                          None, 
                          size = (500, 200), 
                          title = 'Version Info')
        panel = wx.Panel(self)
        
        py_version = 'Python version:    ' + platform.python_version()
        wx_version = 'wxPython version:  ' + wx.version()
        os_version = 'Operating system:  ' + platform.platform()
        
        main_sizer = wx.BoxSizer(wx.VERTICAL)
        size = (20, -1)
        main_sizer.Add(wx.StaticText(panel, label=py_version), 0, wx.ALL, 5)
        main_sizer.Add(wx.StaticText(panel, label=wx_version), 0, wx.ALL, 5)
        main_sizer.Add(wx.StaticText(panel, label=os_version), 0, wx.ALL, 5)
        panel.SetSizer(main_sizer)
        
        self.Show()


if __name__ == '__main__':
    app = wx.App(False)
    frame = MyFrame()
    app.MainLoop()
```

A "minimal" test version from the creator of wxPython:

```python
import wx

class MyFrame(wx.Frame):
    def __init__(self, parent, id, title):
        wx.Frame.__init__(self, parent, id, title)
        self.Bind(wx.EVT_MOVE, self.OnMove)
        self.Bind(wx.EVT_SIZE, self.OnSize)

    def OnSize(self, event):
        size = event.GetSize()
        print("size: {0} {1}".format(size.width, size.height))

    def OnMove(self, event):
        pos = event.GetPosition()
        print("pos: {0} {1}".format(pos.x, pos.y))


class MyApp(wx.App):
    def OnInit(self):
        frame = MyFrame(None, -1, "This is a test")
        frame.Show(True)
        self.SetTopWindow(frame)
        return True


def main():
    app = MyApp(0)
    app.MainLoop()


if __name__ == "__main__":
    main()
```

An updated version of the previous application:

```python
# import the wxPython GUI package
import wx

# Create a new frame class, derived from the wxPython Frame.
class MyFrame(wx.Frame):
    def __init__(self, parent, id, title):
        # First, call the base class' __init__ method to create the frame
        wx.Frame.__init__(self, parent, id, title)
        
        # Associate some events with methods of this class
        self.Bind(wx.EVT_SIZE, self.OnSize)
        self.Bind(wx.EVT_MOVE, self.OnMove)
        
        # Add a panel and some controls to display the size and position
        panel = wx.Panel(self, -1)
        label1 = wx.StaticText(panel, -1, "Size:")
        label2 = wx.StaticText(panel, -1, "Pos:")
        self.sizeCtrl = wx.TextCtrl(panel, -1, "", style=wx.TE_READONLY)
        self.posCtrl = wx.TextCtrl(panel, -1, "", style=wx.TE_READONLY)
        self.panel = panel
        
        # Use some sizers for layout of the widgets
        sizer = wx.FlexGridSizer(2, 2, 5, 5)
        sizer.Add(label1)
        sizer.Add(self.sizeCtrl)
        sizer.Add(label2)
        sizer.Add(self.posCtrl)
        
        border = wx.BoxSizer()
        border.Add(sizer, 0, wx.ALL, 15)
        panel.SetSizerAndFit(border)
        self.Fit()
        
    # This method is called by the System when the window is resized,
    # because of the association above.
    def OnSize(self, event):
        size = event.GetSize()
        self.sizeCtrl.SetValue("{0}, {1}".format(size.width, size.height))
        
        # tell the event system to continue looking for an event handler,
        # so the default handler will get called.
        event.Skip()

    # This method is called by the System when the window is moved,
    # because of the association above.
    def OnMove(self, event):
        pos = event.GetPosition()
        self.posCtrl.SetValue("{0}, {1}".format(pos.x, pos.y))


# Every wxWidgets application must have a class derived from wx.App
class MyApp(wx.App):
    # wxWindows calls this method to initialize the application
    def OnInit(self):
        # Create an instance of our customized Frame class
        frame = MyFrame(None, -1, "This is a test")
        frame.Show(True)
        
        # Tell wxWindows that this is our main window
        self.SetTopWindow(frame)
        
        # Return a success flag
        return True


app = MyApp(0)     # Create an instance of the application class
app.MainLoop()     # Tell it to start processing events
```

A "Hello World" example:

```python
import wx

class MyApp(wx.App):
    
    def OnInit(self):
       frame = MyFrame("Hello World", (50, 60), (450, 340))
       frame.Show()
       self.SetTopWindow(frame)
       return True
    
class MyFrame(wx.Frame):
    
    def __init__(self, title, pos, size):
        wx.Frame.__init__(self, None, -1, title, pos, size)
        menuFile = wx.Menu()
        menuFile.Append(1, "&About...")
        menuFile.AppendSeparator()
        menuFile.Append(2, "E&xit")
        menuBar = wx.MenuBar()
        menuBar.Append(menuFile, "&File")
        self.SetMenuBar(menuBar)
        self.CreateStatusBar()
        self.SetStatusText("Welcome to wxPython!")
        self.Bind(wx.EVT_MENU, self.OnAbout, id=1)
        self.Bind(wx.EVT_MENU, self.OnQuit, id=2)
        
    def OnQuit(self, event):
        self.Close()
         
    def OnAbout(self, event):
        wx.MessageBox("This is a wxPython Hello world sample", 
                "About Hello World", wx.OK | wx.ICON_INFORMATION, self)
                
if __name__ == '__main__':
    app = MyApp(False)
    app.MainLoop()
```
