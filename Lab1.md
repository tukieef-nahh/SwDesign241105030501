
# 🐳 Bài thực hành Lab1 <img src="https://media.giphy.com/media/fYSnHlufseco8Fh93Z/giphy.gif" width="30">
#### 📖 Mục đích 📝
Phân tích kiến trúc và ca sử dụng hệ thống "Payroll System" trong file tài liệu yêu cầu đính kèm.
</br>📑 Tài liệu yêu cầu
</br>📎 https://drive.google.com/file/d/1CSNZ0j5kiMHLyDXOxk1UHgETDVAHx6eP/view 

## ⭐️ 1. Phân tích kiến trúc 📈

#### 👉 Yêu cầu của bài toán:
Bài toán yêu cầu một hệ thống payroll (chấm công và thanh toán lương) với các chức năng chính như:
- Nhân viên chọn phương thức thanh toán (<code>Select Payment</code>).
- Nhân viên cập nhật và duy trì thông tin chấm công (<code>Maintain Timecard</code>).
- Bảo mật thông tin lương và chấm công của nhân viên.
- Tương tác với các hệ thống cơ sở dữ liệu hiện có (<code>Project Management Database</code>).
- Giao diện hệ thống là ứng dụng desktop.

#### 👉 Kiến trúc phù hợp cho bài toán này là kiến trúc <code>three-tier architecture</code> (kiến trúc ba tầng):
- <b> Presentation Layer (Tầng giao diện): </b>
  + Giao diện người dùng cho nhân viên và quản trị viên.
  + Các thành phần liên quan đến việc nhập thông tin chấm công, chọn phương thức thanh toán, thời gian làm việc và thực hiện các tác vụ khác.
- <b> Business Logic Layer (Tầng xử lý nghiệp vụ): </b>
  + Chứa các lớp xử lý logic nghiệp vụ như <code>PaymentManager</code> (xử lý chọn phương thức thanh toán), <code>TimecardManager</code> (xử lý cập nhật chấm công), và các quy trình tính toán lương dựa trên thời gian làm việc và thông tin chấm công.
  + Tầng này chính là nơi chứa tất cả các quy tắc và nghiệp vụ của hệ thống.
- <b> Data Layer (Tầng dữ liệu): </b>
  + Kết nối với cơ sở dữ liệu như <code>Project Management Database</code> và <code>Payroll Database</code> để lưu trữ thông tin chấm công, thanh toán, và nhân viên.
  + Tầng này chịu trách nhiệm lưu trữ và truy xuất dữ liệu.

#### 👉 Lý do chọn kiến trúc <code>three-tier architecture</code>:
- Tính mở rộng: Kiến trúc ba tầng dễ dàng mở rộng và phát triển thêm tính năng hoặc tích hợp với các hệ thống khác.
- Bảo trì dễ dàng: Các thay đổi trong một tầng không ảnh hưởng trực tiếp đến tầng khác, giúp bảo trì dễ dàng hơn.
- Tăng cường bảo mật: Tầng Business Logic có thể đảm nhận vai trò kiểm tra bảo mật và xác thực người dùng.

## ⭐️ 2. Cơ chế phân tích 🔬

#### 👉 Cơ chế cần giải quyết trong bài toán:

- <b> Cơ chế xác thực (Authentication): </b> Đảm bảo chỉ có nhân viên đăng nhập đúng thông tin mới có thể truy cập vào hệ thống Payroll.
- <b> Cơ chế phân quyền (Authorization): </b> Xác định quyền hạn của các đối tượng trong hệ thống, như Payroll Administrator có quyền thêm/sửa/xóa thông tin nhân viên.
- <b> Cơ chế tính toán lương (Payroll Calculation): </b> Tính toán lương cho nhân viên dựa trên loại nhân viên (lương theo giờ, lương theo tháng, hoặc lương kèm hoa hồng).
- <b> Cơ chế lưu trữ (Persistence): </b> Đảm bảo thông tin về timecard và phương thức thanh toán được lưu trữ chính xác trong cơ sở dữ liệu.
- <b> Cơ chế thông báo lỗi và bảo mật (Error Handling and Security): </b> Xử lý các lỗi trong quá trình tính toán hoặc truy xuất thông tin, và bảo mật dữ liệu nhạy cảm như thông tin tài khoản ngân hàng.



- <b> Cơ chế xử lý Payment (Thanh toán): </b>
  + Tạo giao dịch thanh toán cho nhân viên.
  + Quản lý các loại thanh toán khác nhau (chuyển khoản, tiền mặt, thẻ tín dụng).
  + Tính toán tiền lương dựa trên thời gian làm việc (thông qua Timecard).

- <b> Cơ chế xử lý Timecard (Thẻ chấm công): </b>
  + Ghi nhận thời gian làm việc của nhân viên hàng ngày.
  + Quản lý và tính toán tổng số giờ làm việc trong tuần/tháng.
  + Kết hợp thông tin Timecard với thanh toán để tính lương.

👉 <b> Lý do chọn các cơ chế: </b>
Những cơ chế này đảm bảo giải quyết bài toán chính là thanh toán lương cho nhân viên dựa trên thông tin thời gian làm việc đã được ghi nhận.

