# 🐳 Bài thực hành Lab2 <img src="https://media.giphy.com/media/fYSnHlufseco8Fh93Z/giphy.gif" width="30">

</br>📑 Tài liệu yêu cầu
</br>📎 https://drive.google.com/file/d/1CSNZ0j5kiMHLyDXOxk1UHgETDVAHx6eP/view 

## ⭐️ 1. Tiến hành phân tích tất cả các ca sử dụng còn lại trong hệ thống Payroll System 📈

### ⭐️ 1.1. Phân tích ca sử dụng Maintain Timecard 📑

#### 👉 Các lớp phân tích cho ca sử dụng Maintain Timecard:** 
- **Entity classes:** 
  + **Employee:**
  + **Timcard:**

- **Boundary classes:** 
  + **ProjectManagementDatabase:**
  + **TimecardForm:**

- **Control classes:** 
  + **TimeCardController:**  

👉 **Sequence diagram cho ca sử dụng Maintain Timecard:** 

<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/d9HBKeD048RtSuhUgGjJPN2LXPKg7pij5rvW0fq4PMQedaRbR2uyabUmWK0c8P0e1Ojv_5__tJt3pzVttBCcBaoc_5jgWPn7fNJCZk3Uv9ah4TN25JRHL0Ayf0PZJSc38wDYPvbSratUDkCCIQ7bbCjkfHstHD0UqEHRy3EvLupvKLkzGYExxpJhXHOlZPNUkb8Tw_9cnzOChkhNwDIoVC2RnVCBfSADeN1hNRGJKQ-G8Iw895G8wE-lA99ABHiHwepX2J_0MOIOK3Cca2uXPKWSUdl6W9-fPmNo2AwY3jQaYJKTZ8KswOoE93c9Pa381TaUP23FlJ8BudeOCLZhLYq99AdFCrt-eqNH9lkrffLKr2Ne1zipMiYeQzekQb1qaDYGfjjg1B0-QYIji2aXuxI6H653Gld8RH7JOabuQrUGXwNSjetK5cQ1v4zjohIgP94dShQFNvbsjfOT5evubY9v_Ov_FZTri_ULnmn6ZS5UmBdSi-g_-Gi00F__0m00" alt="Diagram">
</p>

👉 **Nhiệm vụ và các thuộc tính của các lớp phân tích:** 
- **Employee (Entity):**
  + Các thuộc tính:
    - `empID`
    - `name`
    - `bank info`
    - `social security number`
    - `address`
    - `phone number`
    - `email`
    - `payment method`
  + Các phương thức:
    - `is payday()`
    - `get pay amount()`
    - `get payment method()`
    - `get bank info()`
    - `get curent timecard()`
    - `calculatePay()`

- **Timecard (Entity):**
  + Các thuộc tính:
    - `hours worked`
    - `pay period`
  + Các phương thức:
    - `save()`
    - `get timecard info()`
    - `update timecard()`

- **ProjectManagenmaentDatabase (Boundary):**  
  + Các phương thức:
    - `get charge codes()`
   
- **TimecardForm (Boundary):**  
  + Các phương thức:
    - `display timecard()`
    - `open()`
    - `enter hours for charge numbers()`
    - `maintain timecard()`
    - `save timecard()`

- **TimecardController (Control):**  
  + Các phương thức:
    - `get curent timecard()`
    - `get charge codes()`
    - `update timecard()`
    - `save timecard()`

👉 **Xác định quan hệ giữa các lớp phân tích:** 
- 

👉 **Class diagram mô tả các lớp phân tích và giải thích:** 

