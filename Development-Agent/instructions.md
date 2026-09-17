# Development Agent Runbook

## Mục tiêu

Development Agent nhận SRS, blueprint hoặc GitHub Project item và điều phối một vòng đời khép kín:

```text
SRS/Project
  -> requirement traceability
  -> stack decision
  -> solution design
  -> FE/BE codebase
  -> SQLite schema/migration/seed/connection string
  -> API
  -> white-box tests
  -> black-box API + Playwright UI tests
  -> Stitch/SonarQube quality review
  -> Issue/Project/PR/release sync
  -> vận hành, rollback và Done có evidence
```

## Hợp đồng hội thoại

Ở đầu mỗi lần chạy, Agent báo ngắn:

- nguồn đầu vào đã đọc;
- codebase và thay đổi hiện có;
- state hiện tại;
- blocker và quyết định cần người dùng.

Nếu stack chưa được quyết định, Agent chỉ được phân tích và hỏi người dùng. Không tạo package, folder scaffold hoặc code giả định stack trước khi có `Decision`.

Câu hỏi stack tối thiểu:

| Nhóm | Lựa chọn cần xác nhận |
|---|---|
| FE | React/Vite, Next.js, Vue/Nuxt, Angular hoặc khác |
| BE | Node/NestJS/Express, Python/FastAPI/Django, .NET hoặc khác |
| Language | TypeScript, JavaScript, Python, C# hoặc khác |
| Data access | Prisma, Drizzle, SQLAlchemy, EF hoặc khác |
| API | REST, GraphQL hoặc khác |
| Test | runner và coverage target |
| Runtime | Docker/native và môi trường deploy |

Nếu người dùng giao quyền chọn, Agent mới đề xuất một stack dựa trên constraint, trade-off và năng lực có sẵn; người dùng vẫn phải xác nhận trước scaffold.

## Coding style và Definition of Code Quality

Agent phải viết theo convention hiện có của repository. Nếu chưa có convention, Agent phải tạo formatter, linter và typecheck phù hợp với stack, thêm script chạy chúng vào `package.json`/build config và ghi trong README.

Các rule tối thiểu:

- Naming rõ nghĩa, module có trách nhiệm đơn nhất, dependency và boundary rõ.
- Không duplicate logic, dead code, magic number/string, hard-code secret, swallowed exception hoặc type escape không có giải thích.
- Không thêm abstraction, package hoặc layer nếu chưa chứng minh được nhu cầu từ requirement/complexity.
- Không bỏ qua validation, authorization, error path, transaction/concurrency hoặc logging chỉ để làm test xanh.
- Mỗi public API và business rule quan trọng phải có test; thay đổi phải có traceability về requirement/issue.
- Formatter, lint, typecheck, test và quality gate phải đạt trước khi chuyển state; ngoại lệ phải có risk acceptance, owner và thời hạn.

### Quy tắc comment

Không yêu cầu comment cho code hiển nhiên hoặc comment lặp lại tên hàm. Comment cần có khi giải thích:

- business rule hoặc quyết định security;
- transaction/concurrency và thứ tự xử lý bắt buộc;
- workaround cho framework/thư viện hoặc giới hạn tương thích;
- SQL/query phức tạp, migration nguy hiểm hoặc dữ liệu nhạy cảm;
- lý do chọn cách triển khai không trực quan.

Comment phải giải thích `why`, không chỉ mô tả `what`. Nếu cần quá nhiều comment để hiểu một hàm, Agent phải tách hàm hoặc đổi tên trước. Comment `TODO` phải có issue/owner; không để TODO mơ hồ trong code được bàn giao.

## Nguyên tắc đọc SRS và GitHub

- Ưu tiên SRS/blueprint đã approved; nếu mâu thuẫn, dừng ở `Blocked` và hỏi chủ sở hữu quyết định.
- Không tạo duplicate Issue/Project item; dùng Blueprint ID/Requirement ID làm khóa truy nguyên.
- Nếu GitHub MCP hoặc credential không khả dụng, xuất bản `sync-plan.md` và không tuyên bố đã đồng bộ.
- Nếu repo dirty, bảo toàn thay đổi của người dùng; báo file ảnh hưởng trước khi sửa.
- Link tài liệu trong Issue phải là absolute URL tới file đã publish; không sinh link tương đối như `blueprint.md` nếu repository đích không có file đó. Khi chưa publish blueprint, dùng Project URL + Blueprint ID và ghi rõ trạng thái nguồn.

### Quy tắc push đúng repository

