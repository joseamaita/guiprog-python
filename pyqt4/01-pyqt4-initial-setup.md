# PyQt4

## Initial setup

### Create virtual environment (version A)

```
$ python3.6 -m venv /home/jose-alberto/.virtualenvs/py36qt4
```

### Activate virtual environment

```
$ workon py36qt4
```

### Download Qt4 (v4.8.6)

* Go [here](http://download.qt.io/archive/qt/4.8/4.8.6/).
* Choose the TAR version (qt-everywhere-opensource-src-4.8.6.tar.gz).
* Download the file and unpack the archive.

### Install Qt4 (v4.8.6) as root

```
# cd qt-everywhere-opensource-src-4.8.6
# ./configure
Type 'o' to use the Open Source Edition.
Type 'yes' to accept this license offer.
# make
# make install
```

### Set the PATH environment variable

```
(py36qt4) $ cd ~
(py36qt4) $ gedit .profile
# set PATH for Qt 4.8.6
PATH="/usr/local/Trolltech/Qt-4.8.6/bin:$PATH"
export PATH
(py36qt4) $ export PATH=/usr/local/Trolltech/Qt-4.8.6/bin:$PATH
```

### Download and install SIP (v4.19.2)

```
(py36qt4) $ cd ~
(py36qt4) $ cd sip-4.19.2/
(py36qt4) $ python configure.py
(py36qt4) $ make
(py36qt4) $ make install
```

### Download and install the PyQt4 toolkit

```
(py36qt4) $ cd PyQt4_gpl_x11-4.12/
(py36qt4) $ python configure-ng.py
(py36qt4) $ make
(py36qt4) $ make install
```

### Test if the PyQt4 toolkit is correctly installed

```
(py36qt4) $ python
>>> import PyQt4
>>> (no error is shown)
```

### Getting the version numbers of Qt, PyQt and SIP

```
(py36qt4) $ python
>>> from PyQt4.QtCore import QT_VERSION_STR
>>> from PyQt4.Qt import PYQT_VERSION_STR
>>> from sip import SIP_VERSION_STR
>>> QT_VERSION_STR
'4.8.6'
>>> PYQT_VERSION_STR
'4.12'
>>> SIP_VERSION_STR
'4.19.2'
```

### Test a PyQt4 application with Python

```
(py36qt4) $ python name_of_pyqt4_application.pyw
```

### Run a Python script from the console

```
-> (within name_of_pyqt4_application.pyw), add this line at the top:
#!/home/jose-alberto/.virtualenvs/py36qt4/bin/python

(py36qt4) $ chmod +x name_of_pyqt4_application.pyw
(py36qt4) $ ./name_of_pyqt4_application.pyw
```

### Basic PyQt4 application

This is the most basic PyQt4 application:

```python
import sys
from PyQt4 import QtGui
app = QtGui.QApplication(sys.argv)
w = QtGui.QWidget()
w.resize(250, 150)
w.move(300, 300)
w.setWindowTitle('Simple')
w.show()
sys.exit(app.exec_())
```

This is another version of the same application:

```python
import sys
from PyQt4 import QtGui

def main():
    app = QtGui.QApplication(sys.argv)
    
    w = QtGui.QWidget()
    w.resize(250, 150)
    w.move(300, 300)
    w.setWindowTitle('Simple')
    w.show()
    
    sys.exit(app.exec_())

if __name__ == '__main__':
    main()
```
