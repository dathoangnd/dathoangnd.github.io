---
layout: post
title:  "Bài 5: Thuật Toán Nonlinear Regression"
description: "Bài này sẽ hướng dẫn bạn tìm hiểu thuật toán Nonlinear Regression trong Machine Learning - thuật toán dự đoán thông tin mới dựa trên dữ kiện cho trước."
---

Bài này sẽ hướng dẫn bạn tìm hiểu thuật toán&nbsp;Nonlinear Regression - thuật toán tổng quát hơn của <a href="https://www.dathoangblog.com/2018/07/linear-regression-mot-bien.html" rel="noopener" target="_blank">Linear Regression</a>.

Bằng thuật toán này, chúng ta có thể dự đoán được thông tin mới dựa trên các dữ liệu cho trước khi thuật toán Linear Regression không áp dụng được hoặc cho kết quả quá sai lệch.

Bạn cũng sẽ được <a href="https://www.dathoangblog.com/2018/07/ung-dung-nonlinear-regression.html" rel="noopener" target="_blank">ứng dụng thuật toán Nonlinear Regression</a> trong một dự án thực tế ở bài tiếp theo.
<!--more-->
<h3>
Vấn đề đối với thuật toán Linear Regression</h3>
Trong bài <a href="https://www.dathoangblog.com/2018/07/linear-regression-nhieu-bien.html" rel="noopener" target="_blank">Linear Regression nhiều biến</a>, tôi đã đặt một câu hỏi cho bạn là:

<i>Nếu các điểm dữ liệu của bộ dữ liệu đào tạo có xu hướng xếp thành một đường cong, mặt cong hoặc một siêu mặt cong thì liệu có thể áp dụng thuật toán Linear Regression được không?</i>

Tôi hy vọng bạn sẽ trả lời là <strong>không</strong>.

Thuật toán Linear Regression chỉ chính xác nếu các điểm dữ liệu có xu hướng xếp thành đường thẳng, mặt phẳng hoặc <a href="https://en.wikipedia.org/wiki/Hypersurface" rel="noopener" target="_blank">siêu mặt</a>&nbsp;phẳng. Nhiệm vụ của thuật toán Linear Regression là tìm ra phương trình tuyến tính biểu diễn đường thẳng, mặt phẳng hay siêu mặt phẳng ấy.

Nếu các điểm dữ liệu có xu hướng xếp thành đường cong, mặt cong hoặc siêu mặt cong mà ta vẫn áp dụng thuật toán Linear Regression thì hàm mất mát sẽ có giá trị rất lớn, hay nói cách khác sự sai lệch trong kết quả là rất lớn.

<div class="separator" style="clear: both; text-align: center;">
<a href="https://2.bp.blogspot.com/-7wwMX1g0toU/W0V5OtUxU7I/AAAAAAAAD3c/F17P7iGfxBQaUTdz29v4hhmly8N_FXa-gCLcBGAs/s1600/linear-nonlinear-relationships.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Linear vs Nonlinear" border="0" data-original-height="179" data-original-width="500" src="https://2.bp.blogspot.com/-7wwMX1g0toU/W0V5OtUxU7I/AAAAAAAAD3c/F17P7iGfxBQaUTdz29v4hhmly8N_FXa-gCLcBGAs/s1600/linear-nonlinear-relationships.png" title="Linear vs Nonlinear" /></a></div>

Trong trường hợp này, thay vì tìm một phương trình giả thuyết dạng tuyến tính biểu diễn quy luật phân bố của các điểm dữ liệu ta tìm phương trình <strong>phi tuyến tính</strong>.

Rất dễ dàng để lấy ví dụ các phương trình phi tuyến tính

$\widehat{y} =&nbsp;&nbsp;3 + x_{1}^{2} + 2x_{2} - \sqrt{x_{1}x_{2}} $

$\widehat{y} =&nbsp;&nbsp;sin x_{1} + cos x_{2} $

$\widehat{y} =&nbsp;&nbsp;ln x_{1} - x_{2} $

