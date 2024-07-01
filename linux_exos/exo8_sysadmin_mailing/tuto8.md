
# SysAdmin Mailing Exercise

Write a script that send CPU, Memory and available storage a E-mail to the sysAdmin 
Linux Distribution: Ubuntu

## CPU performance checking commands
### using top command
top command display all linux processes that occur
```
top
```
### using htop command
```
sudo apt install htop
htop
```
### using mpstat command
```
sudo apt install sysstat
mpstat
```

## Memory checking
### using free command
free displays memory usage
```
free -h
```

## Available Storage
### using df command
df displays storage disk usage
```
df -h
```
## using du command
du displays directories storage disk usage
```
du -sh /path/to/directory
```
## Python script to send CPU - Memory - Storage usage mail
### Step 1: install necessary libraries
```
sudo apt update
sudo apt install python3-pip
pip3 install secure-smtplib
```
## Step 2: write a correct python script
```
#!/usr/bin/env python3

import smtplib
from email.mime.text import MIMEText

def send_email(subject, to_email, filename):
    from_email = "your_email@example.com"
    password = "your_less_secure_app_access_password"

    with open(filename, 'r') as file:
        body = file.read()

    msg = MIMEText(body)
    msg['Subject'] = subject
    msg['From'] = from_email
    msg['To'] = to_email

    server = smtplib.SMTP('smtp.example.com', 587)
    server.starttls()
    server.login(from_email, password)
    server.sendmail(from_email, to_email, msg.as_string())
    server.quit()
    print('Email sent successfully.')

if __name__ == "__main__":
    send_email("Test Subject", "destinataire@example.com", "/path/to/file.txt")
```
## Some code Explanation
* We're sending a mail text with the content of the file.txt as the message.
* your SMTP server could be:
    - Gmail: SMTP server: smtp.gmail.com, Port: 587 (TLS)
    - Yahoo: SMTP server: smtp.mail.yahoo.com, Port: 587 (TLS)
    - Outlook/Hotmail: SMTP server: smtp-mail.outlook.com, Port: 587 (TLS)
* 587 is the default port SMTP server


## Gmail restrictions 
If you're using gmail as SMTP provider or server, you may encouter some restrictions on authenticating your gmail account before sending the mail.
This is due to Google security terms that restricts Less secure app access connexion to your account.

[Please check how to fix it on the following link :](https://support.google.com/accounts/answer/185833?hl=fr&utm_source=google-account&utm_medium=search-screen) 

Hope this little tuto was helpful, thanks !!!