<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/Z9HBRjim48RtFCN0cpG1xCJRmaY2vW5qKI08Ue4nER5OymMIIY0KFLaNELAl48fwc8xbD08aaFmvCnzdXlhtz_KwHFInreg5hJJWRI36Jk2RhOr0ty2DmX0ORx_mKshYwCMzzHfMgtM_v_8IVZD8p_av21cSmWPYl_NBwQ1OHsOt8nF9GsLh7-39Uk0L-Ws1gVMQVDZjqoXDJE-4mu3FL2x_QRblh8dUgadiNbCfy6h5kqd9lg48lFO-iKs4osf7oQsWWh5s0YDzbl3EH1dxlD9xn0H6MH-vkXIzMBybaHTSoguZBwrWPPnzq24eIFDaFo9DI1t1dNRADaI710OrvG5fz_qsZzPejjbrdWNB9Ie8b9BN7gqhOfPG24-f41cyiePAaL9nrN0ctMPTKwoASydGAWARg_tJjIb0dRel7gmNRlQr4VbTHO_McwFYjKhfUi2cJDI3jx-8nnzeS4Djk5kCkCP0Hsx4HD_aFdYav5nQ4ohf0jkxMhFbOh6SmNm-Z0uxc4qqzUnYiJZhp2wosL7KOzRBqdhioQymf6bO-ezz1prq51jRgnVEvhKRO4UFx9gCQ7z3Rm000F__0m00" alt="Diagram">
</p>

- **Giải thích:** 
  + _ProjectManagenmaentDatabase:_
 
  +  _TimecardForm:_

  + _TimecardController:_ 

  + _Employee:_

  + _Timecard:_

## ⭐️ 1.2 Phân tích ca sử dụng Run Payroll 📇

#### 👉 Các lớp phân tích cho ca sử dụng Run Payroll:
- **Entity classes:** 
  + **Employee:**
  + **Timcard::**
  + **Paycheck:**
  + **HourlyEmployee:**
  + **SalariedEmployee:**
  + **CommissioneEmployee:**
  + **PurchaseOrder:**

- **Boundary classes:** 
  + **SystemClockInterface:**
  + **BankSystem:**
  + **PrinterInterface:** 

- **Control classes:** 
  + **PayRollController:**  

👉 **Sequence diagram cho ca sử dụng Run Payroll:** 

<p align="center">
  <img src="" alt="Diagram">
</p>

👉 **Nhiệm vụ và các thuộc tính của các lớp phân tích:** 
- **Employee (Entity):**  
  + Các thuộc tính:
    - `empID`
    - `name`
    - `bank info`
    - `social security number`
    - `address`
    - `phone number`
    - `email`
    - `payment method`
  + Các phương thức:
    - `is payday()`
    - `get pay amount()`
    - `get payment method()`
    - `get bank info()`
    - `get curent timecard()`
    - `calculatePay()`

- **Timecard (Entity):**  
  + Các thuộc tính:
    - `hours worked`
    - `pay period`
  + Các phương thức:
    - `save()`
    - `get timecard info()`
    - `update timecard()`

- **Paycheck (Entity):**  
  + Các thuộc tính:
    - `amount`
  + Các phương thức:
    - `create with amount()`

- **HourlyEmployee (Entity):**  
  + Các thuộc tính:
    - `hourlyRate`
  + Các phương thức:
    - `getHourlyRate()`

- **SalariedEmployee (Entity):**  
  + Các thuộc tính:
    - `annualSalary`
  + Các phương thức:
    - `getAnnualSalary()`

- **CommissioneEmployee (Entity):**  
  + Các thuộc tính:
    - `commissionRate`
  + Các phương thức:
    - `getPurchaseOrders()`
    - `getCommissionRate()`

- **PurchaseOrder (Entity):**  
  + Các phương thức:
    - `get PO info()`

- **SystemClockInterface (Boundary):**  
  + Các phương thức:
    - `start()`

- **BankSystem (Boundary):**  
  + Các phương thức:
    - `send bank transaction(thePaycheck: Paycheck, theBankInfo)`

- **PrinterInterface (Boundary):**  
  + Các phương thức:
    - `print()`

- **PayRollController (Control):**  
  + Các phương thức:
    - `run payroll()`
      
👉 **Xác định quan hệ giữa các lớp phân tích:** 
- 

👉 **Class diagram mô tả các lớp phân tích và giải thích:** 

