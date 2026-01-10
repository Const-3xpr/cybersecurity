# 🟢 kramazon

**Contents:**

1. [Description](kramazon.md#id-1-description)
2. [Enumeration of website](kramazon.md#enumeration-of-website)
3. [Source code analysis](kramazon.md#source-code-analysis)
4. [XOR-Decoding](kramazon.md#xor-decoding)
5. [Exploitation](kramazon.md#exploitation)
6. [Conclusion](kramazon.md#conclusion)

&#x20;

&#x20;

#### Description:

<figure><img src="../../../../.gitbook/assets/image (91).png" alt=""><figcaption></figcaption></figure>

&#x20;

#### Enumeration of website:

<figure><img src="../../../../.gitbook/assets/image (92).png" alt=""><figcaption></figcaption></figure>

* visit the website
* for now let's only analyze resources or pages which has host name https://kramazon.csd.lol/

<figure><img src="../../../../.gitbook/assets/image (93).png" alt=""><figcaption></figcaption></figure>

* go to Target -> site map -> add to scope

&#x20;

<figure><img src="../../../../.gitbook/assets/image (94).png" alt=""><figcaption></figcaption></figure>

* this way we will only be dealing with kramazon

&#x20;

<figure><img src="../../../../.gitbook/assets/image (95).png" alt=""><figcaption></figcaption></figure>

* after careful inspection i identified Order Now is the only working functionality

&#x20;

<figure><img src="../../../../.gitbook/assets/image (96).png" alt=""><figcaption></figcaption></figure>

* when i clicked i observed that it has created 3 requests(highlighted in yellow)
* in the 1st request above there's interesting callback\_url in response that we can intercept the response and make changes with it

&#x20;

<figure><img src="../../../../.gitbook/assets/image (97).png" alt=""><figcaption></figcaption></figure>

* 2nd request and it's response

&#x20;

<figure><img src="../../../../.gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure>

* 3rd request and response
* here i still don't understand how did response get user id because there was no login and it set-cookie when visiting it's home page so it's cookie used as user id and in request body there is no mention of user id

&#x20;

<figure><img src="../../../../.gitbook/assets/image (99).png" alt=""><figcaption></figcaption></figure>

* cookie is base64 encoded so i decoded it

&#x20;

<figure><img src="../../../../.gitbook/assets/image (100).png" alt=""><figcaption></figcaption></figure>

* so i just changed base64 cookie from BA to BB and it changed user id in response
* i tried manipulating it but can't get user id 1

&#x20;

#### Source code analysis:

<figure><img src="../../../../.gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>

* now let's look at how requests are created
* in home page inside response i don't see **create-order** or **finalize** request codes but have javascript called `script.js`

&#x20;

<figure><img src="../../../../.gitbook/assets/image (102).png" alt=""><figcaption></figcaption></figure>

* there is **create-order** and **finalize** requests in this javascript and there is a interesting function which has XOR but it's an unused code left as a hint so note down that hexadecimal `0x37`&#x20;

&#x20;

#### XOR-Decoding:

<figure><img src="../../../../.gitbook/assets/image (3) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* let's decode our cookie using base64 decoder in burp

&#x20;

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* after base64 decoding i took the first byte which is `0x04`  and did XOR decoding (you can also use windows calculator in programmer mode)
* do it with all the other hex and convert it to ascii to get our user id

&#x20;

<figure><img src="../../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

&#x20;

#### Exploitation:

<figure><img src="../../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

* let's forge the cookie using user id 1
* to forge the cookie convert ascii `1` to hexadecimal which is `31` in hexadecimal

&#x20;

<figure><img src="../../../../.gitbook/assets/image (4) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* now i will XOR encode it using `0x37` which is `0x31` XOR `0x37` = `0x06`&#x20;

&#x20;

<figure><img src="../../../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>

* encode the XOR result using Hex to Base64 encoder

&#x20;

<figure><img src="../../../../.gitbook/assets/image (6) (1) (1).png" alt=""><figcaption></figcaption></figure>

* copy and paste that base64 encoded forged cookie in request and also URL encode like the above screenshot
* we only got half the flag but now we know the location of full flag which is displayed in the response

&#x20;

<figure><img src="../../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

* now modify request to the flag path and we will get the full flag

&#x20;

#### Conclusion:

During source code analysis, unused code revealed XOR-based logic which made it possible to decode the XOR obfuscation of the cookie and used that same XOR obfuscation logic to forge our own cookie leading to IDOR vulnerability.

