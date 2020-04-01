---
layout: post
title:  "Bài 12: Ứng Dụng Thuật Toán Support Vector Machine"
description: "Trong bài này chúng ta sẽ ứng dụng thuật toán Support Vector Machine trong Machine Learning để dự đoán tên loài hoa dựa trên các số đo cho trước."
---

Trong bài này, ta sẽ quay lại vấn đề dự đoán tên loài hoa đã được giải quyết trong bài <a href="https://www.dathoangblog.com/2019/01/ung-dung-logistic-regression.html">Ứng dụng thuật toán Logistic Regression</a>.

Thay vì sử dụng thuật toán Logistic Regression, ta sẽ sử dụng thuật toán Support Vector Machine bằng cách tự cài đặt và sử dụng hàm có sẵn trong thư viện.
<!--more-->
<h3>
Nhắc lại vấn đề</h3>
Xét bộ dữ liệu chứa số đo độ dài đài hoa, độ rộng đài hoa, độ dài cánh hoa, độ rộng cánh hoa tính bằng cm của 20 bông hoa thuộc chi Iris. Trong đó 10 bông hoa thuộc loài Iris setosa và 10 bông hoa thuộc loài&nbsp;Iris virginica.

<div class="separator" style="clear: both; text-align: center;">
<a href="https://1.bp.blogspot.com/-Txh-kp0uyss/XC7cIYkvvCI/AAAAAAAAENA/T9qyhFuZNokA1dPGuvyizdqcMUyIwfOmwCLcBGAs/s1600/Untitled.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Iris data set" border="0" data-original-height="396" data-original-width="500" src="https://1.bp.blogspot.com/-Txh-kp0uyss/XC7cIYkvvCI/AAAAAAAAENA/T9qyhFuZNokA1dPGuvyizdqcMUyIwfOmwCLcBGAs/s1600/Untitled.png" title="Iris data set" /></a></div>
<div class="separator" style="clear: both; text-align: center;">
</div>
<div class="separator" style="clear: both; text-align: center;">
</div>
<div class="separator" style="clear: both; text-align: center;">
</div>

Coi như output là Iris setosa ứng với giá trị 0, output là Iris virginica ứng với giá trị 1.

Ta cần tìm ra vector hệ số của Decision Boundary w =&nbsp;$\begin{bmatrix}w_{0} \\\\ w_{1} \\\\ w_{2} \\\\ w_{3} \\\\ w_{4} \end{bmatrix} $ sao cho với mỗi input mới x =&nbsp;$\begin{bmatrix}1 \\\\ x_{1} \\\\ x_{2} \\\\ x_{3} \\\\ x_{4} \end{bmatrix}$, ta có thể dự đoán được output

$\widehat{y} =&nbsp;\begin{cases}1 &amp; khi\ x^{T}w \geq 0\\\\0 &amp; khi\ x^{T}w &lt; 0\end{cases}$
<h3>
Giải quyết vấn đề</h3>
Để đơn giản ta sẽ không sử dụng kernel.
<h4>
Tự cài đặt thuật toán</h4>
Các bước cài đặt thuật toán

<strong>Bước 1:</strong>&nbsp;Chọn w = $\begin{bmatrix}0 \\\\ 0 \\\\ 0 \\\\ 0 \\\\ 0 \end{bmatrix} $ và các tham số α = 0.0003, C = 0.01, k = 1.

<strong>Bước 2:</strong>&nbsp;Liên tiếp lặp lại các phép biến đổi

$w_{0} := w_{0} - \alpha C \sum_{i=1}^{m} [y^{(i)}(x^{(i)T}w \geq 1\ ?\ 0:-k) + (1 - y^{(i)})(x^{(i)T}w \geq -1\ ?\ k:0)]$

