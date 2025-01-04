# 1.Mô tả tóm tắt bài toán.

- ## 1.1 Sự cần thiết và lợi ích khi giải quyết bài toán

    - *Sự cần thiết:*

        - Hệ thống trạm thời tiết ở vùng hẻo lánh thu thập thông tin thời tiết tại những khu vực không có hạ tầng địa phương (điện, truyền thông, đường sá), góp phần cung cấp dữ liệu cần thiết cho hệ thống thông tin thời tiết quốc gia.

        - Trạm phải tự hoạt động hoàn toàn độc lập, tự tạo năng lượng và duy trì kết nối qua vệ tinh, đặc biệt phù hợp với các vùng xa xôi, khó tiếp cận.

    - *Lợi ích:*

        - Phân tích và dự đoán thời tiết: Dữ liệu thu thập giúp phân tích sự thay đổi khí hậu cả ở cấp địa phương lẫn quốc gia, hỗ trợ dự báo thời tiết chính xác hơn.

        - Tự động hóa và tiết kiệm nguồn lực: Trạm vận hành không cần sự can thiệp thường xuyên của con người, giảm chi phí bảo trì và nhân lực.

        - Hỗ trợ nghiên cứu khí hậu: Cung cấp dữ liệu dài hạn và đáng tin cậy về khí hậu ở những khu vực hẻo lánh.

- ## 1.2 Các yêu cầu chức năng

    - *Thu thập dữ liệu thời tiết:*

        - Đo lường các thông số thời tiết như tốc độ và hướng gió, nhiệt độ đất và không khí, áp suất khí quyển, lượng mưa trong 24 giờ.

        - Quản lý việc thu thập và lưu trữ dữ liệu từ các thiết bị đo.

    - *Xử lý dữ liệu:*

        - Thực hiện xử lý và tổng hợp dữ liệu cục bộ để tối ưu hóa việc truyền qua liên kết vệ tinh có băng thông hạn chế.

    - *Truyền và lưu trữ dữ liệu:*

        - Truyền dữ liệu đã xử lý đến hệ thống lưu trữ và quản lý thông tin qua vệ tinh.

        - Bảo lưu dữ liệu tại trạm nếu không thể thiết lập kết nối.

    - *Quản lý năng lượng và bảo trì hệ thống:*

        - Sử dụng năng lượng tái tạo (mặt trời hoặc gió) để đảm bảo hoạt động.

        - Giám sát và báo cáo lỗi phần cứng, năng lượng, và phần mềm cho hệ thống bảo trì.

    - *Tái cấu hình hệ thống:*

        - Cho phép thay thế phần mềm từ xa hoặc sử dụng các thiết bị dự phòng khi xảy ra lỗi.

    - *Đảm bảo tính tự động và tự vận hành:*

        - Hệ thống phải hoạt động liên tục mà không cần sự can thiệp trực tiếp, ngay cả khi điều kiện môi trường khắc nghiệt.

- ## 1.3 Các yêu cầu phi chức năng

    - *Độ tin cậy cao:* Hệ thống phải hoạt động ổn định trong các điều kiện khắc nghiệt và thời gian dài, đồng thời Phát hiện và báo cáo lỗi phần cứng (thiết bị đo, năng lượng, truyền thông) kịp thời tới hệ thống quản lý.

    - *Tính tự chủ cao:* Tự vận hành không cần sự can thiệp của con người, tự bảo trì trong thời gian dài mà không cần kết nối hoặc bảo dưỡng trực tiếp.

    - *Tiết kiệm năng lượng:* Sử dụng hiệu quả nguồn năng lượng tái tạo(mặt trời, gió) hạn chế, ưu tiên các chức năng quan trọng. Tự động ngắt các bộ phát điện khi gặp điều kiện thời tiết nguy hiểm (gió lớn) để bảo vệ thiết bị.

    - *Khả năng mở rộng:* Hệ thống có thể dễ dàng nâng cấp hoặc bổ sung chức năng mới trong tương lai.
    
    - *Khả năng bảo trì từ xa:* Cho phép thay thế hoặc cập nhật phần mềm mới từ xa qua liên kết vệ tinh, tự động chuyển đổi sang các thiết bị dự phòng khi thiết bị chính gặp sự cố, đảm bảo hoạt động liên tục.

    - *Khả năng chống chịu môi trường:* Thiết kế để hoạt động trong các điều kiện thời tiết khắc nghiệt và chống lại các nguy cơ hư hại từ động vật hoặc môi trường tự nhiên.

    - *Giao tiếp đáng tin cậy:* Truyền dữ liệu qua vệ tinh với băng thông hạn chế nhưng vẫn đảm bảo thông tin quan trọng được ưu tiên gửi trước, bảo lưu dữ liệu cục bộ nếu mất kết nối và tự động gửi khi kết nối được khôi phục.

# 2.Phân tích các ca sử dụng.

## 2.1 Kiến trúc đề xuất.

- Kiến trúc được đề xuất là: **Kiến trúc phân lớp "Layered Architecture"**

- Hệ thống được chia thành các lớp chính, bao gồm:

    - *Lớp Thu thập Dữ liệu:* Quản lý các cảm biến đo lường và thu thập thông tin thời tiết.

    - *Lớp Xử lý Dữ liệu:* Phân tích, tổng hợp và lưu trữ dữ liệu cục bộ trước khi truyền qua vệ tinh.

    - *Lớp Giao tiếp và Truyền thông tin:* Quản lý kết nối vệ tinh để truyền dữ liệu tới hệ thống trung tâm.

    - *Lớp Quản lý Năng lượng:* Điều khiển sạc pin, hoạt động của máy phát, và đảm bảo tiết kiệm năng lượng.

    - *Lớp Bảo trì và Tái cấu hình:* Tự động phát hiện lỗi, thay thế phần mềm hoặc chuyển sang thiết bị dự phòng khi cần thiết.

- Biểu đồ package mô tả kiến trúc.
    ![Diagram](https://www.planttext.com/plantuml/png/b9JDQkCm58NtUeg3zts1K499mhIG46ZneblL5fQ8SsLigKmeNPGkkkWg3r2O46RNC3_CocBemcNUGqymhp3O2MqJcgIpqEPAvpjNvyh-wvwE2iDpOySfOyL84N9T2CQCCgb0N_doYM3ogenmujqTZFHkIWd2t9UpCKBftOE2gSyPnZ8UZNWY4Emz6-3mSAXZqMxZYW4CUD66qjRISf6XvzqtfCgxEriBFkaq5lbA0aGfBmgSMaw3IPUFEqhGQkUQBTTRxBbt2wJLxqreZnj-mGknWJstWqdF3fImEvZ7YklbXJ9SLbyGvdRYtGt1oEeN9J2AQejkgctyRjjzOOPQxN0ujRwSKzFtyFcM4gH_lditfwJcded8l8iTSae6LbEoWzpnvLpNetrSjbxD529VVhMGrIF99k-SZpTpwN0TvYhagiljYIAvvd3D6DiwluE3zhOfj10SUxTGY5-hU9xMZozWMpGDxaC3Q25ugQyRL7DyNi43jYlhncnlOYq4NKj9KypUj81Bxsv0wqosdzUuRekpXQ1VBI89gNqvCp2o-R1muTrzVSqVo6Jryp-CFfpbXXoZnfUycwg0iID1SVqt-GS00F__0m00)

## 2.2 Các cơ chế phân tích.

- *Cơ chế giám sát:* Giám sát hoạt động của cảm biến, năng lượng và kết nối.

- *Cơ chế lưu trữ và phục hồi dữ liệu:* Lưu trữ dữ liệu cục bộ khi mất kết nối và phục hồi khi có kết nối trở lại.

- *Cơ chế quản lý năng lượng:* Tối ưu việc sử dụng năng lượng tái tạo.

- *Cơ chế tái cấu hình:* Tự động cập nhật phần mềm hoặc chuyển đổi thiết bị dự phòng.

- *Cơ chế giao tiếp:* Đảm bảo truyền thông qua vệ tinh đáng tin cậy với băng thông hạn chế.

## 2.3 Kết quả phân tích từng ca sử dụng.

- Hệ thống *"Wilderness Weather Station"* có các ca sử dụng:

    - Ca sử dụng cho Hệ thống Trạm Khí Tượng (Weather Station System).

    - Ca sử dụng cho Hệ thống Quản lý và Lưu trữ Dữ liệu (Data Management and Archiving System).

    - Ca sử dụng cho Hệ thống Bảo trì Trạm (Station Maintenance System).

    - Ca sử dụng cho Hệ thống Quản lý Năng Lượng (Power Management).

    - Ca sử dụng cho Hệ thống Giám sát Cảm biến (Instrument Monitoring System).

    - Ca sử dụng cho Quản lý Cập nhật và Thay thế Cảm biến (Instrument Management).

    - Ca sử dụng cho Quản lý Hệ thống Phần Mềm (Software Management).

    - Ca sử dụng cho Báo cáo và Cảnh báo (Reporting and Alerts).

    - Ca sử dụng cho Quản lý Thông tin Liên Lạc (Communication Management).

    - Ca sử dụng cho Quản lý Môi Trường và Điều Kiện Thiên Nhiên (Environmental Monitoring and Management).

### 2.3.1 Phân tích Ca Sử Dụng Hệ thống Trạm Khí Tượng (Weather Station System)V

- a) Xác định các lớp phân tích

    - WeatherStation (Trạm khí tượng)

    - WeatherData (Dữ liệu thời tiết)

    - Sensor (Cảm biến)

    - SatelliteCommunication (Giao tiếp vệ tinh)

    - DataStorage (Lưu trữ dữ liệu)

- b) Nhiệm vụ của từng lớp phân tích

    - WeatherStation (Trạm khí tượng):

        - Thu thập dữ liệu từ các cảm biến về các thông số thời tiết.

        - Thực hiện xử lý và tổng hợp dữ liệu thu thập được.

        - Truyền tải dữ liệu đã tổng hợp đến hệ thống quản lý dữ liệu khi có kết nối vệ tinh.

        - Lưu trữ dữ liệu tạm thời nếu không thể kết nối.

    - WeatherData (Dữ liệu thời tiết):

        - Lưu trữ thông tin về các thông số thời tiết như nhiệt độ, độ ẩm, tốc độ gió, áp suất, lượng mưa.

        - Cung cấp thông tin về các thông số đã được xử lý và tổng hợp.

    - Sensor (Cảm biến):

        - Đo lường các thông số môi trường (nhiệt độ, tốc độ gió, lượng mưa, v.v.).

        - Cung cấp dữ liệu thời gian thực cho hệ thống.

    - SatelliteCommunication (Giao tiếp vệ tinh):

        - Thiết lập và duy trì kết nối vệ tinh.

        - Truyền tải dữ liệu từ trạm khí tượng về hệ thống quản lý dữ liệu khi có kết nối.

    - DataStorage (Lưu trữ dữ liệu):

        - Lưu trữ dữ liệu tạm thời khi không thể truyền tải qua vệ tinh.

        - Cung cấp khả năng truy xuất dữ liệu khi kết nối được khôi phục.

### Mô tả Use case 
### Hệ thống Trạm Khí Tượng

| **Tiêu đề**        | **Nội dung**                                                                                 |
|---------------------|---------------------------------------------------------------------------------------------|
| **Tên Use Case**    | Hệ thống Trạm Khí Tượng                                                                     |
| **Actor**           | Trạm khí tượng                                                                             |
| **Mô tả**           | Cho phép trạm khí tượng thu thập dữ liệu từ cảm biến, xử lý dữ liệu, và truyền tải đến hệ thống lưu trữ dữ liệu. |
| **Các lớp phân tích** | **Boundary**: Cảm biến<br>**Controller**: Trạm khí tượng<br>**Entity**: Giao tiếp xử lý, Lưu trữ dữ liệu |
| **Luồng sự kiện chính**   | 1. Trạm khí tượng yêu cầu thu thập dữ liệu thời tiết.<br>2. Cảm biến cung cấp dữ liệu (nhiệt độ, gió, áp suất, mưa) cho trạm khí tượng.<br>3. Trạm khí tượng xử lý và tổng hợp dữ liệu.<br>4. Trạm khí tượng kiểm tra kết nối vệ tinh.<br>5. Nếu kết nối khả dụng:<br>- Trạm khí tượng truyền tải dữ liệu đến hệ thống quản lý dữ liệu.<br>- Hệ thống quản lý dữ liệu nhận và lưu trữ dữ liệu. |
| **Luồng sự kiện phụ** | **Kết nối vệ tinh không khả dụng**:<br>5a. Nếu không có kết nối: Trạm khí tượng lưu trữ dữ liệu tạm thời.<br>5b. Nếu kết nối được khôi phục: <br>- Trạm khí tượng truyền tải dữ liệu đã lưu trữ tạm thời đến hệ thống quản lý dữ liệu.<br>- Hệ thống quản lý dữ liệu nhận và lưu trữ dữ liệu. |  

- c) Sequence Diagram (Biểu đồ trình tự)
    ![Diagram](https://www.planttext.com/plantuml/png/h9InYjj048RxVOeVLGdOB-327DXmWLpIs92aNDkBTh6qygrcZxXCTRMB52aEOeG914mCbqfBSA73xx5Fa5S8ApkvKz0TAL88X9Zv_fd_7_JJxSzouePich1yhZHCbWl6I54Y48sbnLZwShl0qBjlk53UNTUVt8t2MFboJ-XY92wjq5E1eUAnuMd469zIPX2DZI_NAUQose8EE-yA7KVWETu8JbAO4N5IcMQJpEePDqj40ryMAIO1hUlAaT1vPjWqqsIof1s9zzvjaLG_MjYZPKuYPKAJeYMYSyKpKC0lSENTDKXfUHJY9994aHXaQMgrcXv7ct7Y4vuBH2_gSkdTIiUujBuiTD34B5YJrDRKe24d_efh7ejKQFfB_-Amio0JMjhwHfGP7Wl6cakWspyPWHxULLyjfhxyOa4oF7L03sZra3Vgk2QnKsEtt-eCUXXO7GVWfabvfcLu8TojlFlKGQogsmwgzGAvzUM6EaWFE_wSjL8VLtjxoWfNrMUGTnzr3EbTqH1dF26yzkNUObvVcVPkfUuJmrpwiWWT6nqp0ErgmRRMMD73kNTRrT0Cc4VAk_tMMD73sDYbTnyqo9T5aoUINFnUGbRVWydLxSDzdXnyU7yEwA7zReBeEZtbpOIUrRwzbAhXMkBBzTDQ_suIxbPLWUJFDF_VD3rZx4peMVWb_G800F__0m00)

- d) Class Diagram (Biểu Đồ Lớp)
    ![Diagram](https://www.planttext.com/plantuml/png/T5BBJiCm4BpdAtA4Gty1LIeVW0XIpuiz44j-HBkReWhnPHpu97u1MR5RDmg-xSnwPdVit--VlIYnpi5tnfD8VmJf21wKrANOVtPzFYPv3wE5V2Ibk_k5cJWPYBIGCaK9JbjCD34AyDNTUcMu6Yd212QT6Gimpi5Pf-Ub-d3H3XDWgpb4BgrCBhwHzrU30L4IL-q0oiqlLuiwNM6ELNs5FnMR5VnS_DgL1b9uxnI75C8SdRc94QBqwfsCXnGZJAOk0I7QTJwv7ZGnlQCgICqnRv6OsFbpbM0eEvoGhw0HMptfRlVG9hz5BxbjCflxRNKsmtVb7TRE_uJLj1N1Rezeyn_z0m00__y30000)

### 2.3.2 Phân tích Ca Sử Dụng Quản lý và Lưu trữ Dữ liệu (Data Management and Archiving System)

- a) Xác định các lớp phân tích

    - DataManagement (Quản lý Dữ liệu)
    - DataArchiving (Lưu trữ Dữ liệu)
    - WeatherData (Dữ liệu Thời Tiết) 
    - UserInterface (Giao diện Người Dùng)
    - SecurityManagement (Quản lý An ninh) 

- b) Nhiệm vụ của từng lớp phân tích

    - DataManagement (Quản lý Dữ liệu): 
        - Tiếp nhận dữ liệu từ các trạm khí tượng thông qua các phương thức kết nối (vệ tinh, mạng không dây).  
        - Tổ chức, chuẩn hóa, và xử lý dữ liệu trước khi lưu trữ.  
        - Đảm bảo dữ liệu được phân loại và sẵn sàng cho việc phân tích hoặc truy vấn.  

    - DataArchiving (Lưu trữ Dữ liệu): 
        - Lưu trữ dữ liệu lịch sử vào cơ sở dữ liệu một cách có tổ chức và an toàn.  
        - Đảm bảo khả năng sao lưu và phục hồi dữ liệu khi xảy ra sự cố.  
        - Quản lý không gian lưu trữ và dọn dẹp các dữ liệu cũ hoặc ít dùng.  

    - WeatherData (Dữ liệu Thời Tiết):  
        - Đại diện cho các thông số thời tiết như nhiệt độ, độ ẩm, tốc độ gió, lượng mưa, áp suất khí quyển.  
        - Đảm bảo thông tin được lưu trữ đầy đủ và chính xác.  
        - Cho phép sử dụng dữ liệu này trong các báo cáo hoặc phân tích.  

    - UserInterface (Giao diện Người Dùng):  
        - Cung cấp công cụ tìm kiếm, lọc, và truy vấn dữ liệu thời tiết.  
        - Cho phép xuất dữ liệu dưới dạng báo cáo hoặc các định dạng file (CSV, Excel, PDF).  
        - Hiển thị kết quả phân tích hoặc đồ thị xu hướng khí hậu dựa trên dữ liệu đã thu thập.  

    - SecurityManagement (Quản lý An ninh):  
        - Đảm bảo chỉ những người dùng được phân quyền mới có thể truy cập dữ liệu.  
        - Giám sát và ghi lại các hoạt động liên quan đến truy cập và quản lý dữ liệu.  
        - Thực hiện mã hóa dữ liệu để đảm bảo an toàn trước các mối đe dọa.  

### Mô tả Use case 
### Quản lý và Lưu trữ Dữ liệu

