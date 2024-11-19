# 🐳 Bài thực hành Lab4 <img src="https://media.giphy.com/media/fYSnHlufseco8Fh93Z/giphy.gif" width="30">
#### 📖 Mục đích 📝
Thiết kế các ca sử dụng cho hệ thống "Payroll System" dựa vào kết quả phân tích ca sử dụng và các phần tử thiết kế (cho trong file đính kèm).
</br>📑 File đính kèm
</br>📎 https://drive.google.com/file/d/1iEzKHthBh7MzLOhVgudpa_aXpL4LreCc/view
</br>📎 https://drive.google.com/file/d/17KDqTyZMsdNrgZlmMPAVKjA6kZWxqzCW/view

## ⭐️ 1. Describe interaction among design objects 📈

### 👉 Xác định các đối tượng tham gia và cách chúng tương tác với nhau trong từng ca sử dụng.

#### Trong Payroll System, sự tương tác giữa các đối tượng thiết kế có thể được mô tả như sau:
- `Employee` tương tác với hệ thống bằng cách gửi thông tin về giờ làm việc (qua `Timecard`) và các dữ liệu liên quan khác. Dữ liệu của `Employee` được thu thập và lưu trữ trong cơ sở dữ liệu để tính toán thêm.
- Đối tượng `Timecard` lưu trữ thông tin về số giờ làm việc của nhân viên và được gửi qua `TimecardForm`. `TimecardForm` giao tiếp với `TimecardController` , nơi xác minh và cập nhật dữ liệu `Timecard`.
- `TimecardController` phối hợp giữa `Timecard`, `Employee` và `ProjectManagementDatabase`. Nó lấy `charge codes` và cập nhật `Timecard` với số giờ làm việc chính xác cho từng `Project`. Nó cũng đảm bảo rằng tổng số giờ nằm ​​trong giới hạn cho phép.
- Khi đến lúc xử lý `payroll`(bảng lương), `PayRollController` tương tác với các lớp con `Employee` (`HourlyEmployee` , `SalariedEmployee`, `CommissionedEmployee`) để tính lương dựa trên số giờ làm việc và mức lương. Sau đó, `PayRollController` phối hợp với `BankSystem` để xử lý thanh toán và `PrinterInterface` để tạo `Paycheck`.
- Đối tượng `Paycheck` được bộ điều khiển tạo ra (dựa trên loại `Employee`) và `SystemClockInterface` xác định thời điểm trả lương, kích hoạt sự kiện xử lý `Payroll`.

## ⭐️ 2. Simplify sequence diagrams using subsystems 🔬

### 👉 Để đơn giản hóa sequence diagrams, chúng ta có thể nhóm các thành phần liên quan thành các subsystem:

#### Payroll Calculation Subsystem - Hệ thống tính lương:
- `PayRollController`: Quản lý việc tính toán lương
- `Employee Subclasses` (`HourlyEmployee` , `SalariedEmployee`, `CommissionedEmployee`): Đại diện cho các loại nhân viên khác nhau.
- `Paycheck`: Thể hiện chi tiết tiền lương sau khi tính toán.

#### Timecard Subsystem - Hệ thống thẻ chấm công:
- `TimecardController`: Quản lý việc gửi và xác thực dữ liệu thẻ chấm công.
- `Timecard`: Chứa dữ liệu về số giờ làm việc.
- `ProjectManagementDatabase`: Lưu trữ `charge codes` liên quan đến `Project`.

#### Payment Subsystem - Hệ thống thanh toán:
- `BankSystem`: Xử lý các giao dịch gửi tiền trực tiếp.
- `PrinterInterface`: In `Paycheck` cho những nhân viên được trả lương thông qua check.

#### System Management Subsystem - Hệ thống quản lý hệ thống con:
- `SystemClockInterface`: Xử lý các hành động theo thời gian, chẳng hạn như tính lương vào ngày trả lương.

### 👉 Sequence diagrams đã được đơn giản hóa:
#### Sequence diagrams của ca sử dụng Select Payment Mebthod
<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/V5D1ReCm4BppYlr0F-135HLIjOTAKHArvutP41TZHsiJYRVrq2Vr2pKGC92q78nOp-pEpYu_Nzyhvv5zNUd4bSe0MqT9Wj9RXdLrrhOXIWwsDZbo0tjLaKJEdorNYRJ6izLZCEs_DN52nYiVuIDqWyqs86wHuKAUI9Qnr1EQSjSuJrMCRLWPJ_pQ7aUKDERjWQcsieoNIS6sFeyYO5SVN9yGmZCq1m-FixO4hDiCy69hTl1XkQIy8qn1Kr9iHhGbAkLZtrDUn4tP0jvHgnmz0PgW4I_q3sl3zfEaVqE31LN1kmmz7j2HW2rvLdGXI4_8HNZPd5omDnzy21QtYI15BMkDNbcpiEIUYrtLvTG4x5aLHT1qJThHRs3pFaU1DyxU9Gxp4QDWQe5_4uOL2WIcAxhVgRa9hMsBnk_cYmieMjybEJVGErAyNyYrvgZ2YcIAmwWWexDrol-ZUx7Keez4-Hrp0PgNp4YhIp-DsF4g7Erl_Gi00F__0m00" alt="Diagram">
</p>

