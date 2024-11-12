# 🐳 Bài thực hành Lab1 <img src="https://media.giphy.com/media/fYSnHlufseco8Fh93Z/giphy.gif" width="30">
#### 📖 Mục đích 📝
Phân tích kiến trúc và ca sử dụng hệ thống "Payroll System" trong file tài liệu yêu cầu đính kèm.
</br>📑 Tài liệu yêu cầu
</br>📎 https://drive.google.com/file/d/1CSNZ0j5kiMHLyDXOxk1UHgETDVAHx6eP/view 

## ⭐️ 1. Phân tích kiến trúc 📈

#### 👉 Yêu cầu của bài toán:
Bài toán yêu cầu một hệ thống payroll (chấm công và thanh toán lương) với các chức năng chính như:
- Nhân viên chọn phương thức thanh toán (`Select Payment`).
- Nhân viên cập nhật và duy trì thông tin chấm công (`Maintain Timecard`).
- Bảo mật thông tin lương và chấm công của nhân viên.
- Tương tác với các hệ thống cơ sở dữ liệu hiện có (`Project Management Database`).
- Giao diện hệ thống là ứng dụng desktop.

#### 👉 Kiến trúc phù hợp cho bài toán này là kiến trúc `three-tier architecture` (kiến trúc ba tầng):
- **Presentation Layer (Tầng giao diện):** 
  + Giao diện người dùng cho nhân viên và quản trị viên.
  + Các thành phần liên quan đến việc nhập thông tin chấm công, chọn phương thức thanh toán, thời gian làm việc và thực hiện các tác vụ khác.
- **Business Logic Layer (Tầng xử lý nghiệp vụ):** 
  + Chứa các lớp xử lý logic nghiệp vụ như `PaymentController` (xử lý chọn phương thức thanh toán), `TimecardController` (Chịu trách nhiệm quản lý và cập nhật thông tin timecard và đảm bảo tính chính xác của tổng giờ làm việc, ngăn ngừa việc vượt quá giờ giới hạn cho từng nhân viên).
  + Tầng này giúp duy trì tính nhất quán của các quy tắc nghiệp vụ, làm rõ ràng và tập trung vào xử lý logic mà không ảnh hưởng tới giao diện hoặc tầng dữ liệu.
- **Data Layer (Tầng dữ liệu):** 
  + Kết nối với cơ sở dữ liệu như `Project Management Database` và `Payroll Database` để lưu trữ thông tin chấm công, thanh toán, và nhân viên.
  + Tầng này đóng vai trò là lớp giao tiếp với cơ sở dữ liệu, cung cấp các thao tác lưu trữ và truy xuất dữ liệu cho tầng Business Logic.

#### 👉 Lý do lựa chọn và ý nghĩa của kiến trúc `three-tier architecture`:
- **Tính mở rộng:**  Kiến trúc ba tầng dễ dàng mở rộng và phát triển thêm tính năng hoặc tích hợp với các hệ thống khác.
- **Bảo trì dễ dàng:**  Các thay đổi trong một tầng không ảnh hưởng trực tiếp đến tầng khác, giúp bảo trì dễ dàng hơn.
- **Tăng cường bảo mật:**  Tầng Business Logic có thể đảm nhận vai trò kiểm tra bảo mật và xác thực người dùng.
- **Độ tin cậy và hiệu quả:**  Kiến trúc ba tầng giúp xử lý các tác vụ nghiệp vụ phức tạp mà không ảnh hưởng đến tầng giao diện người dùng hay tầng dữ liệu.

