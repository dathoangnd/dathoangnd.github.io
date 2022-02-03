---
tag: learn
layout: post
title:  "Bài 7: Thuật Toán Gradient Descent"
description: "Bài này sẽ hướng dẫn bạn tìm hiểu thuật toán Gradient Descent - một thuật toán có nhiều ứng dụng trong các lĩnh vực khoa học, đặc biệt là Machine Learning."
---

Bài này sẽ hướng dẫn bạn tìm hiểu thuật toán Gradient Descent, một thuật toán có nhiều ứng dụng trong các lĩnh vực khoa học, đặc biệt là Machine Learning.

Thuật toán Gradient Descent có ưu thế trong các bài toán Machine Learning mà số lượng dữ liệu đào tạo rất lớn.

Bạn sẽ được áp dụng thuật toán này cùng với Linear Regression ở bài tiếp theo.
<!--more-->
<h3>
Vấn đề đối với các thuật toán Machine Learning</h3>
Cho đến thời điểm này, bạn đã được học 3 thuật toán Machine Learning là <a href="https://www.dathoangblog.com/2018/07/linear-regression-mot-bien.html" rel="noopener" target="_blank">Linear Regression một biến</a>, <a href="https://www.dathoangblog.com/2018/07/linear-regression-nhieu-bien.html" rel="noopener" target="_blank">Linear Regression nhiều biến</a> và <a href="https://www.dathoangblog.com/2018/07/nonlinear-regression.html" rel="noopener" target="_blank">Nonlinear Regression</a>.

Qua các bài thực hành, bạn đã được áp dụng những thuật toán này để giải quyết các bài toán thực tế. Xin chúc mừng bạn đã đi được một chặng đường dài. Tôi tin rằng bằng sự kiên trì, bất cứ ai cũng có thể làm nên những điều lớn lao.

Hãy cùng xem lại <a href="https://www.dathoangblog.com/2018/07/linear-regression-nhieu-bien.html" rel="noopener" target="_blank">thuật toán Linear Regression nhiều biến</a>.

Hàm mất mát của thuật toán là

$J(w) =&nbsp;\frac{1}{2m} \sum_{i=1}^{m} ( \widehat{y}^{(i)} - y^{(i)}) ^{2}$

$= \frac{1}{2m} \sum_{i=1}^{m} ( wx^{(i)} - y^{(i)}) ^{2}$

$= \frac{1}{2m}&nbsp;\parallel Xw - y \parallel ^{2}$

với&nbsp;w = $\begin{bmatrix}w_{0} \\\\ w_{1} \\\\ ... \\\\ w_{n} \end{bmatrix} $,&nbsp;X = $\begin{bmatrix}1 &amp; x_{1}^{(1)}&nbsp;&amp; ... &amp; x_{n}^{(1)}&nbsp;\\\\1 &amp; x_{1}^{(2)} &amp; ... &amp; x_{n}^{(2)} \\\\... &amp; ... &amp; ... &amp; ... \\\\1 &amp; x_{1}^{(m)} &amp; ... &amp; x_{n}^{(m)}\end{bmatrix}$ và y = $\begin{bmatrix}y^{(1)} \\\\ y^{(2)} \\\\ ... \\\\ y^{(m)} \end{bmatrix}$

Nhiệm vụ của ta là tìm vector w sao cho hàm mất mát J(w) nhỏ nhất.

Bằng phương pháp của Giải tích, ta tính <a href="https://vi.wikipedia.org/wiki/%C4%90%E1%BA%A1o_h%C3%A0m_ri%C3%AAng" rel="noopener" target="_blank">đạo hàm riêng</a> theo từng biến $w_{0}, w_{1}, ..., w_{n}$, giải hệ các đạo hàm riêng bằng 0 và tìm được nghiệm

$w = (X^{T}X)^{+}X^{T}y$

Ở đây có hai vấn đề cần xem xét

<strong>Thứ nhất</strong>, nếu m và n lớn thì các ma trận và vector trên sẽ rất lớn. Điều này chẳng những tốn bộ nhớ mà quá trình tính toán còn trở nên chậm chạp. Nếu m, n không quá lớn, công thức trên là cách đơn giản nhất để giải quyết bài toán, ngược lại, ta sẽ cần một cách khác tối ưu hơn.

<strong>Thứ hai</strong>, khi khảo sát hàm mất mát, để tìm điểm cực tiểu ta giải hệ các đạo hàm riêng bằng 0. Đối với phương trình tuyến tính việc này rất đơn giản và ta tìm ra được nghiệm như trên. Nhưng trong nhiều thuật toán, hàm mất mát phức tạp hơn và cách giải đó trở nên quá khó hoặc bất khả thi. Ta cần phương pháp tổng quát hơn để tìm điểm cực trị của hàm bất kỳ, hay trong trường hợp này là tìm cực tiểu.