Thuật toán tìm ra phương trình giả thuyết của các điểm dữ liệu không phải dạng tuyến tính gọi là thuật toán&nbsp;<strong>Nonlinear Regression</strong> (Hồi quy phi tuyến tính).
<h3>
Thuật toán Nonlinear Regression</h3>
<h4>
Mô hình toán học</h4>
Ta nhắc lại phương trình cần tìm trong thuật toán Linear Regression một biến

$\widehat{y} = w_{0} + w_{1}x_{1}$
$= x^{T}w$

với w =&nbsp;$\begin{bmatrix}w_{0} \\\\ w_{1} \end{bmatrix} $ và x =&nbsp;$\begin{bmatrix}1 \\\\ x_{1}\end{bmatrix}$

Đây là phương trình của đường thẳng và chỉ có hiệu quả khi các điểm dữ liệu có xu hướng xếp thành đường thẳng. Trong trường hợp các điểm dữ liệu có xu hướng xếp thành đường cong thì nói chung sai khác sẽ rất lớn.

<div class="separator" style="clear: both; text-align: center;">
<a href="https://4.bp.blogspot.com/-0Qnba7zZEUw/W0V51S7T1II/AAAAAAAAD3o/2z1DAPuNVv8HdMcLJaRRKYR_0Wbvx1MfgCLcBGAs/s1600/scattter-plot-linear-regression-in-python.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Linear Regression không phù hợp" border="0" data-original-height="306" data-original-width="500" src="https://4.bp.blogspot.com/-0Qnba7zZEUw/W0V51S7T1II/AAAAAAAAD3o/2z1DAPuNVv8HdMcLJaRRKYR_0Wbvx1MfgCLcBGAs/s1600/scattter-plot-linear-regression-in-python.png" title="Linear Regression không phù hợp" /></a></div>



Lúc này, thay vì tìm phương trình đường thẳng, ta có thể tìm phương trình đường cong để phương trình giả thuyết biểu diễn chính xác hơn và giảm thiểu sự mất mát.

<div class="separator" style="clear: both; text-align: center;">
<a href="https://1.bp.blogspot.com/-UX8WNUSNTKw/W0V6AmorkgI/AAAAAAAAD3s/SRYUkU6P3QQkFY1HvbxxTsa4GbgwYlDGgCLcBGAs/s1600/scattter-plot-linear-regression-in-python-1.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Thuật toán Nonlinear Regression" border="0" data-original-height="306" data-original-width="500" src="https://1.bp.blogspot.com/-UX8WNUSNTKw/W0V6AmorkgI/AAAAAAAAD3s/SRYUkU6P3QQkFY1HvbxxTsa4GbgwYlDGgCLcBGAs/s1600/scattter-plot-linear-regression-in-python-1.png" title="Thuật toán Nonlinear Regression" /></a></div>


Giả sử ta tìm phương trình đa thức bậc 3

$\widehat{y} = w_{0} + w_{1}x_{1} + w_{2}x_{1}^{2} + w_3x_{1}^{3}$

Bằng cách đặt $u_{1} =&nbsp;x_{1}, u_{2} =&nbsp;x_{1}^{2}, u_{3} =&nbsp;x_{1}^{3}$ ta lại đưa về được việc tìm phương trình tuyến tính với 3 biến mới $u_{1}, u_{2}, u_{3}$

$\widehat{y} = w_{0} + w_{1}u_{1} + w_{2}u_{2} + w_{3}u_{3}$

Như vậy ta có thể quy thuật toán&nbsp;Nonlinear Regression&nbsp; về thuật toán Linear Regression bằng cách đặt ẩn phụ.

Phương pháp này còn có thể áp dụng trong trường hợp hàm phân bố không phải dạng đa thức. Chẳng hạn, nếu ta muốn tìm phương trình giả thuyết dạng

$\widehat{y} =&nbsp; w_{0} + w_{1}sin x_{1} + w_{2}cos x_{2} $

thì ta đặt&nbsp;$u_{1} = sin x_{1}, u_{2} = cos x_{2}$ sẽ đưa về việc tìm hàm tuyến tính với 2 biến mới&nbsp;$u_{1}, u_{2}$

