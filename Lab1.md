**Lab1.md**  
**Bài tập thực hành** 

1. Phân tích kiến trúc  
1.1. Đề xuất kiến trúc
- Kiến trúc phân lớp (Layered Architecture)  

1.2. Giải thích lý do vì: Kiến trúc của hệ thống mới Payroll cần phải có các yêu cầu sau:
- Nhập và lưu thông tin vào cơ sở dữ liệu
- Hiện đại, thay đổi và cập nhật thông tin
- Bảo mật
- Phân quyền người dùng
- Tự động thanh toán lương theo định kỳ
- Có khả năng mở rộng và linh hoạt xử lý nhiều loại nhân viên và cấu trúc thanh toán khác nhau  
->Dựa trên thông tin đã phân tích, việc sử dụng kết hợp kiến trúc phân lớp sẽ là giải pháp lý tưởng để đáp ứng yêu cầu này. Kiến trúc này cần phải phù hợp với các hệ thống cũ, cung cấp giao diện máy tính để bàn hiện tại cho Windows và đảm bảo truy cập dữ liệu nhân viên được bảo mật  

1.3. Ý nghĩa từng thành phần:
- Presentation Layer: là tầng giao diện, tương tác với người dùng. Có chức năng phân tích yêu cầu từ Client
- Business Layer: là tầng thực hiện xử lý các logic nghiệp vụ. Tầng này nhận yêu cầu từ Presentation Layer, xử lý nó và gửi yêu cầu tương ứng đến Persistence Layer
- Persistence Layer: là tầng gửi các yêu cầu từ Business Layer đến Database Layer để thực hiện các thao tác liên quan đến dữ liệu
- Database Layer: là tầng gồm cơ sở dữ liệu và các thành phần liên quan. Có chức năng quản lý cơ sở dữ liệu, thực hiện thao tác đọc và ghi dữ liệu, triển khai các truy vấn và lưu trữ dữ liệu