<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/d5HBRjmm3Dth5CAi9a4TDDiksYJJ0fbL1aqlmCXCBLWVGvy6HfkJTT4ZzGgLD9OjVz15PZCq7_b8FOhw-_lFZNLWd9U2s9OhQhH5GfW0Q-bZRntAWz2iFIg7vXaOqf-4fbzAsr-Gro7uP7YCMGTs4IW2xq2rP-Q92rLDduAVEWFA0dDSgxrhy0GzQv2r7sYstj7WZXH7zQmZQMus11Wjn44h5__HZEp6AzgTqNsPyKLsGlUOErKWCHaek-FdPAMMU2YKlgnc74Hebdd3NK-Lbqze4WHrRT3QP7UDLbY2A86BCmIzHEMeHDVeEhcgQkYIsmZNqEylFWskx-YYZuBKFaauSnTCCsXiUkODFPkOuBX41cPAOI2O5-2YriMKxhKtebz8r2Jdrn0yxpqKk1-XWkGH11YEzO86bF8W4jYlY6uBiA0wQ2cvjU5UhEZO26rsTlA6DM3nmTHeR2dAOPPO5FisY5GSsz8NRLgiynnfXuOlPsZX1yvKpshFv-6xEjGhH_4wNU9qoxDGQV3p6inWJ7xXhfaknfXVddKWARMWfuVSIjY3pVtUNLzTNUz2LhPMYqNMgxPxFoO5wt8txXOPPpMmNLQ-oq5Pvly6PKd8gCq03CMsErm-HlC6ttIgO4rF5rdiHrNz-ZWTUdNlv_3cNKuXoyJjq2sLoi4JSXCUrFYa_mC00F__0m00" alt="Diagram">
</p>

- **Giải thích:** 
  + _Employee:_ 

  + _Timecard:_ 

  + _Paycheck:_ 

  + _HourlyEmployee:_

  + _SalariedEmployee:_

  + _CommissioneEmployee:_

  + _PurchaseOrder:_

  + _SystemClockInterface:_

  + _BankSystem:_

  + _PrinterInterface:_

  + _PayRollController:_
  

## ⭐️ 2. Viết code Java mô phỏng ca sử dụng Maintain Timecard 🔬

#### 👉 Class Entity của Employee
```
package Lab2;

public class Employee {
    private String empID;
    private String name;
    private Timecard currentTimecard;
    private int maxHours;
    private String username;
    private String password;

    public Employee(String empID, String name, int maxHours, String username, String password) 
    {
        this.empID = empID;
        this.name = name;
        this.maxHours = maxHours;
        this.username = username;
        this.password = password;
        this.currentTimecard = new Timecard(empID);
    }

    public Timecard getCurrentTimecard() {
        return currentTimecard;
    }

    public boolean canWorkMoreHours(int hours) {
        return currentTimecard.getTotalHours() + hours <= maxHours;
    }
}
```
- `getCurrentTimecard()`: Lấy phiếu chấm công hiện tại của nhân viên.
- `canWorkMoreHours(int hours)`: Kiểm tra xem nhân viên có thể làm thêm hours giờ mà không vượt quá maxHours.

#### 👉 Class Entity của Timecard
```
package Lab2;

import java.util.Date;
import java.util.HashMap;
import java.util.Map;
import java.util.UUID;

public class Timecard {
    private String timecardID;
    private String empID;
    private Date startDate;
    private Date endDate;
    private Map<Date, Integer> hoursWorked;
    private Map<Date, String> chargeNumbers;
    private String status;
    private Date submittedDate;

    public Timecard(String empID) {
        this.timecardID = UUID.randomUUID().toString();
        this.empID = empID;
        this.hoursWorked = new HashMap<>();
        this.chargeNumbers = new HashMap<>();
        this.status = "draft";
    }

    public int getTotalHours() {
        return hoursWorked.values().stream().mapToInt(Integer::intValue).sum();
    }

    public void setHoursWorked(Date date, int hours, String chargeNumber) {
        hoursWorked.put(date, hours);
        chargeNumbers.put(date, chargeNumber);
    }

    public void submitTimecard() {
        this.status = "submitted";
        this.submittedDate = new Date();
    }

    public boolean isSubmitted() {
        return "submitted".equals(status);
    }
}
```
- `getTotalHours()`: Tính tổng số giờ đã làm việc của nhân viên.
- `setHoursWorked(Date date, int hours, String chargeNumber)`: Cập nhật số giờ làm việc cho một ngày cụ thể với charge number.
- `submitTimecard()`: Đánh dấu timecard là "submitted" và lưu lại ngày nộp.
- `isSubmitted()`: Kiểm tra xem timecard đã được gửi hay chưa.

