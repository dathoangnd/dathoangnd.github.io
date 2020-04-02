---
layout: post
title:  "Bài 8: Ứng Dụng Thuật Toán Gradient Descent"
description: "Trong bài này chúng ta sẽ ứng dụng thuật toán Gradient Descent trong Machine Learning để dự đoán huyết áp tâm thu của những người ở độ tuổi khác nhau."
---

Trong bài này, ta sẽ giải quyết lại vấn đề dự đoán huyết áp tâm thu của những người ở độ tuổi khác nhau bằng cách ứng dụng <a href="https://www.dathoangblog.com/2018/07/gradient-descent.html" rel="noopener" target="_blank">thuật toán Gradient Descent</a>.

Bài thực hành này nhằm mục đích giúp bạn biết cách áp dụng Gradient Descent - một thuật toán rất quan trọng trong nghiên cứu Machine Learning.
<!--more-->
<h3>
Nhắc lại vấn đề</h3>
Dưới đây là dữ liệu độ tuổi và huyết áp tâm thu (HATT) của 20 người được khảo sát

<div class="separator" style="clear: both; text-align: center;">
<a href="https://3.bp.blogspot.com/-wFpNeT5e4v8/W0VqLd7xQCI/AAAAAAAAD2k/zYJzqJmAA7AZ8jwiX3KQAduD2y2E32I5ACPcBGAYYCw/s1600/1.jpg" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Bảng dữ liệu tuổi - huyết áp tâm thu" border="0" data-original-height="647" data-original-width="500" src="https://3.bp.blogspot.com/-wFpNeT5e4v8/W0VqLd7xQCI/AAAAAAAAD2k/zYJzqJmAA7AZ8jwiX3KQAduD2y2E32I5ACPcBGAYYCw/s1600/1.jpg" title="Bảng dữ liệu tuổi - huyết áp tâm thu" /></a></div>


Ta cần dựa vào các dữ kiện trên để tìm ra mối liên hệ tuyến tính giữa huyết áp tâm thu và tuổi. Từ đó ta có thể dự đoán huyết áp tâm thu của người ở độ tuổi bất kỳ.

$\widehat{y} =&nbsp;&nbsp;w_{0} + w_{1}x_{1}$

với&nbsp;$\widehat{y}$ là huyết áp tâm thu của người $x_{1}$ tuổi.

Đây chính xác là vấn đề ta đã giải quyết ở bài <a href="https://www.dathoangblog.com/2018/07/ung-dung-linear-regression-mot-bien.html" rel="noopener" target="_blank">ứng dụng thuật toán Linear Regression một biến</a>.

Bằng việc tính các đạo hàm riêng của hàm mất mát và giải hệ các đạo hàm riêng bằng 0 ta tìm được kết quả

<i>HATT của người 26 tuổi là 120</i>

<i>HATT của người 10 tuổi là 105</i>

<i>HATT của người 80 tuổi là 172</i>

Bây giờ, ta sẽ sử dụng thuật toán Gradient Descent để xem có thu được kết quả giống như vậy hay không.
<h3>
Giải quyết vấn đề bằng Gradient Descent</h3>
<h4>
Gradient Descent trong Linear Regression</h4>
Trong thuật toán Linear Regression nhiều biến, hàm mất mát có giá trị

$J(w) =&nbsp;\frac{1}{2m} [ \sum_{i=1}^{m} ( \widehat{y}^{(i)} - y^{(i)}) ^{2} + \lambda \sum_{j=1}^{n}w_{j}^{2}]$

$= \frac{1}{2m} [ \sum_{i=1}^{m} ( w_{0} + w_{1}x_{1}^{(i)} + ... +&nbsp;w_{n}x_{n}^{(i)} - y^{(i)}) ^{2} + \lambda \sum_{j=1}^{n}w_{j}^{2}]$

Ta cần tìm ra&nbsp;n + 1 biến $w_{0}, w_{1}, ..., w_{n} $ để hàm mất mát trên có giá trị nhỏ nhất.

Ở bài trước, ta đã có nhận xét rằng hàm mất mát của thuật toán Linear Regression chỉ có một cực tiểu nên nếu áp dụng thuật toán Gradient Descent ta sẽ tìm được điểm cực tiểu đó cũng chính là điểm mà hàm mất mát đạt giá trị nhỏ nhất.

Các bước áp dụng thuật toán như sau

<strong>Bước 1:</strong>&nbsp;Chọn một điểm bất kỳ&nbsp;$(w_{0}, w_{1}, ..., w_{n})$ và một giá trị learning rate&nbsp;α.

<strong>Bước 2:</strong>&nbsp;Liên tiếp lặp lại các phép biến đổi

$w_{0} := w_{0} - \alpha \frac{1}{m} \sum_{i=1}^{m} ( \widehat{y}^{(i)} - y^{(i)})$

$w_{1} := w_{1}(1- \alpha \frac{\lambda}{m}) - \alpha \frac{1}{m} \sum_{i=1}^{m} (( \widehat{y}^{(i)} - y^{(i)})x_{1}^{(i)})$

...

$w_{n} := w_{n}(1- \alpha \frac{\lambda}{m}) - \alpha \frac{1}{m} \sum_{i=1}^{m} (( \widehat{y}^{(i)} - y^{(i)})x_{n}^{(i)})$

