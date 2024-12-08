# 🐳 Bài thực hành Lab6 - Class Design <img src="https://media.giphy.com/media/fYSnHlufseco8Fh93Z/giphy.gif" width="30">
#### 📖 Mục đích 📝
👉  Thiết kế các lớp dựa vào kết quả thiết kế ca sử dụng ở bài lab trước, kết quả thiết kế hệ thống con được cho trong file đính kèm.
</br>📑 File đính kèm
</br>📎 https://docs.google.com/document/d/14UdARihLFYB7hsMGky43VaBVaskw5M7Hn_ay2QA2y6o/edit?tab=t.0
</br>📎 https://drive.google.com/file/d/1f_GnpyWZnbItHN08uC75PHpkiMFoYMtP/view

## ⭐️ 1. Create Initial Design Classes:
#### 👉 Xác định các lớp
- **Payroll Calculation Subsystem:**
  - Lớp chính: `PayrollController`, `Employee`, `Paycheck`.
- **Timecard Subsystem:**
  - Lớp chính: `TimecardController`, `Timecard`, `ProjectManagementDatabase`.
- **Payment Subsystem:**
  - Lớp chính: `BankSystem`, `PrinterInterface`.
- **System Management Subsystem:**
  - Lớp chính: `SystemClockInterface`.

## ⭐️ 2. Define Operations:
#### 👉 Danh sách các phương thức chính:
- **Payroll Calculation Subsystem:**
  - **`PayrollController`:**
      - `calculatePay(employee: Employee): Paycheck`
      - `distributePaychecks()`
  - **`Employee`:**
    - `getHourlyRate(): float`
    - `getSalariedAmount(): float`
  - **`Paycheck`:**
    - `markPaid()`
- **Timecard Subsystem:**
  - **`TimecardController`:**
    - `submitTimecard(timecard: Timecard)`
    - `validateTimecard(timecard: Timecard): bool`
  - **`Timecard`:**
    - `linkToProject(String)`
  - **`ProjectManagementDatabase`:**
    - `fetchChargeCodes(projectId: String): List<String>`
- **Payment Subsystem:**
  - **`BankSystem`:**
    - `processDirectDeposit(paycheck: Paycheck, bankInfo: BankInformation)`
  - **`PrinterInterface`:**
    - `printPaycheck(paycheck: Paycheck)`
- **System Management Subsystem:**
  - **`SystemClockInterface`:**
    - `triggerEventAt(DateTime, Runnable)`

## ⭐️ 3. Define Methods:
#### 👉 Mô tả chi tiết các phương thức:
- calculatePay:
  - Input: Employee
  - Output: Paycheck
  - Mô tả: Tính toán số tiền lương dựa trên loại nhân viên và thông tin giờ làm việc từ Timecard.

- processDirectDeposit:
  - Input: Paycheck, BankInformation
  - Output: None
  - Mô tả: Xử lý thanh toán trực tiếp qua ngân hàng dựa trên thông tin paycheck và tài khoản ngân hàng.

## ⭐️ 4. Define States:
#### 👉 Trạng thái chính của các lớp quan trọng:
- **Paycheck**:
  - `Pending`, `Paid`, `Error`.
- **Timecard**:
  - `New`, `Submitted`, `Validated`.
  - 
## ⭐️ 5. Define Attributes:
#### 👉 Thuộc tính cho các lớp:
- **Payroll Calculation Subsystem**
  - **`PayrollController`:**
      - `currentPayPeriod: DateRange`
  - **`Employee`:**
    - `id: int`
    - `name: String`
    - `employmentType: EmploymentType`
  - **`Paycheck`:**
    - `amount: float`
    - `status: PaycheckStatus`
- **Timecard Subsystem**
  - **`TimecardController`:**
    - `activeTimecards: List<Timecard>`
  - **`Timecard`:**
    - `hoursWorked: float`
    - `chargeCode: String`
  - **`ProjectManagementDatabase`:**
    - `projectData: Map<String, Project>`
