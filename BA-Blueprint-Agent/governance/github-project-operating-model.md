# GitHub Project Operating Model

GitHub Project là điểm điều phối delivery sau khi BA xác định chức năng. Blueprint là nguồn mô tả và traceability; Issue là đơn vị công việc; branch/PR là bằng chứng thay đổi; Project view là bảng tiến độ của team.

## Field chuẩn

| Field | Giá trị | Mục đích |
|---|---|---|
| Status | Backlog, Ready, In Progress, In Review, Blocked, Done, Cancelled | Theo dõi vòng đời |
| Priority | P0 Critical, P1 High, P2 Medium, P3 Low | Xếp thứ tự |
| Type | Feature, Story, Bug, Task, Spike | Phân loại |
| Area | Capability/domain | Lọc theo nhóm |
| Owner | GitHub assignee | Đầu mối chịu trách nhiệm |
| Iteration | Sprint/release | Lập kế hoạch |
| Target date | YYYY-MM-DD | Theo dõi cam kết |
| Blueprint ID | BR/FR/UC/US/NFR | Truy nguyên |
| Risk | None, Low, Medium, High, Critical | Điều phối rủi ro |

## View cần có

- **Team Board:** Status theo cột, lọc item chưa hoàn thành.
- **Priority Queue:** P0/P1, owner và target date.
- **Sprint View:** Iteration theo nhóm status.
- **Blocked Work:** chỉ item `Blocked`, có blocker owner và next action.
- **Delivery Traceability:** Blueprint ID, Issue, PR, test evidence và release.

## Definition of Ready

Issue có Blueprint ID, context, scope, acceptance criteria, priority, owner/assignee, dependency và target iteration.

## Definition of Done

Acceptance criteria đạt; review/PR hoàn tất; test evidence được ghi; tài liệu cập nhật; PR liên kết Issue; Project item chuyển `Done`; comment cuối có link bằng chứng.

## Nhịp vận hành

- Hàng ngày: cập nhật status, next step, blocker và branch/PR.
- Hàng tuần: rà soát item quá hạn, blocked, không owner và P0/P1 chưa có kế hoạch.
- Cuối sprint: kiểm tra Definition of Done và traceability từ blueprint đến delivery.
