---
tag: diary
layout: post
title:  "Design principles & Design patterns"
description: "Tóm tắt lại các Design principles và Design patterns, đây là các kiến thức quan trọng cho Software Engineer để viết phần mềm tốt hơn."
---
### Design principles
#### Single responsibility
Mỗi class chỉ nên mang nhiệm vụ của một thứ.
<img class="post-image" class="post-image" src="{{ '/assets/img/single-responsibility.png' | prepend: site.baseurl }}" />

#### Open / Closed
Class nên mở với việc kế thừa và đóng với việc chỉnh sửa.
<img class="post-image" src="{{ '/assets/img/open-closed.png' | prepend: site.baseurl }}" />

#### Liskov substitution
Khi kế thừa một class, lưu ý để class con có thể truyền vào vị trí yêu cầu class cha mà không làm thay đổi logic code.
<img class="post-image" src="{{ '/assets/img/liskov-substitution.png' | prepend: site.baseurl }}" />

#### Interface segregation
Không nên bắt class con tạo thể hiện của phương thức interface mà nó không dùng.
<img class="post-image" src="{{ '/assets/img/interface-segregation.png' | prepend: site.baseurl }}" />

#### Dependency inversion
Class bậc cao không nên phụ thuộc vào class bậc thấp, cả hai nên phụ thuộc vào sự trừu tượng.
<img class="post-image" src="{{ '/assets/img/dependency-inversion.png' | prepend: site.baseurl }}" />


### Design patterns
#### Creational patterns
Cách nhớ: <b>A</b>braham <b>B</b>ecame <b>F</b>irst <b>P</b>resident of <b>S</b>tate.
##### Abstract factory
Cho phép tạo ra các nhóm của các object liên quan mà không phải xác định cụ thể class nào.
<img class="post-image" src="{{ '/assets/img/abstract-factory.png' | prepend: site.baseurl }}" />

##### Builder
Cho phép tạo ra các object phức tạp theo từng bước.
<img class="post-image" src="{{ '/assets/img/builder.png' | prepend: site.baseurl }}" />

##### Factory method
Cung cấp interface cho việc tạo ra các object từ class cha, nhưng để các class con quyết định loại object nào sẽ được tạo ra.
<img class="post-image" src="{{ '/assets/img/factory-method.png' | prepend: site.baseurl }}" />

##### Prototype
Cho phép tạo ra các object giống hệt một object có sẵn.
<img class="post-image" src="{{ '/assets/img/prototype.png' | prepend: site.baseurl }}" />

##### Singleton
Đảm bảo chỉ có một object của một class nào đó trong chương trình.
<img class="post-image" src="{{ '/assets/img/singleton.png' | prepend: site.baseurl }}" />

#### Structural patterns
Cách nhớ: <b>ABCDFFP</b>
##### Adapter
Cho phép các object với interface không tương thích tương tác với nhau.
<img class="post-image" src="{{ '/assets/img/adapter.png' | prepend: site.baseurl }}" />

##### Bridge
Cho phép tách một nhóm các class liên quan thành hai phân hệ là trừu tượng và thể hiện.
<img class="post-image" src="{{ '/assets/img/bridge.png' | prepend: site.baseurl }}" />

##### Composite
Giúp tạo ra cấu trúc phân cấp của các object.
<img class="post-image" src="{{ '/assets/img/composite.png' | prepend: site.baseurl }}" />

##### Decorator
Cho phép thêm hành động vào object bằng cách gói nó trong một object khác.
<img class="post-image" src="{{ '/assets/img/decorator.png' | prepend: site.baseurl }}" />

##### Facade
Tạo ra một interface đơn giản để sử dụng các class phức tạp bên dưới.
<img class="post-image" src="{{ '/assets/img/facade.png' | prepend: site.baseurl }}" />

##### Flyweight
Cho phép tái sử dụng tại các object có một phần dữ liệu không đổi.
<img class="post-image" src="{{ '/assets/img/flyweight.png' | prepend: site.baseurl }}" />

##### Proxy
Cho phép thực hiện một số hành động trước hoặc sau khi gọi phương thức của một object.
<img class="post-image" src="{{ '/assets/img/proxy.png' | prepend: site.baseurl }}" />

#### Behavioral patterns
Cách nhớ: <b>2 MICS O</b>n <b>TV</b>
##### Mediator
Cho phép các object giao tiếp với nhau qua một object trung gian.
<img class="post-image" src="{{ '/assets/img/mediator.png' | prepend: site.baseurl }}" />

##### Memento
Cho phép lưu và khôi phục object.
<img class="post-image" src="{{ '/assets/img/memento.png' | prepend: site.baseurl }}" />

##### Iterator
Cho phép duyệt một nhóm các object theo thứ tự.
<img class="post-image" src="{{ '/assets/img/iterator.png' | prepend: site.baseurl }}" />

##### Intepretor
Cho phép định nghĩa cách thể hiện ngữ pháp của một ngôn ngữ, và tạo ra object có khả năng xử lý được cách thể hiện đó.
<img class="post-image" src="{{ '/assets/img/intepretor.png' | prepend: site.baseurl }}" />

##### Chain of responsibility
Cho phép truyền một yêu cầu qua danh sách các object xử lý.
<img class="post-image" src="{{ '/assets/img/chain-of-responsibility.png' | prepend: site.baseurl }}" />

##### Command
Cho phép thực thi một yêu cầu mà không cần quan tâm tới object nào sẽ xử lý yêu cầu đó.
<img class="post-image" src="{{ '/assets/img/command.png' | prepend: site.baseurl }}" />

##### State
Cho phép một object thay đổi hành động khi trạng thái của nó thay đổi, giống như nó đã được thay đổi class.
<img class="post-image" src="{{ '/assets/img/state.png' | prepend: site.baseurl }}" />

##### Strategy
Cho phép định nghĩa một nhóm các thuật toán của một bài toán, và cho các object của chúng thay đổi được cho nhau.
<img class="post-image" src="{{ '/assets/img/strategy.png' | prepend: site.baseurl }}" />

##### Observer
Cho phép một nhóm object theo dõi sự thay đổi của một object và hành động khi có thay đổi.
<img class="post-image" src="{{ '/assets/img/observer.png' | prepend: site.baseurl }}" />

##### Template method
Cho phép định nghĩa các bước của một thuật toán trong class cha và để class con thay đổi hành động của một số bước đó.
<img class="post-image" src="{{ '/assets/img/template-method.png' | prepend: site.baseurl }}" />

##### Visitor
Cho phép tách rời thuật toán khỏi object nơi chúng được thực thi.
<img class="post-image" src="{{ '/assets/img/visitor.png' | prepend: site.baseurl }}" />
