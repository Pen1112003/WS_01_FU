# BUG-003: Nham Blueprint khi xac dinh FR-002

- **Status:** Recorded
- **Area:** Requirements traceability / GitHub Project mapping
- **Detected:** 2026-09-18
- **Severity:** High

## Symptom

Agent da trien khai `FR-002` theo tai lieu class registration, trong khi GitHub Project #19 va Issue #4 dinh nghia:

> `[FR-002] Quản lý hồ sơ thành viên (Tạo mới, cập nhật, khóa/mở)`

Class registration la mot feature khac trong SRS/blueprint va khong duoc dung de dai dien cho Issue #4.

## Root cause

- Dung cung mot ma `FR-002` tu tai lieu feature local khac ma khong doi chieu Issue/Project item chinh thuc.
- Khong map `Blueprint ID -> Project item -> Issue URL` truoc khi bat dau implement.
- Suy dien title/feature tu context gan nhat thay vi xac minh `Project item.content.number`, `content.url` va body issue.
- Khong dung source-of-truth theo quy tac repository: GitHub Issue/Project contract co uu tien khi co mapping.

## Impact

- Class registration da duoc implement va merge o PR BE #22, FE #2.
- Issue #4 ve member management van chua duoc implement.
- Khong duoc danh dau Issue #4 la Done dua tren code class registration.

## Prevention checklist

Truoc khi implement bat ky FR nao:

- [ ] Tim ma FR trong `srs.txt`, blueprint local va GitHub Project.
- [ ] Lay `Project item.content.number`, `content.url`, title va body Issue.
- [ ] Lap mapping `Blueprint ID -> Project item ID -> Issue URL -> target repo`.
- [ ] Neu cung ma FR xuat hien o nhieu tai lieu, dung Issue/Project da duoc chi dinh lam source of truth.
- [ ] Xac nhan title va acceptance criteria khop truoc khi sua code.
- [ ] Khong cap nhat status cua issue neu implementation khong khop scope issue.
- [ ] Ghi ro `Assumption`, `Decision` hoac `Open Question` neu co xung dot requirement.

## Correct handling for FR-002 Issue #4

Issue #4 yeu cau member management:

- CRUD member profile cho Receptionist/Manager.
- Sinh Member ID dang `MEM-XXXX`.
- Tim kiem theo phone, ten, member ID.
- Cap nhat phone, email, ngay sinh, dia chi, lien he khan cap.
- Khoa/mo account.
- Unique phone/email, RBAC, audit log, migration, OpenAPI va test.

## AI instruction

Khi user chi nhac `[FR-002]`, khong duoc tu dong dung feature gan nhat. Phai doc title/body cua Project item va Issue number truoc khi chon scope. Neu title khong khop voi tai lieu local, dung lai de xac minh mapping, khong implement tiep theo phan doan.
