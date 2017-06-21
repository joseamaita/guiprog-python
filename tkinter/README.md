# Tkinter

## Introduction

Tkinter provides Python applications with an easy-to-program user 
interface. Tkinter supports a collection of Tk widgets that support most 
application needs. Tkinter is the Python interface to Tk, the GUI 
toolkit for Tcl/Tk.

Like Python extensions, Tcl/Tk is implemented as a C library package 
with modules to support interpreted scripts, or *applications*. The 
Tkinter interface is implemented as a Python module, `tkinter.py`, which 
is bound to a C-extension ( `_tkinter` ) which utilizes these same 
Tcl/Tk libraries. In many cases a Tkinter programmer need not be 
concerned with the implementation of Tcl/Tk since Tkinter can be viewed 
as a simple extension of Python.

## Literature

These books will help you to know more about Tkinter:

* Python and Tkinter Programming (Manning - John E. Grayson)
* Tkinter GUI Application Development Blueprints (Packt Publishing - 
Bhaskar Chaudhary)
* Tkinter GUI Application Development HOTSHOT (Packt Publishing - 
Bhaskar Chaudhary)
* Modern Tkinter for Busy Python Developers (TkDocs.com - Mark Roseman)
* Tkinter References (New Mexico Tech - John W. Shipman)
* An Introduction to Tkinter (Fredrik Lundh)

## Overview of Tkinter and Pmw widgets

Category | Widget
------------ | -------------
Windows, Frames, Containers | tkinter.Toplevel, tkinter.Frame, tkinter.LabelFrame, Pmw.ScrolledFrame, Pmw.Group, Pmw.LabeledWidget, tkinter.PanedWindow, Pmw.PanedWidget
Text, Images | tkinter.Label, Pmw.ScrolledField
Information, Help | tkinter.Message, Pmw.Balloon, Pmw.MessageBar
Dialog | Pmw.AboutDialog, Pmw.TextDialog, Pmw.MessageDialog, Pmw.SelectionDialog, Pmw.ComboBoxDialog, Pmw.CounterDialog, Pmw.PromptDialog, Pmw.Dialog
Entry | tkinter.Entry, tkinter.Spinbox, Pmw.EntryField, tkinter.Text, Pmw.ScrolledText
Selection | tkinter.Radiobutton, tkinter.OptionMenu, Pmw.OptionMenu, tkinter.Checkbutton, tkinter.Listbox, Pmw.ScrolledListBox, Pmw.ComboBox, Pmw.RadioSelect, Pmw.NoteBook
Buttons | tkinter.Button, Pmw.ButtonBox
Menu | tkinter.Menu, tkinter.Menubutton, Pmw.MenuBar
Images, Graphics | tkinter.Canvas, Pmw.ScrolledCanvas, tkinter.Scale, tkinter.Scrollbar, tkinter.BitmapImage, tkinter.PhotoImage
Count | Pmw.Counter, Pmw.TimeCounter

## Web Resources

