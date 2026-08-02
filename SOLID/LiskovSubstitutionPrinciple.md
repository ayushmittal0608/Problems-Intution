# Liskov's Substitution Principle

For eg, let's say we have a large group of people that can perform same functions like we have lots of coders who can code well, and for all of them, their task is to code, but if we talk about frontend engineer, then they can design website, if we talk about backend engineer, then they can build functionality of website, so primary function is to code but we are extending the coder to frontend engineer to design websites and so on. Now, we have 10 companies where we want those coders to place out of which three companies are those that needs frontend engineers, hence

```
interface Coders {
  void code();
}

interface FrontendEngineer extend Coders {
  void designWebsites();
}

class FrontendCompanies implement FrontendEngineer {
  public void code() {}
  public void designWebsites() {}
}

class BackendCompanies implement BackendEngineer {
  public void code() {}
}
```

Now, let's watch it as per the lens of god, that how can we find code in such an implementation:

Suppose let's say, we have 8 coders, out of which 5 coders are frontend engineers who knows how to design websites and we have a list of 10 skills on which companies are hiring:

frontend, backend, devops, cloud, marketing, finance, hr, ai, ml, and customer service, so their id can be 0000, 0001, 0010, 0011, 0100, 0101, 0110, 0111, 1000, 1001, now if id is 0000, then coders will be hired because this code can only match if both criterias of coding and design websites is being fulfilled because in the criteria of frontend engineer by company, this ID resembles code function and design websites which needs to match the coders to be hired, but is it applying filter appropriately.

More appropriate filtration will be:
Frontend, backend, cloud, devops, ai and ml are related to coding who can code, so we assign them an ID of 0 and finance, HR, customer service and Marketing are related to non-coding who doesn't know how to code, so we assign them an ID of 1.

Hence, we have 0000, 0001, 0010, 0011, 0100 and 0101, these IDs are allocated to coding, while for non-coding, we have 100, 101, 110 and 111 which is much more optimized and work differently, like one common differentiation that is it coding or non coding, one filter, then 000 which is assigned to function design websites. When someone meets the 0000 criteria, he will be shortlisted for the frontend role. This is what is known as liskov's substitution rule.

0 - code()
- 000 - designWebsites()
- 001 - functionalities()
- 010 - manageCloud()
- 011 - devOps() and so on

1 - cantCode()
- 00 - finance()
- 01 - hr()
- 10 - support()
- 11 - marketing()






