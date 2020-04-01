---
layout: post
title:  "Bài 20: Ứng Dụng Thuật Toán Collaborative Filtering"
description: "Trong bài này chúng ta sẽ ứng dụng thuật toán Collaborative Filtering trong Machine Learning dự đoán bộ phim người dùng có thể quan tâm."
---

Trong bài này, ta sẽ dự đoán bộ phim người dùng có thể quan tâm thông qua các đánh giá trước đó bằng thuật toán Collaborative Filtering.

Đây là bài toán rất quan trọng và thường gặp trong thực tế.
<!--more-->
<h3>
Đặt vấn đề</h3>
Một website xem phim trực tuyến nhỏ có 5 người dùng và 5 bộ phim. Mỗi người dùng có thể đánh giá các bộ phim từ 1 tới 5 sao. Dưới đây là dữ liệu đánh giá của người dùng.

<div class="separator" style="clear: both; text-align: center;">
<a href="https://3.bp.blogspot.com/-I7Piur2wJ6k/XDzCprHEyCI/AAAAAAAAEUc/n1rhjvp5DAEm0HM3OcPeHqA6WJQ0YZ6lgCLcBGAs/s1600/Untitled.jpg" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Đánh giá phim" border="0" data-original-height="135" data-original-width="500" src="https://3.bp.blogspot.com/-I7Piur2wJ6k/XDzCprHEyCI/AAAAAAAAEUc/n1rhjvp5DAEm0HM3OcPeHqA6WJQ0YZ6lgCLcBGAs/s1600/Untitled.jpg" title="Đánh giá phim" /></a></div>
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
<div class="separator" style="clear: both; text-align: center;">
</div>
<div class="separator" style="clear: both; text-align: center;">
</div>
<div class="separator" style="clear: both; text-align: center;">
</div>

Ta cần cài đặt thuật toán Collaborative Filtering để dự đoán thứ tự các bộ phim yêu thích của từng người dùng.
<h3>
Giải quyết vấn đề</h3>
Nhận thấy không có người dùng nào mà chưa đánh giá bất cứ bộ phim nào nên ta có thể bỏ qua bình thường hóa dữ liệu. Để đơn giản ta cũng sẽ không áp dụng chính quy hóa dữ liệu. Các bước cài đặt thuật toán

<strong>Bước 1:<span style="font-weight: 400;">&nbsp;</span></strong>&nbsp;Chọn n = 2, α = 0.03 và khởi tạo&nbsp;các giá trị&nbsp;&nbsp;$w^{(1)}, w^{(2)}, ..., w^{(5)}, x^{(1)}, x^{(2)}, ..., x^{(5)}$ ngẫu nhiên.

<strong>Bước 2:</strong>&nbsp;Liên tiếp lặp lại các phép biến đổi

<i>$w_{k}^{(i)} := w_{k}^{(i)} - \alpha \sum_{j:r(i,j)=1}(x^{(j)T}w^{(i)} - Y_{ij})x_{k}^{(j)}$</i>

<i>$x_{k}^{(j)} := x_{k}^{(j)} - \alpha \sum_{i:r(i,j)=1}(x^{(j)T}w^{(i)} - Y_{ij})w_{k}^{(i)}$</i>

<strong>Bước 3:</strong>&nbsp;Thuật toán dừng lại khi J thay đổi rất nhỏ hoặc trị tuyệt đối các đạo hàm riêng rất nhỏ. Nếu thuật toán không thể kết thúc thì chọn giá trị&nbsp;α nhỏ hơn rồi quay lại bước 2.

Mở trình soạn thảo yêu thích của bạn, tạo file&nbsp;<strong>bai20.html</strong>&nbsp;rồi dán vào đoạn code sau

<script src="https://gist.github.com/dathoangnd/d6cae261a2ba47fd2384c396fc755bc0.js"></script>
Ta có thể được kết quả

<i>Bộ phim gợi ý cho từng người là:</i>

<i>Người 1: Vùng đất linh hồn</i>

<i>Người 2: Vua sư tử</i>

<i>Người 3: Vùng đất linh hồn</i>

<i>Người 4: Kỵ sĩ bóng đêm</i>

<i>Người 5: Kỵ sĩ bóng đêm</i>
<h3>
Giờ đến lượt bạn</h3>
Mỗi lần chạy lại chương trình, ta có thể nhận được kết quả khác nhau. Theo bạn, tại sao lại có sự thay đổi đó?