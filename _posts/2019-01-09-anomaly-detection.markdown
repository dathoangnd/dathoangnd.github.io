---
tag: learn
layout: post
title:  "Bài 17: Thuật Toán Anomaly Detection"
description: "Bài này sẽ hướng dẫn bạn tìm hiểu thuật toán Anomaly Detection để phát hiện các điểm dữ liệu bất thường."
---

Bài này sẽ hướng dẫn bạn tìm hiểu thuật toán Anomaly Detection để xác định một điểm dữ liệu có bình thường hay không dựa trên phân bố dữ liệu đã có.

Anomaly Detection được sử dụng để phát hiện các gian lận hoặc hành động bất thường của người dùng.
<!--more-->
<h3>
Đặt vấn đề</h3>
Xét bộ dữ liệu gồm m phần tử $x^{(1)}, x^{(2)}, ..., x^{(m)}$.

Cho dữ liệu mới $x_{test}$, ta muốn biết liệu dữ liệu này có bình thường hay không.

<div class="separator" style="clear: both; text-align: center;">
<a href="https://2.bp.blogspot.com/-70z4c1LqUgA/XDvzC8-vVVI/AAAAAAAAESs/W3A-K_V4Q8YOjQp3QQ5wqpmW16udx7a1gCLcBGAs/s1600/corrcoefs_1%2B%25281%2529.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Phân bố bất thường" border="0" data-original-height="312" data-original-width="500" src="https://2.bp.blogspot.com/-70z4c1LqUgA/XDvzC8-vVVI/AAAAAAAAESs/W3A-K_V4Q8YOjQp3QQ5wqpmW16udx7a1gCLcBGAs/s1600/corrcoefs_1%2B%25281%2529.png" title="Phân bố bất thường" /></a></div>

Ta cần tìm ra hàm p(x) đặc trưng cho độ bình thường của dữ liệu. Tập hợp các điểm có $p(x) \geq \epsilon\ (\epsilon &gt; 0)$ hợp thành một vùng có mật độ tập trung dữ liệu cao và ta coi dữ liệu mới là bình thường khi nó nằm trong vùng này, bất thường khi nó nằm ngoài vùng này.
<h3>
Thuật toán Anomaly Detection</h3>
Thuật toán Anomaly Detection sử dụng <a href="https://en.wikipedia.org/wiki/Normal_distribution" target="_blank"><b>phân phối chuẩn</b></a> để tính xác suất để một điểm dữ liệu có giá trị nào đó.
<h4>
Phân phối chuẩn</h4>
Nếu biến $x \in R$ có dạng phân phối chuẩn thì <b><a href="https://en.wikipedia.org/wiki/Probability_distribution" target="_blank">hàm phân bố</a></b> của nó là

$p(x) = \frac{1}{\sqrt{2\pi}\sigma}e^{-\frac{(x - \mu)^{2}}{2\sigma^{2}}}$

với $\mu$ và $\sigma$ lần lượt là <a href="https://en.wikipedia.org/wiki/Expected_value" target="_blank"><b>kỳ vọng</b></a> và <a href="https://en.wikipedia.org/wiki/Variance" target="_blank"><b>phương sai</b></a> của x.

Đồ thị hàm phân bố của x có dạng chuông với xác suất cao nhất khi $x = \mu$ và giảm dần khi x tiến ra xa $\mu$.

<div class="separator" style="clear: both; text-align: center;">
</div>
<div class="separator" style="clear: both; text-align: center;">
<a href="https://4.bp.blogspot.com/-atdu3T6ifm4/XDv534AlDtI/AAAAAAAAES4/GGwxQlcBgY8PD7JMa-fGxqg_RQaYy0oWQCLcBGAs/s1600/1_IdGgdrY_n_9_YfkaCh-dag.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Phân phối chuẩn" border="0" data-original-height="263" data-original-width="500" src="https://4.bp.blogspot.com/-atdu3T6ifm4/XDv534AlDtI/AAAAAAAAES4/GGwxQlcBgY8PD7JMa-fGxqg_RQaYy0oWQCLcBGAs/s1600/1_IdGgdrY_n_9_YfkaCh-dag.png" title="Phân phối chuẩn" /></a></div>
<div class="separator" style="clear: both; text-align: center;">

