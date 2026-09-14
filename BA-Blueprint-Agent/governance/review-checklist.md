# Blueprint Review Checklist

## Business

- [ ] Vấn đề và outcome đo được.
- [ ] In-scope/out-of-scope rõ ràng.
- [ ] Stakeholder và decision maker được xác định.
- [ ] Quy trình hiện tại và pain point có bằng chứng.

## Product and Requirements

- [ ] Actor, trigger, precondition và postcondition rõ.
- [ ] Happy path, alternate path và error path đầy đủ.
- [ ] User story độc lập, có giá trị và có acceptance criteria.
- [ ] Priority và dependency đã được thống nhất.

## Technical and Operational

- [ ] Data ownership, lifecycle, validation và retention được nêu.
- [ ] API có request, response, error và authorization.
- [ ] NFR có metric, target và cách đo.
- [ ] Security, privacy, audit, monitoring và support được xem xét.

## Approval

- [ ] Mọi assumption quan trọng có owner xác nhận.
- [ ] Open question không bị che lấp trong phần kết luận.
- [ ] Traceability matrix không có mục tiêu hoặc requirement mồ côi.

## GitHub Project Delivery

- [ ] Project item/Issue được liên kết bằng Blueprint ID và không bị tạo trùng.
- [ ] Status, Priority, Type, Area, Owner, Iteration, Target date và Risk đã được gán.
- [ ] Issue có scope, acceptance criteria, dependency và link blueprint.
- [ ] Branch/PR liên kết đúng Issue; comment có Evidence, Next và Blocker.
- [ ] Chỉ chuyển `Done` sau khi PR merge và có test/review evidence.
