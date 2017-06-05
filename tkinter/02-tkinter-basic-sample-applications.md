# Tkinter

## Basic sample applications

### Simple Tkinter application that does an incremental count

This simple Tkinter application shows basic concepts and principles, and 
involves a button for incremental count:

```python
# simple_tkinter_app_count.py
# Features: button, command, count_label, count_value, hello_label
#           incr_button, main_window, quit_button
from tkinter import *
main_window = Tk()
count_label = Label(main_window, text="Count: 0")
count_label.grid(row=0, column=1)
count_value = 0

def increment_count():
	global count_value, count_label
	count_value = count_value + 1
	count_label.configure(text='Count: ' + str(count_value))

incr_button = Button(main_window, text="Increment", 
                     command=increment_count)
incr_button.grid(row=0, column=0)
quit_button = Button(main_window, text="Quit", 
                     command=main_window.destroy)
quit_button.grid(row=1, column=0)
hello_label = Label(main_window, text="Hello !", background='white',
                    foreground='red', font='Times 20',
                    relief='groove', borderwidth=3)
hello_label.grid(row=2, column=0)
button1 = Button(main_window, text="one")
button1.grid(row=3, column=0)
button2 = Button(main_window, text="two")
button2.grid(row=4, column=1)

mainloop()
```

### Simple Tkinter application that does a widget placement

This simple Tkinter application shows widget placement using the 'grid' 
method:

```python
# simple_tkinter_app_grid.py
# Features: horizontal_scroller, main, text, vertical_scroller
from tkinter import *
main = Tk()
main.columnconfigure(0, weight=1)
main.rowconfigure(0, weight=1)
text = Text(main)
text.grid(row=0, column=0, sticky='nesw')

vertical_scroller = Scrollbar(main, orient='vertical')
vertical_scroller.grid(row=0, column=1, sticky='ns')
horizontal_scroller = Scrollbar(main, orient='horizontal')
horizontal_scroller.grid(row=1, column=0, sticky='ew')

mainloop()
```

### Simple Tkinter application that does basic OOP

This simple Tkinter application shows the basic use of classes 
(object-oriented programming):

```python
# simple_tkinter_app_oop.py
# Features: class, frame, __init__, create_widgets, button, command, 
#           count_label, count_value, incr_button, main_window, 
#           quit_button
from tkinter import *
class Application(Frame):
	def __init__(self, master=None):
		Frame.__init__(self, master)
		self.grid()
		self.create_widgets()
		self.count_value = 0
	
	def create_widgets(self):
		self.count_label = Label(self, text="Count: 0")
		self.count_label.grid(row=0, column=1)
		self.incr_button = Button(self, text="Increment",
		                          command=self.increment_count)
		self.incr_button.grid(row=0, column=0)
		self.quit_button = Button(self, text="Quit",
		                          command=self.master.destroy)
		self.quit_button.grid(row=1, column=0)
		
	def increment_count(self):
		self.count_value += 1
		self.count_label.configure(text='Count: ' + 
		                           str(self.count_value))

app = Application()
app.mainloop()
```

### Simple Tkinter application that shows core widgets

First, for the whole application to work, make sure files *gir.xbm*
, *textcontent.txt* and *dance.gif* are available in the *files* folder:

