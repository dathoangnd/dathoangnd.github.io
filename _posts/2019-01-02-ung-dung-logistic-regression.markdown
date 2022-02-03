---
tag: learn
layout: post
title:  "Bài 10: Ứng Dụng Thuật Toán Logistic Regression"
description: "Trong bài này chúng ta sẽ ứng dụng thuật toán Logistic Regression trong Machine Learning để dự đoán tên loài hoa dựa trên các số đo cho trước."
---

Trong tự nhiên, nhiều loài có họ hàng gần với nhau lập thành một chi với các đặc điểm hình thái tương tự nhau nhưng vẫn có một số điểm khác biệt.

Bài thực hành này sẽ sử dụng <a href="https://www.dathoangblog.com/2019/01/logistic-regression.html">thuật toán Logistic Regression</a> đã được học ở bài trước để dự đoán tên loài hoa trong một chi dựa vào các đặc điểm hình thái cho trước.
<!--more-->
<h3>
Đặt vấn đề</h3>
Bộ dữ liệu <a href="https://en.wikipedia.org/wiki/Iris_flower_data_set" target="_blank">Iris flower data set</a>&nbsp;là bộ dữ liệu rất nổi tiếng trong nghiên cứu Machine Learning, được công bố bởi <a href="https://en.wikipedia.org/wiki/Ronald_Fisher" target="_blank">Ronald Fisher</a>&nbsp;vào năm 1936.

Bộ dữ liệu chứa số đo độ dài đài hoa, độ rộng đài hoa, độ dài cánh hoa, độ rộng cánh hoa tính bằng cm của 150 bông hoa thuộc chi Iris. Trong đó 50 bông hoa thuộc loài Iris setosa, 50 bông hoa thuộc loài&nbsp;Iris virginica và 50 bông hoa thuộc loài&nbsp;Iris versicolor.

Trong bài này, để đơn giản ta sẽ chỉ xét bài toán với một phần của bộ dữ liệu Iris với 2 loài Iris setosa và Iris virginica, mỗi loài lấy 10 mẫu dữ liệu.

<div class="separator" style="clear: both; text-align: center;">
<a href="https://1.bp.blogspot.com/-Txh-kp0uyss/XC7cIYkvvCI/AAAAAAAAENA/T9qyhFuZNokA1dPGuvyizdqcMUyIwfOmwCLcBGAs/s1600/Untitled.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Iris data set" border="0" data-original-height="396" data-original-width="500" src="https://1.bp.blogspot.com/-Txh-kp0uyss/XC7cIYkvvCI/AAAAAAAAENA/T9qyhFuZNokA1dPGuvyizdqcMUyIwfOmwCLcBGAs/s1600/Untitled.png" title="Iris data set" /></a></div>
<div class="separator" style="clear: both; text-align: center;">
</div>
<div class="separator" style="clear: both; text-align: center;">
</div>
<div class="separator" style="clear: both; text-align: center;">
</div>

Coi như output là Iris setosa ứng với giá trị 0, output là Iris virginica ứng với giá trị 1.

Ta cần tìm ra vector hệ số của Decision Boundary w =&nbsp;$\begin{bmatrix}w_{0} \\\\ w_{1} \\\\ w_{2} \\\\ w_{3} \\\\ w_{4} \end{bmatrix} $ sao cho với mỗi input mới x =&nbsp;$\begin{bmatrix}1 \\\\ x_{1} \\\\ x_{2} \\\\ x_{3} \\\\ x_{4} \end{bmatrix}$, ta có thể dự đoán được xác suất để output bằng 1

$\widehat{y} = \frac{1}{1 + e^{-x^{T}w}}$
<h3>
Giải quyết vấn đề</h3>
Để đơn giản ta sẽ không thực hiện chính quy hóa dữ liệu. Các bước cài đặt thuật toán

<strong>Bước 1:</strong>&nbsp;Chọn w = $\begin{bmatrix}0 \\\\ 0 \\\\ 0 \\\\ 0 \\\\ 0 \end{bmatrix} $&nbsp;và α = 0.0003.

<strong>Bước 2:</strong>&nbsp;Liên tiếp lặp lại các phép biến đổi

$w_{0} := w_{0} - \alpha \frac{1}{m} \sum_{i=1}^{m} ( \widehat{y}^{(i)} - y^{(i)})$

$w_{1} := w_{1} - \alpha \frac{1}{m} \sum_{i=1}^{m} (( \widehat{y}^{(i)} - y^{(i)})x^{(i)}_{1})$

$w_{2} := w_{2} - \alpha \frac{1}{m} \sum_{i=1}^{m} (( \widehat{y}^{(i)} - y^{(i)})x^{(i)}_{2})$

$w_{3} := w_{3} - \alpha \frac{1}{m} \sum_{i=1}^{m} (( \widehat{y}^{(i)} - y^{(i)})x^{(i)}_{3})$

$w_{4} := w_{4} - \alpha \frac{1}{m} \sum_{i=1}^{m} (( \widehat{y}^{(i)} - y^{(i)})x^{(i)}_{4})$

Hoặc viết ngắn gọn

$w = w - \alpha \frac{1}{m} X^{T}(\widehat{y} - y)$

<strong>Bước 3:</strong>&nbsp;Thuật toán dừng lại khi J(w) thay đổi rất nhỏ hoặc trị tuyệt đối các đạo hàm riêng rất nhỏ. Nếu thuật toán không thể kết thúc thì chọn giá trị&nbsp;α nhỏ hơn rồi quay lại bước 2

Mở trình soạn thảo yêu thích của bạn, tạo file&nbsp;<strong>bai10.html</strong>&nbsp;rồi dán vào đoạn code sau

<script src="https://gist.github.com/dathoangnd/0ac85bb2eb494bfcc5dc34a8eee77e00.js"></script>
Ta được kết quả

<i>Bông hoa có độ dài đài hoa 5 cm, độ rộng đài hoa 3.3 cm, độ dài cánh hoa 1.4 cm, độ rộng cánh hoa 0.2 cm là Iris setosa.

Bông hoa có độ dài đài hoa 5.7 cm, độ rộng đài hoa 2.8 cm, độ dài cánh hoa 4.1 cm, độ rộng cánh hoa 1.3 cm là Iris virginica.

Bông hoa có độ dài đài hoa 5.9 cm, độ rộng đài hoa 3 cm, độ dài cánh hoa 5.1 cm, độ rộng cánh hoa 1.8 cm là Iris virginica.</i>
<h3>
Giờ đến lượt bạn</h3>
Chúc mừng bạn đã cài đặt thành công thuật toán loại Classification đầu tiên.

Bạn hãy thử sửa đổi chương trình trên sao cho kết quả hiển thị xác suất một bông hoa là Iris setosa hay Iris virginica thay vì hiển thị dự đoán.

Hãy cài đặt thuật toán với <a href="https://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data" target="_blank">bộ dữ liệu Iris flower data set</a> đầy đủ gồm 3 lớp và 150 mẫu dữ liệu. Theo bạn, những khó khăn khi thực hiện là gì?