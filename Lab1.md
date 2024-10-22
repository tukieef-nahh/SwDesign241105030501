
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
  + Chứa các lớp xử lý logic nghiệp vụ như <code>PaymentController</code> (xử lý chọn phương thức thanh toán), <code>TimecardManager</code> (xử lý cập nhật chấm công), và các quy trình tính toán lương dựa trên thời gian làm việc và thông tin chấm công.
  + Tầng này chính là nơi chứa tất cả các quy tắc và nghiệp vụ của hệ thống.
- <b> Data Layer (Tầng dữ liệu): </b>
  + Kết nối với cơ sở dữ liệu như <code>Project Management Database</code> và <code>Payroll Database</code> để lưu trữ thông tin chấm công, thanh toán, và nhân viên.
  + Tầng này chịu trách nhiệm lưu trữ và truy xuất dữ liệu.

#### 👉 Lý do lựa chọn và ý nghĩa của kiến trúc <code>three-tier architecture</code>:
- Tính mở rộng: Kiến trúc ba tầng dễ dàng mở rộng và phát triển thêm tính năng hoặc tích hợp với các hệ thống khác.
- Bảo trì dễ dàng: Các thay đổi trong một tầng không ảnh hưởng trực tiếp đến tầng khác, giúp bảo trì dễ dàng hơn.
- Tăng cường bảo mật: Tầng Business Logic có thể đảm nhận vai trò kiểm tra bảo mật và xác thực người dùng.

#### 👉 Package diagram mô tả kiến trúc:


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

## ⭐️ 3. Phân tích ca sử dụng Select Payment 📑
#### 👉 Các lớp phân tích cho ca sử dụng Select Payment: </b>
- <b> Entity classes: </b>
  + <b> Employee: </b> Người dùng chọn phương thức thanh toán, bao gồm các thuộc tính như: employeeID, name, PaymentMethod, address, bankName, accountNumber.
  + <b> PaymentMethod: </b> Lớp này lưu trữ thông tin về phương thức thanh toán mà nhân viên đã chọn (ví dụ: "pick up", "mail", "direct deposit").
- <b> Boundary classes: </b>
  + <b> PaymentBoundaryForm: </b> Lớp này chịu trách nhiệm giao tiếp với người dùng để thu thập thông tin phương thức thanh toán và hiển thị các yêu cầu hoặc lỗi.
- <b> Control classes: </b>
  + <b> PaymentController: </b> Lớp này điều phối luồng sự kiện giữa người dùng và hệ thống. Nó sẽ xác định phương thức thanh toán và cập nhật thông tin nhân viên sau khi nhận được thông tin đầu vào.

👉 <b> Sequence diagram cho ca sử dụng Payment: </b>

<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/d9GzKiCm48NxFSMMKAJWjr3114XImKo630TGh2NHH9Q4j6R6PwFWI5m1EOaJx1ZouswjVKzlFrd-_lpgHvQ1Yzm0n8Ms65ma09cn2pZClN4b4KnTOPKC9OvbcPFb1rTKvSY5739dEJXJBpskIaC1KgMvtBWCboL0NMFlhiDFu8N09pT3RM5tzPTckv70Iu4lz5vGP8naA6FqgoRCYUTEmOwcCce64tWbS4ISpP7gX4goX6RR7mckgmHS1DiITsxSDVMDm86EtiXoazrvrix6lS1k1Kx-cte_lmbPjIP7gkq2qZ2ETRRe5Rv-X-avYEchJnYePObdbHqM_Xp8HC9dgKs7SojtRRqzQwbKe1YNcdsGni5zQ4KDpN5yEfGdpRwS5l5-PRT6CD2XEa15taNDfy2OIhj8Uaxknn7P4Hw7vI_vIMoQ618Rcxw_W-zGwdZJ8PVLjKcMCSePGJzvLB-t7m000F__0m00" alt="Diagram">
</p>

👉 <b> Nhiệm vụ và các thuộc tính của các lớp phân tích: </b>
- <b> Employee (Entity): </b> Lưu trữ và cung cấp thông tin của nhân viên như tên, phương thức thanh toán, địa chỉ và chi tiết ngân hàng. Các thuộc tính:
  + <code>employeeID</code>: ID của nhân viên.
  + <code>name</code>: Tên nhân viên.
  + <code>paymentMethod</code>: Phương thức thanh toán hiện tại (Pick-up, Mail, Direct Deposit).
  + <code>address</code>: Địa chỉ (nếu chọn Mail).
  + <code>bankName</code>: Tên ngân hàng (nếu chọn Direct Deposit).
  + <code>accountNumber</code>: Số tài khoản ngân hàng.
 
- <b> PaymentMethod (Entity): </b> Lưu trữ thông tin về phương thức thanh toán mà nhân viên chọn. Các thuộc tính:
  + <code>methodType:</code> Loại phương thức thanh toán (Pick up, Mail, Direct Deposit).

