Bài 2 - Tái cấu trúc lịch sử commit bằng Interactive Rebase

1\. Mục tiêu

Thực hành sử dụng Interactive Rebase để chỉnh sửa lịch sử commit cục bộ:

\- Gộp nhiều commit nhỏ bằng squash.

\- Đổi tên commit sau khi gộp.

\- Xóa commit không cần thiết bằng drop.

\- Kiểm tra lại lịch sử commit sau khi hoàn tất.

2\. Các commit ban đầu

Ban đầu tạo 4 commit:

feat: khoi tao module auth

fix typo

adds utility functions

add temp file for debug

Kiểm tra bằng lệnh:

git log --oneline -4

Kết quả ban đầu:

e8c365d add temp file for debug

8f97e0b adds utility functions

2e1eba1 fix typo

d9b8f3b feat: khoi tao module auth

3\. Thực hiện Interactive Rebase

Do repository chỉ có đúng 4 commit tính từ commit đầu tiên nên sử dụng:

git rebase -i --root

Trong giao diện Interactive Rebase, cấu hình:

pick d9b8f3b feat: khoi tao module auth

squash 2e1eba1 fix typo

squash 8f97e0b adds utility functions

drop e8c365d add temp file for debug

Ý nghĩa:

\- pick: giữ commit đầu tiên.

\- squash: gộp commit thứ 2 và thứ 3 vào commit đầu tiên.

\- drop: xóa commit chứa file rác temp.txt.

Sau đó lưu và đóng trình soạn thảo.

4\. Đổi tên commit sau khi gộp

Tên commit cuối cùng được đổi thành:

feat: hoan thien module authentication

Nếu cần sửa lại tên commit sau khi rebase, có thể dùng:

git commit --amend -m "feat: hoan thien module authentication"

5\. Kiểm tra kết quả

Kiểm tra lịch sử commit

git log --oneline

Kết quả:

2ab34ae feat: hoan thien module authentication

Kiểm tra file rác

Trong PowerShell:

Test-Path temp.txt

Kết quả:

False

Điều này chứng minh file temp.txt đã bị xóa.

Kiểm tra trạng thái Git

git status

Kết quả:

On branch master

nothing to commit, working tree clean

6\. Kết luận

Sau khi thực hiện Interactive Rebase:

\- Ba commit liên quan đến chức năng authentication đã được gộp thành một commit duy nhất.

\- Commit cuối cùng có tên:

feat: hoan thien module authentication

\- Commit chứa file rác temp.txt đã bị xóa hoàn toàn.

\- Lịch sử Git đã được làm sạch và dễ đọc hơn.

7\. Ảnh minh chứng cần chèn

Ảnh 1 - Giao diện Interactive Rebase

Chụp màn hình có nội dung tương tự:

pick d9b8f3b feat: khoi tao module auth

squash 2e1eba1 fix typo

squash 8f97e0b adds utility functions

drop e8c365d add temp file for debug

Chèn ảnh tại đây.

Ảnh 2 - Kết quả Git Log

Chụp màn hình sau khi chạy:

git log --oneline

Kết quả:

2ab34ae feat: hoan thien module authentication

Chèn ảnh tại đây.

Ảnh 3 - Kiểm tra file temp và trạng thái Git

Chụp màn hình sau khi chạy:

Test-Path temp.txt

git status

Kết quả:

False

On branch master

nothing to commit, working tree clean

