---
tag: learn
layout: post
title:  "Bài 19: Thuật Toán Collaborative Filtering"
description: "Bài này sẽ hướng dẫn bạn tìm hiểu thuật toán Collaborative Filtering - thuật toán được sử dụng trong các hệ thống gợi ý."
---

Bài này sẽ hướng dẫn bạn tìm hiểu thuật toán Collaborative Filtering - thuật toán được sử dụng trong các hệ thống gợi ý.

Đây là thuật toán có nhiều ứng dụng thực tiễn, đặc biệt là với thương mại điện tử.
<!--more-->
<h3>
Mở đầu</h3>
Một trong những ứng dụng quan trọng và phổ biến nhất của Machine Learning là để xây dựng các hệ thống gợi ý sản phẩm. Các hệ thống này giúp đưa ra những lựa chọn mà người dùng có thể quan tâm, giúp tăng trải nghiệm người dùng và lợi nhuận cho doanh nghiệp.

<div class="separator" style="clear: both; text-align: center;">
<a href="https://1.bp.blogspot.com/-5MQRwGmndRI/W0VdQWsRH0I/AAAAAAAAD0s/-AyBIUcueaIbrFSO0Rd89HU1yfEBwDomQCPcBGAYYCw/s1600/product-page-suggestions-09-amazon-mockup-3fd2ae3d9c43414610ef962b92802f3b.jpg" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Hệ thống gợi ý của Amazon" border="0" data-original-height="256" data-original-width="500" src="https://1.bp.blogspot.com/-5MQRwGmndRI/W0VdQWsRH0I/AAAAAAAAD0s/-AyBIUcueaIbrFSO0Rd89HU1yfEBwDomQCPcBGAYYCw/s1600/product-page-suggestions-09-amazon-mockup-3fd2ae3d9c43414610ef962b92802f3b.jpg" title="Hệ thống gợi ý của Amazon" /></a></div>

Xét một hệ thống bán hàng trực tuyến có $n_{u}$ người dùng và $n_{p}$ sản phẩm bày bán. Người dùng có thể đánh giá sản phẩm từ 1 tới 5 sao. $Y = \begin{bmatrix}2 &amp; 4 &amp; ... &amp; 5\\\\? &amp; ? &amp; ... &amp; ? \\\\ ... &amp; ... &amp; ... &amp; ... \\\\ 2 &amp; 5 &amp; ... &amp; 5 \end{bmatrix}$ là ma trận chứa dữ liệu đánh giá của người dùng. Ta cần xây dựng hệ thống gợi ý dựa vào các dữ liệu này.

<div class="separator" style="clear: both; text-align: center;">
<a href="https://4.bp.blogspot.com/-2xZeZYnvzXk/XDyahMiSVgI/AAAAAAAAETo/JRoNHTYE6m8KjN9kKNZLqxOFUk4f6SvQgCLcBGAs/s1600/Untitled.jpg" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Đánh giá người dùng về sản phẩm" border="0" data-original-height="174" data-original-width="500" src="https://4.bp.blogspot.com/-2xZeZYnvzXk/XDyahMiSVgI/AAAAAAAAETo/JRoNHTYE6m8KjN9kKNZLqxOFUk4f6SvQgCLcBGAs/s1600/Untitled.jpg" title="Đánh giá người dùng về sản phẩm" /></a></div>

Một cách thực hiện là sử dụng các thuật toán Regression mà ta đã học để dự đoán đánh giá của từng người dùng cho mỗi sản phẩm. Nếu hệ số phương trình giả thuyết của người dùng thứ i là $w^{(i)}$ và vector các thuộc tính của sản phẩm thứ j là $x^{(j)}$ thì đánh giá dự đoán của người dùng i với sản phẩm j là $Y_{ij} = x^{(j)T}w^{(i)}$. Ta sẽ đưa ra gợi ý theo thứ tự xếp hạng giảm dần.

Cách này có nhược điểm là chỉ có thể thực hiện với những người dùng đã đánh giá một số lượng sản phẩm đủ lớn, nó cũng đòi hỏi phải xác định được giá trị thuộc tính của các sản phẩm. Hơn nữa, nó không tận dụng được kết quả đánh giá của những người dùng khác để tăng độ chính xác của gợi ý.
<h3>
Thuật toán Collaborative Filtering</h3>
Trong thuật toán Collaborative Filtering, ta tìm cả giá trị thuộc tính các sản phẩm lẫn phương trình giả thuyết của mỗi người dùng dựa trên các đánh giá đã có.

Với mỗi bộ giá trị $w^{(1)}, w^{(2)}, ..., w^{(n_{u})}, x^{(1)}, x^{(2)}, ..., x^{(n_{p})}$ thì hàm mất mát của thuật toán được định nghĩa

