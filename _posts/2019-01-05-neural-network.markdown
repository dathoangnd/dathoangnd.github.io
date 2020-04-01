---
layout: post
title:  "Bài 13: Thuật Toán Neural Network"
description: "Bài này sẽ hướng dẫn bạn tìm hiểu thuật toán Neural Network - một thuật toán rất mạnh mẽ trong Machine Learning."
---

Trong bài này chúng ta sẽ tìm hiểu thuật toán Neural Network - một trong những thuật toán Machine Learning mạnh mẽ nhất.

Neural Network là nền tảng của&nbsp;<b><a href="https://en.wikipedia.org/wiki/Deep_learning" target="_blank">Deep Learning</a></b> - một lĩnh vực hẹp của Machine Learning.

Neural Network không mới. Nhưng sự phát triển của máy tính điện tử với tốc độ tính toán nhanh đã thúc đẩy ứng dụng Neural Network.
<!--more-->
<h3>
Mở đầu</h3>
Tôi đã từng học 4 năm tại trường Đại học y Hà Nội. Tôi nhận thấy một trong những chủ đề khó khăn nhất cho sinh viên là về thần kinh. Bộ não của con người là cỗ máy hoàn hảo nhất mà tự nhiên đã sinh ra và nó quá phức tạp để có thể hiểu hết.

<div class="separator" style="clear: both; text-align: center;">
<a href="https://2.bp.blogspot.com/-M_8YkH5NcR8/XDblPxWcuAI/AAAAAAAAEP0/u3URf2AkeSEUYN4jNqrcvMXJIFVZ5zuEACLcBGAs/s1600/2-whyareneuron.jpg" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Neuron" border="0" data-original-height="243" data-original-width="500" src="https://2.bp.blogspot.com/-M_8YkH5NcR8/XDblPxWcuAI/AAAAAAAAEP0/u3URf2AkeSEUYN4jNqrcvMXJIFVZ5zuEACLcBGAs/s1600/2-whyareneuron.jpg" title="Neuron" /></a></div>

Các tế bào thần kinh được gọi là <b><a href="https://en.wikipedia.org/wiki/Neuron" target="_blank">neuron</a></b> có chức năng dẫn truyền xung động thần kinh. Mỗi neuron nhận xung động thần kinh vào từ neuron đứng trước nó, truyền dọc theo <b>axon</b> và truyền ra neuron đứng sau nó thông qua <b>synapse</b>.

Xung động thần kinh truyền từ neuron này sang neuron khác trong mạng neuron tạo nên mọi chức năng thần kinh của não bộ.

Một ý tưởng hấp dẫn là nếu có thể mô phỏng cách bộ não học tập, chúng ta sẽ có một thuật toán Machine Learning vô cùng mạnh mẽ.
<h3>
Thuật toán Neural Network</h3>
<h4>
Mô hình toán học</h4>

Dưới đây là mô hình mạng neuron với 3&nbsp;<b>lớp</b> và 8&nbsp;<b>nút</b>

<div class="separator" style="clear: both; text-align: center;">
<a href="https://1.bp.blogspot.com/-DUEH03NMRAo/XDbyb9HdPJI/AAAAAAAAEQM/7ymwom31C0I_BLX2BDTAHxr4Xgia4vq6wCLcBGAs/s1600/1_-a-flCLHLCGM0-7TOcNJnQ.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Mạng neuron" border="0" data-original-height="351" data-original-width="500" src="https://1.bp.blogspot.com/-DUEH03NMRAo/XDbyb9HdPJI/AAAAAAAAEQM/7ymwom31C0I_BLX2BDTAHxr4Xgia4vq6wCLcBGAs/s1600/1_-a-flCLHLCGM0-7TOcNJnQ.png" title="Mạng neuron" /></a></div>

Lớp đầu tiên là lớp input nhận input của bài toán. Lớp giữa là lớp ẩn sẽ nhận giá trị trả về của lớp trước nó để tính toán các giá trị phức tạp hơn trước khi chuyển tới lớp kể tiếp. Lớp cuối cùng là lớp output.

Mỗi nút trừ các nút thuộc lớp input giống như một thuật toán Logistic Regression. Trong đó nó nhận vector input là các giá trị của các nút thuộc lớp trước và output của nó lại là một phần tử của vector input cho các nút thuộc lớp tiếp theo.

Ký hiệu $z^{(l)}$ là vector chứa các giá trị phương trình Decision Boundary của các nút lớp thứ l, $a^{(l)} = g(z^{(l)})$ là vector chứa các giá trị trả về của các nút tương ứng. Ký hiệu $W^{(l)}$ là ma trận mà mỗi hàng là vector hệ số phương trình Decision Boundary của một nút thuộc lớp l+1. Lưu ý các ma trận này có chỉ số hàng bắt đầu từ 1 và chỉ số cột bắt đầu từ 0.

Giá trị của các nút là

