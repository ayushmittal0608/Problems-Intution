3x+4y=11, how will we calculate the value of x and y?

Concept Name: Extended Euclid

For understanding it, firstly we need to calculate gcd of a and b first and how is it calculated, 
  gcd(a, b) = gcd(b, a%b)
Now, at the deepest, a is becoming b and b is becoming a%b, so if b==0, we might get infinity, so we stop there and return a which is our final answer because now we have reached 1 finally, so at that point we take x=1 and y=0 which are the values inside gcd.

Now, x1 becomes y as per gcd calculation, same y1 becomes x1-(a/b)y1, now at deepest point, we have calculated that what could be the value of x1 which is x1*(11/gcd(3, 4)) and y1 which is y1*(11/gcd(3, 4)) and finally we get x1 and y1 value.

This is extended euclid which helps to calculate the value of x and y easily.