$\widehat{y} =&nbsp; w_{0} + w_{1}u_{1} + w_{2}u_{2} $

<em><strong>Lưu ý:</strong>&nbsp;Thuật toán Linear Regression chỉ là trường hợp riêng của thuật toán Nonlinear Regression khi phương trình giả thuyết có dạng đa thức bậc 1. Trong Nonlinear Regression, thay vì chỉ sử dụng các biến có sẵn, ta đã tự tạo ra biến mới bằng cách đặt ẩn phụ. Số biến mới <strong>p</strong> không nhất thiết phải bằng số biến cũ <strong>n</strong>.</em>
<h4>
Độ chính xác của phương trình giả thuyết</h4>
Hàm mất mát của thuật toán Nonlinear Regression

$J(w) =&nbsp;\frac{1}{2m} \sum_{i=1}^{m} ( \widehat{y}^{(i)} - y^{(i)}) ^{2}$

$= \frac{1}{2m} \sum_{i=1}^{m} ( w_{0} + w_{1}u_{1}^{(i)} + ... +&nbsp;w_{p}u_{p}^{(i)} - y^{(i)}) ^{2}$

$= \frac{1}{2m} \sum_{i=1}^{m} ( u^{(i)T}w - y^{(i)}) ^{2}$

trong đó m là số input ban đầu được dùng để đào tạo thuật toán, w = $\begin{bmatrix}w_{0} \\\\ w_{1} \\\\ ... \\\\ w_{p} \end{bmatrix} $ là vector các hệ số của phương trình giả thuyết, $u^{(i)} = \begin{bmatrix}1 \\\\ u_{1}^{(i)} \\\\ ... \\\\ u_{p}^{(i)} \end{bmatrix}$ là vector các biến mới của input thứ i.

Đặt U = $\begin{bmatrix}1 &amp; u_{1}^{(1)} &amp; ... &amp; u_{p}^{(1)} \\\\ 1 &amp; u_{1}^{(2)} &amp; ... &amp; u_{p}^{(2)} \\\\... &amp; ... &amp; ... &amp; ... \\\\ 1 &amp; u_{1}^{(m)} &amp; ... &amp; u_{p}^{(m)}\end{bmatrix}$ là ma trận với mỗi hàng là một input (hàng i ứng với $x^{(i)T}$), đặt y = $\begin{bmatrix}y^{(1)} \\\\ y^{(2)} \\\\ ... \\\\ y^{(m)} \end{bmatrix}$ là vector các output thì hàm mất mát được viết lại thành

$J(w) = \frac{1}{2m}&nbsp;\parallel U^{T}w - y \parallel ^{2}$
<h4>
Nghiệm của thuật toán Nonlinear Regression</h4>
Việc tìm nghiệm của thuật toán Nonlinear Regression một biến là&nbsp;tìm ra tham số w =&nbsp;$\begin{bmatrix}w_{0} \\\\ w_{1} \\\\ ... \\\\ w_{p} \end{bmatrix} $ để hàm mất mát có giá trị nhỏ nhất.

Thực hiện việc khảo sát hàm mất mát đối với p + 1 biến $w_{0},&nbsp;w_{1}, ...,&nbsp;w_{p}$ ta được phương trình của vector w để hàm mất mát đạt giá trị nhỏ nhất như sau

$U^{T}Uw = U^{T}y$

Giống thuật toán Linear Regression, ta tìm được w bằng công thức

$w = (U^{T}U)^{+}U^{T}y$
<h3>
Chính quy hóa dữ liệu</h3>
<h4>
Underfitting và Overfitting</h4>

Khi chọn biến mới cho phương trình giả thuyết, có thể xảy ra 2 vấn đề ảnh hưởng tới độ chính xác kết quả bài toán.

Nếu số biến mới quá ít hoặc phương trình giả thuyết có dạng quá đơn giản thì phương trình giả thuyết tìm được sẽ không phản ánh đúng xu hướng phân bố của dữ liệu ban đầu. Kết quả sẽ sai lệch lớn không chỉ với input ban đầu mà cả kết quả dự đoán với các input mới. Ta gọi là hiện tượng <b>underfitting</b>.

