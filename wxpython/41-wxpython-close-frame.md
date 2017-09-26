# wxPython

## Putting widgets in frames

### What happens when I close a frame?

When you close a frame, it goes away. Eventually. Unless the frame is 
explicitly told not to close. In other words, it's not completely 
straightforward. The purpose behind the widget closure architecture in 
wxPython is to give the closing widget ample opportunity to close 
documents or free any non-wxPython resources it might be holding onto. 
This is especially welcome if you are holding onto some kind of 
expensive external resource, such as a large data structure or a 
database connection.

Admittedly, managing resources is a more serious issue in the C++ 
wxWidgets world, since C++ does not manage cleanup of memory allocations 
for you. In wxPython, the explicit need for a multiple step closing 
process is lessened, but it can still be useful to have the extra hooks 
into the process (by the way, the switch from the word *frame* to the 
word *widget* in this paragraph is deliberate, which means, everything 
in this part is applicable to all top-level widgets, such as frames or 
dialogs).

**When a user triggers the close process**

The close process is most commonly triggered by a user action, such as 
clicking on a close box or choosing `Close` from the system menu or when 
the application calls the frame's `Close` method in response to some 
other event. When that happens, the wxPython framework causes 
an `EVT_CLOSE` event to be fired. Like any other event in the wxPython 
framework, you can bind an event handler to be called when 
an `EVT_CLOSE` happens.

If you do not declare your own event handler, the default behavior is 
invoked. This default behavior is different for frames and dialogs.

* By default, the frame handler calls the `Destroy()` method and deletes 
the frame and all of its component widgets.
* By default, the close handler for dialogs does not destroy the dialog, 
it merely simulates a cancel button press, and hides the dialog. The 
dialog object continues to exist in memory so the application can fetch 
values from its data entry widgets, if desired. The application should 
call the dialog's `Destroy()` method when it is finished with the 
dialog.

If you write your own close handler, you can use that handler to close 
or delete any external resources, but it's your responsibility to call 
the `Destroy()` method explicitly if you choose to delete the frame. 
Even though `Destroy()` is often called from `Close()`, just calling 
the `Close()` method does not guarantee the destruction of the frame. 
It's perfectly legitimate to decide to not destroy the frame under 
certain circumstances, such as when the user cancels the close. However, 
you'll still need a way to destroy the frame if you choose to. If you 
choose not to destroy the window, it's good practice to call 
the `wx.CloseEvent.Veto()` method of the close event, to signal to any 
interested party that the frame has declined the invitation to close 
itself.

If you choose to close your frame from somewhere within your program 
other than the close handler, such as from a different user event like a 
menu item, the recommended mechanism is to call the `Close()` method of 
the frame. This starts the process described previously in exactly the 
same way as a system close action would. If you must ensure that the 
frame is definitely deleted, you can call the `Destroy()` method 
directly; however, doing so may result in resources or data managed by 
the frame not being freed or saved.

**When the system triggers the close process**

If the close event is triggered by the system itself, due to system 
shutdown or something similar, there's one other place where you can 
manage the event. The `wx.App` class receives an `EVT_QUERY_END_SESSION` 
event that allows you to veto the application shutdown if desired, 
followed by a `EVT_END_SESSION` event if all running apps have approved 
the shutdown of the system or GUI environment. The behavior if you 
choose to veto the close is system-dependent.

Finally, it's worth noting that calling the `Destroy()` method of a 
widget doesn't mean that the widget is immediately destroyed. The 
destruction is actually processed when the event loop next goes idle, 
after any events that were pending when the `Destroy()` was called have 
been handled. This prevents certain problems that may occur if events 
are processed for widgets that no longer exist.

Now, let's see an application that creates a default frame and shows the 
close handlers:

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
                          style = wx.DEFAULT_FRAME_STYLE, 
                          size = (300, 100))
        self.panel = wx.Panel(self, -1)
        button = wx.Button(self.panel, 
                           -1, 
                           "Close Me", 
                           pos = (100, 15))
        self.Bind(wx.EVT_BUTTON, self.OnCloseMe, button)
        self.Bind(wx.EVT_CLOSE, self.OnCloseWindow)

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
