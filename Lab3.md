# 🐳 Bài thực hành Lab3 - Identify design elements <img src="https://media.giphy.com/media/fYSnHlufseco8Fh93Z/giphy.gif" width="30">

## ⭐️ 1. Subsystem context diagrams 📈

#### 👉 Biểu đồ ngữ cảnh của các hệ thống con:
<p align="center">
  <img src="" alt="Diagram">
</p>

#### 👉 Giải thích:













## ⭐️ 2. Analysis Class to Design Element Map 📑
| Analysis Class           | Design Element                          |
|--------------------------|-----------------------------------------|
| LoginForm                | LoginForm                               |
| MaintainTimecardForm     | MaintainEmployeeForm TimecardForm       |
|                          | MainApplicationForm                     |
| TimecardController       | TimecardController                      |
| SystemClockInterface     | SystemClockInterface                    |
| PayrollController        | PayrollController                       |
| Paycheck                 | Paycheck                                |
| Employee                 | Design Class **Employee**               |
| Timecard                 | Design Class **Timecard**               |
| Project                  | Design Class **Project**                |
| Payroll Administrator    | Interface for managing employee records |

## ⭐️ 3. Design element to owning package map 🔬
| Design Element                | "Owning" Package                              |
|-------------------------------|-----------------------------------------------|
| LoginForm                     | Middleware::Security:GUI Framework            |
| MainEmployeeForm TimecardForm | Applications::Employee Activities             |
| MainApplicationForm           | Middleware::Security:GUI Framework            |
| TimecardController            | Apllications::Employee Activities             |
| SystemClockInterface          | Applications::Payroll                         |
| PayrollController             | Apllications::Payroll                         |
| Paycheck                      | Business Services::Payroll Artifacts          |
| Employee                      | EmployeeManagement::Employee                  |
| PayrollAdministrator          | EmployeeManagement::Administration            |
| Timecard                      | TimecardPackage::TimecardManagement           |
| Project                       | TimecardPackage::ProjectTracking              |
| BankSystem Interface          | PaymentProcessing::BankIntegration            |
| PrintService Interface        | PaymentProcessing::PrintIntegration           |
| Transaction Classes           | PaymentProcessing::TransactionManagement      |


## ⭐️ 4. Architectural layers and their dependencies 📇
