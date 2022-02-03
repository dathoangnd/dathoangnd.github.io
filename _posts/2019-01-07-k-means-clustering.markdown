---
tag: learn
layout: post
title:  "Bài 15: Thuật Toán K-Means Clustering"
description: "Bài này sẽ hướng dẫn bạn tìm hiểu thuật toán K-Means Clustering - một thuật toán phân cụm phổ biến trong Machine Learning."
---

Bài này sẽ hướng dẫn bạn tìm hiểu thuật toán thuộc nhóm Unsupervised Learning đầu tiên, đó là K-Means Clustering.

K-Means Clustering là thuật toán Machine Learning phổ biến để phân cụm dữ liệu.
<!--more-->
<h3>
Mở đầu</h3>
Nhắc lại khái niệm về Unsupervised Learning đã nói đến trong <a href="https://www.dathoangblog.com/2018/07/machine-learning-la-gi.html">bài mở đầu</a>. Trong thuật toán Unsupervised Learning, chúng ta cũng được cung cấp các bộ input nhưng không có output. Thuật toán Unsupervised Learning không hề biết dữ liệu nó còn trả về sẽ như thế nào bởi nó không được cung cấp các ví dụ như ở Supervised Learning. Bằng cách nào đó Unsupervised Learning cần tự tìm ra cấu trúc dữ liệu để thực hiện nhiệm vụ nào đó.

Thuật toán Clustering là một loại của nhóm thuật toán Unsupervised Learning. Trong đó các dữ liệu ban đầu được phân thành <b>cụm</b> dựa trên vị trí tương đối của chúng so với nhau. Trong hình dưới đây, một cách định tính ta có thể thấy các dữ liệu có thể phân thành 3 cụm.

<div class="separator" style="clear: both; text-align: center;">
<a href="https://4.bp.blogspot.com/-OYd6b2lFdl4/XDqhwlIZ2AI/AAAAAAAAEQ8/v8LsgZwDwy8TxiyqUmZYIGrmdfXQAB5DwCLcBGAs/s1600/main.jpg" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Clustering" border="0" data-original-height="374" data-original-width="500" src="https://4.bp.blogspot.com/-OYd6b2lFdl4/XDqhwlIZ2AI/AAAAAAAAEQ8/v8LsgZwDwy8TxiyqUmZYIGrmdfXQAB5DwCLcBGAs/s1600/main.jpg" title="Clustering" /></a></div>
<div class="separator" style="clear: both; text-align: center;">

</div>
K-Means Clustering là thuật toán thường được sử dụng để giải quyết các bài toán phân cụm như vậy.
<h3>
Thuật toán K-Means Clustering</h3>
<h4>
Mô hình toán học</h4>
Ta gọi điểm tại vị trí trung bình của tất cả các điểm dữ liệu trong một cụm là <b>trung tâm cụm</b>. Như vậy, nếu có K cụm thì sẽ có K trung tâm cụm và mỗi trung tâm cụm sẽ nằm gần các điểm dữ liệu trong cụm tương ứng hơn các trung tâm cụm khác.

Trong hình dưới đây, K = 3 và ta có 3 trung tâm cụm là các điểm màu vàng.

<div class="separator" style="clear: both; text-align: center;">
<a href="https://3.bp.blogspot.com/-NMrDyo4_ySg/XDqlicW58WI/AAAAAAAAERI/bWXciHyrL_UzlGV2JSkB3D3iCKTtKnyYACLcBGAs/s1600/main.jpg" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Trung tâm cụm" border="0" data-original-height="374" data-original-width="500" src="https://3.bp.blogspot.com/-NMrDyo4_ySg/XDqlicW58WI/AAAAAAAAERI/bWXciHyrL_UzlGV2JSkB3D3iCKTtKnyYACLcBGAs/s1600/main.jpg" title="Trung tâm cụm" /></a></div>

Để phân cụm dữ liệu bằng K-Means Clustering, trước hết ta chọn K là số cụm để phân chia và chọn ngẫu nhiên K trong số m dữ liệu ban đầu làm trung tâm cụm<b> </b>$\mu_{1}, \mu_{2}, ..., \mu_{K}$.&nbsp;

Sau đó, với điểm dữ liệu $x^{(i)}$ ta sẽ gán nó cho cụm $c^{(i)}$ là cụm có trung tâm cụm gần nó nhất.

$c^{(i)} = argmin_{k} \lVert x^{(i)} - \mu_{k} \lVert^{2}$

Khi tất cả các điểm dữ liệu đã được gán về các cụm, bước tiếp theo là tính toán lại vị trí các trung tâm cụm bằng trung bình tọa độ các điểm dữ liệu trong cụm đó.

$\mu_{k} = \frac{1}{n}(x^{(k_{1})} + x^{(k_{2})} + ... + x^{(k_{n})})$

với $k_{1}, k_{2}, ..., k_{n}$ là chỉ số các dữ liệu thuộc cụm thứ k.

Các bước trên được lặp lại cho tới khi vị trí các trung tâm cụm không đổi sau một bước lặp nào đó.

