# PHIẾU BÀI TẬP 03 — ĐÁP ÁN

## PHẦN A — KIỂM TRA ĐỌC HIỂU

### Câu A1 — 3 Cách nhúng CSS

1. Inline CSS
```html
<p style="color: red;">Nội dung</p>
```
- Ưu điểm: Áp dụng nhanh, chỉ cho một thẻ duy nhất.
- Nhược điểm: Khó bảo trì, không tái sử dụng được, làm HTML lộn xộn.
- Khi dùng: Dùng khi muốn test nhanh hoặc áp dụng style độc nhất cho 1 phần tử.

2. Internal CSS
```html
<head>
    <style>
        p { color: blue; }
    </style>
</head>
```
- Ưu điểm: Gọn với một trang, dễ quản lý hơn inline.
- Nhược điểm: Chỉ áp dụng cho trang hiện tại, vẫn không tách được style khỏi nội dung.
- Khi dùng: Dùng khi chỉ có 1 trang hoặc đang thử nghiệm thiết kế.

3. External CSS
```html
<link rel="stylesheet" href="style.css">
```
- Ưu điểm: Tách biệt nội dung và trình bày, dễ tái sử dụng cho nhiều trang, cache trình duyệt.
- Nhược điểm: Cần thêm request HTTP nếu không được cache.
- Khi dùng: Dùng cho dự án thực tế, nhiều trang hoặc khi muốn giữ code sạch.

**Trường hợp cùng 1 element có cả 3 cách:**
- Inline CSS thắng vì nó có độ ưu tiên (specificity) cao nhất.
- Internal và external đều bị so sánh theo nguồn và thứ tự xuất hiện; nếu cùng selector thì internal sau external sẽ thắng.
- Nhìn chung: inline > internal > external, vì cascade ưu tiên style attribute trên style sheet.

### Câu A2 — CSS Selectors

1. `h1` → Chọn thẻ `<h1>` có nội dung `ShopTLU`.
2. `.price` → Chọn hai phần tử `<p class="price">` chứa `25.990.000đ` và `45.990.000đ`.
3. `#app header` → Chọn phần tử `<header class="top-bar dark">` chứa tiêu đề và menu.
4. `nav a:first-child` → Chọn liên kết đầu tiên trong nav: `Home`.
5. `.product.featured h2` → Chọn thẻ `<h2>` trong sản phẩm có class `product featured`: `MacBook Pro`.
6. `article > p` → Chọn tất cả thẻ `<p>` trực tiếp con của mỗi `<article>`:
   - `25.990.000đ`
   - `Mô tả sản phẩm...`
   - `45.990.000đ`
   - `Mô tả sản phẩm...`
7. `a[href="/"]` → Chọn liên kết `Home`.
8. `.top-bar.dark h1` → Chọn thẻ `<h1>` `ShopTLU` bên trong header có class `top-bar dark`.

### Câu A3 — Box Model

Trường hợp 1: content-box
- Chiều rộng hiển thị của phần tử = 400px + 20px + 20px + 5px + 5px = 450px.
- Không gian chiếm trên trang = 450px + 10px + 10px = 470px.

Trường hợp 2: border-box
- Chiều rộng hiển thị của phần tử = 400px (bao gồm padding và border).
- Kích thước content thực tế = 400px - 20px - 20px - 5px - 5px = 350px.
- Không gian chiếm trên trang = 400px + 10px + 10px = 420px.

Trường hợp 3: Margin collapse
- Khoảng cách giữa `.box-a` và `.box-b` = 40px.
- Giải thích: margin-bottom 25px và margin-top 40px không cộng, mà bị hợp nhất (collapse) thành giá trị lớn hơn là 40px.

Nâng cao: margin-bottom -10px và margin-top 40px
- Khoảng cách giữa hai hộp = 30px.
- Giải thích: margin âm được cộng với margin dương khi collapse; kết quả là 40 + (-10) = 30.

