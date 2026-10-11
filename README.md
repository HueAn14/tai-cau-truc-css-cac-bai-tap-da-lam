# [Bài tập] Tái cấu trúc mã CSS của các bài tập đã làm (Landing Page)

> **Khóa học:** CodeGym Web Development  
> **Học viên:** HueAn14  
> **Repository GitHub:** [https://github.com/HueAn14/tai-cau-truc-css-cac-bai-tap-da-lam](https://github.com/HueAn14/tai-cau-truc-css-cac-bai-tap-da-lam)

---

## 🎯 Mục tiêu bài tập
Tái cấu trúc (refactor) toàn bộ mã nguồn CSS của 4 bài tập giao diện Landing Page đã thực hiện trong bài Template:
1. **[Bài tập] Dựng navigation và header của landing page thiết kế sẵn.**
2. **[Bài tập] Dựng phần sản phẩm nổi bật của landing page thiết kế sẵn.**
3. **[Bài tập] Dựng phần số liệu thống kê của landing page thiết kế sẵn.**
4. **[Bài tập] Dựng phần footer của landing page thiết kế sẵn.**

Áp dụng đầy đủ các tính năng SASS (SCSS) hiện đại:
- **Variables (Biến):** Quản lý tập trung toàn bộ màu sắc, kích thước font chữ, khoảng cách đệm, bóng đổ và thời gian chuyển động.
- **Nesting (Lồng nhau):** Trực quan hóa cấu trúc HTML, giảm trùng lặp bộ chọn (selectors).
- **Mixins:** Đóng gói các đoạn định kiểu lặp lại nhiều lần (Flexbox, Grid layout, Button themes, Card styles, Responsive breakpoints).
- **Functions:** Tính toán tỷ lệ phần trăm và chuyển đổi kích thước chuẩn.
- **Kiến trúc SASS 7-1:** Phân chia mã nguồn thành các thư mục chuyên biệt (`abstracts/`, `base/`, `layout/`, `components/`).

---

## 📁 Cấu trúc thư mục dự án

```
tai-cau-truc-css-cac-bai-tap-da-lam/
├── index.html                       # Trang Landing Page hoàn chỉnh (tích hợp đủ 4 phần)
├── original/
│   └── style-original.css           # Mã nguồn CSS thuần trước khi tái cấu trúc
├── scss/
│   ├── abstracts/
│   │   ├── _variables.scss          # Biến màu sắc, khoảng cách, font chữ, bóng đổ
│   │   ├── _functions.scss          # Hàm tính toán rem và phần trăm cột
│   │   └── _mixins.scss             # Mixins flex-layout, grid-layout, button-theme, card-theme, respond-to
│   ├── base/
│   │   ├── _reset.scss              # Reset margin, padding, box-sizing
│   │   └── _typography.scss         # Kiểu chữ, tiêu đề, thẻ tag
│   ├── layout/
│   │   ├── _container.scss          # Khung container và các section
│   │   ├── _header.scss             # Bài tập 1: Navigation & Header + Hero banner
│   │   └── _footer.scss             # Bài tập 4: Dựng phần Footer 4 cột
│   ├── components/
│   │   ├── _buttons.scss            # Nút bấm và các biến thể kích thước / màu sắc
│   │   ├── _products.scss           # Bài tập 2: Thẻ và lưới sản phẩm nổi bật
│   │   └── _stats.scss              # Bài tập 3: Khối số liệu thống kê counter
│   └── main.scss                    # File chính tập hợp toàn bộ partials theo chuẩn 7-1
├── css/
│   ├── style.css                    # File CSS biên dịch hoàn chỉnh từ SASS
│   └── style.css.map                # Source map
├── package.json                     # Scripts biên dịch npm
├── .gitignore                       # Bỏ qua node_modules, log
└── README.md                        # Báo cáo kỹ thuật chi tiết
```

---

## 📌 Chi tiết tái cấu trúc 4 phần của Landing Page

### 1. Navigation và Header (`layout/_header.scss` & `components/_buttons.scss`)
- **Trước tái cấu trúc:** Thanh điều hướng và Hero banner viết bằng CSS đơn lẻ, lặp lại các giá trị `#2563eb`, `#ffffff`, lặp lại cấu trúc flexbox và padding.
- **Sau tái cấu trúc:**
  - Áp dụng `@mixin flex-layout` căn chỉnh logo, danh mục menu và nút hành động.
  - Sử dụng Nesting lồng các trạng thái `:hover`, `&.active` và pseudo-element `::after` tạo gạch chân hiệu ứng mượt mà.
  - Sử dụng biến `$dark-bg`, `$primary-color` tạo dải màu gradient sang trọng cho Hero banner.

### 2. Phần Sản phẩm nổi bật (`components/_products.scss`)
- **Trước tái cấu trúc:** Các thẻ sản phẩm viết thủ công, khó tái sử dụng khi thêm sản phẩm mới.
- **Sau tái cấu trúc:**
  - Áp dụng `@mixin grid-layout(3, 30px)` tạo bố cục 3 cột đều nhau.
  - Sử dụng `@mixin card-theme` đóng gói bo góc (`$border-radius-md`), bóng đổ (`$shadow-md`) và hiệu ứng hover nâng thẻ (`transform: translateY(-5px)`).
  - Tách các badge nhãn trạng thái (`.badge-label--hot`, `.badge-label--new`) bằng biến màu tương ứng.

### 3. Phần Số liệu thống kê (`components/_stats.scss`)
- **Trước tái cấu trúc:** Mã màu nền cứng, các cột viết riêng rẽ, không tối ưu hiển thị trên màn hình nhỏ.
- **Sau tái cấu trúc:**
  - Lưới 4 cột tự động co giãn (`repeat(4, 1fr)`) và chuyển sang 2 cột hoặc 1 cột trên mobile bằng `@include respond-to("md")` và `@include respond-to("sm")`.
  - Hiệu ứng kính mờ (`backdrop-filter: blur(5px)`) và viền bán trong suốt (`rgba($white, 0.15)`).

### 4. Phần Footer (`layout/_footer.scss`)
- **Trước tái cấu trúc:** Khối chân trang dài dòng, lặp lại nhiều lần mã màu xám và viền kẻ.
- **Sau tái cấu trúc:**
  - Bố cục 4 cột mạch lạc: Giới thiệu công ty, Danh mục sản phẩm, Hỗ trợ khách hàng, Form đăng ký Newsletter.
  - Hiệu ứng hover menu (`transform: translateX(4px)`) mượt mà.
  - Responsive linh hoạt: Tự động xếp chồng dọc trên thiết bị di động.

---

## 📊 Bảng so sánh trước và sau khi tái cấu trúc

| Tiêu chí | Trước tái cấu trúc (CSS thuần) | Sau tái cấu trúc (SASS/SCSS) |
|---|---|---|
| **Quản lý biến** | ❌ Màu sắc, font size lặp lại rải rác | ✅ Tập trung 100% trong `_variables.scss` |
| **Bố cục Flex & Grid** | ❌ Viết lại `display: flex; justify-content:...` | ✅ Đóng gói qua `@mixin flex-layout` và `@mixin grid-layout` |
| **Nút bấm & Card** | ❌ Viết lặp lại các đoạn border-radius, box-shadow | ✅ Đóng gói qua `@mixin button-theme`, `@mixin card-theme` |
| **Cấu trúc Selector** | ❌ Phẳng, dài dòng, khó đọc cây DOM | ✅ Nesting lồng nhau tự nhiên, dễ bảo trì |
| **Media Queries** | ❌ Rải rác, khó đồng bộ breakpoint | ✅ Quản lý qua `@mixin respond-to($breakpoint)` |
| **Kiến trúc file** | ❌ Gom 1 file CSS khổng lồ | ✅ Chia 11 file partials theo chuẩn SASS 7-1 |

---

## 🛠️ Hướng dẫn biên dịch SASS

```bash
# Biên dịch một lần:
npm run compile:sass
# hoặc dùng lệnh sass:
sass scss/main.scss css/style.css

# Chế độ tự động lắng nghe (Watch mode):
npm run watch:sass
# hoặc dùng lệnh:
sass --watch scss/main.scss css/style.css
```
