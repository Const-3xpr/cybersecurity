# 🟢 all paths lead home chall

<figure><img src="../../../../.gitbook/assets/image (91).png" alt=""><figcaption></figcaption></figure>

let's visit the website

<figure><img src="../../../../.gitbook/assets/image (92).png" alt=""><figcaption></figcaption></figure>

it's a very simple page so let's test the functionality of the web page by clicking 'Open' button to see what will happen

<figure><img src="../../../../.gitbook/assets/image (93).png" alt=""><figcaption></figcaption></figure>

looks like LFI at first glance so let's test that first

<figure><img src="../../../../.gitbook/assets/image (94).png" alt=""><figcaption></figcaption></figure>

a simple payload got blocked

in challenge they mentioned '/secret/' that we are not supposed to see

<figure><img src="../../../../.gitbook/assets/image (95).png" alt=""><figcaption></figcaption></figure>

now we got 2 hints 1st it has legacy compatibility and 2nd the file location

<figure><img src="../../../../.gitbook/assets/image (96).png" alt=""><figcaption></figcaption></figure>

when we visited file loaction at `/docs/legacy.html` we got 2 more hints 1st `&legacy=1`  maybe a parameter and it accepts UTF-7 encoding for legacy decoding

let's research about UTF-7

<figure><img src="../../../../.gitbook/assets/image (97).png" alt=""><figcaption></figcaption></figure>

**To represent non-ASCII Unicode characters, the encoder "shifts" into a special mode. This mode begins with a plus sign (`+`).** The following characters are then encoded in a modified Base64 format, representing UTF-16 code units. **This block of modified Base64 ends when a character not in the Base64 set is encountered. A hyphen (`-`)** is often used as a specific delimiter to mark the end of the shifted sequence.

source: chatGPT

The start of these blocks of modified Base64-encoded UTF-16 is indicated by a `+` sign. The end is indicated by any character not in the modified Base64 set. If the character after the modified Base64 is a `-` (ASCII [hyphen-minus](https://en.wikipedia.org/wiki/Hyphen-minus)) then it is consumed by the decoder and decoding resumes with the next character. Otherwise decoding resumes with the character after the Base64.

source: [wikipedia](https://en.wikipedia.org/wiki/UTF-7)

<figure><img src="../../../../.gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure>

this site provided this info:

{% embed url="https://www.fileformat.info/info/unicode/char/002f/index.htm" %}

<figure><img src="../../../../.gitbook/assets/image (99).png" alt=""><figcaption></figcaption></figure>

then use hex to base64 converter

{% embed url="https://goteleport.com/resources/tools/hex-to-base64/" %}

```
+AC8-
```

special mode or shift mode and for `.`

```
+AC4-
```

so:

```
+AC4-+AC4-+AC8-secret+AC8-flag.txt
```

many ctf put their flag in flag.txt and don't forget URL encode the payload and put `legacy=1` parameter otherwise it won't work

<figure><img src="../../../../.gitbook/assets/image (100).png" alt=""><figcaption></figcaption></figure>



