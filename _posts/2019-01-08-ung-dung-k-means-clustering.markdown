---
layout: post
title:  "Bài 16: Ứng Dụng Thuật Toán K-Means Clustering"
description: "Trong bài này chúng ta sẽ ứng dụng thuật toán K-Means Clustering trong Machine Learning để phân cụm các mẫu rượu dựa trên các số đo cho trước."
---

Trong bài này, ta sẽ phân cụm các mẫu rượu bằng <a href="https://www.dathoangblog.com/2019/01/k-means-clustering.html">thuật toán K-Means Clustering</a> đã được học ở bài trước.

Kết quả cũng sẽ được so sánh với thực tế để đảm bảo thuật toán được cài đặt chính xác.
<!--more-->
<h3>
Đặt vấn đề</h3>
Bộ dữ liệu mà ta xét là một phần của kết quả phân tích các chất trong rượu. Bảng dưới đây chứa số đo etanol, acid malic, magnesium, phenol, độ đậm màu, sắc thái của các mẫu thuộc 1 trong 3 loại rượu.

<div class="separator" style="clear: both; text-align: center;">
<a href="https://2.bp.blogspot.com/-eX4KTX7KEG0/XDrw8ZqTyxI/AAAAAAAAESI/h8JMu4uOiHkB4UpyLm6qvahmP5DIR0D_ACLcBGAs/s1600/Untitled.jpg" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Bảng số đo các mẫu rượu" border="0" data-original-height="245" data-original-width="500" src="https://2.bp.blogspot.com/-eX4KTX7KEG0/XDrw8ZqTyxI/AAAAAAAAESI/h8JMu4uOiHkB4UpyLm6qvahmP5DIR0D_ACLcBGAs/s1600/Untitled.jpg" title="Bảng số đo các mẫu rượu" /></a></div>
<div class="separator" style="clear: both; text-align: center;">
</div>
<div class="separator" style="clear: both; text-align: center;">
</div>
<div class="separator" style="clear: both; text-align: center;">
</div>
<div class="separator" style="clear: both; text-align: center;">
</div>
<div class="separator" style="clear: both; text-align: center;">
</div>
<div class="separator" style="clear: both; text-align: center;">
</div>

Cột loại rượu chỉ có ý nghĩa tham khảo để đánh giá hiệu quả thuật toán. Do là bài toán nhóm Unsupervised Learning nên các mẫu dữ liệu không có output.

Ta sẽ dùng thuật toán K-Means Clustering để phân chia các mẫu dữ liệu thành 3 cụm.
<h3>
Giải quyết vấn đề</h3>
<h4>
Tự cài đặt thuật toán</h4>
Các bước cài đặt thuật toán

<strong>Bước 1:&nbsp;</strong>Chọn ngẫu nhiên 3 trong số 15 điểm dữ liệu làm trung tâm cụm $\mu_{1}, \mu_{2}, \mu_{3}$.

<strong>Bước 2:</strong>&nbsp;Gán mỗi điểm dữ liệu về cụm có trung tâm cụm gần nhất.

$c^{(i)} = argmin_{k} \lVert x^{(i)} - \mu_{k} \lVert^{2} $

<b>Bước 3:</b>&nbsp;Di chuyển các trung tâm cụm về vị trí trung bình của các điểm dữ liệu trong cụm tương ứng.

$\mu_{k} = \frac{1}{n}(x^{(k_{1})} + x^{(k_{2})} + ... + x^{(k_{n})})$

<b>Bước 4:</b>&nbsp;Lặp lại hai bước trên tới khi vị trí các trung tâm cụm không đổi sau một bước lặp nào đó.

<b>Bước 5:</b>&nbsp;Lặp lại tất cả các bước trên một số lần và chọn phương án có hàm mất mát nhỏ nhất.

$&nbsp;argmin_{c^{(1)}, ..., c^{(15)}, \mu_{1}, \mu_{2}, \mu_{3}}J(c^{(1)}, ..., c^{(15)}, \mu_{1}, \mu_{2}, \mu_{3})$

Mở trình soạn thảo yêu thích của bạn, tạo file&nbsp;<strong>bai16.html</strong>&nbsp;rồi dán vào đoạn code sau

<script src="https://gist.github.com/dathoangnd/4d47826df7ef63b57259544310b3e73f.js"></script>
Ta được kết quả

<i>Các mẫu rượu trong cùng nhóm là:</i>

<i>1 4 5 11</i>

<i>2 3 7 8 12 13 14</i>

<i>6 9 10 15</i>
 
Kết quả này là phù hợp với thực tế.
<h4>
Sử dụng hàm có sẵn</h4>
Các thư viện giúp chúng ta sử dụng K-Means Clustering một cách đơn giản và nhanh chóng.

<script src="https://gist.github.com/dathoangnd/1adc785b08eceae3cec47a0233eac95b.js"></script>
Ta cũng được kết quả

<i>Các mẫu rượu trong cùng nhóm là:</i>

<i>1 4 5 11</i>

<i>2 3 7 8 12 13 14</i>

<i>6 9 10 15</i>
<h3>
Giờ đến lượt bạn</h3>
Bạn hãy thử đổi một vài số liệu để quan sát sự thay đổi kết quả của thuật toán. Lưu ý trường hợp thay một giá trị bằng một số rất lớn hoặc rất nhỏ so với các giá trị khác.