---
tag: learn
layout: post
title:  "Bài 3: Thuật Toán Linear Regression Nhiều Biến"
description: "Bài này sẽ hướng dẫn bạn tìm hiểu thuật toán Linear Regression nhiều biến - một thuật toán rất quan trọng trong Machine Learning."
---

Bài này sẽ hướng dẫn bạn tìm hiểu thuật toán Linear Regression nhiều biến trong Machine Learning.

Đây là trường hợp mở rộng của <a href="https://www.dathoangblog.com/2018/07/linear-regression-mot-bien.html" rel="noopener" target="_blank">thuật toán Linear Regression một biến</a> mà bạn đã được học.

Bạn sẽ được ứng dụng thuật toán này trong dự án thực tế ở bài tiếp theo.
<!--more-->
<h3>
Thuật toán Linear Regression nhiều biến</h3>
Trong thuật toán Linear Regression một biến, các input của bộ dữ liệu đào tạo chỉ chứa một biến duy nhất.

Nếu mỗi input chứa nhiều hơn một biến thì thuật toán được gọi là Linear Regression nhiều biến.

Nhắc lại bài toán tìm giá nhà bằng Linear Regression một biến, ta đơn giản hóa bài toán bằng cách giả định giá nhà chỉ phụ thuộc vào diện tích. Như vậy mỗi input của bộ dữ liệu đào tạo chỉ có duy nhất biến diện tích.

Trong thực tế, giá nhà còn phụ thuộc vào nhiều yếu tố khác như số phòng, vị trí, số năm tuổi.

Giả sử giá nhà phụ thuộc vào hai yếu tố là diện tích và khoảng cách tới trung tâm thành phố, khi đó thuật toán Linear Regression với hai biến có nhiệm vụ tìm ra mặt phẳng biểu diễn sự phụ thuộc giữa giá nhà với hai yếu tố trên một cách chính xác nhất.


<div class="separator" style="clear: both; text-align: center;">
<a href="https://3.bp.blogspot.com/-hWOGLO2sbFo/W0VjsbIb33I/AAAAAAAAD1k/CvP6P3OvRwY5gewNdE7vqOWTtPW8R71QACPcBGAYYCw/s1600/figure_2.jpg" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Thuật toán Linear Regression nhiều biến" border="0" data-original-height="418" data-original-width="500" src="https://3.bp.blogspot.com/-hWOGLO2sbFo/W0VjsbIb33I/AAAAAAAAD1k/CvP6P3OvRwY5gewNdE7vqOWTtPW8R71QACPcBGAYYCw/s1600/figure_2.jpg" title="Thuật toán Linear Regression nhiều biến" /></a></div>


Phương trình mặt phẳng trên có thể viết dưới dạng tổng quát như sau

$\widehat{P}(s, d) = w_{0} + w_{1}s + w_{2}d$

với $\widehat{P}(s, d)$ là giá căn nhà diện tích s và cách trung tâm thành phố khoảng cách d.

Trong trường hợp tổng quát, input bao gồm n biến $x_{1}, x_{2}, ..., x_{n}$ và output&nbsp;$\widehat{y}$ phụ thuộc vào n biến đó theo phương trình tuyến tính

$\widehat{y} =&nbsp;&nbsp;w_{0} + w_{1}x_{1} + ... +&nbsp;w_{n-1}x_{n-1} + w_{n}x_{n}$

thì thuật toán tìm ra phương trình ở trên gọi là Linear Regression n biến.

Nếu n = 1 thì đó là phương trình đường thẳng và ta đã xét trường hợp này trong bài <a href="https://www.dathoangblog.com/2018/07/linear-regression-mot-bien.html" rel="noopener" target="_blank">thuật toán Linear Regression một biến</a>.

Nếu n = 2 thì đó là phương trình mặt phẳng.

Nếu n ≥ 3 thì phương trình đã trên không thể biểu diễn một cách hình học, nó được gọi là một <a href="https://en.wikipedia.org/wiki/Hyperplane" rel="noopener" target="_blank">siêu phẳng</a> n chiều (trong không gian n + 1 chiều).