Thuật toán Gradient Descent giải quyết cả hai vấn đề trên.
<h3>
Thuật toán Gradient Descent</h3>
Thuật toán Gradient Descent dùng để tìm điểm cực trị của hàm số.

Đối với nhiều hàm số, việc khảo sát bằng cách tính đạo hàm rất khó khăn hoặc bất khả thi, Gradient Descent cung cấp một phương thức tổng quát cho những trường hợp này.
<h4>
Gradient Descent với hàm một biến</h4>
Ta xem xét hiện tượng sau

<div class="separator" style="clear: both; text-align: center;">
<a href="https://2.bp.blogspot.com/-jrJGcYa4N_k/W0WAmMSkHOI/AAAAAAAAD4o/RkYkXx8MGw0g5NnGG4iT3hatkPEcYOWfgCLcBGAs/s1600/ezgif.com-resize.gif" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" data-original-height="313" data-original-width="500" src="https://2.bp.blogspot.com/-jrJGcYa4N_k/W0WAmMSkHOI/AAAAAAAAD4o/RkYkXx8MGw0g5NnGG4iT3hatkPEcYOWfgCLcBGAs/s1600/ezgif.com-resize.gif" /></a></div>



Quả bóng đang lăn xuống dốc. Trong một môi trường vật lý mà ta giả định thì quả bóng lăn xuống càng nhanh khi dốc càng đứng (mặc dù không phải vậy) và khi xuống đến chân dốc thì quả bóng dừng lại.

Hiện tượng này rất dễ hình dung và giúp bạn hiểu tư tưởng của Gradient Descent.

Xét hàm số y = f(x) và ta cần tìm điểm cực tiểu của hàm số.

Xuất phát từ điểm x bất kỳ, ta cần điều chỉnh x để nó có xu hướng tiến về điểm mà hàm số đạt cực tiểu. Điều này có thể đạt được bằng cách lặp lại liên tiếp phép biến đổi

<i>x := x - αf'(x)</i>

với ký hiệu := mượn từ ngôn ngữ Pascal nghĩa là gán giá trị vế phải cho biến bên trái.

Một cách hình ảnh, khi f'(x) &gt; 0 thì đồ thị dốc sang trái, x có xu hướng giảm để "xuống dốc"; khi f'(x) &lt; 0 thì đồ thị dốc sang phải, x có xu hướng tăng cũng để "xuống dốc"; khi f'(x) = 0 thì x nằm ở "chân dốc" và ta tìm được điểm cực tiểu của hàm số.


<div class="separator" style="clear: both; text-align: center;">
<a href="https://3.bp.blogspot.com/-sfuanZ1tu3A/W0WBJsEKIHI/AAAAAAAAD4w/pt6bJDp076k_4iwMRWnH9emmWtmrTuceACLcBGAs/s1600/sgd_optimal.jpg" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Minh họa thuật toán Gradient Descent" border="0" data-original-height="142" data-original-width="500" src="https://3.bp.blogspot.com/-sfuanZ1tu3A/W0WBJsEKIHI/AAAAAAAAD4w/pt6bJDp076k_4iwMRWnH9emmWtmrTuceACLcBGAs/s1600/sgd_optimal.jpg" title="Minh họa thuật toán Gradient Descent" /></a></div>

<p>Thông thường, ta không thể thực hiện phép lặp đến khi f'(x) = 0 được mà khi |f'(x)| rất nhỏ ta coi như đã tìm được điểm cực tiểu.</p>

Trong phép biến đổi trên,&nbsp;α được gọi là <strong>learning rate.</strong> Learning rate càng lớn thì mỗi "bước nhảy" của x sẽ càng lớn và số lần lặp cần thiết để tìm được điểm cực tiểu sẽ giảm đi. Tuy nhiên nếu learning rate quá lớn thì có thể sau mỗi lần lặp x càng cách xa điểm cực tiểu và ta không thể tìm được điểm cực tiểu.