| **Tiêu đề**        | **Nội dung**                                                                                 |
|---------------------|---------------------------------------------------------------------------------------------|
| **Tên Use Case**    | Quản lý và Lưu trữ Dữ liệu                                                                   |
| **Actor**           | Người dùng                                                                                 |
| **Mô tả**           | Cho phép người dùng truy vấn dữ liệu thời tiết thông qua hệ thống, bao gồm thu thập, xử lý, lưu trữ dữ liệu và kiểm soát truy cập. |
| **Các lớp phân tích** | **Boundary**: Giao diện người dùng<br>**Controller**: Quản lý dữ liệu, Lưu trữ dữ liệu, Quản lý an ninh<br>**Entity**: Trạm khí tượng, Dữ liệu thời tiết |
| **Luồng sự kiện chính**   | 1. Người dùng yêu cầu truy vấn dữ liệu.<br>2. Giao Diện Người Dùng yêu cầu dữ liệu thời tiết.<br>3. Quản Lý Dữ Liệu yêu cầu dữ liệu thời tiết.<br>4. Trạm Khí Tượng thu thập và cung cấp dữ liệu cho Quản Lý Dữ Liệu.<br>5. Quản Lý Dữ Liệu chuẩn hóa và xử lý dữ liệu, sau đó trả về dữ liệu đã xử lý cho Giao Diện Người Dùng.<br>6. Giao Diện Người Dùng lưu trữ dữ liệu.<br>7. Nếu dữ liệu hợp lệ: Xác nhận việc lưu trữ thành công và trả về kết quả cho Người dùng.<br>8. Người dùng yêu cầu truy cập dữ liệu đã lưu trữ.<br>9. Quản Lý An Ninh xác thực quyền truy cập của Người dùng.<br>10. Quản Lý An Ninh giám sát truy cập dữ liệu.<br>11. Quản Lý Dữ Liệu ghi lại hoạt động truy cập dữ liệu. |
| **Luồng sự kiện phụ** | 7a. Nếu dữ liệu không hợp lệ: Hệ thống thông báo lỗi. |

- c) Sequence Diagram (Biểu đồ trình tự)
    ![Diagram](https://www.planttext.com/plantuml/png/d5G_QnH15E_dKpoklozmHKZWGCGeI5Qi9tlZpd1xRvFPDqUk31OfR0mMOY6u726e11EqSOUGOaA-ntm2luBCNdBPYLEepLQ_V--zt-mlUxLP4zTaPYLZzLGXwAeMZ96YKi3WkV7j4c7RNSBSVOBjctC3cVRs6up3PrjvUsHW23it3Lo_zVOTPCQtfmYPjnS3ndXEbOR1i-BctDkF2iRk9nO3u3MCEN4ca1GjO91ftpOpU2BT6MG1khn5xH0dLU4Qs7VDP2UPATzUKOT-AJX9eJlfl4BILHcDq6ElCppbo0in4qZtbFIOQygMpgMQAopORcLmmlK21eyKhs0SS0Y9QL_KGZz64leLpqKosnR2CuLoDRN8ZLQqw6LZmHY66x4IZ63XlXZ8VNjgWBHPmDot9mYJ4BliOhEOCTnuC7QiqIC2hHPCtOBP0zPmu-uuC0AI7Rezsui5lFqAjBhjDDoMRc_BxgYfDBd18gGvsVkdDBtZ1n5fVFiPGRhllAlkWRTdKBhBQ3LzJYfAoBw4kRU7KPJhOxTS2oQYH2M14PIXJzJrgUyUmrB-1wx90SDYiIV262zfrSpRGDBRvHwKtXun07YeasXDRx1fs2ViXoP6wKHPYyXaAjqFBFx3QyNRTKqLQEyL4pXXwLh22AJozZLsvtuJ1M9tP_hpUIJUGHxQo1BGUwTkky7d8eTzi_3s4F-E6naNoZKpg5r3VNBYjQHI5r91wTj6WQnysn1S7tlx0Ok-5DiKE0d_vzy0003__mC0)  

- d) Class Diagram (Biểu Đồ Lớp)
    ![Diagram](https://www.planttext.com/plantuml/png/R9D1JiGm34NtFSKiOJ5NG3CI2rWW94Q8jKb_MuiqBOupq46SZ0L7uWeefRHDfzb4UKxidn_dv-jxvvL4Gsspp5ZoVdDDIdVag4GDfvkFRDCFWG4V4QCNbmDhf2J7fnHw9PUJv4lUIcFWVSBwYbnq0_oSQzYBgVZ8hXmbU6q4DnmdDcIJJCzaNaAR845_865rVx63DXAdbWncMa3ktkPBBKyWhI0HZqeKTGiX3OA1LA7cdBKRbc_iyaCBvFzQY5r1revUmFlfy5pdMFVHGswTGWeoc3m0YQcIEnLizK_VY5u3f4j82HS5um5j8pfYlCVbilG19WXhjz865BHgX4_Oc_YQOoBRb7kZV6HbJ1JEIDVEyY-QQxkzclkx5aviMDjmBhRVDRNFMf4qkf8YTN-POiMWSwtP3YwF7-iN003__mC0) 

### 2.3.3 Phân tích Ca Sử Dụng Hệ thống Bảo trì Trạm (Station Maintenance System)

- a) Xác định các lớp phân tích

    - MaintenanceRequest (Yêu cầu bảo trì)  
    - Technician (Kỹ thuật viên)  
    - StationEquipment (Thiết bị trạm)  
    - MaintenanceSchedule (Lịch bảo trì)  
    - NotificationSystem (Hệ thống thông báo)  
    - UserInterface (Giao diện người dùng)  

---

- b) Nhiệm vụ của từng lớp phân tích

    - MaintenanceRequest (Yêu cầu bảo trì):  
        - Tiếp nhận và quản lý yêu cầu bảo trì từ người dùng hoặc hệ thống tự động.  
        - Ghi nhận thông tin về vấn đề xảy ra, thiết bị liên quan, và mức độ ưu tiên.  

    - Technician (Kỹ thuật viên):  
        - Quản lý danh sách kỹ thuật viên được phân công bảo trì.  
        - Cập nhật tình trạng hoàn thành các yêu cầu bảo trì.  
        - Theo dõi hiệu suất và lịch sử công việc của từng kỹ thuật viên.  

    - StationEquipment (Thiết bị trạm):  
        - Lưu trữ thông tin về thiết bị trong trạm, bao gồm tình trạng hiện tại và lịch sử bảo trì.  
        - Cung cấp thông tin cần thiết để hỗ trợ bảo trì.  

    - MaintenanceSchedule (Lịch bảo trì):
        - Tạo và quản lý lịch bảo trì định kỳ cho các thiết bị trong trạm.  
        - Đảm bảo thời gian bảo trì không ảnh hưởng đến hoạt động của hệ thống.  

    - NotificationSystem (Hệ thống thông báo): 
        - Gửi thông báo đến kỹ thuật viên và quản lý về yêu cầu bảo trì mới hoặc lịch bảo trì định kỳ.  
        - Cảnh báo khi có thiết bị yêu cầu bảo trì khẩn cấp hoặc vượt thời gian bảo trì dự kiến.  

    - UserInterface (Giao diện người dùng):  
        - Cung cấp giao diện để người dùng gửi yêu cầu bảo trì và theo dõi trạng thái.  
        - Hỗ trợ quản lý theo dõi lịch sử bảo trì và cập nhật tình trạng thiết bị.  

### Mô tả Use case 
### Hệ thống Bảo trì Trạm

| **Tiêu đề**        | **Nội dung**                                                                                 |
|---------------------|---------------------------------------------------------------------------------------------|
| **Tên Use Case**    | Hệ thống Bảo trì Trạm                                                                       |
| **Actor**           | Bảo trì Trạm                                                                                |
| **Mô tả**           | Cho phép quản lý và xử lý các yêu cầu bảo trì, bao gồm cả bảo trì định kỳ và khẩn cấp, đảm bảo trạm hoạt động ổn định và liên tục. |
| **Các lớp phân tích** | **Boundary**: Giao diện người dùng<br>**Controller**: Lịch bảo trì, Hệ thống thông báo<br>**Entity**: Yêu cầu bảo trì, Kỹ thuật viên, Thiết bị trạm |
| **Luồng sự kiện chính**   | 1. Bảo Trì Trạm gửi yêu cầu bảo trì qua Giao Diện Người Dùng.<br>2. Giao Diện Người Dùng ghi nhận yêu cầu bảo trì và chuyển tiếp yêu cầu này đến Yêu Cầu Bảo Trì.<br>3. Yêu Cầu Bảo Trì xác định lịch bảo trì và chuyển thông tin đến Lịch Bảo Trì.<br>4. Lịch Bảo Trì phân công công việc bảo trì cho Kỹ Thuật Viên.<br>5. Nếu cập nhật tình trạng bảo trì:<br>- Kỹ Thuật Viên cập nhật tình trạng bảo trì cho Yêu Cầu Bảo Trì.<br>- Yêu Cầu Bảo Trì cập nhật trạng thái thiết bị trạm trong Thiết Bị Trạm.<br>- Thiết Bị Trạm ghi nhận tình trạng thiết bị và gửi thông tin trở lại Yêu Cầu Bảo Trì.<br>- Yêu Cầu Bảo Trì thông báo kết quả bảo trì cho Hệ Thống Thông Báo.<br>- Hệ Thống Thông Báo gửi thông báo kết quả bảo trì đến Bảo Trì Trạm.<br>6. Yêu Cầu Bảo Trì cung cấp kết quả yêu cầu bảo trì cho Giao Diện Người Dùng. |
| **Luồng sự kiện phụ** | 5a. Yêu cầu bảo trì khẩn cấp:<br>- Yêu Cầu Bảo Trì gửi cảnh báo khẩn cấp qua Hệ Thống Thông Báo.<br>- Hệ Thống Thông Báo gửi thông báo về yêu cầu bảo trì khẩn cấp đến Kỹ Thuật Viên. |

- c) Sequence Diagram (Biểu đồ trình tự)
    ![Diagram](https://www.planttext.com/plantuml/png/d9InRXD148RxVOhHzNu15rOKWW01AV21bFAytdXNFi_PTtCHBgbIk26YfZ0MYeXiAKWqkIrIR9Jtc2VW5T2UZUsppu1eJ_j_-yy__zvFUt-KKPHIFeY5oFe68Kqo9GGPYXK4pzbUGgZPNc4FZhcO9H2cRWvXoiLq00reFqxXuIFRJn3cN5mZX6o_1q94af8KWZr90546RpEL2eLaQ0p1cRl9uGaNr_dM1UMnrv51KXYXL6_KA5SPhKKlsTv1g7Ck5WJlZBl1KX4ggT584-7wPAWD5_S4nsmdsnxQ5959yEaeDyE1GX8oGKgJ689NR2TI_y5CMshLpMCbEacEtIWTG_3CH0cS6BQN2AUznrksdmsSk3lihGT-WQJIyqYgpKsLT4FjVlYGtJGfDQS9cNCZIvVjSKPg88JdGADLvK4JUcmN1iO-ILacsIdDK-hcedgsqQg9rHEq0THSBF00faPLPVrE1PhmtaqbF5ondQ26U1bdFMejQhIsbWTD66ht1K6MaMoa87K2VRzxMkt-mkzUY2Wctw75S3a40RavQY2_xmf10C3sJOVoa8TXctnAM7qmk_NQGwvWfDtK0ArAsc4xAQ5xyiRVzrPrkOUizxdVidMTQ5d8Zflwp3rhb7CnsmspXh1gA3J_XQ6mkzpVMLtleA-v-8R--zVX_yqXkPYXNddOfTMxhrHnUuOBjX_g7qWLNGvLxtJtxSeSUqjL9Q7wLoYE57Rzl_eN0000__y30000)  

- d) Class Diagram (Biểu Đồ Lớp)
    ![Diagram](https://www.planttext.com/plantuml/png/Z5H1JiCm4Bpx5JssXtu1bKCb8b5KDI3EnjcagyPskbvNgb1Vne4dyGMKX3XEam8vxentPdTM-VhuN3cMn5wNGgXIEZVRI3GCHXe5EpXwS3nx5xFc8r20fwuyN_HbIrdYd8TGAssnFdgiD9YUw82tX9QGp_E5k7IApw3s1XLA4vIqDBA07dZ4ICzNcUJEHSgIlGiOarI7BL1kITSZ385NIuS7T6nfOA3kWTO4my56pOHGJankhuQEbjNtRGaLsHDc435-tWVP24hL7Z9VGb1M1993EJHjzxA3mfUIelU10CPvWWqQrB9Cpuv19xgIYcFX9ykOesg6RZdzn62o60wDPGd4VI33-gQnHL7G9bjhe0ACEj_NZ5Z-nG4bXe5ogVg9dN_JoDUtrSGs7NMxY-krjySHCWjlBa9CNFPoUJTA_nQl7rv45riZumU_CBfCnUZgRhJwYvTs3QVkwShuHFB_Oqpf3NEyuNvCYiJ6u2WCiGAJrR-dRm000F__0m00)

### 2.3.4 Phân tích Ca Sử Dụng "Hệ thống Quản lý Năng Lượng (Power Management)"

- a) Xác định các lớp phân tích

    - EnergySource (Nguồn năng lượng)  
    - EnergyConsumption (Tiêu thụ năng lượng)  
    - EnergyStorage (Lưu trữ năng lượng)  
    - PowerControlSystem (Hệ thống điều khiển năng lượng)  
    - NotificationSystem (Hệ thống thông báo)  
    - UserInterface (Giao diện người dùng)  


- b) Nhiệm vụ của từng lớp phân tích

    - EnergySource (Nguồn năng lượng):  
        - Quản lý các nguồn năng lượng như pin mặt trời, máy phát điện, hoặc lưới điện.  
        - Cung cấp thông tin về trạng thái hiện tại và công suất đầu ra của từng nguồn.  

    - EnergyConsumption (Tiêu thụ năng lượng):  
        - Theo dõi lượng năng lượng được tiêu thụ bởi các thiết bị và hệ thống.  
        - Đưa ra các phân tích để tối ưu hóa tiêu thụ năng lượng.  

    - EnergyStorage (Lưu trữ năng lượng):  
        - Quản lý các hệ thống lưu trữ năng lượng như pin hoặc ắc quy.  
        - Đảm bảo lưu trữ năng lượng hiệu quả và cung cấp năng lượng khi cần thiết.  

    - PowerControlSystem (Hệ thống điều khiển năng lượng):  
        - Điều phối giữa các nguồn năng lượng, tiêu thụ và lưu trữ để đảm bảo hoạt động tối ưu.  
        - Cung cấp các chức năng chuyển đổi giữa các chế độ sử dụng năng lượng như tiết kiệm, khẩn cấp, hoặc tối đa hóa hiệu suất.  

    - NotificationSystem (Hệ thống thông báo):  
        - Gửi cảnh báo khi năng lượng đạt mức thấp hoặc khi phát hiện các sự cố trong hệ thống.  
        - Thông báo về lịch bảo trì cho các thiết bị liên quan đến năng lượng.  

    - UserInterface (Giao diện người dùng):  
        - Cung cấp thông tin về trạng thái năng lượng, mức tiêu thụ và dự báo sử dụng.  
        - Cho phép người dùng điều chỉnh cấu hình năng lượng và nhận thông báo.  

### Mô tả Use case 
### Hệ thống Quản lý Năng Lượng

| **Tiêu đề**        | **Nội dung**                                                                                 |
|---------------------|---------------------------------------------------------------------------------------------|
| **Tên Use Case**    | Hệ thống Quản lý Năng Lượng                                                                   |
| **Actor**           | Quản lý Năng Lượng                                                                            |
| **Mô tả**           | Cho phép người dùng theo dõi trạng thái năng lượng, điều chỉnh cấu hình tiêu thụ và nhận thông báo, đảm bảo hệ thống năng lượng hoạt động hiệu quả và ổn định. |
| **Các lớp phân tích** | **Boundary**: Giao diện người dùng<br>**Controller**: Hệ thống điều khiển năng lượng, Hệ thống thông báo<br>**Entity**: Nguồn năng lượng, Tiêu thụ năng lượng, Lưu trữ năng lượng |
| **Luồng sự kiện chính**   | 1. Quản lý Năng Lượng yêu cầu trạng thái năng lượng thông qua Giao Diện Người Dùng.<br>2. Giao Diện Người Dùng chuyển yêu cầu này đến Hệ Thống Điều Khiển Năng Lượng.<br>3. Hệ Thống Điều Khiển Năng Lượng kiểm tra trạng thái của Nguồn Năng Lượng.<br>4. Hệ Thống Điều Khiển Năng Lượng theo dõi mức Tiêu Thụ Năng Lượng.<br>5. Hệ Thống Điều Khiển Năng Lượng kiểm tra mức Lưu Trữ Năng Lượng.<br>- Nếu năng lượng đủ: Hệ Thống Điều Khiển Năng Lượng hiển thị trạng thái năng lượng lên Giao Diện Người Dùng.<br>6. Quản lý Năng Lượng yêu cầu điều chỉnh cấu hình năng lượng qua Giao Diện Người Dùng.<br>7. Giao Diện Người Dùng gửi yêu cầu điều chỉnh này đến Hệ Thống Điều Khiển Năng Lượng.<br>8. Nếu chế độ tiết kiệm năng lượng được chọn:<br>- Hệ Thống Điều Khiển Năng Lượng chuyển sang Nguồn Năng Lượng Tiết và tối ưu hóa Lưu Trữ Năng Lượng.<br>9. Quản lý Năng Lượng yêu cầu thông báo lịch bảo trì qua Hệ Thống Thông Báo.<br>10. Hệ Thống Thông Báo gửi thông báo lịch bảo trì đến Giao Diện Người Dùng. |
| **Luồng sự kiện phụ** | 5a. Nếu năng lượng thấp:<br>- Hệ Thống Điều Khiển Năng Lượng gửi cảnh báo năng lượng thấp đến Hệ Thống Thông Báo.<br>- Hệ Thống Thông Báo thông báo cho Quản lý Năng Lượng về tình trạng năng lượng thấp.<br>8a. Nếu chế độ tối đa hiệu suất được chọn:<br>- Hệ Thống Điều Khiển Năng Lượng chuyển sang Nguồn Năng Lượng Tối Đa và tối đa hóa Tiêu Thụ Năng Lượng. |