</div>
Phân phối chuẩn là dạng phân phối quan trọng và phổ biến trong nhiều dữ liệu thống kê thực tế.
<h4>
Mô hình toán học</h4>
Tập dữ liệu ban đầu gồm các phần tử trong không gian $R^{n}$, tức mỗi phần tử là một vector n chiều.

Biểu diễn riêng rẽ phân bố của từng biến để xem chúng có hình chuông đặc trưng của phân phối chuẩn không. Giả dụ $x_{j}$ không có dạng phân phối chuẩn ta sẽ thay $x_{j}$ bằng $u_{j}$ thông qua một phép biến đổi nào đó để đảm bảo nó có dạng phân phối chuẩn như

$u_{j} = log(x_{j})$

$u_{j} = \sqrt{x_{j}}$

$u_{j} = x_{j}^{2}$

Ta có thể tính được kỳ vọng và phương sai của từng biến

$\mu_{j} = \frac{1}{m}\sum_{i=1}^{m}x^{(i)}_{j}$

$\sigma_{j}^{2} = \frac{1}{m}\sum_{i=1}^{m}(x_{j}^{(i)} - \mu_{j})^{2}$

Hàm phân bố tương ứng là

$p(x_{j}) = \frac{1}{\sqrt{2\pi}\sigma_{j}}e^{-\frac{(x_{j} - \mu_{j})^{2}}{2\sigma_{j}^{2}}}$

Lúc này, nếu các biến không phụ thuộc vào nhau ta có thể tính được hàm phân bố của x

$p(x) = \prod_{j=1}^{n}p(x_{j})$

Trong trường hợp không thể đảm bảo các biến không phụ thuộc nhau, ta có thể tìm p(x) bằng cách áp dụng phân phối chuẩn nhiều biến.

Kỳ vọng của x được tính bằng công thức

$\mu = \frac{1}{m}\sum_{i=1}^{m}x^{(i)}$

Ma trận hiệp phương sai $\Sigma$ kích cỡ n x n có các giá trị trên đường chéo chính là phương sai các biến, mỗi giá trị khác là hiệp phương sai của một cặp biến $\Sigma_{ij} = E[(x_{i} - \mu_{i})(x_{j} - \mu_{j})]$ được tính bằng công thức

$\Sigma = E[(x - \mu)(x - \mu)^{T}]$

Khi đó hàm phân bố của nó là
$p(x) = \frac{1}{(2\pi)^{\frac{n}{2}}\sqrt{|\Sigma|}}e^{-\frac{(x - \mu)^{T}\Sigma^{-1}(x - \mu)}{2}}$

Cuối cùng ta so sánh p(x) với $\epsilon$ để đưa ra kết luận.
<h3>
Tóm tắt thuật toán Anomaly Detection</h3>
<h4>
Yêu cầu</h4>
Có m điểm dữ liệu $x^{(1)}, x^{(2)}, ..., x^{(m)}$ và một dữ liệu mới $x_{test}$. Hãy xác định xem liệu $x_{test}$ có bình thường hay không.
<h4>
Thuật toán</h4>
<b>Bước 0:</b>&nbsp;Đảm bảo các biến có phân phối chuẩn.

<b>Bước 1:</b> Chọn một giá trị $\epsilon$.

<strong>Bước 2:</strong>&nbsp;Tìm hàm phân bố p(x).

<strong>Bước 3:</strong>&nbsp;Nếu $p(x_{test}) &lt; \epsilon$ ta kết luận $x_{test}$ bất thường, ngược lại ta kết luận $x_{test}$ bình thường.
<h3>
Bạn đang nghĩ gì?</h3>
Bạn vừa được học thuật toán Anomaly Detection - thuật toán để phát hiện bất thường của dữ liệu.

Theo bạn, khi nào nên dùng hàm phân bố bằng tích các hàm phân bố của từng biến thay vì dùng phân phối chuẩn nhiều biến? Khi đó, nếu có hai biến phụ thuộc nhau thì giải pháp khắc phục là gì?