# 🐳 Bài thực hành Lab5 - Subsystem Design <img src="https://media.giphy.com/media/fYSnHlufseco8Fh93Z/giphy.gif" width="30">
#### 📖 Mục đích 📝
👉 Thiết kế các hệ thống con trong hệ thống Payroll System, dựa vào kết quả tham khảo về thiết kế ca sử dụng ở bài Lab4.

</br>📑 File đính kèm
</br>📎 https://drive.google.com/file/u/0/d/1OwzLi1iYoWp0GAnArMh0Oz-rMmIj8KS9/view?usp=classroom_web
## ⭐️ 1. Distribute subsystem behavior to subsystem elements: Phân phối hành vi subsystem cho các phần tử
#### 👉 Xác định các hành vi chính của từng subsystem và phân phối chúng cho các phần tử tương ứng:
| Subsystem	         | Hành vi	                                                                 | Phần tử                     |
|--------------------|---------------------------------------------------------------------------|-----------------------------|
|Payroll Calculation |- Tính toán lương theo loại nhân viên (Hourly, Salaried, Commissioned).    | PayrollController, Employee |
|                    |- Tạo đối tượng Paycheck với chi tiết lương.	                             | Paycheck                    |
|Timecard Subsystem	 |- Thu thập và lưu trữ thông tin giờ làm việc của nhân viên.	               | TimecardController, Timecard|
|                    |- Liên kết Timecard với charge codes và dự án.                             | ProjectManagementDatabase   |
|Payment Subsystem   |- Xử lý thanh toán qua ngân hàng (Direct Deposit).	                       | BankSystem                  |
|                    |- In paycheck cho nhân viên được trả qua séc (Check).	                     | PrinterInterface            |
| System Management  |- Theo dõi thời gian và kích hoạt quy trình Run Payroll vào ngày trả lương.| SystemClockInterface        |

## ⭐️ 2. Document subsystem elements 
| Phần tử                 	| Thuộc subsystem	    | Mô tả chi tiết                                                                      |
|---------------------------|---------------------|-------------------------------------------------------------------------------------|
| PayrollController       	| Payroll Calculation |	Điều phối toàn bộ quy trình tính lương, tương tác với Employee và Paycheck.         |
| Paycheck                  |	Payroll Calculation |	Lưu trữ chi tiết tiền lương của nhân viên, bao gồm số tiền và trạng thái thanh toán.|
| TimecardController	      |Timecard Subsystem   |	Quản lý việc thu thập và xác minh thông tin Timecard.                               |
| Timecard                  |	Timecard Subsystem  | Lưu số giờ làm việc và liên kết với charge codes hoặc dự án cụ thể.                 |
| ProjectManagementDatabase	|Timecard Subsystem 	| Lưu charge codes và thông tin dự án liên quan.                                      |
| BankSystem	              | Payment Subsystem	  | Xử lý các giao dịch Direct Deposit cho nhân viên.                                   |
| PrinterInterface          | Payment Subsystem	  | In paycheck cho nhân viên được trả qua séc.                                         |
| SystemClockInterface      | System Management 	| Theo dõi thời gian và kích hoạt các sự kiện liên quan đến Payroll.                  |

#### 👉 Mỗi subsystem sẽ được mô tả như sau:
|Subsystem	          | Chức năng                                                                 | Lớp/Thành phần                        |
|---------------------|---------------------------------------------------------------------------|---------------------------------------|
| Payroll Calculation | Tính toán lương dựa trên loại nhân viên, tạo paycheck	                    | PayrollController, Employee, Paycheck |
| Timecard	          | Thu thập và quản lý dữ liệu giờ làm việc, liên kết với charge codes dự án	| TimecardController, Timecard          |
| Payment	            | Xử lý thanh toán (gửi tiền trực tiếp hoặc in paycheck)	                  | BankSystem, PrinterInterface          |
| System Management 	| Quản lý các sự kiện dựa trên thời gian (như payday)	                      | SystemClockInterface                  |

## ⭐️ 3. Describe subsystem dependencies: Mô tả sự phụ thuộc giữa các subsystem
#### Timecard Subsystem → Payroll Calculation Subsystem:
- `TimecardController` cung cấp thông tin giờ làm cho `PayrollController`.
- `Payroll Calculation` phụ thuộc vào `Timecard Subsystem` để lấy dữ liệu giờ làm việc.

#### Payroll Calculation Subsystem → Payment Subsystem:
- `PayrollController` chuyển thông tin lương cho `BankSystem` hoặc `PrinterInterface` để xử lý thanh toán.

#### System Management Subsystem → Payroll Calculation Subsystem:
- `SystemClockInterface` kích hoạt `PayrollController` vào thời gian được chỉ định (ngày trả lương).

## ⭐️ 4. Checkpoints
#### 👉 Consistency:
Kiểm tra sự nhất quán giữa các lớp và subsystem. Đảm bảo mỗi subsystem có trách nhiệm rõ ràng và không trùng lặp.

