---
tag: learn
layout: post
title:  "Bài 2: Ứng Dụng Thuật Toán Linear Regression Một Biến"
description: "Cách ứng dụng thuật toán Linear Regression một biến trong Machine Learning để dự đoán huyết áp tâm thu của những người ở độ tuổi khác nhau."
---

Trong bài này, chúng ta sẽ ứng dụng <a href="https://www.dathoangblog.com/2018/07/linear-regression-mot-bien.html" rel="noopener" target="_blank">thuật toán Linear Regression một biến</a> đã được học ở bài trước&nbsp;để giải một bài toán thực tế.

Đây là bài thực hành đầu tiên trong khóa học, và chúng ta bắt đầu đụng đến code để nghiên cứu Machine Learning.
<!--more-->
<h3>
Cài đặt môi trường thực hành</h3>
Do đây là bài thực hành đầu tiên nên tôi sẽ giới thiệu sơ qua các công cụ chúng ta sử dụng để nghiên cứu Machine Learning.

Như đã đề cập trong bài&nbsp;<a href="https://www.dathoangblog.com/2018/07/machine-learning-la-gi.html" rel="noopener" target="_blank">giới thiệu Machine Learning và khóa học</a>, chúng ta sẽ sử dụng ngôn ngữ <strong>JavaScript</strong> trong khóa học này. Tôi chọn JavaScript bởi nó là ngôn ngữ rất quen thuộc với nhiều người. Hơn nữa JavaScript lại chạy ngay trên trình duyệt nên bạn không cần cài bất cứ chương trình dịch nào.

Chúng ta cũng sẽ sử dụng thư viện&nbsp;<strong><a href="https://github.com/mljs/ml" rel="noopener" target="_blank">ml.js</a></strong> xuyên suốt khóa học. Đây là một thư viện JavaScript với đầy đủ các hàm tính toán ma trận cũng như thuật toán Machine Learning được cài đặt sẵn. Trong các bài thực hành, chúng ta sẽ tự cài đặt thuật toán Machine Learning, sau đó sử dụng hàm có sẵn trong thư viện để đảm bảo thuật toán đã cài đặt đúng.

Thứ duy nhất bạn cần cài đặt là một trình viết code đơn giản. Tôi khuyên bạn nên dùng các trình soạn thảo như Visual Studio Code, Sublime Text, Atom. Cá nhân tôi rất yêu thích Visual Studio Code. Bạn cũng có thể chọn một trình soạn thảo khác phù hợp với mình.
<h3>
Đặt vấn đề</h3>
Dưới đây là dữ liệu độ tuổi và huyết áp tâm thu (HATT) của 20 người được khảo sát


<div class="separator" style="clear: both; text-align: center;">
<a href="https://3.bp.blogspot.com/-wFpNeT5e4v8/W0VqLd7xQCI/AAAAAAAAD2g/KjKtpAjlZ-4amW1zsOFYwyrUgsrrL1OvwCLcBGAs/s1600/1.jpg" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Bảng dữ liệu tuổi - huyết áp tâm thu" border="0" data-original-height="647" data-original-width="500" src="https://3.bp.blogspot.com/-wFpNeT5e4v8/W0VqLd7xQCI/AAAAAAAAD2g/KjKtpAjlZ-4amW1zsOFYwyrUgsrrL1OvwCLcBGAs/s1600/1.jpg" title="Bảng dữ liệu tuổi - huyết áp tâm thu" /></a></div>


Biểu đồ dưới đây biểu diễn các giá trị tuổi - HATT trong bảng trên. Ta cần tìm được phương trình đường thẳng biểu diễn mối liên hệ giữa độ tuổi và HATT, từ đó dự đoán được HATT của những người ở độ tuổi khác nhau.

<div class="separator" style="clear: both; text-align: center;">
<a href="https://1.bp.blogspot.com/-hYnTHSqXwPs/W0VqbedG0RI/AAAAAAAAD2o/_VI9f3uuE6chkrOXLNA-YTHR048_IdWEwCLcBGAs/s1600/2.jpg" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Ứng dụng thuật toán Linear Regression một biến để dự đoán huyết áp tâm thu theo tuổi" border="0" data-original-height="238" data-original-width="500" src="https://1.bp.blogspot.com/-hYnTHSqXwPs/W0VqbedG0RI/AAAAAAAAD2o/_VI9f3uuE6chkrOXLNA-YTHR048_IdWEwCLcBGAs/s1600/2.jpg" title="Ứng dụng thuật toán Linear Regression một biến để dự đoán huyết áp tâm thu theo tuổi" /></a></div>
<div class="separator" style="clear: both; text-align: center;">

