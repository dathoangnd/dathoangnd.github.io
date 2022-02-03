---
tag: learn
layout: post
title:  "Bài 1: Thuật Toán Linear Regression Một Biến"
description: "Bài này sẽ hướng dẫn bạn tìm hiểu thuật toán Linear Regression một biến - một thuật toán cơ bản và rất quan trọng trong Machine Learning."
---

Bài này sẽ hướng dẫn bạn tìm hiểu thuật toán Linear Regression một biến - một thuật toán cơ bản trong Machine Learning.

Bạn cũng sẽ được áp dụng thuật toán này trong một dự án thực tế ở bài tiếp theo.
<!--more-->
<h3>
Mở đầu</h3>
Linear Regression&nbsp;(Hồi quy tuyến tính) là thuật toán quan trọng và có nhiều ứng dụng trong thực tiễn.

Linear Regression thuộc loại Supervised Learning, trong đó giá trị của output là một hàm tuyến tính của các biến trong input. Tôi sẽ giải thích điều này rõ hơn trong các phần dưới đây.
<h4>
Linear Regression một biến</h4>
Nếu mỗi input chỉ chứa một biến thì thuật toán được gọi là Linear Regression một biến.

Quay lại bài toán tìm giá căn nhà đã được nhắc đến ở bài&nbsp;<a href="https://www.dathoangblog.com/2018/07/machine-learning-la-gi.html" rel="noopener" target="_blank">giới thiệu Machine Learning</a>, giá của mỗi căn nhà được giả định chỉ phụ thuộc vào một biến duy nhất là diện tích và bỏ qua các yếu tố khác. Nhiệm vụ của của ta là cài đặt một thuật toán để tìm ra đường thẳng biểu diễn sự phụ thuộc giữa giá nhà và diện tích một cách chính xác nhất.

Thuật toán ta cần sử dụng chính là Linear Regression một biến. Khi đó, ta có thể tìm ra được đường thẳng trên hệ trục tọa độ hai chiều biểu diễn sự phụ thuộc giữa giá nhà và diện tích. Ở đồ thị dưới đây, các điểm màu xanh ứng với các input cho trước, các input này chỉ chứa một biến duy nhất là diện tích; đường thẳng cần tìm là đường màu đỏ.


<div class="separator" style="clear: both; text-align: center;">
<a href="https://3.bp.blogspot.com/-Jyp0eyF7w2I/W0Vdyfq--FI/AAAAAAAAD1A/JiKhsD3G4gcsEF4HI0Fveis37bwwZGG2ACPcBGAYYCw/s1600/dsBuffer.bmp.jpg" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Thuật toán Machine Learning tìm giá nhà" border="0" data-original-height="336" data-original-width="500" src="https://3.bp.blogspot.com/-Jyp0eyF7w2I/W0Vdyfq--FI/AAAAAAAAD1A/JiKhsD3G4gcsEF4HI0Fveis37bwwZGG2ACPcBGAYYCw/s1600/dsBuffer.bmp.jpg" title="Thuật toán Machine Learning tìm giá nhà" /></a></div>


Phương trình đường thẳng trên có thể viết dưới dạng tổng quát như sau

$\widehat{P}(s) = w_{0} + w_{1}s$

với $\widehat{P}(s)$ là giá căn nhà diện tích s.

<em><strong>Lưu ý:</strong>&nbsp;Dấu mũ trong&nbsp;$\widehat{P}(s)$ có nghĩa là giá trị này là output được dự đoán từ input nhờ phương trình tìm ra bởi thuật toán. Đối với output thuộc các cặp (<strong>input</strong>, <strong>output</strong>) cho trước, ta không dùng dấu mũ. <strong>Đây là quy ước chung và được áp dụng mặc định từ giờ trở đi</strong>.</em>
<em>
</em> Do phương trình trên là một hàm tuyến tính và bài toán thuộc loại Regression nên thuật toán được gọi là Linear Regression. Điều này cũng đúng đối với Linear Regression nhiều biến.
<h4>
Linear Regression nhiều biến</h4>
Nếu mỗi input chứa nhiều hơn một biến thì thuật toán được gọi là Linear Regression nhiều biến.

