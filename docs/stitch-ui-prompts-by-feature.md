# Bộ Prompt Thiết Kế Giao Diện Stitch MCP Theo Từng Chức Năng (FR-001 -> FR-019)

**Project:** Sports Center Management System (Hệ thống Quản lý Trung tâm Thể thao)  
**Tài liệu tham chiếu:** [blueprint.md](file:///Users/penpen1112003/Demo/WS_01_FU/blueprint.md) | [srs.txt](file:///Users/penpen1112003/Demo/WS_01_FU/srs.txt) | [stitch-ui-design.prompt.md](file:///Users/penpen1112003/Demo/WS_01_FU/.github/prompts/stitch-ui-design.prompt.md)  
**Công cụ thực thi:** Stitch MCP (`generate_screen_from_text`, `generate_variants`, `edit_screens`, `create_design_system`)  
**Mô hình AI:** `GEMINI_3_8_FLASH`  

---

## 🎨 Quy chuẩn Thiết kế Chung (Design System Guidelines)
- **Palette màu sắc:**
  - Nền Dark mode: Nền đen sâu (`#0B0F17`), thẻ phụ (`#151D2A`), viền mờ (`rgba(255,255,255,0.08)`).
  - Màu chủ đạo (Primary): Xanh thể thao rực rỡ (`#3B82F6` / `#6366F1`), Xanh lá năng lượng (`#10B981`).
  - Màu cảnh báo/nhấn (Accent): Cam hổ phách (`#F59E0B`), Đỏ san hô (`#EF4444`), Tím điện quang (`#8B5CF6`).
- **Typography:** `Inter` hoặc `Outfit`, phân cấp rõ ràng (H1 Display, H2 Section, Body 14px, Badge 12px Semibold).
- **Hiệu ứng:** Glassmorphism nhẹ (backdrop-blur, border gradient), bo góc mềm (`rounded-2xl`), đổ bóng chiều sâu.

---

## 📱 Danh mục Prompt Chi tiết theo Từng Chức Năng

### [FR-001] Xác thực tài khoản và Phân quyền RBAC 4 vai trò
- **Target Role:** Tất cả vai trò (Member, Coach, Receptionist, Center Manager)
- **Device Type:** `DESKTOP` & `MOBILE`
- **Stitch MCP Prompt:**
> "Thiết kế màn hình Đăng nhập (Sign In) hiện đại cho Hệ thống Quản lý Trung tâm Thể thao. Bố cục chia đôi (Split-screen) trên Desktop: Nửa bên trái là hình ảnh động lực thể thao với slogan 'Level Up Your Fitness' cùng hiệu ứng gradient neon; nửa bên phải là form đăng nhập tối giản. Form gồm: Logo trung tâm, tiêu đề chào mừng, ô nhập Email/Số điện thoại, ô Mật khẩu có icon ẩn/hiện, nút 'Quên mật khẩu', nút bấm CTA chính 'Đăng nhập vào hệ thống'. Phía dưới có thanh chuyển đổi tab nhanh mô phỏng 4 vai trò demo: [Member | Coach | Receptionist | Center Manager] để chuyển đổi nhanh quyền truy cập. Giao diện Dark theme cao cấp, bo góc viền 16px, hiệu ứng glassmorphism."

---

### [FR-002] Quản lý hồ sơ thành viên (Tạo mới, cập nhật, khóa/mở)
- **Target Role:** Receptionist (Lễ tân) / Center Manager (Quản lý)
- **Device Type:** `DESKTOP`
- **Stitch MCP Prompt:**
> "Thiết kế màn hình Quản lý Danh sách Thành viên (Member Directory) dành cho Lễ tân và Quản lý trên Desktop. Header có thanh tìm kiếm thông minh theo Tên/SĐT/Mã Member ID, bộ lọc theo Trạng thái (Hoạt động, Sắp hết hạn, Đã khóa) và nút '+ Thêm thành viên mới'. Khu vực chính là Bảng dữ liệu (Data table) hiện đại: Cột Avatar + Tên, Mã hội viên, SĐT, Gói tập hiện tại, Ngày đăng ký, Badge trạng thái (Active màu xanh lá, Suspended màu vàng, Locked màu đỏ) và Cột Thao tác (Xem chi tiết, Sửa, Khóa tài khoản). Kèm ngăn kéo trượt (Slide-over drawer) bên phải hiển thị Form tạo mới/chỉnh sửa thông tin hội viên có tải ảnh đại diện và thông tin liên hệ khẩn cấp."

---

### [FR-003] Cấu hình danh mục gói tập thể thao
- **Target Role:** Center Manager
- **Device Type:** `DESKTOP`
- **Stitch MCP Prompt:**
> "Thiết kế màn hình Cấu hình Danh mục Gói tập (Membership Packages Config) cho Quản lý trung tâm. Bố cục dạng Lưới thẻ (Card Grid 3 cột): Mỗi thẻ đại diện cho một gói tập (Gói Tháng Gym, Gói Yoga 3 Tháng, Gói VIP Full-Access 1 Năm). Trên thẻ hiển thị: Tên gói, mức giá nổi bật (VND), thời hạn sử dụng, số buổi tập tối đa, danh sách tiện ích tích hợp (tick xanh), huy hiệu 'Bán chạy nhất' (Best Seller) và nút bật/tắt (Toggle) trạng thái kinh doanh. Phía trên có nút '+ Tạo gói tập mới' mở Modal nhập liệu với các trường: Tên gói, Giá niêm yết, Số ngày hiệu lực, Bộ môn áp dụng (Checkboxes), và Ràng buộc giờ tập."

---

### [FR-004] Kích hoạt và theo dõi trạng thái gói tập
- **Target Role:** Member & Receptionist
- **Device Type:** `MOBILE` (App Học viên) & `DESKTOP` (Quầy Lễ tân)
- **Stitch MCP Prompt:**
> "Thiết kế màn hình Mobile 'Thẻ Hội Viên Điện Tử & Gói Tập Của Tôi' cho Học viên. Phần trên cùng là Thẻ hội viên số (Digital Member Card) hiệu ứng Holographic gradient chuyển động: hiển thị Mã thẻ VIP, Tên học viên, Mã QR động check-in tại quầy, ngày hết hạn gói. Phần thân dưới hiển thị trạng thái chi tiết gói tập: Thanh tiến trình (Progress bar) thể hiện thời gian đã sử dụng và số ngày còn lại; Số buổi tập đã tham gia/tổng số buổi; Nút CTA lớn 'Gia hạn gói tập ngay'. Bên dưới là danh sách lịch sử các lần gia hạn và hóa đơn thanh toán đã thanh toán."

---

### [FR-005] Lập thời khóa biểu và phân công HLV / Phòng tập
- **Target Role:** Center Manager
- **Device Type:** `DESKTOP`
- **Stitch MCP Prompt:**
> "Thiết kế màn hình Lập Thời Khóa Biểu Tuần (Weekly Class Schedule Builder) cho Quản lý trung tâm. Giao diện dạng Calendar Grid kéo thả (Drag-and-Drop) từ Thứ 2 đến Chủ nhật, trục tung là các khung giờ từ 06:00 đến 21:00. Mỗi ô lớp học trên lịch là một Card màu sắc phân theo bộ môn (Yoga xanh dương, Gym cam, Boxing đỏ, Pilates tím) hiển thị: Tên lớp, Tên HLV phụ trách kèm avatar, Phòng tập chỉ định, Sĩ số hiện tại (ví dụ: 15/20). Thanh công cụ trên cùng có nút lọc theo Phòng tập, lọc theo HLV, chuyển đổi chế độ xem Ngày/Tuần/Tháng và nút '+ Thêm lịch lớp'."

---

### [FR-006] Cơ chế cảnh báo và ngăn chặn xung đột lịch học
- **Target Role:** Center Manager
- **Device Type:** `DESKTOP`
- **Stitch MCP Prompt:**
> "Thiết kế Modal Cảnh báo Xung đột Lịch học (Schedule Conflict Alert Dialog) trên cổng Quản lý. Khi Manager kéo thả lớp hoặc chọn giờ trùng: Modal hiển thị icon cảnh báo đỏ nổi bật, tiêu đề 'Phát hiện xung đột lịch vận hành!'. So sánh trực quan 2 cột: Cột 1 là Lớp học hiện tại đã có lịch (HLV Tuấn, Phòng Yoga 1, 08:00 - 09:30); Cột 2 là Lớp học mới dự kiến xếp (HLV Tuấn, Phòng Gym 2, 08:30 - 10:00). Nêu rõ lý do vi phạm: 'HLV Tuấn đã có ca dạy trùng 60 phút'. Cung cấp 2 hành động: Nút 'Tự động tìm HLV khác còn trống ca' và nút phụ 'Hủy thay đổi để chọn khung giờ khác'."

---

### [FR-007] Đặt chỗ lớp học thể thao trực tuyến cho Hội viên
- **Target Role:** Member
- **Device Type:** `MOBILE`
- **Stitch MCP Prompt:**
> "Thiết kế màn hình Mobile App 'Khám phá & Đặt chỗ Lớp học' cho Hội viên. Header có thanh chọn ngày dạng cuộn ngang (Horizontal date picker) trong tuần. Thanh lọc nhanh theo bộ môn dạng Chips (Tất cả, Gym, Yoga, Zumba, Kickboxing). Danh sách lớp học hiển thị dạng Card trực quan: Ảnh đại diện lớp học, Giờ tập (07:00 - 08:00), Phòng tập, HLV kèm đánh giá sao, Thanh hiển thị sĩ số (còn 3/20 chỗ trống), Huy hiệu 'Được đặt bằng gói hiện tại'. Nút bấm 'Đặt chỗ ngay' màu xanh neon nổi bật. Nhấn vào hiển thị Bottom-sheet tóm tắt chi tiết lớp học và nút xác nhận giữ chỗ."

---

### [FR-008] Hủy lịch đặt lớp học có điều kiện
- **Target Role:** Member
- **Device Type:** `MOBILE`
- **Stitch MCP Prompt:**
> "Thiết kế màn hình Mobile 'Lịch Tập Của Tôi & Hủy Lớp Học'. Hiển thị danh sách các lớp đã đăng ký sắp tới. Mỗi lớp có đồng hồ đếm ngược tới giờ bắt đầu. Nút 'Hủy lịch đặt' hiển thị rõ điều kiện: 'Miễn phí hủy trước 2 tiếng'. Khi nhấn hủy: Hiển thị Popup xác nhận cảnh báo nếu thời gian hủy hợp lệ (hủy thành công và hoàn trả slot) hoặc cảnh báo nếu hủy sát giờ (< 2 tiếng) sẽ bị ghi nhận điểm chuyên cần hoặc mất lượt tập theo chính sách trung tâm."

---

### [FR-009] Cảnh báo và hiển thị lớp học sắp đầy (>= 90%)
- **Target Role:** Center Manager & Member
- **Device Type:** `DESKTOP` (Quản lý) & `MOBILE` (Học viên)
- **Stitch MCP Prompt:**
> "Thiết kế giao diện Thẻ Lớp Học Đạt Trạng Thái Sắp Đầy (Capacity Alert Badge >= 90%). Trên Mobile App: Thẻ lớp học gắn huy hiệu 'CHỈ CÒN 2 CHỖ' màu cam chớp nhẹ, thanh sĩ số chuyển màu đỏ rực rỡ thôi thúc hội viên nhanh tay đặt chỗ. Trên Dashboard Quản lý: Bảng thông báo khẩn các lớp có sĩ số >= 90% kèm nút thao tác nhanh: 'Mở thêm lớp phụ' hoặc 'Nâng cấp sang phòng tập lớn hơn' để tối đa hóa doanh thu."

---

### [FR-010] Ghi nhận thanh toán và in/xuất hóa đơn tại quầy
- **Target Role:** Receptionist
- **Device Type:** `DESKTOP`
- **Stitch MCP Prompt:**
> "Thiết kế màn hình POS Thu tiền & Xuất hóa đơn Quầy Lễ Tân trên Desktop. Bố cục 2 phần: Bên trái là form chọn Hội viên và gói tập/dịch vụ phát sinh (kèm giảm giá coupon nếu có); Bên phải là Tóm tắt thanh toán: Tạm tính, Thuế VAT, Tổng tiền thanh toán lớn nổi bật. Lựa chọn phương thức thanh toán dạng nút bấm lớn: [Tiền mặt | Quét mã VietQR Chuyển khoản | POS Thẻ]. Sau khi xác nhận thanh toán: Hiển thị ngay Preview Hóa đơn Điện tử (e-Invoice) với đầy đủ mã hóa đơn, thông tin trung tâm, mã QR tra cứu và 2 nút: 'In hóa đơn nhiệt 80mm' và 'Gửi hóa đơn qua Email/Zalo cho khách'."

---

### [FR-011] Dashboard và Báo cáo Doanh thu & Vận hành trực quan
- **Target Role:** Center Manager
- **Device Type:** `DESKTOP`
- **Stitch MCP Prompt:**
> "Thiết kế Executive Dashboard Điều hành Trung tâm Thể thao cho Giám đốc trên Desktop. Thanh lọc thời gian (Hôm nay, Tuần này, Tháng này, Quý này, Tùy chọn). Hàng trên cùng gồm 4 KPI Cards bóng bẩy: Tổng doanh thu (kèm % tăng trưởng xanh lá), Số hội viên mới gia nhập, Tổng lượt check-in hôm nay, Tỷ lệ lấp đầy phòng tập trung bình (82%). Hàng tiếp theo: Biểu đồ đường (Line chart) doanh thu theo ngày so với mục tiêu; Biểu đồ tròn (Donut chart) tỷ trọng doanh thu theo gói tập (Gym 45%, Yoga 30%, PT 25%). Bảng top 5 lớp học đông khách nhất và biểu đồ nhiệt (Heatmap) khung giờ cao điểm."

---

### [FR-012] Điểm danh và Check-in hội viên bằng mã QR động
- **Target Role:** Receptionist & Coach
- **Device Type:** `DESKTOP` (Màn hình trạm Check-in Quầy) & `TABLET` (HLV tại phòng)
- **Stitch MCP Prompt:**
> "Thiết kế màn hình Trạm Check-in & Điểm danh Tự động tại Quầy lễ tân. Trung tâm màn hình là khung quét mã QR lớn sẵn sàng nhận camera/máy quét. Bên cạnh là ô nhập nhanh SĐT/Mã số hội viên. Khi quét thành công: Màn hình chuyển hiệu ứng chúc mừng xanh lá rực rỡ với âm thanh ping, hiển thị ảnh đại diện hội viên, Tên, Gói tập Active, Tên lớp học tham gia hôm nay (18:00 Yoga Cơ Bản) và số buổi còn lại. Bên dưới là danh sách 10 lượt check-in gần nhất hiển thị thời gian thực theo từng giây."

---

### [FR-013] Quản lý kế hoạch giáo án và bài tập nhóm/cá nhân
- **Target Role:** Coach (Huấn luyện viên)
- **Device Type:** `TABLET` / `DESKTOP`
- **Stitch MCP Prompt:**
> "Thiết kế màn hình Soạn Giáo Án & Kế Hoạch Tập Luyện (Workout Plan Builder) cho Huấn luyện viên. Header hiển thị tên lớp hoặc tên học viên cá nhân, mục tiêu thể lực (Tăng cơ, Giảm mỡ, Phục hồi). Thân trang là danh sách bài tập được chia theo nhóm cơ (Ngực, Lưng, Chân, Core). Mỗi bài tập có form nhập thông minh: Tên động tác (có thư viện gợi ý), Số Set, Số Reps, Khối lượng tạ (kg), Thời gian nghỉ giữa hiệp (giây) và Ghi chú kỹ thuật. Có nút 'Thêm bài tập từ Thư viện' và nút '+ Yêu cầu AI soạn giáo án mẫu'."

---

### [FR-014] Ghi nhận kết quả tập luyện và theo dõi tiến độ thể lực
- **Target Role:** Coach & Member
- **Device Type:** `MOBILE` & `TABLET`
- **Stitch MCP Prompt:**
> "Thiết kế màn hình Mobile 'Sổ Tay Thể Lực & Tiến Độ Tập Luyện' cho Học viên và Huấn luyện viên. Hiển thị biểu đồ theo dõi các chỉ số quan trọng theo tuần/tháng: Cân nặng, Tỷ lệ mỡ Body Fat %, Khối lượng cơ Bắp Muscle Mass và Chỉ số nâng tạ tối đa (1RM Bench Press, Squat, Deadlift). Dưới biểu đồ là timeline các buổi tập gần nhất kèm lời nhận xét, chấm điểm chuyên cần và huy hiệu thành tích (Streak 7 ngày liên tục, Kỷ lục mới) tạo động lực cao."

---

### [FR-015] Tích hợp AI gợi ý bài tập cá nhân hóa theo thể trạng
- **Target Role:** Member & Coach
- **Device Type:** `MOBILE`
- **Stitch MCP Prompt:**
> "Thiết kế giao diện 'Trợ Lý AI Gợi Ý Lộ Trình Tập Luyện Cá Nhân Hóa'. Gồm bước nhập nhanh thông số thể trạng: Giới tính, Độ tuổi, Chiều cao, Cân nặng, Mục tiêu (Giảm cân, Tăng cơ, Dẻo dai), Thói quen sinh hoạt và Tiền sử chấn thương (ví dụ: Đau khớp gối). Sau khi nhấn 'Phân tích cùng AI': Hiển thị giao diện kết quả đẹp mắt với thẻ phân tích thể trạng, cảnh báo vùng cần tránh tải trọng, và Lộ trình 3 giai đoạn kèm danh sách 4 bài tập an toàn tối ưu được AI đề xuất riêng biệt."

---

### [FR-016] Tích hợp Chatbot AI hỗ trợ tư vấn hội viên 24/7
- **Target Role:** Member
- **Device Type:** `MOBILE`
- **Stitch MCP Prompt:**
> "Thiết kế giao diện Chatbot AI Thông Minh 'Sports Center Virtual Assistant' cho Học viên trên Mobile. Header có avatar AI Bot kèm trạng thái 'Đang trực tuyến 24/7'. Khung chat có các bong bóng tin nhắn hiển thị đẹp mắt, hỗ trợ hiển thị thẻ tương tác (Rich Cards) trong tin nhắn: Thẻ thông tin gói tập có nút mua ngay, Thẻ lịch lớp học có nút đặt chỗ trực tiếp, Gợi ý câu hỏi nhanh dạng pill tags (ví dụ: 'Hôm nay có lớp Yoga nào?', 'Gói tập của tôi còn bao nhiêu ngày?', 'Quy định bảo lưu gói?'). Thanh nhập liệu có icon đính kèm ảnh và micro nhập giọng nói."

---

### [FR-017] Cơ chế gửi thông báo đẩy nhắc lịch học và hạn gói tập
- **Target Role:** Member & Center Manager
- **Device Type:** `MOBILE` (Trung tâm thông báo) & `DESKTOP` (Trình quản trị thông báo)
- **Stitch MCP Prompt:**
> "Thiết kế màn hình Mobile 'Trung tâm Thông báo' (Notification Center) cho Hội viên. Phân loại theo tabs: [Tất cả | Lịch học | Gói tập | Ưu đãi]. Thẻ thông báo nhắc lịch học có icon đồng hồ: 'Nhắc nhở: Buổi tập Yoga Flow bắt đầu sau 60 phút tại Phòng 2', có nút CTA 'Xem vé QR' hoặc 'Báo bận'. Thẻ thông báo gia hạn có icon cảnh báo vàng: 'Gói tập của bạn sẽ hết hạn sau 7 ngày', có nút CTA 'Gia hạn nhận ưu đãi 10%'."

---

### [FR-018] Hệ thống ghi log kiểm toán bất biến (Audit Trail Logging)
- **Target Role:** Center Manager
- **Device Type:** `DESKTOP`
- **Stitch MCP Prompt:**
> "Thiết kế màn hình Tra Cứu Nhật Ký Kiểm Toán (Audit Trail Log Viewer) dành riêng cho Center Manager trên Desktop. Header có bộ lọc đa chiều: Khoảng ngày giờ, Tác nhân thực hiện (User/Role), Loại hành động (CREATE, UPDATE, DELETE, OVERRIDE, CANCEL_BILL), và Đối tượng (Bảng giá, Phân quyền, Lịch học, Hóa đơn). Bảng dữ liệu hiển thị: Timestamp chính xác đến mili-giây, Tên tài khoản + IP Hash, Hành động (kèm badge màu), Đối tượng bị tác động, Nút 'Xem chi tiết Diff'. Khi bấm xem: Hiển thị Modal so sánh JSON Diff trực quan (Giá trị cũ màu đỏ, Giá trị mới màu xanh lá) bảo đảm tính bất biến minh bạch."

---

### [FR-019] Hệ thống mẫu Prompt và quy chuẩn sinh giao diện người dùng bằng Stitch MCP
- **Target Role:** Tech Lead, Frontend Developer & UI/UX Designer
- **Device Type:** `DESKTOP`
- **Stitch MCP Prompt:**
> "Thiết kế màn hình Portal Quản trị Thư viện Thiết kế & Prompt Stitch MCP (Design System & Prompt Registry Hub). Giao diện mang phong cách Developer/Design Hub: Bên trái là cây thư mục các module theo vai trò (Member Mobile, Coach Tablet, Receptionist Desktop, Manager Portal). Trung tâm là trình xem trước trực tiếp (Live Preview) màn hình sinh từ Stitch, kèm bộ chọn độ phân giải thiết bị (iPhone, iPad, Desktop 1920x1080). Bên dưới là hộp mã (Code / Prompt Box) chứa prompt chuẩn, danh sách Design Tokens (Màu sắc, Typography, Spacing) và nút 'Copy Prompt' hoặc 'Tạo biến thể mới qua Stitch MCP'."
