## Bài thực hành Lab5.md  
### Thiết kế các hệ thống con trong hệ thống Payroll System  
**1. Authentication System (Hệ thống Xác thực)**   
Yêu cầu chức năng: Quản lý đăng nhập và xác thực người dùng.  
Yêu cầu phi chức năng:  
- Độ bảo mật cao (mã hóa mật khẩu).  
- Thời gian phản hồi < 2 giây.  

Thành phần:  
- LoginController: Xử lý yêu cầu đăng nhập.  
- UserManager: Quản lý thông tin người dùng (username, password).  
- AuthenticationService: Kiểm tra tính hợp lệ thông tin đăng nhập.  

Tương tác:  
- Cung cấp token JWT để các hệ thống khác xác thực người dùng.  
- RBAC System kiểm tra vai trò dựa trên token.  


**2. Timecard Management System (Hệ thống Quản lý Thẻ chấm công)**   
Yêu cầu chức năng: Quản lý thông tin thời gian làm việc.  
Yêu cầu phi chức năng:  
- Hỗ trợ tải dữ liệu thẻ chấm công nhanh chóng (< 3 giây).  
- Đảm bảo độ chính xác cao trong lưu trữ và cập nhật dữ liệu.  

Thành phần:  
- TimecardController: Xử lý yêu cầu từ giao diện.  
- TimecardService: Xử lý logic cập nhật và lưu dữ liệu.  
- TimecardRepository: Tương tác với cơ sở dữ liệu.  

Tương tác:  
- Lấy thông tin người dùng từ Authentication System.  
- Gửi dữ liệu chấm công đến Payroll Processing System.  

**3. Payroll Processing System (Hệ thống Xử lý Lương)**  
Yêu cầu chức năng: Tính toán và xử lý lương cho nhân viên.  
Yêu cầu phi chức năng: Tính toán lương nhanh và chính xác.  
Thành phần:  
- PayrollController: Xử lý yêu cầu tính lương.  
- PayrollCalculator: Tính toán lương dựa trên dữ liệu thẻ chấm công, hoa hồng, và phụ cấp.  
- PaymentService: Xác định và xử lý phương thức thanh toán.  
- ReportGenerator: Tạo bảng lương và báo cáo.  

Tương tác:  
- Lấy thông tin thẻ chấm công từ Timecard Management System.  
- Gửi lệnh thanh toán đến Payment System.  
- Gửi dữ liệu lương đến Reporting System.  

**4. Payment System (Hệ thống Thanh toán)**  
Yêu cầu chức năng: Thực hiện giao dịch thanh toán.  
Yêu cầu phi chức năng:  
- Đảm bảo thanh toán thành công trong vòng 5 giây.  
- Kết nối an toàn với ngân hàng qua giao thức HTTPS/TLS.  

Thành phần:  
- BankInterface: Gửi yêu cầu thanh toán đến ngân hàng.  
- PrintService: In paycheck nếu chọn nhận lương trực tiếp.

Tương tác:  
- Nhận yêu cầu thanh toán từ Payroll Processing System.   
- Kết nối với BankInterface để thực hiện thanh toán.  
- Gửi xác nhận thanh toán đến Notification System.  


**5. Database System (Hệ thống Cơ sở dữ liệu)**  
Yêu cầu chức năng: Lưu trữ và quản lý dữ liệu.  
Yêu cầu phi chức năng:  
- Hỗ trợ tải 1 triệu bản ghi trong < 10 giây.  
- Đảm bảo backup định kỳ và phục hồi dữ liệu nhanh chóng.  

Thành phần:  
- ProjectManagementDatabase: Lưu dữ liệu thẻ chấm công.  
- PayrollDatabase: Lưu thông tin lương, phương thức thanh toán.  
- UserDatabase: Lưu thông tin người dùng.  

Tương tác:  
- Lưu trữ dữ liệu cho tất cả các hệ thống con (chấm công, lương, người dùng, thông báo).  
- Các hệ thống khác sử dụng Repository để truy vấn dữ liệu.  


**6. Scheduler System (Hệ thống Lập lịch)**  
Yêu cầu chức năng: Tự động khởi chạy các quy trình định kỳ.  
Yêu cầu phi chức năng:  
- Độ trễ của các job định kỳ < 1 phút.  
- Cấu hình dễ dàng, hỗ trợ điều chỉnh thời gian lập lịch linh hoạt.  

