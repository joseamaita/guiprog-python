# PyQt4

## Pop-up alert

### First version

```python
#!/usr/bin/env python
import sys
import time
from PyQt4.QtCore import *
from PyQt4.QtGui import *

app = QApplication(sys.argv)

try:
    due = QTime.currentTime()
    message = "Alert!"
    if len(sys.argv) < 2:
        raise ValueError
    hours, mins = sys.argv[1].split(":")
    due = QTime(int(hours), int(mins))
    if not due.isValid():
        raise ValueError
    if len(sys.argv) > 2:
        message = " ".join(sys.argv[2:])

except ValueError:
    message = "Usage: alert.pyw HH:MM [optional message]" # 24hr clock

while QTime.currentTime() < due:
    time.sleep(20) # 20 seconds

label = QLabel("<font color=red size=72><b>{}</b></font>"
               .format(message))
label.setWindowFlags(Qt.SplashScreen)
label.show()
QTimer.singleShot(60000, app.quit) # 1 minute
app.exec_()
```

### Second version

```python
#!/usr/bin/env python
import sys
import time
from PyQt4.QtCore import (QTime, QTimer, Qt, SIGNAL)
from PyQt4.QtGui import (QApplication, QLabel)

app = QApplication(sys.argv)

try:
    due = QTime.currentTime()
    message = "Alert!"
    if len(sys.argv) < 2:
        raise ValueError
    hours, mins = sys.argv[1].split(":")
    due = QTime(int(hours), int(mins))
    if not due.isValid():
        raise ValueError
    if len(sys.argv) > 2:
        message = " ".join(sys.argv[2:])

except ValueError:
    message = "Usage: alert.pyw HH:MM [optional message]" # 24hr clock

while QTime.currentTime() < due:
    time.sleep(20) # 20 seconds

label = QLabel("<font color=red size=72><b>{0}</b></font>"
               .format(message))
label.setWindowFlags(Qt.SplashScreen)
label.show()
QTimer.singleShot(60000, app.quit) # 1 minute
app.exec_()
```

### Third version

```python
#!/usr/bin/env python
import sys
import time
from PyQt4.QtCore import *
from PyQt4.QtGui import *

app = QApplication(sys.argv)

try:
    due = QTime.currentTime()
    message = "Alert!"
    if len(sys.argv) < 2:
        raise ValueError
    hours, mins = sys.argv[1].split(":")
    due = QTime(int(hours), int(mins))
    if not due.isValid():
        raise ValueError
    if len(sys.argv) > 2:
        message = " ".join(sys.argv[2:])

except ValueError:
    message = "Usage: alert.pyw HH:MM [optional message]" # 24hr clock

while QTime.currentTime() < due:
    time.sleep(20) # 20 seconds

font = QFont("Helvetica", 36, QFont.Bold)
fm = QFontMetrics(font)
pixmap = QPixmap(fm.width(message) + 5, fm.height() + 5)
pixmap.fill(Qt.white)
painter = QPainter(pixmap)
document = QTextDocument()
document.setDefaultFont(font)
document.setHtml("<font color=red>{}</font>".format(message))
document.drawContents(painter)
painter.end()
label = QLabel()
label.setPixmap(pixmap)
label.setMask(pixmap.createMaskFromColor(Qt.white))
label.setWindowFlags(Qt.SplashScreen|Qt.FramelessWindowHint)
label.show()
QTimer.singleShot(60000, app.quit) # 1 minute
app.exec_()
```

### Fourth version

```python
#!/usr/bin/env python
import sys
import time
from PyQt4.QtCore import (QTime, QTimer, Qt, SIGNAL)
from PyQt4.QtGui import (QApplication, QFont, QFontMetrics, QLabel, 
                         QPainter, QPixmap, QTextDocument)

app = QApplication(sys.argv)

try:
    due = QTime.currentTime()
    message = "Alert!"
    if len(sys.argv) < 2:
        raise ValueError
    hours, mins = sys.argv[1].split(":")
    due = QTime(int(hours), int(mins))
    if not due.isValid():
        raise ValueError
    if len(sys.argv) > 2:
        message = " ".join(sys.argv[2:])

except ValueError:
    message = "Usage: alert.pyw HH:MM [optional message]" # 24hr clock

while QTime.currentTime() < due:
    time.sleep(20) # 20 seconds

font = QFont("Helvetica", 36, QFont.Bold)
fm = QFontMetrics(font)
pixmap = QPixmap(fm.width(message) + 5, fm.height() + 5)
pixmap.fill(Qt.white)
painter = QPainter(pixmap)
document = QTextDocument()
document.setDefaultFont(font)
document.setHtml("<font color=red>{0}</font>".format(message))
document.drawContents(painter)
painter.end()
label = QLabel()
label.setPixmap(pixmap)
label.setMask(pixmap.createMaskFromColor(Qt.white))
label.setWindowFlags(Qt.SplashScreen|Qt.FramelessWindowHint)
label.show()
QTimer.singleShot(60000, app.quit) # 1 minute
app.exec_()
```