#### 👉 Modularity:
Đảm bảo rằng các subsystem được thiết kế độc lập, dễ mở rộng và bảo trì.

#### 👉 Dependency Management:
Kiểm tra các phụ thuộc giữa subsystem. Các phụ thuộc nên được giảm thiểu và sử dụng giao diện hoặc API để giao tiếp.

## ⭐️ 5. Class Diagram
#### 👉 Biểu đồ này mô tả các lớp chính và mối quan hệ của chúng trong các subsystem.
<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/b5JDQjmm4BxhANJSGlm29eIGJQ615fPkISyJQPeLbZIBHYwODa_MGn-fhr3BAtlNibFIYss-qVUZqSX_Vls-vGWXjiuAReoNWHY5K1QOvNjtjDGXoXz2oaeQNKlZu_3jmM4jzp4O_pm0H-WS-lW9uu7qHKLA1LQr5YBkeDkygwMczicYU1bTFb0RR5Tu7GRmSy-Q22FCNoaqg2_mVtYSBFPW8HZKXGadkFiVeIqvPvWD-OMOcagBr94Ys3u3yjkyibaF1x9sIpwcDuR1QSvBXSJzJaQVcL-CGmL1vsXw27JVFyzDd2Kn_0ZMw2JqH6GH_59h4GEq7ciRpBruE8t8bOovKa_yCMIYFcCSOIwv_RgFXkFrkE1crX1rGDNaRHN40GD7hO-pxkV9l3ytOHAy0z_iEuxeyfwEWHGoxqwKpJ4RrfFrejMxViuZXeVq-0OA9w4U7ablqJd5s5fIJQd5FKEtTksufncy_bbLnKqgYkKTACfhatsXNrKtAvCWbYEQ5axyzVBO0x4oMfS-hz3FX_QQVd4aOhMtEScSBsxHw_Gl_0i00F__0m00" alt="Diagram">

## ⭐️ 6. Sequence Diagram (Maintain Timecard Use Case)
#### 👉 Biểu đồ này minh họa luồng sự kiện khi quản lý thẻ chấm công.
<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/X95DZi8m38NtFeNLLP6O2tGnGa8isB4O3c0rHbYaSUMa8CusYpdIN866VzGoiydY-RtdBydlzyyi9hBKDHxYJWAQHWQWEgdXEh8XHImMJUlro5n0stkbbfP2mYzfk2PpSmt9r7ksqV6BkA9ZjZv5uBpbutEaha9oxYQNV8LOkYccgpY1OUgvgy8zUN6Kk9m0-GSKIhoC04SMvue1QOLTcvl-0S9XyjtjQWqRiOQIQEZvs4T-0PJmDs9-kGhZLWyBCxMoM5u2TtlHbmO7i_x87tm2003__mC0" alt="Diagram">

## ⭐️ 7. Sequence Diagram (Run Payroll Use Case)
#### 👉 Biểu đồ này minh họa luồng sự kiện khi tính lương.
<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/T58xRiCm3Drr2YAJ3QGNy52aBJfa252WkG0XCObXVGo97dos33rIhr3AdxQEaqK6oFVqFjRtzMkN62DtpghKr1vYIAGKQWuHNeoJ2IROV60VWxLmG8zdYXlL2gVMTOkUOLg-1S_vIt6nVNUj3JtHBKLVI3UBuIlwvhDFJ6w9ZRLdYljyd52Bkz7Nq_DQkGADLdSMcQPTKQeLAbDdMql68_Jiju8pUOeZU9WKD5sqDrj05phFMp02A1NQ8QWZ2N4WlWG3THfImZ6YJoTf2jOPijvV5HMqCMXAQRgfQ2VXKf5DT4TWTZOMzqZXjjMi8vFVMFzalBbVol0RX3Vlf0XYCjBXJZZvHVq0003__mC0" alt="Diagram">

## ⭐️ 8. Component Diagram
#### 👉 Biểu đồ này thể hiện các subsystem và sự phụ thuộc giữa chúng.
<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/T98z3i8m38NtdC9YxnKGec9WG4A23NKmgO4gVoX9XmfnCWQEn1KWf5KfJQSepyyl_goy7i-5ysXzhIHpej9WZIF6hiW5dWbckyPvKh11_Ragqdu6DmPmY7ek3HThxScUa5F1xZ-TMsoiaH9obBoMw2kZszwsaXljmqcs2EfANQLfY8hMmY_4nJ1oNodYQ4lOrKVt7Q1Dx0f_aPqy6Yo0Z4AMg4N4YYFOAe0DwTBSa6Np95P2YzuUTjBIhs3IyZlnTCw8etyzEbBRIub3Ty4MfClmRzu0003__mC0" alt="Diagram">

#### ⭐️ <i> From [Trần Thị Thanh Kiều](https://github.com/tukieef-nah) - 4451051111 </i> 💙
