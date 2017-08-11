Sending An Email With Send Grid 

1. Get Credentials
```
sg = sendgrid.SendGridClient(settings.SENDGRID_API_KEY)
```

2. Set-up Email Template
```
htmly = get_template('account/email/order_confirmation_email.html')
  context = {}
  context["organization"] = event.organization
  context["organization_settings"] = organization_settings
  context["event"] = event
  context["order"] = order
  context["attendees"] = attendees
  context["transaction"] = transaction
  context["organization_content"] = event.email_text
  context["cart_items"] = cart_items
  context["cart"] = cart
  html_content = htmly.render(context)
```

3. Send Message
```
message = sendgrid.Mail()
message.add_to('%s <%s>' % (order.first_name, order.email))
message.set_subject('Order Confirmation')
message.set_html(html_content)
message.set_text('Order Confirmation - %s' % (event_or_course.title))
message.set_from('%s <orders@arqamhouse.com>' % (event_or_course.registrar.name))

if event_or_course.pdf_tickets:
  # Attach file
  message.add_attachment_stream('Tickets.pdf', html.write_pdf())


# You pass substitutions to your template like this
message.add_substitution('-thing_to_sub-', 'Hello! I am in a template!')

# Turn on the template option
message.add_filter('templates', 'enable', '1')

# Tell SendGrid which template to use
message.add_filter('templates', 'template_id', '91aa67f2-c1c0-427a-abfc-fe9ca72cc08d')
```
4. Check Result
```
# Get back a response and status
status, msg = sg.send(message)
```
