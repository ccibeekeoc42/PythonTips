# PythonTips

In this repo, we explore some tips and tricks and some short projects.

### Software, Tools, and prerequisits

1. Access to [Google Colab](https://colab.research.google.com/).

### Table Of Content

- [Annotate Dataset Features](https://github.com/ccibeekeoc42/PythonTips#annotate-dataset-features)
- [Binary Search](https://github.com/ccibeekeoc42/PythonTips#binary-search)
- [Email Sender](https://github.com/ccibeekeoc42/PythonTips#email-sender)
- [English Dictionary](https://github.com/ccibeekeoc42/PythonTips#english-dictionary)
- [Face Detection](https://github.com/ccibeekeoc42/PythonTips#face-detection)
- Files, Folders, and Directories
  - [Create Directory](https://github.com/ccibeekeoc42/PythonTips#files-and-folders-creation)
  - [Get Specific Files](https://github.com/ccibeekeoc42/PythonTips#files-and-folders-get-specific-files)
  - [Unzip Files](https://github.com/ccibeekeoc42/PythonTips#unzip-files)
- Image Handling
  - [Resizing](https://github.com/ccibeekeoc42/PythonTips#image-manipulation-resizing)
  - [Remove Background](https://github.com/ccibeekeoc42/PythonTips#image-manipulation-remove-background)
- [Math to Latex Description](https://github.com/ccibeekeoc42/PythonTips#math-to-latex-description)
- QR Codes
  - [QR Code Generator (texts & URLs)](https://github.com/ccibeekeoc42/PythonTips#qr-code-generator-texts--urls)
  - [QR Code Generator (WIFI)](https://github.com/ccibeekeoc42/PythonTips#qr-code-generator-wifi)
- [Schedule Functions](https://github.com/ccibeekeoc42/PythonTips#schedule-functions)
- [Send Text Messages](https://github.com/ccibeekeoc42/PythonTips#send-text-messages)
- [Site Connectivity Checker](https://github.com/ccibeekeoc42/PythonTips#site-connectivity-checker)
- [Timing Your Code](https://github.com/ccibeekeoc42/PythonTips#timing-your-code)
- [Using Pipes for Cleaner Code](https://github.com/ccibeekeoc42/PythonTips#using-pipes-for-cleaner-code)

### Annotate Dataset Features

- Ensure to first install the _pigeon_ module.
  `!pip install pigeon-jupyter`

```python
from pigeon import annotate

data = annotate(
    ["The food taste good.", "Very awesome resturant!", "Terrible place."],
    options=["positive", "negative"]
)
```

### Binary Search

- Ensure to the list/ sequence is sorted in ascending order.

```python
def search(nums, target):
  l, mid, r = 0, 0, len(nums)
  step = 0
  while (l <= r):
    print(f"Step{step}: {nums[l:r+1]}")
    step += 1
    mid = (l+r) // 2
    if target == nums[mid]:
      return mid
    elif target < nums[mid]:
      r = mid - 1
    else:
      l = mid + 1
  return f'{target} not found'

# Driver Code
nums, target = [1,2,3,4,5,6,7,8,9], 0
search(nums, target)
```

### Email Sender

- Ensure to first setup 2FA with your email provider (Gmail)

```python
def sendEmail(sender, password, reciever, subject, message):
  '''Sends emails using the smtp protocol'''
  import email, ssl, smtplib
  message = email.message.EmailMessage()
  message['To'] = reciever
  message['From'] = sender
  message['Subject'] = subject
  message['Date'] = email.utils.formatdate(localtime=True)
  message['Message-ID'] = email.utils.make_msgid()
  message.set_content(body)

  context = ssl.create_default_context()
  with smtplib.SMTP_SSL('smtp.gmail.com', 465, context=context) as smtp:
    smtp.login(sender, password)
    smtp.sendmail(sender, reciever, message.as_string())

# Driver Code
sender, password = 'sender@gmail.com', 'sender_password'
reciever = 'reciever@gmail.com'

subject = 'ANNONCEMENT'
body = '''"With great power, comes great responsibility." - Uncle Ben.'''
sendEmail(sender, password, reciever, subject, body)
```

### English Dictionary

- Ensure to first install the _PyDictionary_ module.
  `!pip install PyDictionary`

```python
def dictionary(word):
  '''Returns the meaning of the word'''
  from PyDictionary import PyDictionary
  diction = PyDictionary()
  result = diction.meaning(word)
  for key, value in result.items():
    for idx,item in enumerate(value):
      print(f"[{idx+1}] [{key}]: {item}")

# Driver Code
word = input("Enter a word: ")
print(dictionary(word))
```

### Face Detection

- Ensure to first install the _opencv_ module.
  `!pip install opencv-python`

```python
import cv2

face_cascade_file = cv2.CascadeClassifier('/content/face_detection/haarcascade_frontalface_default.xml')
img = cv2.imread('/content/face_detection/chris.png')
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
faces = face_cascade_file.detectMultiScale(gray, 1.1, 4)
# Drawing rectangle around face
for (x, y, w, h) in faces:
  cv2.rectangle(img, (x,y), (x+w, y+h), (0, 225, 0), 2)

cv2.imwrite("face_detected.jpg", img)
from IPython.display import Image
Image(filename='face_detected.jpg')
```

### Files and Folders (Creation)

- Both the _pathlib_ and the _calendar_ modules come with the default python installation.

```python
from pathlib import Path
import calendar

months = list(calendar.month_name[1:])
weeks = ['Week 1', 'Week 2', 'Week 3', 'Week 4']

for i, month in enumerate(months, start=1):
  for week in weeks:
    Path(f"2022/{i}.{month}/{week}").mkdir(parents=True,exist_ok=True)
```

### Files and Folders (Get Specific Files)

- Both the _pathlib_ modules come with the default python installation.

```python
from pathlib import Path

folder = Path('.')
paths = folder.glob('**/*.csv')
for path in paths:
  if path.is_file():
    print(path)
```

### Unzip Files

- Both the _pathlib_ and the _zipfile_ modules come with the default python installation.

```python
from pathlib import Path
import zipfile

current_directory = Path('.')
target_directory = Path('temp')

for path in current_directory.glob('*.zip'):
    with zipfile.ZipFile(path, 'r') as zip_file:
        zip_file.extractall(path=target_directory)
```

### Image Manipulation (Resizing)

- The _PIL_ module should come by default. If not, use this command.
  `!pip install pillow`

```python
from PIL import Image
img = Image.open('/content/me.jpg')
resized_img = img.resize((150, 150))
resized_img.save('me_150.jpg')

display(resized_img)
```

### Image Manipulation (Remove Background)

- The _PIL_ module should come by default. However, you need to install the _rembg_ module.
  `!pip install pillow` and `!pip install rembg`

```python
from PIL import Image
from rembg import remove
img = Image.open('/content/me_150.jpg')
rem_back_img = remove(img)

display(rem_back_img)
```

### Math to Latex Description

- The _math_ module comes with default python but the _latexify-py_ module would need to be installed.
  `!pip install latexify-py`.

```python
import math
import latexify

@latexify.with_latex
def solve(a,b,c):
  return (-b + math.sqrt(b**2 - 4*a*c)) / (2*a)
solve
```

### QR Code Generator (texts & URLs)

- Ensure to install the qrcode and image modules
  `!pip install qrcode image`

```python
def generateQRcode(text):
  '''returns image of a QR code'''
  qr = qrcode.QRCode(
      version=1,
      error_correction=qrcode.constants.ERROR_CORRECT_L,
      box_size=10, border=4,
  )
  qr.add_data(text)
  qr.make(fit=True)
  img = qr.make_image(fill_color="black", back_color="white")
  img.save('test.png')

# Driver Code
generateQRcode('https://www.youtube.com/watch?v=dQw4w9WgXcQ')
Image(filename='test.png')
```

### QR Code Generator (WIFI)

- Ensure to install the wifi-qrcode-generator module
  `!pip install wifi-qrcode-generator`

```python
import wifi_qrcode_generator as qr
from IPython.display import Image
qr.wifi_qrcode('WIFI name', False, 'WPA', 'WIFI password')
```

### Schedule Functions

- Ensure to install the schedule module
  `!pip install schedule`

```python
def sayHi():
  print("Hi")
  return schedule.CancelJob

import schedule, time
schedule.every(3).seconds.do(sayHi)

while True:
  schedule.run_pending()
```

### Send Text Messages

- Ensure to use the textbelt API.

```python
def sendTextMessage(msg):
  '''Sends scheduled text messages'''
  import requests
  resp = requests.post('https://textbelt.com/text', {
    'phone': '9175363007',
    'message': f'{msg}',
    'key': 'textbelt',
  })
  print(resp.json)

# Driver Code
msg = 'Hello world'
sendTextMessage(msg)
```

### Site Connectivity Checker

- The _urllib_ package should come installed by default. if not, use the command
  `!pip install urllib`

```python
def checkSiteConnectivity(url):
  '''Returns the status code of any url'''
  import urllib.request as request
  response = request.urlopen(url)
  return f"The connection status code is: {response.getcode()}"

# Driver Code
url = 'https://www.youtube.com/watch?v=dQw4w9WgXcQ&list=RDdQw4w9WgXcQ&start_radio=1'
print(checkSiteConnectivity(url))
```

### Timing Your Code

- The time module should come by default. Ensure to import it.

```python
import time

# Method 1
start = time.time()
time.sleep(5)
end = time.time()
print(end - start)

# method 2
start = time.perf_counter()
time.sleep(5)
end = time.perf_counter()
print(end - start)
```

### Using Pipes for Cleaner Code

- Ensure to install the _pipe_ package using the command.
  `!pip install pipe`

```python
from pipe import select, where

nums = [1,2,3,4,5,6,7,8,9]
# Without Pipes
without_pipes = list(
    filter(lambda x: x % 2 == 0,
            map(lambda x: x ** 2, nums))
)

# With Pipes
with_pipes =list(
    nums | select(lambda x: x ** 2) | where(lambda x: x % 2 == 0)
)

print(without_pipes)
print(with_pipes)
```
