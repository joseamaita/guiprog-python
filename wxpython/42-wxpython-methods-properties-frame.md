# wxPython

## Putting widgets in frames

### What are the methods and properties of wx.Frame?

The following table contains some of the publicly readable and 
modifiable properties of `wx.Frame`:

Property | Description
-------- | -----------
`GetBackgroundColour()` and `SetBackgroundColour(wx.Colour)` | The background color of a frame is the color chosen for any part of the frame not covered by a child widget. You can pass a `wx.Colour` to the setter method or you can pass a string with the color name. Any string passed to a wxPython method expecting a color is interpreted as a call to the function `wx.NamedColour()`.
`GetId()` and `SetId(int)` | Returns or sets the wxPython identifier for the widget.
`GetMenuBar()` and `SetMenuBar(wx.MenuBar)` | Gets or sets the menu bar object that is currently associated with the frame (if any). Gets `None` if there is no menu bar.
`GetPosition()` and `SetPosition(wx.Point)` | Gets or sets the (x, y) position of the upper-left corner of the window, as a `wx.Point`. For top-level windows, the position is in terms of the display coordinates, for child windows, the position is in terms of the parent window.
`GetSize()` and `SetSize(wx.Size)` | Gets or sets the size of the entire window in pixels, including title bar, border, scrollbars, etc.
`GetStatusBar()` and `SetStatusBar(wx.StatusBar)` | Gets or sets the status bar object that is currently associated with the frame (if any). Gets `None` if there is no status bar.
`GetStatusBarPane()` and `SetStatusBarPane(n)` | Gets or sets the status bar pane used to display menu and toolbar help. Using `n=-1` disables help display.
`GetTitle()` and `SetTitle(string)` | Gets or sets the title string associated with a frame, which is displayed in the title bar of the frame if it was created with the `wx.CAPTION` style.
`GetToolBar()` and `SetToolBar(wx.ToolBar)`| Gets or sets the toolbar object that is currently associated with the frame (if any). Gets `None` if there is no toolbar bar.

The following table displays some of the more useful nonproperty methods 
of `wx.Frame`:

