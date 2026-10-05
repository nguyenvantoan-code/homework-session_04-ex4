# Báo Cáo Bài 4: Quản lý tệp tin bỏ qua (.gitignore) và Sửa lịch sử (Amend)

## 📌 Tổng Quan Bài Tập
- **Học viên:** Đã thực hiện đầy đủ các yêu cầu theo bài tập.
- **Đường dẫn nộp bài:** `homework/session_04/ex4/`
- **Mục tiêu đạt được:**
  1. Cấu hình tệp tin ẩn `.gitignore` để tự động bỏ qua các tệp nhạy cảm (như `credentials.txt`).
  2. Gỡ bỏ tệp đã lỡ commit ra khỏi bộ nhớ đệm (Git cache/index) bằng `git rm --cached` mà vẫn giữ nguyên tệp vật lý trên ổ đĩa.
  3. Chỉnh sửa thông điệp và nội dung commit gần nhất thông qua tùy chọn `git commit --amend`.

---

## 🛠️ Các Bước Thực Hiện Chi Tiết

### Bước 1: Tình huống giả lập
Giả lập tình huống lỡ commit nhầm tệp chứa thông tin bảo mật `credentials.txt` vào Git:
```bash
git add .
git commit -m "feat: Khoi tao du an va commit nham credentials.txt"
```

### Bước 2: Gỡ bỏ `credentials.txt` khỏi Git Index (Cache)
Sử dụng lệnh `git rm --cached` để ngưng theo dõi tệp mà không xóa tệp thực tế trên đĩa cứng:
```bash
git rm --cached homework/session_04/ex4/credentials.txt
```
> **Giải thích:**
> - `git rm`: Xóa tệp khỏi Git repository.
> - `--cached` (hoặc `--staged`): Chỉ xóa tệp khỏi chỉ mục bộ nhớ đệm (Stage/Index) của Git, giữ nguyên tệp vật lý ở thư mục làm việc (Working Tree).

### Bước 3: Cấu hình tệp `.gitignore`
Tạo tệp `.gitignore` trong thư mục `homework/session_04/ex4/` để Git tự động bỏ qua `credentials.txt` và các tệp rác khác:
```gitignore
# Ignore sensitive credential files and secrets
credentials.txt
*.env
*.log
```

### Bước 4: Cập nhật Staging và sửa Commit gần nhất bằng `--amend`
Đưa `.gitignore` vào Staging Area và tiến hành sửa commit gần nhất:
```bash
git add .
git commit --amend -m "feat: Initial commit for exercise 4 (remove credentials.txt and add .gitignore)"
```
> **Giải thích:**
> - `git commit --amend`: Ghi đè lên commit gần nhất, kết hợp các thay đổi mới trong Staging Area và cập nhật thông điệp commit cho sạch sẽ.

---

## ✅ Kết Quả Kiểm Tra (Verification)

### 1. Kiểm tra trạng thái Git (`git status`)
```bash
git status
```
**Kết quả thực tế:**
```text
On branch master
nothing to commit, working tree clean
```
*Tệp `credentials.txt` không còn xuất hiện trong danh sách theo dõi của Git (không ở dạng Staged hay Modified).*

### 2. Kiểm tra danh sách tệp đang được Git theo dõi (`git ls-files`)
```bash
git ls-files
```
**Kết quả thực tế:**
```text
.gitignore
homework/session_04/ex4/.gitignore
homework/session_04/ex4/app.js
homework/session_04/ex4/README.md
```
*Tệp `credentials.txt` đã hoàn toàn được gỡ bỏ khỏi index theo dõi.*

### 3. Kiểm tra sự tồn tại vật lý của tệp trên đĩa cứng
Tệp `credentials.txt` vẫn còn nguyên vẹn trong thư mục làm việc cục bộ `homework/session_04/ex4/credentials.txt`.

### 4. Kiểm tra lịch sử Commit gần nhất (`git log -n 1`)
```bash
git log -n 1
```
**Kết quả thực tế:**
```text
commit 5f2590f14d39f1fb975edc20006c7916851080a0
Author: Hoc Vien <hocvien@example.com>
Date:   Mon Oct 5 21:36:20 2026 +0700

    feat: Initial commit for exercise 4 (remove credentials.txt and add .gitignore)
```