<div class="separator" style="clear: both; text-align: center;">
<a href="https://3.bp.blogspot.com/-YwhPRp33Icg/XDqrJbA1cFI/AAAAAAAAERU/pp4Wx6weR5IRWC6-05T3Q8jMzKypIbzBwCLcBGAs/s1600/k%2Bmeans.gif" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="K-Means Clustering" border="0" data-original-height="375" data-original-width="500" src="https://3.bp.blogspot.com/-YwhPRp33Icg/XDqrJbA1cFI/AAAAAAAAERU/pp4Wx6weR5IRWC6-05T3Q8jMzKypIbzBwCLcBGAs/s1600/k%2Bmeans.gif" title="K-Means Clustering" /></a></div>
<h4>
Độ chính xác của thuật toán</h4>
Hàm mất mát của thuật toán K-Means Clustering đặc trưng cho độ chính xác của nó sẽ càng lớn khi khoảng cách từ mỗi điểm dữ liệu tới trung tâm cụm càng lớn.

$J(c^{(1)}, ..., c^{(m)}, \mu_{1}, ..., \mu_{K}) = \frac{1}{m}\sum_{i=1}^{m}\lVert x^{(i)} - \mu_{c^{(i)}} \lVert^{2}$
<h4>
Nghiệm của thuật toán K-Means Clustering</h4>
Trong các bước của thuật toán, thực chất bước gán các điểm dữ liệu về trung tâm cụm gần nhất và bước thay đổi trung tâm cụm về vị trí trung bình của các điểm dữ liệu trong cụm đều nhằm mục đích giảm hàm mất mát. Thuật toán kết thúc khi vị trí các trung tâm cụm không đổi sau một bước lặp nào đó. Khi đó hàm mất mát đạt giá trị nhỏ nhất.

Khi K càng nhỏ so với m, thuật toán càng dễ đi đến kết quả chưa phải tối ưu. Điều này phụ thuộc vào cách chọn K trung tâm cụm ban đầu.

<div class="separator" style="clear: both; text-align: center;">
<a href="https://3.bp.blogspot.com/-rrkJKQxS2iU/XDqu94rQBCI/AAAAAAAAERg/7ld-oIlnhMoEM89zvDMEdRpsJRXYpX4dACLcBGAs/s1600/Image%2B%255B10%255D.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Tối ưu địa phương K-Means Clustering" border="0" data-original-height="496" data-original-width="500" src="https://3.bp.blogspot.com/-rrkJKQxS2iU/XDqu94rQBCI/AAAAAAAAERg/7ld-oIlnhMoEM89zvDMEdRpsJRXYpX4dACLcBGAs/s1600/Image%2B%255B10%255D.png" title="Tối ưu địa phương K-Means Clustering" /></a></div>

Để khắc phục điều này, ta cần lặp lại thuật toán nhiều lần và chọn phương án có giá trị hàm mất mát nhỏ nhất.
<h3>
Tóm tắt thuật toán K-Means Clustering</h3>
<h4>
Yêu cầu</h4>
Cho trước m bộ dữ liệu $x^{(1)}, x^{(2)}, ..., x^{(m)}$. Nhiệm vụ của ta là phân chia các điểm dữ liệu thành K cụm dựa trên vị trí tương đối của chúng so với nhau.
<h4>
</h4>
<h4>
Thuật toán</h4>
<strong>Bước 1: </strong>Chọn ngẫu nhiên K trong số m điểm dữ liệu làm trung tâm cụm $\mu_{1}, \mu_{2}, ..., \mu_{K}$.

<strong>Bước 2:</strong>&nbsp;Gán mỗi điểm dữ liệu về cụm có trung tâm cụm gần nhất.

$c^{(i)} = argmin_{k} \lVert x^{(i)} - \mu_{k} \lVert^{2} $

<b>Bước 3:</b>&nbsp;Di chuyển các trung tâm cụm về vị trí trung bình của các điểm dữ liệu trong cụm tương ứng.

$\mu_{k} = \frac{1}{n}(x^{(k_{1})} + x^{(k_{2})} + ... + x^{(k_{n})})$

<b>Bước 4:</b>&nbsp;Lặp lại hai bước trên tới khi vị trí các trung tâm cụm không đổi sau một bước lặp nào đó.

<b>Bước 5:</b>&nbsp;Lặp lại tất cả các bước trên một số lần và chọn phương án có hàm mất mát nhỏ nhất.

$&nbsp;argmin_{c^{(1)}, ..., c^{(m)}, \mu_{1}, ..., \mu_{K}}J(c^{(1)}, ..., c^{(m)}, \mu_{1}, ..., \mu_{K})$
<h3>
Bạn đang nghĩ gì?</h3>
Bạn vừa được học thuật toán K-Means Clustering để phân cụm các điểm dữ liệu dựa theo vị trí tương đối của chúng so với nhau.

K-Means Clustering là thuật toán đơn giản và phổ biến, được biết đến như một trong những thuật toán Unsupervised Learning được sử dụng nhiều nhất.

Theo bạn, khác biệt giữa thuật toán K-Means Clustering so với những thuật toán loại Supervised Learning mà bạn đã học là gì?