---
layout: post
title: Tính năng mới siêu xịn của Python 3.9 Merging dictionaries
summary: Các ngôn ngữ lập trình liên tục phát triển và giới thiệu những tính năng mới cho phép lập trình viên được "lazy code" - viết ít code, chạy được nhiều. Python là một ngôn ngữ trẻ so với các bậc đàn anh lão làng trong ngành lập trình, nhưng đã nhận được sự chú ý đặc biệt từ cộng đồng. Mới đây, Python đã tung ra phiên bản mới nhất Python 3.9 với nhiều thay đổi hấp dẫn. Trong số đó thì Merging dictionary có thể coi là tính năng quan trọng nhất được giới thiệu trong bản cập nhật này.
date: 2020-04-30 16:43
categories: Programming Python
---

Các ngôn ngữ lập trình liên tục phát triển và giới thiệu những tính năng mới cho phép lập trình viên được "lazy code" - viết ít code, chạy được nhiều. Python là một ngôn ngữ trẻ so với các bậc đàn anh lão làng trong ngành lập trình, nhưng đã nhận được sự chú ý đặc biệt từ cộng đồng. Mới đây, Python đã tung ra phiên bản mới nhất Python 3.9 với nhiều thay đổi hấp dẫn. Trong số đó thì Merging dictionary có thể coi là tính năng quan trọng nhất được giới thiệu trong bản cập nhật này.

