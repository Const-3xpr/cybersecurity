# 🟢 what's mine is yours

first unintended way

<figure><img src="../../../../.gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (102).png" alt=""><figcaption></figcaption></figure>

very simple looking website which has only sign in button so we will do the usual test functionality and see where it goes

<figure><img src="../../../../.gitbook/assets/image (103).png" alt=""><figcaption></figcaption></figure>

one click made 3 request we will analyze all the 3 one by one

<figure><img src="../../../../.gitbook/assets/image (104).png" alt=""><figcaption></figcaption></figure>

it set's cookie

<figure><img src="../../../../.gitbook/assets/image (105).png" alt=""><figcaption></figcaption></figure>

it sets cookie in next request

<figure><img src="../../../../.gitbook/assets/image (106).png" alt=""><figcaption></figcaption></figure>

got api token and as the chall says we will go to `/api/flag` and put this api token in `X-Flag-Token`

<figure><img src="../../../../.gitbook/assets/image (107).png" alt=""><figcaption></figcaption></figure>

it says not found&#x20;

next i decided to change request methods because in response headers of  `/login` request it says access control allow methods GET, POST, OPTIONS and i without any thought behind it tried it

<figure><img src="../../../../.gitbook/assets/image (108).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (109).png" alt=""><figcaption></figcaption></figure>

very interesting error just because i changed method of request

so i added cookie from our session as it say 'not authenticated'

<figure><img src="../../../../.gitbook/assets/image (110).png" alt=""><figcaption></figcaption></figure>

i don't know how but it worked

my real intention was changing method to see if there's any different outcome and yes it did but i didn't expect i was on my way to flag but when i put my own cookie because it said 'not authenticated' and gave 401 unauthorized error flag shouldn't have revealed, i tried this challenge 2 times(my first try and 2nd try while posting this challenge) with different cookies and token result was same.
