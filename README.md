# PythonTips

In this repo, we explore some tips and tricks and some short projects.

### Email Sender

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
