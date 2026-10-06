# Báo cáo Bài tập 1: Khởi tạo Local Repository và Cấu hình danh tính

**Thông tin sinh viên:**
- **Họ và tên:** Phạm Thanh Phong
- **Mã sinh viên / Lớp:** N24DTCN120
- **Môn học:** IT209 - Phát triển ứng dụng Web / Cloud Infrastructure
- **Session:** Session 04 - Quản lý phiên bản mã nguồn với Git & GitHub
- **Bài tập:** Bài tập 1 (ex1)

---

## 1. Mục tiêu & Bối cảnh bài toán

### 1.1. Bối cảnh (Context)
Trong môi trường phát triển phần mềm chuyên nghiệp (DevOps / Software Engineering), một kỹ sư có thể cùng lúc tham gia nhiều dự án khác nhau (dự án công ty, bài tập học phần đại học, dự án cá nhân mã nguồn mở). Mỗi dự án có thể yêu cầu danh tính tác giả (Author Name & Email) khác nhau. Do đó, việc hiểu rõ và cấu hình danh tính ở phạm vi cục bộ (**Local Scope**) là kỹ năng nền tảng bắt buộc để đảm bảo tính minh bạch, chính xác trong lịch sử commit mà không gây xung đột với cấu hình toàn cục (**Global Scope**) của hệ điều hành.

### 1.2. Mục tiêu kỹ thuật
- Khởi tạo thành công một kho lưu trữ Git cục bộ trống (**Local Repository**) tại thư mục dự án.
- Thiết lập thông tin danh tính tác giả (`user.name` và `user.email`) ở cấp độ cục bộ (**Local**) thông qua tùy chọn `--local`.
- Tạo tệp tin mã nguồn mới, đưa vào vùng chuẩn bị (**Staging Area / Index**) bằng lệnh `git add`.
- Đóng gói và ghi lại trạng thái thay đổi vào kho lưu trữ bằng lệnh `git commit` với thông điệp rõ nghĩa, tuân thủ quy ước conventional commits.
- Đọc, phân tích và nghiệm thu trạng thái thư mục làm việc (`git status`), cấu hình cục bộ (`git config --local --list`) và lịch sử commit (`git log`).

### 1.3. Ràng buộc kỹ thuật
- **Bắt buộc sử dụng cờ `--local`:** Tuyệt đối không sử dụng cờ `--global` hoặc `--system` để tránh ghi đè thông tin danh tính dùng chung trên máy tính.
- **Tính toàn vẹn của commit:** Đảm bảo commit đầu tiên (Root Commit) mang đúng thông tin tác giả vừa được thiết lập trong repository.

---

## 2. Cơ sở lý thuyết & Phân tích kiến trúc Git

### 2.1. Ba trạng thái và Ba vùng làm việc của Git

Hệ thống Git quản lý mã nguồn thông qua 3 vùng chính:

```
┌─────────────────────────┐       git add       ┌─────────────────────────┐     git commit      ┌─────────────────────────┐
│    Working Directory    │ ──────────────────► │  Staging Area (Index)   │ ──────────────────► │    Local Repository     │
│   (Thư mục làm việc)    │                     │     (Vùng chuẩn bị)     │                     │     (Kho lưu trữ .git)  │
└─────────────────────────┘                     └─────────────────────────┘                     └─────────────────────────┘
  (Untracked / Modified)                              (Staged files)                              (Committed / HEAD)
```

1. **Working Directory (Thư mục làm việc):** Nơi chứa các tệp tin vật lý người dùng trực tiếp tạo mới, chỉnh sửa hoặc xóa bỏ trên ổ đĩa.
2. **Staging Area / Index (Vùng chuẩn bị):** Nơi ghi nhận và đánh dấu các thay đổi sẵn sàng được đưa vào lần commit kế tiếp.
3. **Local Repository (Kho lưu trữ `.git`):** Nơi lưu trữ vĩnh viễn cơ sở dữ liệu đối tượng (objects: blob, tree, commit, tag) và lịch sử các phiên bản commit.

### 2.2. Phân cấp mức độ cấu hình trong Git (Configuration Hierarchy)

Git quản lý cấu hình theo thứ tự ưu tiên từ cao xuống thấp:

| Mức độ (Level) | Cờ lệnh | Vị trí lưu trữ | Mức độ ưu tiên | Mô tả |
| :--- | :--- | :--- | :---: | :--- |
| **Local** | `--local` | `.git/config` (trong thư mục dự án) | **Cao nhất (Highest)** | Áp dụng riêng cho repository hiện tại, ghi đè global và system. |
| **Global** | `--global` | `~/.gitconfig` (thư mục Home người dùng) | **Trung bình** | Áp dụng cho tất cả repository của người dùng hiện tại trên OS. |
| **System** | `--system` | `/etc/gitconfig` hoặc `C:\Program Files\Git\etc\gitconfig` | **Thấp nhất** | Áp dụng cho toàn bộ người dùng trên toàn hệ điều hành. |

---

## 3. Quy trình thực hiện chi tiết

### Bước 1: Khởi tạo Git Repository cục bộ
Di chuyển vào thư mục làm việc và khởi tạo Git repository:
```bash
# Khởi tạo repository rỗng
git init
```
*Hệ thống sẽ tạo thư mục ẩn `.git/` chứa toàn bộ metadata, object store và cấu hình của repository.*

---

