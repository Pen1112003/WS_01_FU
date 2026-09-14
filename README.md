# BA Blueprint Agent

BA Blueprint Agent hỗ trợ Business Analyst chuyển hóa nhu cầu nghiệp vụ thành Software Development Blueprint có thể xác nhận, phát triển, kiểm thử và theo dõi delivery trên GitHub Project.

## 1. Mục tiêu và phạm vi

Agent phục vụ toàn bộ vòng đời phân tích và delivery:

1. Khám phá business problem, outcome, stakeholder, user và constraint.
2. Phân tích current state, pain point, future state và exception.
3. Chuẩn hóa requirement, use case, user story và acceptance criteria.
4. Làm rõ data model, API contract, security và non-functional requirements.
5. Tổng hợp Software Development Blueprint có traceability.
6. Chuyển chức năng đã xác nhận thành GitHub Project item/Issue.
7. Theo dõi branch, Pull Request, comment, blocker, test evidence và trạng thái Done.

Agent không được tự bịa dữ kiện. Phần chưa xác nhận phải được đánh dấu `Assumption`, `Constraint`, `Decision` hoặc `Open Question`.

## 2. Cấu trúc repository

```text
.
├── README.md
├── .env.example
├── .gitignore
└── BA-Blueprint-Agent/
    ├── agent.yaml
    ├── instructions.md
    ├── governance/
    │   ├── github-project-operating-model.md
    │   ├── quality-gates.md
    │   └── review-checklist.md
    ├── skills/
    │   ├── api-generator/SKILL.md
    │   ├── blueprint-generator/SKILL.md
    │   ├── data-model-generator/SKILL.md
    │   ├── functional-analysis/SKILL.md
    │   ├── github-project-sync/SKILL.md
    │   ├── nfr-generator/SKILL.md
    │   ├── process-analysis/SKILL.md
    │   ├── requirement-discovery/SKILL.md
    │   ├── use-case-generator/SKILL.md
    │   └── user-story-generator/SKILL.md
    └── templates/
        └── blueprint-template.md
```

## 3. File cấp repository

| File | Nhiệm vụ |
|---|---|
| `README.md` | Tài liệu bắt đầu: mục tiêu, cấu trúc, trách nhiệm từng file, workflow và cách cấu hình. |
| `.env.example` | Mẫu biến môi trường GitHub Project để thành viên copy thành `.env` khi clone. Không chứa secret thật. |
| `.gitignore` | Ngăn `.env`, token cục bộ, file editor và file hệ điều hành bị commit. |
| `.env` | Cấu hình local không được commit; chứa URL Project, repository, project number, token và chế độ dry-run. File này chỉ tồn tại ở máy người dùng. |

## 4. Thư mục `BA-Blueprint-Agent/`

Đây là gói chính của BA Blueprint Agent. Mọi tài liệu, quy tắc và skill phục vụ agent được tổ chức bên trong thư mục này.

### 4.1. File cấu hình và điều phối

| File | Nhiệm vụ | Đầu ra/ảnh hưởng |
|---|---|---|
| `agent.yaml` | Khai báo tên, version, vai trò, mục tiêu, nguyên tắc, workflow 10 bước, input, output contract và quality gates. | Là manifest trung tâm để biết Agent phải chạy những năng lực nào và kiểm tra tài liệu nào. |
| `instructions.md` | Hướng dẫn hành vi hội thoại và quy trình đầu-cuối từ Discover đến Verify and close. | Buộc Agent không dừng ở blueprint mà phải nối tới Project item, Issue, branch, PR, test evidence và `Done`. |

### 4.2. Thư mục `governance/`

Chứa các luật kiểm soát chất lượng, review và vận hành delivery. Governance không sinh nội dung nghiệp vụ; nó quyết định tài liệu hoặc chức năng đã đủ điều kiện chuyển bước hay chưa.

| File | Nhiệm vụ |
|---|---|
| `governance/quality-gates.md` | Định nghĩa 5 gate: Context Ready, Requirement Ready, Solution Ready, Delivery Ready và GitHub Delivery Complete. |
| `governance/review-checklist.md` | Checklist review theo nhóm Business, Product/Requirements, Technical/Operational, Approval và GitHub Project Delivery. |
| `governance/github-project-operating-model.md` | Chuẩn hóa field của Project, các view theo dõi, Definition of Ready, Definition of Done và nhịp vận hành hàng ngày/hàng tuần/cuối sprint. |

### 4.3. Thư mục `skills/`

Mỗi skill là một năng lực chuyên biệt. Skill nhận context/artefact từ bước trước và tạo artefact có thể dùng ở bước sau. Tất cả ID phải ổn định để giữ traceability.

