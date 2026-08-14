# oedition-setup-hackathon

Trang hướng dẫn setup máy trước hackathon, dành cho **người chưa từng cài công cụ lập trình** — dev, support, marketing, PO đều dùng được.

Nội dung: cài Claude → tạo tài khoản GitHub → nối GitHub vào Claude/ChatGPT → cài VS Code + GitHub Desktop bằng một lần dán → checklist đối chiếu.

## Đây là gì

**Một file HTML tĩnh duy nhất.** Không framework, không build step, không dependency, không gọi ra mạng ngoài. Mở `index.html` bằng trình duyệt là chạy.

Tính năng:

- **Switch macOS / Windows** ở góc trên — lọc toàn trang, chỉ hiện lệnh của máy người đọc, nhớ lựa chọn trong `localStorage`
- **Nút Copy** trên mọi khối lệnh, có fallback bôi đen khi trình duyệt chặn clipboard
- **Checklist tick được**, có thanh tiến độ, lưu trạng thái qua các lần mở
- **Điều hướng bằng hash** (`#cai-app`) — gửi link thẳng tới một mục được, nút back hoạt động
- **Tự đổi màu** theo theme sáng/tối của máy người đọc

## Chạy thử local

```bash
open index.html            # macOS — mở thẳng bằng trình duyệt
# hoặc chạy qua server nếu muốn giống môi trường thật:
python3 -m http.server 8777
```

## Deploy lên GitHub Pages

1. Push repo này lên GitHub.
2. Vào **Settings → Pages → Source** → chọn **GitHub Actions**.
3. Workflow ở `.github/workflows/pages.yml` tự deploy mỗi lần push vào `main`.

Không dùng Actions cũng được: **Settings → Pages → Source: Deploy from a branch** → `main` / `(root)`. File `.nojekyll` có sẵn để Pages không chạy Jekyll qua thư mục.

## Deploy chỗ khác

Chỉ cần đưa `index.html` lên là xong — Netlify (kéo thả thư mục), Vercel, S3, hay bất kỳ web server nội bộ nào. Không có build step.

## Sửa nội dung

Sửa thẳng `index.html`. Cấu trúc bên trong:

| Phần | Tìm bằng |
|---|---|
| Biến màu, font | khối `:root` ở đầu `<style>` |
| Mục lục bên trái | `<nav class="side">` |
| Từng trang nội dung | `<section class="panel" id="p-...">` |
| Danh sách trang cho routing | `var PAGES = [...]` trong `<script>` |
| Khối lệnh có nút copy | `<div class="cmd">` + `<button class="copy">` |
| Nội dung chỉ hiện trên 1 OS | thêm class `os os-mac` hoặc `os os-win` |

Thêm một trang mới: thêm `<li>` vào nav, thêm `<section class="panel" id="p-tên">`, rồi thêm `'tên'` vào `PAGES`.

## Nguồn

Bản markdown gốc nằm ở `~/second-brain/team-onboarding/` (có thêm phần dành cho dev: prompt setup máy tự động, đăng nhập gh/SSH, cách dùng `gh` và GitHub Desktop hằng ngày — đã lược khỏi trang này).

Lệnh cài đặt và ID gói trong trang đã verify ngày **14/08/2026** với tài liệu chính thức của Claude Code, Microsoft và GitHub. Chữ ký số của 2 app đã kiểm chứng thật:

```
Visual Studio Code → Developer ID Application: Microsoft Corporation (UBF8T346G9)
GitHub Desktop     → Developer ID Application: GitHub (VEKTX9H2N7)
```