<div class="separator" style="clear: both; text-align: center;">
<a href="https://2.bp.blogspot.com/-kHHuUXW4A2o/W0WBXeeydSI/AAAAAAAAD40/bxTS06cr-1sSpRYXPwZ41oO-aJG1cPtWwCLcBGAs/s1600/Screen-Shot-2018-02-24-at-11.47.09-AM.jpg" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Ảnh hưởng của learning rate" border="0" data-original-height="194" data-original-width="500" src="https://2.bp.blogspot.com/-kHHuUXW4A2o/W0WBXeeydSI/AAAAAAAAD40/bxTS06cr-1sSpRYXPwZ41oO-aJG1cPtWwCLcBGAs/s1600/Screen-Shot-2018-02-24-at-11.47.09-AM.jpg" title="Ảnh hưởng của learning rate" /></a></div>


Vì lý do đó việc chọn learning rate phù hợp là rất quan trọng. Ta có thể thử nhiều giá trị learning rate khác nhau để tìm ra giá trị learning rate đủ tốt (chứ không cần phải tốt nhất).

Thuật toán Gradient Descent dùng để tìm ra điểm mà hàm số đạt <a href="https://vi.wikipedia.org/wiki/C%E1%BB%B1c_tr%E1%BB%8B_c%E1%BB%A7a_h%C3%A0m_s%E1%BB%91" rel="noopener" target="_blank">cực tiểu</a> chứ không phải đạt giá trị nhỏ nhất. Đối với hàm số có nhiều cực tiểu thì tùy thuộc vào vị trí điểm chọn ban đầu, ta có thể tìm được kết quả khác nhau.


<div class="separator" style="clear: both; text-align: center;">
<a href="https://3.bp.blogspot.com/-tyEpDCg7nS0/W0WBjpcp-VI/AAAAAAAAD48/pvMaHts-l9MXrKizC0MyDmRnILpbFj4_QCLcBGAs/s1600/Polynomial-Gradient-Descent-Capatin-Kirk.jpg" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Ảnh hướng của điểm ban đầu với kết quả của Gradient Descent" border="0" data-original-height="269" data-original-width="500" src="https://3.bp.blogspot.com/-tyEpDCg7nS0/W0WBjpcp-VI/AAAAAAAAD48/pvMaHts-l9MXrKizC0MyDmRnILpbFj4_QCLcBGAs/s1600/Polynomial-Gradient-Descent-Capatin-Kirk.jpg" title="Ảnh hướng của điểm ban đầu với kết quả của Gradient Descent" /></a></div>


Trong hình ở trên, nếu ta xuất phát từ vị trí thứ nhất thì thuật toán sẽ dừng lại khi di chuyển đến A, nếu xuất phát từ vị trí thứ hai thì thuật toán dừng lại tại B, nếu xuất phát từ vị trí thứ ba thì thuật toán dừng lại tại C.

Đối với thuật toán Linear Regression, thật may mắn khi hàm mất mát của nó chỉ có một cực tiểu. Do đó ta có thể dùng Gradient Descent để tìm điểm cực tiểu đó cũng chính là điểm mà hàm mất mát đạt giá trị nhỏ nhất. Đây chính xác là những gì chúng ta sẽ làm ở bài <a href="https://www.dathoangblog.com/2018/07/ung-dung-gradient-descent.html" rel="noopener" target="_blank">ứng dụng thuật toán Gradient Descent</a>.
<h4>
Gradient Descent với hàm nhiều biến</h4>
Xét hàm số $y = f(x_{1}, x_{2}, ..., x_{n})$ và ta cần tìm điểm cực tiểu của hàm số.

Hoàn toàn tương tự như với hàm một biến, xuất phát từ một điểm $(x_{1}, x_{2}, ..., x_{n})$ bất kỳ ta thực hiện lặp lại các phép biến đổi

<i>$x_{1} := x_{1} - α f'_{x_1}(x_1, x_2, ..., x_n)$</i>

<i>...</i>

<i>$x_{n} := x_{n} - α f'_{x_n}(x_1, x_2, ..., x_n)$</i>

Một cách hình ảnh, điểm ta đang xét sẽ từ từ lăn "xuống hố" và dừng lại khi nó ở "đáy hố". Khi đó ta tìm được điểm cực tiểu của hàm số.


<div class="separator" style="clear: both; text-align: center;">
<a href="https://4.bp.blogspot.com/-60S9yFSNstc/W0WB9O1ruPI/AAAAAAAAD5M/sXKA3PoVFgUR-axLLuUSlcs6rD0gcP3KwCLcBGAs/s1600/gradient.jpg" imageanchor="1"><img alt="Minh họa Gradient Descent với hàm nhiều biến" border="0" data-original-height="295" data-original-width="500" src="https://4.bp.blogspot.com/-60S9yFSNstc/W0WB9O1ruPI/AAAAAAAAD5M/sXKA3PoVFgUR-axLLuUSlcs6rD0gcP3KwCLcBGAs/s1600/gradient.jpg" title="Minh họa Gradient Descent với hàm nhiều biến" /></a></div>