Title | Web Address
------------ | -------------
An Introduction to Tkinter (Work in Progress) | http://effbot.org/tkinterbook/
Tkinter 8.5 reference - a GUI for Python | http://infohost.nmt.edu/tcc/help/pubs/tkinter/web/index.html
Tk Commands, version 8.6.6 | http://www.tcl.tk/man/tcl8.6/TkCmd/contents.htm
The Tkinter Toplevel Widget | http://effbot.org/tkinterbook/toplevel.htm
The Tkinter Frame Widget | http://effbot.org/tkinterbook/frame.htm
The Tkinter LabelFrame Widget | http://effbot.org/tkinterbook/labelframe.htm
Pmw.ScrolledFrame reference manual | http://pmw.sourceforge.net/doc/ScrolledFrame.html
Pmw.Group reference manual | http://pmw.sourceforge.net/doc/Group.html
Pmw.LabeledWidget reference manual | http://pmw.sourceforge.net/doc/LabeledWidget.html
The Tkinter PanedWindow Widget | http://effbot.org/tkinterbook/panedwindow.htm
Pmw.PanedWidget reference manual | http://pmw.sourceforge.net/doc/PanedWidget.html
The Tkinter Label Widget | http://effbot.org/tkinterbook/label.htm
Pmw.ScrolledField reference manual | http://pmw.sourceforge.net/doc/ScrolledField.html
The Tkinter Message Widget | http://effbot.org/tkinterbook/message.htm
Pmw.Balloon reference manual | http://pmw.sourceforge.net/doc/Balloon.html
Pmw.MessageBar reference manual | http://pmw.sourceforge.net/doc/MessageBar.html
Pmw.AboutDialog reference manual | http://pmw.sourceforge.net/doc/AboutDialog.html
Pmw.TextDialog reference manual | http://pmw.sourceforge.net/doc/TextDialog.html
Pmw.MessageDialog reference manual | http://pmw.sourceforge.net/doc/MessageDialog.html
Pmw.SelectionDialog reference manual | http://pmw.sourceforge.net/doc/SelectionDialog.html
Pmw.ComboBoxDialog reference manual | http://pmw.sourceforge.net/doc/ComboBoxDialog.html
Pmw.CounterDialog reference manual | http://heim.ifi.uio.no/~inf3330/scripting/doc/python/Pmw/CounterDialog.html
Pmw.PromptDialog reference manual | http://pmw.sourceforge.net/doc/PromptDialog.html
Pmw.Dialog reference manual | http://pmw.sourceforge.net/doc/Dialog.html
The Tkinter Entry Widget | http://effbot.org/tkinterbook/entry.htm
The Tkinter Spinbox Widget | http://effbot.org/tkinterbook/spinbox.htm
Pmw.EntryField reference manual | http://pmw.sourceforge.net/doc/EntryField.html
The Tkinter Text Widget | http://effbot.org/tkinterbook/text.htm
Pmw.ScrolledText reference manual | http://pmw.sourceforge.net/doc/ScrolledText.html
The Tkinter Radiobutton Widget | http://effbot.org/tkinterbook/radiobutton.htm
The Tkinter OptionMenu Widget | http://effbot.org/tkinterbook/optionmenu.htm
Pmw.OptionMenu reference manual | http://pmw.sourceforge.net/doc/OptionMenu.html
The Tkinter Checkbutton Widget | http://effbot.org/tkinterbook/checkbutton.htm
The Tkinter Listbox Widget | http://effbot.org/tkinterbook/listbox.htm
Pmw.ScrolledListBox reference manual | http://pmw.sourceforge.net/doc/ScrolledListBox.html
Pmw.ComboBox reference manual | http://pmw.sourceforge.net/doc/ComboBox.html
Pmw.RadioSelect reference manual | http://pmw.sourceforge.net/doc/RadioSelect.html
The Tkinter Button Widget | http://effbot.org/tkinterbook/button.htm
Pmw.ButtonBox reference manual | http://pmw.sourceforge.net/doc/ButtonBox.html
The Tkinter Menu Widget | http://effbot.org/tkinterbook/menu.htm
The Tkinter Menubutton Widget | http://effbot.org/tkinterbook/menubutton.htm
Pmw.MenuBar reference manual | http://pmw.sourceforge.net/doc/MenuBar.html
The Tkinter Canvas Widget | http://effbot.org/tkinterbook/canvas.htm
Pmw.ScrolledCanvas reference manual | http://pmw.sourceforge.net/doc/ScrolledCanvas.html
The Tkinter Scale Widget | http://effbot.org/tkinterbook/scale.htm
The Tkinter Scrollbar Widget | http://effbot.org/tkinterbook/scrollbar.htm
The Tkinter BitmapImage Class | http://effbot.org/tkinterbook/bitmapimage.htm
The Tkinter PhotoImage Class | http://effbot.org/tkinterbook/photoimage.htm
Pmw.Counter reference manual | http://pmw.sourceforge.net/doc/Counter.html
Pmw.TimeCounter reference manual | http://pmw.sourceforge.net/doc/TimeCounter.html
