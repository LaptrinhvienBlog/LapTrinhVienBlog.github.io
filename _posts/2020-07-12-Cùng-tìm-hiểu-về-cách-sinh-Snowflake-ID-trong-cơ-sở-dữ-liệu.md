---
layout: post
title: Cùng tìm hiểu về cách sinh Snowflake ID trong cơ sở dữ liệu
summary: Trong cơ sở dữ liệu, trong lập trình, việc sinh ID là việc khá quan trọng. ID giúp chúng ta đảm bảo dữ liệu duy nhất, truy vấn dữ liệu và tạo các ràng buộc quan hệ trên cơ sở dữ liệu. Hầu hết các hệ quản trị cơ sở dữ liệu hiện nay đều có thể tự động sinh ID đảm bảo tính duy nhất. Tuy nhiên trong bài viết trước, chúng ta đã có lí do để không sử dụng ID sinh sẵn. Lí do quan trọng nhất vẫn là trên các hệ thống phân tán việc sử dụng ID sinh sẵn sẽ không bảo đảm tính duy nhất, không trùng lặp của ID. Snowflake ID chính là câu trả lời của các kĩ sư làm việc tại Twitter cho vấn đề trên. Làm sao để có thể sinh 6000 ID mỗi giây một cách độc lập trên nhiều server mà không trùng lặp?
date: 2020-07-12 20:11
categories: SQL Database
---