## ⭐️ 3. Phân tích ca sử dụng Payment 📑
#### 👉 Lớp phân tích cho ca sử dụng Payment: </b>
- <b> Employee: </b> Người dùng chọn phương thức thanh toán.
- <b> PaymentMethod:: </b> Chứa thông tin về phương thức thanh toán (direct deposit, mail, pick-up).
- <b> PaymentManager: </b>  Xử lý logic liên quan đến chọn và thay đổi phương thức thanh toán.

👉 <b> Sequence diagram cho ca sử dụng Payment: </b>
- <code>Employee</code> tương tác với <code>PaymentManager</code> để chọn phương thức thanh toán.
- <code>PaymentManager</code> gọi lớp <code>PaymentMethod</code> để lưu lại lựa chọn phương thức thanh toán của nhân viên.

<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/X91D2i9038NtEKNelXVeGWhYib0ekW-Tg8FpnqmKUZON7iahs8xJZHHS9NdvNXBoVhxQ91JbRWr0kcc7qIS6e55yn8CDna_C46P4ZpgG4wnwcYmxwSZHXME5bB3ljX6MgrU5o3d0EXFhtImsEB3XKR0ui61zz-tdgi4J6Qr8-0ysq6C3oH7hic_ltLb7IwAzo_vPNszgVinu3CjM1IqxjRpe0m00__y30000" alt="Diagram">
</p>

- Biểu đồ sequence sẽ mô tả quá trình từ khi nhân viên chọn phương thức thanh toán và hệ thống cập nhật thông tin vào cơ sở dữ liệu.

👉 <b> Nhiệm vụ của các lớp: </b>
- <b> Employee: </b> Lựa chọn, cung cấp thông tin và xác nhận phương thức thanh toán.
- <b> PaymentMethod: </b> Chứa thông tin về phương thức thanh toán của nhân viên.
- <b> PaymentManager: </b> Điều phối xử lý và lưu lại phương thức thanh toán được chọn.

## ⭐️ 4. Phân tích ca sử dụng Maintain Timecard 📇
#### 👉 Lớp phân tích cho ca sử dụng Maintain Timecard:
- <b> Employee: </b> Nhân viên nhập thông tin chấm công.
- <b> Timecard: </b> Lưu trữ và xử lý dữ liệu thời gian làm việc.
- <b> TimecardManager: </b> Xử lý logic cập nhật thông tin thời gian làm việc.

👉 <b> Sequence diagram cho ca sử dụng Maintain Timecard: </b>
- <code>Employee</code> tương tác với <code>TimecardManager</code> để nhập và gửi thông tin chấm công.
- <code>TimecardManager</code> lưu lại thông tin thời gian làm việc vào lớp <code>Timecard</code>.

<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/R9112i8m44NtSugX-rwW2oc4WfjkjE9wQ4O9RP8oIGNFvi8ZUGLZQuj8jtblteUy7iyoH98usXuWTCQX-C00r4OlMDcXztTc699YMZEGYvWrnd9BecjoT6N9a08szROpGmMmf33V9Rd0oaKMF7lfSEz72T3K4r857ZYAuHlZ4e56OVwzIt0KXseKuJIqAl_zqw0f_YRM_95IUiPwSs9vcypvCf5be43btSM8fMYyWvAT_dpU6m00__y30000" alt="Diagram">
</p>

- Biểu đồ sequence sẽ mô tả quá trình từ khi người dùng nhập thông tin <code>Timecard</code> thông qua <code>TimecardManager</code>, sau đó lưu dữ liệu vào <code>Timecard</code>.

👉 <b> Nhiệm vụ của các lớp: </b>
- <b> Employee: </b> Nhân viên nhập và gửi thông tin chấm công hàng ngày.
- <b> Timecard: </b> Lưu trữ thời gian làm việc theo ngày, tuần.
- <b> TimecardManager: </b> Xử lý việc lưu trữ và kiểm tra thông tin thời gian làm việc.

## ⭐️ 5. Hợp nhất kết quả phân tích 📁
#### 👉 Hợp nhất các ca sử dụng:
- <b> Employee: </b> Cho phép nhân viên quản lý thông tin cá nhân như cập nhật chấm công thời gian làm việc và phương thức thanh toán.
- <b> PaymentMethod: </b> Lớp chứa thông tin phương thức thanh toán (như direct deposit, mail, pick-up) và chứa thông tin chi tiết về lựa chọn của nhân viên.
- <b> Timecard: </b> Đảm bảo các lớp xử lý chỉ cho phép nhân viên tương tác với dữ liệu cá nhân của họ, chứa thông tin chi tiết về thời gian làm việc, ngày giờ mà nhân viên đã làm trong kỳ tính lương.
- <b> PaymentManager: </b> Chịu trách nhiệm quản lý các yêu cầu liên quan đến phương thức thanh toán của nhân viên.
- <b> TimecardManager: </b> Chịu trách nhiệm xử lý các yêu cầu liên quan đến việc chấm công của nhân viên.

#### ⭐️ <i> From [Trần Thị Thanh Kiều](https://github.com/tukieef-nah) - 4451051111 </i> 💙
