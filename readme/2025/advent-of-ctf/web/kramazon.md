# 🟢 kramazon

<figure><img src="../../../../.gitbook/assets/image (91).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (92).png" alt=""><figcaption></figcaption></figure>

1. visit the website
2. for now let's only analyze resources or pages which has host name https://kramazon.csd.lol/
3. go to Target -> site map -> add to scope

<figure><img src="../../../../.gitbook/assets/image (93).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (94).png" alt=""><figcaption></figcaption></figure>

now we will only be dealing with kramazon

<mark style="color:red;background-color:red;">**look closely Title column says IDOR**</mark>

<figure><img src="../../../../.gitbook/assets/image (95).png" alt=""><figcaption></figcaption></figure>

only working functionality is Order Now

<figure><img src="../../../../.gitbook/assets/image (96).png" alt=""><figcaption></figcaption></figure>

which created 3 requests(1st request and response is shown above)

interesting callback\_url we can intercept the response and make changes with it

<figure><img src="../../../../.gitbook/assets/image (97).png" alt=""><figcaption></figcaption></figure>

2nd request and it's response

<figure><img src="../../../../.gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure>

3rd request and response

here i still don't understand how did response get user id because there was no login and only set cookie when visiting it's home page so may be it's cookie used as user id and in request json body there is no mention of user id

<figure><img src="../../../../.gitbook/assets/image (99).png" alt=""><figcaption></figcaption></figure>

cookie is base64 encoded

<figure><img src="../../../../.gitbook/assets/image (100).png" alt=""><figcaption></figcaption></figure>

i just changed base64 cookie from BA to BB and it changed user id in response

i tried manipulating it but can't get user id 1

so let's look at how requests are created

<figure><img src="../../../../.gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>

in home page i don't see create-order or finalize but have script.js

<figure><img src="../../../../.gitbook/assets/image (102).png" alt=""><figcaption></figcaption></figure>

there is create-order and finalize requests in this javascript and there is a interesting function which has bit-wise xor but it's an unused code left as a hint

<figure><img src="../../../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

base64 decode

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

reverse the xor logic

do with all the other hex and convert it to ascii to get our user id

<figure><img src="../../../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

let's use this logic to forge cookie of user\_id 1

<figure><img src="../../../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

only got half the flag but now we know the location of full flag

<figure><img src="../../../../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

got the full flag
