Sending A Text Message With Twilio

1. Get Credentials
```
account_sid = settings.TWILIO_ACCOUNT_SID
account_auth_token = settings.TWILIO_AUTH_TOKEN
```

2. Send Message 
```
try:
    client = TwilioRestClient(account_sid, account_auth_token)
    client.messages.create(
    to = '+16472985582',
    from_ = '+16472985582',
    body = "Hello From Zaeem Maqsood",
    )

  except Exception as e:
    print(e)
    pass
```
