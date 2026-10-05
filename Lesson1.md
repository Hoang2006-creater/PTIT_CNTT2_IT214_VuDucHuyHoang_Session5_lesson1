# Bài 1: Khôi phục commit đã mất bằng Git Reflog

## 1. Khởi tạo repository

Khởi tạo một repository Git mới bằng lệnh:

```bash
git init
```

Tạo file `feature.txt` với nội dung:

```text
Day la tinh nang quan trong
```

Sau đó thêm file và commit:

```bash
git add .
git commit -m "Them tinh nang quan trong"
```

## 2. Giả lập việc mất commit

Để mô phỏng trường hợp vô tình xóa commit, thực hiện:

```bash
git reset --hard HEAD~1
```

Sau khi reset, kiểm tra lịch sử:

```bash
git log --oneline
```

Commit `Them tinh nang quan trong` không còn xuất hiện trong lịch sử hiện tại và file `feature.txt` cũng bị xóa khỏi working directory.

## 3. Tra cứu commit bằng Reflog

Sử dụng lệnh:

```bash
git reflog
```

Kết quả cho thấy commit trước đó vẫn được Git lưu lại trong Reflog, ví dụ:

```text
abc1234 HEAD@{0}: reset: moving to HEAD~1
e3a5b2c HEAD@{1}: commit: Them tinh nang quan trong
```

Từ đó xác định được mã hash của commit cần khôi phục là `e3a5b2c`.

## 4. Khôi phục commit

Sử dụng lệnh:

```bash
git reset --hard e3a5b2c
```

Trong đó `e3a5b2c` là mã hash thực tế lấy được từ `git reflog`.

## 5. Kiểm tra kết quả

Kiểm tra lịch sử commit:

```bash
git log --oneline
```

Commit đã được khôi phục:

```text
e3a5b2c Them tinh nang quan trong
```

Kiểm tra file:

```bash
Get-Content feature.txt
```

Kết quả:

```text
Day la tinh nang quan trong
```

## 6. Kết luận

Đã sử dụng thành công `git reflog` để tìm lại commit bị mất sau khi thực hiện `git reset --hard HEAD~1` và khôi phục commit về nhánh hiện tại bằng `git reset --hard`.
