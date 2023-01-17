# **PROG/MISC**
## 1.Split String
### Topic :
    nc 146.190.115.228 10463
    Split it: Thencomestheelectriczappercollar
    Ans: Then comes the electric zapper collar
### Solution :
+ Bài này ban đầu mình làm là tự split bằng tay sau check từ bằng thư viện của python: `enchant`,`nltk` nhưng vẫn không ra đáp án đúng
+ Sau mình tìm được thư viện split chuỗi có nghĩa là **`wordninja`**
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