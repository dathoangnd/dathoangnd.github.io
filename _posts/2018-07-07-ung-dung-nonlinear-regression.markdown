---
layout: post
title:  "Bài 6: Ứng Dụng Thuật Toán Nonlinear Regression"
description: "Trong bài này chúng ta sẽ ứng dụng thuật toán Nonlinear Regression trong Machine Learning để dự đoán số giờ sử dụng Internet trong từng tháng."
---

Trong bài này, chúng ta sẽ ứng dụng <a href="https://www.dathoangblog.com/2018/07/nonlinear-regression.html" rel="noopener" target="_blank">thuật toán Nonlinear Regression</a> đã được học ở bài trước&nbsp;để giải một bài toán thực tế.

Do thuật toán Nonlinear Regression được quy về <a href="https://www.dathoangblog.com/2018/07/linear-regression-nhieu-bien.html" rel="noopener" target="_blank">thuật toán Linear Regression</a> nên cách triển khai thuật toán rất giống như bài <a href="https://www.dathoangblog.com/2018/07/ung-dung-linear-regression-nhieu-bien.html" rel="noopener" target="_blank">ứng dụng thuật toán Linear Regression</a>.
<!--more-->
<h3>
Đặt vấn đề</h3>
Trong một nghiên cứu, người ta chọn ra ngẫu nhiên 5 người chưa từng sử dụng Internet trước đây và cung cấp miễn phí Internet cho họ sử dụng trong vòng 6 tháng.

Dưới đây là số giờ sử dụng Internet hàng tháng của mỗi người được ghi lại

<div class="separator" style="clear: both; text-align: center;">
<a href="https://3.bp.blogspot.com/-AP9DMe1uFIU/W0V8VRa7MVI/AAAAAAAAD4A/0QNnVNkcg08xULd1HYDNnV1ZwsWXc6odACLcBGAs/s1600/Untitled-1.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Số giờ sử dụng Internet" border="0" data-original-height="160" data-original-width="500" src="https://3.bp.blogspot.com/-AP9DMe1uFIU/W0V8VRa7MVI/AAAAAAAAD4A/0QNnVNkcg08xULd1HYDNnV1ZwsWXc6odACLcBGAs/s1600/Untitled-1.png" title="Số giờ sử dụng Internet" /></a></div>

Nhiệm vụ của ta là tìm ra mối liên hệ giữa số tháng với số giờ sử dụng Internet để có thể dự đoán số giờ sử dụng Internet ở tháng bất kỳ.

<em><strong>Lưu ý:</strong> Trong bài toán này, do số giờ sử dụng Internet không thể tăng mãi được nên ta chỉ có thể xét bài toán với số tháng không lớn mà thôi.</em>
<em>
</em> Biểu diễn các điểm dữ liệu trên hệ tọa độ ta được biểu đồ phân tán như sau

<div class="separator" style="clear: both; text-align: center;">
<a href="https://4.bp.blogspot.com/-XdwJxpt2BZQ/W0V8g7S0nuI/AAAAAAAAD4E/VZC-oVEo9x0nXdapv6FH5VBjJjfVVPBDACLcBGAs/s1600/Untitled-2.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Biểu đồ số giờ dùng Internet" border="0" data-original-height="222" data-original-width="500" src="https://4.bp.blogspot.com/-XdwJxpt2BZQ/W0V8g7S0nuI/AAAAAAAAD4E/VZC-oVEo9x0nXdapv6FH5VBjJjfVVPBDACLcBGAs/s1600/Untitled-2.png" title="Biểu đồ số giờ dùng Internet" /></a></div>

Nhìn biểu đồ ta thấy các điểm dữ liệu có xu hướng xếp thành hình parabol. Vì thế, thay vì dùng thuật toán Linear Regression ta dùng thuật toán Nonlinear Regression để tìm phương trình giả thuyết dạng đa thức bậc hai

$\widehat{y} = w_{0} + w_{1}x + w_{2}x^{2}$

với&nbsp;$\widehat{y}$ là số giờ sử dụng Internet của tháng thứ x.
<h3>
Giải quyết vấn đề</h3>
<h4>
Tự cài đặt thuật toán</h4>
Các bước cài đặt thuật toán

<strong>Bước 0:</strong>&nbsp;Đặt $u_{1} = x, u_{2} = x^{2}$ ta quy về việc tìm hàm tuyến tính với 2 biến $u_{1}, u_{2}$

