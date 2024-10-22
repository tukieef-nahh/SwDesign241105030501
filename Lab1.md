
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
- <b> Tính mở rộng: </b> Kiến trúc ba tầng dễ dàng mở rộng và phát triển thêm tính năng hoặc tích hợp với các hệ thống khác.
- <b> Bảo trì dễ dàng: </b> Các thay đổi trong một tầng không ảnh hưởng trực tiếp đến tầng khác, giúp bảo trì dễ dàng hơn.
- <b> Tăng cường bảo mật: </b> Tầng Business Logic có thể đảm nhận vai trò kiểm tra bảo mật và xác thực người dùng.

#### 👉 Package diagram mô tả kiến trúc:
<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/Z5QzZjGm4Exp5DOs_4Zx0XJeTDmXa6vFLvn4WIXcdM5ZDh73s5uKeQkfgQbu0XvW2mgUP9-0Ly29avoTE7UuM6d7CzytFzzO-NlyVQODaB5LcUcza8oKnYohWUzXXsnrGwXH6Z12INO53TAAVSsOExm4hTcjg903vUVAoXoeUQsewXtyoOMkIsW6lwVFWhiTchUojYOoQhkjX9duttM_0UyDD9NBQu5spR2gIzKWTlWnvGPDeU94-YGlYHGjCLxsY6cQYy0eeSBWR-rJzRI17VBSDLS7bYt8_NKS39ox4isrhRP8WPrR8WSwj2ckS4Zr0Wn4TTew1uENOsy-gh7Qks3evrOBwL9ZLsed-4DZtu1q4HHDt9EyKPPqH7w0KhGtIIaafpuMb0w1mnHhIIQlb3IaoZBAT6pYq8yG6qlaAQNuudhOaNNEw4CZjgeptJRr8qGn7AbFpY42ghqjqbnlcwY75q0x3CGJOG_DYy1DRupGkoV2gId4HfbFB4KxydUAzfY__x2GXOvk7AwnuGPu6HYyXuwLsIewfSVMlWMDRj3IjQ5zh499Sc-UxdniJecd5Ss07I5gesYGGR17_X0Q4dX8tCyv_Dpy7hNE3x3rOrzaczrtlNl2DgVZTy4-Mv2iE1s_iPqu7Ny1utz-SbQUZZ_gBFcAhzSlPtl-WgsiHhrYMUe1RYFc6pV4PECBke3i-g6uS8FNx8imXIE98fB8GXeau6OCoQR0pzVhUwMxYAgpjoLCFPNp7FOjcSuyWo2lVkFdrRO9p7mAI6NGmYMaFElw98F7GY8LBmVqwz05BSholyApC_Swj9yK_m000F__0m00" alt="Diagram">
</p>

## ⭐️ 2. Cơ chế phân tích 🔬

#### 👉 Cơ chế cần giải quyết trong bài toán:
- <b> Cơ chế xác thực (Authentication): </b>
  + Đảm bảo chỉ có nhân viên đăng nhập đúng thông tin mới có thể truy cập vào Payroll System.
  + <b> Lý do: </b> Bảo vệ hệ thống tránh truy cập trái phép và đảm bảo bảo mật thông tin của nhân viên.

- <b> Cơ chế phân quyền (Authorization): </b>
  + Xác định quyền hạn của các đối tượng trong hệ thống, như <code>Payroll Administrator</code> có quyền quản lý thông tin nhân viên và xử lý chấm công, nhân viên thông thường chỉ có quyền nhập và xem thông tin cá nhân và timecard của mình.
  + <b> Lý do: </b> Đảm bảo rằng mỗi người dùng chỉ có thể truy cập và thao tác trong phạm vi quyền hạn của mình, tránh xung đột quyền và bảo mật thông tin.

- <b> Cơ chế tính toán lương (Payroll Calculation): </b>
  + Tính toán lương cho nhân viên dựa trên loại nhân viên (lương theo giờ, lương theo tháng, lương tăng ca hoặc lương kèm hoa hồng).
  + <b> Lý do: </b> Đảm bảo rằng lương của nhân viên được tính toán chính xác và kịp thời, dựa trên thông tin <code>timecard</code> và các thông tin liên quan khác.