- c) Sequence Diagram (Biểu đồ trình tự)
    ![Diagram](https://www.planttext.com/plantuml/png/h9N1Qjj048Rl-nI3xtu17q9eKjhIO5hYFe0YRxHBvDsmcctnCUHWIYunEVNGWp4cjAGafUsXMaeECdcFUOA-Gj7Ak98YEQJqPjax__p_pBVoRtUxdM1Wq8vYnf8ZgS3eX3E64cCEdUVa9Z0GvAOgWjUMqhc2lUmNz9UdAeAzknjoSnL15_RlPh0y9tS10qlffO81kQyTne8GjO5EQsa7WWJU9Dmmhb3Y63hzo9AxK4tddYfkel6-jYRaw_C3cNsstkEYlMP7gyIEZb5gjIxSkxknC33ahZVqGcs2YBDGApGwhWraUIx9dLXuAIIvqqRBh_GxRdQAwlrnWdpKeZKGsNSLmPDifdrXNwCyb66GMruL7cYhXe4PG-UP33JiId8J1Vqex_THmcxsipJF5mgvEGn2pbZ-2DsjwjVGWt4-k93IImjeA9sf251aCmdAvuXNELYrhhlL4AgcLcH1gU0jkPEwNaDvTwkoNEZ1KJxI4Q09wkPMV3n2jBHzw04Ahc6O_P0m8lSf1FG0eGVeCKuBDAfM2yMgIlx1JzXTCnR4kC9a_VDoIkwI0K3JN1lM9WhOSiDdcnV7uuJNkw6WT76yeTrzyA074RalCj_kN0auo6Qwdh4aso2mIk67xz7O8C7Li1tPvRIuSQ4Wzrw9tD72WiYkbFWtQejW9NOtT2YsjoCelVLB-m0eARr53y1aL3VGFk8Qwg6mOx_I951H2z_LLWzhh-54SbC9EO4Y-nQKMVHqLDBueyjfu16RM4WifGlytq5erUL1tTgr_Uik3rAnMBx3LO0QQRx_gl8ynkJEGW47bCureCckM3lAPIWBXZOhiMskXlcVx1y0003__mC0)  

- d) Class Diagram (Biểu Đồ Lớp)
    ![Diagram](https://www.planttext.com/plantuml/png/T5JBQiCm4BphAtni3lc5aX9IA2HfmOIU5sdjgCWh8wqItD8lww6Vr5yeYVn--AYPdPtPNVptyxln38v3OOIG1hnFTeGkhr8RdCJaIoJthm227FkGVrZLMEdiHIjC6JXCNby3bu7Vx1NTmqfy3vjiBVbGbAmjTPqiQROk4auUScmbWS1KdpYfRGcsP5teXd7oE6sPidMGZuFLhsdb6Oik0v8FhaaTARiiqr8ZoMgSDDBUpqX7H8Mgt_kUVsk9dJMnIMj0MkkK9k25wSfOjHnwi9feiiNyLRCyH-nWrLssDNMqh3CjuQOsCkMHr9D1nwqItSZLtbwZsEZz09eO2KXYAi-eWkbvG59H_Xcq2GuRuTR8oQDx8KQNGU_abFQbWQe9DZYk6kkDOuyND1q1r4VmNDSYiwQy0nrAr1Vivwy7CxZzzVfnvawJAMbckmsflhPvbfWfd6swH9pPe1WESydUb3NL4cA3f6v_Xdy0003__mC0)

### 2.3.5 Phân tích Ca Sử Dụng Hệ thống Giám sát Cảm biến (Instrument Monitoring System)

- a) Xác định các lớp phân tích

    - Sensor (Cảm biến)  
    - MonitoringSystem (Hệ thống giám sát)  
    - DataLogger (Ghi dữ liệu)  
    - NotificationSystem (Hệ thống thông báo)  
    - UserInterface (Giao diện người dùng)  
    - MaintenanceSchedule (Lịch bảo trì)  


- b) Nhiệm vụ của từng lớp phân tích

    - Sensor (Cảm biến):  
        - Thu thập thông tin thời gian thực về các thông số môi trường (nhiệt độ, độ ẩm, áp suất, v.v.).  
        - Báo cáo trạng thái hoạt động của chính nó, bao gồm tuổi thọ và hiệu suất.  

    - MonitoringSystem (Hệ thống giám sát):  
        - Theo dõi dữ liệu từ các cảm biến được kết nối.  
        - Phân tích dữ liệu để phát hiện các bất thường hoặc sự cố trong hoạt động.  

    - DataLogger (Ghi dữ liệu):  
        - Lưu trữ dữ liệu từ cảm biến trong một khoảng thời gian cụ thể.  
        - Hỗ trợ xuất dữ liệu cho các mục đích phân tích hoặc báo cáo.  

    - NotificationSystem (Hệ thống thông báo):  
        - Gửi cảnh báo về các sự cố hoặc bất thường trong hệ thống cảm biến.  
        - Thông báo nhắc nhở lịch bảo trì định kỳ cho các cảm biến.  

    - UserInterface (Giao diện người dùng): 
        - Hiển thị thông tin trạng thái của các cảm biến.  
        - Cho phép người dùng truy cập, tìm kiếm, và phân tích dữ liệu từ hệ thống.  

    - MaintenanceSchedule (Lịch bảo trì):  
        - Quản lý và theo dõi các lịch bảo trì cho từng cảm biến.  
        - Đảm bảo bảo trì đúng hạn để tăng tuổi thọ và hiệu quả hoạt động của cảm biến.  

### Mô tả Use case 
### Hệ thống Giám sát Cảm biến

| **Tiêu đề**        | **Nội dung**                                                                                 |
|---------------------|---------------------------------------------------------------------------------------------|
| **Tên Use Case**    | Hệ thống Giám sát Cảm biến                                                                   |
| **Actor**           | Giám sát Cảm biến                                                                            |
| **Mô tả**           | Cho phép người dùng giám sát dữ liệu cảm biến, nhận cảnh báo bất thường và xem lịch bảo trì, đảm bảo hoạt động ổn định của hệ thống cảm biến. |
| **Các lớp phân tích** | **Boundary**: Giao diện người dùng<br>**Controller**: Hệ thống giám sát, Hệ thống thông báo<br>**Entity**: Cảm biến, Ghi dữ liệu, Lịch bảo trì |
| **Luồng sự kiện chính**   | 1. Giám sát Cảm biến yêu cầu xem thông tin cảm biến thông qua Giao Diện Người Dùng.<br>2. Giao Diện Người Dùng gửi yêu cầu này đến Hệ Thống Giám sát.<br>3. Hệ Thống Giám sát thu thập dữ liệu từ Cảm Biến.<br>4. Cảm Biến cung cấp dữ liệu cảm biến cho Hệ Thống Giám sát.<br>5. Hệ Thống Giám sát lưu trữ dữ liệu cảm biến vào Ghi Dữ Liệu.<br>6. Ghi Dữ Liệu xác nhận việc lưu trữ dữ liệu cho Hệ Thống Giám sát.<br>- Nếu phát hiện bất thường: Hệ Thống Giám sát gửi cảnh báo bất thường và Hệ Thống Thông Báo thông báo cho Giám sát Cảm biến về sự cố.<br>7. Giám sát Cảm biến yêu cầu xem lịch bảo trì của cảm biến qua Lịch Bảo Trì.<br>8. Lịch Bảo Trì cung cấp thông tin lịch bảo trì qua Giao Diện Người Dùng.<br>9. Giao Diện Người Dùng hiển thị lịch bảo trì cảm biến cho Giám sát Cảm biến.<br>- Nếu cảm biến cần bảo trì: Lịch Bảo Trì thông báo và Hệ Thống Thông Báo gửi thông báo bảo trì đến Giám sát Cảm biến. |
| **Luồng sự kiện phụ** | Không có |

- c) Sequence Diagram (Biểu đồ trình tự)
    ![Diagram](https://www.planttext.com/plantuml/png/b9H1Qjj068NtSug7zxw05oOuXhJWceBT0yZoH1eg_nD6lqgoB5raaKr3rrsO409jGXFefff55Yg-nvoWLoWpDew4v4AtqhnFRzvxw8zzFievCboiCY7ozufWT2w5OCMPHE-LivUOfyvUKu8JLQrNoAiruzYLDokCb2kV2NtCDcly_kpi5ymBLzuHviu-zOI8OjO6lPPm4OGzH3dUvT88IQpu0hqwDhoTISgr4R4cDZexw2USVQD9iJQAajb5pdArfvwa2cDdVs2YdBqimk5nnD549uay19-drKzACAhMEWYccjMfYYDMcdRyXIve6Hd_1HLfZ3sTC4qsZyv-LHXNloZPt_4riJIdKIptjYRENiKfHgwyqPYRwdvxYqWHIueebhCubSiYaq9u0Fh39WW3N5JV2iIkl2jmBbVWhMTMv1_kSnPDMN_OYgg9Mlgiif1LazEIzOUxXZ00fmKuTUN3MGF0pdvlKdQARXjnGOa_VdlsVpPU-iG0sUQn01klFmYf2RgTd5Vh6EGlH0U0GaGPustgTvrkor-uyfR1QPW09G90czqVTgm90oJEFgZWab8ighNkn4tRqjqoGWbX0K7ymTcFo9rzGkpijP2qV1bInyhQSygs0rs4WRAfxaMNh6EMjH9haynQkDOkTxVmONuYloPxrPOrUmmT78UVJeqSSkyssnbzFJSVG0lspzItnTKPDNN8_KZIqlzY_m800F__0m00)  

- d) Class Diagram (Biểu Đồ Lớp)
    ![Diagram](https://www.planttext.com/plantuml/png/X5FBJiCm4BpxAtfi3_q5H2KEHQ8S6lY0nPcc5iwwMcyG0V5b7FWaVW6vIVDe8f6ZTpGpExFv_VwvZKgYLUcDiPvYN6JW66JnQHRdpmRlONKFya-kn1qfBLVjJ70AefcILh5xB0Cx3R85UJqkL-RhGhnh1ewBh8wAifDG8VlQo8xeYSdN7sF970gh6mubUOSuv4-uXr0KwCr73O8PPe6AmzkO6kzfc_QfOtqCwWxEahh0LxuZEDzuY7OKdC3rveM397_QEBnebexp7JbMCB75KEKvGkvP8GUow0Ho5q-UwcQ1gvWZIEpntxmAC8GK-tDLexm6LZ9xH5xvNhaafW9ZiuEo1eEjIo7NVOeSAq4w5LzFbcrlQxs-cLo3cPn7GlMTpi-dxPZ16IJ4A5apq-OKD1TCGhNkpRYikMNcC3FInjo2y_Jl_G400F__0m00)

### 2.3.6 Phân tích Ca Sử Dụng Quản lý Cập nhật và Thay thế Cảm biến (Instrument Management)

- a) Xác định các lớp phân tích

    - Sensor (Cảm biến)  
    - InstrumentManagementSystem (Hệ thống quản lý cảm biến)  
    - MaintenanceTeam (Nhóm bảo trì)  
    - UserInterface (Giao diện người dùng)  
    - NotificationSystem (Hệ thống thông báo)  
    - InventorySystem (Hệ thống tồn kho)


- b) Nhiệm vụ của từng lớp phân tích

    - Sensor (Cảm biến):  
        - Cung cấp thông tin trạng thái và hiệu suất của cảm biến.  
        - Cung cấp dữ liệu về tuổi thọ, mức độ hao mòn và yêu cầu thay thế.

    - InstrumentManagementSystem (Hệ thống quản lý cảm biến):  
        - Theo dõi tình trạng hoạt động và yêu cầu thay thế cảm biến.  
        - Cập nhật và ghi nhận thông tin về các cảm biến mới hoặc thay thế.  
        - Quản lý lịch sử thay thế cảm biến và bảo trì.

    - MaintenanceTeam (Nhóm bảo trì):  
        - Thực hiện công tác thay thế cảm biến khi có yêu cầu.  
        - Kiểm tra và xác nhận tình trạng của các cảm biến mới được cài đặt.

    - UserInterface (Giao diện người dùng):  
        - Hiển thị thông tin về các cảm biến và tình trạng hoạt động của chúng.  
        - Cho phép người dùng theo dõi các yêu cầu thay thế cảm biến và lịch bảo trì.

    - NotificationSystem (Hệ thống thông báo):  
        - Gửi thông báo về các cảm biến cần thay thế hoặc bảo trì.  
        - Cung cấp thông báo cho nhóm bảo trì và người dùng khi cảm biến mới được cài đặt hoặc thay thế.

    - InventorySystem (Hệ thống tồn kho):  
        - Quản lý tồn kho cảm biến mới và các bộ phận thay thế.  
        - Cập nhật thông tin về tình trạng sẵn có của các cảm biến và bộ phận thay thế.

### Mô tả Use case 
### Quản lý Cập nhật và Thay thế Cảm biến

| **Tiêu đề**        | **Nội dung**                                                                                 |
|---------------------|---------------------------------------------------------------------------------------------|
| **Tên Use Case**    | Quản lý Cập nhật và Thay thế Cảm biến                                                       |
| **Actor**           | Quản lý Cảm biến                                                                             |
| **Mô tả**           | Cho phép người dùng quản lý tình trạng cảm biến, tự động kích hoạt quy trình thay thế khi cần và cung cấp lịch sử thay thế cho người dùng. |
| **Các lớp phân tích** | **Boundary**: Giao diện người dùng<br>**Controller**: Hệ thống quản lý cảm biến, Nhóm bảo trì, Hệ thống thông báo<br>**Entity**: Cảm biến, Hệ thống tồn kho |
| **Luồng sự kiện chính**   | 1. Quản Lý Cảm Biến yêu cầu xem tình trạng cảm biến qua Giao Diện Người Dùng.<br>2. Giao Diện Người Dùng gửi yêu cầu này đến Hệ Thống Quản Lý Cảm Biến.<br>3. Hệ Thống Quản Lý Cảm Biến thu thập thông tin tình trạng cảm biến từ Cảm Biến.<br>4. Cảm Biến cung cấp trạng thái và yêu cầu thay thế (nếu có) cho Hệ Thống Quản Lý Cảm Biến.<br>   Nếu cảm biến cần thay thế:<br>- Hệ Thống Quản Lý Cảm Biến gửi thông báo yêu cầu thay thế cảm biến đến Hệ Thống Thông Báo.<br>- Hệ Thống Thông Báo thông báo cho Nhóm Bảo Trì về việc thay thế cảm biến.<br>- Nhóm Bảo Trì kiểm tra Hệ Thống Tồn Kho để xác nhận sự sẵn có của cảm biến thay thế.<br>- Hệ Thống Tồn Kho xác nhận sự sẵn có của cảm biến thay thế cho Nhóm Bảo Trì.<br>- Nhóm Bảo Trì thay thế cảm biến và thông báo cho Hệ Thống Quản Lý Cảm Biến.<br>- Hệ Thống Quản Lý Cảm Biến gửi thông báo thay thế hoàn thành đến Hệ Thống Thông Báo.<br>- Hệ Thống Thông Báo gửi thông báo hoàn thành thay thế đến Quản Lý Cảm Biến.<br>5. Quản Lý Cảm Biến yêu cầu theo dõi lịch sử thay thế cảm biến qua Giao Diện Người Dùng.<br>6. Giao Diện Người Dùng gửi yêu cầu lịch sử thay thế đến Hệ Thống Quản Lý Cảm Biến.<br>7. Hệ Thống Quản Lý Cảm Biến cung cấp thông tin lịch sử thay thế qua Giao Diện Người Dùng. |
| **Luồng sự kiện phụ** | Không có |

- c) Sequence Diagram (Biểu đồ trình tự)
    ![Diagram](https://www.planttext.com/plantuml/png/d9L1Qjj058RtSueVxtq1Bqn80sreOoXH3p2H9veXrfiWZKAqxYABRbgoB8KOKm8bXfOqYseeNap9FUO4lKAHx3WUOwiXEw6P_zF__lSU-cjdExdXcIdI4MFvYI9aEXUC6ML60fstXQycX3VkDrxuQdgAWVJLrE3CNI6Il4GaVJMhpoOfTfMlPeGk3k_7-FFHsqj4XQ-k2P6tFpgCyTZeR0aTpQ6J54UDi0EUurqkCYR8A5EYiufjJWy5vJfZiIQJwH4whxozg2tOJvGWz1eAzoatMP4ACWUSU2BgfyCoDo9zX0sakqsnwwk9HfIvcqPum1KPGPnY4GcUiYDTq91d9Jel5TVOKzvU40R9_NTlloZikL-KB0lP9oEoOnwBBOuZwNvIWbqtrerce8qwLZ4tIjF2tKCKeSxRIy9hELVjqvaWexDo8M7rfz7jXnRGG-c-5OXzTLtWNAGmxeOaJEQhCINr-sKdMAZizblo2xbcNf5H509RzDt-egtemSWQqGpQ2gd5w4BvFuTnCHT-FLrYZ7HZrSnnO9-NZO4POtnaWl5ihj3g5G1jd-tsDpGKFIJUJjL3VKTkh5UOONK0DY6w_VMnRA9x6czTsKGN311wE57UlazXCWxJpDg9r04AgRUVrIA1KBtHtRaRnw2wiuJSLtU4sDs6nBLWD_fiQN5RpSzeqfOufNPNjLLtHRAbFSq6FWqYQBXzOuqK6aDtfp3ozaCiaNixNKtgsOkwXTUUrBgzrRLwNDSjQBOZQ5Z_Plu1003__mC0)  

- d) Class Diagram (Biểu Đồ Lớp)
    ![Diagram](https://www.planttext.com/plantuml/png/X5JDJi904BxlKt2K0wzW83564a52CPx7xHGtR6Vhx1JI69_CWu_aAvXjQMaN0Zqr_URd-vdqx-TtwWLOojmgfIruFqgGlEFHbnhLJy5kRr9C1AJqT-FXrnLovZW7qlW00Z7yR3Bq1T00OomSoni2poZT8F3TM7sto-VaXSiSIHP0iCNmbbHUCEy82OFUDIGZKjPjrrXOq7NRa_7YkEhGiaX1i6cSK-Ow8AytzJhN-5cY5zydjW13WXIKRX1ER8h6WMPiRqOtVOziicg9XtQp5x0Mn3ZgQhIZpBH37alI0GLhfEfJUFN8SnBa33Hs15BZ2mlL1LsrKPTb7QaPFFHq9Ve3qz9YV-VIYScChkb6ENYaj3TzPf5FgYdqLP5f4Hhql6HHahrBs2E50AErJLfjbzExAE3P7eo5TnFSY-uZDcG5t8PyFFh9vFxA2Qehrnaw8xdgHlaWprl5aHqgliVpWSDp2VXvcEf2lfUe3QEuuPAQ8gNXX_8F003__mC0)

### 2.3.7 Ca sử dụng cho Quản lý Hệ thống Phần Mềm (Software Management)
- a) Xác định các lớp phân tích

    - Software (Phần mềm)
    - SoftwareManagementSystem (Hệ thống quản lý phần mềm)
    - DevelopmentTeam (Nhóm phát triển)
    - UserInterface (Giao diện người dùng)
    - NotificationSystem (Hệ thống thông báo)
    - VersionControlSystem (Hệ thống kiểm soát phiên bản)