1.4 Sơ đồ Package
![Diagram](https://www.planttext.com/api/plantuml/png/X5FDIWCn4BxdAORS-mOYhRiz22sK8dWUiqE8cqn2aaKMySay-4Y-WcbLtDRzkMQ-dvdl8v_l7-kKCUREMI5IQpXWH0SfzvOW-aH215GjQW9PMKESOOSzHGcl0Y2IoiYwGEMHWe_Pi8QzRpfBydByQBZnBmbgIcts0JOXMACm6yzIl0rCxhfac5A2dTT6JPWTi8_UMZX4hmhsvBfbNNXNhW_6aSBOm1wvgBko_XMYyiwPek0PAhIgioChtNCc7S-3wNrEsiDzVbCO2jMO4JPAdS_x4shAynEc0jYwO7rF1FNFaxmO5_ddOZguPW0iHlzBWDNgTZQksMAMsTEpR-ve0OkigL8MYJCzZ6GBDyltpII-J1ThugRyh2y0003__mC0)

 Đường liên kết của sơ đồ: https://www.planttext.com/api/plantuml/png/X5FDIWCn4BxdAORS-mOYhRiz22sK8dWUiqE8cqn2aaKMySay-4Y-WcbLtDRzkMQ-dvdl8v_l7-kKCUREMI5IQpXWH0SfzvOW-aH215GjQW9PMKESOOSzHGcl0Y2IoiYwGEMHWe_Pi8QzRpfBydByQBZnBmbgIcts0JOXMACm6yzIl0rCxhfac5A2dTT6JPWTi8_UMZX4hmhsvBfbNNXNhW_6aSBOm1wvgBko_XMYyiwPek0PAhIgioChtNCc7S-3wNrEsiDzVbCO2jMO4JPAdS_x4shAynEc0jYwO7rF1FNFaxmO5_ddOZguPW0iHlzBWDNgTZQksMAMsTEpR-ve0OkigL8MYJCzZ6GBDyltpII-J1ThugRyh2y0003__mC0
  
```- Code:    
@startuml  
skinparam style rose  
package "Client Layer" {  
  rectangle "Reporting Module"  
  rectangle "Windows Desktop Application"  
}  
  
package "Business Logic Layer" {  
  rectangle "Payroll Processing Engine"  
  rectangle "Timecard Management"  
  rectangle "Commission Calculation"  
}  
  
package "Integration Layer" {  
  rectangle "Payment Processing Module"  
}  
  
package "Data Access Layer" {  
  database "Employee Database"  
  database "Project Management Database"  
}  
  
"Reporting Module" --> "Payroll Processing Engine"  
"Windows Desktop Application" --> "Payroll Processing Engine"  
"Payroll Processing Engine" --> "Timecard Management"  
"Payroll Processing Engine" --> "Commission Calculation"  
"Payroll Processing Engine" --> "Payment Processing Module"  
"Employee Database" <--> "Payroll Processing Engine"  
"Project Management Database" <--> "Payroll Processing Engine"  
  
@enduml
```

2. Cơ chế phân tích
Các cơ chế cần giải quyết trong bài toán và giải thích lý do:    
2.1. Cơ chế bảo mật và kiểm soát quyền truy cập   
•	Bảo vệ dữ liệu và chỉ cho phép họ truy cập thông tin của riêng mình.  
•	Admin có quyền truy cập nâng cao để quản lý thông tin nhân viên.  
•	Lý do: Để đảm bảo tính bảo mật và tuân thủ đúng quy định bảo mật dữ liệu.  

2.2. Cơ chế tính lương tự động   
•	Tính toán lương và hoa hồng tự động dựa trên thời gian làm việc và đơn hàng.  
•	Tính toán lương tăng ca (1,5x lương cơ bản) cho người làm việc quá 8 giờ/ngày.  
•	Lý do: Giảm thiểu rủi ro khi tính toán thủ công và tăng hiệu quả, chính xác trong việc tính lương.  

2.3. Tích hợp dữ liệu cũ  
•	Đảm bảo khả năng truy cập nhưng không thay đổi dữ liệu cũ từ Cơ sở dữ liệu quản lý dự án DB2 hệ thống.   
•	Đảm bảo đồng bộ và cập nhật dữ liệu chính xác từ các hệ thống khác.  
•	Lý do: Đảm bảo khả năng liên kết thông tin giữa hệ thống mới và hệ thống cũ để giảm chi phí và tránh thay đổi hệ thống.  

2.4. Cơ chế tạo báo cáo   
•	Tạo các báo cáo chi tiết về số giờ làm việc, tổng lương và các dữ liệu khác.  
•	Các báo cáo cho phép nhân viên truy cập dữ liệu của họ, trong khi Admin có quyền tạo báo cáo tổng hợp.  
•	Lý do: Để theo dõi số giờ làm, tổng lương và dữ liệu liên quan một cách minh bạch, rõ ràng và chi tiết nhất.  

2.5. Cơ chế bảo trì và quản lý nhân viên    
•	Admin cần có quyền bổ sung, xóa và cập nhật thông tin nhân viên.  
•	Cung cấp các API để xử lý yêu cầu liên   
•	Lý do: Cần có quy trình rõ ràng để Admin quản lý thông tin nhân viên một cách chính xác và linh hoạt.  

2.6. Cơ chế thanh toán   
•	Xử lý và quản lý các phương thức thanh toán (chuyển tài khoản, gửi qua bưu điện hoặc nhận trực tiếp).  
•	Đảm bảo rằng thanh toán diễn ra chính xác vào thời gian quy định (thứ sáu hoặc vào ngày làm việc cuối cùng của tháng ).  
•	Lý do: Đảm bảo quá trình thanh toán diễn ra chính xác, đúng lịch trình và theo nhu cầu của từng nhân viên.  
  
3. Phân tích ca sử dụng Payment
- Xác định các lớp phân tích:  
3.1. Employee (Nhân viên)  
•	Thuộc tính:  
o	employeeID: ID của nhân viên.  
o	name: Tên nhân viên.  
o	paymentMethod: Phương thức thanh toán hiện hành.  
•	Quan hệ: Có mối quan hệ 1-1 với lớp PaymentMethod.  

3.2. PaymentMethod (Phương thức thanh toán)  
•	Thuộc tính:  
o	methodType: Loại phương thức thanh toán (nhận hàng, gửi thư, gửi trực tiếp).  
o	address: Địa chỉ (nếu chọn "mail").  
o	bankName: Tên ngân hàng (nếu chọn "gửi tiền trực tiếp").  
o	accountNumber: Số tài khoản ngân hàng (nếu chọn "gửi tiền trực tiếp").  
•	Quan hệ: Không có quan hệ với các lớp khác trong phân tích này.

3.3. PaymentSystem (Hệ thống thanh toán)  
•	Phương pháp:  
o	updatePaymentMethod(employeeID, paymentMethod): Cập nhật phương thức thanh toán cho nhân viên.  
o	getPaymentMethods(): Lấy sẵn danh sách thanh toán phương thức.  
•	Quan hệ: Tương tác Employeevà PaymentMethod.  

- Biểu đồ lớp mô tả các lớp phân tích và quan hệ:  
•  Employee có quan hệ 1-1 với PaymentMethod (mỗi nhân viên chỉ có một phương thức thanh toán).  
•  PaymentMethod có quan hệ 1-1 với Employee.  
•  PaymentSystem tương tác với cả Employee và PaymentMethod để cập nhật và lấy thông tin.  

- Nhiệm vụ của từng lớp phân tích  
•	Employee: Tương tác với hệ thống để chọn và cập nhật phương thức toán toán.  
•	PaymentMethod: Lưu trữ thông tin liên quan đến phương thức thanh toán mà nhân viên đã chọn.  
•	PaymentSystem: Xử lý logic để cập nhật và xác thực phương thức thanh toán cho nhân viên.  

- Sơ đồ lớp ca sử dụng Payment  
![Diagram](https://www.planttext.com/api/plantuml/png/V551Ri8m4Bpx5IjE81KahbQ5EBG7f1OXmGUMU9LOZPt8km55Y9Tnw9FuGXiIqZfKzSNQ6NjcTlTw-LooO93AvIh9aHbUNPaNDH6S53I7kdhrec4hmVgqnJqwYf4IQqTUtacomcZO_2xLMNNw4NmtSRTgLvS3IJGc47CCxj5_h1_SCKcAoikwSdiAFJMqtTOivEwsLMbGA4eqVkptwT_E9XeEXJMjO4eIaJp-fjyiotC4BvfS_Q17yn5CfxSh7ew635d5oMUpnS-AD5Wl530HXgELx8-tGyN1XoLvq-p-2m00__y30000)  

- Đường liên kết của sơ đồ: https://www.planttext.com/api/plantuml/png/V551Ri8m4Bpx5IjE81KahbQ5EBG7f1OXmGUMU9LOZPt8km55Y9Tnw9FuGXiIqZfKzSNQ6NjcTlTw-LooO93AvIh9aHbUNPaNDH6S53I7kdhrec4hmVgqnJqwYf4IQqTUtacomcZO_2xLMNNw4NmtSRTgLvS3IJGc47CCxj5_h1_SCKcAoikwSdiAFJMqtTOivEwsLMbGA4eqVkptwT_E9XeEXJMjO4eIaJp-fjyiotC4BvfS_Q17yn5CfxSh7ew635d5oMUpnS-AD5Wl530HXgELx8-tGyN1XoLvq-p-2m00__y30000
  
```- Code:     
@startuml  
class Employee {  
    +employeeID: String  
    +name: String  
    +paymentMethod: PaymentMethod  
}  
  
class PaymentMethod {  
    +methodType: String  
    +address: String  
    +bankName: String  
    +accountNumber: String  
}  
  
class PaymentSystem {  
    +updatePaymentMethod(employeeID: String, paymentMethod: PaymentMethod): void  
    +getPaymentMethods(): List<PaymentMethod>  
}  
  
Employee "1" -- "1" PaymentMethod : has  
PaymentSystem ..> Employee : interacts with  
PaymentSystem ..> PaymentMethod : interacts with    
@enduml  
```
4. Phân tích ca sử dụng Maintain Timecard  
- Xác định các lớp phân tích:  

4.1. Employee (Nhân viên): Đại diện cho nhân viên tương tác với hệ thống để nhập hoặc gửi thẻ chấm công.  
•	Thuộc tính:  
o	employeeID: ID nhân viên  
o	name: Tên nhân viên  
o	position: Vị trí công tác  
•	Quan hệ: Có mối quan hệ với lớp Timecard.  

4.2. Timecard (Thẻ chấm công): Đại diện cho bảng chấm công của nhân viên trong một kỳ lương.  
•	Thuộc tính:  
o	timecardID: ID của thẻ chấm công  
o	startDate: Ngày bắt đầu của kỳ lương   
o	endDate: Ngày kết thúc của kỳ lương  
o	status: Thẻ chấm trạng thái (ví dụ: Đã gửi)  
o	submitDate: Ngày chấm  
•	Quan hệ: Có quan hệ với lớp TimecardEntry.  

4.3. TimecardEntry (Dòng nhập thời gian): Giao diện cho một mục trong thẻ chấm, ghi lại số ngày và số giờ làm việc của nhân viên.   
•	Thuộc tính:  
o	date: Ngày làm việc  
o	hoursWorked: Số giờ làm trong ngày  
o	chargeNumber: Mã chi phí  
•	Quan hệ: Mỗi Timecard có nhiều TimecardEntry.  

4.4. ChargeNumber (Mã chi phí): Đại diện cho mã chi phí từ cơ sở dữ liệu Quản lý Dự án.  
•	Thuộc tính:  
o	chargeNumberID: ID mã chi phí  
o	description: Mô tả mã chi phí  
•	Quan hệ: Liên kết với TimecardEntry.

4.5. Project ManagementDB (Cơ sở quản lý dự án): Giao diện cơ sở dữ liệu Quản lý dự án.  
•	Phương pháp:  
o	getAvailableChargeNumbers(): Lấy chi phí mã hóa hiện có của danh sách.  

4.6 TimecardSystem (Hệ thống thẻ chấm công): Đại diện cho hệ thống xử lý thẻ chấm công, cam kết thực hiện các nhiệm vụ chính.  
•	Phương pháp:  
o	retrieveTimecard(employeeID): Lấy thẻ hiện tại của nhân viên  
o	saveTimecard(timecard): Lưu thẻ chấm công  
o	submitTimecard(timecard): Gửi thẻ chấm công  

- Biểu đồ lớp mô tả các lớp phân tích và quan hệ:  
•	Employee có quan hệ 1-nhiều với Timecard (một nhân viên có thể có nhiều thẻ chấm công trong các kỳ lương khác nhau).  
•	Timecard có quan hệ 1-nhiều với TimecardEntry (một thẻ chấm công có nhiều dòng nhập thời gian cho công việc từng ngày).  
•	TimecardEntry có quan hệ n-1 với ChargeNumber (một dòng nhập có thể liên kết với một công cụ mã hóa).  
•	TimecardSystem và Project ManagementDB là hai lớp quản lý hệ thống xử lý các yêu cầu từ phía Employee.  

- Nhiệm vụ của từng lớp phân tích  
•	Employee: Tương tác với hệ thống để nhập, cập nhật và gửi thẻ chấm công.  
•	Timecard: Lưu trữ thông tin về thời gian làm việc, trạng thái và kỳ lương.  
•	TimecardEntry: Ghi nhận chi tiết từng ngày làm việc và số giờ làm cho mã chi phí.  
•	ChargeNumber: Cung cấp thông tin mã hóa chi phí từ cơ sở dữ liệu Quản lý Dự án.  
•	TimecardSystem: Xử lý logic của các ca sử dụng, bao gồm truy xuất, lưu và gửi thẻ chấm công.  
•	Project ManagementDB: Cung cấp sẵn các mã chi phí từ hệ thống quản lý dự án.  

- Sơ đồ lớp ca sử dụng Maintain Timecard
![Diagram](https://www.planttext.com/api/plantuml/png/Z5D1JiCm4Bpd5QkS2b8ZSRLGLQ0z8052AX9drraIGsnNzgQeGhoC0q_Y2xXDdBXf9CZ1qOvdPzUUzS_NzzmHjrIhAX4LTmwMQbEP7I9y9B3_i8rl5mnMPAKk6bnpXSV8nZX9qkWE_KnQpIUfK72R1qrguw7cePK59o-yNzi6T3w4F8zgDyYjrqh6oIVLbvhiBhIG3oHBKrltREmRvWoafWOL9RS5FjHgZPR1JHJryZ4QrEEyuI5pTCBApVXDFLhpYeBkkUO5AjIqk0wQ1TBLbikAhokCQxh96OCxwUWoHcUdvr_j7A4ASXPzQTnYs9sS6krrmsvxnppY1nDxakTlZSnZF_x1zdrsCvTUf32T-b-MdQVzs30ekKkwS9pLsCj064rSwfxVR7H9wR5Z32gflUj09XdSL9RD-kTmc0gqN923Tqdb63bg-6_ocDMiiyN1YpKgcVlftx_DNm000F__0m00)

- Đường liên kết của sơ đồ: https://www.planttext.com/api/plantuml/png/Z5D1JiCm4Bpd5QkS2b8ZSRLGLQ0z8052AX9drraIGsnNzgQeGhoC0q_Y2xXDdBXf9CZ1qOvdPzUUzS_NzzmHjrIhAX4LTmwMQbEP7I9y9B3_i8rl5mnMPAKk6bnpXSV8nZX9qkWE_KnQpIUfK72R1qrguw7cePK59o-yNzi6T3w4F8zgDyYjrqh6oIVLbvhiBhIG3oHBKrltREmRvWoafWOL9RS5FjHgZPR1JHJryZ4QrEEyuI5pTCBApVXDFLhpYeBkkUO5AjIqk0wQ1TBLbikAhokCQxh96OCxwUWoHcUdvr_j7A4ASXPzQTnYs9sS6krrmsvxnppY1nDxakTlZSnZF_x1zdrsCvTUf32T-b-MdQVzs30ekKkwS9pLsCj064rSwfxVR7H9wR5Z32gflUj09XdSL9RD-kTmc0gqN923Tqdb63bg-6_ocDMiiyN1YpKgcVlftx_DNm000F__0m00



```- Code:  
@startuml  
class Employee {  
    +employeeID: String  
    +name: String  
    +position: String  
}  
  
class Timecard {  
    +timecardID: String  
    +startDate: Date  
    +endDate: Date  
    +status: String  
    +submitDate: Date  
}  
  
class TimecardEntry {  
    +date: Date  
    +hoursWorked: int  
    +chargeNumber: ChargeNumber  
}  
  
class ChargeNumber {  
    +chargeNumberID: String  
    +description: String  
}  
  
class ProjectManagementDB {  
    +getAvailableChargeNumbers(): List<ChargeNumber>  
}  
  
class TimecardSystem {  
    +retrieveTimecard(employeeID: String): Timecard  
    +saveTimecard(timecard: Timecard): void  
    +submitTimecard(timecard: Timecard): void  
}  
  
Employee "1" -- "1..*" Timecard : has  
Timecard "1" -- "1..*" TimecardEntry : contains  
TimecardEntry "1" -- "1" ChargeNumber : linked to  
TimecardSystem ..> Employee : interacts with  
TimecardSystem ..> Timecard : interacts with  
TimecardSystem ..> ProjectManagementDB : retrieves from  
@enduml  
```

5. Hợp nhất kết quả phân tích   
5.1. Employee (Nhân viên)  
- Thuộc tính:    
employeeID: Mã định danh của nhân viên.  
name: Tên của nhân viên.  
position: Vị trí công việc của nhân viên.  
paymentMethod: Phương thức thanh toán của nhân viên.  
- Quan hệ:   
Có mối quan hệ 1-nhiều với Timecard(nhân viên có thể có nhiều dấu chấm công).  
Có mối quan hệ 1-1 với PaymentMethod( mỗi nhân viên chỉ có một phương thức thanh toán).  

5.2. Thẻ chấm công (Thẻ chấm công)  
- Thuộc tính: 
timecardID: Mã định nghĩa của thẻ chấm.  
startDate: Ngày bắt đầu kỳ lương.  
endDate: Ngày kết thúc kỳ lương.  
status: Trạng thái của thẻ chấm công (ví dụ: "Đã gửi").  
submitDate: Ngày thẻ được gửi.  
- Quan hệ:  
Có mối quan hệ 1-nhiều với TimecardEntry(một thẻ chấm có nhiều dòng ghi nhận thời gian làm việc).  

5.3. TimecardEntry (Dòng nhập thời gian)  
- Thuộc tính:   
date: Ngày làm việc.  
hoursWorked: Số giờ làm việc trong ngày.  
chargeNumber: Mã chi phí được phân bổ cho ngày làm việc.  
- Quan hệ:  
Liên kết với ChargeNumberđể ghi mã chi phí ứng dụng cho công việc thời gian.  

5.4. ChargeNumber (Mã chi phí)  
- Thuộc tính:  
chargeNumberID: Mã định nghĩa của mã khóa.  
description: Mô tả chi phí mã hóa.  
- Quan hệ:  
Được liên kết TimecardEntry để xác định công việc chi phí.  

5.5. Project ManagementDB (Cơ sở quản lý dự án)  
- Phương pháp:  
getAvailableChargeNumbers(): Lấy danh sách các chi phí mã hóa hiện có từ dự án quản lý cơ sở dữ liệu.  

5.6. TimecardSystem (Hệ thống thẻ chấm công)  
- Phương pháp:  
retrieveTimecard(employeeID: String): Lấy thẻ hiện tại của nhân viên.  
saveTimecard(timecard: Timecard): Lưu thẻ chấm công.  
submitTimecard(timecard: Timecard): Gửi thẻ chấm công.  
- Quan hệ:   
Tương tác Employeeđể lấy thông tin nhân viên.  
Tương tác Timecardđể quản lý và lưu trữ thẻ chấm công.  
Kết nối ProjectManagementDBđể lấy mã chi phí.  

5.7. PaymentMethod (Phương thức thanh toán)   
- Thuộc tính:  
methodType: Loại phương thức thanh toán (nhận hàng, gửi thư hoặc gửi tiền trực tiếp).  
address: Địa chỉ nhận thanh toán (dùng cho phương thức "gửi thư").  
bankName: Tên ngân hàng (dùng cho phương thức "gửi tiền trực tiếp").  
accountNumber: Số tài khoản ngân hàng (dùng cho phương thức "gửi tiền trực tiếp").  
- Quan hệ:  
Không có quan hệ trực tiếp với các lớp khác bên ngoài Employee.  

5.8. PaymentSystem (Hệ thống thanh toán) 
- Phương pháp:  
updatePaymentMethod(employeeID: String, paymentMethod: PaymentMethod): Cập nhật phương thức thanh toán của nhân viên.  
getPaymentMethods(): Lấy danh sách các phương thức thanh toán có sẵn.  
- Quan hệ:  
Tương tác Employeeđể cập nhật và quản lý phương thức thanh toán.  
Tương tác PaymentMethodđể lưu và lấy thông tin chi tiết về các phương thức thanh toán.  

- Sơ đồ hợp nhất 2 ca sử dụng
![Diagram](https://www.planttext.com/api/plantuml/png/Z5JDJjmm4BxdAQoSA2ehzHeXHEbog5GG4aWzpph3nX3RaJtPAgfuCWuyKby1PnCdjXDHzf3LZB_vyJVV-D_hswKbCDJAEkCrMCkkPLFh3f7zpLZ_mz7-kItOFHcXzeDVWSJOqsWhI6YLUA6JgEW6gT9bmUv2Ctl9ngeFGY87K_ggDDffrMEpMo1Nkl-EBQeoTJaSjJQ9RNTIXC6BwjUAJETRA9EKbMwD_QtDCxfh24M3brTWzdZRoXsQWlq8h3bzwFNPmxZqaYLQRaGJSJabkpFw2JdTW88zzbHkhtpEFTBt0uWQTZM6DUt9buBz4fREG-_5ylxtdIMKFfr1LneFw4zFbb9mUVtfo344U3_46UJm1otAS1wVGCzt3yNZsvH7ww5h4Zb2MHgqYGPse9vl5ye5pdMho4znGVbGDcQdRNg1H1sj4FJrG_r7TBZfHOVpr2BtSMpJakRVSdPsvlusczDytgA2LM2poLn73Mel6DUAGAWPFnnCGNaiu8BLGhabOAIpH3YRpSNyVXoN10rmikoFe6eD73JyV_2Qyej9fPOz6YtNgCaJtGpan4FzkFCbDisO16INxatgtzHt0000__y30000)

- Đường liên kết của sơ đồ: https://www.planttext.com/api/plantuml/png/Z5JDJjmm4BxdAQoSA2ehzHeXHEbog5GG4aWzpph3nX3RaJtPAgfuCWuyKby1PnCdjXDHzf3LZB_vyJVV-D_hswKbCDJAEkCrMCkkPLFh3f7zpLZ_mz7-kItOFHcXzeDVWSJOqsWhI6YLUA6JgEW6gT9bmUv2Ctl9ngeFGY87K_ggDDffrMEpMo1Nkl-EBQeoTJaSjJQ9RNTIXC6BwjUAJETRA9EKbMwD_QtDCxfh24M3brTWzdZRoXsQWlq8h3bzwFNPmxZqaYLQRaGJSJabkpFw2JdTW88zzbHkhtpEFTBt0uWQTZM6DUt9buBz4fREG-_5ylxtdIMKFfr1LneFw4zFbb9mUVtfo344U3_46UJm1otAS1wVGCzt3yNZsvH7ww5h4Zb2MHgqYGPse9vl5ye5pdMho4znGVbGDcQdRNg1H1sj4FJrG_r7TBZfHOVpr2BtSMpJakRVSdPsvlusczDytgA2LM2poLn73Mel6DUAGAWPFnnCGNaiu8BLGhabOAIpH3YRpSNyVXoN10rmikoFe6eD73JyV_2Qyej9fPOz6YtNgCaJtGpan4FzkFCbDisO16INxatgtzHt0000__y30000

```- code
@startuml  
class Employee {  
    +employeeID: String    
    +name: String  
    +position: String  
    +paymentMethod: PaymentMethod  
}  
  
class Timecard {  
    +timecardID: String  
    +startDate: Date  
    +endDate: Date  
    +status: String  
    +submitDate: Date  
}  
  
class TimecardEntry {  
    +date: Date  
    +hoursWorked: int  
    +chargeNumber: ChargeNumber  
}  
  
class ChargeNumber {  
    +chargeNumberID: String  
    +description: String  
}  
  
class ProjectManagementDB {  
    +getAvailableChargeNumbers(): List<ChargeNumber>  
}  
  
class TimecardSystem {  
    +retrieveTimecard(employeeID: String): Timecard  
    +saveTimecard(timecard: Timecard): void  
    +submitTimecard(timecard: Timecard): void  
}  
  
class PaymentMethod {  
    +methodType: String  
    +address: String  
    +bankName: String  
    +accountNumber: String  
}  
  
class PaymentSystem {  
    +updatePaymentMethod(employeeID: String, paymentMethod: PaymentMethod): void  
    +getPaymentMethods(): List<PaymentMethod>  
}  
  
Employee "1" -- "1..*" Timecard : has  
Timecard "1" -- "1..*" TimecardEntry : contains  
TimecardEntry "1" -- "1" ChargeNumber : linked to  
TimecardSystem ..> Employee : interacts with  
TimecardSystem ..> Timecard : interacts with  
TimecardSystem ..> ProjectManagementDB : retrieves from  
  
Employee "1" -- "1" PaymentMethod : has  
PaymentSystem ..> Employee : interacts with  
PaymentSystem ..> PaymentMethod : interacts with  
  
@enduml
```  


