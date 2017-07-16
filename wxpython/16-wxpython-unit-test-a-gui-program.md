# wxPython

## Unit test a GUI program

### Introduction

A key advantage of good refactoring and the MVC design pattern is that 
it makes it easier to validate the performance of your program 
using *unit tests*. A unit test is a test of a single, specific function 
of your program. Because both refactoring and the use of an MVC design 
pattern tend to break your program into smaller pieces, it is easier for 
you to write specific unit tests targeting individual parts of your 
program. Unit testing is a particularly useful tool when combined with 
refactoring, because a complete suite of unit tests allows you to verify 
that you are not introducing any errors as you move your code around.

A continual challenge in unit testing is how to test UI code. Testing a 
model is relatively straightforward, as most of the model functionality 
will not depend on user input. Testing the functionality of the 
interface itself can be more difficult because the behavior of the 
interface depends on user behavior that can be hard to encapsulate. In 
this section we'll show you how to use unit testing in wxPython, 
particularly the use of manually generated events to trigger behavior 
during a unit test.

### The unittest module

When writing user tests, it's helpful to use a pre-existing test engine 
to spare you the repetitive task of writing code to run your tests. 
The `unittest` module implements a test framework called PyUnit (a 
a Tkinter based user interface for `unittest` and some other goodies are 
available [here](http://pyunit.sourceforge.net/). A PyUnit module is 
made up of tests, test cases, and test suites. The following table 
defines the three levels of abstraction in the `unittest` module:

Item | Definition
---- | ----------
Test | An individual method called by the PyUnit engine. By convention, the name of a test method begins with `test`. A test method typically executes some code, then performs one or more assert statements to test whether the results are as expected.
TestCase | A class defining one or more individual tests that share a common setup. The class is defined in PyUnit to manage a group of such tests. The `TestCase` class has support for doing common setup before and tear down after each test, ensuring that each test runs separately from the others. The `TestCase` class also defines some special assert methods, such as `assertEqual`.
TestSuite | One or more test methods or `TestCase` objects grouped together for the purpose of being run at the same time. When you actually tell PyUnit to run tests, you pass it a `TestSuite` object to run.

A single PyUnit test can have one of three results: success, failure, or 
error. Success indicates that the test method ran to completion, all 
assertions were true, and no errors were triggered. That is, of course, 
the desirable outcome. Failure and error indicate different problems 
with the code. A failure result means that one of your assertions 
returned false, indicating that the code runs successfully, but is not 
doing what you expect. An error result means that a Python exception was 
triggered somewhere in the execution of the test, showing that your code 
is not running successfully. The first failure or error in a single test 
will end the execution of that test, even if there are more assertions 
to test in the code, and the test runner will move on to the next test.

### A unittest sample

Let's assume you want to test this custom model:

```python
#!/usr/bin/env python
# modelExample.py
import wx
from files import abstractmodel

class SimpleName(abstractmodel.AbstractModel):

    def __init__(self, first="", last=""):
        abstractmodel.AbstractModel.__init__(self)
        self.set(first, last)

    def set(self, first, last):
        self.first = first
        self.last = last
        self.update()


class ModelExample(wx.Frame):

    def __init__(self, parent, id):
        wx.Frame.__init__(self, 
                          parent, 
                          id, 
                          'Flintstones', 
                          size = (340, 200))
        panel = wx.Panel(self)
        panel.SetBackgroundColour("White")
        self.Bind(wx.EVT_CLOSE, self.OnCloseWindow)
        self.textFields = {}
        self.createTextFields(panel)
        self.model = SimpleName()
        self.model.addListener(self.OnUpdate)
        self.createButtonBar(panel)

    def buttonData(self):
        return (("Fredify", self.OnFred), 
                ("Wilmafy", self.OnWilma), 
                ("Barnify", self.OnBarney), 
                ("Bettify", self.OnBetty)) 

    def createButtonBar(self, panel, yPos=0):
        xPos = 0
        for eachLabel, eachHandler in self.buttonData():
            pos = (xPos, yPos)
            button = self.buildOneButton(panel, 
                                         eachLabel, 
                                         eachHandler, 
                                         pos)
            xPos += button.GetSize().width

    def buildOneButton(self, parent, label, handler, pos=(0, 0)):
        button = wx.Button(parent, -1, label, pos)
        self.Bind(wx.EVT_BUTTON, handler, button)
        return button

    def textFieldData(self):
        return (("First Name", (10, 50)), 
                ("Last Name", (10, 80)))

    def createTextFields(self, panel):
        for eachLabel, eachPos in self.textFieldData():
            self.createCaptionedText(panel, eachLabel, eachPos)

    def createCaptionedText(self, panel, label, pos):
        static = wx.StaticText(panel, wx.NewId(), label, pos)
        static.SetBackgroundColour("White")
        textPos = (pos[0] + 75, pos[1])
        self.textFields[label] = wx.TextCtrl(panel, 
                                             wx.NewId(), 
                                             "", 
                                             size = (100, -1), 
                                             pos = textPos, 
                                             style = wx.TE_READONLY)

    def OnUpdate(self, model):
        self.textFields["First Name"].SetValue(model.first)
        self.textFields["Last Name"].SetValue(model.last)

    def OnFred(self, event):
        self.model.set("Fred", "Flintstone")

    def OnBarney(self, event):
        self.model.set("Barney", "Rubble")

    def OnWilma(self, event):
        self.model.set("Wilma", "Flintstone")

    def OnBetty(self, event):
        self.model.set("Betty", "Rubble")

    def OnCloseWindow(self, event):
        self.Destroy()

if __name__ == '__main__':
    app = wx.App()
    frame = ModelExample(parent=None, id=-1)
    frame.Show()
    app.MainLoop()
```

To do that, first, let's write a sample `unittest` module:

```python
#!/usr/bin/env python
# testExample.py
import unittest
import modelExample
import wx

class TestExample(unittest.TestCase):    # Declaring a test case

    def setUp(self):    # Set up for each test
        self.app = wx.App()
        self.frame = modelExample.ModelExample(parent=None, id=-1)

    def tearDown(self):    # Tear down after each test
        self.frame.Destroy()

    def testModel(self):    # Declaring a test
        self.frame.OnBarney(None)
        # An assertion that could fail
        self.assertEqual("Barney", 
                         self.frame.model.first, 
                         msg = "First is wrong")
        self.assertEqual("Rubble", 
                         self.frame.model.last)

def suite():    # Creating a test suite
    suite = unittest.makeSuite(TestExample, 'test')
    return suite

if __name__ == '__main__':
    unittest.main(defaultTest='suite')    # Starting the test
```

Be aware of this:

* The test case is a subclass of `unittest.TestCase`. The test runner 
creates an instance of the class for each test, in order to best allow 
the tests to be independent of each other.
* The `setUp()` method is called before each test is run. This allows 
you to guarantee that each test starts with your application in the same 
state. In this case, we create an instance of the frame that we are 
testing.
* The `tearDown()` method is called after each test is run. This allows 
you to do any clean-up necessary to ensure that the system state remains 
consistent from test to test. Generally this includes resetting global 
data, closing database connections and the like. In this case we 
call `Destroy()` on the frame, which forces wxWidgets to exit, and keeps 
the system in a good state for the next test.
* The test method usually begins with the prefix `test`, although that 
is under your control. Test methods take no arguments. This method 
starts by explicitly calling the `OnBarney` event handler method to test 
behavior.
* The `assertEqual()` method is used to test that the model object has 
been correctly changed. The `assertEqual()` method takes two arguments, 
and the test fails if they are not equal. All PyUnit assertion methods 
take an optional `msg` argument which is displayed if the assertion 
fails (the default for `assertEqual()` is almost always useful enough).
* The `suite()` method creates a test suite through the easiest 
mechanism available, the `makeSuite()` method. The method takes a Python 
class object and a string prefix as arguments, and returns a test suite 
containing all the test methods in that class whose names begin with the 
prefix. There are other mechanisms that allow for more explicit setting 
of a test suite's contents, but this method is generally all you need. 
The `suite()` method as written above is a boilerplate template that can 
be used in all of your test modules.
* At the bottom, the PyUnit text-based runner is invoked. The argument 
is the name of a method that returns a test suite. The suite is then 
run, and the results are output to the console. If you wanted to use the 
GUI test runner, you would change this line to call the main method of 
that module.

One way to run the test would be to just type:

```
(py34wxpy4) $ ./testExample.py
```

The results of this PyUnit test, run from a console window, are as 
follows:

```
.
----------------------------------------------------------------------
Ran 1 test in 0.029s

OK
```

This is a successful test. The top line, with the dot, indicates that 
the one test ran successfully. Each test gets one character in the 
display, `.` indicates success, `F` indicates failure, and `E` indicates 
error. Then comes the simple listing of the number of tests and the 
total time elapsed, and an `OK` indicating that all tests passed.

On a failure or error, you receive a stack trace showing how Python got 
to the point of the error. If we were to change the last name test 
to `Fife`, for instance, we'd receive the following result:

```
F
======================================================================
FAIL: testModel (__main__.TestExample)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "./testExample.py", line 21, in testModel
    self.frame.model.last)
AssertionError: 'Fife' != 'Rubble'
- Fife
+ Rubble


----------------------------------------------------------------------
Ran 1 test in 0.027s

FAILED (failures=1)
```

This indicates the failure in the first line, gives the name of the 
method that failed, and a traceback showing that the assertion on line 
21 failed, and how it failed. You generally need to go a few levels deep 
in the stack trace to show where the actual failure was; the last line 
or two of the stack trace is likely to be in the `unittest` module 
itself.

### Testing user events

This test is not a complete test of the system, of course. We could also 
test that the `TextField` instances in the frame were updated with the 
values after the model was updated. That test would be reasonably 
straightforward. Another test you might want to run would be to 
automatically generate the button-click event itself, and ensure that 
the proper handler is called. That test is a little less 
straightforward. The following code shows an example:

```python
#!/usr/bin/env python
# testEventExample.py
import unittest
import modelExample
import wx

class TestExample(unittest.TestCase):

    def setUp(self):
        self.app = wx.App()
        self.frame = modelExample.ModelExample(parent=None, id=-1)

    def tearDown(self):
        self.frame.Destroy()

    def testModel(self):
        self.frame.OnBarney(None)
        self.assertEqual("Barney", 
                         self.frame.model.first, 
                         msg = "First is wrong")
        self.assertEqual("Rubble", 
                         self.frame.model.last)

    def testEvent(self):
        panel = self.frame.GetChildren()[0]
        for each in panel.GetChildren():
            if each.GetLabel() == "Wilmafy":
                wilma = each
                break
        event = wx.CommandEvent(wx.wxEVT_COMMAND_BUTTON_CLICKED, 
                                wilma.GetId())
        wilma.GetEventHandler().ProcessEvent(event)
        self.assertEqual("Wilma", self.frame.model.first)
        self.assertEqual("Flintstone", self.frame.model.last)

def suite():
    suite = unittest.makeSuite(TestExample, 'test')
    return suite

if __name__ == '__main__':
    unittest.main(defaultTest='suite')
```

In the first few lines of the `testEvent` method it finds the 
appropriate button (in this case, the "Wilmafy" button). Since we did 
not explicitly store the buttons as Python instance variables, we just 
need to walk through the panel's children list until we find the right 
button (you could also do this as a Python list comprehension if you 
wanted). The next two lines in such method create the `wx.CommandEvent` 
to be sent from the button. The single parameter to the creator 
is `wx.wxEVT_COMMAND_BUTTON_CLICKED`, a constant for the actual integer 
event type that is bound to the `EVT_BUTTON` binder object (you can find 
the integer constants in the wxPython source file `wx.py`). After that, 
we set the ID of the event to the ID of the Wilmafy button. At this 
point, the event has all the relevant features of the actual event as it 
would be created by wxPython. So, we call `ProcessEvent()` to send it 
into the system. If the code works as planned, then the model first and 
last names will be changed to "Wilma" and "Flintstone".

By generating events, you can test the responsiveness of your system 
from beginning to end. In theory, you could generate a mouse-down and 
mouse-up event within your button to ensure that the button-click event 
is created as a response. In practice, this won't work with native 
widgets because the low level `wx.Events` aren't translated back into 
native system events and sent to the native widget. However, a similar 
process could be useful when testing custom widgets (such as the 
two-button control shown previously). This kind of unit testing can give 
you confidence in the responsiveness of your application.