#### 👉 Package diagram mô tả kiến trúc:
<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/f5PTRXen47xVKrXveX9m05H5AI5L8eK8DPNwK5MHiIVWuhMt_g555IVhGu_KAzJBxeBNEvkY50cqUBxnp3V-Phn_Vls-ieuQvtEPPNOZ537QGfOLb6te2iZ5me05vQWJMZtTqnsO2_8p8-739BMMBEWk3_QfzefJitklJLxRgu-1Rnwigs5pS6lD1sycPAi5Zs1Ss4BItQDd3AoTXs-8te-xCKQR1WNbdmbvT4QeLTUbpc1EXNp7UQ1ZaNrhq9IgpGnSWBP1-ooY_57amAZX_-BSuExKi-wdqg06pGDnzSDvx2lQv524_wxh1w1SAtbcKlji7obbwgrG8S3JlLu9ze9MhhLoHai9fbKr2n9O8XJ8YxjP_z7wWbC7BxWCINvOFVsdbGHE2yjmv0yqXmZ2M3XPz-3p9Q2wGjNGmyf0S8Sj72kQKceC7Lgunv2mDJKhQ6St96ljJM0rfyNRMN0U4g7SPRTYrYzpuNgJIT1RAaMPocsvUPg7quxAsofi21QybrfBe0hHHaY9OeguoGkfTm1HoKQa5ITQznQCYaugCXLXi-_QSDGKgGEn9uA8BAaoOYTC8f6TUMD2qARE22AdFqwrYqekG_EeGKfrs67OFQmLTATi4hPiiWJKxWz4CD2Qd4crK7myH5_HNKSsr-qYedmOLP-qsSorgKMwxXSaqhGjtJKZ3XLVdoWFjsVPSHDI_iOUYgFhXmpBf85__f9sRAoXgCzjYSHYEuyfj-fo1sa2hHeiZFuQ1cwh14MrXZAjRJqTWKsbqo3elaMCiHU7qUYIODV8k7DpO3kYztBlbjsvdMNdnJxiUPfeusQ8uUx8_P3u7s-0L_hN1vbbLq5ovOlSNm000F__0m00" alt="Diagram">
</p>

## ⭐️ 2. Cơ chế phân tích 🔬

#### 👉 Cơ chế cần giải quyết trong bài toán:
- **Cơ chế xác thực (Authentication):** 
  + Đảm bảo chỉ có nhân viên đăng nhập đúng thông tin mới có thể truy cập vào Payroll System.
  + **Lý do:**  Bảo vệ hệ thống tránh truy cập trái phép và đảm bảo bảo mật thông tin của nhân viên.

- **Cơ chế phân quyền (Authorization):** 
  + Xác định quyền hạn của các đối tượng trong hệ thống, như `Payroll Administrator` có quyền quản lý thông tin nhân viên và xử lý chấm công, nhân viên thông thường chỉ có quyền nhập và xem thông tin cá nhân và timecard của mình.
  + **Lý do:**  Đảm bảo rằng mỗi người dùng chỉ có thể truy cập và thao tác trong phạm vi quyền hạn của mình, tránh xung đột quyền và bảo mật thông tin.

- **Cơ chế tính toán lương (Payroll Calculation):** 
  + Tính toán lương cho nhân viên dựa trên loại nhân viên (lương theo giờ, lương theo tháng, lương tăng ca hoặc lương kèm hoa hồng).
  + **Lý do:**  Đảm bảo rằng lương của nhân viên được tính toán chính xác và kịp thời, dựa trên thông tin `timecard` và các thông tin liên quan khác.

- **Cơ chế lưu trữ (Persistence):** 
  + Đảm bảo thông tin về `timecard`, thông tin nhân viên và phương thức thanh toán được lưu trữ chính xác trong cơ sở dữ liệu.
  + **Lý do:**  Đảm bảo thông tin chấm công và thanh toán của nhân viên được bảo quản an toàn, có thể truy xuất và chỉnh sửa khi cần thiết.

- **Cơ chế thông báo lỗi và bảo mật (Error Handling and Security):** 
  + Xử lý các lỗi phát sinh trong quá trình tính toán, nhập liệu, hoặc truy xuất dữ liệu và bảo mật dữ liệu nhạy cảm như thông tin tài khoản ngân hàng.
  + **Lý do:**  Bảo vệ dữ liệu nhạy cảm và giúp người dùng có trải nghiệm mượt mà bằng cách hiển thị thông báo lỗi khi có sự cố.
 
- **Cơ chế giao tiếp với cơ sở dữ liệu khác (Integration with External Databases):** 
  + Hệ thống cần tích hợp với các cơ sở dữ liệu khác, như `Project Management Database`, để lấy thông tin về mã  `charge number`, hoặc các dữ liệu liên quan đến dự án mà nhân viên đang làm việc.
  + **Lý do:**  Đảm bảo rằng thông tin chấm công và dự án của nhân viên được đồng bộ và chính xác.
 