| Thư mục/file | Nhiệm vụ | Artefact chính |
|---|---|---|
| `skills/requirement-discovery/SKILL.md` | Làm rõ bài toán, outcome, stakeholder, scope, assumption, constraint và câu hỏi mở. | Context summary, stakeholder map, scope statement, assumption log. |
| `skills/process-analysis/SKILL.md` | Phân tích current/future process, actor, handoff, bottleneck, control và exception. | Process analysis, business rule, exception catalogue. |
| `skills/functional-analysis/SKILL.md` | Chuyển nhu cầu thành functional requirement, validation, authorization, state transition và error behavior. | Functional requirement catalogue, rule và acceptance criteria. |
| `skills/use-case-generator/SKILL.md` | Mô tả tương tác end-to-end của actor với hệ thống. | Use case gồm trigger, precondition, main flow, alternate/error flow và postcondition. |
| `skills/user-story-generator/SKILL.md` | Chia capability thành story nhỏ, độc lập, có giá trị và kiểm thử được. | User story, priority, dependency và Given/When/Then criteria. |
| `skills/data-model-generator/SKILL.md` | Xác định entity, field, relationship, lifecycle, owner, classification, retention và audit. | Entity catalogue và data rules. |
| `skills/api-generator/SKILL.md` | Tạo contract tích hợp từ use case và data model. | API/event ID, request, response, auth, error, idempotency và versioning. |
| `skills/nfr-generator/SKILL.md` | Chuyển kỳ vọng chất lượng thành mục tiêu đo được. | NFR về performance, availability, security, privacy, operations, accessibility và compatibility. |
| `skills/blueprint-generator/SKILL.md` | Tổng hợp các artefact, xử lý mâu thuẫn và bảo toàn liên kết nguồn. | Software Development Blueprint hoàn chỉnh. |
| `skills/github-project-sync/SKILL.md` | Chuyển chức năng đã xác nhận thành Project item/Issue và theo dõi delivery. | Field, Issue, comment tiến độ, branch, PR, blocker, evidence và trạng thái `Done`. |

### 4.4. Thư mục `templates/`

| File | Nhiệm vụ |
|---|---|
| `templates/blueprint-template.md` | Khuôn mẫu đầu ra duy nhất cho blueprint, gồm summary, scope, stakeholder, requirement, process, use case, story, data, API, NFR, security, delivery, traceability, risk và quality review. |

## 5. Workflow 10 bước

| Bước | Skill/artefact | Điều kiện chuyển bước |
|---:|---|---|
| 1 | `requirement-discovery` | Có business problem, outcome và câu hỏi ưu tiên. |
| 2 | `process-analysis` | Có current/future process, actor, rule và exception. |
| 3 | `functional-analysis` | Requirement có ID, source, priority và acceptance criteria. |
| 4 | `use-case-generator` | Luồng chính và ngoại lệ được mô tả. |
| 5 | `user-story-generator` | Story có giá trị, dependency và tiêu chí kiểm thử. |
| 6 | `data-model-generator` | Dữ liệu có owner, lifecycle, validation và classification phù hợp. |
| 7 | `api-generator` | Contract có request, response, auth và error behavior. |
| 8 | `nfr-generator` | NFR có target, metric, measurement method và owner. |
| 9 | `blueprint-generator` | Blueprint qua quality gates và có traceability. |
| 10 | `github-project-sync` | Project item/Issue, branch, PR, evidence và trạng thái delivery được quản lý. |

## 6. GitHub Project là điểm đầu cuối

Một chức năng chỉ hoàn tất khi có chuỗi liên kết:

```text
Business goal
  -> Blueprint ID
  -> GitHub Project item
  -> Issue
  -> Branch
  -> Pull Request
  -> Review/test evidence
  -> Done
```

### Field bắt buộc

`Status`, `Priority`, `Type`, `Area`, `Owner`, `Iteration`, `Target date`, `Blueprint ID` và `Risk`.

### Quy ước vận hành

- Issue title: `[FR-###] Tên chức năng ngắn gọn`.
- Branch: `<type>/<issue-number>-<short-slug>`.
- PR dùng `Closes #<number>` hoặc `Refs #<number>`.
- Comment phải có `Progress`, `Summary`, `Evidence`, `Branch/PR`, `Next` và `Blocker`.
- Chỉ chuyển `Done` khi acceptance criteria có bằng chứng, PR đã merge và traceability không bị đứt.

## 7. Cấu hình môi trường

Sau khi clone repository:

```bash
cp .env.example .env
```

Điền các biến sau trong `.env`:

```env
GITHUB_PROJECT_URL=https://github.com/OWNER/REPOSITORY/projects/NUMBER
GITHUB_OWNER=OWNER
GITHUB_REPOSITORY=REPOSITORY
GITHUB_PROJECT_NUMBER=NUMBER
GITHUB_TOKEN=REPLACE_WITH_LOCAL_TOKEN
GITHUB_PROJECT_DRY_RUN=true
GITHUB_DEFAULT_BRANCH=main
```

Giữ `GITHUB_PROJECT_DRY_RUN=true` trong lần đầu để xem trước thay đổi. Không commit `.env` hoặc token. Chỉ commit `.env.example`.

## 8. Trạng thái đầu ra

- `Draft`: còn thiếu dữ liệu hoặc quality gate chưa đạt.
- `Ready for Review`: blueprint đủ để Product/Engineering/QA review.
- `Approved`: stakeholder có thẩm quyền đã chấp thuận.
- `In Progress`: đã có Project item/Issue và team đang phát triển.
- `In Review`: đã có Pull Request chờ review.
- `Blocked`: có blocker được ghi rõ owner và next action.
- `Done`: PR merge, test evidence đạt và traceability hoàn chỉnh.

## 9. Hiển thị tài liệu

Các tài liệu HTML/Markdown được kỳ vọng hiển thị theo quy tắc tối giản:

```css
a {
    text-decoration: none;
    color: #464feb;
}
tr th,
tr td {
    border: 1px solid #e6e6e6;
}
tr th {
    background-color: #f5f5f5;
}
```