Trong cơ sở dữ liệu, trong lập trình, việc sinh ID là việc khá quan trọng. ID giúp chúng ta đảm bảo dữ liệu duy nhất, truy vấn dữ liệu và tạo các ràng buộc quan hệ trên cơ sở dữ liệu. Hầu hết các hệ quản trị cơ sở dữ liệu hiện nay đều có thể tự động sinh ID đảm bảo tính duy nhất. Chúng ta có thể hoàn toàn không quan tâm đến việc này và giao toàn bộ công việc cho hệ quản trị cơ sở dữ liệu lo. Tuy nhiên trong bài viết trước, chúng ta đã có lí do để [không sử dụng ID sinh sẵn](https://laptrinhvienblog.github.io/sql/database/2020/06/26/%C4%90%E1%BB%ABng-s%E1%BB%AD-d%E1%BB%A5ng-kh%C3%B3a-trong-b%E1%BA%A3ng-SQL-l%C3%A0-STT-hay-ID-sinh-s%E1%BA%B5n/) trong lập trình. Lí do quan trọng nhất vẫn là trên các hệ thống phân tán, có nhiều server độc lập nhau, mỗi server sẽ chạy độc lập thì việc sử dụng ID sinh sẵn sẽ không bảo đảm tính duy nhất, không trùng lặp của ID.

[Snowflake ID](https://developer.twitter.com/en/docs/basics/twitter-ids) chính là câu trả lời của các kĩ sư làm việc tại Twitter cho vấn đề trên. Theo thống kê, trên Twitter mỗi giây có khoảng 9000 tweet được viết và đăng tải. Làm sao để có thể sinh 9000 ID mỗi giây một cách độc lập trên nhiều server mà không trùng lặp? Chúng ta sẽ cùng tìm hiểu trong bài viết này.

### Khoan đã! Còn UUID thì sao?
UUID cũng là một kĩ thuật sinh ID rất phổ biến (có khi là phổ biến nhất (?)) và đã được sử dụng trong lĩnh vực phần mềm từ rất lâu.

Ý tưởng của kĩ thuật này là sử dụng một số 128 bit để làm ID. Số nguyên 128 bits nghĩa là, nếu mỗi giây chúng ta dùng 9000 IDs, thì chúng ta phải tốn hơn **1 tỷ tỷ tỷ** năm mới có thể dùng hết. Tất nhiên số này sẽ không tạo ra theo kiểu đếm tịnh tiến 1, 2, 3, ... mà nó sẽ được sinh theo một tiêu chuẩn nhất định.

Có hai chuẩn UUID phổ biến là UUID 1 và UUID 4.
- UUID 1 sẽ sinh chuỗi này dựa trên địa chỉ MAC và thời gian yêu cầu sinh ID
*Ví dụ 5 UUID được sinh cho cùng 1 máy, lưu ý đây là 32 số Hexa tương đương 128 bits*
![UUID sinh ID trên hệ quản trị cơ sở dữ liệu Snowflake ID](https://lh3.googleusercontent.com/oIg5_CuANXpwhDx01zVK7uWSbMXVl_N8IE3uvZW0WOWEq07w_huLCqUB3hywJikD1Swa75817PSIDEafA2J8hjlZB_n_h37OkHLynE0Yc9AYb_v1egGrF4F3cCEcovdd5OeHJfsa8A=w2400)
Các bạn sẽ dễ dàng nhận ra, cả 5 ID này nhìn tương tự nhau vì nó cùng dùng một MAC address để sinh.
- UUID 4 sẽ sinh chuỗi này dựa trên một số ngẫu nhiên. Sinh số ngẫu nhiên này tất nhiên không dùng hàm rand() như trong C rồi. Còn sinh như thế nào thì lại hẹn các bạn vào bài viết khác.
*Ví dụ 5 UUID được sinh cho cùng 1 máy*
![UUID sinh ID trên hệ quản trị cơ sở dữ liệu Snowflake ID](https://lh3.googleusercontent.com/C2yrDedJBu5aa9Rcfn_9OBTKxYyY_fqbBIkd_y09g3zuZL23L0NBNWGobYuSNQz6tNoDslBjggPr4SqpfLY2Jp62mohkGcjoG3IiYVJYIbmmjO2inEvwYIFpYeyHyIiodsHpl7jJig=w2400)

UUID nếu sinh đúng chuẩn sẽ giải quyết được vấn đề sinh trên hệ thống phân tán sẽ không gây ra hiện tượng trùng lắp. Tuy nhiên nó lại nảy sinh một vấn đề khác.

128 bits là quá lớn, lớn đến mức không cần thiết. Các cơ sở dữ liệu không có kiểu số 128 bits, thường thì chúng ta phải dùng dạng chuỗi để lưu trữ. 

### Snowflake ID
Để giải quyết vấn đề này, các kĩ sư tại Twitter giới thiệu một hệ thống gọi là Snowflake ID. Ý tưởng của hệ thống này là dùng một số nguyên 64 bits để lưu trữ ID. Nhưng làm sao để sinh ID này một cách độc lập mà không trùng lặp.

Phương pháp được đề xuất như sau:
- 41 bits đầu dùng để lưu thông tin về thời gian tạo ID. Tính bằng số milisecond tính từ một thời điểm nào đó (theo mình ước tính là khoảng 2006).
- 10 bits tiếp theo dùng để chứa thông tin về máy yêu cầu sinh ID
- 12 bits cuối cùng là bộ đếm tuần tự từ 1 đến 4096. Để tránh trường hợp lặp ID khi sinh cùng một máy, trong cùng khoảng thời gian.
![Snowflake ID Generate ID for database](https://lh3.googleusercontent.com/E1KU3dsvB2d0Z__qbGmy5lfpN1sakq8WoPI0ESEyHkV8YRhGtn2iP9XR6Pv3R62uAmxpwLauaZnXeYFbJhK_J6eMn0fbCdzLC5GvS1jFCRZGuJVydVyzEVCVhy1DPmGGTZbpDSCTag=w2400)

Với Snowflake ID, chúng ta đã giải quyết được vấn đề sinh ID không lặp trên hệ thống phân tán với một số 64 bits.

Bên cạnh đó, Snowflake ID còn có ưu điểm là bản thân ID chứa thông tin về thời gian, nên chỉ cần có ID, chúng ta có thể biết được thời gian sinh ID (thời gian tweet được đăng), hoặc sắp xếp theo ID cũng cho chúng ta kết quả sắp xếp theo thứ tự thời gian.

### Kết
Tuy dự án Snowflake ID đã bị Twitter hủy bỏ và thay bằng Twitter's server. Nhưng nó đã truyền cảm hứng cho việc sinh ID của nhiều hệ thống khác (như Instagram). Tất nhiên ngoài những chiến lược sinh ID kể trên, vẫn còn nhiều cách khác nữa (ví dụ Centralized ID server của Flickr). 
Thế mới thấy, để giải quyết một vấn đề, luôn có rất nhiều cách. Đừng nên tự trói buộc mình vào những cách đã có, mà phải luôn tìm tòi một cách làm mới, phù hợp với hoàn cảnh, yêu cầu của mình. Thay vì liệt kê một loạt hướng đi có sẵn để lựa chọn, sao không thử nghĩ xem liệu có hướng đi nào khác hay không?