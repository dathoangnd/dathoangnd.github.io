---
tag: learn
layout: post
title:  "Bài 14: Ứng Dụng Thuật Toán Neural Network"
description: "Trong bài này chúng ta sẽ ứng dụng thuật toán Neural Network trong Machine Learning để dự đoán tên loài hoa dựa trên các số đo cho trước."
---

Trong bài này, ta sẽ giải quyết bài toán dự đoán bông hoa thuộc loài nào trong 3 loài của chi Iris.

Ta sẽ sử dụng thuật toán Neural Network - một thuật toán mạnh mẽ và có khả năng giải các bài toán phân loại đa lớp hiệu quả.
<!--more-->
<h3>
&nbsp;Nhắc lại vấn đề</h3>
Ta mở rộng bộ dữ liệu hoa Iris của các bài trước lên thành phân loại 3 lớp.

Xét bộ dữ liệu chứa số đo độ dài đài hoa, độ rộng đài hoa, độ dài cánh hoa, độ rộng cánh hoa tính bằng cm của 30 bông hoa thuộc chi Iris. Trong đó 10 bông hoa thuộc loài Iris setosa, 10 bông thuộc loài Iris versicolor và 10 bông thuộc loài&nbsp;Iris virginica.

<div class="separator" style="clear: both; text-align: center;">
<a href="https://4.bp.blogspot.com/-KvQhXapjd7M/XDg5cdzdD1I/AAAAAAAAEQk/sWV69toMhvg5rqpu7yyLCjF5F1b0BtKSgCLcBGAs/s1600/Untitled.jpg" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Bộ dữ liệu hoa Iris" border="0" data-original-height="577" data-original-width="500" src="https://4.bp.blogspot.com/-KvQhXapjd7M/XDg5cdzdD1I/AAAAAAAAEQk/sWV69toMhvg5rqpu7yyLCjF5F1b0BtKSgCLcBGAs/s1600/Untitled.jpg" title="Bộ dữ liệu hoa Iris" /></a></div>
<div class="separator" style="clear: both; text-align: center;">
</div>
<div class="separator" style="clear: both; text-align: center;">
</div>
<div class="separator" style="clear: both; text-align: center;">
</div>
<div class="separator" style="clear: both; text-align: center;">
</div>

Coi output là Iris setosa ứng với $\begin{bmatrix}1 \\\\ 0 \\\\ 0 \end{bmatrix}$, output là Iris versicolor ứng với $\begin{bmatrix}0 \\\\ 1 \\\\ 0 \end{bmatrix}$, output là Iris virginica ứng với $\begin{bmatrix}0 \\\\ 0 \\\\ 1 \end{bmatrix}$.

Ta cần tìm ra các hệ số&nbsp;&nbsp;$W_{pq}^{(l)}$ của mô hình mạng neuron đã chọn sao cho với mỗi input mới x =&nbsp;$\begin{bmatrix}1 \\\\ x_{1} \\\\ x_{2} \\\\ x_{3} \\\\ x_{4} \end{bmatrix}$, ta có thể dự đoán được output.
<h3>
Giải quyết vấn đề</h3>
Để đơn giản ta sẽ không thực hiện chính quy hóa dữ liệu.

Ta chọn mô hình mạng neuron có lớp input gồm 4 nút, 1 lớp ẩn gồm 4 nút và lớp output gồm 3 nút.
<h4>
Tự cài đặt thuật toán</h4>
Các bước cài đặt thuật toán

<strong>Bước 1:</strong>&nbsp;Chọn các giá trị $W^{(l)}_{pq}$ ngẫu nhiên và một giá trị learning rate α.

<strong>Bước 2:</strong>&nbsp;Liên tiếp lặp lại các phép biến đổi

$W_{pq}^{(l)}&nbsp;:= W_{pq}^{(l)} - \alpha J_{W_{pq}^{(l)}}'(W)$

với các đạo hàm riêng $J_{W_{pq}^{(l)}}'(W)$ được tính bằng thuật toán&nbsp;Backpropagation.

<strong>Bước 3:</strong>&nbsp;Thuật toán dừng lại khi J(w) thay đổi rất nhỏ hoặc trị tuyệt đối các đạo hàm riêng rất nhỏ. Nếu thuật toán không thể kết thúc thì chọn giá trị&nbsp;α nhỏ hơn rồi quay lại bước 2.

Mở trình soạn thảo yêu thích của bạn, tạo file&nbsp;<strong>bai14.html</strong>&nbsp;rồi dán vào đoạn code sau

<script src="https://gist.github.com/dathoangnd/746faae3e3fbd40bb03eba6d72567ae7.js"></script>
Ta được kết quả

<i>Bông hoa có độ dài đài hoa 5 cm, độ rộng đài hoa 3.3 cm, độ dài cánh hoa 1.4 cm, độ rộng cánh hoa 0.2 cm là Iris setosa.</i>

<i>Bông hoa có độ dài đài hoa 5.7 cm, độ rộng đài hoa 2.8 cm, độ dài cánh hoa 4.1 cm, độ rộng cánh hoa 1.3 cm là Iris versicolor.</i>

<i>Bông hoa có độ dài đài hoa 5.9 cm, độ rộng đài hoa 3 cm, độ dài cánh hoa 5.1 cm, độ rộng cánh hoa 1.8 cm là Iris virginica.</i>
<h4>
Sử dụng hàm có sẵn</h4>
Dùng hàm có sẵn là cách đơn giản hơn để sử dụng Neural Network.

<script src="https://gist.github.com/dathoangnd/46617a63730a297f719f5246a7a651ff.js"></script>
Ta cũng được kết quả

<i>Bông hoa có độ dài đài hoa 5 cm, độ rộng đài hoa 3.3 cm, độ dài cánh hoa 1.4 cm, độ rộng cánh hoa 0.2 cm là Iris setosa.</i>

<i>Bông hoa có độ dài đài hoa 5.7 cm, độ rộng đài hoa 2.8 cm, độ dài cánh hoa 4.1 cm, độ rộng cánh hoa 1.3 cm là Iris versicolor.</i>

<i>Bông hoa có độ dài đài hoa 5.9 cm, độ rộng đài hoa 3 cm, độ dài cánh hoa 5.1 cm, độ rộng cánh hoa 1.8 cm là Iris virginica.</i>
<h3>
Giờ đến lượt bạn</h3>
Hãy sử dụng hàm có sẵn để giải quyết bài toán với&nbsp;<a href="https://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data" target="_blank">bộ dữ liệu Iris flower data set</a>&nbsp;đầy đủ gồm 3 lớp và 150 mẫu dữ liệu bằng thuật toán Neural Network.