- **Payment Subsystem:**
  - **`BankSystem`:**
    - `transactionHistory: List<BankTransaction>`

## ⭐️ 6. Define Dependencies:
#### 👉 Mối phụ thuộc giữa các lớp:
- **Timecard Subsystem** (`Timecard`) → **Payroll Calculation Subsystem** (`PayrollController`): `Timecard` cung cấp thông tin giờ làm việc cho `PayrollController`.
- **Payroll Calculation Subsystem** (`PayrollController`) → **Payment Subsystem:** (`BankSystem`): Chuyển thông tin lương cho hệ thống ngân hàng.
- **System Management Subsystem:** (`SystemClockInterface`) → **Payroll Calculation Subsystem** (`PayrollController`): Kích hoạt quy trình tính lương theo lịch trình.

## ⭐️ 7. Define Associations:
#### 👉 Quan hệ kết hợp giữa các lớp:
- Employee ↔ Timecard (1:N): Một nhân viên có nhiều Timecard.
- PayrollController → BankSystem: Quan hệ sử dụng (uses).
- PayrollController → PrinterInterface: Quan hệ sử dụng (uses).

## ⭐️ 8. Define Internal Structure:
#### 👉 Chi tiết cấu trúc nội bộ:
- `PayrollController`:
  - Lưu tham chiếu đến danh sách nhân viên (`Employee[]`) và bảng tính lương hiện tại (`currentPayPeriod`).
- `BankSystem`:
  - Sử dụng `BankTransaction` để quản lý lịch sử giao dịch.

## ⭐️ 9. Define Generalizations:
#### 👉 Tổng quát hóa các lớp:
- Employee:
  - Subclasses: `HourlyEmployee`, `SalariedEmployee`, `CommissionedEmployee`.
- PrinterInterface:
  - Subclasses: `LaserPrinter`, `InkjetPrinter`.

## ⭐️ 10. Resolve Use-Case Collisions:
#### 👉 Giải quyết xung đột giữa các ca sử dụng:
- Nhiều ca sử dụng cần truy cập vào cùng một subsystem hoặc tài nguyên chung, có thể dẫn đến:
  - Trùng lặp logic xử lý.
  - Xung đột về thứ tự thực thi.
  - Khó khăn trong việc mở rộng hệ thống hoặc thay đổi logic.
👉 **Sử dụng các giao diện (Interface) để giảm xung đột:**
  - Sử dụng `BankSystemInterface` để xử lý giao tiếp giữa `Payroll` và `BankSystem`.
    - Các ca sử dụng `Run Payroll` và `Process Manual Payment` đều yêu cầu thực hiện giao tiếp với `BankSystem` để xử lý thanh toán (`Direct Deposit`).
    - Các ca sử dụng gọi đến `BankSystemInterface` thay vì trực tiếp gọi `BankSystem`.
    - Logic thanh toán có thể trùng lặp hoặc thiếu sự kiểm soát thống nhất.

## ⭐️ 11. Handle Nonfunctnal Requirements in Generral:
#### 👉 Xử lý yêu cầu phi chức năng:
- **Hiệu suất (Performance):**
  - Tối ưu hóa truy xuất `Timecard` từ `ProjectManagementDatabase`.
- **Bảo mật (Security):**
  - Mã hóa thông tin ngân hàng (BankInformation).
- **Khả năng mở rộng (Scalability):**
  - Thiết kế các lớp và phương thức để hỗ trợ nhiều loại nhân viên.

## ⭐️ 12. Check point:
#### 👉 Kiểm tra cuối cùng:
- **Consistency:** Các lớp được định nghĩa rõ ràng, không trùng lặp chức năng.
- **Modularity:** Subsystem tách biệt và dễ bảo trì.
- **Dependency Management:** Mọi phụ thuộc được quản lý qua giao diện và các phương thức API.

