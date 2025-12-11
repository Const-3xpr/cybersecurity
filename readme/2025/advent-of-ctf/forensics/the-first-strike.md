# 🟢 The first strike

<figure><img src="../../../../.gitbook/assets/image (85).png" alt=""><figcaption></figcaption></figure>

it's a pcap file which means wireshark would be good tool to examine logs

<figure><img src="../../../../.gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>

it's a failed login attempt and there's 36095 packets in this log let's try to filter what we want

<figure><img src="../../../../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>

```
ftp.request.command == "PASS"
```

it will filter and display only request command PASS short form for password

in the first pic of wireshark it showed 530 status code in Response for failed login attempt in FTP

so for successful login attempt is 230 in response code in FTP login

<figure><img src="../../../../.gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>

got the successful login now we need to follow the stream in order to get username and password

<figure><img src="../../../../.gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (90).png" alt=""><figcaption></figcaption></figure>

done.
