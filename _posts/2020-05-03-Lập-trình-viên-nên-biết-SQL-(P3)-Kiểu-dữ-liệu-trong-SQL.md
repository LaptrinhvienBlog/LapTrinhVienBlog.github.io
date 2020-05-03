---
layout: post
title: Lập trình viên nên biết SQL (P3) Kiểu dữ liệu trong SQL
summary: Cũng giống như lập trình, thì cơ sở dữ liệu cũng cần có các kiểu dữ liệu. Chúng giúp xác định xem một trường hay thuộc tính có miền giá trị như thế nào để hệ quản trị cơ sở dữ liệu thuận tiện trong việc lưu trữ, quản lý, truy xuất. Bài viết này giống như một từ điển để tra cứu các kiểu dữ liệu trong SQL (MS SQL server) để chuẩn bị cho các bài viết sau.
date: 2020-05-03 15:02
categories: SQL Database
---

### Đề
Cũng giống như lập trình, thì cơ sở dữ liệu cũng cần có các kiểu dữ liệu. Chúng giúp xác định xem một trường hay thuộc tính có miền giá trị như thế nào để hệ quản trị cơ sở dữ liệu thuận tiện trong việc lưu trữ, quản lý, truy xuất. Bài viết này giống như một từ điển để tra cứu các kiểu dữ liệu trong SQL (MS SQL server) để chuẩn bị cho các bài viết sau.

### Kiểu chuỗi trong SQL

| **Kiểu dữ liệu** | **Miền giá trị**                                                   | **Chú thích**                                                                                                                                                                                  |
|------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| CHAR(n)          | Chuỗi có độ dài n (cố định)                                        | - n tối đa 8000<br> - Nếu chuỗi nhập vào không đạt tới độ dài n, khoảng trắng sẽ được tự động thêm vào cho đủ<br> - Không chứa kí tự Unicode                                                   |
| VARCHAR(n)       | Chuỗi có độ dài từ 0..n                                            | - n tối đa 8000<br> - Độ dài không cố định, dù chuỗi nhập không đạt tới độ dài n thì vẫn giữ nguyên.<br> - Không chứa kí tự Unicode<br> - Dùng ```VARCHAR(max)``` để lưu trữ chuỗi lên đến 2GB |
| NCHAR(n)         | Chuỗi unicode có độ dài n (cố định)                                | - n tối đa 4000<br> - Nếu chuỗi nhập vào không đạt tới độ dài n, khoảng trắng sẽ được tự động thêm vào cho đủ                                                                                  |
| NVARCHAR(n)      | Chuỗi unicode có độ dài từ 0..n                                    | - n tối đa 4000<br> - Độ dài không cố định, dù chuỗi nhập không đạt tới độ dài n thì vẫn giữ nguyên.<br> - Dùng ```NVARCHAR(max)``` để lưu trữ chuỗi lên đến 2GB                               |
| TEXT             | Chuỗi có kích thước tối đa 2^31-1 = 2,147,483,647 Bytes ~ 2 GB     | - Độ dài không cố định<br> - Không chứa kí tự Unicode<br> - Không hoàn toàn giống VARCHAR(max)                                                                                                 |
| NTEXT            | Chuỗi Unicode có kích thước tối đa 2^30 - 1 = 1,073,741,823 Bytes  | - Độ dài không cố định<br> - Không hoàn toàn giống NVARCHAR(max)                                                                                                                               |


### Chuỗi nhị phân trong SQL


| **Kiểu dữ liệu** | **Miền giá trị**                     | **Chú thích**                                                                                                                 |
|------------------|--------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| BINARY(n)        | Chuỗi nhị phân gồm n bytes (cố định) | - n tối đa 8000<br> - Dữ liệu nhị phân<br> - Nếu dữ liệu nhập vào không đủ n bytes, tự động thêm khoảng trống để bù đủ.       |
| VARBINARY(n)     | Chuỗi nhị gồm 0..n byte              | - n tối đa 8000<br> - Dữ liệu nhị phân<br> - Độ dài không cố định<br> - Dùng VARBINARY(max) để lưu chuỗi nhị phân lên đến 2GB |
| IMAGE            | Chuỗi nhị phân tối đa 2GB            |  - Dữ liệu nhị phân<br> - Độ dài không cố định                                                                                |


