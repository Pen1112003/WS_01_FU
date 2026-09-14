# Quality Gates

## Gate 1: Context Ready

- Có business problem, outcome và phạm vi sơ bộ.
- Stakeholder, user và system boundary đã được nhận diện.
- Assumption, constraint và open question được tách riêng.

## Gate 2: Requirement Ready

- Requirement có ID, nguồn, priority và trạng thái xác nhận.
- Không có requirement mơ hồ như “nhanh”, “dễ dùng” nếu chưa có thước đo.
- Mỗi requirement quan trọng có acceptance criteria.

## Gate 3: Solution Ready

- Luồng chính và ngoại lệ đã được mô tả.
- Data, API, security, audit và NFR liên quan đã được xem xét.
- Các phụ thuộc, migration và backward compatibility được ghi nhận khi cần.

## Gate 4: Delivery Ready

- Traceability từ goal đến requirement, story và test criteria tồn tại.
- Rủi ro có impact, likelihood, owner và mitigation.
- Tài liệu ghi rõ `Draft`, `Ready for Review` hoặc `Approved`.

## Gate 5: GitHub Delivery Complete

- Project item và Issue được liên kết bằng Blueprint ID, không tạo trùng.
- Issue có status, priority, type, area, owner, iteration, target date và risk.
- Branch và Pull Request liên kết đúng Issue; comment có summary, evidence, next step và blocker.
- Acceptance criteria có bằng chứng test/review và PR đã merge trước khi chuyển `Done`.
- Blueprint, Issue, PR và test evidence không có liên kết bị đứt.