- <b> Cơ chế lưu trữ (Persistence): </b>
  + Đảm bảo thông tin về <code>timecard</code>, thông tin nhân viên và phương thức thanh toán được lưu trữ chính xác trong cơ sở dữ liệu.
  + <b> Lý do: </b> Đảm bảo thông tin chấm công và thanh toán của nhân viên được bảo quản an toàn, có thể truy xuất và chỉnh sửa khi cần thiết.

- <b> Cơ chế thông báo lỗi và bảo mật (Error Handling and Security): </b>
  + Xử lý các lỗi phát sinh trong quá trình tính toán, nhập liệu, hoặc truy xuất dữ liệu và bảo mật dữ liệu nhạy cảm như thông tin tài khoản ngân hàng.
  + <b> Lý do: </b> Bảo vệ dữ liệu nhạy cảm và giúp người dùng có trải nghiệm mượt mà bằng cách hiển thị thông báo lỗi khi có sự cố.
 
- <b> Cơ chế giao tiếp với cơ sở dữ liệu khác (Integration with External Databases): </b>
  + Hệ thống cần tích hợp với các cơ sở dữ liệu khác, như <code>Project Management Database</code>, để lấy thông tin về mã  <code>charge number</code>, hoặc các dữ liệu liên quan đến dự án mà nhân viên đang làm việc.
  + <b> Lý do: </b> Đảm bảo rằng thông tin chấm công và dự án của nhân viên được đồng bộ và chính xác.
 
- <b> Cơ chế backup và phục hồi dữ liệu (Backup and Recovery): </b>
  + Cơ chế này đảm bảo rằng dữ liệu payroll của hệ thống được sao lưu định kỳ và có thể phục hồi khi xảy ra sự cố hoặc mất dữ liệu.
  + <b> Lý do: </b> Đảm bảo an toàn cho dữ liệu quan trọng và tránh mất mát thông tin trong trường hợp hệ thống gặp sự cố.


## ⭐️ 3. Phân tích ca sử dụng Select Payment 📑

#### 👉 Các lớp phân tích cho ca sử dụng Select Payment: </b>
- <b> Entity classes: </b>
  + <b> Employee: </b> Người dùng chọn phương thức thanh toán, bao gồm các thuộc tính như: <code>employeeID</code>, <code>name</code>, <code>PaymentMethod</code>, <code>address</code>, <code>bankName</code>, <code>accountNumber</code>.
  + <b> PaymentMethod: </b> Lớp này lưu trữ thông tin về phương thức thanh toán mà nhân viên đã chọn (ví dụ: <code>Pick up</code>, <code>Mail</code>, <code>Direct deposit</code>).
- <b> Boundary classes: </b>
  + <b> PaymentBoundaryForm: </b> Lớp này chịu trách nhiệm giao tiếp với người dùng để thu thập thông tin phương thức thanh toán và hiển thị các yêu cầu hoặc lỗi.
- <b> Control classes: </b>
  + <b> PaymentController: </b> Lớp này điều phối luồng sự kiện giữa người dùng và hệ thống. Nó sẽ xác định phương thức thanh toán và cập nhật thông tin nhân viên sau khi nhận được thông tin đầu vào.

👉 <b> Sequence diagram cho ca sử dụng Payment: </b>

<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/b9HFKi8m58VtESLRwW9cfFWl2mSLMEaCe-C1GlE436aIazIPdis5H_8A9a2Hba9hTw_9xylBbxG_NzyZvvdrUIO9SIkXm6g7XB3KQmkJp4XT89AvpXLdje0PAp9K_a7diPngcv5KAs-rB8SUDwL4Iq8bVB6ZJDOb8MKDlRi67eKB2azw0KAHmz6zpDz250OKNl0ZH-V1eSJKWzbCWWpzKdDoa8cWQcCK4WfJzEaIiEoGCyz8TTgH3eQn0vzRLGitBjoqwqiAO-6CPCMkTssyqCgr2hkYy7fgr-t-hYD1yQqyv7KGOTB3JAIhNcxATn2UJbfl-k54tqpGWJKkd4KcvEQSe7G8pqp81doj_v8VoOF8Be-USMxHkNMqpLcCXbipi_fJSAn4ErkBZ6HhhW7GPcNG7nxriZO1SB-XRlMCXOs7pD5e9_p_H2NxekPChGB6XqMwsahsRHta_w4isIaxHcdpbfpmLbKKlAbmUJj_WxSKmgHtOJCMlxn0TOuja8m29luXVm400F__0m00" alt="Diagram">
</p>

