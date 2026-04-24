# 🟢 flag market



<figure><img src="../../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

1. Register and login

<figure><img src="../../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

2. so the challenge is we have to collect 10 Flag Artifact which cost 1000 but our credit is also 1000

<figure><img src="../../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

3. we can buy and we can get refund also
4. after testing this 2 functionality for race condition vulnerability i found out buying take 900-1000 milliseconds while refund is instant around 150 milliseconds
5. let's test race condition on buy by using parallelism
6. i will buy 1000 CR flag\_artifact to test

<figure><img src="../../../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

7. put it in repeater and create group by right-clicking

<figure><img src="../../../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

8. right-click the grouped "buy" tab -> Duplicate tab -> then select the amount of tabs you want to duplicate

<figure><img src="../../../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

9. use drop-down and select parallel(single-packet attack)

<figure><img src="../../../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

10. we got flag artifact worth 17000 CR, let's see if refund will give us 17000CR

<figure><img src="../../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

11. now we have 17000 CR which confirms Race-Condition vulnerability

<figure><img src="../../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

12. We got the flag
