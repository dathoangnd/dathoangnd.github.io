---
tag: learn
layout: post
title:  "Bài 11: Thuật Toán Support Vector Machine"
description: "Bài này sẽ hướng dẫn bạn tìm hiểu thuật toán Support Vector Machine - một thuật toán phân loại mạnh mẽ được sử dụng rất phổ biến."
---

Thuật toán Support Vector Machine có nhiều điểm tương tự như Logistic Regression nhưng tính toán đơn giản và có nhiều cách tối ưu giúp nó thực hiện nhanh chóng hơn.

Khi sử dụng khái niệm&nbsp;<b><a href="https://en.wikipedia.org/wiki/Kernel_method" target="_blank">kernel</a></b>, Support Vector Machine trở nên rất mạnh mẽ để giải quyết các bài toán phân loại có Decision Boundary phức tạp.

Với những ưu điểm của mình, nó là một trong những thuật toán Machine Learning phổ biến nhất hiện nay.
<!--more-->
<h3>
Nhắc lại thuật toán Logistic Regression</h3>
Xét đồ thị phân bố dữ liệu dưới đây

<div class="separator" style="clear: both; text-align: center;">
<a href="https://1.bp.blogspot.com/-xiWpyDZc_Mg/XC4jII4YwEI/AAAAAAAAEME/4k59MLL1NacsYIC5nQmgpmD3eXqisgGJQCLcBGAs/s1600/LogisticRegressionWindowLogisticFitChart6.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Thuật toán Logistic Regression" border="0" data-original-height="305" data-original-width="500" src="https://1.bp.blogspot.com/-xiWpyDZc_Mg/XC4jII4YwEI/AAAAAAAAEME/4k59MLL1NacsYIC5nQmgpmD3eXqisgGJQCLcBGAs/s1600/LogisticRegressionWindowLogisticFitChart6.png" title="Thuật toán Logistic Regression" /></a></div>

Thuật toán Logistic Regression giúp ta tìm ra phương trình đường Decision Boundary $x^{T}w = 0$ phân chia các điểm dữ liệu có output 0 và các điểm dữ liệu có output 1 với w =&nbsp;$\begin{bmatrix}w_{0} \\\\ w_{1} \\\\ ... \\\\ w_{n} \end{bmatrix} $ và x =&nbsp;$\begin{bmatrix}1 \\\\ x_{1} \\\\ ... \\\\ x_{n} \end{bmatrix}$.

Phương trình giả thuyết chính là khả năng một input có output tương ứng là 1

$\widehat{y} = \frac{1}{1 + e^{-x^{T}w}}$

Hàm mất mát sử dụng hàm Sigmoid

$J(w) = -\frac{1}{m} \sum_{i=1}^{m} [y^{(i)}ln (\widehat{y}^{(i)}) + (1 - y^{(i)})ln (1 - \widehat{y}^{(i)})] + \frac{\lambda}{2m}\sum_{j=1}^{n} w^{2}_{j}$

Ở đây $-ln (\widehat{y}^{(i)})$ là phần mất mát mỗi input đóng góp khi output thực tế là 1 và $-ln (1 - \widehat{y}^{(i)})$ là phần mất mát mỗi input đóng góp khi output thực tế là 0.
<h3>
Thuật toán Support Vector Machine</h3>
<h4>
Mô hình toán học</h4>
Support Vector Machine không đưa ra khả năng output bằng 1 như Logistic Regression, thay vào nó nó chỉ đơn thuần dự đoán output bằng 0 hay bằng 1.

$\widehat{y} =&nbsp;\begin{cases}1 &amp; khi\ x^{T}w \geq 0\\\\0 &amp; khi\ x^{T}w &lt; 0\end{cases}$
<h4>
Độ chính xác của phương trình giả thuyết</h4>
Trong Support Vector Machine, phần mất mát mỗi input đóng góp có dạng <a href="https://en.wikipedia.org/wiki/Hinge_loss" target="_blank">hàm hinge loss</a>