👉 <b> Nhiệm vụ và các thuộc tính của các lớp phân tích: </b>
- <b> Employee (Entity): </b> Lưu trữ và cung cấp thông tin của nhân viên như tên, phương thức thanh toán, địa chỉ và chi tiết ngân hàng. Các thuộc tính:
  + <code>employeeID</code>: ID của nhân viên.
  + <code>name</code>: Tên nhân viên.
  + <code>paymentMethod</code>: Phương thức thanh toán hiện tại (<code>Pick-up</code>, <code>Mail</code>, <code>Direct Deposit</code>).
  + <code>address</code>: Địa chỉ (nếu chọn <code>Mail</code>).
  + <code>bankName</code>: Tên ngân hàng (nếu chọn <code>Direct Deposit</code>).
  + <code>accountNumber</code>: Số tài khoản ngân hàng.
 
- <b> PaymentMethod (Entity): </b> Lưu trữ thông tin về phương thức thanh toán mà nhân viên chọn. Các thuộc tính:
  + <code>methodType:</code> Loại phương thức thanh toán (<code>Pick-up</code>, <code>Mail</code>, <code>Direct Deposit</code>).

- <b> PaymentBoundaryForm (Boundary): </b> Tương tác với người dùng, lấy thông tin đầu vào về phương thức thanh toán và hiển thị yêu cầu hoặc lỗi.
  + Các thuộc tính:
    - <code>employeeInput:</code> Input từ người dùng.
  + Các phương thức:
    - <code>getMethod():</code> Lấy phương thức thanh toán từ người dùng.
    - <code>displayError():</code> Hiển thị thông báo lỗi nếu không tìm thấy nhân viên.

- <b> PaymentController (Control): </b> Điều phối giữa <code>PaymentBoudaryForm</code> và <code>Employee</code>, thực hiện cập nhật phương thức thanh toán và xử lý logic chính.
  + Thuộc tính:
    - <code>currentEmployee:</code> Thông tin nhân viên hiện tại.
  + Phương thức:
    - <code>selectMethod():</code> Điều khiển luồng chọn phương thức thanh toán.
    - <code>updatePayment():</code> Cập nhật phương thức thanh toán trong cơ sở dữ liệu.

👉 <b> Xác định quan hệ giữa các lớp phân tích: </b>
- <code>PaymentBoundaryForm</code> tương tác với <code>PaymentController</code> để gửi và nhận dữ liệu, trong khi <code>PaymentController</code> sẽ tương tác với <code>Employee</code> và <code>PaymentMethod</code> để truy xuất và cập nhật thông tin cần thiết.

👉 <b> Class diagram mô tả các lớp phân tích và giải thích: </b>

<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/T99BJiCm48RtFiNiU4Yfr2qBL463n88A0HUOnbCQrI_Ds8i8SJ8M78aha2PEYfBYbUVtpEVnF_xv-bv9H8x96gNaK3jWBwHKPL04dh6nvEATJquZDm-UBNmeQ5S1P8Fn3T6Z2obs6i0xnIUAUwylhxAYQma6cvBPSoj-JiZttaNsnX2Ft2enjoTbncUEaA5g2az1OwIC-aiVYkVDhhFWq5BUXhw-PsSDjMOIoT4MtM5pAi2gQWs9csItnAUN3vUkCUAanNBqQkVFkD1VFJPhk_2j2VyylYs_W1So66llP5y7WPrdUEso1gOwDxkYk9qxh-QpEEQD0nZDl2wAISSti5mibg3KYfm-Vg5V0000__y30000" alt="Diagram">
</p>