#### 👉 Class Entity của Project
```
package Lab2;

public class Project {
    private String projectID;
    private String projectName;
    private String chargeNumber;

    public Project(String projectID, String projectName, String chargeNumber) {
    	this.projectID = projectID;
        this.projectName = projectName;
        this.chargeNumber = chargeNumber;
    }
}
```

#### 👉 Class Boundary của TimecardBoundaryForm
```
package Lab2;

public class TimecardBoundaryForm {
    public void requestTimecardInfo(Employee employee) {
        System.out.println("Enter hours for each day.");
    }

    public void displayTimecard(Timecard timecard) {
        System.out.println("Displaying timecard details...");
    }

    public void displaySuccessMessage() {
        System.out.println("Timecard updated successfully.");
    }

    public void displayErrorMessage(String error) {
        System.out.println("Error: " + error);
    }

    public void displayReadonlyTimecard(Timecard timecard) {
        System.out.println("Timecard is in read-only mode. No changes allowed.");
    }
}
```
- `requestTimecardInfo(Employee employee)`: Yêu cầu nhập thông tin timecard (giờ làm việc) cho từng ngày.
- `displayTimecard(Timecard timecard)`: Hiển thị thông tin timecard.
- `displaySuccessMessage()`: Hiển thị thông báo thành công sau khi cập nhật timecard.
- `displayErrorMessage(String error)`: Hiển thị thông báo lỗi.
- `displayReadonlyTimecard(Timecard timecard)`: Hiển thị timecard ở chế độ chỉ đọc nếu đã được gửi.

#### 👉 Class Control của TimecardController
```
package Lab2;

import java.util.Date;
import java.util.HashMap;
import java.util.Map;

public class TimecardController {
    private TimecardBoundaryForm boundaryForm;
    private Map<String, Project> projectDatabase;

    public TimecardController(TimecardBoundaryForm boundaryForm) {
        this.boundaryForm = boundaryForm;
        this.projectDatabase = new HashMap<>();
    }

    public void retrieveTimecard(Employee employee) {
        Timecard timecard = employee.getCurrentTimecard();
        if (timecard.isSubmitted()) {
            boundaryForm.displayReadonlyTimecard(timecard);
        } else {
            boundaryForm.displayTimecard(timecard);
        }
    }

    public void updateTimecard(Employee employee, Date date, String chargeNumber, int hours) {
        Timecard timecard = employee.getCurrentTimecard();
        if (timecard.isSubmitted()) {
            boundaryForm.displayErrorMessage("Cannot update submitted timecard.");
            return;
        }

        if (hours > 24 || !employee.canWorkMoreHours(hours)) {
            boundaryForm.displayErrorMessage("Invalid number of hours.");
            return;
        }

        timecard.setHoursWorked(date, hours, chargeNumber);
        boundaryForm.displaySuccessMessage();
    }

    public void submitTimecard(Employee employee) {
        Timecard timecard = employee.getCurrentTimecard();
        if (timecard.isSubmitted()) {
            boundaryForm.displayErrorMessage("Timecard already submitted.");
            return;
        }

        if (!employee.canWorkMoreHours(timecard.getTotalHours())) {
            boundaryForm.displayErrorMessage("Exceeded maximum allowable hours.");
            return;
        }

        timecard.submitTimecard();
        boundaryForm.displaySuccessMessage();
    }

    private boolean validateHours(String empID, int totalHours) {
        Employee employee = new Employee(empID, "", 40, "", "");
        return employee.canWorkMoreHours(totalHours);
    }
}
```
- `retrieveTimecard(Employee employee)`: Lấy thông tin timecard của nhân viên và hiển thị. Nếu timecard đã gửi, hiển thị chế độ chỉ đọc; nếu chưa gửi, hiển thị thông tin để chỉnh sửa.
- `updateTimecard(Employee employee, Date date, String chargeNumber, int hours)`: Cập nhật giờ làm việc của nhân viên cho một ngày cụ thể.
  - Nếu timecard đã gửi, hiển thị lỗi "Cannot update submitted timecard".
  - Nếu số giờ lớn hơn 24 hoặc vượt quá giới hạn maxHours của nhân viên, hiển thị lỗi.
  - Nếu hợp lệ, cập nhật giờ và charge number cho ngày đó, sau đó hiển thị thông báo thành công.
