---
tag: learn
layout: post
title:  "Bài 18: Ứng Dụng Thuật Toán Anomaly Detection"
description: "Trong bài này chúng ta sẽ ứng dụng thuật toán Anomaly Detection trong Machine Learning để phát hiện lượt truy cập bất thường của website."
---

Trong bài này, ta sẽ tìm cách phát hiện lượt truy cập bất thường của website thông qua việc xử lý số liệu được ghi lại.

Thuật toán Anomaly Detection là giải pháp cho bài toán này.
<!--more-->
<h3>
Đặt vấn đề</h3>
Website của công ty X là một website lớn với hàng chục nghìn lượt truy cập mỗi ngày. Để đề phòng việc bị sử dụng sai mục đích, website luôn ghi lại thông tin về mỗi lượt truy cập của người dùng gồm thời gian truy cập tính bằng phút và số lần bấm chuột trong thời gian đó. Dưới đây là số liệu của 20 lượt truy cập gần đây nhất.

<div class="separator" style="clear: both; text-align: center;">
<a href="https://4.bp.blogspot.com/-4iZtJLgtVnc/XDwtP7b_M2I/AAAAAAAAETQ/njRKO61i93UrakxaRORKehn4IS8yZQNEgCLcBGAs/s1600/Untitled.jpg" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img alt="Bảng thời gian truy cập và số lần bấm chuột" border="0" data-original-height="583" data-original-width="500" src="https://4.bp.blogspot.com/-4iZtJLgtVnc/XDwtP7b_M2I/AAAAAAAAETQ/njRKO61i93UrakxaRORKehn4IS8yZQNEgCLcBGAs/s1600/Untitled.jpg" title="Bảng thời gian truy cập và số lần bấm chuột" /></a></div>
<div class="separator" style="clear: both; text-align: center;">
</div>
<div class="separator" style="clear: both; text-align: center;">
</div>
<div class="separator" style="clear: both; text-align: center;">
</div>
<div class="separator" style="clear: both; text-align: center;">
</div>
<div class="separator" style="clear: both; text-align: center;">
</div>
<div class="separator" style="clear: both; text-align: center;">
</div>
<div class="separator" style="clear: both; text-align: center;">
</div>

Bây giờ, có một lượt truy cập mới được ghi lại. Ta cần xác định xem lượt truy cập đó liệu có bình thường hay không.

Trong bài này, để đơn giản ta sẽ giả định hai điều. Thứ nhất, ta coi 20 mẫu dữ liệu trên đại diện cho toàn bộ dữ liệu đã ghi lại. Thứ hai, ta coi như các biến đã có phân phối chuẩn, mặc dù điều này chỉ rõ ràng khi số lượng mẫu dữ liệu lớn.
<h3>
Giải quyết vấn đề</h3>
Các bước cài đặt thuật toán

<b>Bước 1:</b>&nbsp;Chọn $\epsilon = 0.0003$.

<strong>Bước 2:</strong>&nbsp;Tìm hàm phân bố p(x).

<strong>Bước 3:</strong>&nbsp;Nếu $p(x_{test}) &lt; \epsilon$ ta kết luận $x_{test}$ bất thường, ngược lại ta kết luận $x_{test}$ bình thường.

Mở trình soạn thảo yêu thích của bạn, tạo file&nbsp;<strong>bai18.html</strong>&nbsp;rồi dán vào đoạn code sau

<script src="https://gist.github.com/dathoangnd/a2321256916f35532ccc5d4991d48f00.js"></script>
Ta được kết quả

<i>Lượt truy cập trong 10 phút và có 20 lần bấm chuột là bình thường.</i>

<i>Lượt truy cập trong 15 phút và có 38 lần bấm chuột là bất thường.</i>
<h3>
Giờ đến lượt bạn</h3>
Hãy thay đổi cài đặt thuật toán để tính hàm phân bố bằng tích các hàm phân bố của từng biến. Bạn có nhận được kết quả như trên không?