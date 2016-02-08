###Forensic 100 - uagent
`We think we are really cool, are we?`

#EN
Challenge gives us a .pcap file. We open it in wireshark, if you analyze first packet, you will see a content of http stream.
![](https://raw.githubusercontent.com/tuvshuud/1up/master/SharifCTF2016/uagent100/shot1.png)
![](https://raw.githubusercontent.com/tuvshuud/1up/master/SharifCTF2016/uagent100/shot2.png)

Interesting things are it's partial contents and user-agents with base64 string.

We have used [Dshell](https://github.com/USArmyResearchLab/Dshell) to merge partial contents. [CTF writeup](https://github.com/naijim/blog/blob/master/writeups/asis-quals-ctf-2015_broken_heart_writeup.md) that uses Dshell.

After reassemble http partial contents, we got password protected zip file containing flag.png.

Ok. That user-agents with base64 string were actually png image that shows archive password.
Once we parse base64 from user-agent and decodes into file, we get image.

```python
import dpkt, base64, re
dest = open('useragent', 'wb')
f = open('ragent.pcap', 'rb')
pcap = dpkt.pcap.Reader(f)
for ts, buf in pcap:
	eth = dpkt.ethernet.Ethernet(buf)
	ip = eth.data
	tcp = ip.data
	if tcp.dport == 80 and len(tcp.data) > 0:
		http = dpkt.http.Request(tcp.data)
		m = re.match(r'sctf-app/(.*)/', http.headers['user-agent'])
		dest.write(base64.b64decode(m.group(1)))
		print http.headers['range']
		if http.headers['range'] == "bytes=4589-4606":
			break
dest.close()
```

`Flag: SharifCTF{94f7df30fbd061cc4f7294369a8bce1c}`

#MN
Энэ даалгавар нь өгөгдсөн .pcap файлыг анализ хийж флаг олох байв. Wireshark дээр нээгээд эхний пакет дээр follow tcp stream гээд үзвэл ямар нэг файл нэг хостоос нөгөө хост руу хуулж авсан талаарх мэдээлэл байв. 

![](https://raw.githubusercontent.com/tuvshuud/1up/master/SharifCTF2016/uagent100/shot1.png)
![](https://raw.githubusercontent.com/tuvshuud/1up/master/SharifCTF2016/uagent100/shot2.png)

Byte range аар нь хуваачихсан файлын хэсгүүд болон HTTP GET хүсэлтийн user-agent нь base64 string байгаа нь дээрх зураг дээр харагдаж байна.

Эхлээд Wireshark дээр File->Export->HTTP гэж салингид котентуудыг авч байгаад python script ээр нэгтгэсэн чинь zip file байсан ба задлах гэтэл corrupted zip гээд нээгдсэнгүй. Миний бичсэн скрипт алдаатай байсан бололтой. Тэгээд partial content уудыг автоматаар reassemble хийх tool юу байна гээд хайж байгаад [Dshell](https://github.com/USArmyResearchLab/Dshell) ийг оллоо. [Энэ](https://github.com/naijim/blog/blob/master/writeups/asis-quals-ctf-2015_broken_heart_writeup.md) даалгаварт хэрхэн ашиглаж байгаа бичсэн байна лээ.

Тэгээд Dshell ээр нэгтгээд гаргаж авсан файлаа задлах гэж үзтэл password protected байв.

Эхэнд ажиглагдсан нэг сонирхолтой зүйл base64 string тэй user-agent ууд. Тэдгээрийг decode хийгээд файлруу бичвэл архив файлын нууц үг бичсэн png зураг гарч ирэв.
```python
import dpkt, base64, re
dest = open('useragent', 'wb')
f = open('ragent.pcap', 'rb')
pcap = dpkt.pcap.Reader(f)
for ts, buf in pcap:
	eth = dpkt.ethernet.Ethernet(buf)
	ip = eth.data
	tcp = ip.data
	if tcp.dport == 80 and len(tcp.data) > 0:
		http = dpkt.http.Request(tcp.data)
		m = re.match(r'sctf-app/(.*)/', http.headers['user-agent'])
		dest.write(base64.b64decode(m.group(1)))
		print http.headers['range']
		if http.headers['range'] == "bytes=4589-4606":
			break
dest.close()
```

Нууц үгээр архив файлаа задлаад flag.png нээвэл
`Flag: SharifCTF{94f7df30fbd061cc4f7294369a8bce1c}`