- **Cơ chế backup và phục hồi dữ liệu (Backup and Recovery):** 
  + Cơ chế này đảm bảo rằng dữ liệu payroll của hệ thống được sao lưu định kỳ và có thể phục hồi khi xảy ra sự cố hoặc mất dữ liệu.
  + **Lý do:**  Đảm bảo an toàn cho dữ liệu quan trọng và tránh mất mát thông tin trong trường hợp hệ thống gặp sự cố.


## ⭐️ 3. Phân tích ca sử dụng Select Payment 📑

#### 👉 Các lớp phân tích cho ca sử dụng Select Payment: 
- **Entity classes:** 
  + **Employee:**  Người dùng chọn phương thức thanh toán, bao gồm các thuộc tính như: `employeeID`, `name`, `PaymentMethod`, `address`, `bankName`, `accountNumber`.

- **Boundary classes:** 
  + **PaymentBoundaryForm:**  Lớp này chịu trách nhiệm tương tác với người dùng để thu thập thông tin liên quan đến phương thức thanh toán và hiển thị các yêu cầu hoặc lỗi.

- **Control classes:** 
  + **PaymentController:**  Lớp này điều phối luồng sự kiện giữa người dùng và hệ thống, xử lý logic nghiệp vụ để cập nhật phương thức thanh toán của nhân viên.

👉 **Sequence diagram cho ca sử dụng Select Payment:** 

<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/b9H1Rjim44NtFCL0gnX834HAsqIB8asT00LgDq1EG9CJXx14gYHLG6VheaVg5JgKB9bohCGrODaavl-P_oJgx-y_jyvpw-koOCnjbGPh73B6XJSMxikgC0qYS0TOLcnjQYsvRU2HDoLglqJ_OkJTRlV1s39KzbLC6EsjASRLNxlD0cse5SEAKONopRXdkyKOzOQBpuCnv72PmtUpsQ04fRq1_uBW6kUnF5ARvl2ZGWt94nOeV3yETFCa-rGasyz3mYm7rqf60SwemxV5Z4Mb9DnDdyDL3izAopv6NyruuVVP7a9B1lGPkqHJVvXJHei_QtG7_MUjy7NEZq5HMVDBIJoccCpvAGWTQZbMLV6gisWl8KdogCJsegwITkTra077TV2kAydzmKo3movEuH2I9LV5b6MKz7gUHdI2w8kK5ftR9JtE9wZIWT1nrIIZ8CuwIh6ITx-pzp6aywi946teSnXPTJWMoeO7Te6LSSgV12QBmDnnlLsW9_ltm6GHc5YrflyhNY9D9mG9_AekrsXFufNrlFxBS99VDidlWD8vlDc41c9ldxoR7AHoLS6Rfre8kYLB-l8D4iFsjWodU6NyQISv7HplhJMszqi69qrEpq51fo4CU4kNy4h-1m00__y30000" alt="Diagram">
</p>

👉 **Nhiệm vụ và các thuộc tính của các lớp phân tích:** 
- **Employee (Entity):**  Lưu trữ và cung cấp thông tin của nhân viên như tên, phương thức thanh toán, địa chỉ và chi tiết ngân hàng.
  + Các thuộc tính:
    - `empID`: ID của nhân viên.
    - `name`: Tên nhân viên.
    - `paymentMethod`: Phương thức thanh toán hiện tại của nhân viên (`Pick up`, `Mail`, `Direct deposit`).
    - `address`: Địa chỉ (nếu chọn `Mail`).
    - `bankName`: Tên ngân hàng (nếu chọn `Direct Deposit`).
    - `accountNumber`: Số tài khoản ngân hàng.
    - `username`: username của tài khoản nhân viên.
    - `password`: password của tài khoản nhân viên.
  + Các phương thức:
    - `getPaymentMethod()`: Trả về phương thức thanh toán hiện tại của nhân viên.
    - `setPaymentMethod(method)`: Đặt phương thức thanh toán cho nhân viên, tham số method là loại thanh toán được chọn.
    - `setMailAddress(address)`: Đặt địa chỉ nhận phiếu lương khi nhân viên chọn phương thức thanh toán là `Mail`.
    - `setBankDetails(bankName, accountNumber)`: Đặt tên ngân hàng và số tài khoản khi nhân viên chọn phương thức thanh toán là `Direct deposit`.

