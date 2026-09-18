---
mode: agent
description: "Use when: the user wants to generate UI screens, design systems, wireframes, or interactive prototypes using Stitch MCP for any module, role, or feature in the project."
---

# Stitch UI Design & Prototyping Prompt

Dùng prompt này để yêu cầu AI Agent hoặc Development Agent thiết kế và sinh giao diện người dùng (UI screens / prototypes) bằng công cụ **Stitch MCP** cho hệ thống Sports Center Management System (hoặc bất kỳ tính năng nào theo yêu cầu).

---

## 1. Mục tiêu (Objective)
Tự động hóa quy trình thiết kế UI/UX từ tài liệu yêu cầu (SRS, Blueprint, User Stories) thành các màn hình hoàn chỉnh, đạt chuẩn thẩm mỹ cao (Glassmorphism, Dark/Light mode chuẩn, Micro-interactions, Typography phân cấp rõ ràng, Responsive cho Desktop & Mobile) thông qua bộ công cụ **Stitch MCP**.

---

## 2. Quy trình thực hiện (Workflow)

### Bước 1: Tiếp nhận yêu cầu & Phân tích vai trò (Context & Role Intake)
- Xác định đối tượng người dùng / vai trò:
  - **Member (Học viên):** Giao diện Mobile/Responsive tập trung trải nghiệm nhanh (xem lịch tập, đăng ký/hủy lớp, gia hạn gói, hỏi trợ lý AI).
  - **Coach (Huấn luyện viên):** Mobile/Tablet hỗ trợ xem lịch dạy, điểm danh học viên, đánh giá tiến độ, xem gợi ý bài tập AI.
  - **Receptionist (Lễ tân):** Desktop Web thao tác quầy nhanh (check-in/điểm danh, tạo thành viên mới, xử lý thanh toán/in hóa đơn, tra cứu gói tập).
  - **Center Manager (Quản lý):** Desktop Web với Dashboard điều hành tổng quát, KPI doanh thu theo thời gian, tỷ lệ lấp đầy lớp học, quản lý nhân sự và audit log.
- Thu thập danh sách các thành phần cốt lõi: Header/Nav, Sidebar, Filter bar, Data table, Card grid, Action modal, Toast alert, Empty & Loading states.

### Bước 2: Khởi tạo Stitch Workspace & Design System
- Kiểm tra hoặc tạo mới Stitch Project:
  ```json
  // StitchMCP: create_project
  {}
  ```
- Khởi tạo hoặc áp dụng Design System chuẩn đồng nhất:
  - Sử dụng `create_design_system` hoặc `create_design_system_from_design_md` với token màu sắc (Primary: Indigo/Emerald/Blue, Neutral dark/light, Accent: Amber/Cyan), Typography (Inter, Roboto, Poppins), Border radius và Spacing scale.
  - Sử dụng `apply_design_system` để đồng bộ toàn bộ các màn hình trong cùng dự án.

### Bước 3: Sinh màn hình chi tiết từ Prompt (Generate Screen)
- Gọi công cụ Stitch MCP `generate_screen_from_text`:
  - `projectId`: ID dự án Stitch vừa tạo/truy xuất.
  - `deviceType`: `DESKTOP` (cho Portal Quản lý/Lễ tân) hoặc `MOBILE` (cho App Học viên/HLV).
  - `modelId`: `GEMINI_3_8_FLASH`.
  - `prompt`: Cung cấp mô tả chi tiết màn hình theo cấu trúc chuẩn:
    - **Tên màn hình & Vai trò**
    - **Header & Navigation**
    - **Khu vực nội dung chính & Bố cục (Layout)**
    - **Bảng dữ liệu / Danh sách thẻ / Biểu đồ trực quan**
    - **Form nhập liệu / Modal xác nhận / Trạng thái tương tác (Hover, Active, Disabled)**
    - **Tone & Mood:** Hiện đại, tối giản, bóng đổ mềm mại, viền tinh tế.