Method | Description
------ | -----------
`Centre(direction=wx.BOTH)` or `Center(direction=wx.BOTH)` | Centres the frame on the display (note that the non-American spelling `Centre`, is also defined). The `direction` parameter can have the value `wx.BOTH` in which case the frame is centered in both directions, or `wx.HORIZONTAL` or `wx.VERTICAL`, in which case it centers in only one direction.
`Close(force=False)` | This function simply generates a `wx.CloseEvent` whose handler usually tries to close the window. It doesn't close the window itself, however. The `force` parameter is `False` if the window's close handler should be able to veto the destruction of this window, `True` if it cannot.
`CreateStatusBar()` | Creates a status bar at the bottom of the frame.
`CreateToolBar()` | Creates a toolbar at the top or left of the frame.
`Destroy()` | Destroys the window safely.
`Disable()` | Disables the window.
`Enable(enable=true)` | If the argument is `True`, the frame is enabled to receive user input. If the argument is `False`, user input is disabled in the frame. A related method is `Disable()`.
`GetBestSize()` | For a `wx.Frame`, returns the minimum size for the frame that fits all of its subwindows.
`GetClientAreaOrigin()` | Returns the origin of the frame client area (in client coordinates). It may be different from (0, 0) if the frame has a toolbar.
`Iconize(iconize)` | If the argument is `True`, minimizes the frame to an icon (the exact behavior is, of course, system-dependent). If the argument is `False`, an iconized frame is restored to normal.
`IsEnabled()` | Returns `True` if the frame is currently enabled, `False` otherwise.
`IsFullScreen()` | Returns `True` if the frame is being displayed in full screen mode, `False` otherwise.
`IsIconized()` | Returns `True` if the frame is currently iconized, `False` otherwise.
`IsMaximized()` | Returns `True` if currently in the maximized state, `False` otherwise.
`IsShown()` | Returns True if the frame is currently visible, `False` otherwise.
`IsTopLevel()` | Always returns `True` for top-level widgets such as frames or dialogs, and `False` for other widget types.
`Maximize(maximize)` | If the argument is `True`, maximizes the frame to fill the screen (the exact behavior is, of course, system-dependent). This will do the same thing as the user clicking on the Maximize box of the frame, which normally will enlarge the frame such that it fills the desktop but leaves the taskbar and other system components still visible.
`OnCreateStatusBar` | Virtual function called when a status bar is requested by `CreateStatusBar`.
`OnCreateToolBar` | Virtual function called when a toolbar is requested by `CreateToolBar`.
`PopStatusText(number=0)` | Pops text from the status bar.
`ProcessCommand(id)` | Simulate a menu command.
`PushStatusText(text, number=0)` | Pushes text to the status bar.
`Refresh(eraseBackground=True, rect=None)` | Triggers a repaint event for the frame. If `rect` is none, then the entire frame is repainted. If a rectangle is specified, only that rectangle is repainted. If `eraseBackground` is `True`, the background of the window will also be repainted, if `False`, the background will not be repainted.
`SetDimensions(x, y, width, height, sizeFlags=wx.SIZE_AUTO)` | Allows you to set the size and position of the window in one method call. The position goes into the `x` and `y` arguments, the size into the `width` and `height` arguments. A value of `-1` passed to any of the first four parameters is interpreted based on the value of the `sizeFlags` argument.
`SetStatusText(text, number=0)` | Sets the status bar text and redraws the status bar.
`SetStatusWidths(widths)` | Sets the widths of the fields in the status bar.
`Show(show=True)` | If passed a value of `True`, causes the frame to be displayed. If passed a value of `False`, causes the frame to be hidden. The call `Show(False)` is equivalent to `Hide()`.
`ShowFullScreen(show, style=wx.FULLSCREEN_ALL)` | If the Boolean argument is `True`, the frame is displayed in full screen mode, meaning it is enlarged to fill the entire display including covering the taskbar or other system components on the desktop. If the argument is `False`, the frame is restored to normal size. The style argument is a bitmask. The default value, `wx.FULLSCREEN_ALL`, directs wxPython to hide all style elements of the window when in full screen mode. The following other values can be composed using bitwise operations to suppress certain parts of the frame in full screen mode: `wx.FULLSCREEN_NOBORDER`, `wx.FULLSCREEN_NOCAPTION`, `wx.FULLSCREEN_NOMENUBAR`, `wx.FULLSCREEN_NOSTATUSBAR`, `wx.FULLSCREEN_NOTOOLBAR`.

The `SetDimensions()` method described above uses a bitmask of size 
flags to define default behavior if the user specifies `-1` as the value 
for a dimension.

The following table describes the size flags for the `SetDimensions` 
method:

Flag | -1 interpreted as
---- | -----------------
`wx.ALLOW_MINUS_ONE` | a valid position or size
`wx.SIZE_AUTO` | converted to a wxPython default
`wx.SIZE_AUTO_HEIGHT` | a valid width, or a wxPython default height
`wx.SIZE_AUTO_WIDTH` | a valid height, or a wxPython default width
`wx.SIZE_USE_EXISTING` | the current value should be carried forward

Now, let's see an application that creates a default frame and shows how 
to use some methods and properties of `wx.Frame`:

```python
#!/usr/bin/env python3
import wx

class DefaultFrame(wx.Frame):

    def __init__(self, parent):
        self.title = "Default Frame"
        wx.Frame.__init__(self, 
                          parent, 
                          -1, 
                          self.title, 
                          size = (400, 100))
        self.panel = wx.Panel(self, -1)
        button = wx.Button(self.panel, 
                           -1, 
                           "Close Me", 
                           pos = (150, 15))
        self.Bind(wx.EVT_BUTTON, self.OnCloseMe, button)
        self.Bind(wx.EVT_CLOSE, self.OnCloseWindow)
        self.Centre(wx.BOTH)
        self.Enable(True)
        self.Iconize(False)
        self.id = self.GetId()
        self.panel.SetBackgroundColour("light blue")
        self.SetTitle("Methods and properties of wx.Frame")
        self.title = self.GetTitle()
        self.Refresh()

    def OnCloseMe(self, evt):
        self.Close(True)

    def OnCloseWindow(self, evt):
        self.Destroy()

class App(wx.App):
    def OnInit(self):
        frame = DefaultFrame(None)
        frame.Show(True)
        self.SetTopWindow(frame)
        return True

def main():
    app = App(False)
    app.MainLoop()


if __name__ == '__main__':
    main()
```
