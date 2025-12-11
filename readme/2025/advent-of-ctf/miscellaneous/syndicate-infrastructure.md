# 🟢 syndicate infrastructure

<figure><img src="../../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

it already gave hint: Dig

`dig` is a tool that queries DNS records

1.

<figure><img src="../../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

```
dig TXT krampus.csd.lol
```

that gives SPF record

2.

<figure><img src="../../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

```
dig TXT _dmarc.krampus.csd.lol 
```

this gives DMARC record which gave us another domain

3.

<figure><img src="../../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

```
dig TXT ops.krampus.csd.lol
```

4.

<figure><img src="../../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

```
dig SRV _metrics._tcp.krampus.csd.lol
```

i have tried other also so i only post about the successful ones

SRV is used query service records it also gives port number of that service

5.

<figure><img src="../../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

```
dig TXT beacon.krampus.csd.lol
```

```
exfil.krampus.csd.lol
```

base 64 decoding gave us this subdomain

6.

<figure><img src="../../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

```
dig TXT exfil.krampus.csd.lol
```

so dkim(DomainKeys Identified Mail)

{% embed url="https://serverfault.com/questions/625008/find-dkim-and-dmarc-records" %}

7.

<figure><img src="../../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

```
dig TXT syndicate._domainkey.krampus.csd.lol
```

once again Base64 decode and you'll get the flag

nice challenge learned more about `dig`
