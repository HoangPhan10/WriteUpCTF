![alt](https://bcm.kcslab.asia/files/7dd496c18a29a6fa58364ff739a3ce08/Thiet_ke_chua_co_ten_3.png)
# **PROG/MISC**
## 1.Split String
### Topic :
    nc 146.190.115.228 10463
    Split it: Thencomestheelectriczappercollar
    Ans: Then comes the electric zapper collar
### Solution :
+ Bài này ban đầu mình làm là tự split bằng tay sau check từ bằng thư viện của python: `enchant`,`nltk` nhưng vẫn không ra đáp án đúng
+ Sau mình tìm được thư viện split chuỗi có nghĩa  **`wordninja`** : để cắt từ từ một chuỗi hỗn tạp 
### Python
```python
import wordninja
splitIt = "Thencomestheelectriczappercollar"
strArr = wordninja.split(splitIt)
# wordninja.split trả về cho chúng ta một mảng các string và ta cần join chúng thành chuỗi
result = " ".join(strArr)
print("result :",result)
# result : Then comes the electric zapper collar
```
+ Đến đây gần như đã hoàn thành 50%,vì bài này cần gửi payload liên tục nên ta cần viết script.Ở đây mình dùng *socket* để kết nối:
```Python
import socket
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
sock.connect(("146.190.115.228",10463))
buffer = ""
buffer+=sock.recv(1024).decode()    
print(buffer)
# Split it: Whyohwhyweweremeanttobe
# Ans:
```
+ Mình cần cắt chuỗi mình cần xử lý,ở đây mình dùng regex để cắt chuỗi :
```Python
import re
regex = (r"Split it: ([A-Za-z'0-9]+)\n"
	r"Ans")
```
+ Bây giờ mình chỉ cần send request thôi:
```Python
import socket
import wordninja
import re

regex = (r"Split it: ([A-Za-z'0-9]+)\n"
	r"Ans")
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
sock.connect(("146.190.115.228",10463))
try :
    while True :
        buffer = ""
        buffer+=sock.recv(1024).decode()
        print(buffer)
        matches = re.search(regex,buffer)
        n = matches.group(1)
        c= wordninja.split(n)
        res = " ".join(c)
        sock.send((res+"\n").encode())
        print(res)
except:
    print(buffer)
```
> Flag: KCSC{Looks like you know how to use that tool, nice hecker}

## 2.Gen Max Number
### Topic:
    nc 146.190.115.228 10464
    Từ số đã cho sắp xếp các chữ số thành một số lớn nhất ví dụ: 4567123098 -> 9876543210
### Solution: 
+ Ý tường là mình sẽ cắt số thành mảng rồi sort theo chiều giảm dần và join lại:
```Python
def maximum(n):
    x = []
    n = int(n)
    while n>0:
        x.append(str(n%10))
        n=n//10
    y= sorted(x)
    y.reverse()
    return "".join(y)
```
+ Bây giờ mình viết script để chạy thôi,tương tự như bài trên
> Flag : KCSC{You will maximize yourself when participating in KCSC, G00d_j0b}
## 3.Smaller Number
### Topic:
    nc 146.190.115.228 10454
    Từ mảng đã cho chẳng hạn Array: [4,5,9,1,1] Chỉ ra số các số nhỏ hơn phần tử hiện tại trong Array 
    Ans: [2, 3, 4, 0, 0]
### Solution: 
+ Ý tường là mình cho 2 vòng for chạy lồng nhau:
```Python
def smallerNumber(arr):
    result = []
    for i in range(len(arr)):
        sum =0
        for j in range(len(arr)):
            if arr[i]>arr[j]:
                sum +=1
        result.append(sum)
    return result
```
+ Bây giờ mình viết script để chạy thôi,tương tự như bài trên
> Flag : KCSC{Phew, i done, you clear, hen ra tet gap mat}
## 4.Xò
### Topic:
[1.jpg](https://bcm.kcslab.asia/files/5b15629bd8aa6e8596a23b25fdecd347/1.jpg?token=eyJ1c2VyX2lkIjo1OCwidGVhbV9pZCI6bnVsbCwiZmlsZV9pZCI6NDF9.Y8ZQ1A.o7GnwPOZqcXHwTxEdezXwAyn__I)

[2.jpg](https://bcm.kcslab.asia/files/0ad891166bb4da976666f3ae3d606f1f/2.jpg?token=eyJ1c2VyX2lkIjo1OCwidGVhbV9pZCI6bnVsbCwiZmlsZV9pZCI6NDJ9.Y8ZQ1A.XPA6vAmR3w0A0CAwe2iXao-71lQ)

    Cứ byte nào khác nhau thì xor là ra flag
### Solution:
+ Đề bài gợi ý cho chúng ta là xor các byte khác nhau giữa 2 ảnh,đầu tiên ta phải đọc byte của 2 bức ảnh:
#### Python
```Python
f1 = open('1.jpg', 'rb')
contentJpg1 = f1.read()

f2 = open('2.jpg', 'rb')
contentJpg2 = f2.read()
```
+ Tiếp đến mình cần tìm byte khác nhau và xor lại với nhau và mình dùng thêm hàm chr để in ra kí tự
```Python
for i in range(max(len(contentJpg1),len(contentJpg2))):
    if contentJpg1[i] != contentJpg2[i]:
        xor = contentJpg1[i] ^ contentJpg2[i]
        result+=chr(xor)
print(result)
```
> Flag : KCSC{Da_bao_roi_cu_x%r_tung_byte_la_ra_ma_li}



