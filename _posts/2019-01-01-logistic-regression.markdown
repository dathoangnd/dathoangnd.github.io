---
tag: learn
layout: post
title:  "Bài 9: Thuật Toán Logistic Regression"
description: "Bài này sẽ hướng dẫn bạn tìm hiểu thuật toán Logistic Regression - một thuật toán phân loại rất quan trọng trong Machine Learning."
---

Trong bài này chúng ta sẽ tìm hiểu thuật toán loại Classification đầu tiên, đó là Logistic Regression.

Mặc dù tên gọi chứa từ "Regression" nhưng đây là thuật toán thuộc loại Classification. Thực tế cho thấy nó là một trong những thuật toán Machine Learning được sử dụng phổ biến nhất.

Kiến thức về thuật toán Logistic Regression là cần thiết trước khi tìm hiểu <a href="https://www.dathoangblog.com/2019/01/support-vector-machine.html">thuật toán Support Vector Machine</a> và <a href="https://www.dathoangblog.com/2019/01/neural-network.html">Neural Network</a>.
<!--more-->
<h3>
Mở đầu</h3>
Xét đồ thị phân bố dữ liệu dưới đây

<div class="separator" style="clear: both; text-align: center;">
<a href="https://1.bp.blogspot.com/-xiWpyDZc_Mg/XC4jII4YwEI/AAAAAAAAEME/4k59MLL1NacsYIC5nQmgpmD3eXqisgGJQCLcBGAs/s1600/LogisticRegressionWindowLogisticFitChart6.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Thuật toán Logistic Regression" border="0" data-original-height="305" data-original-width="500" src="https://1.bp.blogspot.com/-xiWpyDZc_Mg/XC4jII4YwEI/AAAAAAAAEME/4k59MLL1NacsYIC5nQmgpmD3eXqisgGJQCLcBGAs/s1600/LogisticRegressionWindowLogisticFitChart6.png" title="Thuật toán Logistic Regression" /></a></div>

Các điểm dữ liệu màu đỏ ứng với output có giá trị bằng 0 và các điểm dữ liệu màu xanh ứng với output có giá trị bằng 1. Đường ở giữa phân chia 2 loại điểm dữ liệu được gọi là <b>Decision Boundary</b> có phương trình $x^{T}w = 0$ với w =&nbsp;$\begin{bmatrix}w_{0} \\\\ w_{1} \\\\ ... \\\\ w_{n} \end{bmatrix} $ và x =&nbsp;$\begin{bmatrix}1 \\\\ x_{1} \\\\ ... \\\\ x_{n} \end{bmatrix}$.

Bây giờ, ta đặt phương trình giả thuyết $\widehat{y} = g(x^{T}w)$ với hàm g được chọn để:
<ul>
<li>$0 \leq \widehat{y} \leq 1$</li>
<li>Khi $x^{T}w = 0$ thì $\widehat{y} = 0.5$</li>
<li>Khi&nbsp;&nbsp;$x^{T}w &gt; 0$ và tiến tới dương vô cùng thì $\widehat{y}$ tiến tới 1. Khi&nbsp;&nbsp;$x^{T}w &lt; 0$ và tiến tới âm vô cùng thì $\widehat{y}$ tiến tới 0.</li>
</ul>

Khi đó ta có thể dự đoán y = 1 nếu $\widehat{y} \geq 0.5$ và dự đoán y = 0 nếu $\widehat{y} &lt; 0.5$.

Một cách cụ thể, giả sử với một input nào đó ta tìm được $\widehat{y} = 0.7$, ta có thể nói output có 70% khả năng là 1 và 30% khả năng là 0.

<h3>
Thuật toán Logistic Regression</h3>
<h4>
Mô hình toán học</h4>
Hàm số g(z) bên dưới có tên gọi là <b>hàm Sigmoid</b> hoặc <b>hàm Logistic</b>
<b>
</b> g(z) = $\frac{1}{1 + e^{-z}}$

Dưới đây là đồ thị của hàm số trên

<div class="separator" style="clear: both; text-align: center;">
<a href="https://3.bp.blogspot.com/-S10zuvNrzzI/XC4swN1acSI/AAAAAAAAEMQ/8RLmyF4bvy81x2UXesweIkCNazgdaV9DgCEwYBhgL/s1600/main-qimg-07066668c05a556f1ff25040414a32b7.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Hàm Sigmoid" border="0" data-original-height="332" data-original-width="500" src="https://3.bp.blogspot.com/-S10zuvNrzzI/XC4swN1acSI/AAAAAAAAEMQ/8RLmyF4bvy81x2UXesweIkCNazgdaV9DgCEwYBhgL/s1600/main-qimg-07066668c05a556f1ff25040414a32b7.png" title="Hàm Sigmoid" /></a></div>
Từ đồ thị trên ta thấy hàm Sigmoid đáp ứng tất cả các tiêu chuẩn đặt ra để xây dựng phương trình giả thuyết. Thuật toán sử dụng hàm Sigmoid được gọi là Logistic Regression.

