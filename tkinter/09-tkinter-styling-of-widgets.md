# Tkinter

## Styling of widgets

### Basic guidelines

First, let's see how to specify the color options for a widget. You can 
specify the following two types of color for most widgets:

* The background color
* The foreground color

You can specify the color by using hexadecimal color codes for the 
proportion of red, green, and blue. The commonly used representations 
are `#rgb` (4 bits), `#rrggbb` (8 bits), and `#rrrgggbbb` (12 bits).

For example, `#fff` is white, `#000000` is black, `#f00` is 
red ( `R=0xf , G=0x0 , B=0x0` ), `#00ff00` is 
green ( `R=0x00 , G=0xff , B=0x00` ), and `#000000fff` is 
blue ( `R=0x000 , G=0x000 , B=0xfff` ).

Alternatively, Tkinter provides mapping for standard color names. For a 
list of predefined named colors, 
go [here](http://wiki.tcl.tk/37701) or 
also [here](http://wiki.tcl.tk/16166).

Next, let's have a look at how to specify fonts for our widgets. A font 
can be represented as a string by using the following string signature:

```
{font family} fontsize fontstyle
```

The elements of the preceding syntax can be explained as follows:

* font family: This is the complete font family long name.
* fontsize: This is a printer's **point unit (pt)** 
or **pixel unit (px)**.
* fontstyle: This is a mix of `normal/bold/italic` 
and `underline/overstrike`.

The following are the examples that illustrate the method of specifying 
fonts:

```python
widget.configure(font='Times 8')
widget.configure(font='Helvetica 24 bold italic')
```

If you set a Tkinter dimension in a plain integer, the measurements take 
place in pixel units. Alternatively, Tkinter accepts four other 
measurement units, which are m (millimeters), c (centimeters), i 
(inches), and p (printer's points, which are about 1/72").

For instance, if you want to specify the wrap length of a button in 
terms of a printer's point, you can specify it as follows:

```python
button.configure(wraplength="36p")
```

The default border width for most Tkinter widgets is `2 px`. You can 
change the border width of the widgets by specifying it explicitly, as 
shown in the following line:

```python
button.configure(borderwidth=5)
```

The `relief` style of a widget refers to the difference between the 
highest and lowest elevations in a widget. Tkinter offers six possible 
relief styles: `flat`, `raised`, `sunken`, `groove`, `solid`, 
and `ridge`. The line to configure it is:

```python
button.configure(relief='raised')
```

Tkinter lets you change the style of the mouse cursor when you hover 
over a particular widget. This is done by using the `cursor` option, as 
follows:

```python
button.configure(cursor='cross')
```

For a complete list of available cursors, 
go [here](https://www.tcl.tk/man/tcl8.6/TkCmd/cursors.htm).

Though you can specify the styling options at each widget level, 
sometimes it may be cumbersome to do so individually for each widget. 
Widget-specific styling has the following disadvantages:

* It mixes logic and presentation into one file, making the code bulky 
and difficult to manage.
* Any change in styling has to be applied to each widget individually.
* It violates the **don't repeat yourself (DRY)** principle of effective 
coding, as you keep specifying the same style for a large number of 
widgets.

### Using the external option database

Fortunately, Tkinter now offers a way to separate presentation from 
logic and specify styles in what is called 
the **external option database**. This is nothing but a text file where 
you can specify the common styling options.

A typical option database text file looks like this:

```
*background: AntiqueWhite1
*Text*background: #454545
*Button*foreground: gray55
*Button*relief: raised
*Button*width: 3
```

In its simplest use, the asterisk ( `*` ) symbol here means that the 
particular style is applied to all the instances of the given widget. 
For a more complex usage of the asterisk in styling, 
go [here](http://infohost.nmt.edu/tcc/help/pubs/tkinter/web/resource-lines.html).

These entries are placed in an external text file. To apply this styling 
to a particular piece of code, you can simply call it by using 
the `option_readfile()` call early in your code, as shown here:

```python
root.option_readfile('optionDB')
```

### Simple Tkinter application that uses an external styling text file

First, for the whole application to work, make sure file *optionDB* is 
available in the *files* folder:

```
*Button*borderwidth:3
*Button*relief: raised
*Button*width: 3
*Button*height: 1
*Button*pady:3
```

The code for the application is:

```python
from tkinter import *
root = Tk()
root.configure(background='#4D4D4D')

root.option_readfile('files/optionDB')

text = Text(root, 
            background = '#101010', 
            foreground = '#D6D6D6', 
            borderwidth = 18, 
            relief = 'sunken', 
            width = 17, 
            height = 5)
text.insert(END, 
            "Style is knowing who you are,what "
            "you want to say, and not giving a damn.")
text.grid(row=0, column=0, columnspan=6, padx=5, pady=5)

Button(root, text='*' ).grid(row=1, column=1)
Button(root, text='^' ).grid(row=1, column=2)
Button(root, text='#' ).grid(row=1, column=3)
Button(root, text='<' ).grid(row=2, column=1)
Button(root, text='OK', cursor='target').grid(row=2, column=2)
Button(root, text='>').grid(row=2, column=3)
Button(root, text='+' ).grid(row=3, column=1)
Button(root, text='v' ).grid(row=3, column=2)
Button(root, text='-' ).grid(row=3, column=3)

for i in range(10):
    Button(root, 
           text = str(i))\
           .grid(column=3 if i%3==0  else (1 if i%3==1 else 2), 
                 row=4 if i<=3  else (5 if i<=6 else 6))


root.mainloop()
```

The following is a description of the preceding code:

* The code connects to an external styling file called `optionDB` that 
defines common styling for the widgets.
* The next segment of code creates a Text widget and specifies styling 
on the widget level.
* The next segment of code has several buttons, all of which derive 
their styling from the centralized `optionDB` file. One of the buttons 
also defines a custom cursor.

Specifying attributes such as font sizes, the border width, the widget 
width, the widget height, and padding in absolute numbers, as we have 
done in the preceding example, can cause some display variations between 
different operating systems such as Ubuntu, Windows, and Mac 
respectively. This is due to differences in the rendering engines of 
different operating systems.

Take this in consideration: when deploying cross-platform, it is better 
to avoid specifying attribute sizes in absolute numbers. It is often the 
best choice to let the platform handle the attribute sizes.

### Some common root window options

Let's see some commonly used options for the root window:

Method | Description
------------ | -------------
`root.geometry('142x280+150+200')` | You can specify the size and location of a root window by using a string of the `widthxheight + xoffset + yoffset` form.
`self.root.wm_iconbitmap('mynewicon.ico')` or `self.root.iconbitmap('mynewicon.ico ')` | This changes the title bar icon to something that is different from the default Tk icon.
`root.overrideredirect(1)` | This removes the root border frame. It hides the frame that contains the minimize, maximize, and close buttons.

Let's explain these styling options in more detail:

* `root.geometry('142x280+150+200')`: Specifying the geometry of the 
root window limits the launch size of the root window. If the widgets do 
not fit in the specified size, the widgets get clipped from the window. 
It is often better not to specify this and let Tkinter decide this for 
you.
* `self.root.wm_iconbitmap('my_icon.ico')` 
or `self.root.iconbitmap('my_icon.ico ')`: This option is only 
applicable to Windows. Unix-based operating systems do not display the 
title bar icon.
