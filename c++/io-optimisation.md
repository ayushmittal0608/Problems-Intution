How would we optimise the code using iostream knowledge?

Now, there are two things that we use for the newline which is endl and \n, now \n inserts just a newline character while endl inserts newline and flushes the output buffer which forces all the buffered output to be written immediately to the device/OS which is slow because what we need is to store buffered output to cout buffer or RAM memory which is displayed as an output and then OS writes it to terminal/file in chunks which is obviously faster while the usage of endl was resulting in extra overheads. So the best practice is to use \n instead of endl, and to keep it optimised, we at the start of program disables the tie to prevent cin to flush cout before every input, hence we use cin.tie(nullptr).

Now, second optimisation is sync_with_stdio(false), let's assume our C++ compiler is running both types of codes, C++ one and C one, like both IO, imagine how much overhead it would create overall, hence we make its sync with stdio used inside C to be false.

```
ios::sync_with_stdio(false);
cin.tie(nullptr);
int a;
cin>>a;
cout<<a<<'\n';
```
