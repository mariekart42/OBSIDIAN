
- problem 1:
	- path to upload is "www/upload"
		- -> upload doesnt exist
	- rigth filename gets appended: "www/upload/test.jpeg"
-> fixed

- problem 2:
	- _buffer does not contain binary data cause of "\/0" signs somewhere
		- : "POST /upload HTTP/1.1\r\nHost: 127.0.0.1:8081\r\nUser-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:109.0) Gecko/20100101 Firefox/117.0\r\nAccept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8\r\nAccept-Language: en-US,en;q=0.5\r\nAccept-Encoding: gzip, deflate, br\r\nContent-Type: multipart/form-data; boundary=---------------------------170426046437965750923415833481\r\nContent-Length: 632314\r\nOrigin: http://127.0.0.1:8081\r\nDNT: 1\r\nConnection: keep-alive\r\nReferer: http://127.0.0.1:8081/upload.html\r\nUpgrade-Insecure-Requests: 1\r\nSec-Fetch-Dest: document\r\nSec-Fetch-Mode: navigate\r\nSec-Fetch-Site: same-origin\r\nSec-Fetch-User: ?1\r\n\r\n-----------------------------170426046437965750923415833481\r\nContent-Disposition: form-data; name=\"fileToUpload\"; filename=\"test.jpeg\"\r\nContent-Type: image/jpeg\r\n\r\n\xff\xd8\xff\xdb"
	- ->> use _buffer.assign(tmpBuff, bytesRead);!!
- -> fixed

- problem 3:
	- upload does not work
		- keep track:
			- FIRST ITER:
				- test.jpg
				- readStart: 837

- problem 4:
	- if in post copy_file already exist, new file will also be called copy_file
		- ->> gets overwritten!