Cũng giống như hàm một biến, nếu chọn learning rate quá nhỏ, thuật toán cần rất nhiều lần lặp để kết thúc; nếu learning rate quá lớn, điểm ta xét sẽ "lăn ngược lên dốc" và ta không thể tìm được điểm cực tiểu được.

Đối với hàm nhiều biến có nhiều cực tiểu, tùy thuộc vào vị trí chọn ban đầu mà ta có thể tìm được kết quả khác nhau.

<div class="separator" style="clear: both; text-align: center;">
<a href="https://3.bp.blogspot.com/-S_qFVHxLaKY/W0WCWqs_HTI/AAAAAAAAD5Y/oXaELJs_Q58epS-zCJkYeM9-_SVjk0x6wCPcBGAYYCw/s1600/ezgif.com-optimize.gif" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Ảnh hướng của điểm ban đầu với kết quả của Gradient Descent" border="0" data-original-height="375" data-original-width="500" src="https://3.bp.blogspot.com/-S_qFVHxLaKY/W0WCWqs_HTI/AAAAAAAAD5Y/oXaELJs_Q58epS-zCJkYeM9-_SVjk0x6wCPcBGAYYCw/s1600/ezgif.com-optimize.gif" title="Ảnh hướng của điểm ban đầu với kết quả của Gradient Descent" /></a></div>

<h3>
Bình thường hóa dữ liệu</h3>
Nếu bạn còn nhớ ở bài <a href="https://www.dathoangblog.com/2018/07/nonlinear-regression.html" target="_blank">thuật toán Nonlinear Regression</a>, chúng ta đã đặt ẩn phụ để tự tạo ra biến mới trước khi cài đặt thuật toán.

Một ý tưởng tương tự được áp dụng với Gradient Descent giúp thuật toán hiệu quả hơn.

Giả sử ta sử dụng thuật toán Gradient Descent để tìm điểm cực tiểu của hàm số $y = f(x_{1}, x_{2}, x_{3})$ mà các biến $x_{1}, x_{2}, x_{3}$ có phổ giá trị rất chênh lệch. Lấy ví dụ $x_{1}$ dao động từ -5 tới 5, $x_{2}$ dao động từ -10000 tới 20000, $x_{3}$ dao động từ 0.001 tới 0.003

Do phổ giá trị của $x_{3}$ rất nhỏ nên ta cần chọn&nbsp;α rất nhỏ để các "bước nhảy" rất nhỏ, tránh hiện tượng "leo ngược dốc" đã nói ở trên. Nhưng do phổ giá trị của $x_{2}$ lại rất lớn nên thuật toán sẽ cần rất nhiều "bước nhảy" để đưa ra được kết quả.

Để giúp thuật toán nhanh chóng hơn, ta cần thêm một bước xử lý dữ liệu gọi là Bình thường hóa dữ liệu (Feature Normalization).

Ta sẽ đưa các biến về phổ giá trị tương đương bằng các biến đổi

$x_{1} =&nbsp;\frac{x_{1} -&nbsp; \mu_{1}}{s_{1}}$

$x_{2} =&nbsp;\frac{x_{2} -&nbsp; \mu_{2}}{s_{2}}$

$x_{3} =&nbsp;\frac{x_{3} -&nbsp; \mu_{3}}{s_{3}}$

trong đó ký hiệu $\mu_{i}$ là giá trị trung bình của $x_{i}$ trong tất cả các input, $s_{i}$ là độ rộng phổ giá trị (hiệu giữa giá trị lớn nhất và nhỏ nhất) hoặc <a href="https://vi.wikipedia.org/wiki/%C4%90%E1%BB%99_l%E1%BB%87ch_chu%E1%BA%A9n" target="_blank">độ lệch chuẩn</a> của $x_{i}$ trong tất cả các input.

Các biến đổi trên sẽ đưa các giá trị $x_{i}$ về khoảng dao động xung quanh 0 và độ rộng tùy thuộc vào cách chọn $s_{i}$. Ngoài việc giúp các biến có độ rộng phổ giá trị tương đương, nó còn tăng độ chính xác tính toán do biểu diễn số thực trong máy tính có xu hướng tập trung mật độ cao quanh 0.

Khi sử dụng kết quả thu được bằng thuật toán Gradient Descent đã bình thường hóa dữ liệu, ta cũng phải bình thường hóa input mới thì output dự đoán mới chính xác.