Để đơn giản hóa phương trình ở trên, ta có thể đặt w = $\begin{bmatrix}w_{0} \\\\ w_{1} \\\\ ... \\\\ w_{n} \end{bmatrix} $ là vector các hệ số của phương trình giả thuyết, x = $\begin{bmatrix}1 \\\\ x_{1} \\\\ ... \\\\ x_{n} \end{bmatrix}$ là vector các biến của input (phần tử 1 trong vector đóng vai trò như $x_{0}$ chỉ nhằm mục đích thuận tiện cho tính toán) thì có thể viết lại phương trình trên như sau

$\widehat{y} =&nbsp; x^{T}w$
<h4>
Mô hình toán học</h4>
Ta nhắc lại phương trình cần tìm trong thuật toán Linear Regression nhiều biến

$\widehat{y} =&nbsp;&nbsp;w_{0} + w_{1}x_{1} + ... +&nbsp;w_{n-1}x_{n-1} + w_{n}x_{n}$
$= x^{T}w$

với w = $\begin{bmatrix}w_{0} \\\\ w_{1} \\\\ ... \\\\ w_{n} \end{bmatrix} $ và x = $\begin{bmatrix}1 \\\\ x_{1} \\\\ ... \\\\ x_{n} \end{bmatrix}$

Với mỗi bộ giá trị ($w_{0}, w_{1}, ..., w_{n}$) ta được một phương trình siêu phẳng khác nhau biểu diễn sự phụ thuộc giữa $\widehat{y}$ và x, mỗi phương trình như vậy được gọi là một <b>phương trình giả thuyết</b> (hypothesis function).

Do phương trình giả thuyết dùng để dự đoán giá trị thực tế đối với một input mới nên ta có

$y \approx \widehat{y} = x^{T}w$
<h4>
Độ chính xác của phương trình giả thuyết</h4>
Hàm mất mát của thuật toán Linear Regression nhiều biến tương tự như đối với thuật toán Linear Regression một biến

$J(w) =&nbsp;\frac{1}{2m} \sum_{i=1}^{m} ( \widehat{y}^{(i)} - y^{(i)}) ^{2}$

$= \frac{1}{2m} \sum_{i=1}^{m} ( w_{0} + w_{1}x_{1}^{(i)} + ... +&nbsp;w_{n}x_{n}^{(i)} - y^{(i)}) ^{2}$

$= \frac{1}{2m} \sum_{i=1}^{m} ( x^{(i)T}w - y^{(i)}) ^{2}$

trong đó m là số input ban đầu được dùng để đào tạo thuật toán.

Đặt X = $\begin{bmatrix}1 &amp; x_{1}^{(1)} &amp; ... &amp; x_{n}^{(1)} \\\\ 1 &amp; x_{1}^{(2)} &amp; ... &amp; x_{n}^{(2)}&nbsp;\\\\... &amp; ... &amp; ... &amp; ... \\\\ 1 &amp; x_{1}^{(m)} &amp; ... &amp; x_{n}^{(m)} \end{bmatrix}$ là ma trận với mỗi hàng là một input (hàng i ứng với $x^{(i)T}$), đặt y = $\begin{bmatrix}y^{(1)} \\\\ y^{(2)} \\\\ ... \\\\ y^{(m)} \end{bmatrix}$ là vector các output thì hàm mất mát được viết lại thành

$J(w) = \frac{1}{2m}&nbsp;\parallel Xw - y \parallel ^{2}$

<em><strong>Lưu ý:</strong>&nbsp;Như bạn thấy, các công thức của Linear Regression nhiều biến giống hệt như Linear Regression một biến. Mục đích của tôi khi tách riêng bài Linear Regression một biến là để có thể giải thích cho bạn dễ hiểu hơn trước khi học Linear Regression tổng quát.</em>
<h4>
Nghiệm của thuật toán Linear Regression nhiều biến</h4>
Việc tìm nghiệm của thuật toán Linear Regression nhiều biến chính là&nbsp;tìm ra tham số w = $\begin{bmatrix}w_{0} \\\\ w_{1} \\\\ ... \\\\ w_{n} \end{bmatrix} $ để hàm mất mát có giá trị nhỏ nhất.