Phương trình giả thuyết lúc này trở thành

$\widehat{y} = \frac{1}{1 + e^{-x^{T}w}}$
<h4>
Độ chính xác của phương trình giả thuyết</h4>
Ta không thể sử dụng hàm mất mát giống như thuật toán Linear Regression cho Logistic Regression. Lý do là bởi phương trình giả thuyết đã thay đổi và sẽ tồn tại nhiều cực tiểu địa phương dẫn đến khó khăn trong việc tìm nghiệm tại đó hàm mất mát đạt giá trị nhỏ nhất.

Ta cần chọn hàm mất mát sao cho nó chỉ có 1 cực tiểu. Có nhiều cách chọn thỏa mãn điều này, song trong thực tế, người ta hay chọn hàm mất mát như dưới đây

$J(w) = -\frac{1}{m} \sum_{i=1}^{m} [y^{(i)}ln (\widehat{y}^{(i)}) + (1 - y^{(i)})ln (1 - \widehat{y}^{(i)})] + \frac{\lambda}{2m}\sum_{j=1}^{n} w^{2}_{j}$

Đặt X = $\begin{bmatrix}1 &amp; x_{1}^{(1)} &amp; ... &amp; x_{n}^{(1)} \\\\ 1 &amp; x_{1}^{(2)} &amp; ... &amp; x_{n}^{(2)}&nbsp;\\\\... &amp; ... &amp; ... &amp; ... \\\\ 1 &amp; x_{1}^{(m)} &amp; ... &amp; x_{n}^{(m)} \end{bmatrix}$ là ma trận với mỗi hàng là một input (hàng i ứng với $x^{(i)T}$), đặt w = $\begin{bmatrix}w_{0} \\\\ w_{1} \\\\ ... \\\\ w_{n} \end{bmatrix} $ là vector các hệ số của Decision Boundary, đặt $\widehat{y} = g(Xw)$ là vector các dự đoán của các input, đặt y = $\begin{bmatrix}y^{(1)} \\\\ y^{(2)} \\\\ ... \\\\ y^{(m)} \end{bmatrix}$ là vector các output thì hàm mất mát được viết lại thành

$J(w) = -\frac{1}{m} (y^{T}ln (\widehat{y}) + (1 - y)^{T}ln (1 - \widehat{y})) + \frac{\lambda}{2m}\sum_{j=1}^{n} w^{2}_{j}$
<h4>
Nghiệm của thuật toán Logistic Regression</h4>
Ta có thể tìm điểm cực tiểu của hàm mất mát bằng thuật toán Gradient Descent với các biến đổi

$w_{0} := w_{0} - \alpha \frac{1}{m} \sum_{i=1}^{m} ( \widehat{y}^{(i)} - y^{(i)})$

$w_{1} := w_{1}(1- \alpha \frac{\lambda}{m}) - \alpha \frac{1}{m} \sum_{i=1}^{m} (( \widehat{y}^{(i)} - y^{(i)})x_{1}^{(i)})$

...

$w_{n} := w_{n}(1- \alpha \frac{\lambda}{m}) - \alpha \frac{1}{m} \sum_{i=1}^{m} (( \widehat{y}^{(i)} - y^{(i)})x_{n}^{(i)})$

Ta nhận thấy các biến đổi này giống hệt như khi áp dụng Gradient Descent với thuật toán Linear Regression. Có điều này là bởi cách chọn hàm mất mát.
<h3>
Lựa chọn phương án tối ưu</h3>
<h4>
Lựa chọn biến và độ chính quy hóa</h4>
Các thuật toán Classification cũng có thể gặp vấn đề underfitting và overfitting giống như Regression. Chính vì thế, ta cần thử nhiều phương án với cách chọn biến và độ chính quy hóa khác nhau để lựa chọn ra phương án tốt nhất.

Có nhiều cách để đánh giá mức độ tốt của một phương án.&nbsp; Một cách đơn giản nhất ta có thể dùng một tập thử và lấy tỉ lệ kết quả trả về đúng. Phương án nào có tỉ lệ đúng cao nhất sẽ được lựa chọn.

Nhưng khi một trong hai lớp phân loại có tỉ lệ rất nhỏ so với lớp còn lại vấn đề sẽ phức tạp hơn một chút. Giả sử số người mắc một căn bệnh chiếm 5% tổng số người đến khám và thuật toán Machine Learning của ta có tỉ lệ đúng đạt 90%. Nhưng nếu một thuật toán nào đó luôn dự đoán người đến khám không có bệnh thì nó đã có tỉ lệ đúng tới 95%. Do đó, việc dùng tỉ lệ đúng để đánh giá thuật toán Machine Learning không phải lúc nào cũng hợp lý.

Ta đặt

A: số người bị bệnh và chẩn đoán có bệnh

B: số người bị bệnh và chẩn đoán không có bệnh

C: số người không bị bệnh và chẩn đoán có bệnh