$cost(x) =&nbsp; &nbsp;\begin{cases}max(0, k(1 - x^{T}w)) &amp; khi\ y = 1\\\\max(0, k(1 + x^{T}w)) &amp; khi\ y = 0\end{cases}$

với k là số dương bất kỳ.

Khi y = 1, cost(x) = 0 nếu $&nbsp;x^{T}w \geq 1$ và cost(x) tăng dần nếu $&nbsp;x^{T}w &lt; 1$ và tiến tới âm vô cực.

<div class="separator" style="clear: both; text-align: center;">
<a href="https://2.bp.blogspot.com/-wY7L6TaWzYE/XDLWldGh9_I/AAAAAAAAEOQ/lUFw_2gdX9wMx3owPeOv94PFQkaP0Om8wCEwYBhgL/s1600/Plot-of-hinge-loss-function.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Hàm hinge loss" border="0" data-original-height="286" data-original-width="500" src="https://2.bp.blogspot.com/-wY7L6TaWzYE/XDLWldGh9_I/AAAAAAAAEOQ/lUFw_2gdX9wMx3owPeOv94PFQkaP0Om8wCEwYBhgL/s1600/Plot-of-hinge-loss-function.png" title="Hàm hinge loss" /></a></div>

Khi y = 0, cost(x) = 0 nếu $&nbsp;x^{T}w \leq -1$ và cost(x) tăng dần nếu $&nbsp;x^{T}w &gt; -1$ và tiến tới dương vô cực.

<div class="separator" style="clear: both; text-align: center;">
<a href="https://4.bp.blogspot.com/-eMB3BMwZ2sA/XDLXYaG8MdI/AAAAAAAAEOg/grwQFNeU5BcgmDYa4SsivIL03068f0BHwCLcBGAs/s1600/Plot-of-hinge-loss-function.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Hàm hinge loss" border="0" data-original-height="286" data-original-width="500" src="https://4.bp.blogspot.com/-eMB3BMwZ2sA/XDLXYaG8MdI/AAAAAAAAEOg/grwQFNeU5BcgmDYa4SsivIL03068f0BHwCLcBGAs/s1600/Plot-of-hinge-loss-function.png" title="Hàm hinge loss" /></a></div>

Hàm mất mát của Support Vector Machine

$J(w) = C \sum_{i=1}^{m} [y^{(i)}max(0, k(1 - x^{(i)T}w)) + (1 - y^{(i)})max(0, k(1 + x^{(i)T}w))] + \frac{1}{2}\sum_{j=1}^{n} w^{2}_{j}$

Ở đây hằng số C đóng vai trò như $\frac{1}{\lambda}$ là độ chính quy hóa của hàm mất mát giúp kiểm soát sai lầm của phương trình giả thuyết. Khi xảy ra underfitting, ta cần tăng C. Khi xảy ra overfitting, ta cần giảm C.
<h4>
Nghiệm của thuật toán Support Vector Machine</h4>
Ta có thể tìm điểm cực tiểu của hàm mất mát bằng thuật toán Gradient Descent với các biến đổi

$w_{0} := w_{0} - \alpha C \sum_{i=1}^{m} [y^{(i)}(x^{(i)T}w \geq 1\ ?\ 0:-k) + (1 - y^{(i)})(x^{(i)T}w \geq -1\ ?\ k:0)]$

$w_{1} := w_{1}(1 - \alpha) - \alpha C \sum_{i=1}^{m} [y^{(i)}(x^{(i)T}w \geq 1\ ?\ 0:-kx_{1}^{(i)}) + (1 - y^{(i)})(x^{(i)T}w \geq -1\ ?\ kx^{(i)}_{1}:0)]$

...

$w_{n} := w_{n}(1 - \alpha) - \alpha C \sum_{i=1}^{m} [y^{(i)}(x^{(i)T}w \geq 1\ ?\ 0:-kx_{n}^{(i)}) + (1 - y^{(i)})(x^{(i)T}w \geq -1\ ?\ kx^{(i)}_{n}:0)]$