```python
from tkinter import *

root = Tk()
root.title('I am a Top Level Widget, parent to other widgets')

# Create a frame widget for placing menu
my_menu_bar = Frame(root, relief='raised', bd=2)
my_menu_bar.pack(fill=X)

# Create 'Menu Button Widget 1' and 'Sub Menu 1'
my_menu_button = Menubutton(my_menu_bar, text='Menu Button Widget 1', )
my_menu_button.pack(side=LEFT)
# Menu widget
my_menu = Menu(my_menu_button, tearoff=0)
my_menu_button['menu'] = my_menu
my_menu.add('command', label='Sub Menu 1')

# Create 'Menu Button Widget 2' and 'Sub Menu 2'
menu_button_2 = Menubutton(my_menu_bar, text='Menu Button Widget 2', )
menu_button_2.pack(side=LEFT)
my_menu_2 = Menu(menu_button_2, tearoff=0)
menu_button_2['menu'] = my_menu_2
my_menu_2.add('command', label='Sub Menu 2')


# Create a 'my_frame_1' frame to have its widgets
my_frame_1 = Frame(root, bd=2, relief=SUNKEN)
my_frame_1.pack(side=LEFT)

# Add label to 'my_frame_1'
Label(my_frame_1, text='I am a Label widget').pack()

# Add 'Entry' widget to 'my_frame_1'
tv = StringVar()
Entry(my_frame_1, textvariable=tv).pack()
tv.set('I am an entry widget')

# Add 'Button' widget to 'my_frame_1'
Button(my_frame_1, text='Button widget').pack()

# Add 'Checkbutton' widget to 'my_frame_1'
Checkbutton(my_frame_1, text='CheckButton Widget').pack()

# Add 'Radiobutton' widgets to 'my_frame_1'
Radiobutton(my_frame_1, text='Radio Button  Uno', value=1).pack()
Radiobutton(my_frame_1, text='Radio Button  Dos',value=2).pack()
Radiobutton(my_frame_1, text='Radio Button  Tres', value=3).pack()

# Add 'OptionMenu' widget to 'my_frame_1'
Label(my_frame_1, text='Example of OptionMenu Widget:').pack()
OptionMenu(my_frame_1,'', "Option A", "Option B", "Option C").pack()

# Add 'BitmapImage' widget to 'my_frame_1'
Label(my_frame_1, text='Image Fun with Bitmap Class:').pack()
my_image = BitmapImage(file="files/gir.xbm")
my_label = Label(my_frame_1, image=my_image)
my_label.image = my_image
my_label.pack()


# Create a 'my_frame_2' frame to have its widgets
my_frame_2 = Frame(root, bd=2, relief=GROOVE)
my_frame_2.pack(side=RIGHT)

# Add 'PhotoImage' widget to 'my_frame_2'
Label(my_frame_2, text='Image displayed with \nPhotoImage class widget:').pack()
dance_photo = PhotoImage(file='files/dance.gif')
dance_photo_label = Label(my_frame_2, image=dance_photo)
dance_photo_label.image = dance_photo 
dance_photo_label.pack()

# Add 'Listbox' widget to 'my_frame_2'
Label(my_frame_2, text='Below is an example of my_listbox widget:').pack()
my_listbox = Listbox(my_frame_2, height=4)
for line in ['Listbox Choice 1','Choice 2','Choice 3','Choice 4']:
    my_listbox.insert(END, line)
my_listbox.pack()

# Add 'Spinbox' widget to 'my_frame_2'
Label(my_frame_2, text='Below is an example of spinbox widget:').pack()
Spinbox(my_frame_2, values=(1, 2, 4, 8,10)).pack()

# Add 'Scale' widget to 'my_frame_2'
Scale(my_frame_2, from_=0.0, to=100.0, label='Scale widget', orient=HORIZONTAL).pack()

# Add 'LabelFrame' widget to 'my_frame_2'
label_frame = LabelFrame(my_frame_2, text="Labelframe Widget", padx=10, pady=10)
label_frame.pack(padx=10, pady=10)
Entry(label_frame).pack()

# Add 'Message' widget to 'my_frame_2'
Message(my_frame_2, text='I am a Message widget').pack()


# Create a 'my_frame_3' frame to have its widgets
my_frame_3 = Frame(root, bd=2, relief=SUNKEN)

# Add 'Text' and 'Scrollbar' widgets to 'my_frame_3'
my_text = Text(my_frame_3, height=10, width=40)
file_object = open('files/textcontent.txt')
file_content = file_object.read()
file_object.close()
my_text.insert(END, file_content)
my_text.pack(side=LEFT, fill=X, padx=5)
my_scrollbar = Scrollbar(my_frame_3, orient=VERTICAL, command=my_text.yview)
my_scrollbar.pack()
my_text.configure(yscrollcommand=my_scrollbar.set)
my_frame_3.pack()


# Create a 'my_frame_4' frame to have its widgets
my_frame_4 = Frame(root).pack()

# Add 'Canvas' widget to 'my_frame_4'
my_canvas = Canvas(my_frame_4, bg='white', width=340, height=80)
my_canvas.pack()
my_canvas.create_oval(20, 15, 60, 60, fill='red')
my_canvas.create_oval(40, 15, 60, 60, fill='grey')
my_canvas.create_text(130, 38, text='I am a Canvas Widget', font=('arial', 8, 'bold'))

# Add 'PanedWindow' widget to 'my_frame_4'
Label(root, text='Below is an example of PanedWindow widget:').pack()
Label(root, text='Notice you can adjust the size of each pane by dragging it').pack()
my_paned_window_1 = PanedWindow()
my_paned_window_1.pack(fill=BOTH, expand=2)
left_pane_text = Text(my_paned_window_1, height=6, width=15)
my_paned_window_1.add(left_pane_text)
my_paned_window_2 = PanedWindow(my_paned_window_1, orient=VERTICAL)
my_paned_window_1.add(my_paned_window_2)
top_pane_text = Text(my_paned_window_2, height=3, width=3)
my_paned_window_2.add(top_pane_text)
bottom_pane_text = Text(my_paned_window_2, height=3, width=3)
my_paned_window_2.add(bottom_pane_text)

root.mainloop()
```

