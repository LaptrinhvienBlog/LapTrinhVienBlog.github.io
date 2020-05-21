---
layout: post
title: Một bài Project Euler P1 Multiples of 3 and 5
summary: Trong thời gian rảnh rỗi, làm lập trình viên như mình để nâng cao khả năng, củng cố kĩ năng ngoài làm một vài side project hay ho thì cũng có thể làm mấy bài thuật toán như thế này hay phết. Vừa luyện được tư duy, vừa rèn kĩ năng giải quyết vấn đề, lựa chọn giải pháp. Bài toán của kì này chính là Project Euler #1 Multiples of 3 and 5.
Bên cạnh đó, qua bài này mình cũng muốn rút ra quan điểm của mình về một vấn đề cũng gây tranh cãi rất nhiều trong ngành lập trình. Lập trình viên có cần phải biết làm toán hay không?
date: 2020-05-21 14:08
categories: Programming Algorithm
---

Câu chuyện về một ngày nọ anh lập trình viên rảnh rỗi và quyết định giải trí bằng hackerrank.

## Đề:

If we list all the natural numbers below 10 that are multiples of
3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.
Find the sum of all the multiples of  **_3_**  or  **_5_**  below a given number  **_N._**

**Input Format:**

First line contains  **_T_**, the number of test cases. followed by  **_T_**  lines each containing an integer  **_N_**.

**Constraints:**
_1 ≤ T ≤ 10^5._
_1 ≤ N ≤ 10^9._

**Tạm dịch**
Nếu chúng ta liệt kê mọi số tự nhiên nhỏ hơn 10 và là bội số của 3 hoặc 5, chúng ta có 3, 5, 6, 9. Tổng của các số này là 23.
Tìm tổng các số là bội số của **3** hoặc **5** và nhỏ hơn **N**

