# Draft Issue: [FR-001] Đăng ký lớp học cho thành viên

## 1. Summary
Cho phép thành viên xem danh sách lớp học và đăng ký trực tiếp trên hệ thống với các kiểm tra tự động về gói tập, xung đột lịch và số chỗ còn lại.

## 2. Project fields draft
- Status: Ready for Review
- Priority: High
- Type: Feature
- Area: Member / Class booking
- Owner: Product or Backend Team
- Iteration: Sprint 1
- Target date: TBD
- Blueprint ID: BPD-001
- Risk: Medium

## 3. Business context
Thành viên gặp khó khăn khi đăng ký lớp theo cách thủ công, dễ xảy ra lỗi trùng lịch hoặc thiếu thông tin về lớp còn chỗ. Chức năng này giúp tăng hiệu quả và tự động hóa quy trình đăng ký.

## 4. Acceptance criteria
- Thành viên đã đăng nhập và có gói tập còn hiệu lực có thể xem danh sách lớp học đang mở.
- Khi chọn một lớp có chỗ trống, hệ thống tạo bản ghi đăng ký thành công.
- Khi lớp đã đầy, hệ thống từ chối đăng ký và hiển thị thông báo rõ ràng.
- Khi thời gian đăng ký trùng với lịch đã có, hệ thống chặn và thông báo xung đột lịch.
- Thành viên có thể hủy đăng ký trong thời hạn cho phép và cập nhật trạng thái đúng.

## 5. Dependencies
- User authentication và authorization
- Membership validation service
- Class schedule and capacity data
- Audit/logging service

## 6. Risks
- Chưa xác định thời hạn hủy lớp
- Chưa xác định quy tắc chặn khi lớp gần đầy
- Cần đồng bộ rõ ràng giữa gói tập và lịch học

## 7. GitHub Project sync plan
- Title: [FR-001] Đăng ký lớp học cho thành viên
- BE repository: Pen1112003/Sports_Center_Management_System-UAT-BE
- FE repository: Pen1112003/Sports_Center_Management_System-UAT-FE
- Default issue repository: Pen1112003/Sports_Center_Management_System-UAT-BE
- Project: Pen1112003 / Sports Center Management System
- Dry run: true
- Next step: Review and approve field mapping before actual sync
- Review decision: Ready for Review

## 8. Traceability
- Business Goal: Tăng trải nghiệm và giảm thủ công cho thành viên
- Blueprint: feature-01-blueprint.md
- Status: Ready for Review
