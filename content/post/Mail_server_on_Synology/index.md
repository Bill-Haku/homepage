---
title: How to deploy a mail server on Synology NAS?
subtitle: It is always a cool idea to own a mail domain of yourself.

# Summary for listings and search engines
summary: How to deplot a mail server on Synology NAS in DSM?

# Link this post with a project
projects: []

# Date published
date: '2022-08-03T00:00:00Z'

# Date updated
lastmod: '2022-08-03T00:00:00Z'

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: ''
  focal_point: ''
  placement: 2
  preview_only: false

authors:
  - admin

tags:
  - Website
  - Mail server
  - Bill Haku

categories:
  - Web
---

# Overview

I'm firmly believe that owning an email address with your own domain suffix is a cool stuff. I've been looking forwart to it since I was very young. However, it was too defficult for a middle school or earlier student to do such a thing as the college entrance exam plays a immense role in a Chinese teenager's life. Fortunately, I have escaped from that and learning software engireneering helped me a lot to achieve this dream. Finally I am glad to tell all on the Internet that my own email address is available now. You can get contact with me by [i@hakubill.tech](mailto:i@hakubill.tech) at any time.

# Preparation

## Hardware

- Synology NAS

    Any model that is currently supported by Synology is acceptable.

    My model is DS418.

    If you install DSM on your own device, maybe it's also acceptable.

## Software

- DSM

    My Synology NAS software is DSM 7.1-42661 Update 3.

    Maybe DSM 6.0+ is also acceptable.

- Mail Server

    It is an official tool from Synology. You'd better use the newest version. My version is 1.7.4-10659.

## Others

- Domain name

    You need to own a domain name and you can configure DNS on your authority DNS server.

- Public IP address

    You need to get a public IP address from your ISP. In my experience, public IP address is not provided to every user in some regions, for example, in China.

    If you want to know how to check if you are using a public IP address or not, you can refer to [this](https://www.howtogeek.com/117371/how-to-find-your-computers-private-public-ip-addresses/) or search it on [Google](https://www.google.com).

# Operation Steps

## Configure your authority DNS server

You need to create a secondary domain name for your mail server. For example: `mail.yourdomain.com`. If you have a static Public IP address, you can create an A record and use your IP address as the value of the record.

However, not everyone has a static Public IP address. If you don't have a static Public IP address, you can still use the dynamic Public IP address. What you need to do first is to configure a DDNS service.

> Don't worry too much about it. Fortunately, it is so simple that you can find many online tutorials on how to do it. What's more, you can also find many free DDNS service providers. [FreeDDNS](https://www.hostddns.us) and [Huashengke](https://hsk.oray.com) are recommended. If you use Synology NAS, you can use the built-in DDNS service provided by Synology.

After finishing DDNS configuration, you get a domain conbined with your Public IP address. However, the domain name is provided by your DDNS service provider (eg. yourname.ddns.com). You can add a CNAME record to your authority DNS server. Value is your DDNS domain name, and name is your mail server's secondary domain name.

Next, you need to add an MX record to your authority DNS server. If your domain name is `yourdomain.com`, and you want your mail addresses show like `someone@yourdomain.com`, you can add an MX record with the name of `@.yourdomain.com` and the value of `mail.yourdomain.com`.

Now, you have finished the authority DNS server configuration. Let's go to the next.

## Configure your Synology NAS

### Install Mail Server

You can download and install Synology Mail Server from the Package Center.

### Configure Mail Server

- Enable SMTP

  Click the checkbox in front of the "Enable SMTP" option. Enable SMTP authentication is recommended.

  Next is to configure your host name (FQDN). Just as I have mentioned above, if you want to make your main address in a form like `someone@yourdomain.com`, enter `yourdomain.com` in the "Host name" field.

  The port number is 25 by default. You can change it if you want. But just keep it is okay. Next, click the checkbox to enable SMTP-SSL and SMTP-TLS. Keep the port number 465 and 587 provided by default.

- Enable IMAP/POP3

  Click all the checkboxes in the third tab. You know what I am talking about when you see it.

# How to use it?

Now everything is ready. You can start to use your own mail server with your preferred domain name from now on. You can also make a web mail server on your Synology NAS if you would like to, however, I don't think it is necessary in my experience.

However, before telling you how to configure the mail client, I'd like to tell you how to customize your own username of the email.

## Customize your username

On default, the username of an email address, which means the letters before the `@` mark, provided by Synology Mail server is your user name of the Synology NAS OS. For example, if you sign in your NAS with the username `hakubill`, the email address will be `hakubill@yourdomain.com`. Every user on your NAS's OS has an independent email address and space to store the emails.

However, if you want to use another username for the email, you don't need to add a new user. You can create an alias for your self. You can find it on your Mail Server App. For example, you create an alias named `me` for yourself. Then you can use `me@yourdomain.com` as your email address. `me@yourdomain.com` and `yourusername@yourdomain.com` are both valid, and they share the same email space, which means that all the emails sent to `me@yourdomain.com` can also be found when you log in as `yourusername@yourdomain.com`.

## Configure your mail client

Next I will use the built-in Mail App on macOS as an example to show how to configure your mail client. The build-in Mail App on iOS and iPadOS is almost completely same. You can also use other mail clients like Thunderbird, Outlook, etc.

- Go to the Preferences Settings of the Mail App.

- Go to account tab and click the "+" button to add a new account.

- Select "Other Account" and click "Continue".

- Here write the OS's Username, your email address and the password of the OS's username. If you set an alias, enter your alias email address here.

- Click log in. Then it will say that it failed to verify the username or password. And more textfields will appear. Enter the username again. Keep account type as IMAP and enter the domain name of your mail server, `mail.yourdomain.com` in my case. Then go forward.

- Now everything should be done. You can use your email now! Congratulations!

# Notice

Although you can send and receive emails now by theory, you may encounter some problem when trying to send a email. Many public email service providers will ban your email and return it because it is sent from an unknown domain and is highly likely to be a spam email. Of course, there's a way to solve it. You can add a SPF record to your authority DNS server. You can find many online tutorials on how to do it. If you use Synology NAS, you can use the built-in DNS service provided by Synology. But I have no time to learn about it now. See you next time.