- `submitTimecard(Employee employee)`: Gửi timecard của nhân viên.
  - Nếu timecard đã gửi, hiển thị lỗi "Timecard already submitted".
  - Nếu tổng số giờ vượt quá giới hạn maxHours, hiển thị lỗi.
  - Nếu hợp lệ, đánh dấu timecard là "submitted" và hiển thị thông báo thành công.
- `validateHours`: giúp xác minh xem nhân viên có thể làm thêm số giờ chỉ định mà không vượt quá giới hạn số giờ tối đa.

#### 👉 Phân tích code Java mô phỏng ca sử dụng Maintain Timecard
Lớp `Employee` lưu trữ thông tin nhân viên và timecard.
Lớp `Timecard` lưu trữ thông tin về giờ làm việc và trạng thái của timecard.
Lớp `Project` đại diện cho dự án mà nhân viên có thể làm việc.
`TimecardBoundaryForm` là giao diện, hiển thị thông tin timecard cho người dùng.
`TimecardController` điều khiển logic nghiệp vụ: cập nhật giờ làm việc, kiểm tra giới hạn giờ, và gửi timecard, đảm bảo các quy trình diễn ra đúng theo yêu cầu hệ thống.

⭐️ **Luồng hoạt động cho Maintain Timecard**
**1. Lấy và Hiển thị Thông tin Timecard (`retrieveTimecard`)**
- Người dùng yêu cầu xem timecard của mình.
- `TimecardController` gọi phương thức `retrieveTimecard` để lấy timecard hiện tại của nhân viên `employee.getCurrentTimecard()`.
- Nếu timecard đã được gửi `timecard.isSubmitted()` trả về `true`, hệ thống sẽ hiển thị thông báo rằng timecard này ở chế độ chỉ đọc (không thể chỉnh sửa) thông qua phương thức `displayReadonlyTimecard` của lớp `TimecardBoundaryForm`.
- Nếu timecard chưa gửi, hệ thống sẽ hiển thị thông tin timecard cho phép chỉnh sửa bằng cách gọi `displayTimecard` trong `TimecardBoundaryForm`.

**2. Cập nhật Thông tin Timecard (`updateTimecard`)**
- Người dùng yêu cầu cập nhật giờ làm việc cho một ngày cụ thể, kèm mã dự án và số giờ làm việc.
- `TimecardController` gọi `updateTimecard` để kiểm tra điều kiện trước khi cập nhật.
  - Nếu timecard đã được gửi `isSubmitted()` trả về `true`, `TimecardController` hiển thị thông báo lỗi qua `displayErrorMessage` trong `TimecardBoundaryForm`.
  - Nếu số giờ làm việc lớn hơn 24 hoặc tổng số giờ đã làm cộng thêm số giờ mới vượt quá giới hạn của nhân viên `canWorkMoreHours` trả về `false`, `TimecardController` hiển thị thông báo lỗi qua `displayErrorMessage`.
- Nếu tất cả điều kiện hợp lệ, `TimecardController` gọi phương thức `setHoursWorked` trên `Timecard` để cập nhật số giờ làm và mã dự án. Sau khi cập nhật thành công, hệ thống hiển thị thông báo thành công `displaySuccessMessage` qua `TimecardBoundaryForm`.

**3. Nộp Timecard (`submitTimecard`)**
- Khi người dùng yêu cầu nộp timecard, `TimecardController` gọi phương thức `submitTimecard`.
- Nếu timecard đã được gửi `isSubmitted()` trả về `true`, `TimecardController` hiển thị thông báo lỗi qua `displayErrorMessage`.
- Nếu tổng số giờ đã làm vượt quá giới hạn cho phép của nhân viên `canWorkMoreHours` trả về `false`, `TimecardController` hiển thị thông báo lỗi qua `displayErrorMessage`.
- Nếu tất cả điều kiện hợp lệ, `TimecardController` gọi `submitTimecard` trong `Timecard` để cập nhật trạng thái `timecard` thành "submitted" và gán ngày nộp `submittedDate` là ngày hiện tại. Cuối cùng, `TimecardBoundaryForm` hiển thị thông báo thành công `displaySuccessMessage`.

#### ⭐️ _From [Trần Thị Thanh Kiều](https://github.com/tukieef-nah) - 4451051111_ 💙