Trong bài toán tìm giá nhà bằng Linear Regression một biến, ta đã lý tưởng hóa bài toán khi cho rằng giá nhà chỉ phụ thuộc vào diện tích. Trong thực tế, giá nhà còn phụ thuộc vào nhiều yếu tố khác như số phòng, vị trí, thời điểm.

Giả sử giá nhà phụ thuộc vào hai yếu tố là diện tích và khoảng cách tới trung tâm thành phố, khi đó thuật toán Linear Regression với hai biến có nhiệm vụ tìm ra mặt phẳng biểu diễn sự phụ thuộc giữa giá nhà với hai yếu tố trên một cách chính xác nhất.


<div class="separator" style="clear: both; text-align: center;">
<a href="https://4.bp.blogspot.com/-hWOGLO2sbFo/W0VjsbIb33I/AAAAAAAAD1g/yjnhCqynlyU5nlFwOkg-_Sprjq0_8RsUgCLcBGAs/s1600/figure_2.jpg" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Thuật toán Linear Regression nhiều biến" border="0" data-original-height="418" data-original-width="500" src="https://4.bp.blogspot.com/-hWOGLO2sbFo/W0VjsbIb33I/AAAAAAAAD1g/yjnhCqynlyU5nlFwOkg-_Sprjq0_8RsUgCLcBGAs/s1600/figure_2.jpg" title="Thuật toán Linear Regression nhiều biến" /></a></div>


Phương trình mặt phẳng trên có thể viết dưới dạng tổng quát như sau

$\widehat{P}(s, d) = w_{0} + w_{1}s + w_{2}d$

với $\widehat{P}(s, d)$ là giá căn nhà diện tích s và cách trung tâm thành phố khoảng cách d.

Trong trường hợp tổng quát, input bao gồm n biến $x_{1}, x_{2}, ..., x_{n}$ và output&nbsp;$\widehat{y}$ phụ thuộc vào n biến đó theo phương trình tuyến tính

$\widehat{y} =&nbsp;&nbsp;w_{0} + w_{1}x_{1} + ... +&nbsp;w_{n-1}x_{n-1} + w_{n}x_{n}$

thì thuật toán tìm ra phương trình ở trên gọi là Linear Regression n biến.

Để đơn giản hóa phương trình ở trên, ta có thể đặt w = $\begin{bmatrix}w_{0} \\\\ w_{1} \\\\ ... \\\\ w_{n} \end{bmatrix} $ là vector các hệ số của phương trình, x = $\begin{bmatrix}1 \\\\ x_{1} \\\\ ... \\\\ x_{n} \end{bmatrix}$ là vector các biến của input (phần tử 1 trong vector đóng vai trò như $x_{0}$ chỉ nhằm mục đích thuận tiện cho tính toán) thì có thể viết lại phương trình trên như sau

$\widehat{y} =&nbsp; x^{T}w$

Bài này sẽ chỉ trình bày thuật toán Linear Regression một biến. Thuật toán Linear Regression nhiều biến sẽ được nói đến trong một bài khác.
<h3>
Thuật toán Linear Regression một biến</h3>
<h4>
Mô hình toán học</h4>
Ta nhắc lại phương trình cần tìm trong thuật toán Linear Regression một biến

$\widehat{y} = w_{0} + w_{1}x_{1}$
$= x^{T}w$

với w =&nbsp;$\begin{bmatrix}w_{0} \\\\ w_{1} \end{bmatrix} $ và x =&nbsp;$\begin{bmatrix}1 \\\\ x_{1}\end{bmatrix}$

