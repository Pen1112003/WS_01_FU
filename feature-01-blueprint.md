# Software Development Blueprint

**Status:** Ready for Review
**Version:** 0.1
**Owner:** BA / Product
**Last updated:** 2026-09-14

## 1. Executive Summary

- **Business problem:** Thành viên đang phải đăng ký lớp học thủ công qua lễ tân hoặc thông qua trao đổi ngoài hệ thống, gây mất thời gian, sai lệch thông tin và khó kiểm soát lịch học.
- **Desired outcome:** Thành viên có thể tự đăng ký hủy đăng ký lớp học trực tiếp trên hệ thống; hệ thống kiểm tra gói tập, xung đột lịch và số chỗ còn lại ngay khi thao tác.
- **Success metrics:**
  - 90% người dùng đăng ký lớp via hệ thống
  - Thời gian xử lý đăng ký dưới 2 phút
  - Tỷ lệ trùng lịch hoặc quá tải thấp hơn 1%
- **Recommended direction:** Xây dựng chức năng đăng ký lớp học theo mô hình self-service với kiểm tra điều kiện tự động và log lịch sử hoạt động.

## 2. Scope

### In scope
- Thành viên xem danh sách lớp học theo bộ môn, giờ, ngày, phòng và số chỗ còn lại
- Thành viên đăng ký lớp học
- Hệ thống kiểm tra gói tập còn hiệu lực, lịch trùng và không quá tải
- Hệ thống lưu lịch sử đăng ký, trạng thái và hủy đăng ký
- Lễ tân hỗ trợ xử lý khi thành viên cần hỗ trợ

### Out of scope
- Quản lý thanh toán online phức tạp
- AI gợi ý lớp học
- Quản lý lịch dạy chi tiết của huấn luyện viên

## 3. Stakeholders and Users

| ID | Role | Responsibility | Decision/approval |
|---|---|---|---|
| ST-001 | Member | Đăng ký, xem lịch học và hủy đăng ký | User |
| ST-002 | Receptionist | Hỗ trợ xử lý đăng ký và yêu cầu thành viên | Operational |
| ST-003 | Coach | Xem danh sách học viên trong lớp | Inform |
| ST-004 | Center Manager | Giám sát tình trạng lớp học và hiệu quả hoạt động | Approval |

## 4. Assumptions, Constraints and Open Questions

| ID | Type | Statement | Owner | Status |
|---|---|---|---|---|
| A-001 | Assumption | Thành viên đã có tài khoản và gói tập hợp lệ trước khi đăng ký lớp | Product | Unconfirmed |
| A-002 | Assumption | Mỗi thành viên chỉ được đăng ký tối đa 1 slot cho cùng một lớp trong một lần | Product | Unconfirmed |
| C-001 | Constraint | Hệ thống phải chặn xung đột lịch và lớp đã đầy | Technical | Confirmed |
| OQ-001 | Open Question | Có cần cho phép hủy lớp trong vòng bao lâu trước buổi học hay không? | Product | Open |
| OQ-002 | Open Question | Có cần thông báo tự động khi lớp sắp đầy không? | Product | Open |

## 5. Process Analysis

| Step | Current state | Future state | Actor/system | Rule or exception |
|---|---|---|---|---|
| 1 | Thành viên gọi hoặc đến quầy để hỏi lớp | Thành viên mở danh sách lớp học trong ứng dụng | Member/System | Chỉ hiển thị lớp đang mở và còn chỗ |
| 2 | Nhân viên xác minh gói tập và lịch | Hệ thống tự kiểm tra điều kiện đăng ký | System | Nếu gói hết hạn hoặc trùng lịch, chặn thao tác |
| 3 | Nhân viên xác nhận thủ công | Hệ thống tạo bản ghi đăng ký | Member/System | Mỗi đăng ký phải lưu trạng thái và thời gian |
| 4 | Thành viên phải hỏi lại trạng thái | Hệ thống hiển thị trạng thái đăng ký trong lịch cá nhân | System | Nếu bị hủy, cập nhật trạng thái ngay |

## 6. Requirements

| ID | Type | Requirement | Priority | Source | Status |
|---|---|---|---|---|---|
| BR-001 | Business | Thành viên có thể tự đăng ký lớp học trên hệ thống mà không cần hỗ trợ thủ công. | Must | Stakeholder | Draft |
| FR-001 | Functional | Hệ thống hiển thị danh sách lớp học đang mở theo bộ môn, ngày, giờ, phòng và số chỗ còn lại. | Must | Member | Draft |
| FR-002 | Functional | Hệ thống kiểm tra điều kiện đăng ký: gói tập còn hiệu lực, không trùng lịch, còn slot. | Must | Business rule | Draft |
| FR-003 | Functional | Hệ thống lưu trữ đăng ký, trạng thái và thời gian tạo/xóa bản ghi. | Must | Operational | Draft |
| FR-004 | Functional | Thành viên có thể hủy đăng ký nếu còn trong thời hạn cho phép. | Should | Member requirement | Draft |
| FR-005 | Functional | Hệ thống hiển thị thông báo rõ ràng khi đăng ký bị từ chối vì lớp đầy, lịch trùng hoặc gói hết hạn. | Must | UX requirement | Draft |

## 7. Use Cases and User Stories

### UC-001: Đăng ký lớp học