#### Sequence diagrams của ca sử dụng Maintain Timecard
<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/b9DDRi8m48NtFiM8VI_0ea9AgRefHQKzmDGPY8N_DED0SxOkUgHUeGuK0WGGpIePp_Syxzdv-VeUIK9EjRDAoT9uu22a5EeK6COksj0G0GgGYohcJgDDH9zWy6OSQUGIPlM7D9B83Tg-NNbVFQQcs72m5WgqkhQOJF0d0dyTbtb7-QN7jDKBp6nJWsVqkA0pz7QzWrNs2dVtVIimX9T8Vhy0Zu6TwhTbzjH5HbyfiQ4LGL4pjrFim1otxRvW_6aaYOByd9Lkfnl2Wv5eiUcBaHM22QqxmO894vMtAXwobvap1cUuEjvPaI-lfZdsYHYUGiq2ytpXYWfvaGCA9SdDkRx7CjlhxAvDghQQL_VUJBkVz5yUjpkM1mTuUW6xL2SXcNdJIkcAz1Ac73I9vEDGennF--Fz0W00__y30000" alt="Diagram">
</p>

#### Sequence diagrams của ca sử dụng Run Payroll
<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/d9HDJiCm48NtFiMe6rPS859HeKMeYwAATey6UrAiEdQmdKev6mkEn1MmqwHj4bS8ieYIoNppy_oKxy-lcVDeVLKenjnUQh364MF8lR6mgPsdudMk3D-teSUYLAOc0dH0HSbO6MZ9POdQmsIDjJLAmHmLhnHwQJHigZVNr9b4fiqu1VlyLXR4qOe1r8MlKA5cGU5Xr2b6hp37rM256dUKe8_Vpp2RJc4JbUesWBKrd9o3wPHTwWItTqCOiZJAXda17UeJsAsLknrPI8ZBs2W_r3YTKGRpTmeZoHoalt5GOYsmPgVlwNvXkeCKT58TK8kO1qkTcsJ3qVc4AY_ahQJ3HPa5UcJZrFGG0Q-i7i2_RjigGx5YCZd4U2D91a-aoRQvJIouNldEDh0Y_sv41WjfYNjOK6cSz0p2TQLmpstD2XyLEGyFgFT7xI8y47y8TU8tq88yIkMwfltSguVNk78mDYb7ezNMLeQtnYB_sMiLPfDw1_T2sEZcFsoNGfCBnWd9BkCjHqxG7vgqQ3mnuYuyyMoypElpmRS2aM2pWCV_tWy0003__mC0" alt="Diagram">
</p>

## ⭐️ 3. Describe persistence-related behavior 📑

### 👉 Các hành vi persistence-related của hệ thống có thể được mô tả bằng cách tập trung vào cách dữ liệu được lưu trữ và truy xuất:

#### Các lớp liên quan đến persistence:
- `Employee`: Lưu thông tin cơ bản (tên, địa chỉ, phương thức thanh toán).
- `Timecard`: Lưu dữ liệu giờ làm của nhân viên tính theo giờ.
- Đối tượng `Employee` và `Timecard` phải được lưu trữ liên tục trong cơ sở dữ liệu. Mỗi đối tượng `Employee` có một mã định danh duy nhất (`empID`), và các `timecard` liên quan của chúng được lưu trữ trong một bảng riêng được liên kết bởi `empID`.
- `PurchaseOrder`: Lưu đơn đặt hàng của nhân viên hoa hồng.
- `Paycheck`: Lưu thông tin paycheck đã được tạo.
- Thông tin `Project` được lưu trữ trong một bảng riêng và liên quan đến `Timecard` thông qua `charge codes`.

#### Hành vi lưu trữ:
- Khi `Timecard` được gửi bởi nhân viên, hệ thống sẽ lưu số giờ làm việc , số tiền công và trạng thái (`draft`/`submitted`) vào cơ sở dữ liệu, đảm bảo tính nhất quán của dữ liệu.
- Sau khi tạo `Paycheck`, hệ thống lưu thông tin `Paycheck` vào lịch sử giao dịch.
- Thông tin chi tiết về nhân viên như phương thức thanh toán, thông tin ngân hàng và mức lương được cập nhật thường xuyên và những thay đổi sẽ được lưu trong hệ thống để phản ánh tình trạng hiện tại của nhân viên.

## ⭐️ 4. Refine the flow of events description 📇

### 👉 Luồng sự kiện trong Hệ thống tính lương có thể được tinh chỉnh, làm mịn thành các bước sau:

