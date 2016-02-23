### Misc 80 - Flag not found
`I tried to download the flag, but somehow received only 404 errors :(`

#EN
We have flag.pcapng file containing dns request and response packets along with HTTP get request to /flag.zip.
If we analyze .pcapng file, following points are found.
- DNS queries for A record
- DNS queries for AAAA record (IPv6)
- Each DNS query for different hostname but same host

First, we thought it's kind of challenge points to IPv6 which was not. We tried to send http GET /flag.zip 
request for each hostname. Didn't get lucky. After sometime, different hostnames look interesting
```
496e2074686520656e642c206974277320616c6c2061626f757420666c61.2015.ctf.internetwache.org
67732e0a5768657468657220796f752077696e206f72206c6f736520646f.2015.ctf.internetwache.org
65736e2774206d61747465722e0a7b4f66632c2077696e6e696e67206973.2015.ctf.internetwache.org
20636f6f6c65720a44696420796f752066696e64206f7468657220666c61.2015.ctf.internetwache.org
67733f0a4e6f626f62792066696e6473206f7468657220666c616773210a.2015.ctf.internetwache.org
53757065726d616e206973206d79206865726f2e0a5f4845524f2121215f.2015.ctf.internetwache.org
0a48656c70206d65206d7920667269656e642c2049276d206c6f73742069.2015.ctf.internetwache.org
6e206d79206f776e206d696e642e0a416c776179732c20616c776179732c.2015.ctf.internetwache.org
20666f72206576657220616c6f6e652e0a437279696e6720756e74696c20.2015.ctf.internetwache.org
49276d206479696e672e0a4b696e6773206e65766572206469652e0a536f.2015.ctf.internetwache.org
20646f20492e0a7d210a.2015.ctf.internetwache.org
```
`x.2015.ctf.internetwache.org` that x subdomain is actually hex string. if we decode it `echo hostnames | xxd -r -p`
```
In the end, it's all about fla gs.
Whether you win or lose do esn't matter.
{Ofc, winning is  cooler
Did you find other fla gs?
Noboby finds other flags!
 Superman is my hero.
_HERO!!!_ 
Help me my friend, I'm lost i n my own mind.
Always, always,  for ever alone.
Crying until  I'm dying.
Kings never die.
So  do I.
}!
```
Again, where is the flag?. If you look steady, first letters of every line constructs flag. Misc challenge is misc LOL.
```
IW{DNS_HACKS}
```

#MN
Даалгаврын өгөгдөл нь flag.pcapng, dns query хүсэлт болон хариу өгсөн packet ууд болон /flag.zip рүү хандсан HTTP хүсэлтүүдтэй
.pcapng файл байв. Нээж үзвээс, дараах зүйлүүд тодорхой байлаа.
- A record ийн DNS хүсэлт 
- AAAA record ийн DNS хүсэлт (IPv6)
- DNS хүсэлт болгон өөр өөр домэйн нэр асуусан ба хариулт нэг хост руу байсан.

Эхлээд IPv6 тай холбоотой гэж үзээд http://[ipv6address]/flag.zip гээд хүсэлт явуулаад амжилт олсонгүй. Хэсэг хугацааны дараа domain
нэрсийг жагсаагаад нэг нэгээр мөн хүсэлт явуулж үзлээ, бас үгүй.
```
496e2074686520656e642c206974277320616c6c2061626f757420666c61.2015.ctf.internetwache.org
67732e0a5768657468657220796f752077696e206f72206c6f736520646f.2015.ctf.internetwache.org
65736e2774206d61747465722e0a7b4f66632c2077696e6e696e67206973.2015.ctf.internetwache.org
20636f6f6c65720a44696420796f752066696e64206f7468657220666c61.2015.ctf.internetwache.org
67733f0a4e6f626f62792066696e6473206f7468657220666c616773210a.2015.ctf.internetwache.org
53757065726d616e206973206d79206865726f2e0a5f4845524f2121215f.2015.ctf.internetwache.org
0a48656c70206d65206d7920667269656e642c2049276d206c6f73742069.2015.ctf.internetwache.org
6e206d79206f776e206d696e642e0a416c776179732c20616c776179732c.2015.ctf.internetwache.org
20666f72206576657220616c6f6e652e0a437279696e6720756e74696c20.2015.ctf.internetwache.org
49276d206479696e672e0a4b696e6773206e65766572206469652e0a536f.2015.ctf.internetwache.org
20646f20492e0a7d210a.2015.ctf.internetwache.org
```
Харин `x.2015.ctf.internetwache.org`x гэх subdomain ийг харвал hex string байв. Эдгээрийг decode `echo hostnames | xxd -r -p` хийвэл
```
In the end, it's all about fla gs.
Whether you win or lose do esn't matter.
{Ofc, winning is  cooler
Did you find other fla gs?
Noboby finds other flags!
 Superman is my hero.
_HERO!!!_ 
Help me my friend, I'm lost i n my own mind.
Always, always,  for ever alone.
Crying until  I'm dying.
Kings never die.
So  do I.
}!
```
Гэхдээ флаг хаана байна?. Тогтож харвал, Мөр болгоны эхний үсэг нийлээд флаг байлаа.
```
IW{DNS_HACKS}
```