$a_{1}^{(2)} = g(W_{10}^{(1)}x_{0} + W_{11}^{(1)}x_{1} + W_{12}^{(1)}x_{2} + W_{13}^{(1)}x_{3})$

$a_{2}^{(2)} = g(W_{20}^{(1)}x_{0} + W_{21}^{(1)}x_{1} + W_{22}^{(1)}x_{2} + W_{23}^{(1)}x_{3})$

$a_{3}^{(2)} = g(W_{30}^{(1)}x_{0} + W_{31}^{(1)}x_{1} + W_{32}^{(1)}x_{2} + W_{33}^{(1)}x_{3})$

$a_{4}^{(2)} = g(W_{40}^{(1)}x_{0} + W_{41}^{(1)}x_{1} + W_{42}^{(1)}x_{2} + W_{43}^{(1)}x_{3})$

$\widehat{y} = a_{1}^{(3)} = g(W_{10}^{(2)}a_{0}^{(2)} + W_{11}^{(2)}a_{1}^{(2)} + W_{12}^{(2)}a_{2}^{(2)} + W_{13}^{(2)}a_{3}^{(2)} + W_{14}^{(2)}a_{4}^{(2)})$

Viết một cách ngắn gọn

$a^{(2)} = g(W^{(1)}a^{(1)}) = g(z^{(2)})$

$\widehat{y} =&nbsp;a^{(3)} = g(W^{(2)}a^{(2)}) = g(z^{(3)})$

Lưu ý là $a^{(l)}_{0} = 1$ với mọi lớp l.
<h4>
Độ chính xác của phương trình giả thuyết</h4>
Do lớp output có thể có nhiều hơn một nút nên hàm mất mát của thuật toán Neural Network rất phức tạp.

Ký hiệu L, K, $s_{l}$ lần lượt là số lớp, số nút của lớp output và số nút của lớp thứ l (khác lớp output) thì hàm mất mát có phương trình

$J(W) = -\frac{1}{m} \sum_{i=1}^{m}&nbsp;\sum_{k=1}^{K}&nbsp;[y_{k}^{(i)}ln(ŷ_{k}^{(i)}) + (1 - y_{k}^{(i)})ln(1 - ŷ_{k}^{(i)})] + \frac{\lambda}{2m}\sum_{l=1}^{L - 1}\sum_{q=1}^{s_{l}}\sum_{p=1}^{s_{l+1}} (W_{pq}^{(l)})^{2}$
<h4>
Nghiệm của thuật toán Neural Network</h4>
Để tìm điểm cực tiểu của hàm mất mát, ta có thể dùng Gradient Descent. Nhưng vấn đề là hàm mất mát quá phức tạp khiến việc tìm các đạo hàm riêng với từng $W^{(l)}_{pq}$ là rất khó khăn.

<a href="https://en.wikipedia.org/wiki/Backpropagation" target="_blank"><b>Thuật toán Backpropagation</b></a>&nbsp;giúp ta tìm được các đạo hàm riêng này.

Trong trường hợp m = 1 ta có đạo hàm riêng của J(W) với $z_{p}^{(L)}$ là

$\delta_{z_p^{(L)}} = ŷ_{p}^{(1)}&nbsp;- y_{p}^{(1)}$

Đạo hàm riêng của J(W) với $z^{(l)}_{p}$ với 1 &lt; l &lt; L được tính bằng công thức quy nạp

$\delta_{z_{p}^{(l)}} = a_{p}^{(l)}(1 - a_{p}^{(l)})\sum_{r=1}^{s_{l+1}} (W_{rp}^{(l)}\delta_{z_{r}^{(l+1)}})$

Đạo hàm riêng của J(W) với các hệ số $W^{(l)}_{pq}$ khi không áp dụng chính quy hóa là

$\Delta_{W_{pq}^{(l)}} = a_{q}^{(l)}\delta_{z_{p}^{(l+1)}}$

Tổng quát ta có đạo hàm riêng của J(W) với các hệ số&nbsp; $W_{pq}^{(l)}$&nbsp;là

$J_{W_{pq}^{(l)}}' = \begin{cases}\frac{1}{m}\sum_{i=1}^{m}\Delta_{W_{pq}^{(l)}}^{(i)} +&nbsp; \frac{\lambda}{m}W_{pq}^{(l)} &amp; khi\ q&nbsp;\neq 0\\\\\frac{1}{m}\sum_{i=1}^{m}\Delta_{W_{pq}^{(l)}}^{(i)} &amp; khi\ q = 0\end{cases}$

Một lưu ý là khi áp dụng Gradient Descent với Neural Network, ta không thể khởi tạo tất cả các giá trị $W^{(l)}_{pq}$ bằng 0 vì nếu làm vậy thì giá trị của các nút trong cùng một lớp khác lớp input sẽ giống nhau, dẫn đến thuật toán không thể kết thúc. Thay vào đó ta khởi tạo các giá trị ngẫu nhiên. Thông thường, các giá trị ngẫu nhiên này được khởi tạo trong một lân cận của 0.

