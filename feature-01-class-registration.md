# Feature Demo 01: Đăng ký lớp học cho thành viên

**Status:** Draft
**Blueprint ID:** BPD-001
**Owner:** Product / BA
**Last updated:** 2026-09-14

## 1. Executive Summary

- **Business problem:** Thành viên gặp khó khăn khi phải đăng ký lớp học thủ công qua nhân viên hoặc tin nhắn, dẫn đến sai sót, xung đột lịch và thiếu minh bạch về khả năng còn chỗ.
- **Desired outcome:** Thành viên có thể tự đăng ký hoặc hủy đăng ký lớp học trực tiếp trên hệ thống, đồng thời hệ thống kiểm tra lịch, số chỗ và giá gói phù hợp.
- **Success metrics:**
  - 90% đăng ký lớp được thực hiện trực tiếp trên hệ thống
  - Tỷ lệ lỗi xung đột lịch < 1%
  - Thời gian xử lý đăng ký dưới 2 phút

## 2. Scope

### In scope
- Thành viên xem danh sách lớp học và lịch học
- Thành viên đăng ký lớp học
- Hệ thống kiểm tra độ đầy, lịch trùng và điều kiện gói tập
- Hệ thống hiển thị xác nhận đăng ký và trạng thái
- Nhân viên lễ tân hỗ trợ đăng ký/hủy trong trường hợp cần hỗ trợ

### Out of scope
- Quản lý huấn luyện viên và lịch dạy chi tiết không nằm trong chức năng này
- Tích hợp thanh toán online nâng cao
- AI recommendation cho lớp học

## 3. Stakeholders and Users

| ID | Role | Responsibility | Decision/approval |
|---|---|---|---|
| ST-001 | Member | Đăng ký và quản lý lớp học cá nhân | User |
| ST-002 | Receptionist | Hỗ trợ đăng ký và xử lý khi có sự cố | Operational |
| ST-003 | Center Manager | Giám sát tình trạng lớp và báo cáo | Approval |
| ST-004 | Coach | Xem danh sách học viên trong lớp | Inform |

## 4. Assumptions, Constraints and Open Questions

| ID | Type | Statement | Owner | Status |
|---|---|---|---|---|
| A-001 | Assumption | Thành viên đã có tài khoản và gói tập hợp lệ trước khi đăng ký lớp | Product | Unconfirmed |
| C-001 | Constraint | Hệ thống phải ngăn không cho đăng ký trùng thời gian hoặc vượt số chỗ tối đa | Technical | Confirmed |
| OQ-001 | Open Question | Có cần cảnh báo ngay khi lớp sắp đầy hay chỉ hiện thị khi quá đầy? | Product | Open |

## 5. Process Analysis

| Step | Current state | Future state | Actor/system | Rule or exception |
|---|---|---|---|---|
| 1 | Thành viên gọi hoặc đến quầy để hỏi lớp | Thành viên mở danh sách lớp học trên hệ thống | Member/System | Chỉ hiển thị lớp đang mở và còn chỗ |
| 2 | Nhân viên kiểm tra lịch và gói tập | Hệ thống tự kiểm tra lịch hội đủ điều kiện | System | Nếu trùng lịch hoặc gói hết hạn thì từ chối |
| 3 | Xác nhận thủ công | Hệ thống tạo đơn đăng ký và xác nhận | Member/System | Mỗi thành viên chỉ được đăng ký 1 slot cho lớp nếu đang hoạt động |
| 4 | Nhân viên ghi nhận sự kiện | Hệ thống lưu lịch sử đăng ký và điểm danh | System | Ghi log thay đổi trạng thái |

## 6. Requirements

| ID | Type | Requirement | Priority | Source | Status |
|---|---|---|---|---|---|
| BR-001 | Business | Thành viên phải có thể đăng ký lớp học trực tiếp trên hệ thống mà không cần yêu cầu nhân viên thủ công. | Must | Stakeholder | Draft |
| FR-001 | Functional | Hệ thống phải hiển thị danh sách lớp học đang mở theo bộ môn, ngày, giờ, phòng và số chỗ còn lại. | Must | Member | Draft |
| FR-002 | Functional | Hệ thống phải kiểm tra điều kiện đăng ký: gói tập còn hiệu lực, thời gian không trùng với lịch đã đăng ký, và số chỗ còn lại > 0. | Must | Business rule | Draft |
| FR-003 | Functional | Hệ thống phải lưu thông tin đăng ký, trạng thái đăng ký và lịch sử thay đổi. | Must | Operational | Draft |
| FR-004 | Functional | Thành viên phải có thể hủy đăng ký lớp học trong thời hạn cho phép. | Should | Member need | Draft |

## 7. Use Cases and User Stories

### UC-001: Đăng ký lớp học

- **Actor:** Member
- **Trigger:** Thành viên chọn một lớp học và nhấn Đăng ký
- **Preconditions:** Thành viên đã đăng nhập, có tài khoản hợp lệ và gói tập còn hiệu lực
- **Main flow:**
  1. Thành viên mở danh sách lớp học
  2. Chọn lớp phù hợp
  3. Hệ thống kiểm tra lịch, gói tập và số chỗ còn lại
  4. Nếu hợp lệ, hệ thống tạo bản ghi đăng ký và hiển thị xác nhận
