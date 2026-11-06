# CNTT1-nh-p-m-n-c-ng-ngh-th-ng-tin-Session21_Ex09
## Phần 1: Thiết kế Prompt 3 Thành phần Chuẩn hóa

**1. Nguyên nhân khiến AI trả lời sai (Ảo giác AI):**
Câu hỏi *"AI ơi phần mềm trạm sạc của tôi bị hỏng rồi"* quá chung chung, không có thông tin về hệ điều hành, tên phần mềm hay nhật ký lỗi. AI không đủ dữ liệu đầu vào nên buộc phải phỏng đoán theo xác suất từ khóa, dẫn đến câu trả lời đưa ra hướng giải quyết phần cứng (tháo vỏ, kiểm tra dây) thay vì xử lý đúng bản chất lỗi phần mềm.

**2. Prompt 3 Thành phần chuẩn:**

text

[Context]
Tôi là kỹ thuật viên trực ca tại Bến xe Miền Đông. Trụ sạc nhanh số 04 của trạm VoltCharge (chạy Windows 11) bị dừng đột ngột và báo lỗi khi khởi động ControllerDaemon.


[Raw Error]

2026-09-21 21:15:30 [FATAL] ControllerDaemon failed to start.

System.UnauthorizedAccessException: Access to the path 'C:\Program Files\VoltCharge\data\session.log' is denied.

at System.IO.FileStream.ValidateFileHandle(SafeFileHandle handle)

  at VoltCharge.Core.SessionManager.Initialize()

InnerException: None. Process terminated with exit code 5 (0x00000005).

Suggestion: Run the application with elevated administrator privileges or verify NTFS file permissions.



[Instruction]

Giải thích nguyên nhân lỗi bằng tiếng Việt đơn giản cho nhân viên mới và cho 3 bước xử lý cụ thể trên Windows 11 để khắc phục.





## Phần 2: Giải mã Lỗi & Kịch bản Khắc phục

**3. Giải thích lỗi:**
Lỗi `UnauthorizedAccessException` (mã exit code 5) có nghĩa là phần mềm muốn ghi dữ liệu vào file `session.log` nhưng bị hệ thống từ chối. Giống như việc phần mềm cố mở cửa phòng để cất đồ nhưng lại không có chìa khóa. Thư mục `Program Files` được Windows bảo mật rất kỹ, nếu chạy ứng dụng bằng tài khoản thường mà không có quyền Quản trị viên (Admin) thì hệ thống sẽ chặn lại ngay.

**4. 3 bước xử lý tại chỗ trên Windows 11:**

1. **Chạy quyền Admin:** Nhấp chuột phải vào icon phần mềm VoltCharge -> chọn **Run as administrator**.
2. **Cấp quyền cho thư mục data:** Tìm đến `C:\Program Files\VoltCharge\`, nhấp chuột phải vào thư mục `data` -> chọn **Properties** -> chuyển qua thẻ **Security** -> nhấn **Edit** -> chọn nhóm `Users` -> tích chọn **Full control** (hoặc **Modify**) rồi bấm **OK**.
3. **Khởi động lại phần mềm:** Mở lại chương trình và kiểm tra xem trụ sạc số 04 đã nhận điện bình thường chưa.

**5. Bẫy an ninh (API Key):**

* **Cách xử lý:** Xóa hoặc thay thế chuỗi `API_KEY: volt_secret_token_889922` thành `API_KEY: [REDACTED]` trước khi gửi lên AI.
* **Lý do:** Các hệ thống AI công cộng có thể lưu lại dữ liệu chat để huấn luyện mô hình. Nếu để lộ chìa khóa bảo mật (API Key), kẻ xấu có thể lợi dụng token này để xâm nhập, chiếm quyền điều khiển hoặc làm rò rỉ dữ liệu của trạm sạc.