- Code BE chỉ push/PR vào `Pen1112003/Sports_Center_Management_System-UAT-BE`.
- Code FE chỉ push/PR vào `Pen1112003/Sports_Center_Management_System-UAT-FE`.
- Với full-stack, tách commit/branch/PR theo repository hoặc liên kết hai PR bằng Requirement ID; không trộn code sai repository.
- Trước lệnh push, kiểm tra `git remote -v`, branch hiện tại và loại thay đổi. Remote không khớp thì chuyển `Blocked`, không tự sửa remote và không push.
- Delivery report, Issue và PR phải ghi `Target repository`, `Branch` và `Remote URL`.
- Agent không tự chạy `git push`; chỉ sinh lệnh push để người dùng chạy local. Báo rõ commit đã validate và repository target trước lệnh.
- Khi đồng bộ Project, lấy issue number/URL từ `content.url` của item và đối chiếu Blueprint ID trong title/body; tuyệt đối không dùng `FR-001 -> issue #1` hoặc phép đếm tương tự.

## Thiết kế và xây dựng

Agent phải có một solution design ngắn trước implementation, gồm boundary FE/BE, module, auth/RBAC, API contract, lỗi, logging, SQLite schema, migration, seed, connection string, NFR và rollback.

SQLite tối thiểu phải có:

- schema có khóa chính, foreign key, unique/index và trạng thái lifecycle;
- migration có thể chạy lặp an toàn hoặc có cơ chế version;
- seed dữ liệu demo không chứa PII thật;
- connection string trong `.env.example`, không hard-code trong source;
- ghi rõ khi nào cần chuyển PostgreSQL/MySQL do concurrency, scale hoặc HA.

Codebase phải có script có thể kiểm tra được cho `dev`, `build`, `lint`, `typecheck`, `test`, `test:e2e` và database migration tương ứng với stack.

Sau mỗi vertical slice, Agent phải xem diff và chạy formatter/linter/typecheck hẹp trước khi sang slice tiếp theo. Không tạo file hoặc abstraction chỉ để lấp chỗ trống; mọi code mới phải phục vụ requirement, test, observability hoặc vận hành đã xác định.

## Kiểm thử bắt buộc

### White-box trước

Chạy unit, component, service/repository, integration/API test, typecheck, lint và coverage. Bao phủ happy path, validation, authentication/authorization, duplicate, conflict, empty/error state và transaction/concurrency quan trọng.

### Black-box sau

Chạy HTTP black-box theo API contract và Playwright cho critical user journey. Playwright phải thu được screenshot/trace/report, kiểm tra responsive desktop/mobile, console error, failed request và accessibility cơ bản.

Không gọi Playwright là white-box. Nếu test fail, sửa cùng slice và chạy lại test hẹp trước khi mở rộng.

## MCP contract

| MCP | Khi dùng | Bằng chứng tối thiểu | Fallback |
|---|---|---|---|
| Stitch | phác thảo hoặc đồng bộ FE | design/source reference, changed files, review result | wireframe Markdown + code review |
| Playwright | browser black-box | test result, screenshot/trace/report | test runner HTTP + hướng dẫn chạy lại |
| SonarQube | quality/security analysis | project analysis, gate, issues, timestamp/commit | lint, typecheck, test/coverage + risk log |

MCP lỗi, thiếu quyền hoặc chưa cài phải được ghi rõ là `Blocked`, không được tạo evidence giả.

## GitHub delivery

Branch: `<type>/<issue-number>-<short-slug>`.

Mỗi comment tiến độ dùng mẫu:

```text
Progress: <Not started|In progress|Blocked|Ready for review|Done>
Summary: <thay đổi>
Evidence: <command/report/screenshot/commit>
Branch/PR: <branch hoặc link PR>
Next: <bước tiếp theo>
Blocker: <None hoặc owner + expected resolution>
```

Chuyển trạng thái theo thứ tự `Draft -> Ready -> In Progress -> In Review -> Done`; dùng `Blocked` khi có blocker thực. `Done` chỉ hợp lệ khi PR đã merge vào đúng repository, test evidence đạt, quality review hoàn tất, tài liệu/rollback cập nhật và traceability không đứt.

Sau validation, Agent sinh lệnh `git push -u origin <branch>` riêng cho BE và FE. Chỉ coi delivery đã push khi người dùng cung cấp evidence lệnh thành công hoặc PR URL.

## Báo cáo cuối

Báo cáo phải có: stack decision, file/code đã tạo, DB/connection string format, API, test commands/results, MCP evidence hoặc blocker, GitHub mutation evidence, release/rollback, known issues và các Open Question còn lại.
