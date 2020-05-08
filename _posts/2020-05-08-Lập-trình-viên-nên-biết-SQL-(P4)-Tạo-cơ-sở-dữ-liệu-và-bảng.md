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

![Visual studio database project lập trình SQL](/images/Lap-trinh-vien-nen-biet-sql/VS-Database-project.png)

Sau khi tạo project, bạn mở Solution Explorer và tạo một file script mới

![Visual studio database project thêm file script lập trình SQL](/images/Lap-trinh-vien-nen-biet-sql/VS-Database-project-new-script.png)

Và bây giờ bạn sẽ viết lệnh trên file script mới này.

![Lập trình SQL script tạo file và viết mã lệnh truy vấn tạo bảng SQL](/images/Lap-trinh-vien-nen-biet-sql/Create-SQL-database.png)

### Tạo cơ sở dữ liệu (CSDL)
Trước khi có thể tạo bảng và lưu trữ dữ liệu, bạn cần tạo một cơ sở dữ liệu trước.

Mặc định khi tạo Database project thì Visual studio cũng sẽ tạo một Database cho bạn trên SQL server với tên Database trùng với tên Project. Các bạn có tạo thao tác trực tiếp ở CSDL này.

Nếu không, các bạn có thể tạo CSDL khác để tiện cho việc quản lý của bạn
```sql
CREATE DATABASE DATABASENAME
```
Các bạn có thể xem thông tin về các CSDL ở SQL server object explorer

![SQL server tạo bảng tạo cơ sở dữ liệu kiểm tra bảng visual studio](/images/Lap-trinh-vien-nen-biet-sql/Create-SQL-database.png)

Như hình mình tạo CSDL ```EMPLOYEE```. Còn CSDL ```DemoDatabase``` là được tạo mặc định kèm với project.

Và để cho nhất quán và tiện theo dõi, bài này mình sẽ cùng xây dựng một cơ sở dữ liệu ```EMPLOYEE``` như hình

![Tạo cơ sở dữ liệu SQL tạo bảng mô hình nhân viên](/images/Lap-trinh-vien-nen-biet-sql/Employee-model-sql.jpg)

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