Với mỗi cặp giá trị ($w_{0}, w_{1}$) ta được một phương trình đường thẳng khác nhau biểu diễn sự phụ thuộc giữa $\widehat{y}$ và x, mỗi phương trình như vậy được gọi là một <b>phương trình giả thuyết</b> (hypothesis function).

Do phương trình giả thuyết dùng để dự đoán giá trị thực tế đối với một input mới nên ta có

$y \approx \widehat{y} = x^{T}w$

Các phương trình giả thuyết khác nhau sẽ có độ chính xác khác nhau. Trong hình dưới đây, rõ ràng đường màu đỏ có độ chính xác cao hơn đường màu xanh khi biểu diễn mối liên hệ giữa&nbsp;$\widehat{y}$ và x. Lưu ý là input x chỉ chứa một biến $x_{1}$.


<div class="separator" style="clear: both; text-align: center;">
<a href="https://1.bp.blogspot.com/-b_INKfWC7dk/W0VkaqU3ZWI/AAAAAAAAD1o/Pmpv6fIcB_08i5LBp-zUfOV-O9PPGSQQACLcBGAs/s1600/dsBuffer.jpg" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Các phương trình giả thuyết trong Linear Regression một biến" border="0" data-original-height="336" data-original-width="500" src="https://1.bp.blogspot.com/-b_INKfWC7dk/W0VkaqU3ZWI/AAAAAAAAD1o/Pmpv6fIcB_08i5LBp-zUfOV-O9PPGSQQACLcBGAs/s1600/dsBuffer.jpg" title="Các phương trình giả thuyết trong Linear Regression một biến" /></a></div>

Nhiệm vụ của thuật toán Linear Regression một biến là tìm đường thẳng liên hệ giữa $\widehat{y}$&nbsp; và x - hay nói cách khác là tìm ra w - một cách chính xác nhất. Nhưng trước hết, ta cần định nghĩa cụ thể độ chính xác của phương trình giả thuyết là gì đã.
<h4>
Độ chính xác của phương trình giả thuyết</h4>
Nói chung, ta không thể tìm được một đường thẳng đi qua tất cả các điểm input cho trước được (trừ khi chúng thẳng hàng). Do vậy với mỗi phương trình giả thuyết luôn có sự mất mát nhất định. Độ lớn của sự mất mát phụ thuộc các tham số&nbsp;($w_{0}, w_{1}$) và được tính bằng phương trình <strong>hàm mất mát</strong>&nbsp;(cost function) sau

$J(w_{0}, w_{1}) =&nbsp;\frac{1}{2m} \sum_{i=1}^{m} ( \widehat{y}^{(i)} - y^{(i)}) ^{2}$

$= \frac{1}{2m} \sum_{i=1}^{m} ( w_{0} + w_{1}x_{1}^{(i)} - y^{(i)}) ^{2}$

$= \frac{1}{2m} \sum_{i=1}^{m} ( x^{(i)T}w - y^{(i)}) ^{2}$

trong đó m là số input ban đầu được dùng để đào tạo thuật toán; ký hiệu $x_{1}^{(2)}$ có nghĩa là giá trị biến $x_{1}$ thuộc vào input thứ 2 trong bộ input ban đầu để đào tạo thuật toán. <strong>Các quy ước về ký hiệu này sẽ được sử dụng mặc định từ giờ trở đi</strong>.

Một cách hình học, hàm mất mát bằng một nửa trung bình cộng bình phương các khoảng cách sai lệch trong hình dưới đây.


<div class="separator" style="clear: both; text-align: center;">
<a href="https://3.bp.blogspot.com/-9L6VHpY5Z9U/W0VmfTJJDqI/AAAAAAAAD10/pc13ZRjlmhw8p7R3QxpybmA1uPgbC7ccACLcBGAs/s1600/1_yLeh6JjWHenfH4zFOA3HpQ.jpg" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Hàm mất mát trong Linear Regression" border="0" data-original-height="317" data-original-width="500" src="https://3.bp.blogspot.com/-9L6VHpY5Z9U/W0VmfTJJDqI/AAAAAAAAD10/pc13ZRjlmhw8p7R3QxpybmA1uPgbC7ccACLcBGAs/s1600/1_yLeh6JjWHenfH4zFOA3HpQ.jpg" title="Hàm mất mát trong Linear Regression" /></a></div>


