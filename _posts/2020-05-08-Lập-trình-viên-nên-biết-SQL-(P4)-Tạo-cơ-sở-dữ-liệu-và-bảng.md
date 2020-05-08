---
layout: post
title: Lập trình viên nên biết SQL (P4) Tạo cơ sở dữ liệu và bảng
summary: Dữ liệu là yếu tố không thể thiếu đối với bất kì mô hình quản lí nào. Dù là một tập đoàn, một công ty, hay chỉ là một cửa hàng nhỏ cũng cần có cách tổ chức và quản lý dữ liệu hiệu quả. Cơ sở dữ liệu và các hệ quản trị ra đời. Trong ngành lập trình, việc tạo lập, quản lý cơ sở dữ liệu cũng là yêu cầu bắt buộc đối với lập trình viên (nhất là lập trình viên backend). Trong bài viết này, mình sẽ bước đầu xây dựng một cơ sở dữ liệu và tạo các yếu tố cơ sở nhất chính là các bảng dữ liệu.
date: 2020-05-03 15:02
categories: SQL Database
---

### Đề
Dữ liệu là yếu tố không thể thiếu đối với bất kì mô hình quản lí nào. Dù là một tập đoàn, một công ty, hay chỉ là một cửa hàng nhỏ cũng cần có cách tổ chức và quản lý dữ liệu hiệu quả. Cơ sở dữ liệu và các hệ quản trị ra đời.

Trong ngành lập trình, việc tạo lập, quản lý cơ sở dữ liệu cũng là yêu cầu bắt buộc đối với lập trình viên (nhất là lập trình viên backend). Trong bài viết này, mình sẽ bước đầu xây dựng một cơ sở dữ liệu và tạo các yếu tố cơ sở nhất chính là các bảng dữ liệu.

### Warning!
Các bạn hoàn toàn có thể tạo cơ sở dữ liệu và bảng thông qua giao diện. Nhưng trong bài viết này, mình sẽ chủ yếu giới thiệu cách dùng lệnh SQL.