- **PaymentBoundaryForm (Boundary):**  Tương tác với người dùng, lấy thông tin đầu vào về phương thức thanh toán và hiển thị yêu cầu hoặc lỗi.
  + Các phương thức:
    - `requestPaymentMethod()`: Yêu cầu nhân viên chọn phương thức thanh toán mong muốn.
    - `displaySuccessMessage()`: Hiển thị thông báo thành công khi phương thức thanh toán được cập nhật.
    - `displayErrorMessage(error)`: Hiển thị thông báo lỗi với nội dung lỗi được truyền vào qua tham số error.
    - `requestMailAddress()`: Yêu cầu nhân viên nhập địa chỉ gửi phiếu lương khi chọn phương thức thanh toán `Mail`.
    - `requestBankDetails()`: Yêu cầu nhân viên cung cấp thông tin ngân hàng và số tài khoản khi chọn phương thức thanh toán `Direct deposit`.

- **PaymentController (Control):**  Điều phối giữa `PaymentBoudaryForm` và `Employee`, thực hiện cập nhật phương thức thanh toán và xử lý logic chính.
  + Các phương thức:
    - `selectPaymentMethod(empID)`: Bắt đầu quá trình lựa chọn phương thức thanh toán cho nhân viên có mã empID.
    - `updatePaymentMethod(empID, method, address, bankName, accountNumber)`:Cập nhật thông tin phương thức thanh toán cho nhân viên. Phương thức này xử lý các trường hợp khác nhau dựa trên method được chọn (có thể là `Pick up`, `Mail`, hoặc `Direct deposit`), với các tham số address, bankName, và accountNumber sẽ được sử dụng nếu cần thiết.

👉 **Xác định quan hệ giữa các lớp phân tích:** 
- `PaymentBoundaryForm` tương tác với `PaymentController` để gửi và nhận dữ liệu, trong khi `PaymentController` sẽ tương tác với `Employee` để tìm, truy xuất và cập nhật thông tin cần thiết.

👉 **Class diagram mô tả các lớp phân tích và giải thích:** 

<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/X9DDJiCm48NtFiMegnIbbRejcr9Q91Qja7e2Dnw5gFu9OniK8Kx6WYDn1LoHbCGE42bIF7upVbzc_Fd-iRAEa_DACcPFbGOo5Xah9BSMjggMfa64LmRXcG6g-dwpX8EZIfTjp5iapHL6uJeKU34aad2ZKBiTkaSJxt4X2AsDeaUkJ_kqFYyAuxNRUtL46km1I5DMEekDvOcdwHAUJIMksxGItKFVNZQDwjfOe0OORRaVyOvNykORAelW4kqwO6xGXGoRnSZvE6rNuwthLsjk7QI2KtDdIBMj0o1yycXJm9uBKTbQykRWYo8utOMNbpYksH8PwXHuNeo3jQVsVyIee4__6zQjqOwCb4WNA8iIYuXfCAF3mtmjkCC_v3aCEvh7Cvadu_X_RowtQBAOpwycC9jrNmaOIr7FqiKbQJ4PQp9ReHRdA_m5003__mC0" alt="Diagram">
</p>

- **Giải thích:** 
  + <i> PaymentBoundaryForm: </i> Lớp boundary chịu trách nhiệm giao tiếp với nhân viên, thu thập dữ liệu đầu vào và hiển thị các thông báo lỗi hoặc yêu cầu. Lớp này không thực hiện bất kỳ logic nào liên quan đến nghiệp vụ.

  + <i> PaymentController: </i> Đây là lớp điều khiển, đóng vai trò điều phối toàn bộ luồng sự kiện giữa `PaymentBoundaryForm` và `Employee`. Nó kiểm soát luồng xử lý từ việc yêu cầu phương thức thanh toán cho đến khi cập nhật thông tin vào cơ sở dữ liệu.

  + <i> Employee: </i> Lớp thực thể quản lý thông tin của nhân viên, bao gồm các thuộc tính và phương thức để truy xuất và cập nhật thông tin.
  
## ⭐️ 4. Phân tích ca sử dụng Maintain Timecard 📇