Ta thậm chí còn có thể đơn giản hóa hàm mất mát hơn nữa bằng cách đặt X = $\begin{bmatrix}1 &amp; x_{1}^{(1)} \\\\ 1 &amp; x_{1}^{(2)} \\\\ ... &amp; ... \\\\ 1 &amp; x_{1}^{(m)} \end{bmatrix}$ là ma trận với mỗi hàng là một input (hàng i ứng với $x^{(i)T}$), đặt y = $\begin{bmatrix}y^{(1)} \\\\ y^{(2)} \\\\ ... \\\\ y^{(m)} \end{bmatrix}$ là vector các output thì hàm mất mát được viết lại thành

$J(w) = \frac{1}{2m}&nbsp;\parallel Xw - y \parallel ^{2}$

Xin được nhắc lại nếu bạn quên, ký hiệu $\parallel Xw - y \parallel$ là độ dài của vector Xw - y.

<em><strong>Lưu ý:</strong>&nbsp;Nếu bạn thắc mắc tại sao chỉ lấy một nửa, đó là do khi khảo sát hàm mất mát, việc lấy đạo hàm của một bình phương sẽ phải nhân hệ số 2 và nó sẽ bù trừ cho $\frac{1}{2}$ giúp đạo hàm trở nên đơn giản hơn.</em>
<h4>
Nghiệm của thuật toán Linear Regression một biến</h4>
Việc tìm nghiệm của thuật toán Linear Regression một biến chính là&nbsp;tìm ra tham số w =&nbsp;$\begin{bmatrix}w_{0} \\\\ w_{1} \end{bmatrix} $ để hàm mất mát có giá trị nhỏ nhất.

Việc này có thể thực hiện được bằng cách tính đạo hàm và khảo sát hảm mất mát theo hai biến $w_{0}$ và $w_{1}$. Bạn đã được học điều này trong môn Giải tích I.

Trong bài này, để tránh làm bạn đau đầu với quá nhiều phép tính toán, tôi xin được bỏ qua quá trình khảo sát nhàm chán này và đưa ra ngay phương trình của w để hàm mất mát đạt giá trị nhỏ nhất

$X^{T}Xw = X^{T}y$

$X^{T}X$ là một ma trận vuông và nếu nó khả nghịch ta có tính ngay được w bằng công thức

$w = (X^{T}X)^{-1}X^{T}y$

Với bài này, do chỉ có 1 biến duy nhất nên $X^{T}X$ luôn khả nghịch. Song để đồng bộ công thức với bài <a href="https://www.dathoangblog.com/2018/07/linear-regression-nhieu-bien.html" rel="noopener" target="_blank">Thuật toán Linear Regression nhiều biến</a>&nbsp;ta sẽ sử dụng <b>ma trận giả đảo</b>.

Ma trận giả đảo của ma trận A được ký hiệu là $A^{+}$ và có một số tính chất tương tự ma trận nghịch đảo

$AA^{+}A = A$
$A^{+}AA^{+} = A^{+}$

Đối với mọi ma trận, ma trận giả đảo luôn tồn tại và là duy nhất. Nếu ma trận là khả nghịch thì ma trận giả đảo và ma trận nghịch đảo sẽ trùng nhau. Như vậy một cách gần đúng có thể nói ma trận nghịch đảo chỉ là một trường hợp riêng của ma trận giả đảo.

Bạn có thể tự tìm hiểu thêm về <a href="https://en.wikipedia.org/wiki/Moore%E2%80%93Penrose_inverse" rel="noopener" target="_blank">ma trận giả đảo</a>. Bạn cũng không cần phải tính toán ma trận giả đảo, tốt nhất bạn nên sử dụng hàm có sẵn trong thư viện để tiết kiệm công sức.