Ngược lại, nếu có quá nhiều biến hoặc phương trình giả thuyết có dạng quá phức tạp thì phương trình giả thuyết tìm được sẽ sai lệch ít với input ban đầu nhưng lại sai lệch lớn với các input mới. Ta gọi hiện tượng này là <b>overfitting</b>.

Thuật toán sẽ cho kết quả tốt nếu ta chọn các biến mới và dạng phương trình giả thuyết phù hợp.

<div class="separator" style="clear: both; text-align: center;">
<a href="https://2.bp.blogspot.com/-PaBqD3GLSEI/XC3TQkN4V1I/AAAAAAAAELo/3vOdnWsKf1oSsm3CJ-CaDIZGUqI-bSLiQCLcBGAs/s1600/t0zit.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Underfitting và Overfitting" border="0" data-original-height="148" data-original-width="500" src="https://2.bp.blogspot.com/-PaBqD3GLSEI/XC3TQkN4V1I/AAAAAAAAELo/3vOdnWsKf1oSsm3CJ-CaDIZGUqI-bSLiQCLcBGAs/s1600/t0zit.png" title="Underfitting và Overfitting" /></a></div>

Để khắc phục hiện tượng Underfitting, ta cần chọn thêm các biến mới thích hợp.

Để khắc phục hiện tượng Overfitting, ta có thể loại bớt một số biến hoặc dùng kỹ thuật chính quy hóa dữ liệu.
<h4>
Chính quy hóa dữ liệu với Nonlinear Regression</h4>

Mục đích của việc chính quy hóa dữ liệu nhằm không phải loại bớt biến nhưng vẫn tránh được Overfitting bằng cách giữ cho các hệ số của phương trình giả thuyết không quá lớn, tránh việc quá phục thuộc vào một biến nào đó.

Ta làm việc này bằng cách sửa lại hàm mất mát như sau

$J(w) = \frac{1}{2m} [ \sum_{i=1}^{m} ( u^{(i)T}w - y^{(i)}) ^{2} + \lambda \sum_{j=1}^{p}w_{j}^{2} ]$

Giá trị&nbsp;λ &gt; 0 là <b>độ chính quy hóa</b>. Nếu&nbsp;λ càng lớn, hàm mất mát sẽ càng lớn khi trị tuyệt đối các hệ số lớn. Do đó, các hệ số sẽ được giữ ở một giá trị nhỏ, tránh sự quá phụ thuộc của phương trình giả thuyết vào một biến nào đó. Nhưng ta cũng không được chọn&nbsp;λ quá lớn vì khi đó sẽ lại xảy ra hiện tượng underfitting.

Khi áp dụng chính quy hóa, công thức nghiệm của thuật toán thay đổi một chút như ở dưới đây.

$w = (U^{T}U + \lambda L)^{+}U^{T}y$

với L = $\begin{bmatrix}0 &amp; 0 &amp; ... &amp; 0 \\\\ 0 &amp; 1 &amp; ... &amp; 0 \\\\ ... &amp; ... &amp; ... &amp; ... \\\\ 0 &amp; 0 &amp; ... &amp; 1 \end{bmatrix}$ là ma trận cấp (p+1) x (p+1). Khi λ &gt; 0 thì kỹ thuật chính quy hóa dữ liệu được áp dụng và $U^{T}U + \lambda L$ luôn khả nghịch.
<h3>
Lựa chọn biến và độ chính quy hóa</h3>

Việc lựa chọn biến phù hợp với bộ dữ liệu đào tạo đôi khi rất khó khăn. Nhất là trong trường hợp số biến nhiều, ta không thể dễ dàng biểu diễn trực quan các điểm dữ liệu.

Để lựa chọn phương án tối ưu, ta chia tập input ban đầu thành 3 tập: <b>tập đào tạo</b>, <b>tập kiểm định</b> và <b>tập thử</b>. Trước tiên, các phương án lựa chọn sẽ được thực hiện trên tập đào tạo để tính các phương trình giả thuyết. Phương trình giả thuyết với mất mát nhỏ nhất trên tập kiểm định sẽ được lựa chọn. Tập thử có vai trò dùng tính toán mất mát của phương án lựa chọn với dữ liệu mới.