[Đề gốc](https://www.hackerrank.com/contests/projecteuler/challenges/euler001/problem)

## Thực
Bài này là bài đầu tiên của Project Euler và là một bài dễ. Mình không gặp quá nhiều khó khăn khi giải bài toán này và rất may mắn là pass trong lần chạy đầu tiên. Trong bài viết này mình sẽ không chỉ nêu ra cách giải mà còn sẽ đi sâu phân tích các hướng đi cho bài toán.

    Các bạn nên thử tự làm trước khi đọc xuống dưới.

## Luận
### Đơn giản là vét cạn
Đây là hướng đi đầu tiên mà nhiều bạn sẽ nghĩ đến. Cách vét cạn thì quá dễ dàng rồi nên mình không bàn luận gì thêm.

Code C++: 
```c++
#include <iostream>
using namespace std;

long int SumMultiple35(int n);

int main() 
{
    int t;
    cin >> t;
    for (int i = 0; i < t; i++) 
    {
        int n;
        cin >> n;
        cout << SumMultiple35(n) << endl;
    }
    return 0;
}
```
Và hàm ```SumMultiple35``` chúng ta viết như sau:
Code C++
```c++
long int SumMultiple35(int n)
{
    long int sum = 0;
    for (int i = 1; i < n; i++)
    {
        if (i % 3 == 0 || i % 5 == 0)
        {
            sum += i;
        }
    }

    return sum;
}
```
 Cần lưu ý kiểu trả về là ```long int``` vì miền giá trị _1 ≤ N ≤ 10^9._ thì tổng các số thoản mãn có thể rất lớn.
 Chạy thử trên hacker rank:
 ![Hackerrank lập trình viên blog lập trình thuật toán multiples of 3 and 5](https://lh3.googleusercontent.com/f2vqHf_WNXcHZH8NfPFWvfOW14zMmoTNWnFI-J9k6hsb9em6IGTSLT-RbU5JqKwdQFUVXAyo4lejwYkMIOG94S9n0WnK7br5q2SoFdEefwj1mXtxblgfEFYkGfwbtSlMo9YzqsK25A=w2400)
 
 Như đã thấy, thuật toán vét cạn cho ra kết quả đúng, nhưng với độ phức tạp  bộ dữ liệu N lớn và T lớn thời gian thực thi không tối ưu.

### Dynamic programming aka Quy hoạch động?
Sau khi dùng xong hướng vét cạn, mình chợt nảy ra suy nghĩ về việc dùng quy hoạch động giải quyết bài toán này.

Ta có `SumMultiple35(1 -> n)` = `SumMultiple35(1 -> k)`+ `SumMultiple35(k -> n)`

Như vậy nếu ta có thể lưu các kết quả đã tính toán được vào bộ nhớ. Mỗi khi tính một giá trị `n` mới, chúng ta chỉ cần tính từ giá trị `k` lớn nhất nhỏ hơn `n` đã lưu trong mảng chứ không cần tính lại từ đầu.

Tuy nhiên mình sẽ không thử cách này vì tự thấy cách làm này có nhiều vấn đề:

 - Để tìm giá trị `k` lớn nhất nhỏ hơn `n` chúng ta lại cần một bước tìm kiếm. Điều này lại làm tăng số lượng vòng lặp.
 - Quy hoạch động bản chất vẫn phải tính từ đầu một số giá trị nhất định. Và nếu giá trí phải tính từ đầu đó là 10^9 thì việc dùng quy hoạch động không có nhiều ý nghĩa.
 
Vì những lý do đó, mình sẽ bỏ qua quy hoạch động.

### Thuật toán sinh: generation method

Ngồi lại một chút, cùng phân tích đề. Ta thấy đề yêu cầu tìm tổng của những số là bội của 3 và 5.
Nếu ta gọi S3 là tổng của các số là bội của 3 nhỏ hơn N

```
S3 = 3*0 + 3*1 + 3*2 + ... + 3*k với 3*k < N, k lớn nhất
```

Và S5 là tổng của các số là bội của 5 nhỏ hơn N
```
S5 = 5*0 + 5*1 + 5*2 + ... + 5*t với 5*t < n, t lớn nhất
```
Mấu chốt là ở đây. Thay vì lặp qua tất cả các số và kiểm tra xem số đó có thỏa mãn hay không. Chúng ta sẽ tự sinh ra những số thỏa mãn có dạng `3k` và `5t` rồi cộng lại với nhau.

Tuy nhiên có chút vấn đề. Nếu có số `3k` và `5t` nào trùng nhau thì chúng ta sẽ cộng số đó đến 2 lần. Có nhiều cách để giải quyết vấn đề này, nhưng cách đơn giản nhất là tìm ra những số đó và trừ đi. Vì đã được cộng đến 2 lần nên khi trừ đi thì sẽ cho ra kết quả chính xác.

Những số đó vừa chia hết cho 3 (có dạng `3k`) và vừa chia hết cho 5 (có dạng `5t`) nên nó cũng chia hết cho bội chung nhỏ nhất của 3 và 5 là 15. Vậy số đó có dạng là `15u`
```
S15 = 15*0 + 15*1 + 15*2 + ... + 15*u với 15*u < N, u lớn nhất
```

Vây kết quả của bài toán sẽ là:
```
S3 + S5 - S15
```

Hàm `SumMultiple35` viết lại như sau:
```c++
long int SumMultiple(int num, int limit)
{
    long int sum = 0;
    int i = 0;
    while (num * i < limit)
    {
        sum += num * i;
        i++;
    }
    return sum;
}


long int SumMultiple35(int n)
{
    return SumMultiple(3, n) + SumMultiple(5, n) - SumMultiple(15, n);
}
```

Và đây là kết quả
![Hackerrank lập trình viên blog lập trình thuật toán multiples of 3 and 5](https://lh3.googleusercontent.com/f2vqHf_WNXcHZH8NfPFWvfOW14zMmoTNWnFI-J9k6hsb9em6IGTSLT-RbU5JqKwdQFUVXAyo4lejwYkMIOG94S9n0WnK7br5q2SoFdEefwj1mXtxblgfEFYkGfwbtSlMo9YzqsK25A=w2400)
Mặc dù chúng ta đã cải thiện bằng cách dùng thuận toán sinh để bỏ qua những số không là bội của 3 hoặc 5 nhưng vẫn chưa thể vượt qua được.

### Sự kì diệu của toán học
Đánh giá lại hai cách ở trên, vét cạn có độ phức tạp *O(T x N)* và cách sinh cũng có độ phức tạp là *O(T x N)* . Điều này có nghĩa là ở T và N đủ lớn thì những ưu thế của thuật toán sinh sẽ không còn rõ ràng nữa.

Vậy liệu có cách nào để giải tối ưu bài toán này.

Câu trả lời là toán học.

Nhìn lại công thức của thuật toán sinh.
```
S3 + S5 - S15
```
Với
```
S3 = 3*0 + 3*1 + 3*2 + ... + 3*k với 3*k < N, k lớn nhất
S5 = 5*0 + 5*1 + 5*2 + ... + 5*t với 5*t < N, t lớn nhất
S15 = 15*0 + 15*1 + 15*2 + ... + 15*u với 15*u < N, u lớn nhất
```
Ta có thể biến đổi như sau:
```
S3 = 3 * (0 + 1 + 2 + ... + k) với 3*k < N, k lớn nhất
S5 = 5 * (0 + 1 + 2 + ... + t) với 5*t < N, t lớn nhất
S15 = 15 * (0 + 1 + 2 + ... + u) với 15*u < N, u lớn nhất
```
Mà ta có công thức cho chuỗi
```
0 + 1 + 2 + ... + n = n * (n + 1) / 2
```

Công thức này khá là quen thuộc với nhiều bạn và có nhiều cách chứng minh khác nhau, mình không trình bày chứng minh ở đây.
Như vậy, ta có:
```
S3 = 3 * k * (k + 1) / 2 với 3*k < N, k lớn nhất
S5 = 5 * t * (t + 1) / 2 với 5*t < N, t lớn nhất
S15 = 15 * u * (u + 1) / 2 với 15*u < N, u lớn nhất
```
Bài toán đến đây đã khá dễ dàng. Chỉ còn một vấn đề duy nhất. Tìm `k`, `t`, `u` sao cho ```3k, 5t, 15u < N```

Cách đơn giản nhất chính là lấy N chia nguyên cho 3, 5 và 15. Nhưng nếu lấy ```k = N div 3``` thì ```3k <= N```. Nên để đảm bảo điều kiện  ```3k < N (k lớn nhất)``` thì chúng ta sẽ lấy ```k = (N - 1) div 3```. Tương tự với 5 và 15.

Hàm `SumMultiple` viết lại như sau:

```c++
long int SumMultiple(int num, int limit)
{
    long int t = (limit - 1) / num;
    return num * t * (t + 1) / 2;
}


long int SumMultiple35(int n)
{
    return SumMultiple(3, n) + SumMultiple(5, n) - SumMultiple(15, n);
}

```
Và đây cũng là bài giải cuối cùng của mình. Kết quả chạy trên Hacker Rank
![Hackerrank lập trình viên thuật toán multiples of 3 and 5 project euler c++](https://lh3.googleusercontent.com/rngoiSfc2WQ7KeIAWk26Dsaz7-_COK4hKhr3hWCbrG7enRx8ljdtzJGAXBf0_WevpzY7-C1GbPz1yoNZgihva-L1H3qxct0lK9JbT1ObUl0TsPHPUYL0QZigkq2r06B1c44TJncv2Q=w2400)

## Kết
Trong thời gian rảnh rỗi, làm lập trình viên như mình để nâng cao khả năng, củng cố kĩ năng ngoài làm một vài side project hay ho thì cũng có thể làm mấy bài thuật toán như thế này hay phết. Vừa luyện được tư duy, vừa rèn kĩ năng giải quyết vấn đề, lựa chọn giải pháp.

Bên cạnh đó, qua bài này mình cũng muốn rút ra quan điểm của mình về một vấn đề cũng gây tranh cãi rất nhiều trong ngành lập trình. Lập trình viên có cần phải biết làm toán hay không?

> **Toán không bắt buộc, nhưng biết toán là một lợi thế.**


