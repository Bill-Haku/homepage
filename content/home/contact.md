---
# An instance of the Contact widget.
widget: contact

# This file represents a page section.
headless: true

# Order that this section appears on the page.
weight: 130

title: Contact
subtitle:

content:
  # Automatically link email and phone or display as text?
  autolink: true

  # Email form provider
  form:
    provider: netlify
    formspree:
      id:
    netlify:
      # Enable CAPTCHA challenge to reduce spam?
      captcha: false

  # Contact details (edit or remove options as required)
  email: i@hakubill.tech
  # phone: 888 888 88 88
  address:
    street: No. 221 Huangxing Road, Yangpu District
    city: Shanghai
    region: Shanghai
    postcode: '200093'
    country: China
    country_code: CN
  # coordinates:
  #   latitude: '37.4275'
  #   longitude: '-122.1697'
  # directions: Enter Building 1 and take the stairs to Office 200 on Floor 2
  office_hours:
    - 'Monday - Thursday 10:00 to 20:00'
    - 'Friday 10:00 to 19:00'
  # appointment_url: 'https://calendly.com'
  contact_links:
    - icon: twitter
      icon_pack: fab
      name: DM Me
      link: 'https://twitter.com/Haku_Bill'
    - icon: envelope
      icon_pack: fas
      name: Email to Me
      link: 'mailto:i@hakubill.tech'

design:
  columns: '2'
---
