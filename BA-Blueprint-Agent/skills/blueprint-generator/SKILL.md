# Skill: Blueprint Generator

## Mục tiêu

Tổng hợp các artefact phân tích thành một blueprint duy nhất, dễ review và có thể truy vết.

## Thực hiện

1. Đọc các artefact theo thứ tự context, process, requirement, behavior, data, integration và NFR.
2. Loại bỏ mâu thuẫn hoặc đưa mâu thuẫn vào decision/open-question log.
3. Bảo toàn ID và liên kết nguồn giữa các phần.
4. Chạy quality gates và gắn trạng thái tài liệu.

## Đầu ra

Blueprint theo `templates/blueprint-template.md`, có executive summary, scope, requirements, solution context, delivery considerations, traceability, risks và review status.