### Bước 2: Thiết lập danh tính tác giả ở phạm vi Local
Thiết lập tên và địa chỉ email định danh cho sinh viên Phạm Thanh Phong (MSSV: N24DTCN120):
```bash
# Cấu hình tên tác giả cục bộ
git config --local user.name "Pham Thanh Phong"

# Cấu hình email tác giả cục bộ
git config --local user.email "thanhphong102006@gmail.com"
```

---

### Bước 3: Tạo mã nguồn và kiểm tra trạng thái Untracked
Tạo tệp mã nguồn chương trình `app.py`:
```python
"""
IT209 - Session 04 - Bài tập 1
Sinh viên: Phạm Thanh Phong
MSSV: N24DTCN120
"""

def main():
    print("==========================================")
    print("IT209 - Session 04: Git & Version Control")
    print("Học viên: Phạm Thanh Phong - N24DTCN120")
    print("Khởi tạo Local Repository thành công!")
    print("==========================================")

if __name__ == "__main__":
    main()
```

Kiểm tra trạng thái Working Directory:
```bash
git status
```
*Kết quả ghi nhận tệp `app.py` đang ở trạng thái `Untracked files`.*

---

### Bước 4: Đưa tệp tin vào Staging Area và tiến hành Commit đầu tiên
```bash
# Đưa tệp app.py vào vùng Staging Area
git add app.py

# Đóng gói commit đầu tiên (Root Commit)
git commit -m "feat: Initial commit with app.py and local identity configuration"
```

---

## 4. Nhật ký thực thi & Minh chứng nghiệm thu (Verification Logs)

### 4.1. Minh chứng cấu hình danh tính cục bộ (`--local`)

#### Lệnh 1: Kiểm tra Email cục bộ
```bash
git config --local user.email
```
**Output thực tế:**
```text
thanhphong102006@gmail.com
```

#### Lệnh 2: Kiểm tra Tên tác giả cục bộ
```bash
git config --local user.name
```
**Output thực tế:**
```text
Pham Thanh Phong
```

#### Lệnh 3: Liệt kê toàn bộ cấu hình Local Scope
```bash
git config --local --list
```
**Output thực tế:**
```text
core.repositoryformatversion=0
core.filemode=false
core.bare=false
core.logallrefupdates=true
core.symlinks=false
core.ignorecase=true
user.name=Pham Thanh Phong
user.email=thanhphong102006@gmail.com
```

---

### 4.2. Minh chứng nội dung tệp tin cấu hình `.git/config`
Nội dung file cấu hình vật lý tại `.git/config` chứng minh cấu hình `user` đã được ghi trực tiếp vào repository:
```ini
[core]
	repositoryformatversion = 0
	filemode = false
	bare = false
	logallrefupdates = true
	symlinks = false
	ignorecase = true
[user]
	name = Pham Thanh Phong
	email = thanhphong102006@gmail.com
```

---

### 4.3. Minh chứng lịch sử Commit (`git log`)

#### Lệnh 1: Xem log ngắn gọn (`--oneline`)
```bash
git log --oneline
```
**Output thực tế:**
```text
2b4366a feat: Initial commit with app.py and local identity configuration
```

#### Lệnh 2: Xem chi tiết thông tin tác giả và thời gian commit (`--pretty=fuller`)
```bash
git log -1 --pretty=fuller
```
**Output thực tế:**
```text
commit 2b4366aea2950c6983dbe6bb0ed140e5e1cdcebe
Author:     Pham Thanh Phong <thanhphong102006@gmail.com>
AuthorDate: Tue Oct 6 09:01:56 2026 +0700
Commit:     Pham Thanh Phong <thanhphong102006@gmail.com>
CommitDate: Tue Oct 6 09:01:56 2026 +0700

    feat: Initial commit with app.py and local identity configuration
```

#### Lệnh 3: Xem thống kê thay đổi tệp tin (`-1 --stat`)
```bash
git log -1 --stat
```
**Output thực tế:**
```text
commit 2b4366aea2950c6983dbe6bb0ed140e5e1cdcebe
Author: Pham Thanh Phong <thanhphong102006@gmail.com>
Date:   Tue Oct 6 09:01:56 2026 +0700

    feat: Initial commit with app.py and local identity configuration

 app.py | 15 +++++++++++++++
 1 file changed, 15 insertions(+)
```

---

## 5. Hướng dẫn nộp bài & Cấu trúc thư mục kho lưu trữ

- **Đường dẫn trên GitHub:** `homework/session_04/ex1/`
- **Tệp báo cáo:** `README.md` (hoặc `IT209_Session04_BT1_PhamThanhPhong_N24DTCN120.md`)
- **Cấu trúc nộp bài chuẩn:**
```text
homework/session_04/ex1/
├── .git/
├── app.py
├── IT209_Session04_BT1_PhamThanhPhong_N24DTCN120.md
└── README.md
```

---

## 6. Tổng kết & Đánh giá bài học

1. **Hiểu rõ cơ chế phân cấp cấu hình Git:** Việc sử dụng cờ `--local` giúp lập trình viên quản trị nhiều profile (cá nhân, học tập, doanh nghiệp) một cách linh hoạt, độc lập trên cùng một máy trạm.
2. **Làm chủ vòng đời trạng thái tệp tin:** Nắm vững quy trình chuyển đổi tệp tin từ `Untracked` -> `Staged` (`git add`) -> `Committed` (`git commit`).
3. **Chuẩn hóa thông điệp Commit:** Đặt tên commit theo chuẩn Conventional Commits (`feat: ...`, `fix: ...`, `docs: ...`) giúp việc theo dõi lịch sử dự án trở nên rõ ràng và chuyên nghiệp.
