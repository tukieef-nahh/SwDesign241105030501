# 🐳 Bài thực hành Lab3 - Identify design elements <img src="https://media.giphy.com/media/fYSnHlufseco8Fh93Z/giphy.gif" width="30">

## ⭐️ 1. Subsystem context diagrams 📈

#### 👉 Biểu đồ ngữ cảnh của các hệ thống con:
<p align="center">
  <img src="" alt="Diagram">
</p>

#### 👉 Giải thích:













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
