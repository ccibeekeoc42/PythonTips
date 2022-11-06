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
import email, ssl, smtplib

sender = 'sender@gmail.com'
password = 'sender_password'
reciever = 'reciever@gmail.com'

subject = 'ANNONCEMENT'
body = '''I am a hungry boy finally!!'''

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