- <b> Giải thích: </b>
  + <i> PaymentBoundaryForm: </i> Lớp boundary chịu trách nhiệm giao tiếp với nhân viên, thu thập dữ liệu đầu vào và hiển thị các thông báo lỗi hoặc yêu cầu. Lớp này không thực hiện bất kỳ logic nào liên quan đến nghiệp vụ.

  + <i> PaymentController: </i> Đây là lớp điều khiển, đóng vai trò điều phối toàn bộ luồng sự kiện giữa <code>PaymentBoundaryForm</code> và <code>Employee</code>. Nó kiểm soát luồng xử lý từ việc yêu cầu phương thức thanh toán cho đến khi cập nhật thông tin vào cơ sở dữ liệu.

  + <i> Employee: </i> Lớp thực thể quản lý thông tin của nhân viên, bao gồm các thuộc tính và phương thức để truy xuất và cập nhật thông tin.

  + <i> PaymentMethod: </i> Lớp lưu trữ thông tin về phương thức thanh toán. Tùy vào phương thức thanh toán mà nhân viên chọn, lớp này sẽ lưu trữ thông tin phù hợp.
  
## ⭐️ 4. Phân tích ca sử dụng Maintain Timecard 📇

#### 👉 Các lớp phân tích cho ca sử dụng Maintain Timecard:
- <b> Entity classes: </b>
  + <b> Timecard: </b> Lớp chứa thông tin về bảng chấm công của nhân viên, như số giờ làm việc, ngày làm việc, và trạng thái của timecard.
  + <b> Employee: </b> Lớp thông tin của nhân viên. Nhân viên có thể truy cập và chỉnh sửa timecard của mình.
  + <b> Project: </b> Lớp chứa thông tin về các dự án mà nhân viên có thể phân bổ số giờ làm việc.
- <b> Boundary classes: </b>
  + <b> TimecardBoundaryForm: </b> Giao diện tương tác với người dùng, cho phép nhân viên nhập giờ làm việc và nộp timecard.
- <b> Control classes: </b>
  + <b> TimecardController: </b> Điều phối các luồng sự kiện như tạo, cập nhật và nộp timecard. Lớp này cũng chịu trách nhiệm kiểm tra các ràng buộc về giờ làm việc.

👉 <b> Sequence diagram cho ca sử dụng Maintain Timecard: </b>

<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/b5HBRjim4Dtp5BDC5pPYksbIBeAWRHeKw2B8f_knD8XPKwGx7BhGsRB8aNA5K98jkOhTA5e8a8RlmpT3FZy-NGH1bbXOfSBIE60VI2dCn3DS5YlhIo8rzz7bo2NScO8ovFpBviTtpuNAl1FsjYr-RRujiI8dHZhOzlkQ_M_AHAcj0epEzt9hc6ZuwH_0EBMllelhP3LCDTpGdqX188lCIHPaw-7r-bqM3RCAAsneJOV1XuG_rk38xYszJGGQJZHSaG2kqLYSswIvG7uWSB6O4mUrMNX8y5ChsCFzVvl_XdoguPi9AujbQnlGvNtA0Uqwqt3f96ajVEG0VpqlgU4APAjj770vfAcVDTnIOcejnbMEGiaNMe5VQ4rNKv2UjpezEHwdyRh5rEWMHpOG_73hcgtUn02gtiWUZwTTeCJiguEG3vhsoa-S5sRFo0s9Q39jyTpC_suueQg4OBmR5iziFAa2kgzZxc9FDuR40E8RGX4Q67V5D-q5Niz6WKjAXZ4VUMVBfWVjIKDRLSftYVLIdRrg21or1apef3_KZRf8htGZlW000F__0m00" alt="Diagram">
</p>

👉 <b> Nhiệm vụ và các thuộc tính của các lớp phân tích: </b>
- <b> Employee (Entity): </b> Lớp này chứa thông tin về nhân viên và kết nối với timecard. Nhân viên có thể cập nhật giờ làm việc của mình. Các thuộc tính:
  + <code>employeeID</code>: Mã nhân viên.
  + <code>name</code>: Tên nhân viên.
  + <code>currentTimecard</code>: Tham chiếu đến timecard hiện tại của nhân viên.