Tóm lại, ta có công thức cuối cùng của w để hàm mất mát đạt giá trị nhỏ nhất dưới đây

$w = (X^{T}X)^{+}X^{T}y$
<h3>
Tóm tắt thuật toán Linear Regression một biến</h3>
Để giúp bạn dễ nhớ thuật toán Linear Regression một biến, trong phần này tôi sẽ tóm tắt lại các bước cài đặt thuật toán
<h4>
Yêu cầu</h4>
Cho trước m bộ dữ liệu để đào tạo thuật toán. Bộ dữ liệu thứ i chứa input $x^{(i)}$ và output $y^{(i)}$, trong đó input thứ i chỉ chứa một biến duy nhất $x^{(i)}_{1}$. Nhiệm vụ của ta là tìm ra mối liên hệ giữa input và output bằng một hàm tuyến tính để khi đưa vào một input mới, ta có thể dự đoán được output ứng với nó

$\widehat{y} = w_{0} + w_{1}x_{1}$

<div class="separator" style="clear: both; text-align: center;">
<a href="https://1.bp.blogspot.com/-ShAscH0ZJ_s/W0VoXBDxl-I/AAAAAAAAD2E/t2p9IhXinuAHK3mLV6B0obS6q78b8CE5QCPcBGAYYCw/s1600/dsBuffer-Recovered.jpg" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Linear Regression một biến" border="0" data-original-height="336" data-original-width="500" src="https://1.bp.blogspot.com/-ShAscH0ZJ_s/W0VoXBDxl-I/AAAAAAAAD2E/t2p9IhXinuAHK3mLV6B0obS6q78b8CE5QCPcBGAYYCw/s1600/dsBuffer-Recovered.jpg" title="Linear Regression một biến" /></a></div>

<h4>
</h4>
<h4>
Thuật toán</h4>
<strong>Bước 1:&nbsp;</strong>Thiết lập các ma trận và vector dưới đây

w = $\begin{bmatrix}w_{0} \\\\ w_{1} \end{bmatrix} $

X = $\begin{bmatrix}1 &amp; x_{1}^{(1)} \\\\ 1 &amp; x_{1}^{(2)} \\\\ ... &amp; ... \\\\ 1 &amp; x_{1}^{(m)} \end{bmatrix}$

y = $\begin{bmatrix}y^{(1)} \\\\ y^{(2)} \\\\ ... \\\\ y^{(m)} \end{bmatrix}$

<strong>Bước 2:</strong>&nbsp;Vector w được tính bằng công thức

$w = (X^{T}X)^{+}X^{T}y$
<h3>
Bạn đang nghĩ gì?</h3>
Bạn vừa được học thuật toán Linear Regression một biến - một thuật toán cơ bản và quan trọng.

Trong bài tiếp theo, chúng ta sẽ bắt đầu đụng chạm đến code và <a href="https://www.dathoangblog.com/2018/07/ung-dung-linear-regression-mot-bien.html" rel="noopener" target="_blank">ứng dụng thuật toán Linear Regression một biến</a> để giải quyết bài toán thực tế. Thực hành luôn là cách học tốt nhất!

Bạn cũng sẽ được học <a href="https://www.dathoangblog.com/2018/07/linear-regression-nhieu-bien.html" rel="noopener" target="_blank">thuật toán Linear Regression nhiều biến</a> và <a href="https://www.dathoangblog.com/2018/07/nonlinear-regression.html" rel="noopener" target="_blank">thuật toán Nonlinear Regression</a> (Hồi quy phi tuyến tính) trong khóa học này.

Để kết thúc bài này, xin hỏi bạn vài câu

Bạn đã từng gặp vấn đề nào có thể giải quyết bằng Linear Regression một biến chưa?

Bạn có định sử dụng Linear Regression trong dự án nào đó hay không?