$J = \frac{1}{2}\sum_{(i,j):r(i,j)=1}(x^{(j)T}w^{(i)} - Y_{ij})^{2} + \frac{\lambda}{2}\sum_{i=1}^{n_{u}}\sum_{k=1}^{n}w_{k}^{(i)2} + \frac{\lambda}{2}\sum_{j=1}^{n_{p}}\sum_{k=1}^{n}x_{k}^{(j)2}$

với r(i, j) bằng 1 khi người dùng i đã đánh giá sản phẩm j và bằng 0 trong trường hợp ngược lại.

Các đánh giá của người dùng và các thuộc tính của sản phẩm là nghiệm cực tiểu của hàm mất mát trên. Ta có thể sử dụng thuật toán Gradient Descent để giải quyết bài toán này.

Với W là ma trận mà hàng thứ i chứa $w^{(i)T}$, X là ma trận mà hàng thứ j chứa $x^{(j)T}$ thì ma trận các đánh giá dự đoán là $Y' = WX^{T}$.

Một ưu điểm của Collaborative Filtering là có thể tìm được giá trị các thuộc tính của từng sản phẩm. Mặc dù ý nghĩa của các thuộc tính này rất khó xác định, chúng có thể được sử dụng để gợi ý sản phẩm theo mức độ tương tự giữa chúng với sản phẩm đang xét. Độ tương tự giữa hai sản phẩm càng lớn khi độ dài hiệu vector của chúng càng nhỏ.
<h3>
Bình thường hóa dữ liệu</h3>
Đối với người dùng chưa đánh giá bất kỳ sản phẩm nào, để tối ưu hàm mất mát thì các hệ số phương trình giả thuyết của họ sẽ bằng 0, từ đó dẫn tới dự đoán đánh giá cho tất cả các sản phẩm bằng 0. Điều này rõ ràng không phù hợp và ta cần để đánh giá mặc định của người dùng bằng trung bình đánh giá của người khác thông qua việc bình thường hóa dữ liệu.

Gọi $\mu$ là vector chứa các phần tử là trung bình đánh giá từng sản phẩm của những người đã từng đánh giá sản phẩm tương ứng.

$\mu_{j} = \frac{\sum_{i:r(i,j)=1}Y_{ij}}{\sum_{i}r(i, j)}$

Tất cả các đánh giá trong ma trận Y sẽ giảm đi một lượng bằng trung bình đánh giá của sản phẩm tương ứng để đảm bảo trung bình mới về 0.

Sử dụng ma trận Y mới để tìm nghiệm hàm mất mát. Khi đó, đánh giá dự đoán của người dùng i với sản phẩm j sẽ là $x^{(j)T}w^{(i)} + \mu_{j}$.
<h3>
Tóm tắt thuật toán Collaborative Filtering</h3>
<h4>
Yêu cầu</h4>
Một hệ thống bán hàng trực tuyến có $n_{u}$ người dùng và $n_{p}$ sản phẩm bày bán. Y là ma trận chứa dữ liệu đánh giá của người dùng ở các hàng với sản phẩm ở các cột. Ta cần tìm ra n thuộc tính của mỗi sản phẩm và các hệ số phương trình giả thuyết dự đoán đánh giá của từng người dùng.
<h4>
Thuật toán</h4>
<b>Bước 0:</b>&nbsp;Bình thường hóa dữ liệu.

<strong>Bước 1: </strong>Chọn n, α và khởi tạo&nbsp;các giá trị&nbsp;&nbsp;$w^{(1)}, w^{(2)}, ..., w^{(n_{u})}, x^{(1)}, x^{(2)}, ..., x^{(n_{p})}$ ngẫu nhiên.

<strong>Bước 2:</strong>&nbsp;Liên tiếp lặp lại các phép biến đổi

<i>$w_{k}^{(i)} := w_{k}^{(i)}(1 - \alpha \lambda) - \alpha \sum_{j:r(i,j)=1}(x^{(j)T}w^{(i)} - Y_{ij})x_{k}^{(j)}$</i>

<i>$x_{k}^{(j)} := x_{k}^{(j)}(1 - \alpha \lambda) - \alpha \sum_{i:r(i,j)=1}(x^{(j)T}w^{(i)} - Y_{ij})w_{k}^{(i)}$</i>

<strong>Bước 3:</strong>&nbsp;Thuật toán dừng lại khi J thay đổi rất nhỏ hoặc trị tuyệt đối các đạo hàm riêng rất nhỏ. Nếu thuật toán không thể kết thúc thì chọn giá trị&nbsp;α nhỏ hơn rồi quay lại bước 2.
<h3>
Bạn đang nghĩ gì?</h3>
Bạn vừa được học thuật toán Collaborative Filtering - một thuật toán có nhiều ứng dụng thực tiễn.

Collaborative Filtering là một trong những thuật toán được quan tâm nhiều nhất do tầm quan trọng mà nó mang lại với hoạt động kinh doanh.

Bạn hãy thử trải nghiệm tính năng gợi ý sản phẩm của một website nào đó và đánh giá xem những gợi ý của chúng có phù hợp với bạn không, và có phù hợp với nội dung bài học không.