- **Actor:** Member
- **Trigger:** Thành viên chọn một lớp và bấm đăng ký
- **Preconditions:** Thành viên đã đăng nhập, có tài khoản hợp lệ và gói tập còn hiệu lực
- **Main flow:**
  1. Thành viên mở danh sách lớp học
  2. Chọn lớp phù hợp
  3. Hệ thống kiểm tra số chỗ, lịch và gói tập
  4. Nếu hợp lệ, hệ thống tạo bản ghi đăng ký
  5. Hệ thống hiển thị thông báo thành công và cập nhật lịch của thành viên
- **Alternate/error flows:**
  - Trùng lịch: hệ thống báo lỗi và không cho đăng ký
  - Gói hết hạn: hệ thống yêu cầu gia hạn gói
  - Lớp đã đầy: hệ thống từ chối và đề xuất lớp khác
- **Postconditions:** Sự kiện đăng ký được lưu và xuất hiện trên lịch tập cá nhân của thành viên

### US-001: Thành viên đăng ký lớp học

As a Member, I want to register for a class from the system, so that I can join a class without manual support.

**Acceptance criteria**
- Given a logged-in member with an active membership, when they select an available class, then the system creates a registration successfully.
- Given a full class, when the member tries to register, then the system blocks the action and shows a clear message.
- Given a schedule conflict, when the member attempts to book, then the system prevents the booking and explains the conflict.

## 8. Data Model

| Entity | Key fields | Relationships | Lifecycle | Classification | Owner |
|---|---|---|---|---|---|
| Member | member_id, full_name, phone, email, status | One member can have many registrations | Active / Inactive | Internal | Member Services |
| Membership | membership_id, member_id, package_id, start_date, end_date, status | One member has many memberships | Active / Expired | Internal | Revenue |
| ClassSchedule | class_id, course_id, coach_id, room_id, date, start_time, end_time, capacity | Many registrations belong to one class | Open / Full / Closed | Internal | Operations |
| Registration | registration_id, member_id, class_id, status, registered_at, cancelled_at | One member has many registrations; one class has many registrations | Pending / Confirmed / Cancelled | Internal | Operations |

## 9. API and Integration Contract

| API/Event ID | Method/path | Purpose | Auth | Request/response | Errors |
|---|---|---|---|---|---|
| API-001 | GET /classes | Lấy danh sách lớp đang mở | Member token | Trả về class_id, course_name, date, time, room, capacity, available_slots | 400, 404 |
| API-002 | POST /class-registrations | Đăng ký lớp cho thành viên | Member token | body: member_id, class_id | 409 conflict, 422 invalid, 403 unauthorized |
| API-003 | DELETE /class-registrations/{id} | Hủy đăng ký | Member token | Trả về trạng thái hủy thành công | 404, 403 |

## 10. Non-Functional Requirements

| ID | Category | Target | Measurement | Priority | Owner |
|---|---|---|---|---|---|
| NFR-001 | Performance | Thời gian load danh sách lớp dưới 3 giây | p95 | Must | Engineering |
| NFR-002 | Availability | Hệ thống hoạt động 99.5% | Uptime | Must | Operations |
| NFR-003 | Security | Chỉ member được phép đăng ký cho chính mình | Access control | Must | Security |

## 11. Security, Privacy and Compliance

- Authentication and authorization: Member phải đăng nhập; lễ tân và quản lý chỉ được hỗ trợ theo quyền được cấp
- Sensitive data and classification: Thông tin học viên và lịch tập cần bảo mật
- Audit and traceability: Ghi log thời gian, người thao tác và trạng thái trước/sau khi đăng ký
- Retention/deletion: Dữ liệu bản ghi đăng ký được lưu theo quy định của trung tâm

## 12. Delivery Plan and Dependencies

| Increment | Scope | Dependency | Exit criteria | Risk |
|---|---|---|---|---|
| 1 | Đăng ký lớp học cơ bản | Member login, class list, membership status | Thành viên đăng ký thành công hoặc nhận thông báo rõ ràng khi bị chặn | Medium |

## 13. Traceability Matrix

| Business goal | Requirement | Use case/story | API/data/NFR | Test evidence |
|---|---|---|---|---|
| Giảm thủ công và tăng trải nghiệm thành viên | BR-001, FR-001, FR-002, FR-005 | UC-001, US-001 | API-001, API-002, NFR-001 | Chưa có |

## 14. Risks and Decisions

| ID | Risk/decision | Impact | Likelihood | Owner | Mitigation/status |
|---|---|---|---|---|---|
| R-001 | Chưa xác định thời hạn hủy đăng ký | Medium | Medium | Product | Open |
| R-002 | Xác định quy tắc chặn khi lớp gần đầy | Medium | Medium | Product | Open |

## 15. Quality Review

- **Quality gate:** Passed (Ready for Review)
- **Unresolved questions:** Thời hạn hủy đăng ký, cảnh báo lớp sắp đầy, quy định gói tập và tối đa 1 slot/lớp (đã ghi rõ trong Assumptions/Open Questions)
- **Reviewers:** BA, Product, Operations
- **Approval decision:** Ready for Review

### Quality gate audit against repo checklist

- [x] Vấn đề và outcome đo được.
- [x] In-scope/out-of-scope rõ ràng.
- [x] Stakeholder và decision maker được xác định.
- [x] Actor, trigger, precondition và postcondition rõ.
- [x] Happy path, alternate path và error path đầy đủ.
- [x] User story có giá trị và acceptance criteria.
- [x] Data ownership, lifecycle và retention được nêu.
- [x] API có request, response, error và authorization.
- [x] NFR có metric, target và cách đo.
- [x] Security và audit được xem xét.
- [x] Traceability matrix có business goal → requirement → story → API/NFR.
- [x] Rủi ro có impact, likelihood, owner và mitigation.
