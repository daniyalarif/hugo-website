---
title: Why not automate 'Emails'?
author: ''
date: '2021-09-18'
slug: why-not-automate-emails
categories:
  - R
tags:
  - Blastula
subtitle: ''
summary: 'Automate your worfkflow and sending emails'
authors: []
lastmod: '2021-09-18T12:54:16+02:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---



### Automated Emails through R

Imagine you can send hundreds of emails in a click. Make a basic template, customize and send it to several in a click!

Either you use an office email or Gmail, does not matter.

Are you a professor at work, send similar emails to all your students in a click. Wait for the next post in which you will see an example case in the same page.

<br>

Library is **Blastula**. Install it NOW!!


```r
library(blastula)
library(dplyr)
```

<br>

Function `add_readable_time()` lets add current date and time in the email. Let's save that in a variable.


```r
date_time <- add_readable_time()
```

<br>

We also intend to have inline image in the email. We will create html fragment that needs to be put into email text.




```r
#img_file_path <- "automate.jpg"

img_string <- add_image(file = img_file_path)
```

<br>

Function `compose_email()` lets us formulate a full html email to be sent. There are three parts of the entire email.

1.  Header: For the top portion of email
2.  Body: Main message to communicate in the email
3.  Footer: Foot notes for the email


```r
email <-
  
  compose_email(
    
    body = md(glue::glue(
      "Hello,

Do you want to learn how to send several emails **AUTOMATED** and **FREE**!!! 

Let's **GO THEN**

{img_string}
")),
    
    footer = md(glue::glue("Email sent on {date_time} \n\n Blastula is fantastic"))
  )
```

<br>

Preview the email


```r
# email
```

Shows up in the viewer pane.

<br>

![](images/viewer.png)

<br>

Insert email password here:

![](images/Password.png)

<br>

Create SMTP credentials through the function `create_smtp_creds_file()` for Rstudio to connect with your email. Replace your email in the user field and email service in the provider.


```r
create_smtp_creds_file( file = "gmail_creds",
   user = "daniyalarifsaeed2@gmail.com",
   provider = "gmail",
   use_ssl = TRUE  )
```

```
## Please enter password in TK window (Alt+Tab)
```

```
## The SMTP credentials file (`gmail_creds`) has been generated
```

<br>

Finally, sending the email. Pipe the email into `smtp_send()`

creds_file is the same as created above.


```r
email %>%
  smtp_send(
    to = "daniyalarifsaeed@gmail.com",
    from = "daniyalarifsaeed2@gmail.com",
    subject = "Automate sending `Emails`",
    credentials = creds_file("gmail_creds")
  )
```

```
## The email message was sent successfully.
```

<br>

![](images/Received.png)