### Câu A4 — Specificity

Các rule với selector và specificity:
- Rule A `p { color: black; }` → (0,0,1)
- Rule B `.price { color: blue; }` → (0,1,0)
- Rule C `#main-price { color: red; }` → (1,0,0)
- Rule D `p.price { color: green; }` → (0,1,1)

2. Element có màu gì?
- Màu cuối cùng là `red`, vì rule C có specificity cao nhất trong số các rule bình thường.

3. Nếu thêm `style="color: orange;"`
- Element có màu `orange`, vì style inline có độ ưu tiên cao hơn các rule CSS bình thường.

4. Nếu Rule A thêm `!important`
- Element có màu `black` nếu không có rule khác !important hoặc inline !important.
- Vì `!important` làm rule A mạnh hơn bất kỳ rule bình thường nào, kể cả rule C với ID selector.

## PHẦN B — NỘI DUNG FILE

- `selectors_test.html`: kiểm chứng A2 selector với HTML mẫu.
- `profile.html` + `style.css`: bài B1, sử dụng external CSS, hover/active cho navigation, table zebra striping và box-sizing reset.
- `boxmodel_lab.html` + `boxmodel.css`: bài B2, minh họa content-box vs border-box và layout 3 cột.
- `specificity.html` + `specificity.css`: bài B3, 10 rule color khác nhau, final color do !important.
- `debug_layout.html` + `debug_layout.css`: C1, chứng minh cả 2 cách sửa layout.
- `cascade_puzzle.html` + `cascade_puzzle.css`: chứng minh C2 cascade và inheritance.

> Chụp screenshot: Tôi không thể tự chụp screenshot trong môi trường này. Bạn mở các file sau và chụp ảnh theo yêu cầu:
> - `selectors_test.html`
> - `boxmodel_lab.html` (tab Computed box model)
> - `specificity.html`
> - `debug_layout.html`
> - `cascade_puzzle.html`

## PHẦN C — DEBUG & SUY LUẬN

### Câu C1 — Debug CSS Layout

1. Chiều rộng thực tế (content-box):
   - Sidebar: 300px + 20px + 20px + 1px + 1px = 342px.
   - Content: 660px + 30px + 30px + 1px + 1px = 722px.

2. Tại sao layout bị vỡ?
   - Tổng diện tích thực tế của sidebar và content = 342px + 722px = 1064px, lớn hơn container 960px.
   - Vì content-box cộng padding và border vào ngoài width, nên hai khối không còn vừa hàng.

3. Hai cách sửa:
   - Cách 1: dùng `box-sizing: border-box;` cho cả `.sidebar` và `.content`, khi đó width đã bao gồm padding/border.
   - Cách 2: vẫn dùng content-box nhưng giảm width thực tế của `.sidebar` và `.content` sao cho tổng không vượt 960px.

4. File kiểm chứng:
   - `debug_layout.html`
   - `debug_layout.css`

### Câu C2 — Cascade Puzzle

1. "Sản phẩm A" (h2) có:
   - `font-size`: 20px, vì rule `.card .title` là rule cụ thể nhất chỉ định kích thước.
   - `color`: green, vì `.highlight { color: green !important; }` được dùng và đánh bại các rule bình thường khác.

2. "Mô tả sản phẩm" (p trong card featured) có:
   - `color`: blue.
   - Giải thích: `.card p { color: inherit; }` khiến thẻ p kế thừa màu từ `.card`, và `.card { color: blue; }` là rule áp dụng trực tiếp.

3. "Sản phẩm B" (h2) có:
   - `font-size`: 20px.
   - `color`: blue, vì rule `.card .title` chỉ định kích thước nhưng không thay đổi màu; màu kế thừa từ `.card`.

4. "Mô tả sản phẩm B" (p.highlight) có:
   - `color`: green, vì `.highlight` có `!important`.

File kiểm chứng: `cascade_puzzle.html` + `cascade_puzzle.css`.