- **Alternate/error flows:**
  - Trùng lịch: hệ thống hiển thị cảnh báo và không cho đăng ký
  - Gói hết hạn: hệ thống yêu cầu gia hạn gói
  - Lớp đã đầy: hệ thống từ chối đăng ký
- **Postconditions:** Bản ghi đăng ký được lưu và hiển thị trên lịch tập cá nhân của thành viên

### US-001: Thành viên đăng ký lớp học

As a Member, I want to register for an available class, so that I can attend the session without manual support.

**Acceptance criteria**
- Given a logged-in member with an active membership, when they select a class with available slots, then the system creates a registration successfully.
- Given a class that is full, when the member attempts to register, then the system blocks the action and shows a clear message.
- Given a schedule conflict, when the member tries to book, then the system prevents booking and explains the conflict.

## 8. Data Model

| Entity | Key fields | Relationships | Lifecycle | Classification | Owner |
|---|---|---|---|---|---|
| Member | member_id, full_name, phone, email, status | One member can have many registrations | Active / Inactive | Internal | Member Services |
| ClassSchedule | class_id, course_id, coach_id, room_id, date, start_time, end_time, capacity | Many registrations belong to one class | Open / Full / Closed | Internal | Operations |
| Membership | membership_id, member_id, package_id, start_date, end_date, status | One member has many memberships | Active / Expired | Internal | Revenue |
| Registration | registration_id, member_id, class_id, status, registered_at, cancelled_at | One member has many registrations; one class has many registrations | Pending / Confirmed / Cancelled | Internal | Operations |

## 9. API and Integration Contract

| API/Event ID | Method/path | Purpose | Auth | Request/response | Errors |
|---|---|---|---|---|---|
| API-001 | GET /classes | Lấy danh sách lớp đang mở | Member token | Trả về class_id, course_name, date, time, room, capacity, available_slots | 400/404 |
| API-002 | POST /class-registrations | Đăng ký lớp cho thành viên | Member token | body: member_id, class_id | 409 conflict, 422 invalid, 403 unauthorized |
| API-003 | DELETE /class-registrations/{id} | Hủy đăng ký | Member token | Trả về trạng thái hủy thành công | 404, 403 |

## 10. Non-Functional Requirements

| ID | Category | Target | Measurement | Priority | Owner |
|---|---|---|---|---|---|
| NFR-001 | Performance | Thời gian load danh sách lớp dưới 3 giây | p95 | Must | Engineering |
| NFR-002 | Availability | Hệ thống hoạt động 99.5% | Uptime | Must | Operations |
| NFR-003 | Security | Chỉ member được phép đăng ký tài khoản của mình | Access control | Must | Security |

## 11. Security, Privacy and Compliance

- Authentication and authorization: Member phải đăng nhập để thao tác, Receptionist/Manager có quyền hỗ trợ khi được ủy quyền
- Sensitive data and classification: Thông tin từng thành viên và lịch học cần được bảo vệ
- Audit and traceability: Không gian log cho mỗi thao tác đăng ký/hủy
- Retention/deletion: Dữ liệu đăng ký lưu giữ theo chính sách lưu trữ của trung tâm

## 12. Delivery Plan and Dependencies

| Increment | Scope | Dependency | Exit criteria | Risk |
|---|---|---|---|---|
| 1 | Đăng ký lớp học cơ bản | Member login, class list, membership check | Đăng ký thành công và từ chối trường hợp lỗi | Medium |

## 13. Traceability Matrix

| Business goal | Requirement | Use case/story | API/data/NFR | Test evidence |
|---|---|---|---|---|
| Tăng khả năng đăng ký lớp trực tiếp | BR-001, FR-001, FR-002 | UC-001, US-001 | API-001, API-002, NFR-001 | Chưa có |

## 14. Risks and Decisions

| ID | Risk/decision | Impact | Likelihood | Owner | Mitigation/status |
|---|---|---|---|---|---|
| R-001 | Chờ quy định hủy lớp và thời hạn tối đa | Medium | Medium | Product | Open |

## 15. Quality Review

- **Quality gate:** In progress
- **Unresolved questions:** Cần xác nhận thời hạn hủy đăng ký và quy tắc số chỗ tối đa
- **Reviewers:** BA, Product, Ops
- **Approval decision:** Pending review

## 16. GitHub Project Draft Issue

**Title:** [FR-001] Đăng ký lớp học cho thành viên

**Fields draft:**
- Status: Draft
- Priority: High
- Type: Feature
- Area: Member / Class booking
- Owner: Product or Backend Team
- Iteration: Sprint 1
- Target date: TBD
- Blueprint ID: BPD-001
- Risk: Medium

**Issue summary:**
Cho phép thành viên xem danh sách lớp học và đăng ký trực tiếp trên hệ thống với các kiểm tra gói tập, xung đột lịch và số chỗ còn lại.
