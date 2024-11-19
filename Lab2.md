## Bài thực hành Lab2.md  
### Phân tích các ca sử dụng còn lại của hệ thống Payroll System 
**1.Create Administrative Report**    
**Xác định các lớp phân tích:**  
**1.1. PayrollAdministrator (Người quản trị tiền lương)**  
- Thuộc tính:  
adminID: ID của người quản trị.  
nameAdmin: Tên của người quản trị.  
loGin: Trạng thái đăng nhập.  
- Quan hệ: Có quyền thực hiện thao tác trên Report.   

**1.2. Report (Báo cáo)**  
- Thuộc tính:  
reportType: Loại báo cáo (Tổng số giờ làm việc hoặc Lương năm đến ngày).  
startDate: Ngày bắt đầu của báo cáo.  
endDate: Ngày kết thúc của báo cáo.  
nameEmployee: Danh sách tên nhân viên.  
reportContent: Nội dung chi tiết của báo cáo.  
- Quan hệ:  
Phụ thuộc vào yêu cầu từ PayrollAdministrator để tạo và lưu báo cáo.  

**1.3. ReportSystem (Hệ thống báo cáo)**  
- Phương thức:  
generateReport(criteria): Tạo báo cáo dựa trên tiêu chí do người dùng cung cấp.  
saveReport(report, location): Lưu báo cáo vào một vị trí cụ thể.  
validateReportCriteria(criteria): Xác minh thông tin đầu vào cho báo cáo.   
- Quan hệ:  
Tương tác với PayrollAdministrator để nhận yêu cầu.  
Xử lý dữ liệu và quản lý Report.  

**Biểu đồ lớp (Class Diagram)**  
- PayrollAdministrator tương tác với ReportSystem để yêu cầu tạo và lưu báo cáo.  
- ReportSystem quản lý dữ liệu và xác minh tiêu chí trước khi tạo Report.  
- Report lưu trữ chi tiết báo cáo được tạo.   

**Nhiệm vụ của từng lớp:**  
- PayrollAdministrator:  
Yêu cầu hệ thống tạo và lưu báo cáo.  
Cung cấp thông tin đầu vào cần thiết (loại báo cáo, ngày tháng, danh sách nhân viên).  
- Report:  
Lưu trữ thông tin của báo cáo được tạo.  
- ReportSystem:  
Thực hiện logic để tạo báo cáo dựa trên đầu vào.  
Xử lý và lưu trữ báo cáo theo yêu cầu.  

**Sơ đồ lớp**  
Code:
```  
@startuml  
class PayrollAdministrator {  
    - adminID: String  
    - nameAdmin: String  
    - loGin: Boolean  
    --  
    + requestReport(criteria: String): void  
}  
  
class Report {  
    - reportType: String  
    - startDate: Date  
    - endDate: Date  
    - nameEmployee: List<String>  
    - reportContent: String  
}  
  
class ReportSystem {  
    + generateReport(criteria: String): Report  
    + saveReport(report: Report, location: String): void  
    + validateReportCriteria(criteria: String): Boolean  
}  
  
PayrollAdministrator --> ReportSystem : "Yêu cầu tạo/lưu báo cáo"  
ReportSystem --> Report : "Quản lý và tạo báo cáo"  
@enduml
```  
Link sơ đồ:  https://www.planttext.com/api/plantuml/png/T5B1IiGm4BttAuOzALYy5rbMTqK43-fwyHZROGcaIKscXIB-Yui7mPFdYdWe-1_x1Vw2QPFMRLrpICYRUVFUJFBz_Zapn3JbgGXYmOo1IrPg9SHnadB93Mb6IiD307Q5m1hqV171aZINAuzAbcARFyA5Eckm4wK4Ckd0i3q0DDxdQEWQCwLfBzQSK7FM5TYFe50y2Hu3xyhbzJvqUxqfCnn9jiqi65cysJsAClc3DQPFqqoe4ctWmhPwv2fD1nfp9GabzJ8ZHylI4ARU5y0A9Tg9uVzjkOXFDwpeKfrQ5p-miuiPSIN74t74WWcUz3fpBxDBhnk-zRtpPSDmEcmbWibj_Pf3lAbUSg1DjLQ7ukijXxjwhI2ssoGO47uhDDohV5CzIn3r1nJra-DlKsVsBPhFzWC00F__0m00  