- b) Nhiệm vụ của từng lớp phân tích

    - Software (Phần mềm):
        - Cung cấp thông tin về phiên bản phần mềm, tính năng và trạng thái hoạt động.
        - Quản lý các bản vá lỗi và nâng cấp phần mềm.

    - SoftwareManagementSystem (Hệ thống quản lý phần mềm):
        - Theo dõi trạng thái và yêu cầu cập nhật phần mềm.
        - Cập nhật và ghi nhận thông tin về các phiên bản phần mềm mới hoặc đã nâng cấp.
        - Quản lý lịch sử thay đổi phần mềm và các bản vá lỗi.

    - DevelopmentTeam (Nhóm phát triển):
        - Phát triển và kiểm tra phần mềm, bao gồm cả các bản vá lỗi và nâng cấp.
        - Xác nhận các thay đổi trong phần mềm trước khi triển khai.

    - UserInterface (Giao diện người dùng):
        - Hiển thị thông tin về các phiên bản phần mềm và trạng thái hoạt động của chúng.
        - Cho phép người dùng theo dõi các yêu cầu cập nhật và lịch sử thay đổi phần mềm.

    - NotificationSystem (Hệ thống thông báo):
        - Gửi thông báo về các bản vá lỗi hoặc cập nhật phần mềm mới.
        - Cung cấp thông báo cho nhóm phát triển và người dùng khi có bản cập nhật mới được triển khai.

    - VersionControlSystem (Hệ thống kiểm soát phiên bản):
        - Quản lý các phiên bản phần mềm và các thay đổi trong mã nguồn.
        - Cập nhật thông tin về trạng thái các phiên bản phần mềm và các nhánh phát triển.

### Mô tả Use case 
### Quản lý Hệ thống Phần Mềm

| **Tiêu đề**        | **Nội dung**                                                                                 |
|---------------------|---------------------------------------------------------------------------------------------|
| **Tên Use Case**    | Quản lý Hệ thống Phần Mềm                                                                   |
| **Actor**           | Quản lý Phần Mềm                                                                             |
| **Mô tả**           | Cho phép quản lý thông tin và trạng thái phần mềm, tự động thông báo và điều phối quy trình cập nhật khi cần, đồng thời cung cấp lịch sử thay đổi cho người dùng. |
| **Các lớp phân tích** | **Boundary**: Giao diện người dùng<br>**Controller**: Hệ thống quản lý phần mềm, Nhóm phát triển, Hệ thống thông báo<br>**Entity**: Phần mềm, Hệ thống kiểm soát phiên bản |
| **Luồng sự kiện chính**   | 1. Quản Lý Phần Mềm yêu cầu thông tin phần mềm qua Giao Diện Người Dùng.<br>2. Giao Diện Người Dùng gửi yêu cầu này đến Hệ Thống Quản Lý Phần Mềm.<br>3. Hệ Thống Quản Lý Phần Mềm thu thập thông tin về phần mềm từ Phần Mềm.<br>4. Phần Mềm cung cấp thông tin về phiên bản và trạng thái cho Hệ Thống Quản Lý Phần Mềm.<br>   Nếu phần mềm cần cập nhật:<br>- Hệ Thống Quản Lý Phần Mềm gửi thông báo cập nhật đến Hệ Thống Thông Báo.<br>- Hệ Thống Thông Báo thông báo cho Nhóm Phát Triển yêu cầu thực hiện cập nhật.<br>- Nhóm Phát Triển kiểm tra và cập nhật mã nguồn trong Hệ Thống Kiểm Soát Phiên Bản.<br>- Hệ Thống Kiểm Soát Phiên Bản xác nhận thay đổi phiên bản và gửi thông tin này đến Nhóm Phát Triển.<br>- Nhóm Phát Triển triển khai bản cập nhật vào Hệ Thống Quản Lý Phần Mềm.<br>- Hệ Thống Quản Lý Phần Mềm gửi thông báo cập nhật thành công đến Hệ Thống Thông Báo.<br>- Hệ Thống Thông Báo thông báo cho Quản Lý Phần Mềm về việc cập nhật hoàn tất.<br>5. Quản Lý Phần Mềm yêu cầu theo dõi lịch sử thay đổi phần mềm qua Giao Diện Người Dùng.<br>6. Giao Diện Người Dùng gửi yêu cầu lịch sử thay đổi đến Hệ Thống Quản Lý Phần Mềm.<br>7. Hệ Thống Quản Lý Phần Mềm cung cấp thông tin lịch sử thay đổi cho Giao Diện Người Dùng. |
| **Luồng sự kiện phụ** | Không có |

- c) Sequence Diagram (Biểu đồ trình tự)
    ![Diagram](https://www.planttext.com/plantuml/png/f9MzQXj154RxUOeFzNe15S8uWYGaDWvIqezMuvt1ktV4xgmJbI65YpGn9cL0Yma6Wo0cIH4D9iKOlySyGLuXpCe_Mach8cdKNDqpPxuxb_rZV-_aXcUcI1F6yYD5o7Gk63FA90AjLuMVdnDUkciyy_O40-djASKua7v-GTZpzdsADlgt9Mu-UNk6GL4L1jvUjHZZaT7P0oLnrxN65dYErxd8c22Zp0IjjMfV7vgtF1CiqcGodQ1LqrZIQspTuyHZaGeo_KbkHFg8sfVkUue3wKg3GQQy_K1LPqySYqIFGyj0y9GDTK4ZdatGUgguHazvUqBOZs-_UVj5eUT-KVnmb-TaH7R8eoRbWNG_ACQkAtNLiw-DEbGHDqhJdU1z6hM-5y4lHLy7smEft2LXDzo-ehmHMQuqFLaSUSTXmGVjRjqB7KpSPO78poyAc8MEKOJn8i4q9CZgBUrkOvmhkCpFoy2JhbHrOYDW2OuEZ0nIVZuRDxez_7kxLbHG7BI-hf2gw8RLmpbsqxeoOpm9yJwULbsCmkzi30fYXW5eFhZTtJ1JT11xErFt9aDNwdNcXhvsT_KvLXazGfR2N-EjThQx6nyAEZXQl2wJyIgJPH9ITmwA2s_FgA9kH6pqVEVAQ44X6Cadk3drzhEgpQ19TCjWpM9NSIIvkXla_u-dQJ2XC2M9A9ItJAdQjIqOgTqqf11WJD2eUJkD51eZzrCXyVPZ995xErlExr-NimctBQjLkSrBrKHcEu96uTFo5m00__y30000)  

- d) Class Diagram (Biểu Đồ Lớp)
    ![Diagram](https://www.planttext.com/plantuml/png/V5JBJiD03BplL_G8X_u2WhP2z015b7AtDawxOhCENgTLXFfb7FWaVW5jdiscROvhUsOyO-Nlv_VU2x0KcLLAM_1-igPK3i0u-LQJwikPzYR13sHlo2rTIZUtmz8ZWXICFdvVvSWWXXpOjO0KVKC63hRu2g9trTWnPd-k6Z9qiYwzODQf4GRzsNP5g9QsZSfDde2S26BKn4d5zsIy49UHb7hW3RyAz39GjC0zMig3b7U4NaXIlxTIEZn1BwD7JIurdCrtuBRePvWIum9pIsN0FQNRUEIb4-GKT9z1OdnkeMnn1o5KZepqrxMzmKDDsg_TKRsGcDJeAg78PO-kTgl6VR38GMLTT66kZ7o9gc4Dlqhx73hM9g4vEM6o4MyTHhjcq-g7gyufmSR8hb1KF3C6ftVTKHoLwevvEhsxU5lguj65gMXFTRLvaDxrrdC-gFZOnfZ3-mZrSOpgJB9ZfBD1NFL9tQDBmg_Y7m00__y30000)

### 2.3.8 Ca sử dụng cho Báo cáo và Cảnh báo (Reporting and Alerts)

- a) Xác định các lớp phân tích

    - Report (Báo cáo)
    - Alert (Cảnh báo)**
    - ReportingSystem (Hệ thống báo cáo)
    - AlertSystem (Hệ thống cảnh báo)
    - UserInterface (Giao diện người dùng)
    - NotificationSystem (Hệ thống thông báo)
    - Database (Cơ sở dữ liệu)


- b) Nhiệm vụ của từng lớp phân tích

    - Report (Báo cáo):
        - Chứa thông tin chi tiết và tổng quan về các sự kiện hoặc tình trạng trong hệ thống.
        - Cung cấp báo cáo theo yêu cầu từ người dùng hoặc hệ thống tự động.

    - Alert (Cảnh báo):
        - Chứa thông tin về các sự kiện bất thường hoặc cảnh báo cần được chú ý.
        - Cảnh báo người dùng hoặc các bên liên quan khi có tình huống khẩn cấp.

    - ReportingSystem (Hệ thống báo cáo):
        - Xử lý và tạo báo cáo từ dữ liệu có trong hệ thống.
        - Cung cấp giao diện cho người dùng để yêu cầu và truy cập các báo cáo.

    - AlertSystem (Hệ thống cảnh báo):
        - Xử lý và tạo các cảnh báo khi có sự kiện bất thường hoặc điều kiện khẩn cấp.
        - Cung cấp giao diện để người dùng cài đặt và theo dõi các cảnh báo.

    - UserInterface (Giao diện người dùng):
        - Hiển thị các báo cáo và cảnh báo cho người dùng.
        - Cho phép người dùng yêu cầu báo cáo, theo dõi tình trạng cảnh báo và tùy chỉnh cài đặt.

    - NotificationSystem (Hệ thống thông báo):
        - Gửi thông báo cho người dùng hoặc các bên liên quan khi có cảnh báo hoặc báo cáo quan trọng.
        - Cung cấp thông báo qua email, SMS, hoặc các phương tiện khác.

    - Database (Cơ sở dữ liệu):
        - Lưu trữ dữ liệu cần thiết để tạo báo cáo và cảnh báo.
        - Cung cấp các truy vấn để lấy thông tin phục vụ cho báo cáo và cảnh báo.

### Mô tả Use case 
### Báo cáo và Cảnh báo

| **Tiêu đề**        | **Nội dung**                                                                                 |
|---------------------|---------------------------------------------------------------------------------------------|
| **Tên Use Case**    | Báo cáo và Cảnh báo                                                                          |
| **Actor**           | Người dùng                                                                                 |
| **Mô tả**           | Cho phép người dùng yêu cầu và xem báo cáo, tạo và xem cảnh báo dựa trên dữ liệu, đồng thời gửi thông báo khẩn cấp khi cần. |
| **Các lớp phân tích** | **Boundary**: Giao diện người dùng<br>**Controller**: Hệ thống thông báo, Hệ thống báo cáo, Hệ thống cảnh báo<br>**Entity**: Cơ sở dữ liệu, Báo cáo, Cảnh báo |
| **Luồng sự kiện chính**   | 1. Người Dùng yêu cầu báo cáo thông qua Giao Diện Người Dùng.<br>2. Giao Diện Người Dùng gửi yêu cầu tạo báo cáo đến Hệ Thống Báo Cáo.<br>3. Hệ Thống Báo Cáo truy vấn dữ liệu từ Cơ Sở Dữ Liệu.<br>4. Cơ Sở Dữ Liệu cung cấp dữ liệu cho Hệ Thống Báo Cáo.<br>5. Hệ Thống Báo Cáo hiển thị báo cáo qua Giao Diện Người Dùng.<br>6. Giao Diện Người Dùng hiển thị báo cáo cho Người Dùng.<br>   Nếu báo cáo hoàn thành:<br>- Người Dùng yêu cầu cảnh báo thông qua Giao Diện Người Dùng.<br>- Giao Diện Người Dùng gửi yêu cầu tạo cảnh báo đến Hệ Thống Cảnh Báo.<br>- Hệ Thống Cảnh Báo truy vấn dữ liệu cảnh báo từ Cơ Sở Dữ Liệu.<br>- Cơ Sở Dữ Liệu cung cấp dữ liệu cảnh báo cho Hệ Thống Cảnh Báo.<br>- Hệ Thống Cảnh Báo hiển thị cảnh báo qua Giao Diện Người Dùng.<br>- Giao Diện Người Dùng hiển thị cảnh báo cho Người Dùng. |
| **Luồng sự kiện phụ** | 6a. Nếu không có báo cáo: Giao Diện Người Dùng thông báo lỗi cho Người Dùng.<br>6b. Nếu có cảnh báo khẩn cấp:<br>- Hệ Thống Cảnh Báo gửi thông báo khẩn cấp đến Hệ Thống Thông Báo.<br>- Hệ Thống Thông Báo gửi thông báo khẩn cấp đến Người Dùng. |

- c) Sequence Diagram (Biểu đồ trình tự)
    ![Diagram](https://www.planttext.com/plantuml/png/Z5HDRjD05DxFAJvvdmja4HKQ2H2e2n8EC76czgZkJ3L-hkGrYoxOW5YmGYH2LGKI0WGRF0iMHhd7dA1NgCQEZEqwIJUMxFU-d_Uz6T_QlqSfSKFPUS9OUYOLZ4u5OoGf4GWUbskDO_-uB5SuTiLd5QFwEC9iiyQ_jyw-npnpnOt2tDcV0MCy96qGd4IR7yv-b9YMVrGKWATubGh3X299UOkwAhqK5zfGKsmfLUL7YJ34Ggt8w0J1KsUlC8-TVQSY31595StobCJv3imW_nQnq9bQSfCZU2AvnbGwUwMmOvndYeGvvQ7O8JIFozzRZnNcH9CybI4dgTLMhvbviyRCsK-OEliTBxniLc6cdFY2-wruHOmcNMMCaPTVCuIkkCcmy6c4vLgpRjDeqe-cYoDNh7KBtMyUJHeV68DCbkFI5TSAI-ysgToofcDGBSnKvDMkBpgW0QN-VB5qzhK2nSw-sJTXbS_ETiOJga-BVqMiovLlAbSgPW3mW7J3-jnupWRIST0wI4Fvzl7jzeSaZ3v1E_6kzd3QXnpiJVxWz4Fvjq4YIGMUrrSYB7-rThEFZcf0rPmu-q4oePRrDhVtk2gTnQxuekgHXqQxV_KmHkJiDzbHk4SpWFllxG2-CdearDB_N-y0003__mC0)  

- d) Class Diagram (Biểu Đồ Lớp)
    ![Diagram](https://www.planttext.com/plantuml/png/Z9J1JiCm38RlVOeTuT1Nc3Pj875XOWZk8VL6f3GfjbkO44_6WKVY5L2IahL9aEZHl-FFlstr-_DhHIoG-rPNbTI2QB67pY8ltgk5_uvW00N35bWe3KsGBouJUJS03WfU4xb3EwW6GfHsPWylFP3JFtvvQmqJd4GG33uMYnZBwd1w8C0OQgrHR763YfKK-ce0mpIj6eZA7EzFnD36-XrQ2KH1tWeMcPEnrxA56yE01o4XSr3cUAc8yKf6yT4YnDcFGiGqYZejJcdFRXC90CFaqynna34vycxTq9KKhAn9l16OnZ-OviIAJWsKednU9ZqgiNaMne2UaTsudWITJH9R7ES_6wMFvnE6Dv0zmrqFg82kBQQUiuJrnFru_dMzJ6-e2fVgbCd6g_JIwdePBOGd9M6-pX8jpvXI2-jnARD7VoNzeqxQJDn93gbMO1ht__W1003__mC0)

### 2.3.9 Phân tích Ca Sử Dụng Quản lý Thông tin Liên Lạc (Communication Management)

- a) Xác định các lớp phân tích

    - Message (Tin nhắn)
    - CommunicationSystem (Hệ thống liên lạc)
    - User (Người dùng)
    - NotificationSystem (Hệ thống thông báo)
    - MessageQueue (Hàng đợi tin nhắn)
    - UserInterface (Giao diện người dùng)


- b) Nhiệm vụ của từng lớp phân tích

    - Message (Tin nhắn):
        - Chứa thông tin về nội dung và thông tin liên lạc giữa các bên.
        - Lưu trữ trạng thái của tin nhắn, bao gồm trạng thái đã gửi, đã nhận, hoặc bị lỗi.

    - CommunicationSystem (Hệ thống liên lạc):
        - Quản lý việc gửi, nhận và xử lý tin nhắn trong hệ thống.
        - Đảm bảo tin nhắn được chuyển đến đúng người nhận và theo dõi các sự kiện liên quan đến tin nhắn.

    - User (Người dùng):
        - Người gửi hoặc nhận tin nhắn trong hệ thống.
        - Thực hiện các thao tác như gửi tin nhắn, nhận tin nhắn và truy cập vào thông tin liên lạc.

    - NotificationSystem (Hệ thống thông báo):
        - Gửi thông báo cho người dùng khi có tin nhắn mới hoặc các thay đổi quan trọng.
        - Cung cấp thông báo qua các phương tiện như email, SMS hoặc các hệ thống thông báo trong ứng dụng.

    - MessageQueue (Hàng đợi tin nhắn):
        - Quản lý việc lưu trữ và xử lý tin nhắn trong hệ thống.
        - Đảm bảo tin nhắn được gửi và nhận theo đúng thứ tự và thời gian.

    - UserInterface (Giao diện người dùng):
        - Hiển thị thông tin về các tin nhắn gửi đi và nhận được.
        - Cho phép người dùng gửi, xem và quản lý tin nhắn trong hệ thống.

### Mô tả Use case 
### Quản lý Thông tin Liên Lạc

