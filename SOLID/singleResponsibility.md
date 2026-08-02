# Single Responsibility Principle

As per single responsibility principle, each class is given a single responsibility and we do not assign too many responsibilities to single class. Now, we need to adopt this single responsibility principle because software changes, tech stack changes and so on. So, we want one service to be assigned to a single class so that we can manage it effectively.

We generally segregate the project into different levels like controllers, services, repositories and models. Now, they are required to have a better system design. So, if single service is assigned a single responsibility and same for controllers, repositories and models, then we can easily shift from one part to the other part for that specific code. For eg, we want to integrate certain payment gateway which can be of razorpay, stripe, etc. then each API is having different functions being used, so if we have single responsibility of payment for managing the codebase, then we can easily shift from one mode to the other.

```
class OrderService{
  void createOrder() {}
}

class EmailService{
  void sendEmail() {}
}

class PaymentService{
  void pay() {}
}
```

Now, we want to segregate them all because we can use any email service whether it would be gmail, godaddy or anything else. Same is for payment service where we can use any payment gateway such as stripe, razorpay, etc. If that would be the case, it would be easy to switch without touching other services keeping everything entirely separate from each other leading to a better design.

If for eg, we assign a single class for each service, then we are executing different functions within same class which is too difficult for us to switch between the APIs we need because ultimately it is affecting other services attached to it. So, we need to take care on how it should be implemented.

Let's discuss it in god language so that we could know it in a better way:

- Gmail: 0, goDaddy: 1
- Stripe: 0, Razorpay: 1

Now, we can have 4 combinations, 00, 01, 10 and 11 and we have option to choose within them, now let's fix the Gmail as email service as 0, now we are just changing stripe and razorpay as 0 or 1, so either we have 00 or 01 if we are following this model but let's say we have a same class, then it would disturb the email service as well like for eg, we initially have gmail as email service, now if we change or switch between stripe and razorpay, then we are not fixing gmail as email service because it is executed two times, 00 and 01, which is expensive for us to implement because 0 and 1 are dependent over 0 which is gmail service now affecting it as well while switching.

















