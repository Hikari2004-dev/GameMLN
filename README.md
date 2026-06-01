# Hướng dẫn deploy lên Vercel

Mô tả nhanh: project này là một trang tĩnh nhỏ (tập tin như `gamemln.html`, `gamemln.js`,...). Tài liệu này hướng dẫn cách deploy lên Vercel bằng Dashboard hoặc Vercel CLI.

## Yêu cầu trước
- Tài khoản Vercel (https://vercel.com)
- (Tùy chọn) Cài Vercel CLI nếu muốn deploy từ dòng lệnh:

```bash
npm install -g vercel
```

## Deploy bằng Vercel Dashboard (khuyên dùng)
1. Đẩy (push) mã nguồn của bạn lên GitHub / GitLab / Bitbucket.
2. Vào https://vercel.com, đăng nhập và chọn "New Project" → "Import Git Repository".
3. Chọn repository chứa project và làm theo hướng dẫn.

Cấu hình build (nếu được yêu cầu):
- Framework Preset: `Other` hoặc `Static Site`.
- Build Command: (để trống) — nếu không cần build step.
- Output Directory: (để trống hoặc `.`) — nếu các file tĩnh ở gốc repo.

Ví dụ: nếu file chính là `gamemln.html` ở gốc, Vercel sẽ phục vụ nó như một trang tĩnh.

## Deploy bằng Vercel CLI
1. Đăng nhập:

```bash
vercel login
```

2. Trong thư mục dự án (chứa `gamemln.html`), chạy:

```bash
vercel --prod
```

3. Theo các bước để liên kết project (chọn scope, project name, và cài đặt). CLI sẽ trả về URL deploy.

## Cấu hình tùy chọn với `vercel.json`
Bạn có thể thêm file `vercel.json` để tinh chỉnh behavior. Ví dụ tối giản cho trang tĩnh:

```json
{
  "version": 2,
  "builds": [
    { "src": "**/*", "use": "@vercel/static" }
  ]
}
```

Đặt file này ở gốc repo nếu bạn cần override detection mặc định.

## Biến môi trường
Nếu project cần biến môi trường (API keys, v.v.), thêm chúng trong Dashboard: Project → Settings → Environment Variables. Tránh commit các secret vào repo.

## Kiểm tra sau deploy
- Mở URL do Vercel cung cấp.
- Nếu gặp lỗi 404, kiểm tra `Output Directory` và file index (ví dụ `gamemln.html`).

## Commit & Push
1. Thêm file mới và commit:

```bash
git add .
git commit -m "Add README with Vercel deploy instructions"
git push origin main
```

2. Sau push, Vercel sẽ tự động build nếu bạn đã import repo vào Dashboard.

## Tài liệu tham khảo
- Vercel Docs: https://vercel.com/docs

---
Nếu bạn muốn, tôi có thể thêm một `vercel.json` mẫu vào repo hoặc viết hướng dẫn cụ thể cho deploy từ branch/CI cụ thể.
