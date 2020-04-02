---
layout: post
title:  "Bài 4: Ứng Dụng Thuật Toán Linear Regression Nhiều Biến"
description: "Cách ứng dụng thuật toán Linear Regression nhiều biến trong Machine Learning để dự đoán giá nhà dựa trên các thông tin cho trước."
---

Trong bài này, chúng ta sẽ ứng dụng <a href="https://www.dathoangblog.com/2018/07/linear-regression-nhieu-bien.html" rel="noopener" target="_blank">thuật toán Linear Regression nhiều biến</a> đã được học ở bài trước&nbsp;để giải một bài toán thực tế.

Qua bài này, chúng ta sẽ giải quyết triệt để bài toán dự đoán giá nhà đã được đặt ra từ bài <a href="https://www.dathoangblog.com/2018/07/machine-learning-la-gi.html" rel="noopener" target="_blank">giới thiệu Machine Learning</a>.
<!--more-->
<h3>
Đặt vấn đề</h3>
Giả sử giá nhà phụ thuộc vào các yếu tố: <strong>diện tích</strong>, <strong>số phòng</strong>, <strong>tuổi căn nhà</strong>, <strong>số bếp lửa</strong>. Các yếu tố trên chính là các biến của một input.

Dưới đây là các thông số cùng giá của 20 căn nhà

<div class="separator" style="clear: both; text-align: center;">
<a href="https://4.bp.blogspot.com/-M5nHaMHj1rM/W0V3WYqGWeI/AAAAAAAAD3I/R6L-WOiuJmEL77IgYUtbEl2saUpy6vE4gCLcBGAs/s1600/Untitled.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Ứng dụng thuật toán linear regression nhiều biến để tìm giá nhà" border="0" data-original-height="340" data-original-width="500" src="https://4.bp.blogspot.com/-M5nHaMHj1rM/W0V3WYqGWeI/AAAAAAAAD3I/R6L-WOiuJmEL77IgYUtbEl2saUpy6vE4gCLcBGAs/s1600/Untitled.png" title="Ứng dụng thuật toán linear regression nhiều biến để tìm giá nhà" /></a></div>



Ta cần dựa vào các dữ kiện trên để tìm ra mối liên hệ tuyến tính giữa giá nhà với các thông số của căn nhà. Từ đó ta có thể dự đoán giá của căn nhà bất kỳ.

$\widehat{y} =&nbsp;&nbsp;w_{0} + w_{1}x_{1} + w_{2}x_{2} +w_{3}x_{3} +w_{4}x_{4}$

với&nbsp;$\widehat{y}$ là giá dự đoán của căn nhà diện tích $x_{1}$, có&nbsp;$x_{2}$ phòng, đã xây dựng được $x_{3}$ năm và có&nbsp;$x_{4}$ bếp lửa.
<h3>
Giải quyết vấn đề</h3>
<h4>
Tự cài đặt thuật toán</h4>
Ta nhắc lại các bước cài đặt thuật toán đã trình bày ở bài trước.

<strong>Bước 1:&nbsp;</strong>Thiết lập các ma trận và vector

w = $\begin{bmatrix}w_{0} \\\\ w_{1} \\\\ ... \\\\ w_{n} \end{bmatrix} $

X = $\begin{bmatrix}1 &amp; 100 &amp; ... &amp; 0 \\\\ 1 &amp; 150 &amp; ... &amp; 0 \\\\ ... &amp; ... &amp; ... &amp; ... \\\\ 1 &amp; 150 &amp; ... &amp; 0 \end{bmatrix}$

y = $\begin{bmatrix}259 \\\\ 295 \\\\ ... \\\\ 439 \end{bmatrix}$

<strong>Bước 2:</strong>&nbsp;Tính vector w

$w = (X^{T}X)^{+}X^{T}y$

Mở trình soạn thảo yêu thích của bạn, tạo file <strong>bai4.html</strong>&nbsp;rồi dán vào đoạn code sau

<script src="https://gist.github.com/dathoangnd/6058aa0899f8d39ffeb8335f368d78b9.js"></script>

Ta được kết quả

<i>Giá căn nhà diện tích 159 mét vuông, 7 phòng, xây được 37 năm, không có bếp lửa là 390 nghìn đôla</i>

<i>Giá căn nhà diện tích 205 mét vuông, 10 phòng, xây được 20 năm, có 1 bếp lửa là 629 nghìn đôla</i>

<i>Giá căn nhà diện tích 110 mét vuông, 5 phòng, xây được 50 năm, không có bếp lửa là 229 nghìn đôla</i>
<h4>
Sử dụng hàm có sẵn</h4>
Việc sử dụng hàm Linear Regression nhiều biến được cài đặt sẵn trong thư viện <a href="https://github.com/mljs/ml" rel="noopener" target="_blank">ml.js</a> sẽ giúp code trông đơn giản đi rất nhiều.

Mã nguồn sử dụng hàm Linear Regression nhiều biến có sẵn

<script src="https://gist.github.com/dathoangnd/fb5119d3c46a3354a8bbdcf79e30361d.js"></script>

Ta được kết quả

<i>Giá căn nhà diện tích 159 mét vuông, 7 phòng, xây được 37 năm, không có bếp lửa là 390 nghìn đôla</i>

<i>Giá căn nhà diện tích 205 mét vuông, 10 phòng, xây được 20 năm, có 1 bếp lửa là 629 nghìn đôla</i>

<i>Giá căn nhà diện tích 110 mét vuông, 5 phòng, xây được 50 năm, không có bếp lửa là 229 nghìn đôla</i>

Kết quả này giống như ở trên. Điều đó cho thấy ta đã cài đặt thuật toán một cách chính xác.

<em><strong>Lưu ý:</strong>&nbsp;Khi sử dụng hàm có sẵn, cách thiết lập ma trận hơi khác so với khi ta tự cài đặt thuật toán. Bạn hãy tra cứu <a href="https://github.com/mljs/ml" rel="noopener" target="_blank">tài liệu của thư viện ml.js</a>&nbsp;để có thể biết cách sử dụng đúng các hàm của nó.&nbsp;</em>
<h3>
Giờ đến lượt bạn</h3>
Trong bài thực hành này, bạn đã được học cách sử dụng thuật toán Machine Learning để dự đoán giá nhà dựa trên nhiều thông số khác.

Với thuật toán Linear Regression, bạn có thể giải quyết được vô số vấn đề thực tế yêu cầu dự đoán thông tin nào đó dựa trên các thông tin có sẵn.

Bây giờ đến lượt bạn

Hãy sửa đổi dữ liệu đầu vào để quan sát sự thay đổi dự đoán giá nhà của thuật toán. Bạn cũng có thể thêm một vài dữ liệu nhiễu để xem ảnh hưởng của nó.

Bạn hãy tìm một bộ dữ liệu khác hoặc tự nghĩ ra một bộ dữ liệu có thể áp dụng thuật toán Linear Regression nhiều biến, sau đó tự mình cài đặt thuật toán với bộ dữ liệu mới này.