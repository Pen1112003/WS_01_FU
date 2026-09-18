# BUG-002: Git push bi tu choi quyen ghi voi HTTP 403

- **Status:** Blocked / Resolved locally
- **Area:** GitHub authentication and delivery
- **Detected:** 2026-09-18
- **Affected repositories:** `Sports_Center_Management_System-UAT-BE`, `Sports_Center_Management_System-UAT-FE`
- **Severity:** High for delivery, Low for source code

## Symptom

Commit local thanh cong nhung `git push -u origin feature/3-fr-001-auth` that bai:

```text
remote: Permission to Pen1112003/<repository>.git denied to Pen1112003.
fatal: unable to access ...: 403
```

Hai commit van con an toan o local va branch `feature/3-fr-001-auth` dang `ahead 1`:

- BE: commit `aea3837`
- FE: commit `a6eeda5`

## Root cause

Codespaces co nhieu credential GitHub:

- `GITHUB_TOKEN` dang duoc uu tien cho `gh`/Git operations.
- Credential luu trong `~/.config/gh/hosts.yml` la account khac/inactive nhung co scope `repo`.
- Remote URL cua FE va BE dung dung repository, nhung credential dang active khong co quyen push phu hop.

Kiem tra quyen repository bang credential co quyen cho thay `viewerPermission: ADMIN`, vi vay loi nam o credential duoc Git dung khi push, khong phai branch hay remote sai.

## Prevention checklist

Truoc khi push, AI/user phai kiem tra:

- [ ] `git remote -v` dung repository target.
- [ ] `git branch --show-current` dung branch can day.
- [ ] `git status --short --branch` xac nhan commit local va khong co thay doi bat ngo.
- [ ] `gh auth status` xac nhan dung account active.
- [ ] `gh repo view <owner>/<repo> --json viewerPermission` tra ve `WRITE` hoac `MAINTAIN`/`ADMIN`.
- [ ] Kiem tra `GITHUB_TOKEN` khong phai token cu, het han, sai owner hoac khong co quyen repository.
- [ ] FE va BE push tach rieng dung remote.
- [ ] Khong in token vao terminal log, chat, issue hoac commit.

## Remediation

Chon mot trong hai cach:

### Cach 1: Dung credential Codespaces co quyen `repo`

```bash
gh auth status
gh auth switch --hostname github.com
```

Chon account co quyen write vao hai repository, sau do push lai tung repo.

### Cach 2: Cap nhat credential/token dung quyen

- Tao/rotate token co quyen ghi vao hai repository.
- Xoa token cu/bi lo.
- Cap nhat secret trong Codespaces, khong commit vao `.env`.
- Mo terminal moi de credential helper nhan gia tri moi.

### Cach da xac nhan trong Codespaces

Dry-run push thanh cong cho ca FE va BE khi bo qua bien moi truong dang override credential:

```bash
cd /workspaces/Sports_Center_Management_System-UAT-BE
env -u GITHUB_TOKEN git push -u origin feature/3-fr-001-auth

cd /workspaces/Sports_Center_Management_System-UAT-FE
env -u GITHUB_TOKEN git push -u origin feature/3-fr-001-auth
```

Khong dung `git push` that tu dong trong agent. User chay hai lenh tren sau khi kiem tra lai remote va branch.

## AI instruction

Khi user yeu cau push, truoc khi thao tac phai kiem tra remote, branch va quyen repository. Neu gap HTTP 403, khong lap lai push vo han; kiem tra credential active va `viewerPermission`, bao ro commit local dang an toan, sau do yeu cau user xac nhan credential co quyen write.