Thành phần:  
- SystemClockInterface: Xác định ngày trả lương.  
- JobScheduler: Kích hoạt các quy trình theo lịch (tính lương, báo cáo).  

Tương tác:  
- Kích hoạt Payroll Processing System vào ngày trả lương.  
- Gửi thông báo nhắc nhở chấm công qua Notification System.  


**7. Role-Based Access Control (RBAC System)**  
Yêu cầu chức năng: Quản lý phân quyền người dùng (Nhân viên, Quản lý, Quản trị viên).  
Yêu cầu phi chức năng:   
- Phân quyền chính xác theo vai trò, áp dụng ngay sau khi cập nhật.  
- Đảm bảo bảo mật trong kiểm tra quyền truy cập.  

Thành phần:  
- RoleManager: Gán và kiểm tra quyền của người dùng.  
- PermissionService: Đảm bảo người dùng chỉ truy cập chức năng phù hợp vai trò.  

 Tương tác:  
- Kiểm tra quyền người dùng cho tất cả các hệ thống.  
- Authentication System sử dụng RoleManager để gán vai trò.  

**8. Notification System (Hệ thống Thông báo)**  
Yêu cầu chức năng: Gửi thông báo đến người dùng (nhắc nhở chấm công, xác nhận lương, lỗi đăng nhập).  
Yêu cầu phi chức năng:  
- Gửi thông báo email trong vòng 10 giây từ thời điểm kích hoạt.  
- Hỗ trợ hiển thị thông báo thời gian thực trong ứng dụng.  

Thành phần:  
- NotificationManager: Xử lý và quản lý thông báo.  
- EmailService: Gửi thông báo qua email.  
- InAppNotification: Hiển thị thông báo trong ứng dụng.  

Tương tác:  
- Nhận yêu cầu gửi thông báo từ Scheduler, Payroll, và Timecard Systems.  
- Gửi email hoặc thông báo trong ứng dụng.  

**9. Reporting System (Hệ thống Báo cáo)**    
Yêu cầu chức năng: Tạo báo cáo về lương, thời gian làm việc, và các hoạt động khác.  
Yêu cầu phi chức năng:  
- Tạo báo cáo nhanh (dưới 10 giây).  
- Hỗ trợ xuất nhiều định dạng (PDF, Excel, CSV).  

Thành phần:  
- ReportController: Xử lý yêu cầu tạo báo cáo.  
- ReportService: Tạo báo cáo tổng hợp từ dữ liệu.  
- ExportService: Xuất báo cáo dưới dạng PDF/Excel.  

Tương tác:  
- Lấy dữ liệu từ Timecard Management, Payroll Processing, và Database Systems.  
- Xuất báo cáo theo yêu cầu từ các hệ thống.  


**10. Integration System (Hệ thống Tích hợp)**  
Yêu cầu chức năng: Tích hợp với các hệ thống bên ngoài (Ngân hàng, CRM).  
Yêu cầu phi chức năng:  
- Độ tin cậy cao khi tích hợp với API bên ngoài (thành công > 99.9%).  
- Khả năng mở rộng dễ dàng để tích hợp hệ thống mới.  

Thành phần:  
- API Gateway: Tương tác với hệ thống bên ngoài.  
- ExternalServiceAdapter: Đóng vai trò trung gian với các API của bên thứ ba.  

Tương tác:  
- Gửi dữ liệu thanh toán đến ngân hàng từ Payment System.  
- Kết nối hệ thống CRM để đồng bộ dữ liệu nhân viên và hoa hồng.  


**11. Bonus & Incentive Management System (Hệ thống Quản lý Thưởng và Hoa hồng)**  
Yêu cầu chức năng: Quản lý các khoản thưởng hoặc hoa hồng của nhân viên.  
Yêu cầu phi chức năng:  
- Tính toán thưởng trong < 3 giây.  
- Giao diện người dùng thân thiện, dễ sử dụng cho quản lý.  

Thành phần:  
- BonusCalculator: Tính thưởng dựa trên hiệu suất làm việc.  
- CommissionManager: Quản lý hoa hồng từ các đơn đặt hàng.   

Tương tác:  
- Lấy thông tin thẻ chấm công và hiệu suất từ Timecard Management System.  
- Gửi dữ liệu thưởng đến Payroll Processing System.    
 
 Tham khảo website vẽ sơ đồ: https://www.planttext.com/    