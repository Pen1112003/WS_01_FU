# BA Blueprint Agent

BA Blueprint Agent hỗ trợ Business Analyst chuyển hóa nhu cầu nghiệp vụ thành Software Development Blueprint có thể bàn giao cho Product, Engineering, QA, Security và Operations.

## Bối cảnh chính

Nếu mục tiêu là để BA sử dụng Agent tạo Software Development Blueprint, Agent không nên trả lời chung chung. Agent phải dùng quy trình chuẩn hóa cho toàn bộ vòng đời phân tích yêu cầu:

1. Khám phá bối cảnh, mục tiêu, stakeholder và các giả định.
2. Phân tích quy trình hiện tại và quy trình đích.
3. Làm rõ requirement, use case, user story và acceptance criteria.
4. Mô tả functional analysis, data model, API contract và non-functional requirements.
5. Tổng hợp blueprint có traceability, rủi ro, open questions và quality gates.

Khi thông tin đầu vào chưa đủ, Agent phải hỏi các câu hỏi có mức độ ưu tiên cao thay vì tự bịa dữ kiện. Mọi giả định do Agent đưa ra phải được đánh dấu rõ là `Assumption`.

## Hiển thị tài liệu

Các tài liệu HTML/Markdown được kỳ vọng hiển thị theo quy tắc tối giản sau:

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

## Cấu trúc

- `agent.yaml`: metadata, vai trò, workflow và output contract.
- `instructions.md`: nguyên tắc điều phối hội thoại và tiêu chuẩn đầu ra.
- `skills/<name>/SKILL.md`: các năng lực phân tích chuyên biệt.
- `governance/quality-gates.md` và `governance/review-checklist.md`: quality gates và checklist review blueprint.
- `governance/github-project-operating-model.md`: field, view, Definition of Ready/Done và nhịp vận hành team.
- `templates/blueprint-template.md`: template đầu ra có cấu trúc ổn định.
- Thư mục `knowledge/` sẵn sàng để mở rộng thành các gói kiến thức riêng khi cần.

## Kết nối GitHub Project

Thiết lập URL/project trong `.env` dựa trên `.env.example`. Mặc định `GITHUB_PROJECT_DRY_RUN=true` để xem trước thay đổi trước khi ghi lên GitHub. Không commit token hoặc `.env` thật.

## GitHub Project là điểm đầu cuối

Sau khi chức năng qua quality gates, Agent phải chuyển chức năng thành Project item/Issue có `Blueprint ID`, `Status`, `Priority`, `Type`, `Area`, `Owner`, `Iteration`, `Target date`, `Risk`, acceptance criteria và dependency. Tiến độ được nối bằng Issue comment, branch và Pull Request; chỉ chuyển `Done` khi có bằng chứng review, test và PR merge.

## Đầu ra chuẩn

Đầu ra cuối cùng phải là Markdown có các phần: executive summary, scope, stakeholders, assumptions, current/future process, requirements, use cases, user stories, data model, API, NFR, security, delivery plan, traceability, risks, open questions và quality review.