## ⭐️ 13. Class Diagram
<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/V5J1Zfim4Btp5JucKl83Q1NjDhlIHkfAKHAfvy5CY8knaMqYeMg_h8T-Kd-XOx21D6Hp2DYUUU_Dcp5_V_zvjWwCQogP9BOKYXbjCKcu16lP7bgZfTngvVmJ3VkLCFgj6M-CGUKeO8z6w3nbh-3m0Ah0Be8n3f8taZOfPe5LBNMBcBAtyBPCFJg_82z3GYwiCo9hkepkm2wMoMVK4XC72O98XN9XfQ0Yz2CXg29izQGLoJorzK0Tru6rGFUk6oFR0qbTaAgprE36moD8C0Bpbqetoeq1dnEFEh63BkWYfq1hHXwxneub7xjrOAd0b7iG-RJQawYGWya7r0k9j3-qAJ6_XUONC0LkTNvRFcDIgFAazqR_HEuMTV_SvJ5gXcocpy2Tk68Ce0g-KvUUudeJg6oJLSB5tOKBB-c0l0o1Lv0Y9wE_2arPfhMS6Dmh_m051VhkqQH11dQSX52Rtq_P1zHFVOMhc1fbdj7notRmoywO4WhiLvjHn3TGvR6r3gk1rHbGrlkZrJlbQDE6P1zx6WyZEv5njFPL6AyLQsq5jIKCn3WQAvPH_awTTTgn-ZTJWKTQJasXqKUpytzduD4BpoAwQzbXpS1FCFfwjbBpyXw732WAD6zNClp5TNtgxxZlquhrfQNiq2W5cSGEzlvpiLvlXelxu7Zu2imVtyzcCZEkqyZXl8T_D3qF-CP6FzBxd_F9h8sXijlyv1bLxh-q_m000F__0m00" alt="Diagram">

  
## ⭐️ 14. Sequence Diagram
#### 👉 Ca sử dụng: Tính lương và thanh toán
<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/V99DJiGm38NtEOMNCukvG1TeW6713WakO1AFi9gVod6HUZOM78aha1H5Gsc7B18fptx-OkVhu_EO5KN7u4tkEOAaJCQWrIHmwm97CnIPBGyO5PvmakJzVOfQJvA5-iA1B8gx8jzXx9-dh1IMdi9HIHxhTaPB2_4X33vDL91c63ZSh1awS9nL-7LKAg9z8zldtTwi0clsch63T_JiKAbf9NST1eVjsYqIYWDkrsoFwC2YjwF7cRDKQS8rx_OQSAJ8Fc_RN_hQmI39Kiud5h9weY5brbspsHlqFsE00QT0fRzvj3NUG5aNdtzuvYoRufabe7AAXdocfUcvi8v2i-acyT-HL-voqpX_0LDqvbYs-Z-_0G00__y30000" alt="Diagram">

## ⭐️ 15. State Diagram
#### 👉 `Paycheck`
<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTnTcQUGb5-SIeNLxHMh8Akhfr2G6fUIcPUEXUKXeWbPgOeM06fojpKl1A5uDBavDJYuhJI71HLhaL5-KL8ojmICtDIKxWWmaX60vK4fPOKLS8KSe6D1oa0ke7B0QW8v3G00000__y30000" alt="Diagram">

## ⭐️ 16. Component Diagram
#### 👉 Mô tả các subsystem và mối liên kết
<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/X55B3e8m5Dpt58rxhc1GOC72X4HtXCMpF0tI3schaHXFvi8ZUGKXKC5_5stIcTVvz7Qv-iQ2jdl1YIaBIRKoI4W5h8Gjqaa2jLQSqsLjB8e9FH7QhBI_3fIqxOawevutfUaSPDbHiz_4H1VIeexRRGCC_z1NXK06EXy1tS07m0ce7JAx0Dda42Xj21RMO9nIvpBWYfM3YNxqpGGvZog9ZWrTWkl4F4ePXUyUSimMc2Mno_WQ_QcHK1U7Nl5xk4XKNDM8GoOVPTx-uHq00F__0m00" alt="Diagram">

  
#### ⭐️ <i> From [Trần Thị Thanh Kiều](https://github.com/tukieef-nah) - 4451051111 </i> 💙