### Tạo Database project
*Phần này chỉ dành cho các bạn dùng Visual studio như mình (hoặc theo hướng dẫn của mình ở [P1](https://laptrinhvienblog.github.io/sql/database/2020/04/27/L%E1%BA%ADp-tr%C3%ACnh-vi%C3%AAn-n%C3%AAn-bi%E1%BA%BFt-SQL-%28P1%29-Gi%E1%BB%9Bi-thi%E1%BB%87u/). Bạn nào dùng SQL server management studio thì chỉ cần connect vào server thôi.*

Các bạn tạo Database project như hình nhé
![Visual studio database project lập trình SQL](https://lh3.googleusercontent.com/ODbdkEbGOMYbH4ZWFzd95_VBfidDsa11gp39bnM8oH2_YqvSQyg_BUvUNUIXD20c2vH4VHUd1U82CHC_-0iskIaNRF-SVj_e9IAIwroxWZbTSVm3Oi0cRE41RHmqjRTqwg22GfX4i_9Q33ycJ6b4a2RnQFBdXcYDAYEtVnYnVMbZ36WmDtXMIm_7bWg04GOWixn8tRv2DPH_HAGcnobD5ioSMYDCSNe207rFA9vGRHGjxZV976B8zorP4GEM8FHmc1KNErpNFMteArN_8njApxmUnrzVjjSiBx-TdqEZc7QzUtT0OqFRGf7Xfbqf_supmwX-EDx_YjY1dTGv4dcriZrEtS_GaDKNXcL4PrrGnH4FFC9BBxYGP_QnncyShlDWimPUhQNDmo1_9L1B5PAp4S06i_Z0NQlIBl2ha2Yk0xp1b98yHWu3nKT6USyFBGXQnOTNxcxPtp4tUQKVkBe5M-nAIA-iwq7Z6HZi4sK0_xwZ0aHfHeKe71YzpGVeyLR7Mw8_oVqyFQTnPOVDIJlx64GNBQ98RLbuPYx1ySe7IvxRipQRbdZaBStZ2GiLLNBDDg-iQo7_bX3hdc1xiZkcmtUYZe5DYLNuCJC5WvBfiYwpdjKAndgNPcecgnRvLy2IHemq3c6EJMP-xG2S5dem_2fSoYXt9FvOQRi_5UxMTY5QgP79bCcY3Xc2mJjhYg=w915-h635-no?authuser=0)

Sau khi tạo project, bạn mở Solution Explorer và tạo một file script mới
![Visual studio database project thêm file script lập trình SQL](https://lh3.googleusercontent.com/tgQFxH6oEE0FMUsJwbGhkOnFbumajKsi8q1ZHtFM1d4MBGot82OlpHx3RlFSDi7_3xvp4uNnzJqimJZ_IkXKzQaXscb5Ak7emUFPHTnygFJ9Fqh4KYkoLCDjLtIcGWdcbaGCZWmrw5IIS1zWWPBelLFi5rwZVQs8V9-2faM2k3Pt6hhxRuhqWHAtkEGUimvyVd5X6J69p7mYAKLcC00A0DBmwhELdn7pw1jSJKRz2dnnqDYC2WsufM2t-wXI4JQ0oK7ZpSX5nBqJCKsliUh09AmgmhC5hJS9hSlXqYcY-GXMEXxxjDHDGEm9XNe6Wb9JLX63mpfl_RWeN3mCo7PXGru6_k5FbdXXanvRWmWQXjAu-InYcnUKHKh1TdsKN0HdXy3OuvrGtgUQ7n1_aHmrWAV7MPkRorpoHCcyWIns8p-brJ7Ha2nYqgJgLstvlI8k_SkfAFsmhyjXqub5X8yU2bqBJCUIgqoygaKZFwwGKtZcHhBpiuHoVakcEnUeQOtIAaQskQGj-RlIWYNxhuFiESOsmIHQFb_nJguZXlNBBm2LkF--YyEcDVYEXdsNwc1XdkinwHgsQPCmQPjOr1NtKU-Ef1g51d1cQVxonIxhKzJYov0WWO998Nf9BWBxfc4GwKl4SqlxH1G_-gOCzOvUCPlUqAztQiACtUSOU235oKzXifXrK0h8O_QeBf2pEw=w572-h635-no?authuser=0)

Và bây giờ bạn sẽ viết lệnh trên file script mới này.
![Lập trình SQL script tạo file và viết mã lệnh truy vấn tạo bảng SQL](https://lh3.googleusercontent.com/w34cy0ua4GbedRN_EblXRp23y0H0WP4BCiBTrFXFebGbbGkTJE7e0vCQnWkJO6zc8kwUgopJ8MnRMPOCfgJeIZnkW5cynyNDRONJRnS_LzEbz8juueA79QvVz4bbt7_swHuEn48lQyv-qG6UosrkENRAq8UEGGnthfdg43Qxu3zexn85_ftTGhSYkTQDOHXexR3a5diT5_ohY2VErP6OTI8t570jIN1bbjrUtDnBg7U7122iQO-rulS6rUqy_5dRagtf-d5AyvdEQPaTveqAT9nEHkPodcRWfd99txP6jwGh-vawjvwRX4YFOEE7cG_degTyGYGUXG9ZM4tQ7546x_I8Ajh2SBLqHZCBCqKz1eO92oWiWg_lSYgHdmgVHgKQCRDy5aJJ4o21T5cbpEJjr-OJChqNfIrg1VDPXeLt0ArEdUHgbvxbSNyU_iYDlR5fx5Zn8omDDiC5tqp3suC-q2gWe4Pi3DTuiOGnA_WJvZDEoEEEywaLcZPrPVUJC2AwwOej0BumzxNcC6NGb-D-CVV9fPLaVYIaHnAQGbs52fvFZOrHxcerr-puCbh2pleuU9QxWAXjzJedQ4Oi-zsFgLqsKVElgEGZMCM5l_JxzqLaVMyp5aO8W_uU4Qh9LQJPIv7G3dNwNtcqJeKA3fomEWWQm7l4Yv7t0gh4Q_CquEfyNdZAgYfwkn1yBQanhA=w933-h422-no?authuser=0)

### Tạo cơ sở dữ liệu (CSDL)
Trước khi có thể tạo bảng và lưu trữ dữ liệu, bạn cần tạo một cơ sở dữ liệu trước.

Mặc định khi tạo Database project thì Visual studio cũng sẽ tạo một Database cho bạn trên SQL server với tên Database trùng với tên Project. Các bạn có tạo thao tác trực tiếp ở CSDL này.

Nếu không, các bạn có thể tạo CSDL khác để tiện cho việc quản lý của bạn
```sql
CREATE DATABASE DATABASENAME
```
Các bạn có thể xem thông tin về các CSDL ở SQL server object explorer
![SQL server tạo bảng tạo cơ sở dữ liệu kiểm tra bảng visual studio](https://lh3.googleusercontent.com/7LX5SEiuSCIz4tCEhfYVoHuFNxji23dg0WldaSD0kl0jvM7u9oG5rxlfpFe_1bQuV35saX3kUn7T929kgF0EIbjY5qJS7vGOVe42skMHOFN14KsXnWKpOAKE8jozgGHTcOLEKzeDXnFRqk5WHF5xvDAE9LzMtOnCJsOvyeGgG7VpHeeClM2I244Pb6uMfJQr9HrIREvUfBfCsVdDDPNPTGz5fH12cEN6JFpm1L7uZQwSq9cqBwd-1Nf1HmUxpzx58n8HhjpV5kCg2qhauGyheLE89GjAy1fZ1TJbV0GdCW-MpxaNODejZyepQOLws-gaUZjgRXY3reayve94BQNWxKl4nIMi4cp6nMJwzxTEQtHCukkT29hjiPKsfM0nsr934g4R4bOg9yUwlPJpprO_Dgj2kOVrM-JEd1-yAXcAZ-OGKvSf4HYDa3qHVBBylglPP-s_QlciEd3gKdj4vmkrwPTNjaH9DtDJOOZ9fEIZaxbeltdzMFHkhpdTEMFniwvXQJ9Tz9juw7jvZewNYtn54SSoRpZjr8TAv1h5-gDTOd5KA94SuPi4EfX8gxo-2noxkcD60vVf8A8PltIygDpz3veWYa3XfdWA82h0k0UcS3jWrZgrhsSw94AADQQHZn-ymwHZVgVqMC-GU3aiU7X8nbVdap4ODxFql8Sc1VhLHaX48O8CS8K2VDYmiuo6rQ=w1307-h586-no?authuser=0)
Như hình mình tạo CSDL ```EMPLOYEE```. Còn CSDL ```DemoDatabase``` là được tạo mặc định kèm với project.

Và để cho nhất quán và tiện theo dõi, bài này mình sẽ cùng xây dựng một cơ sở dữ liệu ```EMPLOYEE``` như hình
![Tạo cơ sở dữ liệu SQL tạo bảng mô hình nhân viên](https://lh3.googleusercontent.com/Bflg3hXpwaGYb1uQUW2NlCWDxn-2HFuPWoekG3-UCy6DHr_J7rvvG_CX13onYElmeskTaiMO6R4XVV6MGc7A5HomYMTp9T_TcnnRTEgkfl61HfV0CFF4XlslQAkGqy8BcJT5cuDAvgBjXIh6xvo17C8V1lCrYyDeU9AGW2hm5IlYW2JDRPaH8Eos68fCHb0OBIjij2qn0YtfdTNjDbqQj0qsjcYN2LfewE2HA9go4I7r9aBvGDadMhqjYjdznc_FiLgH2wagGapEWpkVjH8e-uDAP3yllM0TCZAJwMTjn7B6gLNNV4iTxuhIDXmMcCsjekfII_bABkhLZhj_zP69v6-VKsC9MFmzCUD-5n9flPuklSxRFrM7ip_Ynak2MdnkWaJTBtSfU3oqamrC0iAoGAZeWmNIlMClsRIWiQvNz0e3EiJ9AcLyHOlK6re4HP3d5FDF2ohAl_RyfH3P84V2q_v4vMN8E1vJmJFf6xtlog3IQfz33KQzukSzWb_H-iaf-nTCtgxryEe9h4dnPmnL8LtJLbl3eY522UMtv8M-RZ-5mCFH7HyY9VDdMn1F1NLf5LvQQXiNzH8TgZVmpcs0zY8goIRXh6xUGvHsndjOHzKeOf5QbAOKkS6Lj5miJwiDNIlfHTu1cUvrXqFdldxXaji5xQh0Xk599_XmP8qjBPOO82Rf82qq77DscQenIg=w621-h635-no?authuser=0)
*Mô hình được lấy từ sample của mySQL. Đừng quan tâm đến phần indexes, mình sẽ nói sau.*

### Tạo bảng
Trước khi tạo bảng, bạn chạy lệnh
```SQL
USE EMPLOYEE
```
Để chuyển vào CSDL ```EMPLOYEE```. Sau lệnh này dữ liệu các bạn tạo sẽ nằm trong ```EMPLOYEE```

Cú pháp tạo bảng như sau
```sql
CREATE TABLE
(
	TENCOT1 KIEUDULIEU RANGBUOC(NEU CO),
	TENCOT2 KIEUDULIEU RANGBUOC(NEU CO),
	...
)
```
Kiểu dữ liệu thì các bạn đã biết trong phần [trước](https://laptrinhvienblog.github.io/sql/database/2020/05/03/L%E1%BA%ADp-tr%C3%ACnh-vi%C3%AAn-n%C3%AAn-bi%E1%BA%BFt-SQL-%28P3%29-Ki%E1%BB%83u-d%E1%BB%AF-li%E1%BB%87u-trong-SQL/) rồi. Còn về ràng buộc thì có thể kể đến một số ràng buộc thường thấy như:
- Ràng buộc khóa chính, khóa ngoại
- Ràng buộc giá trị (CHECK)
- Ràng buộc NULL, NOT NULL cho phép ô dữ liệu đó có thể được bỏ trống khi nhập liệu hay không.
- ...

Mình sẽ tạo bảng EMPLOYEES như trong sơ đồ
```sql
CREATE TABLE EMPLOYEES
(
	EMP_NO INT PRIMARY KEY, -- Mặc định PRIMARY KEY sẽ NOT NULL
	BIRTHDAY DATE, -- Nếu không nói gì, mặc định sẽ là NULL
	FIRST_NAME VARCHAR(14) NOT NULL,
	LAST_NAME VARCHAR(16) NOT NULL,
	GENDER CHAR(1) CHECK (GENDER IN ('M', 'F')), -- Điều kiện CHECK kiểm tra giá trị GENDER
	HIRE_DATE DATE
)
```
Để thuận tiện cho việc quản lý lỗi, bạn có thể đưa các ràng buộc thành các đối tượng riêng với cột và đưa vào bảng.
Ví dụ bảng salaries trong sơ đồ:
```SQL
CREATE TABLE SALARIES
(
	EMP_NO INT FOREIGN KEY REFERENCES EMPLOYEES(EMP_NO) ,
	SALARY INT,
	FROM_DATE DATE,
	TO_DATE DATE,
	-- Thêm ràng buộc CONSTRAINT TENRANGBUOC RANGBUOC
	-- Khi phát sinh lỗi, chúng ta sẽ biết được lỗi ở ràng buộc nào thông qua tên ràng buộc
	CONSTRAINT PK_SALARIES PRIMARY KEY (EMP_NO, FROM_DATE),
	CONSTRAINT FK_SALARIES_EMPLOYEES FOREIGN KEY (EMP_NO) REFERENCES EMPLOYEES(EMP_NO),
	CONSTRAINT SALARIES_FROM_TO CHECK (FROM_DATE <= TO_DATE)
)
```
### Sửa bảng 
Trong nhiều trường hợp, chúng ta muốn sửa cấu trúc bảng sau khi tạo. Chúng ta dùng lệnh
```sql
ALTER TABLE TENBANG
LENHSUA
```
Có 3 lệnh sửa cơ bản:
- Thêm cột hoặc ràng buộc
- Xóa cột hoặc ràng buộc
- Sửa kiểu dữ liệu cột

### Thêm
```sql
-- THEM COT
ALTER TABLE TENBANG
ADD TENCOT KIEUDULIEU

-- THEM RANG BUOC
ALTER TABLE TENBANG
ADD CONSTRAINT TENRANGBUOC RANGBUOC
```
Ví dụ
```sql
ALTER TABLE SALARIES
ADD DATE_RECEIVED DATE

ALTER TABLE SALARIES 
ADD CONSTRAINT DR CHECK (DATE_RECEIVED BETWEEN FROM_DATE AND TO_DATE)
```
### Xóa 
```sql
-- XOA COT
ALTER TABLE TENBANG
DROP COLUMN TENCOT

-- XOA RANG BUOC
ALTER TABLE TENBANG
DROP CONSTRAINT TENRANGBUOC
```
Ví dụ:
```SQL
ALTER TABLE SALARIES
DROP CONSTRAINT DR

ALTER TABLE SALARIES
DROP COLUMN DATE_RECEIVED 
```
### Sửa
Thay đổi kiểu dữ liệu của cột
```sql
ALTER TABLE TENBANG
ALTER COLUMN TENCOT KIEUDULIEUMOI
```
### .
Một lý do khiến chúng ta thường dùng các lệnh thêm xóa sửa khi tạo bảng chính là ràng buộc khóa ngoại. Vì các bảng được tạo ra không đồng thời nên sẽ có một số ràng buộc khóa ngoại với các bảng chưa được tạo ra. Cách xử lí là chúng ta sẽ tạo bảng trước, sau đó mới thêm khóa ngoại.
### Ràng buộc khóa ngoại
Trong sơ đồ các bảng ở trên, chúng ta đã tạo bảng ```EMPLOYEES``` và ```SALARIES```. Giữa chúng có một khóa ngoại là ```EMP_ID```.

Chúng ta sẽ thêm ràng buộc khóa ngoại như sau:
```sql
ALTER TABLE SALARIES
ADD CONSTRAINT FK_SALARIES_EMPLOYEES FOREIGN KEY (EMP_NO) REFERENCES EMPLOYEES(EMP_NO)
```
Vì khóa ngoại là của bảng ```SALARIES``` nên chúng ta sẽ thêm vào bảng này một khóa ngoại liên kết cột ```EMP_NO``` tham chiếu đến bảng ```EMPLOYEES``` cột ```EMP_NO```. (Lưu ý trùng tên, cột ```EMP_NO``` trước là của bảng ```SALARIES```, cột   ```EMP_NO``` sau là của bảng ```EMPLOYEES```)

Chúng ta cũng có thể thêm khóa ngoại trực tiếp khi tạo bảng nếu tham chiếu của nó đến bảng đã tồn tại.
Ví dụ bảng ```TITLES```
```sql
CREATE TABLE TITLES
(
	-- -- SHORT WAY
	-- EMP_NO INT REFERENCES EMPLOYEES(EMP_NO)
	EMP_NO INT FOREIGN KEY REFERENCES EMPLOYEES(EMP_NO),
	TITLE VARCHAR(50),
	FROM_DATE DATE,
	TO_DATE DATE,
	CONSTRAINT PK_TITLES PRIMARY KEY (EMP_NO, TITLE, FROM_DATE),
	CONSTRAINT TITLES_FROM_TO CHECK (FROM_DATE <= TO_DATE)
)
```
Hoặc 
```SQL
CREATE TABLE TITLES
(
	EMP_NO INT,
	TITLE VARCHAR(50),
	FROM_DATE DATE,
	TO_DATE DATE,
	CONSTRAINT PK_TITLES PRIMARY KEY (EMP_NO, TITLE, FROM_DATE),
	CONSTRAINT TITLES_FROM_TO CHECK (FROM_DATE <= TO_DATE),
	CONSTRAINT FK_TITLES_EMPLOYEE FOREIGN KEY (EMP_NO) REFERENCES EMPLOYEES(EMP_NO)
)

```

### Xóa bảng, Xóa Database 
Vì một lí do gì đó mà bạn muốn xỏa bảng, xóa Database?
Dùng lệnh ```DROP``` như trên
```sql
DROP TABLE TENBANG
DROP DATABASE TENDB
```
### Kết
Trong bài viết này, mình đã hướng dẫn các bạn xây dựng cấu trúc một database, tạo bảng và ràng buộc.
Mình cũng đã code ví dụ một số bảng của sơ đồ ở trên. Các bạn nên tự code phần còn lại để tập luyện. Về cơ bản thì số lượng lệnh trong SQL cũng không nhiều và khá tương tự nhau nên việc nắm chắc cũng không có gì là khó.

.

*Nếu các bạn muốn nhận file mình đã tạo toàn bộ mô hình ở trên, có thể gửi tin nhắn cho mình ở tính năng [Say Hello](https://laptrinhvienblog.github.io/contact/) của trang.*

*Bài cùng Series:*[P1](https://laptrinhvienblog.github.io/sql/database/2020/04/27/L%E1%BA%ADp-tr%C3%ACnh-vi%C3%AAn-n%C3%AAn-bi%E1%BA%BFt-SQL-%28P1%29-Gi%E1%BB%9Bi-thi%E1%BB%87u/) [P2](https://laptrinhvienblog.github.io/sql/database/2020/04/29/L%E1%BA%ADp-tr%C3%ACnh-vi%C3%AAn-n%C3%AAn-bi%E1%BA%BFt-SQL-%28P2%29-Kh%C3%B3a-trong-SQL/) [P3](https://laptrinhvienblog.github.io/sql/database/2020/05/03/L%E1%BA%ADp-tr%C3%ACnh-vi%C3%AAn-n%C3%AAn-bi%E1%BA%BFt-SQL-%28P3%29-Ki%E1%BB%83u-d%E1%BB%AF-li%E1%BB%87u-trong-SQL/) P4