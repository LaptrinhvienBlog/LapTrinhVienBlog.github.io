---
layout: post
title: Lập trình viên nên biết SQL (P2) Khóa trong SQL
summary: Ràng buộc dữ liệu là một tính chất vô cùng quan trọng trong mô hình cơ sở dữ liệu quan hệ (Relational Database), nhằm đảm bảo tính tin cậy và chính xác của dữ liệu, các luật ràng buộc giúp cho dữ liệu phù hợp và đúng đắn. Khóa (Key) là một thành tố thiết yếu để thực hiện ràng buộc dữ liệu trong SQL. Bài viết này sẽ giúp các bạn tìm hiểu về khóa, khóa chính, khóa ngoại và cách phân biệt.
date: 2020-04-29 10:19
categories: SQL Database
---

### Đề
Ràng buộc dữ liệu là một tính chất vô cùng quan trọng trong mô hình cơ sở dữ liệu quan hệ (Relational Database), nhằm đảm bảo tính tin cậy và chính xác của dữ liệu, các luật ràng buộc giúp cho dữ liệu phù hợp và đúng đắn.
Khóa (Key) là một thành tố thiết yếu để thực hiện ràng buộc dữ liệu trong SQL. Bài viết này sẽ giúp các bạn tìm hiểu về khóa, khóa chính, khóa ngoại và cách phân biệt.
## Các khái niệm về khóa (Key)
Giả sử một bảng dữ liệu có k thuộc tính (k cột). Tập hợp k thuộc tính đó là **R**
### Super key: Siêu khóa
Siêu khóa là một tập các thuộc tính dùng để xác định tính duy nhất của một dữ liệu.
Như vậy tập siêu khóa SK thỏa mãn:
- Là tập con khác rỗng của **R** 
- Với mọi giá trị dữ liệu t1, t2 thì t1[SK] khác t2[SK]
- Mọi bảng dữ liệu quan hệ luôn có ít nhất một siêu khóa

***Ví dụ:***

    KHOA(MÃKHOA,TÊNKHOA,NĂMTL,PHÒNG,ĐIỆNTHOẠI,NGÀYNHẬNCHỨC)
MÃKHOA,TÊNKHOA là một siêu khóa
MÃKHOA,TÊNKHOA,NĂMTL,PHÒNG,ĐIỆNTHOẠI,NGÀYNHẬNCHỨC là một siêu khóa

### Key: Khóa
Như ở trên đã thấy, một bảng có thể có nhiều siêu khóa, cần chọn ra một siêu khóa để làm đặc trưng duy nhất cho dữ liệu. Khái niệm khóa ra đời.
Khóa là siêu khóa có số lượng thuộc tính ít nhất.
Hay tập K là khóa nếu:
- K là một siêu khóa.
- Mọi tập con khác K của K không thể là siêu khóa. Hay nói cách khác, nếu bỏ đi bất kì thuộc tính nào trong K thì K không còn là siêu khóa nữa.

***Ví dụ:***
Vẫn lấy ví dụ ở trên

    KHOA(MÃKHOA,TÊNKHOA,NĂMTL,PHÒNG,ĐIỆNTHOẠI,NGÀYNHẬNCHỨC)
MÃKHOA là một khóa
TÊNKHOA là một khóa
Cả hai khóa này đều là siêu khóa có một phần tử.
***Lưu ý***: 
- Khóa chỉ cần có số lượng phần tử là ít nhất, không nhất thiết phải là 1 nên không phải khóa nào cũng có một phần tử. 
- Một bộ dữ liệu có thể vừa có khóa có 1 phần tử, vừa có khóa có nhiều hơn 1 phần tử. Miễn là đảm bảo khóa không thể bỏ bớt đi thuộc tính nào.
### Primary key: Khóa chính
Chúng ta đã thấy một bộ dữ liệu có thể có nhiều khóa. Do đó chúng ta cần chọn ra một trong số đó làm khóa chính. Khóa chính là do chúng ta chọn ra từ các khóa trong bảng, nên lựa chọn khóa có ít thuộc tính nhất.
Ví dụ:
KHOA( <ins>MÃKHOA</ins>,TÊNKHOA,NĂMTL,PHÒNG,ĐIỆNTHOẠI,NGÀYNHẬNCHỨC)

  ### Reference: Tham chiếu
  Một bộ R1 có một thuộc tính nhận giá trị từ R. Ta nói R1 tham chiếu đến R
  ***Ví dụ:***
  KHOA( <ins>MÃKHOA</ins>,TÊNKHOA,NĂMTL,PHÒNG,ĐIỆNTHOẠI,NGÀYNHẬNCHỨC)
 DIADIEM(<ins>MKHOA</ins>, THANHPHO)
 DIADIEM có giá trị MKHOA nhận giá trị từ MÃKHOA của KHOA nên ta nói DIADIEM tham chiếu đến KHOA
 ### Foreign Key: Khóa ngoại
Từ quan hệ tham chiếu ở trên, ta có khái niệm khóa ngoại
Cho R1 tham chiếu đến R có tập khóa chính PK, tập FK1 là khóa ngoại của R1 thỏa mãn:
- FK1 có cùng miền giá trị với PK
- Với mọi dữ liệu t1 của R1, luôn tồn tại một t trong R sao cho t1[FK1] = t[PK]

Như vậy ta có nhận xét:
- Khóa ngoại luôn tham chiếu đến khóa chính
- Khóa ngoại có thể tham chiếu đến khóa chính của bảng khác hoặc chính khóa chính của bảng hiện tại
- Có thể có nhiều khóa ngoại cùng tham chiếu đến 1 khóa chính.

### Một ví dụ về cơ sở dữ liệu và các khóa
Đây là một ví dụ hoàn chỉnh về cơ sở dữ liệu và các khóa. Các bạn nhớ kí hiệu gạch chân là khóa chính và mũi tên thể hiện quan hệ tham chiếu
![Cơ sở dữ liệu quan hệ SQL](/images/Lap-trinh-vien-nen-biet-sql/CSDL_QH.jpg)

### Kết
Bài viết đã cung cấp cho các bạn các khái niệm cơ bản về khóa và mối quan hệ trong cơ sở dữ liệu. Trong các phần sau chúng ta sẽ bắt đầu viết lệnh SQL để tạo bảng cũng như truy vấn dữ liệu.
*Bài cùng Series:*[P1](https://laptrinhvienblog.github.io/sql/database/2020/04/27/L%E1%BA%ADp-tr%C3%ACnh-vi%C3%AAn-n%C3%AAn-bi%E1%BA%BFt-SQL-%28P1%29-Gi%E1%BB%9Bi-thi%E1%BB%87u/) P2