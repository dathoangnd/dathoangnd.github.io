---
layout: default
title: Liên hệ
---

<div id="contact">
  <h2 class="pageTitle">{{ page.title }}</h2>
  <div class="contactContent">
    <p class="intro">Nếu bạn có thắc mắc, góp ý hoặc đơn giản muốn liên hệ, bạn có thể gửi tin nhắn tới tôi bằng biểu mẫu bên cạnh. Tôi sẽ trả lời bạn ngay khi có thể.</p>
    <p>Bạn cũng có thể <a target="_blank" href="mailto:dathoangnd@gmail.com">gửi email</a> cho tôi hoặc thông qua mạng xã hội có đường dẫn phía cuối trang.</p>
  </div>
  <form action="https://formspree.io/xzbapqpa" method="POST">
    <label for="name">Tên bạn</label>
    <input type="text" id="name" name="name" class="full-width"><br>
    <label for="email">Email</label>
    <input type="email" id="email" name="_replyto" class="full-width"><br>
    <label for="message">Tin nhắn</label>
    <textarea name="message" id="message" cols="30" rows="10" class="full-width"></textarea><br>
    <input type="submit" value="Send" class="button">
  </form>
</div>
