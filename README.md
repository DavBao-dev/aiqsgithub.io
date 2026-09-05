# My Blog — static, zero build step

Blog tĩnh chạy thẳng trên GitHub Pages. Không cần Jekyll, không cần build:
trang tự đọc danh sách file `.md` trong thư mục `posts/` trực tiếp từ GitHub mỗi lần load.
**Push file `.md` mới lên là bài viết xuất hiện ngay**, không cần deploy lại gì cả.

## Cài đặt (làm 1 lần)

1. Tạo một repo mới trên GitHub, để **Public** (cần Public để gọi GitHub API miễn phí, không cần token).
2. Push toàn bộ nội dung thư mục này lên nhánh `main`.
3. Mở file `config.js`, sửa:
   ```js
   owner: "your-github-username",
   repo: "your-repo-name",
   ```
   thành username và tên repo thật của bạn.
4. Vào **Settings → Pages** trên GitHub → Source: chọn branch `main`, folder `/ (root)` → Save.
5. Đợi 1–2 phút, trang sẽ live tại:
   `https://<owner>.github.io/<repo>/`

## Đăng bài mới (từ giờ về sau)

1. Convert file LaTeX/PDF sang Markdown bằng tool converter (đã gửi ở bước trước) — công thức toán ra chuẩn `$...$` / `$$...$$`.
2. Đặt tên file dạng `YYYY-MM-DD-ten-bai-viet.md` (để tự sort theo ngày). Có thể thêm frontmatter ở đầu file:
   ```yaml
   ---
   title: Tiêu đề bài viết
   date: 2026-09-05
   excerpt: Mô tả ngắn hiện ở trang danh sách
   ---
   ```
3. Upload file đó vào thư mục `posts/` — làm trực tiếp trên giao diện web GitHub (Add file → Upload files) hoặc `git push`, đều được.
4. F5 lại trang chủ — bài mới đã xuất hiện, không cần chờ build.

## Giới hạn cần biết

- Trang gọi GitHub API (`api.github.com`) không xác thực để lấy danh sách bài, giới hạn ~60 request/giờ/IP. Với blog cá nhân lượng truy cập vừa phải thì thoải mái. Nếu sau này lượng đọc lớn hoặc muốn để repo **Private**, cần chuyển sang một GitHub Action build tĩnh danh sách bài lúc push thay vì fetch lúc chạy — báo lại nếu cần, mình dựng thêm.
- Công thức toán dùng KaTeX (render phía client). Nếu file `.md` của bạn dùng cú pháp MathJax khác chuẩn (`\(...\)`, `\[...\]`) thì cần convert qua `$...$` / `$$...$$` trước — tool converter ở bước trước đã tự làm việc này.