Một lưu ý nữa khi tìm điểm tối ưu hàm mất mát của Neural Network là có thể gặp điểm tối ưu địa phương. Tuy nhiên, xác suất xảy ra là vô cùng nhỏ, nhất là khi số biến của input lớn.
<h3>
Xây dựng mô hình mạng neuron</h3>
Số nút ở lớp input là số phần tử thuộc một vector input không tính phần tử 1.

Thông thường ta sẽ chỉ dùng 1 lớp ẩn cho mạng neuron. Càng nhiều lớp ẩn sẽ càng có khả năng giải quyết các bài toán phức tạp với độ chính xác cao hơn nhưng thời gian thực hiện sẽ lâu hơn. Nếu có nhiều lớp ẩn thì số nút trong các lớp đó thường được chọn bằng nhau.

Trong các bài toán phân loại 2 lớp thì ta chỉ cần 1 nút ở lớp output là đủ giống như Logistic Regression. Với các bài toán phân loại k lớp thì ta cần k nút ở lớp output. Khi đó ta cần biến đổi output của dữ liệu đào tạo dưới dạng vector. Ví dụ với k = 3 thì output sẽ nhận một trong ba giá trị $\begin{bmatrix}1 \\\\ 0 \\\\ 0 \end{bmatrix}, \begin{bmatrix}0 \\\\ 1 \\\\ 0 \end{bmatrix}, \begin{bmatrix}0 \\\\ 0 \\\\ 1 \end{bmatrix}$. Đối với input mới giả sử kết quả phương trình giả thuyết trả về là $\begin{bmatrix}0.2 \\\\ 0.9 \\\\ 0.1 \end{bmatrix}$ ta sẽ dự đoán nó thuộc lớp phân loại thứ 2 do thành phần thứ 2 của vector output có giá trị lớn nhất.
<h3>
So sánh các thuật toán phân loại</h3>
Ta đã được tìm hiểu 3 thuật toán phân loại Logistic Regression, Support Vector Machine và Neural Network. Chúng đều là những thuật toán phổ biến và có những ưu nhược điểm riêng.

Các bài toán mà số lượng dữ liệu và số lượng biến không lớn, Logistic Regression và Support Vector Machine không sử dụng kernel là hai thuật toán phù hợp bởi sự đơn giản và nhanh chóng. Hai thuật toán này có hiệu quả tương đương nhau.

Các bài toán có số lượng dữ liệu nhiều nhưng số biến không lớn phù hợp với Support Vector Machine có sử dụng Kernel.

Các bài toán có số lượng dữ liệu nhiều và số biến lớn phù hợp với Neural Network.

Việc chọn thuật toán nào tùy thuộc vào trường hợp cụ thể mà có thể khác gợi ý trên. Nhìn chung cách tự chọn biến mới trong các bài toán có Decision Boundary phức tạp rất khó thực hiện nên thường không được áp dụng.
<h3>
Tóm tắt thuật toán Neural Network</h3>
<h4>
Yêu cầu</h4>
Cho trước m bộ dữ liệu để đào tạo thuật toán. Bộ dữ liệu thứ i chứa vector input $x^{(i)}$ và vector output $y^{(i)}$. Nhiệm vụ của ta là tìm ra các hệ số $W^{(l)}_{pq}$ của mô hình Neural Network đã chọn trước.
<h4>
</h4>
<h4>
Thuật toán</h4>
<strong>Bước 1:</strong>&nbsp;Chọn các giá trị $W^{(l)}_{pq}$ ngẫu nhiên và một giá trị learning rate&nbsp;α.

<strong>Bước 2:</strong>&nbsp;Liên tiếp lặp lại các phép biến đổi

$W_{pq}^{(l)}&nbsp;:= W_{pq}^{(l)} - \alpha J_{W_{pq}^{(l)}}'(W)$

với các đạo hàm riêng $J_{W_{pq}^{(l)}}'(W)$ được tính bằng thuật toán&nbsp;Backpropagation.

<strong>Bước 3:</strong>&nbsp;Thuật toán dừng lại khi J(W) thay đổi rất nhỏ hoặc trị tuyệt đối các đạo hàm riêng rất nhỏ. Nếu thuật toán không thể kết thúc thì chọn giá trị&nbsp;α nhỏ hơn rồi quay lại bước 2.
<h3>
Bạn đang nghĩ gì?</h3>
Bạn vừa được học thuật toán Neural Network - một trong những thuật toán Machine Learning mạnh nhất mà ta có.

Neural Network cũng là thuật toán phức tạp nhất mà ta đã tìm hiểu tính đến thời điểm này.

Bạn hãy thử tự mình giải thích các công thức của thuật toán Backpropagation để tính các đạo hàm riêng của hàm mất mát.