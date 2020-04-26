---
layout: post
title: Lập trình viên nên biết SQL (P1): Giới thiệu
date: 2020-04-26 17:30
summary: Bước đầu tìm hiểu về SQL.
categories: SQL Database
---

### Đề
Nói về SQL thì gần ai học lập trình cũng đã từng làm việc hay chí ít là cũng từng nghe qua về nó. Đối với lập trình viên ở phía back-end thì mặc dù hiện nay đã có nhiều công nghệ thay thế (Như Entity Framework của .Net) nhưng SQL vẫn có thể coi là một yêu cầu bắt buộc trong tuyển dụng cũng như công việc. Series này nhằm giúp các bạn mới bắt đầu tìm hiểu có được những kiến thức từ cơ bản đến những khía cạnh "ngách" về SQL.
### Thực
SQL (viết tắt của Structure Query Language) là một ngôn ngữ truy vấn dữ liệu "mang tính cấu trúc". Nói vậy nghĩa là chỉ những hệ quản trị cơ sở dữ liệu (Database Management System - DBMS) quan hệ (có cấu trúc) như MS SQL, MySQL,... mới hỗ trợ truy vấn SQL trực tiếp. Tuy nhiên các hệ DBMS không quan hệ như MongoDB,... bằng cách này hay cách khác vẫn hỗ trợ một số lệnh SQL.
Bên cạnh đó, có một điều cần lưu ý. Dù là một ngôn ngữ, nhưng SQL không thống nhất giữa các DBMS. Điều này cũng không cần phải lấy làm lạ vì nó đã khá là phổ biến trong ngành lập trình cũng giống như việc các ngôn ngữ lập trình không giống nhau tùy vào cách thực thi của trình biên dịch. Tuy nhiên nó vẫn khá tương đồng. Nội dung bài viết sẽ hướng trọng tâm đến MS SQL, tuy nhiên khi có thể mình vẫn sẽ để cách viết của các DBMS khác bên cạnh để các bạn tiện tham khảo và đánh giá.
### Fun Fact về cách phát âm SQL
Hôm trước thì mình có thấy một bài viết về cách đọc SQL là [/ˈsiːkwəl/] (si-kồ). Nhưng theo mình thì cách đọc đúng vẫn nên là ([/ˈɛskjuːˈɛl/] (éts-kiu-eo).
Nghĩa là phát âm theo từng kí tự riêng biệt. Sở dĩ cách có cách đọc thứ nhất là do SQL có nguồn gốc từ một ngôn ngữ khác là Structured English QUEery Language viết tắt là SEQUEL. Tuy nhiên theo mình thì SEQUEL và SQL là hai ngôn ngữ khác nhau (như C và C++ vậy) nên cách đọc cũng phải khác nhau.
### Cài đặt
Để có thể thực hành SQL, bạn cần có một hệ quản trị cơ sở dữ liệu. Các bạn có thể tải và cài đặt MS SQL, MySQL, SQLite cho nhẹ, tùy sở thích của từng bạn từ trang chủ của mỗi phần mềm. Việc này khác đơn giản nên mình sẽ không hướng dẫn chi tiết,
Hoặc một sự lựa chọn khác là các bạn có thể sử dụng MS SQL trực tiếp trên Visual Studio nếu các bạn đã cài sẵn Visual Studio và không muốn cài thêm phần mềm nào khác.
### Hướng dẫn sử dụng MS SQL trên Visual Studio

Phiên bản Visual Studio mình sử dụng là 2019, các phiên bản khác cũng sẽ tương tự.
Đầu tiên các bạn mở Visual Studio Installer, đây là phần mềm đi kèm với Visual Studio khi cài đặt.  Bạn chọn Modify
![Visual Studi Install chọn Modify](/images/Lap-trinh-vien-nen-biet-sql/VSI-modify.png)
Sau đó bạn tìm và tick vào SQL Server Data Tools. Nó nằm trong phần Data Storage and Processing hoặc Individual components.
![Visual Studi Install chọn Modify](/images/Lap-trinh-vien-nen-biet-sql/VSI-sqlserver.png)
Nếu bạn đã cài đặt nó từ trước thì có thể bỏ qua, nếu chưa thì bấm vào modify để cài đặt.
Sau khi cài đặt xong thì bây giờ bạn có thể vào Visual Studio và tạo một Database Project để thực hiện tạo, quản lý và truy vấn cơ sở dữ liệu rồi.
### Kết
Bài viết này đã giúp các bạn có cái nhìn ban đầu về SQL và cài đặt công cụ để thực hành SQL.
Trong những phần sau, chúng ta sẽ cùng tìm hiểu về cú pháp để xây dựng và truy vấn cơ sở dữ liệu bằng SQL.