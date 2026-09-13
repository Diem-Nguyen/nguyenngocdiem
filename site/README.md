# Diem Nguyen — personal site

Static site. No build step, no dependencies. Deploy tới GitHub Pages bằng cách đẩy 2 file này lên repo.

## Files

```
index.html      ← tất cả nội dung nằm ở đây, sửa trực tiếp
styles.css      ← màu, font, khoảng cách
images/         ← ảnh chân dung + logo (tự tạo folder này)
```

## Cần làm trước khi deploy

1. **Substack** — mở `index.html`, tìm khối `SUBSTACK` trong `<head>` và sửa:

```js
const SUBSTACK = {
  handle: "YOURNAME",   // tên Substack của bạn
  formHeight: 200       // chiều cao form subscribe (px)
};
```

Link archive và form subscribe tự cập nhật theo `handle`.

1b. **Danh sách bài viết** — Substack không cho nhúng trang archive vào domain ngoài Substack (CSP `frame-ancestors`), nên section Writing dùng link trực tiếp tới archive. Trang archive luôn hiển thị các bài mới nhất.

2. **Email** — sửa `mailto:hello@example.com` ở section Connect.

3. **Ảnh** — tạo folder `images/` và thêm ảnh, rồi bỏ dấu comment `<!-- -->` quanh thẻ `<img>` tương ứng trong `index.html`:
   - `portrait.jpg` — ảnh chân dung, tỉ lệ dọc 4:5, nên rộng ≥ 680px
   - `nordea.png`, `skenariolabs.png`, `aalto.png`, `standard-chartered.png`, `iuh.png`, `shop.png` — logo timeline, vuông, nền trong suốt
   - Mốc nào không có logo thì cứ để nguyên comment, khung vẫn giữ nhịp cho timeline.

4. **Mốc retail shop** — năm đang để tạm `2023 – 2023`, sửa lại cho đúng.

5. **Canonical URL** — sửa `<link rel="canonical">` và `og:image` trong `<head>` khi biết domain thật.

## Deploy lên GitHub Pages

```
git init
git add .
git commit -m "personal site"
git branch -M main
git remote add origin https://github.com/YOURUSER/YOURUSER.github.io.git
git push -u origin main
```

Repo tên `YOURUSER.github.io` → site chạy ở `https://YOURUSER.github.io`.
Repo tên khác → vào Settings → Pages → Source: `main` / `root`, site chạy ở `https://YOURUSER.github.io/REPONAME/`.

## Thêm một mốc timeline

Copy nguyên khối này, dán vào đúng vị trí theo thứ tự thời gian:

```html
<div class="entry">
  <div class="entry-years">2019 – 2020</div>
  <div class="entry-rail"></div>
  <div class="plate entry-logo"><img src="images/logo.png" alt=""></div>
  <div class="entry-body">
    <p class="entry-role">Chức danh</p>
    <p class="entry-org">Công ty, địa điểm</p>
    <p class="entry-text">Một đến hai câu mô tả.</p>
  </div>
</div>
```

## Ghi chú

- Iframe Substack có thể không hiện khi mở file bằng `file://` — cần chạy qua server. Test local: `python3 -m http.server` rồi mở `http://localhost:8000`.
- Font tải từ Google Fonts. Muốn hoàn toàn offline thì tải Cormorant Garamond + Lora về và đổi sang `@font-face`.
