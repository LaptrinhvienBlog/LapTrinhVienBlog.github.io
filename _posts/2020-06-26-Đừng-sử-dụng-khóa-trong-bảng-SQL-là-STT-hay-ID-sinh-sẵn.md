---
layout: post
title: Đừng sử dụng khóa chính trong bảng là STT hay ID sinh sẵn
summary: Trong quá trình thiết kế cơ sở dữ liệu cho ứng dụng, đôi lúc chúng ta phải phân vân chọn khóa cho bảng dữ liệu. Tất nhiên với những bảng dữ liệu có sẵn các cột mang tính định danh duy nhất (ví dụ bảng khách hàng có cột chứng minh nhân dân) thì vấn đề này khá đơn giản. Tuy nhiên đôi lúc vì nhiều lí do khác nhau mà chúng ta phải sinh ra thêm một cột mới có tính duy nhất để làm khóa cho bảng dữ liệu. Đây là việc hết sức bình thường và có nhiều hệ quản trị cơ sở dữ liệu (DBMS) cũng tích hợp sẵn tính năng auto-increment field aka số thứ tự cho chúng ta. Tuy nhiên liệu có nên sử dụng tính năng này trong thực tế?
date: 2020-06-26 16:29
categories: SQL Database
---

Trong quá trình thiết kế cơ sở dữ liệu cho ứng dụng, đôi lúc chúng ta phải phân vân chọn khóa cho bảng dữ liệu.

Tất nhiên với những bảng dữ liệu có sẵn các cột mang tính định danh duy nhất (ví dụ bảng khách hàng có cột chứng minh nhân dân) thì vấn đề này khá đơn giản. Tuy nhiên đôi lúc vì nhiều lí do khác nhau mà chúng ta phải sinh ra thêm một cột mới có tính duy nhất để làm khóa cho bảng dữ liệu. Đây là việc hết sức bình thường và có nhiều hệ quản trị cơ sở dữ liệu (DBMS) cũng tích hợp sẵn tính năng auto-increment field aka số thứ tự cho chúng ta.

Ví dụ
```sql
CREATE TABLE SOMETHING
(
	ID INT NOT NULL IDENTITY PRIMARY KEY,
	NAME VARCHAR(50),
	PROPERTIES VARCHAR(50)
);

```

Đoạn code SQL trên sẽ tạo một bảng có 3 thuộc tính (3 cột), trong đó cột ID sẽ được sinh tự động. Nghĩa là dù không xác định cột này khi nhập liệu, hệ quản trị cơ sở dữ liệu sẽ tự động điền vào một số và đảm bảo số này là duy nhất trong toàn bộ bảng. Thường là số này sẽ được điền tăng dần 1, 2, 3, ...

Tuy nhiên theo mình, thực tế thì việc thiết kế cơ sở dữ liệu, nhất là cơ sở dữ liệu cho ứng dụng (trong hầu hết trường hợp, cơ sở dữ liệu đều đi kèm ứng dụng truy xuất đến nó) thì việc dùng cột STT hay ID do hệ quản trị cơ sở dữ liệu cung cấp là một ý tưởng rất tệ và nên tránh. Đây là lí do tại sao.

### Lệ thuộc vào hệ quản trị cơ sở dữ liệu

Việc chúng ta làm một ứng dụng (một trang web chẳng hạn) nhưng một phần rất quan trọng trong mã nguồn của chúng ta lại phụ thuộc vào bên thứ ba (hệ quản trị cơ sở dữ liệu - database management system). Giả sử trong quá trình deploy sản phẩm, hoặc trong quá trình vận hành, chúng ta muốn đổi từ DBMS hiện tại (vd: MS SQL server, MySQL) sang một DBMS khác mà không hỗ trợ auto-increment field thì sao? Nếu không sửa lại mã nguồn thì đó là không thể.

Chưa kể, mỗi hệ quản trị cơ sở dữ liệu lại có một cách sinh id này khác nhau, điều này có thể khiến quá trình chuyển đổi gặp nhiều khó khăn.

### Hiệu năng

Giả sử chúng ta có một bảng mà id của nó do DBMS sinh. Khi chúng ta thêm một dòng mới, sau đó vì lí do gì đó chúng ta cần id của dòng mới này (ví dụ để tham chiếu), cách duy nhất là phải truy vấn vào cơ sở dữ liệu. Điều này sẽ làm ảnh hưởng không nhỏ đến hiệu năng của ứng dụng.

###  Hệ thống phân tán

Khi vận hành ứng dụng, chúng ta có thể phải xây dựng trên các hệ thống phân tán gồm nhiều server. Mỗi server lại chứa 1 phần cơ sở dữ liệu khác nhau.

Nếu khi xây dựng ứng dụng, chúng ta giao việc sinh id cho cơ sở dữ liệu thì kết quả trên hệ thống phân tán khi vận hành có thể dẫn tới việc trùng lặp khóa do mỗi server sẽ sinh id một cách độc lập.

### Giải pháp
Giải pháp thật ra rất đơn giản. Nếu vấn đề nằm ở chỗ giao việc sinh id cho DBMS, vậy thì chúng ta không giao việc sinh id cho DBMS nữa.

Chúng ta làm thế nào? Chúng ta sẽ tự sinh ID.

Chúng ta phải tự sinh ID như thế nảo? Chúng ta phải sinh ID đảm bảo tính đơn nhất, không lặp lại.

Chúng ta có thể sinh số ngẫu nhiên (hoặc chuỗi ngẫu nhiên) không? Không. Vì ngẫu nhiên không có nghĩa là không lặp lại.

Vậy chúng ta làm thế nào? Làm thế nào thì bài đã dài rồi, hẹn các bạn trong [bài viết sau](https://laptrinhvienblog.github.io/sql/database/2020/07/12/C%C3%B9ng-t%C3%ACm-hi%E1%BB%83u-v%E1%BB%81-c%C3%A1ch-sinh-Snowflake-ID-trong-c%C6%A1-s%E1%BB%9F-d%E1%BB%AF-li%E1%BB%87u/).