### Bước 4: Tinh chỉnh & Tạo biến thể (Refine & Variants)
- Dùng `get_screen` để kiểm tra kết quả thiết kế.
- Dùng `generate_variants` để tạo 2-3 phương án layout/style khác nhau cho cùng một màn hình để khách hàng/BA lựa chọn.
- Dùng `edit_screens` để tinh chỉnh chi tiết các component theo feedback.

### Bước 5: Bàn giao & Đồng bộ bằng chứng (Traceability & Delivery)
- Lưu ID màn hình (`screenId`), link xem trước và mã token thiết kế vào báo cáo:
  - File báo cáo bàn giao: `Development-Agent/templates/delivery-report.md` (mục Stitch Evidence).
  - Cập nhật tiến độ và comment bằng chứng lên GitHub Issue & GitHub Project #19.

---

## 3. Danh mục Prompt mẫu nhanh (Quick Prompt Templates)

### Template 1: Màn hình Đặt lớp học cho Member (Mobile App)
> "Thiết kế màn hình Mobile App 'Đăng ký lớp học' cho học viên Sports Center. Gồm: Thanh tìm kiếm và bộ lọc nhanh theo bộ môn (Yoga, Gym, Boxing, Pilates), lọc theo ngày trong tuần. Danh sách các lớp học hiển thị dạng Card trực quan với thông tin: tên lớp, HLV phụ trách, thời gian, phòng tập, số chỗ còn trống (hiển thị thanh tiến độ lấp đầy), nút 'Đặt chỗ ngay'. Kèm tab chuyển đổi sang 'Lớp đã đăng ký' và popup xác nhận đặt lớp."

### Template 2: Dashboard Vận hành & Doanh thu cho Center Manager (Desktop Portal)
> "Thiết kế Dashboard điều hành Desktop Portal cho Center Manager trung tâm thể thao. Giao diện Dark theme sang trọng, thanh bên Sidebar tinh gọn. Header có thông báo và avatar. Phần chính gồm: 4 thẻ KPI nổi bật (Doanh thu tháng, Hội viên mới, Số lớp đang mở, Tỷ lệ lấp đầy). Biểu đồ đường doanh thu 12 tháng, biểu đồ tròn phân bổ theo loại gói tập. Bảng danh sách 10 giao dịch nạp tiền/gia hạn gần nhất kèm trạng thái badge (Đã thanh toán, Chờ xử lý)."

### Template 3: Màn hình Lễ tân Check-in & Điểm danh tại quầy (Desktop Web)
> "Thiết kế màn hình Desktop 'Lễ tân - Điểm danh và Check-in học viên tại quầy'. Gồm: Ô tìm kiếm thông minh (tìm theo Mã hội viên, SĐT hoặc Tên) với gợi ý tự động. Thẻ thông tin nhanh của học viên: Ảnh đại diện, gói tập hiện tại, ngày hết hạn gói, số buổi còn lại, cảnh báo nếu gói sắp hết hạn. Nút bấm Check-in lớn nổi bật với âm thanh phản hồi trực quan. Lịch sử 15 lượt check-in gần nhất trong ngày hiển thị thời gian thực."

---

## 4. Bảng tra cứu Tool Stitch MCP

| Tên Tool | Chức năng chính | Gợi ý tham số |
|---|---|---|
| `create_project` | Tạo dự án thiết kế mới | `{}` |
| `generate_screen_from_text` | Sinh giao diện từ văn bản mô tả | `projectId`, `prompt`, `deviceType`, `modelId` |
| `get_screen` | Lấy chi tiết màn hình đã sinh | `projectId`, `screenId` |
| `list_screens` | Liệt kê tất cả màn hình trong dự án | `projectId` |
| `generate_variants` | Tạo các biến thể khác nhau của màn hình | `projectId`, `screenId`, `prompt` |
| `edit_screens` | Sửa màn hình theo hướng dẫn | `projectId`, `screenId`, `editPrompt` |
| `create_design_system` | Tạo bộ Design System chuẩn hóa | `name`, `colorPalette`, `typography` |
| `apply_design_system` | Gắn Design System vào màn hình | `projectId`, `designSystemId` |