- <b> PaymentBoundaryForm (Boundary): </b> Tương tác với người dùng, lấy thông tin đầu vào về phương thức thanh toán và hiển thị yêu cầu hoặc lỗi.
  + Các thuộc tính:
    - <code>employeeInput:</code> Input từ người dùng.
  + Các phương thức:
    - <code>getMethod():</code> Lấy phương thức thanh toán từ người dùng.
    - <code>displayError():</code> Hiển thị thông báo lỗi nếu không tìm thấy nhân viên.

- <b> PaymentController (Control): </b> Điều phối giữa PaymentBoudaryForm và Employee, thực hiện cập nhật phương thức thanh toán và xử lý logic chính.
  + Thuộc tính:
    - <code>currentEmployee:</code> Thông tin nhân viên hiện tại.
  + Phương thức:
    - <code>selectMethod():</code> Điều khiển luồng chọn phương thức thanh toán.
    - <code>updatePayment():</code> Cập nhật phương thức thanh toán trong cơ sở dữ liệu.

👉 <b> Xác định quan hệ giữa các lớp phân tích: </b>
- PaymentBoundaryForm tương tác với PaymentController để gửi và nhận dữ liệu, trong khi PaymentController sẽ tương tác với Employee và PaymentMethod để truy xuất và cập nhật thông tin cần thiết.

👉 <b> Class diagram mô tả các lớp phân tích và giải thích: </b>
<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/T98zRW8n48Lxdy9bAFOA22biGG6Y20SOx4b0-4ypus8LvMGfE5Aka8KrNhIRkBAV_JxFFFld-xfY0PBidL9yEGTDaL4fuu1Pxw7p6EImqPzAzwFHw9EB7U8cf2ntJUiFb2tAATgNHL7icPE3hYMAr8jV4zvh34BHEQJADPcetsaBld0O7PefF2SBWWNrJ7-OvyMkYn30OvccmJ-mYmRM4ZANrH72PJSQm9YOW-ooFoADdJykNOF0fCIsPlKU_qXXkBeMw-_Bjoxzqtnl7v-ZQPRpCDKytjkvccdDvybT-bzXiBSly0i00F__0m00" alt="Diagram">
</p>

- <b> Giải thích: </b>
  + <i> PaymentBoundaryForm: </i> Lớp boundary chịu trách nhiệm giao tiếp với nhân viên, thu thập dữ liệu đầu vào và hiển thị các thông báo lỗi hoặc yêu cầu. Lớp này không thực hiện bất kỳ logic nào liên quan đến nghiệp vụ.

  + <i> PaymentController: </i> Đây là lớp điều khiển, đóng vai trò điều phối toàn bộ luồng sự kiện giữa PaymentUI và Employee. Nó kiểm soát luồng xử lý từ việc yêu cầu phương thức thanh toán cho đến khi cập nhật thông tin vào cơ sở dữ liệu.

  + <i> Employee: </i> Lớp thực thể quản lý thông tin của nhân viên, bao gồm các thuộc tính và phương thức để truy xuất và cập nhật thông tin.

  + <i> PaymentMethod: </i> Lớp lưu trữ thông tin về phương thức thanh toán. Tùy vào phương thức thanh toán mà nhân viên chọn, lớp này sẽ lưu trữ thông tin phù hợp.
  
## ⭐️ 4. Phân tích ca sử dụng Maintain Timecard 📇
#### 👉 Các lớp phân tích cho ca sử dụng Maintain Timecard:
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

👉 <b> Nhiệm vụ của các lớp phân tích: </b>
- <b> Employee: </b> Nhân viên nhập và gửi thông tin chấm công hàng ngày.
- <b> Timecard: </b> Lưu trữ thời gian làm việc theo ngày, tuần.
- <b> TimecardManager: </b> Xử lý việc lưu trữ và kiểm tra thông tin thời gian làm việc.

👉 <b> Xác định quan hệ giữa các lớp phân tích: </b>
-

👉 <b> Class diagram mô tả các lớp phân tích và giải thích: </b>
- 

## ⭐️ 5. Hợp nhất kết quả phân tích 📁
#### 👉 Hợp nhất các ca sử dụng:
- <b> Employee: </b> Cho phép nhân viên quản lý thông tin cá nhân như cập nhật chấm công thời gian làm việc và phương thức thanh toán.
- <b> PaymentMethod: </b> Lớp chứa thông tin phương thức thanh toán (như "direct deposit", "mail", "pick up") và chứa thông tin chi tiết về lựa chọn của nhân viên.
- <b> Timecard: </b> Đảm bảo các lớp xử lý chỉ cho phép nhân viên tương tác với dữ liệu cá nhân của họ, chứa thông tin chi tiết về thời gian làm việc, ngày giờ mà nhân viên đã làm trong kỳ tính lương.
- <b> PaymentController: </b> Chịu trách nhiệm quản lý các yêu cầu liên quan đến phương thức thanh toán của nhân viên.
- <b> TimecardManager: </b> Chịu trách nhiệm xử lý các yêu cầu liên quan đến việc chấm công của nhân viên.

#### ⭐️ <i> From [Trần Thị Thanh Kiều](https://github.com/tukieef-nah) - 4451051111 </i> 💙
