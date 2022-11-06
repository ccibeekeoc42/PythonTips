# PythonTips

In this repo, we explore some tips and tricks and some short projects.

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

### QR Code Generator (texts & URLs)

- Ensure to install the qrcode and image modules

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