$w_{1} := w_{1}(1 - \alpha) - \alpha C \sum_{i=1}^{m} [y^{(i)}(x^{(i)T}w \geq 1\ ?\ 0:-kx_{1}^{(i)}) + (1 - y^{(i)})(x^{(i)T}w \geq -1\ ?\ kx_{1}^{(i)}:0)]$

$w_{2} := w_{2}(1 - \alpha) - \alpha C \sum_{i=1}^{m} [y^{(i)}(x^{(i)T}w \geq 1\ ?\ 0:-kx_{2}^{(i)}) + (1 - y^{(i)})(x^{(i)T}w \geq -1\ ?\ kx_{2}^{(i)}:0)]$

$w_{3} := w_{3}(1 - \alpha) - \alpha C \sum_{i=1}^{m} [y^{(i)}(x^{(i)T}w \geq 1\ ?\ 0:-kx_{3}^{(i)}) + (1 - y^{(i)})(x^{(i)T}w \geq -1\ ?\ kx_{3}^{(i)}:0)]$

$w_{4} := w_{4}(1 - \alpha) - \alpha C \sum_{i=1}^{m} [y^{(i)}(x^{(i)T}w \geq 1\ ?\ 0:-kx_{4}^{(i)}) + (1 - y^{(i)})(x^{(i)T}w \geq -1\ ?\ kx_{4}^{(i)}:0)]$

<strong>Bước 3:</strong>&nbsp;Thuật toán dừng lại khi J(w) thay đổi rất nhỏ hoặc trị tuyệt đối các đạo hàm riêng rất nhỏ. Nếu thuật toán không thể kết thúc thì chọn giá trị&nbsp;α nhỏ hơn rồi quay lại bước 2.

Mở trình soạn thảo yêu thích của bạn, tạo file&nbsp;<strong>bai12.html</strong>&nbsp;rồi dán vào đoạn code sau

<script src="https://gist.github.com/dathoangnd/bcbfe16f987e5adad8a4574af564b740.js"></script>

Ta được kết quả

<i>Bông hoa có độ dài đài hoa 5 cm, độ rộng đài hoa 3.3 cm, độ dài cánh hoa 1.4 cm, độ rộng cánh hoa 0.2 cm là Iris setosa.

Bông hoa có độ dài đài hoa 5.7 cm, độ rộng đài hoa 2.8 cm, độ dài cánh hoa 4.1 cm, độ rộng cánh hoa 1.3 cm là Iris virginica.

Bông hoa có độ dài đài hoa 5.9 cm, độ rộng đài hoa 3 cm, độ dài cánh hoa 5.1 cm, độ rộng cánh hoa 1.8 cm là Iris virginica.</i>
<h4>
Sử dụng hàm có sẵn</h4>
Các thư viện cài đặt Support Vector Machine thường áp dụng nhiều phương pháp tối ưu giúp thuật toán chạy nhanh hơn.

<script src="https://gist.github.com/dathoangnd/cf1a3632392f2650202306a4768035d3.js"></script>
Ta cũng được kết quả

<i>Bông hoa có độ dài đài hoa 5 cm, độ rộng đài hoa 3.3 cm, độ dài cánh hoa 1.4 cm, độ rộng cánh hoa 0.2 cm là Iris setosa.

Bông hoa có độ dài đài hoa 5.7 cm, độ rộng đài hoa 2.8 cm, độ dài cánh hoa 4.1 cm, độ rộng cánh hoa 1.3 cm là Iris virginica.

Bông hoa có độ dài đài hoa 5.9 cm, độ rộng đài hoa 3 cm, độ dài cánh hoa 5.1 cm, độ rộng cánh hoa 1.8 cm là Iris virginica.</i></div>
<h3>
Giờ đến lượt bạn</h3>
Hãy sử dụng hàm có sẵn để giải quyết bài toán với&nbsp;<a href="https://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data" target="_blank">bộ dữ liệu Iris flower data set</a>&nbsp;đầy đủ gồm 3 lớp và 150 mẫu dữ liệu bằng thuật toán Support Vector Machine.