### Kiểu số trong SQL


| **Kiểu dữ liệu** | **Miền giá trị**                                                       | **Chú thích**                                                                                                                  |
|------------------|------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| BIT              | 0 hoặc 1                                                               | Số nguyên                                                                                                                      |
| TINYINT          | 0..255                                                                 | Số nguyên                                                                                                                      |
| SMALLINT         | -32768..32767                                                          | Số nguyên                                                                                                                      |
| INT              | -2,147,483,648..2,147,483,647                                          | Số nguyên                                                                                                                      |
| BIGINT           | -9,223,372,036,854,775,808..9,223,372,036,854,775,807                  | Số nguyên                                                                                                                      |
| DECIMAL(n, d)    | Số thập phân có tất cả n chữ số và d chữ số phần thập phân (sau dấu .) |  - n tối đa 38<br> - 0 <= d <= n<br>- Nếu không được khai báo:<br>   + n mặc định 18<br>   + d mặc đinh 0                      |
| DEC(n, d)        | Như DECIMAL(n, d)                                                      | Như DECIMAL(n, d)                                                                                                              |
| NUMERIC(n, d)    | Như DECIMAL(n, d)                                                      | Như DECIMAL(n, d)                                                                                                              |
| FLOAT(n)         | - 1.79E+308..-2.23E-308, 0, 2.23E-308.. 1.79E+308                      | - Số thực với dấu chấm động. n là số bit của phần chấm động (mantissa)<br> - n từ 1 đến 53. Mặc định là 53 nếu không khai báo. |
| REAL             | -3.40+E38..-1.18E-38, 0, 1.18E-38.. 3.40E+38                           | - Tương đương FLOAT(24)                                                                                                        |
| SMALLMONEY       | - 214,748.364 .. 214,748.3647                                          | - Biểu diễn thập phân chính xác hơn số FLOAT                                                                                   |
| MONEY            | -922,337,203,685,477.5808 .. 922,337,203,685,477.5807                  | - Biểu diễn thập phân chính xác hơn số FLOAT                                                                                   |


### Kiểu ngày tháng và thời gian trong SQL


| **Kiểu dữ liệu** | **Miền giá trị**                                                                               | **Chú thích**                                         |
|------------------|------------------------------------------------------------------------------------------------|-------------------------------------------------------|
| DATE             | '0001-01-01' .. '9999-12-31                                                                    | Định dạng YYYY-MM-DD                                  |
| DATETIME         | '1753-01-01 00:00:00.000' .. '9999-12-31 23:59:59.997'                                         | Định dạng YYYY-MM-DD hh:mm:ss[.mmm]                   |
| DATETIME2        | '0001-01-01 00:00:00' đến '9999-12-31 23:59:59.9999999'                                        | Định dạng YYYY-MM-DD hh:mm:ss[.mmmmmmm]               |
| SMALLDATETIME    | '1900-01-01 00:00:00' đến '2079-06-06 23:59:59'                                                | Định dạng YYYY-MM-DD hh:mm:ss                         |
| TIME             | 00:00:00.0000000 .. 23:59:59.9999999                                                           | Định dạng hh:mm:ss[.mmmmmmm]                          |
| DATETIMEOFFSET   | '0001-01-01 00:00:00' đến '9999-12-31 23:59:59.9999999'<br> Múi giờ lấy từ -14:00 đến +14:00.  | Định dạng YYYY-MM-DD hh:mm:ss[.nnnnnnn] [{+\|-}hh:mm] |


*Bài cùng Series:*[P1](https://laptrinhvienblog.github.io/sql/database/2020/04/27/L%E1%BA%ADp-tr%C3%ACnh-vi%C3%AAn-n%C3%AAn-bi%E1%BA%BFt-SQL-%28P1%29-Gi%E1%BB%9Bi-thi%E1%BB%87u/) [P2](https://laptrinhvienblog.github.io/sql/database/2020/04/29/L%E1%BA%ADp-tr%C3%ACnh-vi%C3%AAn-n%C3%AAn-bi%E1%BA%BFt-SQL-%28P2%29-Kh%C3%B3a-trong-SQL/) P3