| **Tiêu đề**        | **Nội dung**                                                                                 |
|---------------------|---------------------------------------------------------------------------------------------|
| **Tên Use Case**    | Quản lý Thông tin Liên Lạc                                                                   |
| **Actor**           | Người dùng                                                                                 |
| **Mô tả**           | Cho phép người dùng gửi và nhận tin nhắn, xử lý các trường hợp gửi thành công và thất bại, đồng thời thông báo cho người dùng về tin nhắn mới. |
| **Các lớp phân tích** | **Boundary**: Giao diện người dùng<br>**Controller**: Hệ thống thông báo, Hệ thống liên lạc<br>**Entity**: Tin nhắn, Hàng đợi tin nhắn |
| **Luồng sự kiện chính**   | 1. Người Dùng gửi tin nhắn thông qua Giao Diện Người Dùng.<br>2. Giao Diện Người Dùng chuyển tin nhắn đến Hệ Thống Liên Lạc.<br>3. Hệ Thống Liên Lạc thêm tin nhắn vào Hàng Đợi Tin Nhắn.<br>4. Hàng Đợi Tin Nhắn xác nhận tin nhắn đã được thêm vào hàng đợi và gửi thông báo lại cho Hệ Thống Liên Lạc.<br>5. Hệ Thống Liên Lạc cập nhật trạng thái tin nhắn và gửi lại cho Giao Diện Người Dùng.<br>6. Giao Diện Người Dùng hiển thị thông tin tin nhắn cho Người Dùng.<br>   Nếu tin nhắn đã gửi thành công:<br>- Hệ Thống Liên Lạc gửi thông báo về tin nhắn mới đến Hệ Thống Thông Báo.<br>- Hệ Thống Thông Báo thông báo tin nhắn mới đến Người Dùng.<br>7. Người Dùng yêu cầu kiểm tra tin nhắn qua Giao Diện Người Dùng.<br>8. Giao Diện Người Dùng gửi yêu cầu tin nhắn đến Hệ Thống Liên Lạc.<br>9. Hệ Thống Liên Lạc truy vấn tin nhắn từ Hàng Đợi Tin Nhắn.<br>10. Hàng Đợi Tin Nhắn trả về tin nhắn cho Hệ Thống Liên Lạc.<br>11. Hệ Thống Liên Lạc hiển thị tin nhắn qua Giao Diện Người Dùng.<br>12. Giao Diện Người Dùng hiển thị tin nhắn cho Người Dùng. |
| **Luồng sự kiện phụ** | 6a. Nếu tin nhắn gửi không thành công:<br>- Hệ Thống Liên Lạc thông báo lỗi gửi tin nhắn qua Giao Diện Người Dùng.<br>- Giao Diện Người Dùng thông báo lỗi gửi tin nhắn đến Người Dùng. |

- c) Sequence Diagram (Biểu đồ trình tự)
    ![Diagram](https://www.planttext.com/plantuml/png/d9H1Qjj058RtSug7zhg05oQqWQRW6aBK0qpaYJHOUbEa6LCjInTPT5FJHHUb465Am63QGZVLKBgOa7lC2Ng5CfBJIB4KN2yblN_c___teJ_wzr4kQIPLcX2Ippb29d96YEGoOU2TAbkj42Rc5mIn-O4H11nXmiqQOMAhCWGVpcvBk7blzGS8bAsk4GAhltk4q52A3BnfTFlDwiySZirFZ3oWERpCMKOOIYuByDo16DlgAzRVNh0yfn4ZeK2PYGIy4wil8OYjNcBKlhcUVYhIL24FgUG2pufSidH0kRN_n9IYLaw5v1TTuPsZ4tE5KHrfnUkyqnrxfuefHiw5mXdD2l2USIhWc5jzYJ0G-3bAbbtGa17Y7i4VTr_322AhDnpalq98Ty0Vz-M54OInAgn-YsrftwG_xlY74SZOhDEM31RcIa3S5B1q1P2EOj32QrE6zHcRVLmy31xQQlEgaKkGcQrAZ9otyl4swXv74FCcV6prEwToUtQobfJGHDQhtCQyMPhLNTqkRGoXan40w0teZtk0kTzOS-UvAKMxozJgJxm-iaTxRry-fcP9pjh6cmldsv1xMdzOT_l6nEgFZScXUdUcTpbbE1kcUkxMauBCw05e5sQj71xNwW2uCrN0mbPVEYZinxE3S0KBgzySW7CNoFy5k4Nj4SEP-pF_1G00__y30000)  

- d) Class Diagram (Biểu Đồ Lớp)
    ![Diagram](https://www.planttext.com/plantuml/png/d5F1QiCm3BtxAt9i3_s5KSW6ws4jfTi724T9p1AvM4f66Fko7VP9-uNXuYREwi2OZzAJdjwJ_FtvjMK19rtRAAKROCwUa1agpDvLTdairc48vfO4ILRha1C7-ZNaJWBIyPXgWQ32A8UhjVguakIsRJio6iHOEWqis4w4I4Me6xivr6Xw_1q-EwkHEOGvETT3ZoGSaxymkl-mWOx87eqtPeZxxgsOSbdJ7jz2RGmSkvCF3dwsGvdNGB6UItbKnC-rirrLUnnXCrCNE8uTTkabyf9zEpgu0brwXVVOc1xdWlsmEn9q9UY9gp1yRc2uOKivtPlHbCdG17jGUBtDpUOkTK8gTLOU6tko2F9gL6A7OsxcxD88Sq_-ZhebJe1cEjGMgV0VzmS00F__0m00)

### 2.3.10 Ca sử dụng cho Quản lý Môi Trường và Điều Kiện Thiên Nhiên (Environmental Monitoring and Management)

- a) Xác định các lớp phân tích

    - EnvironmentalSensor (Cảm biến môi trường)
    - MonitoringSystem (Hệ thống giám sát)
    - DataLogger (Ghi dữ liệu)
    - WeatherForecastSystem (Hệ thống dự báo thời tiết)
    - NotificationSystem (Hệ thống thông báo)
    - UserInterface (Giao diện người dùng)
    - MaintenanceSchedule (Lịch bảo trì)


- b) Nhiệm vụ của từng lớp phân tích

    - EnvironmentalSensor (Cảm biến môi trường):
        - Thu thập dữ liệu môi trường thời gian thực, bao gồm nhiệt độ, độ ẩm, chất lượng không khí, mức độ ô nhiễm, v.v.
        - Cung cấp dữ liệu về các thay đổi trong điều kiện môi trường và cảnh báo các vấn đề tiềm ẩn.

    - MonitoringSystem (Hệ thống giám sát):
        - Theo dõi và phân tích dữ liệu từ các cảm biến môi trường.
        - Phát hiện bất thường và sự kiện môi trường khẩn cấp như ô nhiễm, bão, hay sóng nhiệt.

    - DataLogger (Ghi dữ liệu):
        - Lưu trữ dữ liệu thu thập từ các cảm biến môi trường.
        - Hỗ trợ việc truy xuất và phân tích dữ liệu theo thời gian hoặc yêu cầu.

    - WeatherForecastSystem (Hệ thống dự báo thời tiết):
        - Cung cấp dự báo thời tiết dựa trên các dữ liệu đầu vào từ cảm biến và các mô hình khí hậu.
        - Cập nhật thông tin về tình trạng thời tiết và cảnh báo khi có điều kiện nguy hiểm như bão hoặc lũ.

    - NotificationSystem (Hệ thống thông báo):
        - Gửi thông báo về các sự kiện bất thường hoặc khẩn cấp liên quan đến môi trường như ô nhiễm không khí, bão, v.v.
        - Cung cấp thông báo về tình trạng môi trường và dự báo thời tiết cho người dùng.

    - UserInterface (Giao diện người dùng):
        - Hiển thị dữ liệu về môi trường, bao gồm các chỉ số chất lượng không khí, độ ẩm, nhiệt độ, và các sự kiện môi trường khẩn cấp.
        - Cung cấp các công cụ cho người dùng để theo dõi và phân tích dữ liệu môi trường theo thời gian.

    - MaintenanceSchedule (Lịch bảo trì):
        - Quản lý lịch bảo trì cho các cảm biến môi trường.
        - Đảm bảo cảm biến luôn hoạt động tốt và có thể thu thập dữ liệu chính xác trong suốt quá trình giám sát.

### Mô tả Use case 
### Quản lý Môi Trường và Điều Kiện Thiên Nhiên

| **Tiêu đề**        | **Nội dung**                                                                                 |
|---------------------|---------------------------------------------------------------------------------------------|
| **Tên Use Case**    | Quản lý Môi Trường và Điều Kiện Thiên Nhiên                                                  |
| **Actor**           | Người dùng                                                                                 |
| **Mô tả**           | Cho phép người dùng giám sát môi trường và điều kiện thiên nhiên, thu thập dữ liệu từ cảm biến, cung cấp cảnh báo, hiển thị dự báo thời tiết, tạo báo cáo và quản lý lịch bảo trì. |
| **Các lớp phân tích** | **Boundary**: Giao diện người dùng<br>**Controller**: Hệ thống thông báo, Hệ thống liên lạc<br>**Entity**: Tin nhắn, Hàng đợi tin nhắn |
| **Luồng sự kiện chính**   | 1. Người Dùng yêu cầu dữ liệu môi trường thông qua Giao Diện Người Dùng.<br>2. Giao Diện Người Dùng gửi yêu cầu thông tin từ cảm biến đến Hệ Thống Giám sát.<br>3. Hệ Thống Giám sát yêu cầu dữ liệu từ Cảm Biến Môi Trường.<br>4. Cảm Biến Môi Trường trả về dữ liệu môi trường cho Hệ Thống Giám sát.<br>5. Hệ Thống Giám sát lưu trữ dữ liệu môi trường vào Ghi Dữ Liệu.<br>6. Ghi Dữ Liệu xác nhận việc lưu trữ dữ liệu.<br>   Nếu có sự kiện bất thường:<br>- Hệ Thống Giám sát gửi cảnh báo về sự kiện môi trường đến Hệ Thống Thông Báo.<br>- Hệ Thống Thông Báo thông báo cho Người Dùng về sự kiện bất thường.<br>   Nếu có yêu cầu dự báo thời tiết:<br>- Hệ Thống Dự Báo Thời Tiết cung cấp thông tin dự báo thời tiết cho Hệ Thống Giám sát.<br>- Hệ Thống Giám sát hiển thị thông tin dự báo qua Giao Diện Người Dùng.<br>- Giao Diện Người Dùng hiển thị thông tin dự báo cho Người Dùng.<br>7. Người Dùng yêu cầu báo cáo môi trường qua Giao Diện Người Dùng.<br>8. Giao Diện Người Dùng gửi yêu cầu báo cáo đến Hệ Thống Giám sát.<br>9. Hệ Thống Giám sát truy vấn dữ liệu môi trường đã lưu trữ từ Ghi Dữ Liệu.<br>10. Ghi Dữ Liệu trả về dữ liệu cho Hệ Thống Giám sát.<br>11. Hệ Thống Giám sát hiển thị báo cáo môi trường qua Giao Diện Người Dùng.<br>12. Giao Diện Người Dùng hiển thị báo cáo cho Người Dùng.<br>13. Người Dùng yêu cầu kiểm tra lịch bảo trì cảm biến qua Giao Diện Người Dùng.<br>14. Giao Diện Người Dùng gửi yêu cầu lịch bảo trì đến Lịch Bảo Trì.<br>15. Lịch Bảo Trì cung cấp lịch bảo trì cho Giao Diện Người Dùng.<br>16. Giao Diện Người Dùng hiển thị lịch bảo trì cho Người Dùng. |
| **Luồng sự kiện phụ** | Không có |

