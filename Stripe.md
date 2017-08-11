Making A Charge With Stripe

1. "GET" DATA
```
Send Public Key with Form
```

2. POST DATA:
```
a. Get Stripe Token from data
Code:
nonce = request.POST.get("stripeToken")
if nonce:
    try:
        stripe.api_key = settings.STRIPE_SECRET_KEY
        result = stripe.Charge.create(
                amount = int(charged_amount * 100),
                currency = "cad",
                card= nonce,
                description= "Name: %s %s, Organization: %s, Event Name: %s, Event ID: %s, Order ID: %s" % (order.first_name, order.last_name, event_or_course.registrar, event.title, event.id, order.id),
            )

    # Check For Any Card Errors
    except stripe.error.CardError:
        messages.error(request, "There was a problem with your payment card. Please try another one.")
        return redirect(event.get_absolute_url())

    # If there is another Problem Catch it and display a generic error, as well as deleting the order and attendees
    except Exception as e:
        attendees.delete()
        messages.error(request, "%s" % (e))
        return redirect(event.get_absolute_url())
```

3. Save Order ID 
```
order.mark_completed(order_id=result.id)
order.save()
```