D: số người không bị bệnh và chẩn đoán không có bệnh

Khi đó, ta định nghĩa <b>độ chính xác</b> P và <b>độ nhạy</b> R như sau

P = $\frac{A}{A + C}$

R = $\frac{A}{A + B}$

Hai chỉ số này giúp đánh giá thuật toán Machine Learning tốt hơn.
<h4>
Tương quan giữa độ chính xác và độ nhạy</h4>
Ở trên, ta đã dự đoán y = 1 nếu $\widehat{y} \geq 0.5$ và dự đoán y = 0 nếu $\widehat{y} &lt; 0.5$.

Nếu ta nâng mức thay đổi dự đoán lên, giả dụ dự đoán y = 1 nếu $\widehat{y} \geq 0.7$ và dự đoán y = 0 nếu $\widehat{y} &lt; 0.7$, khi đó các phép thử sẽ có độ chính xác cao hơn nhưng độ nhạy thấp hơn.

Nếu ta hạ mức thay đổi dự đoán xuống, giả dụ dự đoán y = 1 nếu $\widehat{y} \geq 0.3$ và dự đoán y = 0 nếu $\widehat{y} &lt; 0.3$, khi đó các phép thử sẽ có độ chính xác thấp hơn nhưng độ nhạy cao hơn.

Việc lựa chọn mức thay đổi dự đoán cao hay thấp tùy tình huống thực tế. Chỉ số F1 score được dùng để so sánh các phương án lựa chọn khác nhau.

F1 = 2$\frac{PR}{P + R}$
<h3>
Phân loại đa lớp</h3>
Ở trên ta đã giả định là output chỉ nhận giá trị 0 hoặc 1, hay là có 2 lớp output. Nhiều bài toán phân loại trong thực tế mà có nhiều hơn 2 lớp output.

Xét bài toán mà y nhận một trong các giá trị 0, 1, 2, ..., p (p + 1 lớp).

Bằng cách chia các input có output bằng 0 vào một nhóm và gộp tất cả các input có output từ 1 tới p vào một nhóm, ta có thể tìm được phương trình giả thuyết $\widehat{y}_{0}$ biểu thị khả năng một input có output là 0.

Tương tự, ta có thể tìm được các phương trình giả thuyết $\widehat{y}_1$, $\widehat{y}_2$, ..., $\widehat{y}_p$ biểu thị khả năng một input có output là giá trị tương ứng.

Bây giờ với mỗi input mới, phương trình giả thuyết nào có giá trị cao nhất thì ta dự đoán output thuộc về lớp đó.
<h3>
Tóm tắt thuật toán Logistic Regression</h3>
<h4>
Yêu cầu</h4>
Cho trước m bộ dữ liệu để đào tạo thuật toán. Bộ dữ liệu thứ i chứa input $x^{(i)}$ và output $y^{(i)}$ thuộc một trong hai giá trị 0 và 1. Nhiệm vụ của ta là tìm ra vector hệ số w =&nbsp;$\begin{bmatrix}w_{0} \\\\ w_{1} \\\\ ... \\\\ w_{n} \end{bmatrix} $ của Decision Boundary.
<h4>
</h4>
<h4>
Thuật toán</h4>
<strong>Bước 1:</strong>&nbsp;Chọn một điểm bất kỳ&nbsp;$(w_{0}, w_{1}, ..., w_{n})$ và một giá trị learning rate&nbsp;α.

<strong>Bước 2:</strong>&nbsp;Liên tiếp lặp lại các phép biến đổi

$w_{0} := w_{0} - \alpha \frac{1}{m} \sum_{i=1}^{m} ( \widehat{y}^{(i)} - y^{(i)})$

$w_{1} := w_{1}(1- \alpha \frac{\lambda}{m}) - \alpha \frac{1}{m} \sum_{i=1}^{m} (( \widehat{y}^{(i)} - y^{(i)})x_{1}^{(i)})$

...

$w_{n} := w_{n}(1- \alpha \frac{\lambda}{m}) - \alpha \frac{1}{m} \sum_{i=1}^{m} (( \widehat{y}^{(i)} - y^{(i)})x_{n}^{(i)})$

<strong>Bước 3:</strong>&nbsp;Thuật toán dừng lại khi J(w) thay đổi rất nhỏ hoặc trị tuyệt đối các đạo hàm riêng rất nhỏ. Nếu thuật toán không thể kết thúc thì chọn giá trị&nbsp;α nhỏ hơn rồi quay lại bước 2.
<h3>
Bạn đang nghĩ gì?</h3>
Bạn vừa được học thuật toán Logistic Regression - một thuật toán Classification rất quan trọng và phổ biến.

Chúng ta sẽ áp dụng thuật toán này trong bài Ứng dụng thuật toán Logistic Regression.

Theo bạn, nếu giá trị các lớp output khác 0 và 1, giả sử 2 và 3 thì chúng ta gặp khó khăn gì khi triển khai Logistic Regression? Làm thế nào để khắc phục điều đó?