#### 👉 Các lớp phân tích cho ca sử dụng Maintain Timecard:
- **Entity classes:** 
  + **Timecard:**  Lớp chứa thông tin về timecard của nhân viên, như số giờ làm việc, ngày làm việc, và trạng thái của timecard.
  + **Employee:**  Lớp thông tin của nhân viên. Nhân viên có thể truy cập và chỉnh sửa timecard của mình.
  + **Project:**  Lớp chứa thông tin về các dự án mà nhân viên có thể phân bổ số giờ làm việc.

- **Boundary classes:** 
  + **TimecardBoundaryForm:**  Giao diện tương tác với người dùng, cho phép nhân viên nhập giờ làm việc và gửi timecard.

- **Control classes:** 
  + **TimecardController:**  Điều phối các luồng sự kiện như tạo, cập nhật và gửi timecard. Lớp này cũng chịu trách nhiệm kiểm tra các ràng buộc về giờ làm việc.

👉 **Sequence diagram cho ca sử dụng Maintain Timecard:** 

<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/h9HBJiCm48RtFeN5AaXbmMFL1QeeHNH15y05t7ZQMZXscB4BEHiBZiGLS9BcqIY5L10f3p_cc_7_E_xw-9oG4-XyeXcZ5sKuMWB6HEmiybcIQfi1C31EkQnfBwqtKc36drK2iK1vi-kuivYms1g7LjU3qxAj0IjGDS9OXUHdrxqmFkRdOxu6D_M88RgQ4vsotkajJ9CsG2x67E7L0zM4kLdP299qVjkWMY4jK0Y_pCCTAjX2NK4dzc3ggoBMew7m9gyTCQ5TGuTtHQ6FX-ldEZgwI4Mf5bct7j043LnQ86wiAxCCI1B0CO9mi82tBlhVIZJ3d0z-0zvRZnJ56u5hMFXa2JZYcxplo1tWKnbMjL_AYFTo2t-sGYjPzWoJZKHhS-oBrIsmNdijqPEFOo1w2BTOGxIpKPb3LVnEd25Qh7YGDuOBJtwPg6QB7YTq6TprlD3KLMgLSnpaNyN2LrxhR9ZEfP4yd5lEKpqGdTJCasF5VmGXhT7zlrA19LBMy9LG6kHVV6XWiyQHINZa1_0t0000__y30000" alt="Diagram">
</p>

👉 **Nhiệm vụ và các thuộc tính của các lớp phân tích:** 
- **Employee (Entity):**  Lớp này chứa thông tin về nhân viên và kết nối với timecard. Nhân viên có thể cập nhật giờ làm việc của mình.
  + Các thuộc tính:
    - `empID`: ID của nhân viên.
    - `name`: Tên nhân viên.
    - `currentTimecard`: Tham chiếu đến timecard hiện tại của nhân viên.
    - `maxHours`: Giới hạn giờ làm việc của nhân viên.
    - `username`: username của tài khoản nhân viên.
    - `password`: password của tài khoản nhân viên.
  + Các phương thức:
    - `getCurrentTimecard()`: Lấy thông tin timecard hiện tại.
    - `canWorkMoreHours(hours)`: Kiểm tra xem nhân viên có thể làm thêm số giờ hours.

- **Timecard (Entity):**  Lưu trữ dữ liệu về giờ làm việc trong tuần, dự án mà giờ làm việc được tính vào và trạng thái của timecard.
  + Các thuộc tính:
    - `timecardID`: ID của timecard.
    - `empID`: ID của nhân viên.
    - `startDate`: Ngày bắt đầu kỳ chấm công.
    - `endDate`: Ngày kết thúc kỳ chấm công.
    - `hoursWorked[]`: Mảng chứa số giờ làm việc của mỗi ngày.
    - `chargeNumbers[]`: Dự án tương ứng với số giờ làm việc.
    - `status`: Trạng thái timecard (draft, submitted).
    - `submittedDate`: Ngày gửi timecard.

- **Project (Entity):**  Lớp chứa thông tin về các dự án mà giờ làm việc có thể được tính vào.
  + Các thuộc tính:
    - `projectID`: ID của dự án.
    - `projectName`: Tên dự án.
    - `chargeNumber`: Số để tính chi phí cho dự án.
 
