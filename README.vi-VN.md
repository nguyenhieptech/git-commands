# Git and Command Line 💻

🚀 Các câu lệnh Git hữu ích dùng hàng ngày (có thể) 🚀

## Quy trình sử dụng Git cho các dự án thường thấy

- Tạo 1 nhánh mới từ main ở trên local
- Làm việc trên nhánh đó, rồi commit trên local
- Đẩy nhánh đó lên remote repository (Github, Gitlab, v.v.)
- Tạo pull request (tức là yêu cầu merge code vào main từ nhánh mới đẩy lên) trên Github (remote repository)
- Merge code từ nhánh vừa đẩy lên trên Github vào main trên Github (bước này thường sẽ có người check trước khi merge code, để lại comment bình luận, góp ý sửa đổi...). Sau khi mọi thứ hoàn thành, thì code đc merge vào nhánh chính (main hay master)
- Pull code từ remote về local với 'git pull origin main'

Một bình luận của ai đó:

- Mình cũng giống bạn, khi checkout qua branch của mình để code, thì lúc đó nhánh develop được lead merge source của lập trình viên khác, mình save stash, checkout develop, pull, quay về nhánh mình làm, apply stash, merge develop là conflict, và mình thường sẽ làm thủ công lại, mong có cao nhân chỉ giáo.
  Các bác có thể gõ lệnh git pull --rebase --autostash để nó làm tự động mọi việc trên cho mình
