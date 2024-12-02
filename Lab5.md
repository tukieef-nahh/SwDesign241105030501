# 🐳 Bài thực hành Lab5 - Subsystem Design <img src="https://media.giphy.com/media/fYSnHlufseco8Fh93Z/giphy.gif" width="30">
#### 📖 Mục đích 📝
Thiết kế các hệ thống con trong hệ thống Payroll System, dựa vào kết quả tham khảo về thiết kế ca sử dụng ở bài Lab4.
</br>📑 File đính kèm
</br>📎 https://drive.google.com/file/u/0/d/1OwzLi1iYoWp0GAnArMh0Oz-rMmIj8KS9/view?usp=classroom_web
## ⭐️ 1. Distribute subsystem behavior to subsystem elements: Phân phối hành vi subsystem cho các phần tử
#### Xác định các hành vi chính của từng subsystem và phân phối chúng cho các phần tử tương ứng:
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

#### Mỗi subsystem sẽ được mô tả như sau:
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
#### Consistency:
Kiểm tra sự nhất quán giữa các lớp và subsystem. Đảm bảo mỗi subsystem có trách nhiệm rõ ràng và không trùng lặp.

#### Modularity:
Đảm bảo rằng các subsystem được thiết kế độc lập, dễ mở rộng và bảo trì.

#### Dependency Management:
Kiểm tra các phụ thuộc giữa subsystem. Các phụ thuộc nên được giảm thiểu và sử dụng giao diện hoặc API để giao tiếp.

#### ⭐️ <i> From [Trần Thị Thanh Kiều](https://github.com/tukieef-nah) - 4451051111 </i> 💙
