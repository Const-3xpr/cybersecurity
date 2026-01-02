# 🟢 Mason initiate

<figure><img src="../../../../.gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (12) (1).png" alt=""><figcaption></figcaption></figure>

let's fetch

<figure><img src="../../../../.gitbook/assets/image (13) (1).png" alt=""><figcaption></figcaption></figure>

by default in burp mime type images filter are off so turn it on to see the request

<figure><img src="../../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

well it already said at start that it's SSRF let's get straight to that and we got error which indicate SSL error, we will try http next

<figure><img src="../../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

maybe try with /flag.txt

i won't be posting screenshot but it was same 404 error

i will search online 'aws directory structure for ctf'

[https://rzepsky.medium.com/aws-and-hackerone-ctf-write-up-4c37131f7cbb](https://rzepsky.medium.com/aws-and-hackerone-ctf-write-up-4c37131f7cbb)

very good article

we will try his payload first to get proper path

<figure><img src="../../../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

got the perfect hit thanks to Pawel Rzepa writeup

```
/latest/meta-data/iam/security-credentials/poctf-role
```

```
http://127.0.0.1:8081/latest/meta-data/iam/security-credentials/poctf-role
```