- **TimecardBoundaryForm (Boundary):**  Giao diện tương tác với nhân viên để nhập và gửi timecard.
  + Các phương thức:
    - `requestTimecardInfo(empID)`: Yêu cầu nhân viên nhập giờ làm việc cho từng ngày.
    - `displayTimecard(empID)`: Hiển thị thông tin timecard hiện tại.
    - `displaySuccessMessage()`: Hiển thị thông báo thành công khi cập nhật timecard.
    - `displayErrorMessage(error)`: Hiển thị thông báo lỗi khi có sai sót trong timecard.
    - `displayReadonlyTimecard(empID)`:Hiển thị phiếu chấm công ở chế độ chỉ đọc nếu timecard đã được gửi.

- **TimecardController (Control):**  Điều khiển luồng sự kiện, xác minh tính hợp lệ của timecard, xử lý việc lưu và gửi.
  + Các phương thức:
    - `retrieveTimecard(empID)`: Lấy timecard hiện tại cho nhân viên theo mã empID.
    - `updateTimecard(empID, chargeNumber, hours)`: Cập nhật số giờ làm việc cho project và ngày tương ứng.
    - `submitTimecard(empID)`: Gửi timecard và chuyển trạng thái của timecard thành “submitted” và kiểm tra tính hợp lệ về số giờ làm việc.
    - `validateHours(empID, totalHours)`: Kiểm tra tổng số giờ làm việc, đảm bảo không vượt quá giới hạn của nhân viên.
      
👉 **Xác định quan hệ giữa các lớp phân tích:** 
- `TimecardBoundary` tương tác với `TimecardController` để gửi và nhận thông tin từ người dùng.
- `TimecardController` kết nối với cả `Timecard` và `Project` để lấy và cập nhật thông tin thời gian làm việc cũng như các dự án tương ứng.

👉 **Class diagram mô tả các lớp phân tích và giải thích:** 

<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/Z5HDJ-Cm4BtxLrWz5THMuXgj45e-18SY14XxG7iOag4D-2ECRTXgjRzi3_ma_W9EufWuYH0zLF7CyxnvRoPv__zsP2oGTL8mPfvAnKaRP2mNO0m_bPNGEqJ-bt7_MwAiBauoVcEfL9isf41Y6iaT4IfxMqhCWOeqAU7FkNPaCbugsuQSGHfNgJp_gnvSvnkqnsdv-LwRoK7zqlIqreGDmNmRQVROlqvGTwiJPCDvg6f2Q6FJ2LZVP_qVSAeOXXhUkXKixdvdV0tLZpgvg3iv30vjWJPuwUGzagb10nxhp23cxcLfBVR9egOhqe-OsqvIrHw7xOVmvNXSlMPYPcJOJ-rK0RGxqoG34oTyTcZY92xKW-wcKPIc4h2BGug-TuQdk5CYJMiq1ZOuRrlWMCTIs8tBSm_gW6do6g7GIdp9EP9rh9KbBGJIfoXFZoyOooIh42XTLVWHJ4CMVChH1G_xcEv3gDVEzqlA5n1bJTekzu3HQWlYF5tu-ExE3bQhWnbVBfkd_LaKpw938qZOAJOv_e1UhGwxnyZLq2D1RWr_BUsMJHWTA7hNOnyPbw3yQCstY7jIUkKpRlnRQRWt2xmnZ1tvO_rv-m000F__0m00" alt="Diagram">
</p>

- **Giải thích:** 
  + <i> TimecardBoundaryForm: </i> Lớp biên nhận đầu vào từ nhân viên, cho phép họ nhập số giờ làm việc và gửi timecard. Lớp này cũng xử lý việc hiển thị các thông báo lỗi nếu có.

  + <i> TimecardController: </i> Lớp điều khiển quản lý luồng xử lý của timecard, bao gồm việc lấy dữ liệu từ timecard hiện tại, lưu thay đổi và kiểm tra tính hợp lệ của dữ liệu trước khi gửi.

  + <i> Timecard: </i> Lớp thực thể chứa thông tin về timecard, bao gồm số giờ làm việc, các dự án và trạng thái của timecard.

  + <i> Project: </i> Lớp thực thể lưu trữ thông tin về dự án và mã số mà thời gian làm việc của nhân viên sẽ được tính vào.