### A collage of Tkinter widgets

First, for the whole application to work, save the following contents as 
a file named *guido.txt* and put it in the *files* folder:

```
Pronunciation: 
In Dutch, the "G" in Guido is a hard G, pronounced roughly like the "ch" in 
Scottish "loch". (Listen to the sound clip below.) However, if you're American, 
you may also pronounce it as the Italian "Guido". I'm not too worried about the
associations with mob assassins that some people have :-) 

Spelling: 
My last name is two words, and I'd like keep it that way, the spelling on my 
credit card notwithstanding. Dutch spelling rules dictate that when used 
in combination with my first name, "van" is not capitalized: "Guido van 
Rossum". But when my lastname is used alone to refer to me, it is 
captialized, for example: "As usual, Van Rossum was right." 

Alphabetization: 
In America, I show up in the alphabet under "V". But in Europe, I show up 
under "R". And some of my friends put me under "G" in their address book... 
```

The application that shows the collage is this:

```python
from tkinter import *

class AllTkinterWidgets:
    def __init__(self, master):
        frame = Frame(master, width=500, height=400, bd=1)
        frame.pack()
        
        self.mbar = Frame(frame, relief = 'raised', bd=2)
        self.mbar.pack(fill = X)

        # Create File menu
        self.filebutton = Menubutton(self.mbar, text = 'File')
        self.filebutton.pack(side = LEFT)

        self.filemenu = Menu(self.filebutton, tearoff=0)
        self.filebutton['menu'] = self.filemenu

        # Populate File menu
        self.filemenu.add('command', label = 'Exit', command = self.quit)

        # Create  object menu
        self.objectbutton = Menubutton(self.mbar, text = 'Object', )
        self.objectbutton.pack(side = LEFT)

        self.objectmenu = Menu(self.objectbutton, tearoff=0)
        self.objectbutton['menu'] = self.objectmenu

        # Populate object menu
        self.objectmenu.add('command', label = 'object', command = self.stub)

        # Create  edit menu
        self.editbutton = Menubutton(self.mbar, text = 'Edit', )
        self.editbutton.pack(side = LEFT)

        self.editmenu = Menu(self.editbutton, tearoff=0)
        self.editbutton['menu'] = self.editmenu

        # Populate edit menu
        self.editmenu.add('command', label = 'edit', command = self.stub)

        # Create  view menu
        self.viewbutton = Menubutton(self.mbar, text = 'View', )
        self.viewbutton.pack(side = LEFT)

        self.viewmenu = Menu(self.viewbutton, tearoff=0)
        self.viewbutton['menu'] = self.viewmenu

        # Populate view menu
        self.viewmenu.add('command', label = 'view', command = self.stub)

        # Create  tools menu
        self.toolsbutton = Menubutton(self.mbar, text = 'Tools', )
        self.toolsbutton.pack(side = LEFT)

        self.toolsmenu = Menu(self.toolsbutton, tearoff=0)
        self.toolsbutton['menu'] = self.toolsmenu

        # Populate tools menu
        self.toolsmenu.add('command', label = 'tools', command = self.stub)

        # Create  help menu
        self.helpbutton = Menubutton(self.mbar, text = 'Help', )
        self.helpbutton.pack(side = RIGHT)

        self.helpmenu = Menu(self.helpbutton, tearoff=0)
        self.helpbutton['menu'] = self.helpmenu

        # Populate help menu
        self.helpmenu.add('command', label = 'help', command = self.stub)

        iframe1 = Frame(frame, bd=2, relief=SUNKEN)
        Button(iframe1, text='Button').pack(side=LEFT, padx=5)
        Checkbutton(iframe1, text='CheckButton').pack(side=LEFT, padx=5)

        v=IntVar()
        Radiobutton(iframe1, text='Button', variable=v,
                    value=3).pack(side=RIGHT, anchor=W)
        Radiobutton(iframe1, text='Dio', variable=v,
                    value=2).pack(side=RIGHT, anchor=W)
        Radiobutton(iframe1, text='Ra', variable=v,
                    value=1).pack(side=RIGHT, anchor=W)
        iframe1.pack(expand=1, fill=X, pady=10, padx=5)

        iframe2 = Frame(frame, bd=2, relief=RIDGE)
        Label(iframe2, text='Label widget:').pack(side=LEFT, padx=5)
        t = StringVar()
        Entry(iframe2, textvariable=t, bg='white').pack(side=RIGHT, padx=5)
        t.set('Entry widget')
        iframe2.pack(expand=1, fill=X, pady=10, padx=5)

        iframe3 = Frame(frame, bd=2, relief=GROOVE)
        listbox = Listbox(iframe3, height=4)
        for line in ['Listbox Entry One','Entry Two','Entry Three','Entry Four']:
            listbox.insert(END, line)
        listbox.pack(fill=X, padx=5)
        iframe3.pack(expand=1, fill=X, pady=10, padx=5)
        
        iframe4 = Frame(frame, bd=2, relief=SUNKEN)
        text=Text(iframe4, height=10, width =65)
        fd = open('files/guido.txt')
        lines = fd.read()
        fd.close()
        text.insert(END, lines)
        text.pack(side=LEFT, fill=X, padx=5)
        sb = Scrollbar(iframe4, orient=VERTICAL, command=text.yview)
        sb.pack(side=RIGHT, fill=Y)
        text.configure(yscrollcommand=sb.set)
        iframe4.pack(expand=1, fill=X, pady=10, padx=5)

        iframe5 = Frame(frame, bd=2, relief=RAISED)
        Scale(iframe5, from_=0.0, to=50.0, label='Scale widget',
              orient=HORIZONTAL).pack(side=LEFT)
        c = Canvas(iframe5, bg='white', width=340, height=100)
        c.pack()
        for i in range(25):
            c.create_oval(5+(4*i),5+(3*i),(5*i)+60,(i)+60, fill='gray70')
        c.create_text(260, 80, text='Canvas', font=('verdana', 10, 'bold'))
        iframe5.pack(expand=1, fill=X, pady=10, padx=5)
        
        iframen = Frame(frame, bd=2, relief=FLAT)
        Message(iframen, text='This is a Message widget', width=300,
                relief=SUNKEN).pack(fill=X, padx=5)
        iframen.pack(expand=1, fill=X, pady=10, padx=5)

    def quit(self):
        root.destroy()

    def stub(self):
        pass
    
root = Tk()
root.option_add('*font', ('verdana', 10, 'bold'))
all = AllTkinterWidgets(root)
root.title('Tkinter Widgets')
root.mainloop()
```