Bình thường hóa dữ liệu chỉ cần thiết khi phổ giá trị các biến quá chênh lệch. Nếu sự chênh lệch khoảng vài chục lần thì có thể bỏ qua bước này. Nhưng nếu chênh lệch hàng ngàn lần thì việc bình thường hóa dữ liệu có thể tăng tốc Gradient Descent rất đáng kể.
<h3>
Thuật toán thay thế Gradient Descent</h3>

Gradient Descent tương đối linh hoạt để áp dụng với cả những bài toán phức tạp. Tuy nhiên nhược điểm của nó là ta cần chọn giá trị learning rate α phù hợp, quá trình thực hiện qua rất nhiều bước lặp và có thể tốn nhiều thời gian nếu α quá nhỏ.

Ta có thể sử dụng một số thuật toán khác như <b><a href="https://en.wikipedia.org/wiki/Conjugate_gradient_method" target="_blank">Conjugate Gradient</a></b>, <b><a href="https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm" target="_blank">BFGS</a></b>, <b><a href="https://en.wikipedia.org/wiki/Limited-memory_BFGS" target="_blank">L-BFGS</a></b>&nbsp;thay cho Gradient Descent để tìm cực trị hàm số. Ưu điểm của chúng là không cần phải chọn giá trị α và thường tốc độ thực hiện nhanh hơn. Nhưng nhược điểm là chúng quá phức tạp để cài đặt thủ công và thông thường chúng ta sẽ sử dụng thư viện có sẵn để cài đặt các thuật toán này.
<h3>
Tóm tắt thuật toán Gradient Descent</h3>
Trong bài này không có nhiều lý thuyết phức tạp. Tuy nhiên, giống như mọi bài khác, tôi luôn dành ra một mục để tóm tắt lại các bước sử dụng thuật toán giúp bạn nhanh chóng nắm bắt và dễ dàng áp dụng trong các bài toán thực tế.
<h4>
Yêu cầu</h4>
Cho hàm số $y = f(x_{1}, x_{2}, ..., x_{n})$. Hãy tìm ra một điểm cực trị của nó.
<h4>
Thuật toán</h4>

<b>Bước 0:</b> Bình thường hóa dữ liệu nếu cần thiết.

<strong>Bước 1:</strong>&nbsp;Chọn một điểm bất kỳ&nbsp;$(x_{1}, x_{2}, ..., x_{n})$ và một giá trị learning rate&nbsp;α.

<strong>Bước 2:</strong>&nbsp;Liên tiếp lặp lại các phép biến đổi

<i>$x_{1} := x_{1} - \alpha f'_{x_1}(x_1, x_2, ..., x_n)$</i>

<i>...</i>

<i>$x_{n} := x_{n} - \alpha f'_{x_n}(x_1, x_2, ..., x_n)$</i>

<strong>Bước 3:</strong> Thuật toán dừng lại khi y thay đổi rất nhỏ hoặc trị tuyệt đối các đạo hàm riêng rất nhỏ. Nếu thuật toán không thể kết thúc thì chọn giá trị&nbsp;α nhỏ hơn rồi quay lại bước 2.
<h3>
Bạn đang nghĩ gì?</h3>
Bạn vừa được học thuật toán Gradient Descent - một phương pháp tương đối tổng quát để tìm cực trị của hàm số bất kỳ.

Thuật toán Gradient Descent có lợi thế khi việc khảo sát hàm số để tìm cực trị là quá khó hoặc quá phức tạp.

Gradient Descent cũng có nhiều nhược điểm. Ta cần phải lựa chọn giá trị&nbsp;α phù hợp. Nếu&nbsp;α quá nhỏ thì thuật toán sẽ cần rất nhiều bước để kết thúc. Nếu&nbsp;α quá lớn thì thuật toán có thể không kết thúc được.

Nếu ta chọn điểm xuất phát mà trong lân cận của nó hàm số không đổi thì Gradient Descent sẽ kết thúc chỉ sau một lần lặp mà không đưa ra được kết quả chính xác. Đây cũng là hạn chế của Gradient Descent. Tuy nhiên, với các thuật toán Machine Learning mà ta học trong khóa học này, sẽ không có trường hợp nào như vậy.

Điều cuối cùng, Gradient Descent thường được gắn với các ứng dụng trong Machine Learning, nhưng bạn cần hiểu là nó có thể áp dụng với bất cứ trường hợp nào cần tìm cực trị của hàm số.

Bạn có nhận xét gì về Gradient Descent, liệu nó còn ưu nhược điểm nào nữa hay không?