Sơ đồ:  
![Diagram](https://www.planttext.com/api/plantuml/png/T5B1IiGm4BttAuOzALYy5rbMTqK43-fwyHZROGcaIKscXIB-Yui7mPFdYdWe-1_x1Vw2QPFMRLrpICYRUVFUJFBz_Zapn3JbgGXYmOo1IrPg9SHnadB93Mb6IiD307Q5m1hqV171aZINAuzAbcARFyA5Eckm4wK4Ckd0i3q0DDxdQEWQCwLfBzQSK7FM5TYFe50y2Hu3xyhbzJvqUxqfCnn9jiqi65cysJsAClc3DQPFqqoe4ctWmhPwv2fD1nfp9GabzJ8ZHylI4ARU5y0A9Tg9uVzjkOXFDwpeKfrQ5p-miuiPSIN74t74WWcUz3fpBxDBhnk-zRtpPSDmEcmbWibj_Pf3lAbUSg1DjLQ7ukijXxjwhI2ssoGO47uhDDohV5CzIn3r1nJra-DlKsVsBPhFzWC00F__0m00)  
  
**2.Create Employee Report**  
**Xác định các lớp phân tích:**  
**2.1. Employee (Nhân viên)**    
- Thuộc tính:  
employeeID: ID của nhân viên.  
nameEmployee: Tên nhân viên.  
loGin: Trạng thái đăng nhập.    
- Quan hệ: Tương tác với ReportSystem để yêu cầu tạo và lưu báo cáo.  

**2.2. Report (Báo cáo)**  
- Thuộc tính:
reportType: Loại báo cáo (Tổng số giờ làm việc, Tổng số giờ làm việc cho dự án, Nghỉ phép/ốm, hoặc Lương năm đến ngày).  
startDate: Ngày bắt đầu của báo cáo.  
endDate: Ngày kết thúc của báo cáo.  
chargeNumber: Mã công việc (nếu báo cáo là cho dự án).  
reportContent: Nội dung chi tiết của báo cáo.  
- Quan hệ: Được tạo và quản lý bởi ReportSystem dựa trên yêu cầu từ Employee.  

**2.3. ReportSystem (Hệ thống báo cáo)**  
- Phương thức:  
generateReport(criteria): Tạo báo cáo dựa trên tiêu chí do nhân viên cung cấp.  
saveReport(report, location): Lưu báo cáo vào một vị trí cụ thể.  
valIn(criteria): Xác minh thông tin đầu vào cho báo cáo.  
passJob(): Lấy danh sách mã công việc từ cơ sở dữ liệu quản lý dự án (chỉ áp dụng cho báo cáo dự án).  
- Quan hệ:  
Tương tác với Employee để nhận yêu cầu.  
Xử lý dữ liệu và quản lý Report.  

**Biểu đồ lớp (Class Diagram)**
- Employee tương tác với ReportSystem để yêu cầu tạo và lưu báo cáo.  
- ReportSystem quản lý dữ liệu và xác minh tiêu chí trước khi tạo Report.  
- Report lưu trữ thông tin của báo cáo được tạo.  
- ReportSystem có thể lấy thông tin từ cơ sở dữ liệu quản lý dự án để cung cấp danh sách mã công việc.  

**Nhiệm vụ của từng lớp:**  
- Employee:  
Yêu cầu hệ thống tạo và lưu báo cáo.  
Cung cấp thông tin đầu vào cần thiết (loại báo cáo, ngày tháng, mã công việc nếu cần).  
- Report:  
Lưu trữ thông tin của báo cáo được tạo.  
- ReportSystem:  
Thực hiện logic để tạo báo cáo dựa trên đầu vào.  
Xử lý và lưu trữ báo cáo theo yêu cầu.  
Kết nối với cơ sở dữ liệu để lấy danh sách mã công việc khi cần.  

**Sơ đồ lớp**  
Code:
```  
@startuml
class Employee {
    - employeeID: String
    - nameEmployee: String
    - loGin: Boolean
    --
    + requestReport(criteria: String, reportSystem: ReportSystem): void
}

class Report {
    - reportType: String
    - startDate: Date
    - endDate: Date
    - chargeNumber: String
    - reportContent: String
    --
    + getReportDetails(): String
}

class ReportSystem {
    + generateReport(criteria: String): Report
    + saveReport(report: Report, location: String): void
    + valIn(criteria: String): Boolean
    + passJob(): List<String>
}

Employee --> ReportSystem : "Yêu cầu tạo/lưu báo cáo"
ReportSystem --> Report : "Quản lý và tạo báo cáo"
ReportSystem --> Database : "Truy vấn mã công việc"
@enduml  
```  
Link sơ đồ:  https://www.planttext.com/api/plantuml/png/V5BBIiD05DtdAovTjT3WFaWfMf6A2BRTk9oabpWmcQapaq0Gr_w6fOZWoeMh574Hy3_o1Vw2Cvsajl6HnOIvvvx3EVVEv_fzg3IHEasO5p6Y59ma2oPoHBZrm7m-O5qOZmAOQabvN0ES9DXqjo0cJYaFu4W8XeIxeh_v0KYyIL7f2Iw4rDr8KesIaaQWRt0BJ7EbCGbWidFh1P09ElVklDgh0xTE7NEMBzfsDX57H9kwFPjWVFwZ5bqJ6UD5ceGeMo9E_LXmZLplOqsq6EjO8zI4CjNjRVjQdbsWshabSfJ6nHz3wJLpgDiLoPfMvwh1-sRo4T5Ky1tgPcQEc14svh_9xsuAO66CdedGsZ-dIX-wje4DiNqUlZ_Opn90vwfyJY6gYgSKT5KinG7xU4aXB9S28dDql3t2juBbNgPLiUB0oZV8oWV7_vTgjaP2ej2IPpBD8QkAHmv9kJACLnv3HglrVTJnXcRHzdr_0G00__y30000  
Sơ đồ:  
![Diagram](https://www.planttext.com/api/plantuml/png/V5BBIiD05DtdAovTjT3WFaWfMf6A2BRTk9oabpWmcQapaq0Gr_w6fOZWoeMh574Hy3_o1Vw2Cvsajl6HnOIvvvx3EVVEv_fzg3IHEasO5p6Y59ma2oPoHBZrm7m-O5qOZmAOQabvN0ES9DXqjo0cJYaFu4W8XeIxeh_v0KYyIL7f2Iw4rDr8KesIaaQWRt0BJ7EbCGbWidFh1P09ElVklDgh0xTE7NEMBzfsDX57H9kwFPjWVFwZ5bqJ6UD5ceGeMo9E_LXmZLplOqsq6EjO8zI4CjNjRVjQdbsWshabSfJ6nHz3wJLpgDiLoPfMvwh1-sRo4T5Ky1tgPcQEc14svh_9xsuAO66CdedGsZ-dIX-wje4DiNqUlZ_Opn90vwfyJY6gYgSKT5KinG7xU4aXB9S28dDql3t2juBbNgPLiUB0oZV8oWV7_vTgjaP2ej2IPpBD8QkAHmv9kJACLnv3HglrVTJnXcRHzdr_0G00__y30000)    

**3.Login**  
**Xác định các lớp phân tích:**  
**3.1. Actor (Người dùng)**  
- Thuộc tính:  
actorID: ID của người dùng.  
username: Tên đăng nhập.  
password: Mật khẩu.  
loGin: Trạng thái đăng nhập.  
- Quan hệ: Tương tác với LoginSystem để thực hiện quá trình đăng nhập.

**3.2. LoginSystem (Hệ thống đăng nhập)**  
- Phương thức:  
valIn(username, password): Xác minh thông tin tên đăng nhập và mật khẩu.  
loginActor(actor): Đăng nhập người dùng nếu thông tin xác thực hợp lệ.  
- Quan hệ: Quản lý xác thực và đăng nhập cho Actor.  

**Biểu đồ lớp (Class Diagram)**  
Actor tương tác với LoginSystem để yêu cầu xác thực.  
LoginSystem xử lý logic để xác minh thông tin đăng nhập và cập nhật trạng thái của Actor.  

**Nhiệm vụ của từng lớp:**  
- Actor:  
Cung cấp tên đăng nhập và mật khẩu.  
Thực hiện hành động đăng nhập.  
- LoginSystem:  
Xử lý xác thực thông tin đăng nhập.  
Quản lý trạng thái đăng nhập (thành công hoặc thất bại).    

**Sơ đồ lớp**  
Code:
```  
@startuml
class Actor {
    - actorID: String
    - username: String
    - password: String
    - loGin: Boolean
    --
    + performLogin(loginSystem: LoginSystem): void
}

class LoginSystem {
    + valIn(username: String, password: String): Boolean
    + loginActor(actor: Actor): void
}

Actor --> LoginSystem : "Yêu cầu xác thực"
LoginSystem --> Actor : "Cập nhật trạng thái đăng nhập"
@enduml
```  
Link sơ đồ:  https://www.planttext.com/api/plantuml/png/P54zQiCm5DvrYWzF3jGNq13I7oY1R9ao2bbr3B9a93bjAPrwWXx1Kw7GeQipT70kuXFq2fLbGnr7WnxVz_Izzxsdt-FFoZfcN5L8mYMp5jVSQOCN0dyIi1wjxoYspkGg6zdA2gDO8MPqwVMFsgGpMkhxN57SQ2q5KmEPX02KmZneKsnqbgjOzlVssJfHK6p-mOBYeFEKl9BHuoGtEWKEJAvLF7TsTM5gSUu425t3r76ObWuhc3GTLf8aoxF65D6k_Qp0k-QZmbDRSxXzT_pc4Pa-wsL30I-uxPgl4chlWuCpNLEhpAlQEiVf_VJcGSYL4La9bVQVyWS00F__0m00  

Sơ đồ:  
![Diagram](https://www.planttext.com/api/plantuml/png/P54zQiCm5DvrYWzF3jGNq13I7oY1R9ao2bbr3B9a93bjAPrwWXx1Kw7GeQipT70kuXFq2fLbGnr7WnxVz_Izzxsdt-FFoZfcN5L8mYMp5jVSQOCN0dyIi1wjxoYspkGg6zdA2gDO8MPqwVMFsgGpMkhxN57SQ2q5KmEPX02KmZneKsnqbgjOzlVssJfHK6p-mOBYeFEKl9BHuoGtEWKEJAvLF7TsTM5gSUu425t3r76ObWuhc3GTLf8aoxF65D6k_Qp0k-QZmbDRSxXzT_pc4Pa-wsL30I-uxPgl4chlWuCpNLEhpAlQEiVf_VJcGSYL4La9bVQVyWS00F__0m00)   

**4.Maintain Employee Information**  
**Xác định các lớp phân tích:**  
**4.1. PayrollAdministrator (Người quản trị tiền lương)**  
- Thuộc tính:  
adminID: ID của người quản trị.  
username: Tên đăng nhập của người quản trị.  
loGin: Trạng thái đăng nhập.  
- Quan hệ: Tương tác với EmployeeManagementSystem để thêm, cập nhật hoặc xóa thông tin nhân viên.  

**4.2. Employee (Nhân viên)**  
- Thuộc tính:  
employeeID: ID duy nhất của nhân viên.  
nameEmployee: Tên nhân viên.  
employeeType: Loại nhân viên (giờ, lương cố định, hoa hồng).  
mailingAddress: Địa chỉ gửi thư của nhân viên.  
socialSecurityNumber: Số an sinh xã hội của nhân viên.  
standardTaxDeductions: Các khoản khấu trừ thuế tiêu chuẩn.  
otherDeductions: Các khoản khấu trừ khác (401k, bảo hiểm y tế).  
phoneNumber: Số điện thoại liên lạc.  
hourlyRate: Mức lương theo giờ (áp dụng cho nhân viên làm việc theo giờ).  
salary: Lương cố định (áp dụng cho nhân viên lương cố định và hoa hồng).  
rate: Tỷ lệ hoa hồng (áp dụng cho nhân viên hoa hồng).  
hourLimit: Giới hạn giờ làm việc (nếu có).  
paycheckMethod: Phương thức nhận phiếu lương (mặc định: "pickup").    
- Quan hệ: PayrollAdministrator quản lý thông qua hệ thống EmployeeManagementSystem.  

**4.3. EmployeeManagementSystem (Hệ thống quản lý nhân viên)**  
- Phương thức:  
addEmployee(employeeInfo): Thêm nhân viên mới vào hệ thống, tạo ID duy nhất và đặt phương thức nhận lương mặc định là "pickup".  
updateEmployee(employeeID, updatedInfo): Cập nhật thông tin của một nhân viên dựa trên employeeID.  
deleteEmployee(employeeID): Đánh dấu nhân viên để xóa, xử lý trả lương cuối cùng và xóa khỏi hệ thống.  
getEmployee(employeeID): Lấy thông tin nhân viên dựa trên employeeID.  
validateEmployeeID(employeeID): Kiểm tra xem ID nhân viên có tồn tại hay không.  
- Quan hệ:   
Tương tác với PayrollAdministrator để xử lý các yêu cầu về thông tin nhân viên.  
Quản lý thông tin của các đối tượng Employee.  

**Biểu đồ lớp (Class Diagram)**  
PayrollAdministrator tương tác với EmployeeManagementSystem để thêm, cập nhật hoặc xóa thông tin nhân viên.  
EmployeeManagementSystem xử lý logic và quản lý thông tin các đối tượng Employee.    

**Nhiệm vụ của từng lớp:**  
- PayrollAdministrator  
Gửi yêu cầu thêm, cập nhật hoặc xóa nhân viên.  
Cung cấp thông tin cần thiết để thực hiện các yêu cầu này.  
- Employee  
Lưu trữ thông tin chi tiết về nhân viên, bao gồm lương, loại nhân viên và các khấu trừ.  
- EmployeeManagementSystem  
Xử lý các thao tác thêm, cập nhật, xóa thông tin nhân viên.  
Đảm bảo dữ liệu nhân viên được quản lý chính xác và cập nhật trạng thái hệ thống sau mỗi thao tác.  

**Sơ đồ lớp**  
Code:
```  
@startuml
class PayrollAdministrator {
    - adminID: String
    - username: String
    - loGin: Boolean
    --
    + addEmployee(employeeInfo: Employee): void
    + updateEmployee(employeeID: String, updatedInfo: Employee): void
    + deleteEmployee(employeeID: String): void
}

class Employee {
    - employeeID: String
    - nameEmployee: String
    - employeeType: String
    - mailingAddress: String
    - socialSecurityNumber: String
    - standardTaxDeductions: Double
    - otherDeductions: Double
    - phoneNumber: String
    - hourlyRate: Double
    - salary: Double
    - rate: Double
    - hourLimit: Integer
    - paycheckMethod: String
}

class EmployeeManagementSystem {
    + addEmployee(employeeInfo: Employee): void
    + updateEmployee(employeeID: String, updatedInfo: Employee): void
    + deleteEmployee(employeeID: String): void
    + getEmployee(employeeID: String): Employee
    + validateEmployeeID(employeeID: String): Boolean
}

PayrollAdministrator --> EmployeeManagementSystem : "Gửi yêu cầu quản lý nhân viên"
EmployeeManagementSystem --> Employee : "Quản lý thông tin nhân viên"
@enduml
```  
Link sơ đồ:  https://www.planttext.com/api/plantuml/png/p5HDJjmm5DxFAPvO5QbpWImgG5EXaQ02XWiyujV4glqyjPz7MAYNAGia97PTWQekSf8vGQ_Gf3W3P7xMP9Fa-tlMbzX_d_uS144lqPfHQJ04ECFadJ67ochMGJoAyt0pWlOQ0tReT5B0JBpcAgCna6UqD82DEzPSm95pXf2VmV7_6xH1whET6vU8Fb1-cF9NLq0FxnUmS5fbVPmh55gth9RoCKlKhXH5XdQczF8Vezn6hrqriEx9H5T0hnvGlUSopOUKHMtQjqEbF8Km88ChDPePbT5hIL-YlI8_b0YoGgykyNf2AfQY7RSn4nUl36MDavhyLdPUEwQDsRMBtgIBjjI19Q11dmQWNzTr0IVQQYbWoa8L-NucfhAcyjifIUtKQknQwwV8M94bbbaAGZP_XNV_-ppBAvBTsfxD-WKQ_NgPqybcMx-XshesRjRn-DFs1WlOEru-FMX8pNs4Slbu5-5xN3xUCfZcDt3T_6HOwEQUzqPRGrvFw1BFNmAaRdvn1QBvRTO1iUeEcNy0003__mC0  

Sơ đồ:  
![Diagram](https://www.planttext.com/api/plantuml/png/p5HDJjmm5DxFAPvO5QbpWImgG5EXaQ02XWiyujV4glqyjPz7MAYNAGia97PTWQekSf8vGQ_Gf3W3P7xMP9Fa-tlMbzX_d_uS144lqPfHQJ04ECFadJ67ochMGJoAyt0pWlOQ0tReT5B0JBpcAgCna6UqD82DEzPSm95pXf2VmV7_6xH1whET6vU8Fb1-cF9NLq0FxnUmS5fbVPmh55gth9RoCKlKhXH5XdQczF8Vezn6hrqriEx9H5T0hnvGlUSopOUKHMtQjqEbF8Km88ChDPePbT5hIL-YlI8_b0YoGgykyNf2AfQY7RSn4nUl36MDavhyLdPUEwQDsRMBtgIBjjI19Q11dmQWNzTr0IVQQYbWoa8L-NucfhAcyjifIUtKQknQwwV8M94bbbaAGZP_XNV_-ppBAvBTsfxD-WKQ_NgPqybcMx-XshesRjRn-DFs1WlOEru-FMX8pNs4Slbu5-5xN3xUCfZcDt3T_6HOwEQUzqPRGrvFw1BFNmAaRdvn1QBvRTO1iUeEcNy0003__mC0)  

**5.Maintain Purchase Order**  
**Xác định các lớp phân tích:**  
**5.1. CommissionedEmployee (Nhân viên hoa hồng)**  
- Thuộc tính:  
employeeID: ID của nhân viên hoa hồng.  
nameEmployee: Tên nhân viên.  
commissionRate: Tỷ lệ hoa hồng của nhân viên.  
loGin: Trạng thái đăng nhập.  
- Quan hệ:  
Tương tác với PurchaseOrderSystem để thêm, cập nhật, hoặc xóa đơn đặt hàng.  
Chỉ được phép thao tác trên các đơn đặt hàng do chính mình tạo.  

**5.2. PurchaseOrder (Đơn đặt hàng)**  
- Thuộc tính:  
purchaseOrderID: ID duy nhất của đơn đặt hàng (hệ thống tạo).  
customerContact: Thông tin liên hệ của khách hàng.  
billingAddress: Địa chỉ thanh toán của khách hàng.  
productList: Danh sách các sản phẩm trong đơn đặt hàng.  
orderDate: Ngày tạo đơn đặt hàng.  
status: Trạng thái của đơn đặt hàng (mở hoặc đã đóng).  
- Quan hệ:    
Được tạo, cập nhật hoặc xóa bởi CommissionedEmployee thông qua PurchaseOrderSystem.  

**5.3. PurchaseOrderSystem (Hệ thống quản lý đơn đặt hàng)**  
- Phương thức:  
createPurchaseOrder(orderInfo): Tạo đơn đặt hàng mới, tự động tạo purchaseOrderID và lưu trữ vào hệ thống.  
updatePurchaseOrder(purchaseOrderID, updatedInfo): Cập nhật thông tin của một đơn đặt hàng mở.  
deletePurchaseOrder(purchaseOrderID): Xóa một đơn đặt hàng mở khỏi hệ thống.  
getPurchaseOrder(purchaseOrderID): Truy xuất thông tin chi tiết của đơn đặt hàng.  
validateAccess(purchaseOrderID, employeeID): Kiểm tra quyền truy cập của nhân viên đối với đơn đặt hàng.  
- Quan hệ:  
Tương tác với CommissionedEmployee để quản lý thông tin các đơn đặt hàng.  
Quản lý trạng thái và thông tin các đối tượng PurchaseOrder.  

**Biểu đồ lớp (Class Diagram)**  
CommissionedEmployee tương tác với PurchaseOrderSystem để tạo, cập nhật hoặc xóa các đối tượng PurchaseOrder.  
PurchaseOrderSystem xử lý logic, đảm bảo quyền truy cập hợp lệ và quản lý trạng thái đơn đặt hàng.  

**Nhiệm vụ của từng lớp**
- CommissionedEmployee  
Gửi yêu cầu tạo, cập nhật hoặc xóa đơn đặt hàng.  
Cung cấp thông tin chi tiết cho từng thao tác (thêm thông tin đơn đặt hàng, cập nhật hoặc xóa).  
- PurchaseOrder  
Lưu trữ thông tin liên quan đến đơn đặt hàng như khách hàng, sản phẩm, ngày tạo và trạng thái đơn đặt hàng.  
Được tạo, cập nhật hoặc xóa bởi CommissionedEmployee thông qua PurchaseOrderSystem.  
- PurchaseOrderSystem  
Xử lý các yêu cầu tạo, cập nhật và xóa đơn đặt hàng.  
Kiểm tra quyền truy cập và trạng thái hợp lệ của đơn đặt hàng (chỉ cho phép thao tác đối với các đơn đặt hàng "mở").  
Cập nhật và xóa các đối tượng PurchaseOrder khi có yêu cầu từ CommissionedEmployee.  

**Sơ đồ lớp**  
Code:
```  
@startuml
class CommissionedEmployee {
    - employeeID: String
    - nameEmployee: String
    - commissionRate: Double
    - loGin: Boolean
    --
    + createOrder(orderInfo: PurchaseOrder): void
    + updateOrder(orderID: String, updatedInfo: PurchaseOrder): void
    + deleteOrder(orderID: String): void
}

class PurchaseOrder {
    - purchaseOrderID: String
    - customerContact: String
    - billingAddress: String
    - productList: List<String>
    - orderDate: Date
    - status: String
}

class PurchaseOrderSystem {
    + createPurchaseOrder(orderInfo: PurchaseOrder): String
    + updatePurchaseOrder(orderID: String, updatedInfo: PurchaseOrder): void
    + deletePurchaseOrder(orderID: String): void
    + getPurchaseOrder(orderID: String): PurchaseOrder
    + validateAccess(orderID: String, employeeID: String): Boolean
}

CommissionedEmployee --> PurchaseOrderSystem : "Gửi yêu cầu quản lý đơn hàng"
PurchaseOrderSystem --> PurchaseOrder : "Quản lý đơn hàng"
@enduml
```  
Link sơ đồ:  https://www.planttext.com/api/plantuml/png/d5DRQW8n5FsVLLpygj3Pm514gqM4GX-k82Qf1ZB9D0z1IXVH7RJqer3e1fJI3qltuGgwXMQSZ3eF5JeVTvXxxZcSEJVvNNorjK7As9W7c2EjeIlZc6dDfA3a8awud54A3m6u9mJg6uDU14EZc1XxGA2OvjCb26y4Rv5nO4_Q4QSUvBBFH0JdKdAAHDOCroy0hAWZN2b2rObCwq3SoGYkhS8Jf3EW6S5KCk8PDY4bniRdgGV9KH52ETqZaWy-1ZwiWimcfMItMuaAMsraJ5LN2eEmAQ4ZnhdxwX2YgDObC56IM6mkcNQqj9vbSClZQxkzB6LNVTSjsDYjLBtvuKmR6ljVoBClJ1pQmOxBV0jrt7zluw1OaJ2cvjXq0VUqAU8iTTJ1sELUzLiz-StjiNMHrbwRC6pLfXn1exzQV32OBTyjuDNypSAzNSrV1V3b9tm__Rm8c2oVnRWHrF4hkgdYpHw1DXKalTv_0000__y30000  

Sơ đồ:  
![Diagram](https://www.planttext.com/api/plantuml/png/d5DRQW8n5FsVLLpygj3Pm514gqM4GX-k82Qf1ZB9D0z1IXVH7RJqer3e1fJI3qltuGgwXMQSZ3eF5JeVTvXxxZcSEJVvNNorjK7As9W7c2EjeIlZc6dDfA3a8awud54A3m6u9mJg6uDU14EZc1XxGA2OvjCb26y4Rv5nO4_Q4QSUvBBFH0JdKdAAHDOCroy0hAWZN2b2rObCwq3SoGYkhS8Jf3EW6S5KCk8PDY4bniRdgGV9KH52ETqZaWy-1ZwiWimcfMItMuaAMsraJ5LN2eEmAQ4ZnhdxwX2YgDObC56IM6mkcNQqj9vbSClZQxkzB6LNVTSjsDYjLBtvuKmR6ljVoBClJ1pQmOxBV0jrt7zluw1OaJ2cvjXq0VUqAU8iTTJ1sELUzLiz-StjiNMHrbwRC6pLfXn1exzQV32OBTyjuDNypSAzNSrV1V3b9tm__Rm8c2oVnRWHrF4hkgdYpHw1DXKalTv_0000__y30000)  

**6.Run Payroll**   
**Xác định các lớp phân tích**  
**6.1. Employee (Nhân viên)**  
- Thuộc tính:  
employeeID: ID duy nhất của nhân viên.  
nameEmployee: Tên nhân viên.    
salary: Mức lương cơ bản của nhân viên.  
benefits: Thông tin về các khoản phúc lợi.  
paymentMethod: Phương thức nhận lương (thư, nhận trực tiếp, chuyển khoản).  
status: Trạng thái nhân viên (đang làm việc hoặc bị xóa).  
- Quan hệ: Được xử lý bảng lương bởi PayrollSystem.  

**6.2. PayrollSystem (Hệ thống bảng lương)**
- Phương thức:    
retrieveEmployees(currentDate): Truy xuất danh sách nhân viên cần được trả lương vào ngày hiện tại.  
calculatePay(employeeID): Tính toán tiền lương cho nhân viên dựa trên thẻ chấm công, đơn đặt hàng, thông tin nhân viên và các khoản khấu trừ hợp pháp.  
processPayment(employeeID, paymentMethod): Xử lý thanh toán dựa trên phương thức nhận lương của nhân viên.  
validateBankSystem(): Kiểm tra trạng thái của Hệ thống Ngân hàng và xử lý các giao dịch bị tạm hoãn.  
deleteEmployee(employeeID): Xóa nhân viên đã được đánh dấu sau khi xử lý bảng lương.  
- Quan hệ:    
Quản lý và xử lý bảng lương cho Employee.  
Tương tác với Hệ thống Ngân hàng để thực hiện giao dịch chuyển khoản.  

**6.3. BankSystem (Hệ thống ngân hàng)**  
- Phương thức:  
processTransaction(transactionData): Xử lý giao dịch ngân hàng được gửi từ PayrollSystem.  
isAvailable(): Kiểm tra trạng thái hoạt động của Hệ thống Ngân hàng.  
- Quan hệ: Nhận và xử lý các giao dịch thanh toán từ PayrollSystem.    

**Biểu đồ lớp (Class Diagram)**  
Employee tương tác với PayrollSystem để được xử lý bảng lương.  
PayrollSystem tính toán tiền lương, quản lý trạng thái và xử lý các khoản thanh toán qua BankSystem.  
BankSystem thực hiện giao dịch chuyển khoản ngân hàng.  

**Nhiệm vụ của từng lớp**  
- Employee  
Cung cấp thông tin cần thiết như lương, phúc lợi, và phương thức nhận lương.  
Nhận tiền lương qua phiếu lương hoặc giao dịch ngân hàng.  
- PayrollSystem  
Xử lý logic của việc chạy bảng lương.  
Tính toán lương dựa trên thông tin thẻ chấm công, đơn đặt hàng và các khoản khấu trừ.  
Xác thực trạng thái Hệ thống Ngân hàng và xử lý các giao dịch.  
Xóa nhân viên sau khi hoàn tất xử lý lương nếu được đánh dấu để xóa.  
- BankSystem  
Xử lý giao dịch ngân hàng cho các nhân viên nhận lương qua chuyển khoản.  
Quản lý trạng thái khả dụng để đảm bảo giao dịch được xử lý đúng hạn.  

**Sơ đồ lớp**  
Code:
```  
@startuml
class Employee {
    - employeeID: String
    - nameEmployee: String
    - salary: Double
    - benefits: String
    - paymentMethod: String
    - status: String
}

class PayrollSystem {
    + retrieveEmployees(currentDate: Date): List<Employee>
    + calculatePay(employeeID: String): Double
    + processPayment(employeeID: String, paymentMethod: String): void
    + validateBankSystem(): Boolean
    + deleteEmployee(employeeID: String): void
}

class BankSystem {
    + processTransaction(transactionData: Map<String, Object>): Boolean
    + isAvailable(): Boolean
}

Employee --> PayrollSystem : "Cung cấp thông tin"
PayrollSystem --> BankSystem : "Gửi yêu cầu thanh toán"
@enduml
```  
Link sơ đồ:  https://www.planttext.com/api/plantuml/png/R991JiCm44NtESMegrIY5uYggfGYX4H5fNA1gJDGWsD7zYHIX3WC2uI4n8uLNR3eINe2he13tRHDcuKLs_z_lndxT_apT8oMYqn5Gg5pS9dbobH4y1o1_tf0OU5wdC2ChTGFOKDZHbjrQykXGbibC3R5N55Od9EcUyckfSsnoaZpX7XXqdOE8nSxmqiK8ATOMQFKh79CMI05iEHbL3PGBXQ5jJvxZEm9wx6Rm8rqtDzA1i4gK8b2UO5FZeyhxXwK0f1R8yYvwGRzXE7iT5a-fpGo3IabAfdwCqUedpQbn5umCaOHwg19IH4t5Pr6-uziUhDBQneJSEyiQeU2fT4nx_vzNp212URzBVlj_9443uvWf3ilKIhqZTWdzKSthwRN6xHk9u7EHQ4VGAo_ttBWnUhBJrZgJdIegvrxxDvsjLv-IgXM7qLjVY-y6VK2sAnUlNj8EgsVxHy0003__mC0  

Sơ đồ:  
![Diagram](https://www.planttext.com/api/plantuml/png/R991JiCm44NtESMegrIY5uYggfGYX4H5fNA1gJDGWsD7zYHIX3WC2uI4n8uLNR3eINe2he13tRHDcuKLs_z_lndxT_apT8oMYqn5Gg5pS9dbobH4y1o1_tf0OU5wdC2ChTGFOKDZHbjrQykXGbibC3R5N55Od9EcUyckfSsnoaZpX7XXqdOE8nSxmqiK8ATOMQFKh79CMI05iEHbL3PGBXQ5jJvxZEm9wx6Rm8rqtDzA1i4gK8b2UO5FZeyhxXwK0f1R8yYvwGRzXE7iT5a-fpGo3IabAfdwCqUedpQbn5umCaOHwg19IH4t5Pr6-uziUhDBQneJSEyiQeU2fT4nx_vzNp212URzBVlj_9443uvWf3ilKIhqZTWdzKSthwRN6xHk9u7EHQ4VGAo_ttBWnUhBJrZgJdIegvrxxDvsjLv-IgXM7qLjVY-y6VK2sAnUlNj8EgsVxHy0003__mC0)  

### Code java mô phỏng ca sử dụng Maintain Timecard    
**Code**  
Lớp Employee.java: Chứa thông tin nhân viên và thẻ chấm công.  
```  
import java.util.ArrayList;
import java.util.List;

public class Employee {
    private String employeeID;
    private String name;
    private List<TimecardEntry> timecards;

    public Employee(String employeeID, String name) {
        this.employeeID = employeeID;
        this.name = name;
        this.timecards = new ArrayList<>();
    }

    public String getEmployeeID() {
        return employeeID;
    }

    public String getName() {
        return name;
    }

    public List<TimecardEntry> getTimecards() {
        return timecards;
    }

    public void addTimecard(TimecardEntry entry) {
        timecards.add(entry);
    }
}
```    

Lớp TimecardEntry.java: Chứa thông tin cơ bản về mục nhập thời gian của thẻ chấm công.  
```  
public class TimecardEntry {
    private String date;
    private double hoursWorked;

    public TimecardEntry(String date, double hoursWorked) {
        this.date = date;
        this.hoursWorked = hoursWorked;
    }

    public String getDate() {
        return date;
    }

    public double getHoursWorked() {
        return hoursWorked;
    }
}

```   

Lớp Main.java: Xử lý logic chính.  
```  
public class Main {
    public static void main(String[] args) {
        // Tạo nhân viên
        Employee employee = new Employee("E001", "John Doe");

        // Thêm các mục thời gian vào thẻ chấm công
        employee.addTimecard(new TimecardEntry("2024-11-19", 8));
        employee.addTimecard(new TimecardEntry("2024-11-20", 7.5));

        // Hiển thị thông tin thẻ chấm công
        System.out.println("Timecards for Employee: " + employee.getName());
        for (TimecardEntry entry : employee.getTimecards()) {
            System.out.println("- Date: " + entry.getDate() + ", Hours Worked: " + entry.getHoursWorked());
        }
    }
}
```   
Tham khảo website: https://www.planttext.com/