![Tính năng mới trong Python 3.9](https://lh3.googleusercontent.com/GfKVXaslf5LbFPDM8BLPDG6CrNRCpSVaFjrnKY__RtAtB2yQhmONYzOaG96jIRB_OwBwYlz3EeV8X3nnAyu8OI-LQkOFoP2h_618qeEOpOPghNTbD4AyHGZOHFL5OJ2CaIxjdqk_tbF5y2C-Y_kYnA7pBWqmSvgaiTxZXco09_HRR3ma7hVzZg13Bb9zi5fTF7Lw0vU4pwDUC5QBABi6CmL9P4FnSd1o4_P0c4Fd5vHhCSBxWOP_XCY_gIOLNK-2aqm5Y5rbFe80prqXoq6tiLzePMk7pYzg-poC1-_SPwJHjF6SDsX955-n8C24EOUfwTgU9FKopybKBVwQdiOMnQ5lNus2z6xihiHKfS2O93xXtSPYwC2TCd46LHRsGregq5RJXxXOLuEca8ETFdsbtA7vf33Yjat_xGVjygc7QlCOP8rJ1_YDUupv88rVMCCo_UZu5iAfbSOTP6OEc07h6gUDk5pX1aoP1i458ec9s5zPSTxhZqBhxkHHNRrerCSnchDsyllp8FVo3rBUwIoz5bMmKP4CDIdpihkLSWnb9yHiy3eX-qaBt3e2k8Wpe9LN0v8OPteWlR0OrjI4w-M8cD2fus_nWUbT627vmKAraFR8JoJJ03zkPozEn0YEvvfnPKMGtMPFC8wq18D971HLHAXm_j6pfDc--Q1JawmXd1vaOSRyG9sfWouNFrpjNA=w700-h298-no)

### Python 3.9
Python 3.9 hiện đã ở trong giai đoạn alpha và chuẩn bị ngấp nghé bước sang giai đoạn beta vào tháng 5 năm 2020, theo dự định thì bản chính thức sẽ được ra mắt vào tháng 10 cùng năm. Mọi người có thể xem lịch trình ra mắt của phiên bản này ở [đây](https://www.python.org/dev/peps/pep-0596/)

### Giới thiệu về Dict aka Từ điển trong Python
Dict hay từ điển không phải là một khái niệm riêng của Python mà là cấu trúc dữ liệu quen thuộc (dictionary). Một dictionary là một bộ gồm các cặp key - value, và có thể truy xuất dữ liệu thông qua giá trị của key thay vì index như mảng. Chúng ta lấy ví dụ bằng code Python:

```python
d = {'Hello': 'Xin chao', 'Thanks': 'Cam on'}
```

Ta được một dictionary trong Python gồm hai keys là ```'Hello'``` và  ```'Thanks'``` nhận values tương ứng là ```'Xin Chao'``` và ```'Cam on'``` 
Để truy xuất thông tin của dict chúng ta sẽ sử dụng key giống như index của mảng.
```python
print(d['Hello'])
print(d['Thanks'])
```

Giả sử trong quá trình ứng dụng chạy, chúng ta có thể thu thập được thêm thông tin
```python
d1 = {'Good': 'Tot', 'Bad': 'Xau'}
```
Và đến cuối ngày, bạn muốn kết hợp hai dict này lại với nhau thành một dict hoàn chỉnh. Vậy bây giờ ta phải làm như thế nào?

### Cách 1: For-loop
Cách đầu tiên và đơn giản nhất mà ai cũng có thể nghĩ tới là dùng một vòng lặp for và thêm lần lượt từng giá trị của dictionary ```d``` và ```d1```
Code Python:
```python
# Ngan gon hon co the dung dnew = {}
dnew = dict()
for key, value in d.items():
    dnew[key] = value
for key, value in d1.items():
    dnew[key] = value

# Kiem tra ket qua
print(dnew)
```
Và kết quả ta nhận được sẽ là
```
{'Hello': 'Xin chao', 'Thanks': 'Cam on', 'Good': 'Tot', 'Bad': 'Xau'}
```
Cách này hoàn toàn đúng. Tuy nhiên, việc kết hợp (merge) hai dict nên là một thứ gì đó đơn giản hơn, "built-in" hơn. Hay nói cách khác nó phải readable hơn, nhất là đối với một ngôn ngữ như Python.

### Cách 2: Cách mặc định
Thực ra Python trước đó đã có một hàm mặc định cho việc thêm các giá trị của một dict vào dict khác.
Code Python:
```python
# Khong duoc viet dnew = d
dnew = d.copy()
dnew.update(d1)
```
Ta vẫn nhận được kết quả như trên
```
{'Hello': 'Xin chao', 'Thanks': 'Cam on', 'Good': 'Tot', 'Bad': 'Xau'}
```
Cách này tuy đã readable hơn nhưng vẫn có một nhược điểm. Bạn phải copy dữ liệu từ một dict trước khi gọi hàm update. (Tất nhiên nếu bạn update trực tiếp vào d thay vì dnew thì không nói làm gì)
Và những người thích trường phái lazy code (như mình) thì luôn muốn có một cách nào đó để viết tất cả mọi thứ trên một dòng :D

### Cách 3: Cách "Pro"
Cách này vận dụng unpacking operator của Python (phiên bản >= 3.5)
```python
dnew = {**d, **d1}
```
Ưu điểm:
- Một dòng code
- Trông có vẻ Pro

Nhược điểm:
- Không phải ai cũng hiểu bạn đang code cái gì.
- Tạo một cảm giác rất C chứ không phải Python.

### Cách 3.9: Union operator - Toán tử hội
Và trong phiên bản Python 3.9 sắp tới đây, chúng ta sẽ có thêm một cách nữa để giải quyết vấn đề trên.

Nếu các bạn đã học về tập hợp thì chắc chắn các bạn đều sẽ quen với toán tử hội này, nó cũng là dấu OR (trong lý thuyết tập hợp và lý thuyết logic thì hội và hoặc có thể coi là tương đương với nhau) của các ngôn ngữ khác.
Và cách viết dấu hội này trong Python
```python
dnew = d | d1
```
Đọc thành lời là dnew bằng d hội d1. Và được hiểu là lấy tất cả phần tử nằm trong d hoặc d1.

Thực ra kí hiệu này không mới trong Python, nó đã được dùng để hội hai tập hợp (set)
```python
# Day la tap hop, khong phai dict
a = {1, 2, 3}

# Day cung la tap hop, nhung cach viet khac de khoi nham lan
b = set((3, 4, 5))

print(a)
print(b)
print(a | b)
```

Kết quả:

    {1, 2, 3}
    {3, 4, 5}
    {1, 2, 3, 4, 5}

Và bây giờ thì dấu hội ```|``` đã có thể dùng được trên dict.

### Phiên bản phép gán
Cũng giống như phép cộng ```+``` có ```+=```, thì phép ```|``` cũng có ```|=``` với ý nghĩa tương tự
```python
d1 = d1 | d2
```
sẽ tương đương với
```python
d1 |= d2
```
