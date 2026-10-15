# 🌤️ Nyanz Weather Theme — Thời tiết Hà Nội

Trang thời tiết HTML đơn giản, đẹp, dùng dữ liệu thời tiết **thời gian thực** của [Open-Meteo](https://open-meteo.com/) (miễn phí, không cần API key) cho vị trí **Hà Nội, Việt Nam** (21.0278°N, 105.8342°E).

Toàn bộ nằm trong **một file duy nhất** `index.html` — không cần cài đặt, không build, không dependency.

## 🚀 Cách dùng

**Cách 1 — Mở thẳng file (đơn giản nhất):**
Double-click file `index.html` là chạy được ngay. API của Open-Meteo cho phép CORS từ mọi nguồn (`access-control-allow-origin: *`) nên mở qua `file://` vẫn tải được dữ liệu.

**Cách 2 — Chạy qua server local (khuyên dùng khi chỉnh sửa):**
```bash
cd nyanz-weather-theme
python3 -m http.server 8123
```
Mở [http://localhost:8123](http://localhost:8123) trong trình duyệt.

> Yêu cầu duy nhất: máy phải **có internet** (để gọi API và tải font Be Vietnam Pro từ Google Fonts). Nếu mất mạng, trang sẽ hiện màn hình lỗi kèm nút thử lại.

## ✨ Tính năng

- **Dữ liệu thật, tự cập nhật** mỗi 10 phút (kèm nút "Làm mới" thủ công)
- **Nền gradient động** đổi theo điều kiện thời tiết & ngày/đêm — 13 theme: nắng, ít mây, nhiều mây, mưa, mưa phùn, dông, tuyết, sương mù… (phiên bản ngày & đêm)
- **Icon thời tiết hoạt hình vẽ bằng SVG** (không dùng ảnh): tia nắng quay, mây trôi, mưa rơi, chớp lóe, tuyết rơi, trăng lưỡi liềm + sao lấp lánh
- **Hero**: nhiệt độ hiện tại, mô tả tiếng Việt, cao/thấp hôm nay, cảm giác như, đồng hồ realtime
- **Dự báo 24 giờ**: dải cuộn ngang, icon theo giờ (phân biệt ngày/đêm), xác suất mưa
- **8 thẻ chi tiết**: chỉ số UV (kèm thanh màu), gió (mũi tên xoay theo hướng thật), độ ẩm, chất lượng không khí EAQI + PM2.5, áp suất, mây che phủ, cảm giác như, lượng mưa
- **Cung mặt trời**: vị trí mặt trời theo giờ thực giữa bình minh và hoàng hôn, độ dài ban ngày
- **Dự báo 7 ngày**: kèm thanh khoảng nhiệt min → max
- **Glassmorphism** (thẻ kính mờ), animation xuất hiện lan tỏa, hover mượt
- **Responsive** — đẹp từ điện thoại đến desktop, tôn trọng `prefers-reduced-motion`

## 📁 Cấu trúc

```
nyanz-weather-theme/
├── index.html   # Toàn bộ trang: HTML + CSS + JS (gọi API, render, icon SVG)
└── README.md    # File này
```

## 🔧 Tùy chỉnh

Mở `index.html`, sửa ở đầu khối `<script>` cuối file:

| Muốn đổi | Sửa gì | Vị trí |
|---|---|---|
| Vị trí | `LAT`, `LON` (và tên hiển thị trong HTML) | `const LAT = 21.0278, LON = 105.8342;` + `<h1>Hà Nội</h1>` |
| Chu kỳ tự làm mới | `setInterval(load, 10 * 60 * 1000)` | cuối file (ms) |
| Số ngày dự báo | `forecast_days=7` | trong `FORECAST_URL` |
| Số giờ dự báo | vòng lặp `idx + 24` | hàm `render()` |
| Màu nền các theme | khối CSS `body[data-theme="..."]` | đầu `<style>` |

Tọa độ lấy nhanh: mở [open-meteo.com](https://open-meteo.com/en/docs) hoặc Google Maps (chuột phải vào vị trí → copy kinh độ/vĩ độ).

## 📊 Nguồn dữ liệu

- **Thời tiết**: [Open-Meteo Forecast API](https://open-meteo.com/en/docs) — nhiệt độ, gió, ẩm, UV, mưa, mặt trời, dự báo giờ/ngày
- **Không khí**: [Open-Meteo Air Quality API](https://open-meteo.com/en/docs/air-quality-api) — EAQI (thang châu Âu) và PM2.5; nếu API này lỗi, thẻ không khí sẽ hiện "Không có dữ liệu" mà không ảnh hưởng phần còn lại
- Mô tả thời tiết dịch tiếng Việt theo mã WMO (`weather_code`)