<strong>Bước 3:</strong> Thuật toán dừng lại khi J(w) thay đổi rất nhỏ hoặc trị tuyệt đối các đạo hàm riêng rất nhỏ. Nếu thuật toán không thể kết thúc thì chọn giá trị&nbsp;α nhỏ hơn rồi quay lại bước 2.
<h4>
Áp dụng</h4>
Đối với bài toán đặt ra ở đầu bài, để đơn giản ta bỏ qua việc chính quy hóa dữ liệu thì các bước cài đặt thuật toán cụ thể như sau

<strong>Bước 1:</strong>&nbsp;Chọn $w_{0} =&nbsp;w_{1} = 0$&nbsp; và α = 0.0003

<strong>Bước 2:</strong>&nbsp;Liên tiếp lặp lại các phép biến đổi

$w_{0} := w_{0} - \alpha \frac{1}{20} \sum_{i=1}^{20} ( \widehat{y}^{(i)} - y^{(i)})$

$w_{1} := w_{1} - \alpha \frac{1}{20} \sum_{i=1}^{20} (( \widehat{y}^{(i)} - y^{(i)})x^{(i)}_{1})$

<strong>Bước 3:</strong> Thuật toán dừng lại khi J(w) thay đổi rất nhỏ hoặc trị tuyệt đối các đạo hàm riêng rất nhỏ. Nếu thuật toán không thể kết thúc thì chọn giá trị&nbsp;α nhỏ hơn rồi quay lại bước 2.

Mở trình soạn thảo, tạo file <strong>bai8.html</strong> rồi dán đoạn code sau vào

<script src="https://gist.github.com/dathoangnd/b1f684f4d45e1bc1ae15e8b58ce23c24.js"></script>
Ta được kết quả chính xác

<i>HATT của người 26 tuổi là 120</i>

<i>HATT của người 10 tuổi là 105</i>

<i>HATT của người 80 tuổi là 172</i>

Ta đã rất may mắn khi chọn&nbsp;α = 0.0003 và chương trình nhanh chóng đưa ra được kết quả.

Giả sử ta chọn&nbsp;α = 0.00001 chương trình vẫn sẽ đưa ra được kết quả đúng nhưng thời gian chạy chương trình sẽ rất dài (theo thử nghiệm của tôi thì chương trình tốn tới 17 giây để đưa ra kết quả).

Nhưng nếu chọn&nbsp;α = 0.001 thì ta sẽ gặp "màn hình trắng chết chóc" do vòng lặp không bao giờ kết thúc. Cũng có thể do tôi không đủ kiên nhẫn chờ đợi, nếu bạn thử và chương trình hiện ra kết quả sau một vài tiếng đồng hồ, hãy báo cho tôi biết!

Cách áp dụng thuật toán như ở trên được gọi là <b>Batch Gradient Descent</b>. Trong đó, mỗi bước lặp ta đều tính toán các đạo hàm riêng bằng cách duyệt qua tất cả các input của bộ dữ liệu đào tạo. Cách này sẽ rất chậm khi số lượng dữ liệu lớn.

Để khắc phục điều này, biến thể <b>Mini-batch Gradient Descent</b> làm giảm gánh nặng tính toán bằng cách chia bộ dữ liệu đào tạo thành nhiều phần nhỏ. Mỗi bước lặp sẽ tính toán các đạo hàm riêng trên từng phần nhỏ này. Biến thể <b>Stochastic Gradient Descent</b> áp dụng phương pháp này một cách cực đoan khi mỗi bước lặp chỉ tính toán đạo hàm riêng với một input duy nhất. Hàm mất mát sẽ có thể không giảm sau mỗi lần lặp nhưng giá trị trung bình của hàm mất mát sau mỗi khoảng input có xu hướng giảm. Sau một vài vòng lặp qua tất cả dữ liệu đào tạo, ta sẽ tìm được kết quả tiệm cận với phương án tối ưu. Dù vậy, các biến thể này rất hiệu quả và nhanh chóng.

Stochastic Gradient Descent còn được sử dụng để đào tạo các mô hình có luồng dữ liệu vào liên tục. Lấy ví dụ với dữ liệu hành vi người dùng được ghi lại bởi website, nếu với mỗi dữ liệu mới ta lại phải tính toán lại phương trình giả thuyết từ đầu thì rõ ràng không hiệu quả. Thay vào đó ta có thể thực hiện các thay đổi hệ số

$w_{j} = w_{j} - \alpha ( \widehat{y} - y)x_{j}$

Một ưu điểm nữa của cách làm này là ta không cần lưu lại dữ liệu mới vì thay đổi đã được cập nhật.
<h3>
Giờ đến lượt bạn</h3>
Vậy là bạn đã biết cách ứng dụng thuật toán Gradient Descent để tìm ra được nghiệm của Linear Regression.

Mặc dù việc cài đặt Gradient Descent khá phức tạp nhưng đây là cách tổng quát và đối với các hàm khác nhau thì cách cài đặt vẫn không thay đổi.

Trong bài này, ta cũng thấy vai trò quan trọng của việc chọn learning rate&nbsp;α. Nếu chương trình chạy quá lâu, hãy tăng&nbsp;α, nếu gặp "màn hình trắng chết chóc", hãy giảm&nbsp;α.

Bây giờ, bạn hãy thử áp dụng thuật toán Gradient Descent để giải quyết bài toán <a href="https://www.dathoangblog.com/2018/07/ung-dung-linear-regression-nhieu-bien.html" rel="noopener" target="_blank">dự đoán giá nhà bằng Linear Regression nhiều biến</a>&nbsp;thay vì áp dụng công thức.

Bạn có tìm ra kết quả như trước không? Có những khó khăn gì khi xử lý hàm nhiều biến?