Ví dụ, có 3 phương án lựa chọn và 100 dữ liệu ban đầu. Ta chia 60 dữ liệu vào tập đào tạo và dùng nó để tính toán phương trình giả thuyết đối với từng phương án. Sau đó giả sử phương trình giả thuyết thứ 2 có mất mát nhỏ nhất trên tập kiểm định gồm 20 dữ liệu thì ta sẽ lựa chọn phương án này. Tập thử gồm 20 dữ liệu còn lại được dùng để tính mất mát của phương án 2 với dữ liệu mới.

Viêc lựa chọn độ chính quy hóa cũng giống như trên. Ta thử nhiều độ chính quy hóa khác nhau để lựa chọn giá trị tốt nhất.
<h3>
Tóm tắt thuật toán Nonlinear Regression</h3>
<h4>
Yêu cầu</h4>
Cho trước m bộ dữ liệu để đào tạo thuật toán. Bộ dữ liệu thứ i chứa input $x^{(i)}$ và output $y^{(i)}$, trong đó input thứ i chứa n biến từ $x_{1}^{(i)}$ đến $x_{n}^{(i)}$. Nhiệm vụ của chúng ta là tìm ra mối liên hệ giữa input và output bằng một hàm phi tuyến tính để khi đưa vào một input mới, ta có thể dự đoán được output ứng với nó

$\widehat{y} = w_{0} + w_{1}f_{1}(x_{1}, ..., x_{n}) + ... + w_{p}f_{p}(x_{1}, ..., x_{n})$
<h4>
Thuật toán</h4>
<strong>Bước 0:</strong>&nbsp;Đặt $u_{1} = f_{1}(x_{1}, ..., x_{n}), ..., u_{p} = f_{p}(x_{1}, ..., x_{n})$ ta sẽ quy được về việc tìm hàm tuyến tính

$\widehat{y} = w_{0} + w_{1}u_{1} + ... + w_{p}u_{p}$

<strong>Bước 1:&nbsp;</strong>Thiết lập các ma trận và vector dưới đây

w = $\begin{bmatrix}w_{0} \\\\ w_{1} \\\\ ... \\\\ w_{p} \end{bmatrix} $

U = $\begin{bmatrix}1 &amp; u_{1}^{(1)} &amp; ... &amp; u_{p}^{(1)} \\\\ 1 &amp; u_{1}^{(2)} &amp; ... &amp; u_{p}^{(2)} \\\\... &amp; ... &amp; ... &amp; ... \\\\ 1 &amp; u_{1}^{(m)} &amp; ... &amp; u_{p}^{(m)}\end{bmatrix}$

y = $\begin{bmatrix}y^{(1)} \\\\ y^{(2)} \\\\ ... \\\\ y^{(m)} \end{bmatrix}$

<strong>Bước 2:</strong>&nbsp;Vector w được tính bằng công thức

$w = (U^{T}U + \lambda L)^{+}U^{T}y$

với L = $\begin{bmatrix}0 &amp; 0 &amp; ... &amp; 0 \\\\ 0 &amp; 1 &amp; ... &amp; 0 \\\\ ... &amp; ... &amp; ... &amp; ... \\\\ 0 &amp; 0 &amp; ... &amp; 1 \end{bmatrix}$ là ma trận cấp (p+1) x (p+1). Khi λ &gt; 0 thì kỹ thuật chính quy hóa dữ liệu được áp dụng và $U^{T}U + \lambda L$ luôn khả nghịch.
<h3>
Bạn đang nghĩ gì?</h3>
Bạn vừa được học thuật toán Nonlinear Regression - thuật toán loại Regression rất tổng quát để tìm phương trình giả thuyết biểu diễn sự phân bố các điểm dữ liệu cho trước mà trong nhiều trường hợp không thể áp dụng thuật toán Linear Regression.

Trong thuật toán Nonlinear Regression, chúng ta không chỉ sử dụng các biến có sẵn mà còn tự tạo ra biến mới bằng cách đặt ẩn phụ.