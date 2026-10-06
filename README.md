# IT209 - Session 04 - Bài tập 1: Khởi tạo Local Repository và Cấu hình danh tính

- **Sinh viên:** Phạm Thanh Phong
- **MSSV:** N24DTCN120
- **Lớp / Học phần:** IT209 - Phát triển ứng dụng Web / Cloud Infrastructure
- **Đường dẫn nộp bài:** `homework/session_04/ex1/`

---

## Tóm tắt nội dung thực hiện

1. **Khởi tạo kho lưu trữ:** Sử dụng `git init` khởi tạo Local Repository trống.
2. **Cấu hình danh tính Local Scope:**
   - Tên tác giả: `git config --local user.name "Pham Thanh Phong"`
   - Email tác giả: `git config --local user.email "thanhphong102006@gmail.com"`
3. **Quản lý tệp tin và Commit:**
   - Tạo mã nguồn ban đầu `app.py`.
   - Chuyển tệp tin vào Staging Area bằng `git add app.py`.
   - Tạo commit đầu tiên bằng `git commit -m "feat: Initial commit with app.py and local identity configuration"`.
4. **Kiểm tra và nghiệm thu:**
   - Kiểm tra email cục bộ: `git config --local user.email` -> `thanhphong102006@gmail.com`
   - Kiểm tra tên cục bộ: `git config --local user.name` -> `Pham Thanh Phong`
   - Kiểm tra lịch sử commit: `git log --oneline` -> commit đầu tiên kèm ID và thông điệp chuẩn mực.

---

> 📄 **Xem báo cáo chi tiết đầy đủ:** [IT209_Session04_BT1_PhamThanhPhong_N24DTCN120.md](./IT209_Session04_BT1_PhamThanhPhong_N24DTCN120.md)
