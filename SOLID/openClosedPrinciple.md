#  Open/Closed Principle

Now, for example, we have given single responsibility to each and every service, but how would we manage that specific service, like for eg, I have a payment service where I am using multiple payment methods like UPI, card, netbanking, wallet, etc. Now, one way to implement it is that we just give else-if conditions that if we select particular method, or we can even use switch method but if we want it to scale in a way that other payment methods won't be affected by that change, we need to opt for open/closed principle which states that code is open for extension, closed for modification.

Now, we don't have to modify the code each time affecting other methods, so now each and every method is being executed and extended independently.

```
interface PaymentGateway{
  void pay();
}

class UPIPayment implements PaymentGateway {
  public void pay(){
    console.log("Pay using UPI");
  }
}

class cardPayment implements PaymentGateway {
  public void pay(){
    console.log("Pay using Card");
  }
}

class PaymentService{
  void process(PaymentGateway gateway){
    gateway.pay();
  }
}
```

Let's now understand it through god, like what if we need to find god in this implementation, let's watch it closely:

Email Service:
- Gmail: 0, goDaddy: 1

Payment Service:
- Razorpay: 0; UPI: 00, card: 01, netbanking: 10, wallet: 11
- Stripe: 1; UPI: 00, card: 01, netbanking: 10, bank transfer: 11

Now, if we closely look at stripe, we realise that we have card and bank transfer but card can be debit card or credit card, also bank transfer can be RTGS, IMPS or NEFT, so we need to expand the idea of god for the real execution.

Now, stripe: 1 and UPI: 000, card; debit card: 010, credit card: 011, then netbanking: 100 and bank transfer; RTGS: 110, NEFT: 111, but since it is having three methods, we need to expand it to 4-digits like:

- UPI: 0000
- Card: 0100, 0110
- Netbanking: 1000
- Bank Transfer: 1100, 1101 and 1110

Now, we are using or wasting too much of the god's energy even if it is not needed, so we need to optimize it. Hence, we can state that else-if is not the greatest method to be implemented.

What if we take help of god from different dimensions: like if it is UPI (00), then no further division, if it is card (01), then it is 0 and 1, if it is netbanking (10), then no further division and if it is bank transfer (11), then it is 00, 01 and 10.

This is what is known as OCP on which this world is based upon and it is the beauty of engineering where we are too much connected to god and sometimes we refuse to say that we believe on god or don't believe on god, but that believe is also a god, and if there is no belief, it is also god and through god's grace, we have built the whole system.