Khi thực hiện việc khảo sát hàm mất mát đối với n + 1 biến $w_{0},&nbsp;w_{1}, ...,&nbsp;w_{n}$ ta được phương trình của vector w để hàm mất mát đạt giá trị nhỏ nhất sau

$X^{T}Xw = X^{T}y$

$X^{T}X$ là một ma trận vuông và nếu nó khả nghịch ta có tính ngay được w bằng công thức

$w = (X^{T}X)^{-1}X^{T}y$

Trong hầu hết trường hợp, công thức trên mang lại kết quả đúng đắn. Nhưng nếu trong các biến có hai biến phụ thuộc tuyến tính (tỉ lệ thuận) hoặc số biến lớn hơn hoặc bằng số input đào tạo thuật toán (n ≥ m) thì ma trận $X^{T}X$ không khả nghịch, nói cách khác nó không có ma trận nghịch đảo.

Để khắc phục trường hợp $X^{T}X$ không khả nghịch, ta có thể loại bớt các biến không cần thiết hoặc dùng kỹ thuật <a href="https://en.wikipedia.org/wiki/Regularization_(mathematics)" target="_blank">chính quy hóa dữ liệu</a> sẽ được nói đến trong bài <a href="https://www.dathoangblog.com/2018/07/nonlinear-regression.html">Thuật toán Nonlinear Regression</a>.

Hoặc bằng cách áp dụng ma trận giả đảo, ta tìm được w bằng công thức

$w = (X^{T}X)^{+}X^{T}y$
<h3>
Tóm tắt thuật toán Linear Regression nhiều biến</h3>
<h4>
Yêu cầu</h4>
Cho trước m bộ dữ liệu để đào tạo thuật toán. Bộ dữ liệu thứ i chứa input $x^{(i)}$ và output $y^{(i)}$, trong đó input thứ i chứa n biến từ $x_{1}^{(i)}$ đến $x_{n}^{(i)}$. Nhiệm vụ của chúng ta là tìm ra mối liên hệ giữa input và output bằng một hàm tuyến tính để khi đưa vào một input mới, ta có thể dự đoán được output ứng với nó

$\widehat{y} = w_{0} + w_{1}x_{1} + ... + w_{n}x_{n}$
<h4>
Thuật toán</h4>
<strong>Bước 1:&nbsp;</strong>Thiết lập các ma trận và vector dưới đây

w = $\begin{bmatrix}w_{0} \\\\ w_{1} \\\\ ... \\\\ w_{n} \end{bmatrix} $

X = $\begin{bmatrix}1 &amp; x_{1}^{(1)} &amp; ... &amp; x_{n}^{(1)} \\\\ 1 &amp; x_{1}^{(2)} &amp; ... &amp; x_{n}^{(2)}&nbsp;\\\\... &amp; ... &amp; ... &amp; ... \\\\ 1 &amp; x_{1}^{(m)} &amp; ... &amp; x_{n}^{(m)} \end{bmatrix}$

y = $\begin{bmatrix}y^{(1)} \\\\ y^{(2)} \\\\ ... \\\\ y^{(m)} \end{bmatrix}$

<strong>Bước 2:</strong>&nbsp;Vector w được tính bằng công thức

$w = (X^{T}X)^{+}X^{T}y$
<h3>
Bạn đang nghĩ gì?</h3>
Bạn vừa được học thuật toán Linear Regression nhiều biến. Như bạn đã thấy, thuật toán Linear Regression một biến chỉ là một trường hợp riêng của thuật toán Linear Regression nhiều biến.

Các công thức trong bài này cũng không có nhiều khác biệt so với bài Linear Regression một biến.
Sau khi đã nắm được thuật toán Linear Regression tổng quát, bạn hãy suy nghĩ lời giải cho vấn đề sau

Nếu các điểm dữ liệu của bộ dữ liệu đào tạo có xu hướng xếp thành một đường cong, mặt cong hoặc một <a href="https://en.wikipedia.org/wiki/Hypersurface" rel="noopener" target="_blank">siêu mặt</a> cong thì liệu có thể áp dụng thuật toán Linear Regression được không?