Một đặc điểm của Support Vector Machine là nó luôn cố gắng tìm nghiệm sao cho Dicision Boundary cách xa các điểm dữ liệu nhất cho thể. Trong hình dưới đây, thuật toán có xu hướng chọn phương án A thay vì phương án B vì nó cách xa các điểm dữ liệu hơn. Điều này có thể dẫn tới overfitting và ta có thể làm giảm xu hướng này bằng cách giảm C.

<div class="separator" style="clear: both; text-align: center;">
<a href="https://4.bp.blogspot.com/-_gWGLyBa-iM/XDMMPznVhII/AAAAAAAAEOs/zl_huitdh08Mnlaxh1s9FfF7fpD7QzSGwCLcBGAs/s1600/aHR0cDovL2ltZzEuaW1ndG4uYmRpbWcuY29tL2l0L3U9MTAxNjk1MjQ3LDM4MzE2ODA2NTQmZm09MTEmZ3A9MC5qcGc%253D.jpg" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Thuật toán Support Vector Machine" border="0" data-original-height="357" data-original-width="500" src="https://4.bp.blogspot.com/-_gWGLyBa-iM/XDMMPznVhII/AAAAAAAAEOs/zl_huitdh08Mnlaxh1s9FfF7fpD7QzSGwCLcBGAs/s1600/aHR0cDovL2ltZzEuaW1ndG4uYmRpbWcuY29tL2l0L3U9MTAxNjk1MjQ3LDM4MzE2ODA2NTQmZm09MTEmZ3A9MC5qcGc%253D.jpg" title="Thuật toán Support Vector Machine" /></a></div>


Việc tìm nghiệm của thuật toán Support Vector Machine tương đối phức tạp nếu cài đặt thủ công. Có rất nhiều thư viện đã được cài đặt sẵn Support Vector Machine và ta nên dùng chúng vì chẳng những giúp tiết kiệm thời gian mà các thư viện đó còn được áp dụng nhiều kỹ thuật tối ưu hóa để thuật toán chạy nhanh hơn.</div>
<h3>
Sử dụng Kernel với Support Vector Machine</h3>
Lý do giúp Support Vector Machine trở nên mạnh mẽ khi so sánh với Logistic Regression là bởi nó hoạt động rất tốt khi áp dụng Kernel để giải quyết các bài toán có dữ liệu phân bố phức tạp. Mặc dù Kernel cũng có thể sử dụng với Logistic Regression nhưng Support Vector Machine có nhiều phương pháp tối ưu cho Kernel hơn nên người ta thường chỉ sử dụng Kernel với Support Vector Machine.

Khi các điểm dữ liệu phân bố phức tạp, để tìm Decision Boundary phù hợp ta phải thêm các biến mới. Đây là việc ta đã làm trong các bài trước. Tuy nhiên, nhược điểm của cách này là khó chọn ra bộ các biến phù hợp và tốn nhiều công sức để thử nhiều phương án khác nhau.

Kernel thực chất là một hàm tính toán các biến mới của input. Có nhiều loại Kernel khác nhau. Trong đó phổ biến nhất là <b>Gaussian Kernel</b>.

Gaussian Kernel tìm độ giống nhau giữa điểm dữ liệu x và <b>điểm mốc</b> l như sau

$similarity(x, l) = e^{-\frac{\lVert x - l \lVert^{2}}{2\sigma^{2}}}$

Một cách đơn giản, khi x và l tiến lại gần nhau, f tiến tới 1, khi x và l tiến ra xa nhau, f tiến về 0.

Với bộ dữ liệu đào tạo có m phần tử, ta chọn m điểm mốc tại chính vị trí các phần tử đó. Với dữ liệu đào tạo thứ i ta tìm được input mới ứng với nó là $x^{(i)} = \begin{bmatrix}similarity(x^{(i)}, l^{(1)}) \\\\ similarity(x^{(i)}, l^{(2)})&nbsp;\\\\ ... \\\\ similarity(x^{(i)}, l^{(m)}) \end{bmatrix}$. Áp dụng thuật toán Support Vector Machine với bộ dữ liệu mới này, ta có thể tìm được phương trình đường Decision Boundary cho bài toán ban đầu.

