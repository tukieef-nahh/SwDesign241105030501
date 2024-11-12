# 🐳 Bài thực hành Lab2 <img src="https://media.giphy.com/media/fYSnHlufseco8Fh93Z/giphy.gif" width="30">

</br>📑 Tài liệu yêu cầu
</br>📎 https://drive.google.com/file/d/1CSNZ0j5kiMHLyDXOxk1UHgETDVAHx6eP/view 

## ⭐️ 1. Tiến hành phân tích tất cả các ca sử dụng còn lại trong hệ thống Payroll System 📈

### ⭐️ 1.1. Phân tích ca sử dụng Create Administrative Report 📑

#### 👉 Các lớp phân tích cho ca sử dụng Create Administrative Report:** 
- **Entity classes:** 
  + **Employee:** 

- **Boundary classes:** 
  + **CreateEmployeeBoundaryForm:**  

- **Control classes:** 
  + **CreateEmployeeController:**  

👉 **Sequence diagram cho ca sử dụng Create Employee:** 

<p align="center">
  <img src="" alt="Diagram">
</p>

👉 **Nhiệm vụ và các thuộc tính của các lớp phân tích:** 
- **Employee (Entity):**
  + Các thuộc tính:
    - `empID`: ID của nhân viên.
    - `name`: Tên nhân viên.
    - 
  + Các phương thức:
    - 

- **CreateEmployeeBoundaryForm (Boundary):**  
  + Các phương thức:
    - 

- **CreateEmployeeController (Control):**  
  + Các phương thức:
    - 

👉 **Xác định quan hệ giữa các lớp phân tích:** 
- 

👉 **Class diagram mô tả các lớp phân tích và giải thích:** 

<p align="center">
  <img src="" alt="Diagram">
</p>

- **Giải thích:** 
  + <i> CreateEmployeeBoundaryForm: </i> 

  + <i> CreateEmployeeController: </i> 

  + <i> Employee: </i> 
  
## ⭐️ 1.2 Phân tích ca sử dụng Create Employee Report 📇

#### 👉 Các lớp phân tích cho ca sử dụng Create Employee Report:
- **Entity classes:** 
  + 

- **Boundary classes:** 
  + **TimecardBoundaryForm:**  

- **Control classes:** 
  + **TimecardController:**  

👉 **Sequence diagram cho ca sử dụng Create Employee Report:** 

<p align="center">
  <img src="" alt="Diagram">
</p>

👉 **Nhiệm vụ và các thuộc tính của các lớp phân tích:** 
- **Employee (Entity):**  
  + Các thuộc tính:
    - 
  + Các phương thức:
    - 

- **Timecard (Entity):**  
  + Các thuộc tính:
    - 

- **Project (Entity):**  
  + Các thuộc tính:
    - 
 
- **TimecardBoundaryForm (Boundary):**  
  + Các phương thức:
    - 

- **TimecardController (Control):**  
  + Các phương thức:
    - 
      
👉 **Xác định quan hệ giữa các lớp phân tích:** 
- 

👉 **Class diagram mô tả các lớp phân tích và giải thích:** 

<p align="center">
  <img src="" alt="Diagram">
</p>

- **Giải thích:** 
  + <i> TimecardBoundaryForm: </i> 

  + <i> TimecardController: </i> 

  + <i> Timecard: </i> 

  + <i> Project: </i> 

## ⭐️ 1.7 Hợp nhất kết quả phân tích 📁

👉 **Hợp nhất các lớp phân tích:** 
- **Lớp chung:** 
  + 
- **Điểm hợp nhất:** 
  + 


- 

<p align="center">
  <img src="" alt="Diagram">
</p>






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

#### ⭐️ <i> From [Trần Thị Thanh Kiều](https://github.com/tukieef-nah) - 4451051111 </i> 💙
