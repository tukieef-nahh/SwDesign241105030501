# 🐳 Bài thực hành Lab3 - Identify design elements <img src="https://media.giphy.com/media/fYSnHlufseco8Fh93Z/giphy.gif" width="30">

## ⭐️ 1. Subsystem context diagrams 📈

### 👉 Biểu đồ ngữ cảnh của các hệ thống con:
#### 1.1 BankSystem Subsystem
<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/f58zJyCm4DtzAqwTMecqi4QLLQLJDYG6PfDS4okE7PqT809-6GC_YRz0d0yr8LGTMEpptRrtxvty_Vbri4wGgql5R25r9KYKa2XXBRmnW4WaHKQcrkdHA4Fmc4k7FcyeHUfpaMgRs0UR44Zja4uYmV-G42PEw4pzJQ9abhi6bJ8lbwXw6_UY8QFKqMZdRoJOxuS74kUUUxS3gZLKVUTwuy5d2t4aTF7GM8Tb2ut7FEUTBaYnCbQwjMW79JacHGXZTECNOJmy17_6-cIe54uQlPa9xBfRSjHEkeRpeV8BmzXv9JDDjdwoVLoHUMq6PNx2qlpgThkzMq4Gy26SsWiXbNx6QCf2fyp2inICpHRn7WGJ4REQvnvDBGeBJvU0rt07r6dxRNy0003__mC0" alt="Diagram">
</p>

#### 👉 Giải thích:
IBankSystem: Đóng gói các giao tiếp với tất cả các hệ thống ngân hàng bên ngoài.
deposit: Gửi tiền lương được chỉ định vào ngân hàng được xác nhận.

#### 1.2 PrintService Subsystem
<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/f5AzJiCm4Dxz5ATEhKHQMAF8gjgfMwKEpCOv4gkE7PqT80AUZ857uXMmywEIG2Sctzrtz_r8_lhut3elo3ULPkwiJ2r8L22rS0vU6S1Eo7D1jZ7vtcfBS5ygZt5kAKVgPpiTbjWx-q6WZ4Tw51B_Gq8elJ25_fj4gwBqBMfjdwzHzJ6EeYMhzTuQ7ryaoBAXGU8yScysG8s1kjzShkBn9SBXIA4v8Jsfq6NPOKGuxvn17V6b24AoH7bEOQnkm9hk62c5amzLiPeOwxO29HglVCivOvVGCrNNFBZMUQo2d7rf1-t8zZlWudQzlbj0al2Xd4P88KRjj0TtZCr2lYN9nC0CZyoZ_M3WEhH5auU_zGq00F__0m00" alt="Diagram">
  
#### 👉 Giải thích:
`IPrintService`: Đóng gói các giao tiếp với tất cả printers.
`print`: In `Paycheck`(Phiếu lương) đã cho trên printer được chỉ định.

#### 1.3 ProjectManagementDatabase Subsystem
<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/f5F1JW8n5BptAnfEOCAYLq8s1BoGg371nFEZ-ooLRajUtwf4_J8FVfA_O7TPN5JOn7Xhf_FcpKpIZxVtSM0WBd8hmiguDH3aKba8GJuBAIUWLffyuRAfjvxaxT8mbhYd36cBJMmaYLUn9s0S8zs1ml-842e6f-rX4MlqaZTehNyy9hMDSMDoL41np35vQv7aQ5HVaDAq51yCf4QMgY1qBBcUwFRsdfP06gNo6OOTNgmpOFn53_3m3OnEcZvcr-JlOx1BSA0nZ-lEWM410QEhsOwMfbNcSlEqMdnLv0kaq5KKgoC3GpbdCaxtXj4PRWaN9d0J-skkWaLJPfk1K2p29Z3cSat-QLFRA4KFjDWvJPAJZkptq-furcaBDvHrXT7Ht1UaK8YsBbwIvBZJjiaaINzc_nDvZ2wBl-4J003__mC0" alt="Diagram">
  
#### 👉 Giải thích:
`IProjectManagementDatabase`: Đóng gói các giao tiếp với `Cơ sở dữ liệu quản lý dự án cũ` có chứa thông tin về `project charge numbers`.
`getChargeNumbers`: Truy xuất các `chrage numbers` có sẵn.

## ⭐️ 2. Analysis Class to Design Element Map 📑
| Analysis Class            | Design Element                                  |
|---------------------------|-------------------------------------------------|
| LoginForm                 | LoginForm                                       |
| MaintainTimecardForm      | MaintainEmployeeForm, TimecardForm, MainApplicationForm |
| TimecardController        | TimecardController                              |
| SystemClockInterface      | SystemClockInterface                            |
| PayrollController         | PayrollController                               |
| Paycheck                  | Paycheck                                        |
| HourlyEmployee	          | HourlyEmployee                                  |
| PurchaseOrder	            | PurchaseOrder                                   |
| CommissionedEmployee	    | CommissionedEmployee                            |
| SalariedEmployee	        | SalariedEmployee                                |
| Employee                  | Employee                                        |
| Timecard                  | Timecard                                        |
| Payroll Administrator     | Interface for managing employee records         |
| BankSystem                | BankSystem subsystem, IBankSystem interface     |
| PrinterInterface	        | IPrintService interface, PrintService subsystem |
| ProjectManagementDatabase	| ProjectManagementDatabase subsystem, IProjectManagementDatabase interface |

## ⭐️ 3. Design element to owning package map 🔬
| Design Element                       | "Owning" Package                              |
|--------------------------------------|-----------------------------------------------|
| LoginForm                            | Middleware::Security:GUI Framework            |
| MainEmployeeForm TimecardForm        | Applications::Employee Activities             |
| TimecardForm	                       | Applications::Employee Activities             |
| MainApplicationForm                  | Middleware::Security:GUI Framework            |
| TimecardController                   | Apllications::Employee Activities             |
| SystemClockInterface                 | Applications::Payroll                         |
| PayrollController                    | Apllications::Payroll                         |
| Paycheck                             | Business Services::Payroll Artifacts          |
| HourlyEmployee	                     | Business Services::Payroll Artifacts          |
| Timecard	                           | Business Services::Payroll Artifacts          |
| PurchaseOrder                        | Business Services::Payroll Artifacts          |
| CommissionedEmployee	               | Business Services::Payroll Artifacts          |
| SalariedEmployee	                   | Business Services::Payroll Artifacts          |
| Employee                             | Business Services::Payroll Artifacts          |
| BankSystem subsystem                 | Business Services                             |
| IBankSystem interface                | Business Services::External System Interfaces |
| IPrintService interface              | Business Services::External System Interfaces |
| PrintService subsystem               | Business Services                             |
| ProjectManagementDatabase subsystem  | Business Services                             |
| IProjectManagementDatabase interface | Business Services::External System Interfaces |


## ⭐️ 4. Architectural layers and their dependencies 📇
