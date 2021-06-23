# ANSIBLE
# Ansible là gì?
  - Trong một môi trường với nhiều server thì ta sẽ có vô vàn thứ phải lo. Từ setup crontab, update các gói phần mềm mới, deploy ứng dụng mới, chỉnh sửa file cấu hình..... Những công việc này tuy không khó, nhưng rất mất thời gian của những người quản trị. Vậy có cách nào để tự động hóa những thao tác nhàm chán, lặp đi lặp lại này không??
Câu trả lời chính là ứng dụng những tool automation để quản trị hệ thống. Hiện nay có rất nhiều tool như vậy trên thị trường cụ thể như: Chef, Puppet, CFEngine, StackStorm, Ansible, SaltStack… Trong bài này, mình sẽ giới thiệu đến các bạn một công cụ rất mạnh mẽ trong việc quản trị hệ thống, đó chính là Ansible.
  - Như đã nói ở trên, Ansible là một công cụ dùng để tự động hóa việc cấu hình trên nhiều server. So với các công cụ khác với tính năng tương đương thì Ansible dễ học và dễ tiếp cận hơn rất nhiều. Cộng đồng người dùng cũng nhiều hơn so với các công cụ khác.
  - Có thể thấy Ansible là công cụ tự động hóa phổ biến nhất trên GitHub với số sao được người dùng bình chọn cho project này là 33,500 sao. Ansible cũng là tool dễ tiếp cận và làm quen do được build bằng Python và sử dụng file cấu hình theo dạng YAML dễ đọc và dễ hiểu.
# Kiến túc và cách hoạt động
  - Ansible sử dụng kiến trúc agentless để giao tiếp với các máy khác mà không cần agent. Cơ bản nhất là giao tiếp thông qua giao thức SSH trên Linux, WinRM trên Windows hoặc giao tiếp qua chính API của thiết bị đó cung cấp.
  - Giống như đa phần các phần mềm quản lý cấu hình tập trung khác. Ansible có 2 loại server là control machine và node. Control machine là máy có trách nhiệm quản lý các node con trong hệ thống. Đây cũng là máy lưu trữ các thông tin về các node, playbook và các script cần dùng để deploy trên các node khác qua giao thức SSH.
  - Để quản lý các node, Ansible sẽ gởi các module lệnh tới các node con qua SSH. Các module lệnh này sẽ được lưu trữ tạm thời trên các node con và giao tiếp với máy chủ Ansible bằng JSON. Khi đã thực thi xong tác vụ trên các máy này, các module đó sẽ được xóa đi. Các module này thường được lưu ở folder /root/.ansible hoặc /home/<user>/.ansible, tùy theo user mà Ansible dùng để quản lý các node con.
  - Khi Ansible ở chế độ rảnh, ko có task để thực hiện máy chủ Ansible sẽ không chiếm dụng tài nguyên do Ansible không sử dụng trình daemon hoặc program chạy ở chế độ background. Chỉ khi nào thực thi lệnh thì Ansible mới sử dụng tài nguyên của hệ thống.
  ![image](https://user-images.githubusercontent.com/80019984/123049465-c6439e80-d429-11eb-9a94-6c31d8390ee0.png)

# Các Thuật ngữ quan trọng trong Ansible
  + Ansible server: là nơi ansible được cài đặt và từ đó tất cả các tasks và playbooks sẽ được chạy
  + Module: là một lệnh hoặc tập hợp các lệnh tương tự được thực thi ở client-side. Khi chúng ta giao tiếp với Ansible sẽ thông qua module
  + Task: một task xác định một công việc đơn lẻ được hoàn thành, là những công việc nhỏ trong playbooks
  + Role: Một tập hợp các Playbook, các file liên quan được tổ chức theo cách được xác định trước để tạo điều kiện tái sử dụng và chia sẻ
  + Fact: các biến toàn cục chứa các thông tin về hệ thống
  + Playbook: một file YAML chứa một tập các công việc cần tự động hóa
  + Inventory: một file INI chứa các thông tin về các server từ xa mà bạn quản lý.
  + Play: một lần thực thi một Playbook
  + Handler: sử dụng để kích hoạt thay đổi trạng thái các service
  + Tag: tên được đặt cho một task, có thể được sử dụng sau này có nhiệm vụ chỉ cụ thể task hoặc một nhóm các task
  
