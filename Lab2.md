
# 🐳 Bài thực hành Lab1 <img src="https://media.giphy.com/media/fYSnHlufseco8Fh93Z/giphy.gif" width="30">

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

    public Employee(String empID, String name, int maxHours, String username, String password) {
        this.empID = empID;
        this.name = name;
        this.maxHours = maxHours;
        this.username = username;
        this.password = password;
        this.currentTimecard = new Timecard(empID); // Khởi tạo timecard hiện tại cho nhân viên
    }

    public Timecard getCurrentTimecard() {
        return currentTimecard;
    }

    public boolean canWorkMoreHours(int hours) {
        return currentTimecard.getTotalHours() + hours <= maxHours;
    }
}
```

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

#### 👉 Class Entity của Project
```
package Lab2;

public class Project {
	private String projectID;
    private String projectName;
    private String chargeNumber;

    public Project(String projectID, String projectName, String chargeNumber) {
        this.setProjectID(projectID);
        this.setProjectName(projectName);
        this.chargeNumber = chargeNumber;
    }

    public String getChargeNumber() {
        return chargeNumber;
    }

	public String getProjectName() {
		return projectName;
	}

	public void setProjectName(String projectName) {
		this.projectName = projectName;
	}

	public String getProjectID() {
		return projectID;
	}

	public void setProjectID(String projectID) {
		this.projectID = projectID;
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
        // Assume projects are loaded into projectDatabase from some external source
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


#### ⭐️ <i> From [Trần Thị Thanh Kiều](https://github.com/tukieef-nah) - 4451051111 </i> 💙
