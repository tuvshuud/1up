### Misc 70 - Rock with the wired shark
`Sniffing traffic is fun. I saw a wired shark. Isn't that strange?`

#EN
In this task we got dump.pcapng file to work on. We opened it in Wireshark and saw some tcp and http packets.
Also HTTP GET /flag.zip request. If you follow tcp stream,

```
GET /flag.zip HTTP/1.1
Host: 192.168.1.41:8080
Connection: keep-alive
Authorization: Basic ZmxhZzphenVsY3JlbWE=
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/46.0.2490.80 Safari/537.36
DNT: 1
Referer: http://192.168.1.41:8080/
Accept-Encoding: gzip, deflate, sdch
Accept-Language: en-US,en;q=0.8,ht;q=0.6

HTTP/1.0 200 OK
Server: servefile/0.4.4 Python/2.7.10
Date: Fri, 13 Nov 2015 18:41:09 GMT
Content-Length: 222
Connection: close
Last-Modified: Fri, 13 Nov 2015 18:41:09 GMT
Content-Type: application/octet-stream
Content-Disposition: attachment; filename="flag.zip"
Content-Transfer-Encoding: binary

PK..
.....x.mG....(...........flag.txtUT	...-FV.-FVux..............;......q.........9.....H.!...	>B.....+:PK......(.......PK....
.....x.mG....(.........................flag.txtUT....-FVux.............PK..........N...z.....
```

It's probably a zip file. So we need to get that. `File->Export->Http`. Yet it's password protected. 
After few seconds looking for password, basic authentication header is present in the request. It's base64. 
So `base64 -D <<< "ZmxhZzphenVsY3JlbWE="` to get password, unzip an archive containing flag.txt to get flag.
```
IW{HTTP_BASIC_AUTH_IS_EASY}
```

#MN
Энэ даалгаварт flag нууцсан dump.pcapng файл өгөгдсөн ба үүнийг Wireshark -аар нээж үзвэл tcp болон http пакетууд мөн HTTP GET /flag.zip
хүсэлт байв. Tcp follow stream гэж харваас 

```
GET /flag.zip HTTP/1.1
Host: 192.168.1.41:8080
Connection: keep-alive
Authorization: Basic ZmxhZzphenVsY3JlbWE=
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/46.0.2490.80 Safari/537.36
DNT: 1
Referer: http://192.168.1.41:8080/
Accept-Encoding: gzip, deflate, sdch
Accept-Language: en-US,en;q=0.8,ht;q=0.6

HTTP/1.0 200 OK
Server: servefile/0.4.4 Python/2.7.10
Date: Fri, 13 Nov 2015 18:41:09 GMT
Content-Length: 222
Connection: close
Last-Modified: Fri, 13 Nov 2015 18:41:09 GMT
Content-Type: application/octet-stream
Content-Disposition: attachment; filename="flag.zip"
Content-Transfer-Encoding: binary

PK..
.....x.mG....(...........flag.txtUT	...-FV.-FVux..............;......q.........9.....H.!...	>B.....+:PK......(.......PK....
.....x.mG....(.........................flag.txtUT....-FVux.............PK..........N...z.....
```

`File->Export->Http` гээд zip файлтай болтол задлахад нууц үг асууж байв. Хэдэн секунд нууц үг хайж байтал
HTTP хүсэлтийн толгойд Basic Authentication header байгаа нэр нууц үгийн хоршил магадгүй нууц үг байх.
Base64 decode хийгээд `base64 -D <<< "ZmxhZzphenVsY3JlbWE="`, flag.txt байгаа архивийг задлаад флаг авав.
```
IW{HTTP_BASIC_AUTH_IS_EASY}
```