</div>
<h3>
Giải quyết vấn đề</h3>
<h4>
Tự cài đặt thuật toán</h4>
Mỗi khi bắt đầu học một ngôn ngữ hoặc nội dung mới, chúng ta luôn bắt đầu bằng chương trình Hello World. Tôi sẽ tôn trọng truyền thống này.

Trước tiên bạn mở trình soạn thảo yêu thích của mình, tạo file tên <strong>bai2.html</strong>&nbsp;rồi dán đoạn code sau vào

<script src="https://gist.github.com/dathoangnd/d1108e42f117abf0c0582e7004e0a960.js"></script>
Trong đoạn code trên, ta đã nhúng thư viện ml.js và in ra màn hình dòng chữ Hello World. Hãy mở file vừa tạo bằng trình duyệt để xem kết quả.

Bây giờ, ta bắt đầu cài đặt thuật toán theo các bước đã được trình bày trong bài trước.

<strong>Bước 1:&nbsp;</strong>Thiết lập các ma trận và vector

w = $\begin{bmatrix}w_{0} \\\\ w_{1} \end{bmatrix} $

X = $\begin{bmatrix}1 &amp; 39 \\\\ 1 &amp; 36 \\\\ ... &amp; ... \\\\ 1 &amp; 19\end{bmatrix}$

y = $\begin{bmatrix}144 \\\\ 136 \\\\ ... \\\\ 124 \end{bmatrix}$

<strong>Bước 2:</strong>&nbsp;Tính vector w

$w = (X^{T}X)^{+}X^{T}y$

Cụ thể mã nguồn cài đặt thuật toán như sau

<script src="https://gist.github.com/dathoangnd/1e625a7759a0b1407114e39f1bd183a9.js"></script>
Ta được kết quả như sau

<i>HATT của người 26 tuổi là 120</i>

<i>HATT của người 10 tuổi là 105</i>

<i>HATT của người 80 tuổi là 172</i>

<strong>Lưu ý:</strong>&nbsp;Thư viện ml.js chứa nhiều hàm có sẵn phục vụ rất tốt cho nghiên cứu Machine Learning. Bạn có thể đọc thêm tài liệu hướng dẫn của&nbsp;<a href="https://github.com/mljs/ml" rel="noopener" target="_blank">ml.js</a>&nbsp;trên Github. Tất cả các hàm tôi sử dụng trong khóa học này đều có thể được tìm thấy trong tài liệu hướng dẫn.
<h4>
Sử dụng hàm có sẵn</h4>
Bản thân thư viện ml.js đã cài đặt sẵn nhiều thuật toán Machine Learning để ta không phải triển khai lại từ đầu. Trong phần này, tôi sẽ áp dụng thuật toán Linear Regression một biến có sẵn trong thư viện để xem kết quả tìm được có giống ở trên hay không.

Mã nguồn sử dụng hàm Linear Regression một biến có sẵn

<script src="https://gist.github.com/dathoangnd/2dab0527c4a2938b62ead615fc021a3a.js"></script>
Ta được kết quả

<i>HATT của người 26 tuổi là 120</i>

<i>HATT của người 10 tuổi là 105</i>

<i>HATT của người 80 tuổi là 172</i>

Kết quả này giống như ở trên. Điều đó cho thấy ta đã cài đặt thuật toán một cách chính xác.

Việc sử dụng hàm có sẵn rõ ràng là đơn giản hơn rất nhiều, nhưng bạn cần phải hiểu thuật toán hoạt động như thế nào để có thể tùy chỉnh hoặc gỡ lỗi khi cần thiết.
<h3>
Giờ đến lượt bạn</h3>
Trong bài thực hành đầu tiên này, bạn đã được học cách sử dụng thuật toán Machine Learning để dự đoán huyết áp của những người ở độ tuổi khác nhau.

Bạn cũng biết được rằng, ngoài kia có rất nhiều lập trình viên tốt bụng đã tạo ra các thư viện miễn phí giúp việc nghiên cứu Machine Learning của bạn dễ dàng hơn.

Bây giờ thì đến lượt bạn

Hãy sửa đổi dữ liệu đầu vào để quan sát sự thay đổi dự đoán HATT của thuật toán. Bạn cũng có thể thêm một vài dữ liệu nhiễu để xem ảnh hưởng của nó. Theo bạn, dữ liệu đầu vào cần có những tiêu chí gì để đảm bảo tính đúng đắn của thuật toán?

Bạn hãy tìm một bộ dữ liệu khác hoặc tự nghĩ ra một bộ dữ liệu có thể áp dụng thuật toán Linear Regression một biến, sau đó tự mình cài đặt thuật toán với bộ dữ liệu mới này.