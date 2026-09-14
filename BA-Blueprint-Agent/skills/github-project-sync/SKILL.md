# Skill: GitHub Project Sync

## Mục tiêu

Đồng bộ chức năng đã được xác nhận từ Software Development Blueprint vào GitHub Project để quản lý backlog, tiến độ và bằng chứng delivery.

## Điều kiện trước khi đồng bộ

- Blueprint đã qua quality review tối thiểu.
- Mỗi chức năng có ID, priority, owner, acceptance criteria và dependency.
- Có `GITHUB_PROJECT_URL`, `GITHUB_OWNER`, `GITHUB_REPOSITORY` và `GITHUB_PROJECT_NUMBER`.
- Không ghi token hoặc dữ liệu bí mật vào Issue, comment, branch hoặc Markdown.

## Field chuẩn

- `Status`: Backlog, Ready, In Progress, In Review, Blocked, Done, Cancelled.
- `Priority`: P0 Critical, P1 High, P2 Medium, P3 Low.
- `Type`: Feature, Story, Bug, Task, Spike.
- `Area`: capability/domain phụ trách.
- `Owner`: GitHub assignee.
- `Iteration`: sprint/release.
- `Target date`: ngày dự kiến hoàn thành.
- `Blueprint ID`: BR/FR/UC/US/NFR ID.
- `Risk`: None, Low, Medium, High, Critical.

## Quy tắc Issue và branch

- Issue title: `[FR-###] Tên chức năng ngắn gọn`.
- Issue body phải có context, scope, acceptance criteria, dependency, risk và link blueprint.
- Branch: `<type>/<issue-number>-<short-slug>`.
- Pull Request phải dùng `Closes #<number>` hoặc `Refs #<number>`.
- Mọi trạng thái phải có comment gồm `Progress`, `Summary`, `Evidence`, `Branch/PR`, `Next`, `Blocker`.
- Không đóng Issue nếu acceptance criteria chưa có bằng chứng test/review.

Mẫu comment bắt buộc:

```text
Progress: [Not started|In progress|Blocked|Ready for review|Done]
Summary: <đã hoàn thành hoặc đang xử lý>
Evidence: <commit, PR, test hoặc tài liệu>
Branch/PR: <branch và PR>
Next: <bước tiếp theo>
Blocker: <None hoặc blocker + owner + expected resolution>
```

## Quy trình đồng bộ

1. Khi `GITHUB_PROJECT_DRY_RUN=true`, chỉ báo cáo item/field sẽ tạo hoặc cập nhật.
2. Tạo hoặc cập nhật Project item/Issue theo Blueprint ID, tránh trùng.
3. Gán field, owner, label, iteration, dependency và target date.
4. Khi bắt đầu branch, chuyển `In Progress`; khi có PR, chuyển `In Review`.
5. Khi blocked, chuyển `Blocked`, ghi blocker owner và next action.
6. Chỉ chuyển `Done` sau khi PR merge và có test evidence.
7. Báo cáo item thiếu owner, quá hạn, blocked hoặc thiếu acceptance criteria.

## Bảo mật

Chỉ đọc token từ `.env` cục bộ; không in token ra log, không commit `.env`, và dùng quyền GitHub tối thiểu cần thiết.