- c) Sequence Diagram (Biểu đồ trình tự)
    ![Diagram](https://www.planttext.com/plantuml/png/f5N1Qjj04BtlLmo--mToC2LrcvOwWMALdjVoHbeYpvRLoDJ7q4CEkQJq7AWn9f2c985SggNae93_s2_eBvHTEOuSoKbABnA8VM_Ul7cp-cEkNwJ4DMMZXB5qJo9ebGh6I58YeFK-i_aCeLVyXktYIaAWRo-iESO8niLtk3cIrkndy4vQSu0GnB8uHTWfNstetqxXviYQRn1aDZz12AovR376Gr8QMZkHvvBGBNvXr0AUmeTKQ2QG94sWzTBcin4CfCslyK5rV_WLZgLME198FEaBJ9LceKBIAe7M6siE88Yj-OeHRCbYEeAqc987RYkKfBJ4g3z9IOoM5RTY2Lrhpg7d6ihyuIudtbDH9DQHTwsvXCrYgloNOmc1KrnM-YWunKA_Lbg4FAL5kMQU82wkCF9C7hkZIExAa9DKk00EL8P3hfrIoHLqIzlN-FWMIUXT7efbUprh3iCODcq-Kn3eugnqWqiaWHn3qGzZCSmImPWZW7PdbGWsO5ASPX3Q_2I3eJCgyKR1o4s7xgR3Lb7jJitnLIOgEoU9GDRyS5-NWsSrQBlJD7dOWCJcyybZiffWpU98stm6Osls7-DhadOV5wVezY9pNEQyIiCgPvhBVowc8M1iyvzOuM2C9mHz5xUzSl83cyy9ABuJ101rkdQd8KgmuLt660OkkRxJjCBye5D7t42o28Wph1oX9qiVKIXmMBRXjyOVft9ho6-DhzIuDMki2ZECN2lpJzKO3U_OrrhoCDYnjEOBUZ67z_06SRLiBnnO8MYKudj_ncBvmg5x_DzQBNcU3YhfR09Zcyzn9U-Lx3sPsUQLOV_i_Thkrrgtv-0Z8CqXAM-uWR_XI1TdgtT9tS3wtRVgOOsGDK4QH5LoMUTuLeRgCFP2uD3zgFy2003__mC0)  

- d) Class Diagram (Biểu Đồ Lớp)
    ![Diagram](https://www.planttext.com/plantuml/png/V5H1JiCm4Bpx5Jt2WIyWAYW22H1IGPnNpf1QEEjglGqAg2_Zm9Fu0ahJ9dLYo34xdXdFJlBpzNqHbKGtbJV6Uefnjk3QIU0AhEINu1XazcbckyS6xs4rWLoHqidf7Y1O1z7B5N69sByjeB3w61IiZlnjZ9lTT7lGl0_iD8ZZSjb4HTKBLjsWiv4e4PDlFf2ywtGITtCE5NcNohM7xa9POhXPr238o0XK76haj6zSUyhPFeDUu0MaAyXr45YAEhhKMaBj2en0FVjcNP0UfdCFqI794WmXnH8rv81v8M77PNB5Xw3krLbI5tWa7y75ZhPdvHRS9BdrEpf6_AFt726th91NikYb2XVNdbBc9Ccu2k-Z7E8uvkJqau2B0Q92zcrHGKgmRHOrMDDYaMC54riixGh5nW_cAc8gSOH8MOy6tQARmVMUgkjBoh0r9lS5dPsTJrfk9hLlKKCvy_FfPirHdrj4iWkJxsBMpz_GZ6YcOLFnNFujAXEHIIkKDJY5P8oP2t3H_j1-0G00__y30000)


# 3. Xác định các phần tử thiết kế.  
## 3.1 Các phần tử thiết kế.   
### 3.1.1 Trạm cảm biến (Sensor Station)    
- Mô tả: Bao gồm các thiết bị cảm biến (gió, nhiệt độ, độ ẩm, áp suất, lượng mưa, v.v.) để thu thập thông tin thời tiết.  
- Chức năng: Đo lường các thông số thời tiết và chuyển dữ liệu đến hệ thống xử lý dữ liệu.  

### 3.1.2 Hệ thống xử lý dữ liệu (Data Processing System)  
- Mô tả: Là nơi thu thập và xử lý dữ liệu từ các cảm biến trước khi truyền đến hệ thống trung tâm qua vệ tinh.  
- Chức năng: Xử lý dữ liệu cục bộ, lọc và tổng hợp dữ liệu, tối ưu hóa việc truyền qua vệ tinh với băng thông hạn chế.  

### 3.1.3 Hệ thống truyền thông (Communication System)  
- Mô tả: Quản lý kết nối vệ tinh và truyền dữ liệu đến trung tâm.  
- Chức năng: Đảm bảo truyền tải thông tin quan trọng đến trung tâm, bao gồm việc bảo lưu dữ liệu nếu mất kết nối và tự động truyền tải lại khi kết nối được khôi phục.  

### 3.1.4 Hệ thống quản lý năng lượng (Power Management System)  
- Mô tả: Bao gồm các thiết bị như pin, máy phát điện, và hệ thống sạc để duy trì hoạt động của trạm cảm biến.  
- Chức năng: Điều khiển việc sạc pin, tối ưu hóa việc sử dụng năng lượng tái tạo (mặt trời, gió) và tự động ngắt khi có nguy cơ hư hỏng thiết bị.  

### 3.1.5 Hệ thống bảo trì và tái cấu hình (Maintenance and Reconfiguration System)  
- Mô tả: Hệ thống giúp tự động phát hiện lỗi và thay thế phần mềm hoặc chuyển sang các thiết bị dự phòng khi cần thiết.  
- Chức năng: Phát hiện lỗi phần cứng, phần mềm và tự động sửa chữa mà không cần can thiệp từ xa.  

### 3.1.6 Hệ thống giám sát (Monitoring System)  
- Mô tả: Theo dõi tình trạng hoạt động của các cảm biến, năng lượng, và kết nối.  
- Chức năng: Giám sát sự vận hành của các cảm biến, tình trạng năng lượng và đảm bảo kết nối vệ tinh ổn định.  

### 3.1.7 Hệ thống lưu trữ và phục hồi dữ liệu (Data Storage and Recovery System)  
- Mô tả: Quản lý dữ liệu thu thập được từ các cảm biến và đảm bảo rằng dữ liệu sẽ không bị mất khi mất kết nối vệ tinh.  
- Chức năng: Lưu trữ dữ liệu cục bộ khi mất kết nối và phục hồi dữ liệu khi kết nối được khôi phục.  

### 3.1.8 Hệ thống báo cáo và cảnh báo (Reporting and Alerts System)  
- Mô tả: Cung cấp thông tin báo cáo và cảnh báo khi có sự cố xảy ra.  
- Chức năng: Báo cáo về tình trạng hoạt động của các cảm biến, năng lượng, và hệ thống, gửi cảnh báo khi có sự cố.  

## 3.2 Các cơ chế thiết kế 
### 3.2.1 Cơ chế giám sát
- Mô tả: Giám sát liên tục tình trạng của các cảm biến, năng lượng và kết nối vệ tinh.  
- Cơ chế: Các cảm biến và các hệ thống khác sẽ gửi dữ liệu về trạng thái của chúng tới hệ thống giám sát, giúp phát hiện các sự cố và can thiệp kịp thời.  

### 3.2.2 Cơ chế lưu trữ và phục hồi dữ liệu  
- Mô tả: Hệ thống cần phải đảm bảo rằng dữ liệu sẽ được lưu trữ cục bộ khi không có kết nối và được phục hồi khi kết nối vệ tinh trở lại.  
- Cơ chế: Dữ liệu sẽ được ghi vào bộ nhớ cục bộ trong trạm khi không có kết nối và tự động gửi lại khi có kết nối.  

### 3.2.3 Cơ chế quản lý năng lượng  
- Mô tả: Sử dụng năng lượng tái tạo (mặt trời, gió) và tối ưu hóa việc sử dụng năng lượng này để đảm bảo trạm hoạt động liên tục.  
- Cơ chế: Sử dụng các thuật toán điều khiển để tối ưu hóa việc sạc pin và duy trì hoạt động của các thiết bị, đồng thời tự động ngắt các bộ phát điện khi có nguy cơ hư hại.  

### 3.2.4 Cơ chế tái cấu hình  
- Mô tả: Tự động phát hiện và thay thế phần mềm hoặc chuyển sang các thiết bị dự phòng khi cần thiết.  
- Cơ chế: Hệ thống có thể cập nhật phần mềm từ xa hoặc chuyển sang các thiết bị dự phòng khi phát hiện lỗi phần cứng.  

### 3.2.5 Cơ chế giao tiếp  
- Mô tả: Đảm bảo thông tin quan trọng được truyền qua vệ tinh dù có băng thông hạn chế.  
- Cơ chế: Dữ liệu sẽ được ưu tiên gửi đi nếu băng thông bị giới hạn, với các thông tin quan trọng (như báo cáo tình trạng hệ thống, cảnh báo) được truyền trước.  

### 3.2.6 Cơ chế bảo mật và an toàn  
- Mô tả: Đảm bảo tính bảo mật của dữ liệu và hệ thống khi truyền qua vệ tinh và lưu trữ.  
- Cơ chế: Sử dụng mã hóa dữ liệu khi truyền và bảo mật thông tin cá nhân hoặc dữ liệu quan trọng qua các giao thức bảo mật.  

# 4. Thiết kế hệ thống con  

## 4.1 Thiết kế các hệ thống con.

## 4.1.1 Hệ Thống Thu Thập Dữ Liệu (Data Collection System)
- Mô tả:
    Bao gồm các cảm biến để thu thập thông tin thời tiết như gió, nhiệt độ, độ ẩm, áp suất, lượng mưa, ánh sáng và chất lượng không khí.

- Chức năng:

    - Đo lường các thông số thời tiết.

    - Gửi dữ liệu đến hệ thống xử lý dữ liệu.

- Thành phần:

    - Cảm biến gió.

    - Cảm biến nhiệt độ.

    - Cảm biến độ ẩm.

    - Cảm biến áp suất.

    - Cảm biến lượng mưa.

    - Cảm biến ánh sáng: Đo cường độ ánh sáng mặt trời.

    - Cảm biến chất lượng không khí: CO2, bụi mịn.

    - Tích hợp các cảm biến dự phòng để đảm bảo dữ liệu không bị gián đoạn trong điều kiện môi trường khắc nghiệt.

## 4.1.2 Hệ Thống Xử Lý Dữ Liệu (Data Processing System)

- Mô tả:
    Xử lý và lưu trữ dữ liệu thu thập từ các cảm biến.

- Chức năng:

    - Phân tích và tổng hợp dữ liệu.

    - Lưu trữ dữ liệu cục bộ.

    - Tối ưu hóa dữ liệu trước khi truyền qua vệ tinh.

- Thành phần:

    - Bộ xử lý dữ liệu.

    - Bộ nhớ lưu trữ cục bộ.

    - Giao diện API: Để bên ngoài có thể truy cập và sử dụng dữ liệu thời gian thực.

    - Phần mềm phân tích dữ liệu: Phân tích xu hướng và mô hình thời tiết.

    - Tích hợp AI hoặc mô hình tự học: Dự đoán thời tiết và phát hiện các xu hướng bất thường.

## 4.1.3 Hệ Thống Giao Tiếp và Truyền Thông Tin (Communication and Transmission System)

- Mô tả:
    Quản lý kết nối vệ tinh để truyền dữ liệu đến trung tâm xử lý.

- Chức năng:

    - Đảm bảo truyền tải dữ liệu qua vệ tinh.

    - Lưu trữ tạm thời nếu mất kết nối và gửi lại khi kết nối phục hồi.

    - Cơ chế chuyển đổi linh hoạt giữa các phương thức truyền thông (vệ tinh, mạng di động, LoRaWAN) để tăng tính ổn định trong điều kiện khó khăn.

- Thành phần:

    - Modem vệ tinh. 

    - Thiết bị quản lý kết nối.

    - Giao thức truyền thông: Đảm bảo dữ liệu được mã hóa và an toàn trong quá trình truyền.

## 4.1.4 Hệ Thống Quản Lý Năng Lượng (Power Management System)

- Mô tả:
    Quản lý năng lượng cho các thiết bị trong hệ thống.

- Chức năng:

    - Điều khiển sạc pin và sử dụng năng lượng tái tạo (mặt trời, gió).

    - Giám sát tình trạng năng lượng.

- Thành phần:

    - Pin mặt trời.

    - Máy phát điện.

    - Hệ thống điều khiển sạc.

    - Hệ thống quản lý nhiệt độ: Bảo vệ pin và các thiết bị trong điều kiện nhiệt độ khắc nghiệt.

    - Bộ điều khiển năng lượng thông minh: Tối ưu hóa việc sử dụng năng lượng và giảm thiểu lãng phí.

## 4.1.5 Hệ Thống Bảo Trì và Tái Cấu Hình (Maintenance and Reconfiguration System)

- Mô tả:
    Tự động phát hiện lỗi và thực hiện các biện pháp khắc phục.

- Chức năng:

    - Phát hiện lỗi phần cứng và phần mềm.

    - Cập nhật phần mềm từ xa.

    - Chuyển sang thiết bị dự phòng khi có sự cố.

    - Mô-đun tự động khởi động lại: Khi phát hiện lỗi nghiêm trọng.

    - Phân quyền quản lý bảo trì: Giới hạn quyền truy cập để tăng cường bảo mật.

- Thành phần:

    - Phần mềm giám sát.

    - Thiết bị dự phòng.

    - Giao diện quản lý bảo trì: Theo dõi trạng thái bảo trì và sửa chữa.

## 4.1.6 Hệ Thống Giám Sát (Monitoring System)

- Mô tả:

    Theo dõi tình trạng hoạt động của các cảm biến và hệ thống.

- Chức năng:

    - Giám sát sự vận hành của các cảm biến.

    - Kiểm tra tình trạng năng lượng và kết nối.

    - Theo dõi lịch sử sự cố để phân tích nguyên nhân và cải thiện hệ thống.

    - Tích hợp AI: Phát hiện bất thường trong hoạt động của các hệ thống con.

- Thành phần:

    - Giao diện người dùng để theo dõi tình trạng.

    - Hệ thống cảnh báo.

    - Biểu đồ trực quan: Hiển thị tình trạng cảm biến và dữ liệu theo thời gian thực.

## 4.1.7 Hệ Thống Lưu Trữ và Phục Hồi Dữ Liệu (Data Storage and Recovery System)

- Mô tả:
    Quản lý và bảo vệ dữ liệu thu thập được.

- Chức năng:

    - Lưu trữ dữ liệu cục bộ khi mất kết nối.

    - Phục hồi dữ liệu khi kết nối trở lại.

    - Tăng cường bảo mật: Mã hóa dữ liệu lưu trữ và truyền tải.

- Thành phần:

    - Cơ sở dữ liệu cục bộ.

    - Hệ thống phục hồi dữ liệu.

    - Bản sao lưu dữ liệu: Lưu trữ dữ liệu ở một vị trí an toàn khác để bảo vệ thông tin.

## 4.1.8 Hệ Thống Báo Cáo và Cảnh Báo (Reporting and Alerts System)

- Mô tả:
    Cung cấp thông tin báo cáo và cảnh báo khi có sự cố.

- Chức năng:

    - Gửi báo cáo về tình trạng hoạt động.

    - Gửi cảnh báo khi có sự cố xảy ra.

    - Phân cấp cảnh báo: Ưu tiên các sự cố nghiêm trọng.

- Thành phần:

    - Giao diện báo cáo.

    - Hệ thống thông báo.

    - Tùy chọn tùy chỉnh báo cáo: Cho phép người dùng tùy chỉnh nội dung và định dạng báo cáo theo nhu cầu.

## 4.2 Mối Quan Hệ Giữa Các Hệ Thống Con

## 4.2.1 Hệ Thống Thu Thập Dữ Liệu (Data Collection System)

- Gửi dữ liệu thời gian thực đến Hệ Thống Xử Lý Dữ Liệu.

- Tích hợp cơ chế giám sát từ Hệ Thống Giám Sát để đảm bảo chất lượng dữ liệu.

## 4.2.2 Hệ Thống Xử Lý Dữ Liệu (Data Processing System)

- Phân tích, tổng hợp, và tối ưu hóa dữ liệu trước khi gửi đến Hệ Thống Giao Tiếp.

- Lưu trữ tạm thời dữ liệu trong Hệ Thống Lưu Trữ và Phục Hồi Dữ Liệu.

- Nhận lệnh điều chỉnh từ Hệ Thống Bảo Trì và Tái Cấu Hình khi có sự cố.

## 4.2.3 Hệ Thống Giao Tiếp và Truyền Thông Tin (Communication and Transmission System)

- Truyền dữ liệu đến Hệ thống báo cáo và cảnh báo.

- Nhận và thực hiện lệnh từ Hệ Thống Bảo Trì hoặc trung tâm điều hành.

- Báo cáo trạng thái kết nối và lỗi mạng cho Hệ Thống Giám Sát.

## 4.2.4 Hệ Thống Quản Lý Năng Lượng (Power Management System)

- Cung cấp năng lượng cho tất cả các hệ thống con.

- Gửi thông tin tình trạng năng lượng đến Hệ Thống Giám Sát.

- Tự động điều chỉnh và tối ưu hóa năng lượng theo yêu cầu từ các hệ thống khác.

## 4.2.5 Hệ Thống Bảo Trì và Tái Cấu Hình (Maintenance and Reconfiguration System)

- Theo dõi tình trạng hoạt động của các hệ thống con thông qua Hệ Thống Giám Sát.

- Gửi lệnh bảo trì hoặc cấu hình lại cho các hệ thống khi cần thiết.

- Cập nhật phần mềm từ xa và chuyển đổi thiết bị dự phòng.

## 4.2.6 Hệ Thống Giám Sát (Monitoring System)

- Theo dõi trạng thái toàn bộ hệ thống (năng lượng, dữ liệu, giao tiếp...).

- Gửi cảnh báo đến Hệ Thống Báo Cáo và Cảnh Báo.

- Kích hoạt các cơ chế tự động khắc phục từ Hệ Thống Bảo Trì khi phát hiện bất thường.

## 4.2.7 Hệ Thống Lưu Trữ và Phục Hồi Dữ Liệu (Data Storage and Recovery System)

- Lưu trữ dữ liệu từ Hệ Thống Xử Lý Dữ Liệu.

- Cung cấp dữ liệu lịch sử cho Hệ Thống Báo Cáo hoặc các hệ thống phân tích.

- Đảm bảo dữ liệu không bị mất trong trường hợp hệ thống gặp sự cố.

## 4.2.8 Hệ Thống Báo Cáo và Cảnh Báo (Reporting and Alerts System)

- Gửi báo cáo định kỳ hoặc theo yêu cầu từ các hệ thống khác.

- Phát cảnh báo cấp độ phù hợp khi nhận thông tin từ Hệ Thống Giám Sát.

- Cho phép người dùng tùy chỉnh nội dung báo cáo và cảnh báo.

- Class Package (Biểu Đồ Lớp Package)
    ![Diagram](https://www.planttext.com/plantuml/png/Z5MnRjim4Dtv5GSldf8FC08ZgO8cWnsuYOQkj4H8H2JIfQWKGT6Xw92rGQUWA10ry58aI81s4b5aOE3_u1Vq5ugJt5fI6wUROFBUlNll7VtJt6zdcYgTfmaX_UoO2vZHu9X6x4YV9WmK2pGLKS98TQPanWZHN2SC9lMz33PWxCmvXrSv5H0xSmQ1BGBOnoyTEtCk8WYa8AGF7Xv4zXklxorFoR8bzAeQVrdZnpb-bpSps7Nc5aRScREy1rjR1p9amo7G37QfffvC4XPeBWMy8M_98sWldRc1aVtHnJfaWLvXJPGCM9Pn4Qt3skDKWizTUJ-34ti9lifFdNadm8_jTsJE1K8_bqd8L0tkoJJD1G_eKpnVvAwy4XNJWuVt8eBHuiwPAn5LY8gcoyadyZLJOofen58cz3h8Pwwyak0hUrspjGK7pvNp7FRjjOZRYeuf5ve9AWAsNW9Rf71a2utbNYBpS5al1TTIFQ7WQ76NWw_G2gGqYPsPLv7voBi6eIrJcZKCFz9I8UIwaMqXCMsoWlTGqhZwiUlB8Pj9fV-mxRTZExLV1OX8sajEQA2bWjv1X7vyvWsZUWYq4wPSDEWq9dpuW5gDxPVJZbRLPskQ_b-x575dRcczKisb0U7C1OUfCnUaimKR6yDkc0UmvymDXn3v99Msf7C5gzef7Qo2_KHTqvL1RQwkHc_MjS6nR2L-ezKKNGji8KatubYoCnh10BmStnHNpcSWgYL9baj26l7xrq2r2a6T1-pqlwoQ9UDsZvfIlH2PBJHP0Mnk3biBzPk0hjy9pGLCg-NKobwZ-_xYRb7W2TfzuiodzalP2kIgJSK2yzUMPgLaqvzAbcRm7ZCCGdk9xSj24BBDH8X_4hy0003__mC0)

# 5. Thiết kế các lớp  
## 5.1 Hệ thống Trạm Khí Tượng
### 5.1.1. WeatherStation (Trạm thời tiết)
**Hành vi:**
- `collectWeatherData()`: Thu thập dữ liệu từ các cảm biến.
- `processData()`: Xử lý và tổng hợp dữ liệu thu thập được.
- `transmitData()`: Truyền tải dữ liệu qua vệ tinh.
- `storeData()`: Lưu trữ dữ liệu khi không thể truyền tải qua vệ tinh.

**Quan hệ:**
- WeatherStation có mối quan hệ với Sensor để thu thập dữ liệu.
- WeatherStation có mối quan hệ với SatelliteCommunication để truyền tải dữ liệu.
- WeatherStation có mối quan hệ với DataStorage để lưu trữ dữ liệu tạm thời nếu không thể truyền tải.

### 5.1.2. Sensor (Cảm biến)
**Hành vi:**
- `measureTemperature()`: Đo nhiệt độ.
- `measureWindSpeed()`: Đo tốc độ gió.
- `measurePressure()`: Đo áp suất.
- `measureRainfall()`: Đo lượng mưa.

**Quan hệ:**
- Sensor cung cấp dữ liệu cho WeatherStation.

### 5.1.3. SatelliteCommunication (Giao tiếp vệ tinh)
**Hành vi:**
- `establishConnection()`: Thiết lập kết nối với vệ tinh.
- `sendData()`: Gửi dữ liệu tới vệ tinh.

**Quan hệ:**
- SatelliteCommunication giúp WeatherStation truyền tải dữ liệu qua vệ tinh.

### 5.1.4. DataStorage (Lưu trữ dữ liệu)
**Hành vi:**
- `storeDataTemporarily()`: Lưu trữ dữ liệu tạm thời khi không có kết nối vệ tinh.
- `retrieveStoredData()`: Truy xuất dữ liệu khi kết nối vệ tinh được khôi phục.

**Quan hệ:**
- DataStorage lưu trữ các đối tượng WeatherData khi không thể truyền tải dữ liệu qua vệ tinh.

### 5.1.5. WeatherData (Dữ liệu thời tiết)
**Thuộc tính:**
- `temperature`: Nhiệt độ.
- `humidity`: Độ ẩm.
- `windSpeed`: Tốc độ gió.
- `pressure`: Áp suất.
- `rainfall`: Lượng mưa.

**Quan hệ:**
- WeatherData được DataStorage lưu trữ và WeatherStation sử dụng để tổng hợp thông tin thời tiết.

## 5.2 Hệ thống Quản lý và Lưu trữ Dữ liệu
### 5.2.1. DataManagement (Quản lý dữ liệu)
**Hành vi:**
- `receiveData()`: Nhận dữ liệu đầu vào.
- `organizeData()`: Sắp xếp dữ liệu một cách có tổ chức.
- `standardizeData()`: Chuẩn hóa dữ liệu theo định dạng thống nhất.
- `processData()`: Xử lý dữ liệu để phân tích.
- `classifyData()`: Phân loại dữ liệu theo các nhóm hoặc tiêu chí cụ thể.

**Quan hệ:**
- DataManagement quản lý WeatherData (các thông số thời tiết).
- DataManagement tương tác với UserInterface (để hiển thị và thao tác dữ liệu).
- DataManagement đảm bảo SecurityManagement bảo vệ dữ liệu.

### 5.2.2. DataArchiving (Lưu trữ dữ liệu)
**Hành vi:**
- `storeHistoricalData()`: Lưu trữ dữ liệu lịch sử.
- `backupData()`: Sao lưu dữ liệu để bảo vệ trong trường hợp mất mát.
- `restoreData()`: Khôi phục dữ liệu từ bản sao lưu.
- `manageStorageSpace()`: Quản lý không gian lưu trữ dữ liệu.
- `cleanOldData()`: Dọn dẹp dữ liệu cũ không còn sử dụng.

**Quan hệ:**
- DataArchiving lưu trữ WeatherData (dữ liệu thời tiết).
- DataArchiving bảo vệ dữ liệu thông qua SecurityManagement.

### 5.2.3. WeatherData (Dữ liệu thời tiết)
**Thuộc tính:**
- `temperature`: Nhiệt độ.
- `humidity`: Độ ẩm.
- `windSpeed`: Tốc độ gió.
- `rainfall`: Lượng mưa.
- `pressure`: Áp suất.

**Hành vi:**
- `storeData()`: Lưu trữ dữ liệu thời tiết.

**Quan hệ:**
- WeatherData được quản lý bởi DataManagement và lưu trữ bởi DataArchiving.
- WeatherData được hiển thị bởi UserInterface.

### 5.2.4. UserInterface (Giao diện người dùng)
**Hành vi:**
- `searchData()`: Tìm kiếm dữ liệu.
- `filterData()`: Lọc dữ liệu theo các tiêu chí.
- `queryData()`: Truy vấn dữ liệu dựa trên yêu cầu.
- `generateReport()`: Tạo báo cáo từ dữ liệu.
- `exportData()`: Xuất dữ liệu ra định dạng khác (ví dụ: CSV, Excel).

**Quan hệ:**
- UserInterface hiển thị WeatherData.
- UserInterface tương tác với DataManagement để thao tác dữ liệu.
- UserInterface được kiểm soát quyền truy cập bởi SecurityManagement.

### 5.2.5. SecurityManagement (Quản lý bảo mật)
**Hành vi:**
- `authorizeAccess()`: Xác thực quyền truy cập của người dùng.
- `logActivities()`: Ghi lại các hoạt động người dùng để theo dõi và kiểm tra.
- `encryptData()`: Mã hóa dữ liệu để bảo vệ tính bảo mật.

**Quan hệ:**
- SecurityManagement kiểm soát quyền truy cập của UserInterface.
- SecurityManagement đảm bảo bảo mật dữ liệu cho DataManagement và DataArchiving.

## 5.3 Hệ thống Bảo trì Trạm
### 5.3.1. MaintenanceRequest (Yêu cầu bảo trì)
**Hành vi:**
- `receiveRequest()`: Tiếp nhận yêu cầu bảo trì từ người dùng.
- `recordIssue()`: Ghi lại vấn đề hoặc sự cố cần sửa chữa.
- `logEquipment()`: Lưu thông tin về thiết bị gặp sự cố.
- `setPriority()`: Đặt mức độ ưu tiên cho yêu cầu bảo trì.

**Quan hệ:**
- MaintenanceRequest có mối quan hệ với StationEquipment để ghi lại thông tin thiết bị gặp sự cố.
- MaintenanceRequest có mối quan hệ với Technician để thông báo cho kỹ thuật viên và quản lý yêu cầu bảo trì.

### 5.3.2. Technician (Kỹ thuật viên)
**Hành vi:**
- `manageTechnicianList()`: Quản lý danh sách kỹ thuật viên.
- `updateRequestStatus()`: Cập nhật trạng thái yêu cầu bảo trì.
- `trackPerformance()`: Theo dõi hiệu suất làm việc của kỹ thuật viên.
- `trackWorkHistory()`: Theo dõi lịch sử công việc của kỹ thuật viên.

**Quan hệ:**
- Technician cập nhật yêu cầu bảo trì và có mối quan hệ với MaintenanceSchedule để điều phối lịch bảo trì.
- Technician cũng tương tác với MaintenanceRequest để cập nhật tình trạng yêu cầu.

### 5.3.3. StationEquipment (Thiết bị trạm)
**Hành vi:**
- `storeEquipmentInfo()`: Lưu trữ thông tin về thiết bị trong trạm.
- `recordMaintenanceHistory()`: Ghi lại lịch sử bảo trì của thiết bị.
- `provideMaintenanceInfo()`: Cung cấp thông tin về bảo trì thiết bị.

**Quan hệ:**
- StationEquipment có mối quan hệ với MaintenanceRequest để ghi lại thiết bị gặp sự cố.
- StationEquipment cũng có mối quan hệ với MaintenanceSchedule để lên lịch bảo trì thiết bị.

### 5.3.4. MaintenanceSchedule (Lịch bảo trì)
**Hành vi:**
- `createSchedule()`: Tạo lịch bảo trì cho các thiết bị.
- `manageRegularMaintenance()`: Quản lý bảo trì định kỳ.
- `ensureMinimalSystemImpact()`: Đảm bảo tác động tối thiểu đến hệ thống khi thực hiện bảo trì.

**Quan hệ:**
- MaintenanceSchedule có mối quan hệ với Technician để phân công công việc bảo trì cho kỹ thuật viên.
- MaintenanceSchedule cũng có mối quan hệ với StationEquipment để lên lịch bảo trì thiết bị.

### 5.3.5. NotificationSystem (Hệ thống thông báo)
**Hành vi:**
- `sendNotification()`: Gửi thông báo cho người dùng hoặc quản lý.
- `alertTechnician()`: Cảnh báo kỹ thuật viên về yêu cầu bảo trì.
- `alertManager()`: Cảnh báo quản lý về trạng thái yêu cầu bảo trì.
- `sendEmergencyAlert()`: Gửi thông báo khẩn cấp khi có sự cố nghiêm trọng.

**Quan hệ:**
- NotificationSystem gửi thông báo cho Technician và MaintenanceSchedule để thông báo về yêu cầu bảo trì.

### 5.3.6. UserInterface (Giao diện người dùng)
**Hành vi:**
- `submitRequest()`: Người dùng gửi yêu cầu bảo trì.
- `trackRequestStatus()`: Người dùng theo dõi trạng thái yêu cầu bảo trì.
- `manageHistory()`: Quản lý lịch sử bảo trì của thiết bị.
- `updateEquipmentStatus()`: Cập nhật trạng thái thiết bị.

**Quan hệ:**
- UserInterface tương tác với MaintenanceRequest để gửi yêu cầu bảo trì.
- UserInterface có mối quan hệ với Technician và StationEquipment để theo dõi công việc bảo trì và trạng thái thiết bị.

## 5.4 Hệ thống Quản lý Năng Lượng  
### 5.4.1. EnergySource (Nguồn năng lượng)
**Hành vi:**
- `manageEnergySources()`: Quản lý các nguồn năng lượng (như điện, năng lượng tái tạo).
- `provideStatus()`: Cung cấp trạng thái của nguồn năng lượng.
- `provideOutputPower()`: Cung cấp năng lượng đầu ra cho hệ thống.

**Quan hệ:**
- EnergySource cung cấp năng lượng cho PowerControlSystem.
- EnergySource cũng cung cấp năng lượng cho EnergyConsumption.

### 5.4.2. EnergyConsumption (Tiêu thụ năng lượng)
**Hành vi:**
- `monitorEnergyUsage()`: Giám sát việc sử dụng năng lượng trong hệ thống.
- `analyzeEnergyConsumption()`: Phân tích mức độ tiêu thụ năng lượng.
- `optimizeEnergyUse()`: Tối ưu hóa việc sử dụng năng lượng.

**Quan hệ:**
- EnergyConsumption được cung cấp năng lượng từ EnergySource và bị kiểm soát bởi PowerControlSystem.

### 5.4.3. EnergyStorage (Lưu trữ năng lượng)
**Hành vi:**
- `manageStorageSystems()`: Quản lý hệ thống lưu trữ năng lượng (như pin hoặc ắc quy).
- `ensureEnergyStorageEfficiency()`: Đảm bảo hiệu quả lưu trữ năng lượng.
- `provideEnergyWhenNeeded()`: Cung cấp năng lượng khi cần thiết.

**Quan hệ:**
- EnergyStorage lưu trữ năng lượng và cung cấp năng lượng cho PowerControlSystem khi cần thiết.

### 5.4.4. PowerControlSystem (Hệ thống điều khiển năng lượng)
**Hành vi:**
- `coordinateEnergySources()`: Điều phối các nguồn năng lượng.
- `controlEnergyConsumption()`: Điều khiển mức độ tiêu thụ năng lượng.
- `manageEnergyStorage()`: Quản lý hệ thống lưu trữ năng lượng.
- `switchEnergyModes()`: Chuyển đổi giữa các chế độ năng lượng (như tiết kiệm năng lượng hoặc chế độ bình thường).

**Quan hệ:**
- PowerControlSystem điều khiển EnergyConsumption và phối hợp với EnergyStorage để tối ưu hóa việc sử dụng và lưu trữ năng lượng.
- PowerControlSystem kích hoạt các cảnh báo trong NotificationSystem.

### 5.4.5. NotificationSystem (Hệ thống thông báo)
**Hành vi:**
- `sendAlert()`: Gửi cảnh báo về trạng thái năng lượng.
- `notifyLowEnergy()`: Cảnh báo khi năng lượng thấp.
- `notifyMaintenanceSchedule()`: Thông báo về lịch bảo trì.
- `sendSystemFailureAlert()`: Gửi cảnh báo khi hệ thống gặp sự cố.

**Quan hệ:**
- NotificationSystem nhận thông tin từ PowerControlSystem để gửi cảnh báo và thông báo cho người dùng.

### 5.4.6. UserInterface (Giao diện người dùng)
**Hành vi:**
- `displayEnergyStatus()`: Hiển thị trạng thái năng lượng hiện tại.
- `displayConsumptionLevels()`: Hiển thị mức độ tiêu thụ năng lượng.
- `adjustEnergySettings()`: Điều chỉnh các thiết lập năng lượng.
- `receiveNotifications()`: Nhận thông báo về năng lượng, cảnh báo và bảo trì.

**Quan hệ:**
- UserInterface có mối quan hệ với PowerControlSystem để điều chỉnh cài đặt năng lượng.
- UserInterface cũng nhận thông báo từ NotificationSystem.

## 5.5 Hệ thống Giám sát Cảm biến  
### 5.5.1. Sensor (Cảm biến)
**Phương thức:**
- `collectRealTimeData()`: Thu thập dữ liệu thời gian thực từ cảm biến.
- `reportStatus()`: Cung cấp trạng thái hiện tại của cảm biến.
- `monitorHealth()`: Giám sát tình trạng và trạng thái của cảm biến.

**Quan hệ:**
- Cảm biến cung cấp dữ liệu cho Hệ thống Giám sát.

### 5.5.2. MonitoringSystem (Hệ thống Giám sát)
**Phương thức:**
- `trackSensorData()`: Theo dõi dữ liệu từ cảm biến.
- `analyzeData()`: Phân tích dữ liệu thu được để tạo ra thông tin hữu ích.
- `detectAnomalies()`: Phát hiện bất thường trong dữ liệu, như lỗi hoặc các chỉ số lạ.

**Quan hệ:**
- Hệ thống Giám sát ghi lại dữ liệu vào Hệ thống Ghi nhật ký Dữ liệu.
- Hệ thống Giám sát kích hoạt cảnh báo thông qua Hệ thống Thông báo.
- Hệ thống Giám sát tương tác với Giao diện Người dùng để hiển thị dữ liệu và cho phép người dùng tương tác.

### 5.5.3. DataLogger (Hệ thống Ghi nhật ký Dữ liệu)
**Phương thức:**
- `storeSensorData()`: Lưu trữ dữ liệu thu thập từ các cảm biến.
- `retrieveData()`: Lấy lại dữ liệu đã lưu từ các cảm biến.
- `exportData()`: Xuất dữ liệu đã lưu để thực hiện phân tích hoặc tạo báo cáo.

**Quan hệ:**
- Hệ thống Ghi nhật ký Dữ liệu xuất dữ liệu ra Giao diện Người dùng.

### 5.5.4. NotificationSystem (Hệ thống Thông báo)
**Phương thức:**
- `sendAlert()`: Gửi các cảnh báo liên quan đến tình trạng hệ thống.
- `notifyAbnormalities()`: Thông báo cho người dùng về bất thường phát hiện trong dữ liệu cảm biến.
- `remindMaintenance()`: Gửi nhắc nhở về bảo trì định kỳ cho cảm biến hoặc hệ thống.

**Quan hệ:**
- Hệ thống Thông báo gửi thông báo đến Giao diện Người dùng.
- Hệ thống Thông báo nhận kích hoạt từ Hệ thống Giám sát.

### 5.5.5. UserInterface (Giao diện Người dùng)
**Phương thức:**
- `displaySensorStatus()`: Hiển thị trạng thái hiện tại của cảm biến.
- `searchData()`: Cho phép người dùng tìm kiếm dữ liệu cảm biến trong quá khứ.
- `analyzeData()`: Cung cấp các tính năng phân tích dữ liệu cho người dùng.
- `generateReports()`: Tạo báo cáo dựa trên phân tích dữ liệu.

**Quan hệ:**
- Giao diện Người dùng tương tác với Hệ thống Giám sát để hiển thị dữ liệu cảm biến.
- Giao diện Người dùng nhận thông báo từ Hệ thống Thông báo.
- Giao diện Người dùng xuất dữ liệu từ Hệ thống Ghi nhật ký Dữ liệu.

### 5.5.6. MaintenanceSchedule (Lịch Bảo trì)
**Phương thức:**
- `manageMaintenance()`: Quản lý lịch trình và thực hiện bảo trì cảm biến.
- `trackMaintenanceHistory()`: Theo dõi lịch sử bảo trì các cảm biến.
- `ensureTimelyMaintenance()`: Đảm bảo bảo trì cảm biến được thực hiện đúng hạn để tránh sự cố.

**Quan hệ:**
- Lịch Bảo trì quản lý bảo trì cho cảm biến.  

## 5.6 Quản lý Cập nhật và Thay thế Cảm biến  
### 5.6.1. Sensor (Cảm biến)  
**Phương thức:**
- `provideStatus()`: Cung cấp trạng thái hiện tại của cảm biến.
- `providePerformanceData()`: Cung cấp dữ liệu liên quan đến hiệu suất của cảm biến.
- `provideLifespanData()`: Cung cấp thông tin về tuổi thọ dự kiến của cảm biến.
- `reportWearAndTear()`: Báo cáo bất kỳ sự hư hỏng vật lý hoặc sự cố hoạt động nào của cảm biến.

**Quan hệ:**
- Cảm biến cung cấp trạng thái và dữ liệu cho Hệ thống Quản lý Thiết bị.

### 5.6.2. InstrumentManagementSystem (Hệ thống Quản lý Thiết bị)  
**Phương thức:**
- `trackSensorStatus()`: Theo dõi và giám sát trạng thái của tất cả các cảm biến.
- `logReplacementHistory()`: Lưu trữ lịch sử thay thế cảm biến đã thực hiện.
- `updateSensorInfo()`: Cập nhật chi tiết cảm biến, chẳng hạn như hiệu suất hoặc hồ sơ bảo trì.
- `manageReplacementRequests()`: Quản lý các yêu cầu thay thế cảm biến dựa trên các báo cáo hao mòn.

**Quan hệ:**
- Hệ thống Quản lý Thiết bị tương tác với Nhóm Bảo trì để quản lý việc thay thế cảm biến.
- Hệ thống Quản lý Thiết bị tương tác với Giao diện Người dùng để hiển thị thông tin cảm biến và theo dõi yêu cầu.
- Hệ thống Quản lý Thiết bị tương tác với Hệ thống Quản lý Kho để theo dõi và quản lý tồn kho cảm biến và các bộ phận thay thế.

### 5.6.3. MaintenanceTeam (Nhóm Bảo trì)  
**Phương thức:**
- `performSensorReplacement()`: Thực hiện thay thế cảm biến bị hỏng hoặc lỗi.
- `verifyNewSensorInstallation()`: Xác nhận rằng cảm biến mới đã được cài đặt đúng cách.
- `confirmSensorFunctionality()`: Xác nhận rằng cảm biến mới hoạt động hoàn hảo.

**Quan hệ:**
- Nhóm Bảo trì làm việc với Giao diện Người dùng để theo dõi trạng thái thay thế cảm biến và lịch bảo trì.

### 5.6.4. UserInterface (Giao diện Người dùng)  
**Phương thức:**
- `displaySensorInfo()`: Hiển thị thông tin về trạng thái, hiệu suất và tuổi thọ của cảm biến.
- `trackReplacementRequests()`: Theo dõi và quản lý trạng thái các yêu cầu thay thế cảm biến.
- `viewMaintenanceSchedule()`: Cho phép người dùng xem lịch bảo trì các cảm biến.

**Quan hệ:**
- Giao diện Người dùng tương tác với Hệ thống Quản lý Thiết bị để hiển thị dữ liệu cảm biến và yêu cầu thay thế.
- Giao diện Người dùng làm việc với Hệ thống Thông báo để hiển thị cảnh báo và thông báo.

### 5.6.5. NotificationSystem (Hệ thống Thông báo)  
**Phương thức:**
- `sendReplacementAlert()`: Gửi thông báo về nhu cầu thay thế cảm biến.
- `notifyMaintenanceTeam()`: Gửi thông báo cho nhóm bảo trì về việc thay thế cảm biến sắp tới.
- `notifyUserOfSensorStatus()`: Thông báo cho người dùng về trạng thái của cảm biến hoặc bất kỳ vấn đề nào cần chú ý.

**Quan hệ:**
- Hệ thống Thông báo gửi thông báo cho Giao diện Người dùng và thông báo cho người dùng về trạng thái cảm biến và nhu cầu bảo trì.

### 5.6.6. InventorySystem (Hệ thống Quản lý Kho)  
**Phương thức:**
- `manageSensorStock()`: Quản lý tồn kho các cảm biến có sẵn để thay thế.
- `updateAvailabilityStatus()`: Cập nhật trạng thái sẵn có của cảm biến trong kho.
- `trackReplacementParts()`: Theo dõi tình trạng tồn kho và mức độ sẵn có của các bộ phận cần thiết cho việc thay thế cảm biến.

**Quan hệ:**
- Hệ thống Quản lý Kho tương tác với Hệ thống Quản lý Thiết bị để theo dõi và quản lý các cảm biến và bộ phận thay thế.

## 5.7 Quản lý Hệ thống Phần Mềm  
### 5.7.1. Software (Phần mềm)  
**Phương thức:**
- `provideVersionInfo()`: Cung cấp thông tin liên quan đến phiên bản của phần mềm.
- `provideFeatures()`: Liệt kê các tính năng có trong phiên bản phần mềm.
- `provideOperationalStatus()`: Cung cấp trạng thái vận hành hiện tại của phần mềm.
- `managePatches()`: Quản lý các bản vá, bao gồm áp dụng và cập nhật chúng.

**Quan hệ:**
- Phần mềm được quản lý bởi Hệ thống Quản lý Phần mềm.

### 5.7.2. SoftwareManagementSystem (Hệ thống Quản lý Phần mềm)  
**Phương thức:**
- `trackSoftwareStatus()`: Giám sát trạng thái của các phiên bản phần mềm.
- `logVersionUpdates()`: Ghi lại tất cả các cập nhật của phần mềm.
- `recordPatchHistory()`: Lưu giữ lịch sử các bản vá được áp dụng cho phần mềm.
- `manageUpdateRequests()`: Xử lý các yêu cầu cập nhật phần mềm.

**Quan hệ:**
- Hệ thống Quản lý Phần mềm tương tác với Nhóm Phát triển để theo dõi các cập nhật và xử lý các yêu cầu.
- Hệ thống Quản lý Phần mềm tương tác với Giao diện Người dùng để hiển thị thông tin phần mềm và yêu cầu cập nhật.
- Hệ thống Quản lý Phần mềm tương tác với Hệ thống Quản lý Phiên bản để quản lý các phiên bản và mã nguồn.

### 5.7.3. DevelopmentTeam (Nhóm Phát triển)  
**Phương thức:**
- `developSoftware()`: Phát triển các phiên bản phần mềm và tính năng mới.
- `testSoftware()`: Kiểm tra phần mềm để đảm bảo tính năng và chất lượng.
- `confirmChangesBeforeDeployment()`: Xác nhận các thay đổi trước khi triển khai phần mềm.

**Quan hệ:**
- Nhóm Phát triển tương tác với Giao diện Người dùng để theo dõi các thay đổi và cập nhật.
- Nhóm Phát triển làm việc với Hệ thống Quản lý Phần mềm để xử lý các cập nhật phần mềm.

### 5.7.4. UserInterface (Giao diện Người dùng)  
**Phương thức:**
- `displaySoftwareInfo()`: Hiển thị thông tin chi tiết về phiên bản phần mềm và tính năng.
- `trackUpdateRequests()`: Theo dõi các yêu cầu cập nhật và bản vá.
- `viewChangeHistory()`: Cho phép người dùng xem lịch sử thay đổi phần mềm.

**Quan hệ:**
- Giao diện Người dùng tương tác với Hệ thống Quản lý Phần mềm để xem và quản lý các cập nhật phần mềm và trạng thái yêu cầu.
- Giao diện Người dùng cũng tương tác với Hệ thống Thông báo để nhận thông báo và cập nhật.

### 5.7.5. NotificationSystem (Hệ thống Thông báo)  
**Phương thức:**
- `sendPatchUpdateAlert()`: Gửi thông báo đến người dùng về các bản cập nhật vá lỗi mới.
- `notifyDevelopmentTeam()`: Thông báo cho nhóm phát triển về các cập nhật hoặc vấn đề mới.
- `notifyUsersOfUpdates()`: Gửi thông báo cho người dùng về các bản cập nhật phần mềm.

**Quan hệ:**
- Hệ thống Thông báo tương tác với Giao diện Người dùng để gửi các thông báo và cập nhật cho người dùng.

### 5.7.6. VersionControlSystem (Hệ thống Quản lý Phiên bản)  
**Phương thức:**
- `manageSoftwareVersions()`: Quản lý các phiên bản phần mềm trong hệ thống.
- `trackCodeChanges()`: Theo dõi các thay đổi mã nguồn trong phần mềm.
- `updateBranchStatus()`: Cập nhật trạng thái của các nhánh mã nguồn khác nhau.

**Quan hệ:**
- Hệ thống Quản lý Phiên bản tương tác với Hệ thống Quản lý Phần mềm để theo dõi các phiên bản và cập nhật phần mềm.


## 5.8 Báo cáo và Cảnh báo  
### 5.8.1. Report (Báo cáo)
**Phương thức:**
- `generateDetailedReport()`: Tạo báo cáo chi tiết chứa dữ liệu toàn diện.
- `generateOverviewReport()`: Tạo báo cáo tổng quan hoặc báo cáo tóm tắt.
- `provideReportsOnRequest()`: Cung cấp báo cáo khi người dùng yêu cầu.

**Quan hệ:**
- Lớp Báo cáo tương tác với Hệ thống Báo cáo để tạo và quản lý các báo cáo.

### 5.8.2. Alert (Cảnh báo)
**Phương thức:**
- `createAlert()`: Tạo cảnh báo dựa trên các điều kiện cụ thể.
- `notifyUser()`: Gửi cảnh báo đã tạo đến người dùng.
- `monitorCriticalEvents()`: Giám sát các sự kiện quan trọng để kích hoạt cảnh báo.

**Quan hệ:**
- Lớp Cảnh báo tương tác với Hệ thống Cảnh báo để quản lý và thông báo cho người dùng về cảnh báo.

### 5.8.3. ReportingSystem (Hệ thống báo cáo)
**Phương thức:**
- `processReportData()`: Xử lý dữ liệu sẽ được sử dụng trong các báo cáo.
- `generateReports()`: Tạo các báo cáo cần thiết (chi tiết hoặc tổng quan).
- `provideReportInterface()`: Cung cấp giao diện để người dùng tương tác với các báo cáo.

**Quan hệ:**
- Hệ thống báo cáo tương tác với Cơ sở dữ liệu để thực thi các truy vấn và truy xuất dữ liệu cho báo cáo.
- Hệ thống báo cáo tương tác với Giao diện người dùng để trình bày báo cáo cho người dùng.

### 5.8.4. AlertSystem (Hệ thống cảnh báo)
**Phương thức:**
- `processAlertData()`: Xử lý dữ liệu liên quan đến các cảnh báo.
- `generateAlerts()`: Tạo các cảnh báo dựa trên các điều kiện cụ thể.
- `provideAlertInterface()`: Cung cấp giao diện để người dùng tương tác với các cảnh báo.

**Quan hệ:**
- Hệ thống cảnh báo tương tác với Cơ sở dữ liệu để thực thi các truy vấn và truy xuất dữ liệu cho cảnh báo.
- Hệ thống cảnh báo tương tác với Giao diện người dùng để trình bày cảnh báo cho người dùng.

### 5.8.5. UserInterface (Giao diện người dùng)
**Phương thức:**
- `displayReports()`: Hiển thị các báo cáo đã tạo cho người dùng.
- `viewAlerts()`: Hiển thị các cảnh báo cho người dùng.
- `requestReports()`: Cho phép người dùng yêu cầu các báo cáo cụ thể.
- `monitorAlerts()`: Giám sát các cảnh báo liên quan đến người dùng.

**Quan hệ:**
- Giao diện người dùng tương tác với cả Hệ thống Báo cáo và Hệ thống Cảnh báo để trình bày thông tin cho người dùng.
- Giao diện người dùng cũng được kết nối với Hệ thống Thông báo để nhận các thông báo.

### 5.8.6. NotificationSystem (Hệ thống thông báo)
**Phương thức:**
- `sendAlertNotification()`: Gửi thông báo về cảnh báo mới hoặc đã được cập nhật.
- `sendReportNotification()`: Gửi thông báo về báo cáo mới hoặc đã được cập nhật.
- `notifyUsersViaChannels()`: Thông báo cho người dùng qua các kênh khác nhau (email, thông báo ứng dụng, v.v.).

**Quan hệ:**
- Hệ thống thông báo tương tác với cả Giao diện người dùng và Hệ thống Cảnh báo để thông báo cho người dùng về các cảnh báo.
- Hệ thống thông báo cũng tương tác với Hệ thống Báo cáo để thông báo cho người dùng về các báo cáo.

### 5.8.7. Database (Cơ sở dữ liệu)
**Phương thức:**
- `storeReportData()`: Lưu trữ dữ liệu báo cáo trong cơ sở dữ liệu.
- `storeAlertData()`: Lưu trữ dữ liệu cảnh báo trong cơ sở dữ liệu.
- `executeQueriesForReports()`: Thực thi các truy vấn để truy xuất dữ liệu cần thiết cho báo cáo.
- `executeQueriesForAlerts()`: Thực thi các truy vấn để truy xuất dữ liệu cần thiết cho cảnh báo.

**Quan hệ:**
- Cơ sở dữ liệu được truy cập bởi cả Hệ thống Báo cáo và Hệ thống Cảnh báo để lưu trữ và truy vấn dữ liệu.

## 5.9 Quản lý Thông tin Liên Lạc 
### 5.9.1. Message (Tin nhắn)
**Phương thức:**
- `storeMessageContent()`: Lưu trữ nội dung của tin nhắn.
- `trackMessageStatus()`: Theo dõi trạng thái hiện tại của tin nhắn (ví dụ: đã gửi, đã nhận, đã đọc).
- `manageMessageState()`: Quản lý các trạng thái khác nhau của tin nhắn trong suốt vòng đời của nó.

**Quan hệ:**
- Lớp Message là một phần của CommunicationSystem, nơi tin nhắn được xử lý và theo dõi.

### 5.9.2. CommunicationSystem (Hệ thống giao tiếp)
**Phương thức:**
- `sendMessage()`: Gửi tin nhắn đến người nhận.
- `receiveMessage()`: Nhận tin nhắn từ người gửi.
- `processMessages()`: Xử lý các tin nhắn đã nhận hoặc đã gửi.
- `trackMessageEvents()`: Theo dõi các sự kiện liên quan đến tin nhắn (ví dụ: gửi, nhận, đọc).

**Quan hệ:**
- Hệ thống giao tiếp tương tác với MessageQueue để quản lý việc giao tin nhắn và thứ tự của chúng.
- Hệ thống giao tiếp cũng tương tác với Người dùng để gửi và nhận tin nhắn.

### 5.9.3. User (Người dùng)
**Phương thức:**
- `sendMessage()`: Gửi tin nhắn đến người dùng khác.
- `receiveMessage()`: Nhận tin nhắn từ người dùng khác.
- `accessMessageHistory()`: Truy cập lịch sử các tin nhắn đã gửi hoặc đã nhận.

**Quan hệ:**
- Người dùng tương tác với Hệ thống giao tiếp để gửi, nhận và truy cập tin nhắn.

### 5.9.4. NotificationSystem (Hệ thống thông báo)
**Phương thức:**
- `sendNewMessageNotification()`: Thông báo cho người dùng khi họ nhận được tin nhắn mới.
- `notifyUserOfChanges()`: Thông báo cho người dùng về sự thay đổi trong tin nhắn hoặc trạng thái giao tin.
- `sendNotificationsThroughChannels()`: Gửi thông báo qua các kênh khác nhau (ví dụ: email, thông báo đẩy).

**Quan hệ:**
- Hệ thống thông báo tương tác với Người dùng để thông báo cho họ về tin nhắn mới hoặc cập nhật.

### 5.9.5. MessageQueue (Hàng đợi tin nhắn)
**Phương thức:**
- `storeMessages()`: Lưu trữ tin nhắn trong hàng đợi để xử lý hoặc giao tin.
- `processMessagesInOrder()`: Đảm bảo tin nhắn được xử lý và giao đúng thứ tự.
- `manageMessageDelivery()`: Quản lý việc giao tin nhắn đến người dùng.

**Quan hệ:**
- MessageQueue tương tác với Hệ thống giao tiếp để quản lý việc giao tin nhắn.

### 5.9.6. UserInterface (Giao diện người dùng)
**Phương thức:**
- `displayMessages()`: Hiển thị các tin nhắn cho người dùng theo định dạng dễ đọc.
- `sendMessage()`: Cho phép người dùng gửi tin nhắn.
- `viewMessageHistory()`: Hiển thị lịch sử tin nhắn.
- `manageMessages()`: Quản lý và tổ chức tin nhắn cho người dùng.

**Quan hệ:**
- Giao diện người dùng tương tác với Hệ thống giao tiếp để gửi và nhận tin nhắn.
- Giao diện người dùng cũng làm việc với Hệ thống thông báo để thông báo cho người dùng.
- Giao diện người dùng tương tác với MessageQueue để quản lý và hiển thị tin nhắn.

## 5.10 Quản lý Môi Trường và Điều Kiện Thiên Nhiên  
### 5.10.1. EnvironmentalSensor (Cảm biến môi trường)
**Phương thức:**
- `collectEnvironmentalData()`: Thu thập dữ liệu môi trường theo thời gian thực (ví dụ: nhiệt độ, độ ẩm, chất lượng không khí).
- `reportChanges()`: Báo cáo những thay đổi trong điều kiện môi trường.
- `detectPotentialIssues()`: Phát hiện các vấn đề tiềm ẩn trong môi trường dựa trên dữ liệu cảm biến.

**Quan hệ:**
- EnvironmentalSensor cung cấp dữ liệu cho MonitoringSystem.

### 5.10.2. MonitoringSystem (Hệ thống giám sát)
**Phương thức:**
- `monitorSensorData()`: Giám sát dữ liệu từ cảm biến môi trường.
- `analyzeData()`: Phân tích dữ liệu thu thập được để phát hiện các xu hướng và vấn đề.
- `detectEnvironmentalAnomalies()`: Phát hiện bất thường môi trường dựa trên dữ liệu từ cảm biến.

**Quan hệ:**
- MonitoringSystem tương tác với DataLogger để lưu trữ dữ liệu cảm biến.
- MonitoringSystem liên lạc với NotificationSystem để kích hoạt cảnh báo khi có vấn đề.
- MonitoringSystem tương tác với WeatherForecastSystem để dự báo thời tiết.

### 5.10.3. DataLogger (Máy ghi dữ liệu)
**Phương thức:**
- `storeSensorData()`: Lưu trữ dữ liệu từ cảm biến môi trường.
- `retrieveData()`: Truy xuất dữ liệu đã lưu để phân tích.
- `analyzeHistoricalData()`: Phân tích dữ liệu lịch sử để xác định xu hướng hoặc bất thường.

**Quan hệ:**
- DataLogger tương tác với UserInterface để hiển thị dữ liệu đã lưu hoặc đã phân tích.

### 5.10.4. WeatherForecastSystem (Hệ thống dự báo thời tiết)
**Phương thức:**
- `provideWeatherForecast()`: Cung cấp dự báo thời tiết dựa trên dữ liệu thu thập được.
- `updateWeatherAlerts()`: Cập nhật cảnh báo thời tiết (ví dụ: cảnh báo bão, lũ lụt).
- `generateSevereWeatherWarnings()`: Tạo ra các cảnh báo thời tiết nghiêm trọng.

**Quan hệ:**
- WeatherForecastSystem tương tác với MonitoringSystem để thu thập dữ liệu cần thiết cho dự báo.
- WeatherForecastSystem tương tác với NotificationSystem để gửi cảnh báo về thời tiết cho người dùng.

### 5.10.5. NotificationSystem (Hệ thống thông báo)
**Phương thức:**
- `sendAlert()`: Gửi cảnh báo liên quan đến vấn đề môi trường hoặc thời tiết.
- `notifyEnvironmentalIssues()`: Thông báo cho người dùng về các vấn đề môi trường tiềm ẩn.
- `notifyWeatherWarnings()`: Thông báo cho người dùng về các cảnh báo hoặc dự báo thời tiết.

**Quan hệ:**
- NotificationSystem tương tác với UserInterface để thông báo cho người dùng về các vấn đề.
- NotificationSystem làm việc với WeatherForecastSystem để thông báo cho người dùng về các cảnh báo thời tiết.

### 5.10.6. UserInterface (Giao diện người dùng)
**Phương thức:**
- `displayEnvironmentalData()`: Hiển thị dữ liệu môi trường thu thập được cho người dùng.
- `showWeatherForecasts()`: Hiển thị các dự báo thời tiết cho người dùng.
- `analyzeEnvironmentalTrends()`: Cho phép người dùng phân tích các xu hướng môi trường lâu dài.
- `trackEmergencyEvents()`: Theo dõi các sự kiện khẩn cấp (ví dụ: bão, sóng nhiệt).

**Quan hệ:**
- UserInterface tương tác với MonitoringSystem, NotificationSystem, và DataLogger để hiển thị dữ liệu, nhận cảnh báo và phân tích dữ liệu.

### 5.10.7. MaintenanceSchedule (Lịch bảo trì)
**Phương thức:**
- `manageMaintenance()`: Quản lý lịch bảo trì cho các cảm biến môi trường.
- `trackMaintenanceHistory()`: Theo dõi lịch sử bảo trì của các cảm biến.
- `scheduleSensorMaintenance()`: Lên lịch bảo trì cho các cảm biến để đảm bảo tính chính xác.

**Quan hệ:**
- MaintenanceSchedule tương tác với EnvironmentalSensor để đảm bảo các cảm biến được bảo trì đúng cách.  


# 6. Kết luận  
## 6.1 Những vấn đề chính đã giải quyết  
- Đáp ứng nhu cầu thu thập và phân tích dữ liệu thời tiết:  
    - Cung cấp một giải pháp hiệu quả để thu thập dữ liệu từ các vùng xa xôi, góp phần hỗ trợ hệ thống thông tin thời tiết quốc gia.  
    - Đảm bảo tính chính xác và độ tin cậy cao trong việc đo lường và phân tích các thông số khí tượng.  
- Tự động hóa và tiết kiệm nguồn lực:  
    - Tự vận hành không cần sự can thiệp trực tiếp của con người, tối ưu hóa chi phí vận hành và bảo trì.  
    - Sử dụng năng lượng tái tạo một cách hiệu quả, phù hợp với các khu vực khó tiếp cận.  
- Kiến trúc và cơ chế hỗ trợ hoạt động bền vững:  
    - Kiến trúc phân lớp "Layered Architecture" đảm bảo tính mở rộng, linh hoạt và dễ bảo trì.  
    - Các cơ chế như giám sát, lưu trữ và phục hồi dữ liệu, quản lý năng lượng, tái cấu hình, và bảo mật được thiết kế để đảm bảo hệ thống hoạt động liên tục ngay cả trong điều kiện môi trường khắc nghiệt.  
- Hỗ trợ nghiên cứu dài hạn và dự đoán thời tiết:  
    - Cung cấp dữ liệu đáng tin cậy để hỗ trợ các nghiên cứu khí hậu và cải thiện khả năng dự báo thời tiết.  

## 6.2 Hướng mở rộng  
- Nâng cấp khả năng phân tích dữ liệu:  
    - Áp dụng các công nghệ học máy (*machine learning*) để cải thiện việc phân tích và dự đoán dựa trên dữ liệu thu thập.  
- Mở rộng phạm vi hoạt động:  
    - Triển khai thêm các trạm tương tự tại các khu vực khác có điều kiện môi trường tương tự.  
- Tích hợp IoT và hệ thống cảnh báo thông minh:
    - Kết nối các trạm với mạng IoT để tăng cường khả năng giám sát thời gian thực.
    - Tự động gửi cảnh báo khi có sự cố hoặc thay đổi môi trường bất thường.
- Cải thiện bảo mật:  
    - Ứng dụng các giao thức bảo mật mới nhất để bảo vệ dữ liệu và đảm bảo an toàn hệ thống trước các nguy cơ tấn công mạng.

---

-> Tóm lại: Hệ thống trạm thời tiết vùng hẻo lánh không chỉ giải quyết các nhu cầu hiện tại mà còn mở ra hướng đi mới cho việc áp dụng công nghệ hiện đại trong lĩnh vực khí tượng, bảo vệ môi trường và dự báo thời tiết, góp phần nâng cao chất lượng cuộc sống và hỗ trợ phát triển bền vững. 