#### Maintain Timecard:
- Nhân viên truy cập vào `TimecardForm`.
- `TimecardForm` thu thập số giờ làm việc và hiển thị `timecard` hiện tại.
- `TimecardController` xác thực `timecard` và cập nhật hồ sơ của nhân viên .
- Nếu `timecard` đã hoàn tất, nhân viên sẽ nộp thẻ. `TimecardController` sẽ cập nhật trạng thái của `timecard` (từ `draft` thành `submitted`).

#### Run Payroll:
- `SystemClockInterface` kích hoạt tính lương vào thời điểm được chỉ định: (`payday`)
- `PayRollController` tính toán mức lương dựa trên loại nhân viên:
  + `HourlyEmployee`: Sử dụng số giờ làm việc và mức lương theo giờ.
  + `SalariedEmployee`: Sử dụng mức lương hàng năm và các khoản khấu trừ áp dụng.
  + `CommissionedEmployee`: Tính lương dựa trên doanh số hoặc hoa hồng.
- `BankSystem` xử lý các khoản thanh toán gửi tiền trực tiếp, trong khi `PrinterInterface` tạo ra các `paychecks` trả lương cho những nhân viên không sử dụng dịch vụ gửi tiền trực tiếp (`direct deposit`).
- `Paycheck` được tạo và xử lý (in hoặc gửi).

## ⭐️ 5. Unify classes and subsystems 📁

### 👉 Để thống nhất các lớp và hệ thống con, chúng ta có thể thực hiện các bước sau:

#### Employee Subsystem:
- Kết hợp `HourlyEmployee` , `SalariedEmployee` và `CommissionedEmployee` thành một lớp `Employee` thống nhất với hành vi đa hình để tính lương. Điều này làm giảm sự trùng lặp và hợp lý hóa quy trình tính lương.

#### Timecard and Project Subsystem:
- Thay vì có lớp `ProjectManagementDatabase` riêng , hãy tích hợp `charge codes` vào thực thể `Timecard` , liên kết mỗi `timecard` với một `project` hoặc `charge codes` cụ thể.

#### Paycheck and Payroll Subsystem:
- Hợp nhất việc tạo và phân phối tiền lương thành một lớp `Paycheck` duy nhất có thể xử lý mọi loại nhân viên và phương thức thanh toán (direct deposit hoặc check).

#### Payment System:
- Sử dụng `BankSystem` và `PrinterInterface` trong `PaymentProcessingSubsystem` thống nhất để quản lý cả quy trình gửi tiền trực tiếp và in tiền lương.

### 👉 Sơ đồ tổng hợp: Kết hợp các lớp và subsystem vào sơ đồ lớp tổng thể như sau:
<p align="center">
  <img src="https://www.planttext.com/api/plantuml/png/X5LBRjim4Dtx58HNzi8N28eYXLsqNYG8ug9T55tGr4HYpO_0JrAXzScww95wXGubcVgGSRKHC9_7DsyUfR-__znQHutpKYpiYIjYj8N5egRiH4iWo_Uo5he180T_j8rr89VavuBWGu_M6SeSOO9QIs9XbmtF1cIztv4RmfKRWefAmDZ16QxA8SoyCQ3S9ow1KLEa1PB--AYziJCuRy44oBIXHbelEWTLqqRYMNVWAbsaN4W9RZkbireFMKRL5srETzf0IsXLHLgJAi6ye0uUQBDQuo5FGjEEztdHlZhT0eHeCkgHgiqy8iIaE-PiO075ID_p2FT01JKSYXmoLSfJqLOqCsO3m5PBoQtbMkL1MCpdALegmERcZc1lVcqsi_ap1VD1CYKvgelpoCMNDUBa1Nam-ZkWRnD7TtF7sj6iheybRXulukktUP9Lr9Hmx-KHZ6tJSwVXtNFUPXBFLF02THqRp_gZvAwFJ4nq6Mb4kUv2AUC-SPzSmnunph_Pl8t0DsJv3WKkKM3Yz7AwWr0Okx3oqFAqoyaAy1gm2jYfMm5jZ1RYjHN4sl4yVImTY4hjbKiDM882CqWu5QmZiDNAXJUOYRCdLpS5lD2pK-J8EkWHnK4zzjRwaMxfsVE6Hy2jm3EqFCbUFMaZgKDxNmCOR-1pxvxkys99Pz1htP4yTd_evqmt6BwQv93VMCYXNHYWJrGPDplpP4Zlk45FxQ3M5kqCm-0N3TRZ5jprXTphjRaLNE64G_PXtCkn-OymLr2s6dymNBLIlt1N1SLkGHNXT_eF003__mC0" alt="Diagram">
</p>

#### ⭐️ <i> From [Trần Thị Thanh Kiều](https://github.com/tukieef-nah) - 4451051111 </i> 💙
