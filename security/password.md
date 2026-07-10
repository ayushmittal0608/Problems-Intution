In order to crack password, let's seek what worst can be done to crack some password, like at what level can someone crack our password, so that we could develop a highly secured application.

1. Phishing
Fake login pages, fake emails or SMS, even OAuth consent scams. We migh seek OAuth as an easy access service which we offer users to authenticate but still, a phishing activity might occur which doesn't make application secure. Obviously, best practice is to go to official sites for any activity and only revert to the official emails which are the responsibility of users of how aware they are, and mostly people are aware of it, but still OAuth is not what I think we should practice because we are using third party to authenticate our application.

2. Credentials Stuffing
In today's world, credentials stuffing is the most vulnerable security breach that usually happens with many users and we need something in our web for any extension managing or saving our passwords in the browser but still how can we say that the credentials saved in browser are the most secure, maybe they are the most secure, if that is the case and we think google chrome web browser for managing our credentials, and so we could rely on gmail too, because if we are giving someone access to something, then nothing is secure but still everything runs on internet, we need to have some dependency over the tech giants at initial stage.

Now, if gmail is the most secure, then we can send the credentials which are auto generated over a gmail which we can save inside a browser for easy access but the problem of credentials stuffing would be largerly solved. Nowadays, people use OAuth but still I don't prefer the usage of OAuth.

3. Brute Force
People usually implement a brute force attack on the website login page and we need to prevent it, so for preventing it, we limit the number of requests for each password login and then after that account gets locked for sometimes, hence we implement rate limiter, account lockout and CAPTCHA after repeated failures. Also, we can implement flag limit to detect suspicion.

4. Dictionary Attack
A dictionary of most common passwords has been prepared which according to the ease of comfort of user's psychology, they use those password. Now, they have a feeling in their mind that they would show them hard, tough and sophisticated and so no one would even try cracking their password, but it might happen. So, these can be prevented by setting some password rules which can't predict the password too easily.

4. Offline Hash Cracking
If for eg, an attacker steals our database of password hashes, they can attack it offline. They compare billions of hashes and check for the matches per second. In the past years, when we were having a normal computing using CPU, password can't be guessed too easily, so we used to implement BCrypt.js to encrypt our password, where first three letters show the version, next two shows the number of computational rounds password is being hashed, which is cost factor and then salt+hash in rest 128 bits hashed. Bcrypt uses a 4KB lookup table. Let's say we have 24GB of VRAM with our GPU, now if lookup table is just 4KB, then total memory capacity will accommodate around 6 million hashes, now we have more number of memory capacity to perform large number of guesses. What if we increase the size of lookup table to around 256MB, then total memory capacity will accommodate around 96 hashes, now less number of memory capacity will be there to perform guess, so we can't predict the password so easily.

Hence, earlier the concept of bcrypt.js was being used, but currently, due to introduction of GPUs, it becomes highly difficult to have ultra rich security using bcrypt.js, where we are hashing it to some rounds and store inside DB. Even nowadays, some FPGAs and ASICs are specifically designed to compute bcrypt.js hashes to guess password with millions of cores based capabilities to implement parellelism to guess and crack password with an ease.

Hence, we need some other parameter for encryption which is scrypt and argon2id. In the initial phases, scrypt was doing great job like generation of initial block, then memory allocation, then adding blocks to it and then doing a random shuffling but it would become a puzzle game and could inherit a side channelling attack, for eg, an attacker closely watches the activity of placement of each block before shuffling to random blocks, so it would be easy for attacker to guess password after solving that puzzle because he knows that new block is dependent over prev block.

Hence, argon2id is being used where we use a compression function to combine a random block to the prev block for generating new block, so that attacker could not be able to perform side channel attacks because now he doesn't know the actual order. Alongwith that, there is a huge memory allocated for each block which makes GPU compute heavy and attacker would fail to make such costly guesses per second.

5. Keyloggers
For eg, I am having a cracked version of GTA-6 available with me to play, so I should download it, so we need to avoid installing untrusted software, of course, we have that nostalgia of playing those gta games again, but let's buy it original from rockstar rather than playing it cracked, obviously we have Azure VM or Amazon EC2 if our laptop isn't enough for playing such games, but even that is expensive too. I think there is a business potential for Amazon in this part too, they just have to closely look upon it, arising the nostalgia of middle class people at lower rates. Also, keeping antivirus and maintaining system updates is essential too.

One of the most exciting thing that I find is usage of mTLS where we generate a root certificate authority private key and a certificate, then generate a server private key and a certificate signing request file to sign server certificate using CA and do the same for client/device signing. After that, we generate a .p12 file which we import inside our certificate manager(.certmgr), now for accessing any sensitive part of a software/system, we need to load that certificate from device to the browser. The browser shows the popup, we click on certificate and then click OK, then we can authenticate and generate a jwt token signed with those credentials for short time.

6. Memory Theft
We need to store our keys and credentials inside AWS KMS and security manager, also we can store them inside Azure vault or hardware security modules (HSMs). Keys are the most essential part of the security associated with system. Security groups needs to be configured properly, sometimes we give our secure terminal port access over the internet, so we need to define inbound and outbound rules properly and whitelist IPs effectively. There needs to be short lived session tokens as well.

7. Cookie Theft
We need to use HTTP-only, secure and same site cookie for CSRF protection, revoke sessions on logout or password change. However, google has just implemented password change without session expire which could be an advantageous service for customers but at the same time, a vulnerability issue too.

8. Social Engineering
IAM implementation is the must, access and rights based on identity, roles and permissions, restrictions of different users at different layers of security. If we give * rights to all the users, then all the software shops will be shut down because we need to specify what a user can do based on his responsibility in an organisation. If event triggers tracking each action, with IP and geolocation fetching with mapped user info is being used, the system becomes more secure as now we are having each and every parameter to predict human activity on our system but what about the cost of huge database involved in storing the stuff.

I think security plays an important role in gaining user trust, obviously we can minimise the cost and we should not forget minimising it but if something is making our system more reliable and trustworthy for users to use, then we can turn that cost liability into an asset.

There is another layer to it where we create a margin of what our internal organisation usage costs, till which time we need to store data, how much cost we need to store on each user in comparison to net revenue because obviously either at the earliest, we do a mistake with cost optimisation or security management and both of them are the important aspect.

9. SIM Swapping
We can implement MFA for preventing SIM swapping where it takes into consideration three parameters:
- Something you know (PIN, password)
- Something you have (Mobile OTP, Authenticator)
- Something you are (Biometric, Facial Recognition, Iris scan)
To prevent SIM swapping, again we need to use authenticator app instead of mobile OTP but we can also store the IP and geolocation fetched through navigators for original latitude and longitude, alongwith device info and browser info with which account was being created and predicting suspicion based upon it.