## ⭐️ 5. Hợp nhất kết quả phân tích 📁

👉 **Hợp nhất các lớp phân tích:** 
- **Lớp chung:** 
  + `Employee:` Lớp nhân viên cần thiết trong cả hai ca sử dụng để lưu trữ thông tin về phương thức thanh toán cũng như timecard.
- **Điểm hợp nhất:** 
  + Sau hợp nhất, lớp Employee không chỉ lưu trữ thông tin về phương thức thanh toán mà còn quản lý thông tin liên quan đến timecard.
  + Hợp nhất thông tin giúp tránh việc trùng lặp thông tin và giảm thiểu các quy trình phức tạp. Nhân viên có thể dễ dàng truy cập thông tin về thời gian làm việc và phương thức thanh toán mà không cần phải tương tác với nhiều lớp khác nhau.
  + Có thể kết hợp giao diện người dùng trong một module như EmployeeBoundaryForm, cung cấp cả chức năng chọn phương thức thanh toán và cập nhật timecard.


- **Employee:**  Lớp này lưu trữ thông tin của nhân viên, bao gồm thông tin đăng nhập, thông tin thanh toán và timecard hiện tại.
- **Timecard:**  Lớp này lưu trữ thông tin chi tiết về timecard của nhân viên, bao gồm ID, thời gian làm việc và trạng thái.
- **PaymentController:**  Lớp này quản lý các thao tác liên quan đến việc cập nhật thông tin thanh toán của nhân viên.
- **TimecardController:**  Lớp này điều khiển các thao tác liên quan đến việc cập nhật và gửi timecard.
- **PaymentBoundaryForm:**  Lớp này chỉ phục vụ cho việc tương tác với các chức năng thanh toán.
- **TimecardBoundaryForm:**  Chỉ tập trung vào việc nhập và quản lý timecard.
- **Project:**  Chứa thông tin về các dự án mà nhân viên làm việc.

<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/d5RDZjCm4BxdAQoUkYYjr6k4Lijk5-qUka8i4WV4mOs7DDInmzZkKY6UZ0EFn2lWf8bnRE-FgDGg7d_sp3VppQH_Vls-K9gYDWtFChMl1K6f8CjAJfKYrqtBvH60_CY8_Im8DEtjkY3t6cjH3JQZ00Lj832tze87YImo7niGUWDw9yCzoXY2Ke5rIyN-BhwVbgKqGj-PPWiOx9K6qJhvK3TGqYY4Xdw_aGQjdrhetaO8brKjvY6LF69nLf23hDbmgWBzpkSpFvku8aI5W6R2UtgR1MzepT-SiZ0FiX5XBsrUrg3j2JKFSvIdqnD5VpLDL1H_ISL7YVkDHEXJDj-vn5deLaeEL6G_HxqCN2-jPqRn-5PYCqY748Hl1bISBoyWLgkMq-EzAKjBV6E_j88qvXfHueY0Rf7cE7Zryve4-CaS0I6jAoaqIiu17Ia57Cg0qwH7fivCowY69-0vcGea3tiYZzhXcL8x4cEDNI_hmH0rTAh9-o6nji4NfFiTaO95jbuXdMY0VVfSa0rjNtUxUQUPyx4_TnGhE0MiEbJeIvjm2YYpRMgjmNVuhq0elzewE6hjQHsn6Eo9QU97vBQYt3qbx15pAxx8j6PTbxbIZ2LuNkAdY4YlzFzkclT0cHJy1O54p1FQHx0nmG7SRQ7mnus9-DFeF5c0d0pZPYgYO1BsmdWq20zveBpkGZXDii2_bfhocqUcctiFpbRBvQiPMIp6fsWqPF6mwA0hTsWrIut9mCVAz-7owCeLGOO6o9927T3BvVduw7prN05fgHLvgFKkIzHxSE4TTt4KzbqghDpKYnnxLBph2pj41LF4LeRQAcJPXLrsVqV-0W00__y30000" alt="Diagram">
</p>

#### ⭐️ <i> From [Trần Thị Thanh Kiều](https://github.com/tukieef-nah) - 4451051111 </i> 💙