Tham số $\sigma^{2}$ ảnh hưởng đến kết quả thuật toán. Nếu $\sigma^{2}$ nhỏ, f giảm nhanh khi điểm dữ liệu ra xa điểm mốc. Nếu $\sigma^{2}$ lớn, f giảm chậm khi điểm dữ liệu ra xa điểm mốc. Khi xảy ra underfitting, cần giảm giá trị $\sigma^{2}$. Khi xảy ra overfitting, cần tăng giá trị $\sigma^{2}$.

Một lưu ý là cần thiết phải bình thường hóa dữ liệu nếu các biến có phổ giá trị chênh lệch nhau nhiều trước khi áp dụng Gaussian Kernel.
<h3>
Tóm tắt thuật toán Support Vector Machine</h3>
<h4>
Yêu cầu</h4>
Cho trước m bộ dữ liệu để đào tạo thuật toán. Bộ dữ liệu thứ i chứa input $x^{(i)}$ và output $y^{(i)}$ thuộc một trong hai giá trị 0 và 1. Nhiệm vụ của ta là tìm ra vector hệ số w =&nbsp;$\begin{bmatrix}w_{0} \\\\ w_{1} \\\\ ... \\\\ w_{n} \end{bmatrix} $ của Decision Boundary.
<h4>
</h4>
<h4>
Thuật toán</h4>
<b>Bước 0:</b> Bình thường hóa dữ liệu và áp dụng kernel nếu cần thiết.

<strong>Bước 1:</strong>&nbsp;Chọn một điểm bất kỳ&nbsp;$(w_{0}, w_{1}, ..., w_{n})$ và các tham số α, C, k.

<strong>Bước 2:</strong>&nbsp;Liên tiếp lặp lại các phép biến đổi

$w_{0} := w_{0} - \alpha C \sum_{i=1}^{m} [y^{(i)}(x^{(i)T}w \geq 1\ ?\ 0:-k) + (1 - y^{(i)})(x^{(i)T}w \geq -1\ ?\ k:0)]$

$w_{1} := w_{1}(1 - \alpha) - \alpha C \sum_{i=1}^{m} [y^{(i)}(x^{(i)T}w \geq 1\ ?\ 0:-kx_{1}^{(i)}) + (1 - y^{(i)})(x^{(i)T}w \geq -1\ ?\ kx_{1}^{(i)}:0)]$

...

$w_{n} := w_{n}(1 - \alpha) - \alpha C \sum_{i=1}^{m} [y^{(i)}(x^{(i)T}w \geq 1\ ?\ 0:-kx_{n}^{(i)}) + (1 - y^{(i)})(x^{(i)T}w \geq -1\ ?\ kx_{n}^{(i)}:0)]$

<strong>Bước 3:</strong>&nbsp;Thuật toán dừng lại khi J(w) thay đổi rất nhỏ hoặc trị tuyệt đối các đạo hàm riêng rất nhỏ. Nếu thuật toán không thể kết thúc thì chọn giá trị&nbsp;α nhỏ hơn rồi quay lại bước 2.
<h3>
Bạn đang nghĩ gì?</h3>
Bạn vừa được học thuật toán Support Vector Machine - một thuật toán Classification rất mạnh mẽ và phổ biến.

Mặc dù tính toán đơn giản nhưng cách cài đặt thuật toán lại tương đối phức tạp. Ta nên sử dụng các thư viện để tiết kiệm công sức cũng như để có hiệu suất tính toán tốt nhất.

Kernel là một cách chọn biến mới hoạt động tốt với Support Vector Machine giúp giải quyết những bài toán rất phức tạp.

Theo bạn, khi nào nên sử dụng Logistic Regression và khi nào nên sử dụng Support Vector Machine?