$\widehat{y} = w_{0} + w_{1}u_{1} + w_{2}u_{2}$

và bảng dữ liệu mới là

<div class="separator" style="clear: both; text-align: center;">
<a href="https://2.bp.blogspot.com/-PcQUxQt75K8/W0V86appaiI/AAAAAAAAD4Q/Mv6qaR5RiloetWG-paW2pbagHK4PBi4YgCLcBGAs/s1600/Untitled-3.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Ứng dụng thuật toán Nonlinear Regression" border="0" data-original-height="960" data-original-width="501" src="https://2.bp.blogspot.com/-PcQUxQt75K8/W0V86appaiI/AAAAAAAAD4Q/Mv6qaR5RiloetWG-paW2pbagHK4PBi4YgCLcBGAs/s1600/Untitled-3.png" title="Ứng dụng thuật toán Nonlinear Regression" /></a></div>

<strong>Bước 1:&nbsp;</strong>Thiết lập các ma trận và vector

w = $\begin{bmatrix}w_{0} \\\\ w_{1} \\\\ w_{2} \end{bmatrix} $

U = $\begin{bmatrix}1 &amp; 1 &amp; 1 \\\\1 &amp; 1 &amp; 1 \\\\ ... &amp; ... &amp; ... \\\\1 &amp; 6 &amp; 36\end{bmatrix}$

y = $\begin{bmatrix}7 \\\\ 3 \\\\ ... \\\\ 145 \end{bmatrix}$

<strong>Bước 2:</strong>&nbsp;Tính vector w

$w = (U^{T}U)^{+}U^{T}y$

Mở trình soạn thảo yêu thích của bạn, tạo file <strong>bai6.html</strong>&nbsp;rồi dán vào đoạn code sau

<script src="https://gist.github.com/dathoangnd/48995885334c82f6feed4a33f81bf631.js"></script>

Ta được kết quả

<i>Số giờ sử dụng Internet tháng thứ 3 là 21</i>

<i>Số giờ sử dụng Internet tháng thứ 7 là 245</i>

<i>Số giờ sử dụng Internet tháng thứ 9 là 454</i>
<h4>
Sử dụng hàm có sẵn</h4>
Việc sử dụng hàm có sẵn giống hệt như ở bài&nbsp;<a href="https://www.dathoangblog.com/2018/07/ung-dung-linear-regression-nhieu-bien.html" rel="noopener" target="_blank">ứng dụng thuật toán Linear Regression nhiều biến</a>.

<script src="https://gist.github.com/dathoangnd/368c2bd8e606b791dba9dd840555977a.js"></script>

Ta cũng được kết quả

<i>Số giờ sử dụng Internet tháng thứ 3 là 21</i>

<i>Số giờ sử dụng Internet tháng thứ 7 là 245</i>

<i>Số giờ sử dụng Internet tháng thứ 9 là 454</i>

<em><strong>Lưu ý:</strong>&nbsp;Trong thuật toán Nonlinear Regression, nếu phương trình giả thuyết là một hàm đa thức thì thuật toán còn được gọi là <a href="https://en.wikipedia.org/wiki/Polynomial_regression" rel="noopener" target="_blank"><strong>Polynomial regression</strong></a> (Hồi quy đa thức). Thư viện ml.js có các hàm riêng để tìm ra phương trình giả thuyết dạng đa thức. Nhờ đó ta có thể giải quyết bài toán trên bằng cài đặt đơn giản hơn như sau</em>

<script src="https://gist.github.com/dathoangnd/ac12497a97dbbafe6d944b3dedff1041.js"></script>

<h3>
Giờ đến lượt bạn</h3>
Trong bài thực hành này, bạn đã được học cách ứng dụng thuật toán Nonlinear Regression để dự đoán số giờ sử dụng Internet của từng tháng.

Lưu ý rằng phương trình giả thuyết mà ta tìm được chỉ đúng khi số tháng là nhỏ do số giờ sử dụng Internet không thể vượt quá số giờ trong tháng được.

Qua bài toán này, chúng ta cũng thấy được sức hút của Internet đối với con người khi thời gian chúng ta dành cho chúng là rất lớn.

Thời gian bạn dành cho Internet là bao nhiêu? Bạn thường sử dụng Internet cho những mục đích gì?