- <b> Timecard (Entity): </b> Lưu trữ dữ liệu về giờ làm việc trong tuần, dự án mà giờ làm việc được tính vào và trạng thái của timecard. Các thuộc tính:
  + <code>timecardID</code>: ID của timecard.
  + <code>startDate</code>: Ngày bắt đầu kỳ chấm công.
  + <code>endDate</code>: Ngày kết thúc kỳ chấm công.
  + <code>hoursWorked[]</code>: Mảng chứa số giờ làm việc của mỗi ngày.
  + <code>chargeNumbers[]</code>: Dự án tương ứng với số giờ làm việc.
  + <code>status</code>: Trạng thái (draft, submitted).
  + <code>submittedDate</code>: Ngày nộp timecard.

- <b> Project (Entity): </b> Lớp chứa thông tin về các dự án mà giờ làm việc có thể được tính vào. Các thuộc tính:
  + <code>projectID</code>: ID của dự án.
  + <code>projectName</code>: Tên dự án.
  + <code>chargeNumber</code>: Số để tính chi phí cho dự án.
 
- <b> TimecardBoundaryForm (Boundary): </b> Giao diện tương tác với nhân viên để nhập và nộp bảng chấm công. Các phương thức:
  + <code>displayTimecard()</code>: Hiển thị thông tin timecard.
  + <code>getInput()</code>: Nhận đầu vào từ nhân viên (giờ làm việc, số dự án).
  + <code>submitTimecard()</code>: Thực hiện nộp bảng chấm công.

- <b> TimecardController (Control): </b> Điều khiển luồng sự kiện, xác minh tính hợp lệ của timecard, xử lý việc lưu và nộp. Các phương thức:
  + <code>getTimecard()</code>: Lấy timecard hiện tại của nhân viên.
  + <code>saveTimecard()</code>: Lưu thông tin timecard.
  + <code>submitTimecard()</code>: Nộp timecard và khóa không cho chỉnh sửa thêm.

👉 <b> Xác định quan hệ giữa các lớp phân tích: </b>
- <code>TimecardBoundary</code> tương tác với <code>TimecardController</code> để gửi và nhận thông tin từ người dùng.
- <code>TimecardController</code> kết nối với cả <code>Timecard</code> và <code>Project</code> để lấy và cập nhật thông tin thời gian làm việc cũng như các dự án tương ứng.

👉 <b> Class diagram mô tả các lớp phân tích và giải thích: </b>

<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/X9EzJiCm58LtFyNTW4gfwDe15IY8BXK34WDYSEEhnjH_ig-B8iIJCV18l099STmeRKMsStpowHxh-kVhUnQ8UufQCHOsqe2t0Hah5Gy1dgJ6adjnOwCHtDVtrcluOB3xX0nEyRhBd5yaVusqC2vIDa9SQKcztEUGVsiDUQiK-anlA0VamBTuQFvBJym2A1cBUJ9srUUSC6aqegSg6trujdw3ukKrUMN5_HgNKQ_GX-ms78gX4xk12FSeWEX48nvQO1vyovLitHED-atkj5EsHinDC1cvYU6w6xkCtgF9DxAdF7hxXYLbYFlJcP7qieVgjMqvPt0jX3HhyAWuIMj29Ls0TqaLwAX8EYLBIJLm8w2qsjaWsnWxkaX5SNLa0zYHfUWdOGgJyNXqAjQLdC9bcyetDogA0MAI4M2Rmy6FRDOiG_igVW400F__0m00" alt="Diagram">
</p>

