## Problem
Polycarpus loves hamburgers very much. He especially adores the hamburgers he makes with his own hands. Polycarpus thinks that there are only three decent ingredients to make hamburgers from: a bread, sausage and cheese. He writes down the recipe of his favorite "Le Hamburger de Polycarpus" as a string of letters 'B' (bread), 'S' (sausage) и 'C' (cheese). The ingredients in the recipe go from bottom to top, for example, recipe "ВSCBS" represents the hamburger where the ingredients go from bottom to top as bread, sausage, cheese, bread and sausage again.

Polycarpus has nb pieces of bread, ns pieces of sausage and nc pieces of cheese in the kitchen. Besides, the shop nearby has all three ingredients, the prices are pb rubles for a piece of bread, ps for a piece of sausage and pc for a piece of cheese.

Polycarpus has r rubles and he is ready to shop on them. What maximum number of hamburgers can he cook? You can assume that Polycarpus cannot break or slice any of the pieces of bread, sausage or cheese. Besides, the shop has an unlimited number of pieces of each ingredient.

### Input
The first line of the input contains a non-empty string that describes the recipe of "Le Hamburger de Polycarpus". The length of the string doesn't exceed 100, the string contains only letters 'B' (uppercase English B), 'S' (uppercase English S) and 'C' (uppercase English C).

The second line contains three integers nb, ns, nc (1 ≤ nb, ns, nc ≤ 100) — the number of the pieces of bread, sausage and cheese on Polycarpus' kitchen. The third line contains three integers pb, ps, pc (1 ≤ pb, ps, pc ≤ 100) — the price of one piece of bread, sausage and cheese in the shop. Finally, the fourth line contains integer r (1 ≤ r ≤ 1012) — the number of rubles Polycarpus has.

Please, do not write the %lld specifier to read or write 64-bit integers in С++. It is preferred to use the cin, cout streams or the %I64d specifier.

### Output
Print the maximum number of hamburgers Polycarpus can make. If he can't make any hamburger, print 0.

## Intution:
In order to solve this problem, we need to break down the question. The input given to us is string containing B, S and C representing the recipe of Le Hamburger de Polycarpus. Now, inside the kitchen, he is having nb, ns and nc, now the catch is that the polycarpus can't cut any of the ingredient for the sake of making burgers, he is having a shop besides him, so maybe we observe the question and think off fractional knapsack but it isn't cutting ingredients to make burger.

Let's assume that the shop nearby has infinite ingredients and we also want to make maximum hamburger but we have limited rubles to make burgers. So, firstly we take low as 0 and high as 1e13 to search in infinite search space, now we need to know that how much ingredients do he require, so let's say example is BBBSSC, now hamburger wants 3B, 2S and 1C, suppose polycarpus has 6B, 4S and 1C, now when he go to shop, so needed_B=max(0, 3*mid-6) as it can't be deficit, same for S and C, now we calculate total cost as:

$$cost = (max(0, B*mid-nb))*pb + (max(0, S*mid-ns))*ps + (max(0, C*mid-nc))*pc$$

now if cost <= mid, then we return ans = mid and make low = mid+1 to try more burgers, else we reduce our search space to high = mid-1

## Code
```bash
#include<bits/stdc++.h>
using namespace std;

int main(){
  string s;
  cin>>s;
  long long nb, ns, nc;
  cin>>nb>>ns>>nc;
  long long pb, ps, pc;
  cin>>pb>>ps>>pc;
  long long ruble;
  cin>>ruble;
  long long B=0, S=0, C=0;
  for(int i=0; i<s.size(); i++){
    if(s[i]=='B'){ B++; }
    if(s[i]=='S'){ S++; }
    if(s[i]=='C'){ C++; }
  }
  long long low=0, high=1e13, ans=0;
  while(low<=high){
    long long mid=low+(high-low)/2;
    long long needed_B=max(0LL, B*mid-nb);
    long long needed_S=max(0LL, S*mid-ns);
    long long needed_C=max(0LL, C*mid-nc);
    long long cost=needed_B*pb+needed_S*ps+needed_C*pc;
    if(cost<=ruble){
      ans=mid;
      low=mid+1;
    }
    else{
      high=mid-1;
    }
  }
  cout<<ans<<endl;
}
```

Complexity Analysis:
loop from 0 to s.size() => |s| where s<=100, almost negligible
BS on 0 to 1e13 => log(1e13) where it is too small, approx 43
Total complexity => O(|s|+log R) ~ O(log R)
