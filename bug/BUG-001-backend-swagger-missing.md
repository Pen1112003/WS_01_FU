# BUG-001: Backend khong co Swagger/OpenAPI

- **Status:** Resolved
- **Area:** Backend API documentation
- **Detected:** 2026-09-18
- **Affected repository:** `Sports_Center_Management_System-UAT-BE`
- **Severity:** Medium

## Symptom

Backend co API dang chay nhung khong co Swagger UI, OpenAPI JSON hoac URL de FE/QA tra cuu va thu nghiem contract.

## Root cause

- `package.json` chua co `swagger-ui-express`.
- Express server chua mount route `/api-docs`.
- Khong co OpenAPI document mo ta endpoint, auth scheme, request, response va error code.
- README chi ghi API path roi rac, khong co diem truy cap documentation.

## Corrective action

- Them `swagger-ui-express` va `@types/swagger-ui-express`.
- Tao `src/openapi.ts` lam OpenAPI 3.0.3 document.
- Mount:
  - `GET /api-docs` - Swagger UI.
  - `GET /api-docs.json` - OpenAPI JSON.
- Mo ta health, auth va FR-002 class registration endpoints.
- Cap nhat README voi URL local va endpoint docs.

## Prevention checklist

Truoc khi danh dau mot BE feature la hoan tat, AI phai kiem tra:

- [ ] Moi API public co trong OpenAPI document.
- [ ] Co request schema, response schema va error responses.
- [ ] Endpoint can dang nhap co `securitySchemes` va security requirement.
- [ ] Swagger UI co URL duoc ghi trong README.
- [ ] Co the truy cap `/api-docs.json` khi server dang chay.
- [ ] Chay `npm run typecheck`, `npm run build` va test backend.
- [ ] Neu co feature moi, cap nhat Swagger trong cung vertical slice, khong de sau.

## Verification

```bash
cd Sports_Center_Management_System-UAT-BE
npm run typecheck
npm run build
npm test
npm run dev
curl http://localhost:3000/api-docs.json
```

Expected:

- `/api-docs` tra ve Swagger UI.
- `/api-docs.json` tra ve JSON co `openapi: 3.0.3`.
- FR-002 co trong docs: `GET /api/classes` va `POST /api/class-registrations`.

## AI instruction

Khi them hoac sua backend API, luon tim `src/openapi.ts` truoc khi ket thuc. Neu endpoint moi chua duoc mo ta trong OpenAPI va README chua co URL docs, khong danh dau feature la complete.