- <b> Giải thích: </b>
  + <i> TimecardBoundaryForm: </i> Lớp biên nhận đầu vào từ nhân viên, cho phép họ nhập số giờ làm việc và nộp bảng chấm công. Lớp này cũng xử lý việc hiển thị các thông báo lỗi nếu có.

  + <i> TimecardController: </i> Lớp điều khiển quản lý luồng xử lý của bảng chấm công, bao gồm việc lấy dữ liệu từ timecard hiện tại, lưu thay đổi và kiểm tra tính hợp lệ của dữ liệu trước khi nộp.

  + <i> Timecard: </i> Lớp thực thể chứa thông tin về bảng chấm công, bao gồm số giờ làm việc, các dự án và trạng thái của bảng chấm công.

  + <i> Project: </i> Lớp thực thể lưu trữ thông tin về dự án và mã số mà thời gian làm việc của nhân viên sẽ được tính vào.

## ⭐️ 5. Hợp nhất kết quả phân tích 📁

👉 <b> Hợp nhất các lớp phân tích: </b>
- <b> Lớp chung: </b>
  + <code>Employee:</code> Lớp nhân viên cần thiết trong cả hai ca sử dụng để lưu trữ thông tin về phương thức thanh toán cũng như bảng chấm công.
- <b> Điểm hợp nhất: </b>
  + Cả hai ca sử dụng đều cần có cơ chế xác thực và lưu trữ dữ liệu (<code>payment method</code> và <code>timecard</code>).
  + Có thể kết hợp giao diện người dùng trong một module EmployeeBoundaryForm, cung cấp cả chức năng chọn phương thức thanh toán và cập nhật bảng chấm công.



- <b> Employee: </b> Cho phép nhân viên quản lý thông tin cá nhân như cập nhật chấm công thời gian làm việc và phương thức thanh toán.
- <b> PaymentMethod: </b> Lớp chứa thông tin phương thức thanh toán (như <code>Direct deposit</code>, <code>Mail</code>, <code>pick up</code>) và chứa thông tin chi tiết về lựa chọn của nhân viên.
- <b> Timecard: </b> Đảm bảo các lớp xử lý chỉ cho phép nhân viên tương tác với dữ liệu cá nhân của họ, chứa thông tin chi tiết về thời gian làm việc, ngày giờ mà nhân viên đã làm trong kỳ tính lương.
- <b> PaymentController: </b> Chịu trách nhiệm quản lý các yêu cầu liên quan đến phương thức thanh toán của nhân viên.
- <b> TimecardManager: </b> Chịu trách nhiệm xử lý các yêu cầu liên quan đến việc chấm công của nhân viên.

<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/X9IzRjH04CVxVOhf894SaJO5YY27YCH5aHA90b7CsSFPdBrhzYEIXLAdfgQCKY5U82vu5Zy1hy3QtjtprucJNCnuxhV_-S-i_zP_pfL6gKsHCxNBE4YXYB4NyA6fVvQWc_eNh37ZsZvmcnKKeqnOdADI8NmZ34zGLk-4BE0xW-wNPAhCiV8rBuzSValwafT6XuGocoBJWxfxDk6_5LnBaUSa0zrIPcI5TpHF_fVkc15ebxYyS8dEc0lKv6BYoI1AXP7gev0xIZvzThauHRcbArDiIAgGjHnjb0ywGPhsA01J9ZPutmA3y3lCipPxeADX9zTIVALOXqRAFWvzkFWA2rhGsN96uxwXlALTOrKGr_wCFbeOjVMbA7DH4NLptGzeJJeLUzrk8LPI2ZbItvDdGxOgZPJspShXVV-Tl0cyTz2X5kXzUI0NNNXRbGUW0qlywP0szMC9F6sUdxmfuTtC2MyzttjU3fMu72Q99ELNOuDyDnWInh5rMxifZIm95p6OxQNOhSA9AwimdY_2zxPkwXyPV3F8sxuU-i77pVCZf9X1ZA2Q-ZSaJVt4jspndaVHwuKBoXRkxB0Ipk3qvEJuK9dVv3DurLO5Vu-ZQ88u3GWGzkNaZsnfNRi3fil6vklNreMT6qaOBvFJmSxjTw7zVFu3003__mC0" alt="Diagram">
</p>

#### ⭐️ <i> From [Trần Thị Thanh Kiều](https://github.com/tukieef-nah) - 4451051111 </i> 💙
