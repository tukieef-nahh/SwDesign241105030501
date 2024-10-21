
# 🐳 Bài thực hành Lab1 <img src="https://media.giphy.com/media/fYSnHlufseco8Fh93Z/giphy.gif" width="30">
#### 📖 Mục đích 📝
Phân tích kiến trúc và ca sử dụng hệ thống "Payroll System" trong file tài liệu yêu cầu đính kèm.
</br>📑 Tài liệu yêu cầu
</br>📎 https://drive.google.com/file/d/1CSNZ0j5kiMHLyDXOxk1UHgETDVAHx6eP/view 

## ⭐️ 1. Phân tích kiến trúc 📈


## ⭐️ 2. Cơ chế phân tích 🔬


## ⭐️ 3. Phân tích ca sử dụng Payment 📑
👉 <b> Lớp phân tích cho ca sử dụng Payment: </b>
</br> - <b> PaymentController: </b> Điều khiển quy trình thanh toán.
</br> - <b> PaymentModel: </b> Xử lý logic thanh toán, lưu trữ và tính toán dữ liệu thanh toán.
</br> - <b> BankingService: </b> Dịch vụ kết nối với ngân hàng để thực hiện thanh toán chuyển khoản.
</br> - <b> CashService: </b> Xử lý các khoản thanh toán tiền mặt.

👉 Sử dụng công cụ PlantText để vẽ Sequence diagram:

![Diagram]()

</br> Biểu đồ sequence sẽ mô tả quá trình từ khi người dùng chọn phương thức thanh toán, thông qua PaymentController, gọi đến các dịch vụ BankingService hoặc CashService, và xử lý thanh toán.

👉 </br> <b>Thuộc tính và quan hệ giữa các lớp:</b>
</br> - <b> PaymentModel </b> có thuộc tính như paymentAmount, paymentDate, paymentMethod.
</br> - <b> BankingService </b> có quan hệ với PaymentModel để xử lý thanh toán trực tuyến.

## ⭐️ 4. Phân tích ca sử dụng Maintain Timecard 📇

👉 </br> Lớp phân tích cho ca sử dụng Maintain Timecard:

</br> - <b> TimecardController: </b> Điều khiển quy trình quản lý Timecard.
</br> - <b> TimecardModel: </b> Lưu trữ và xử lý dữ liệu thời gian làm việc.
</br> - <b> EmployeeModel: </b> Thông tin về nhân viên, có quan hệ với TimecardModel.

👉 <b> Sử dụng công cụ PlantText để vẽ Sequence diagram: </b>

![Diagram]()

</br> Biểu đồ sequence sẽ mô tả quá trình từ khi người dùng nhập thông tin Timecard thông qua TimecardController, sau đó lưu dữ liệu vào TimecardModel.

👉 </br> <b> Thuộc tính và quan hệ giữa các lớp: </b>
</br> - <b> TimecardModel </b> có các thuộc tính như workDate, hoursWorked, employeeId.
</br> - <b> EmployeeModel </b> có quan hệ với TimecardModel để ghi nhận thông tin làm việc của nhân viên.

## ⭐️ 5. Hợp nhất kết quả phân tích 📁

Cuối cùng, bạn có thể tiến hành hợp nhất các kết quả phân tích từ hai ca sử dụng Payment và Maintain Timecard vào một tài liệu mô tả chung về kiến trúc và cơ chế hoạt động của hệ thống. Tài liệu sẽ bao gồm các biểu đồ lớp tổng quan về các thành phần của hệ thống, các biểu đồ sequence cho thấy luồng xử lý dữ liệu, và phần mô tả chi tiết từng lớp, thuộc tính, và mối quan hệ.

#### ⭐️ From [Trần Thị Thanh Kiều](https://github.com/tukieef-nah) - 4451051111 💙
