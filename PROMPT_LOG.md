# NHẬT KÝ PROMPT ENGINEERING (VIBE CODING LOG)

- **Họ và tên:** Mai Huy Phong
- **MSSV:** 125000312
- **Tên đề tài Website:** Web Bán Các Sản Phẩm Độc Quyền Trên Thị Trường Nhật Bản - HONEYVAULT (Pokemon, Figure, Light Novel/Truyện Tranh Nhật Bản)
- **Công cụ AI đã sử dụng:** Gemini 3.8 Flash (Google DeepMind Antigravity)

---

## 1. Yêu cầu ban đầu (System/Initial Prompt)

> *"Tôi muốn làm website với tiêu đề 'Web bán các sản phẩm và các sản phẩm độc quyền bán trên thị trường' (HONEYVAULT). Sử dụng 2 ngôn ngữ chính là HTML5 và CSS3 theo đúng yêu cầu đề thi, tuyệt đối không dùng thêm ngôn ngữ lập trình nào khác. Tông màu chính chỉ định gồm: Trắng (`#FFFFFF`), Đen (`#141414`) và Vàng mật ong (`#E5A93C`). Xây dựng hệ thống gồm 1 trang chủ (index.html) và 3 trang sản phẩm con chuyên biệt:
> 1. Pokémon (`pokemon.html`): Các sản phẩm độc quyền từ Pokémon Center Japan (thẻ bài TCG hiếm, gấu bông kỷ niệm, Pokéball kim loại).
> 2. Figure (`figure.html`): Mô hình Anime Figure độc quyền tỉ lệ 1/7, 1/4, Nendoroid Limited từ Good Smile Company, Alter, Aniplex+.
> 3. Light Novel / Truyện tranh Nhật (`manga-novel.html`): Ấn bản đặc biệt có chữ ký tác giả, boxset manga kẹp đai Obi nguyên bản, Artbook triển lãm Tokyo.
> Yêu cầu đáp ứng chuẩn Semantic HTML5 (header, nav, main, section, article, figure, footer), CSS Variables cho bảng màu, layout hiện đại Flexbox/Grid responsive, tích hợp thư viện Animate.css và AOS (Animate On Scroll), hiệu ứng :hover, :focus tự viết, cùng tiện ích chuyển đổi chế độ Sáng / Tối (Dark / Light mode) thuần CSS."*

---

## 2. Quá trình tinh chỉnh & Giải quyết sự cố (Iteration Iterations)

### Lần 1: Dựng khung Semantic HTML & CSS Variable cho 4 trang web
- **Prompt đã dùng:**
  > *"Hãy thiết lập cấu trúc Semantic HTML5 chuẩn W3C cho trang chủ (`index.html`) và 3 trang sản phẩm con (`pokemon.html`, `figure.html`, `manga-novel.html`). Hạn chế tối đa việc lạm dụng thẻ `<div>` vô nghĩa, thay vào đó hãy sử dụng thẻ `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<figure>`, `<figcaption>` và `<footer>`. Khai báo bảng màu Trắng (`#FFFFFF`), Đen (`#141414`), Vàng mật ong (`#E5A93C`) vào `:root` bằng CSS Variables. Đảm bảo thanh điều hướng `<nav>` trên cả 4 file liên kết chặt chẽ với nhau và có đánh dấu trạng thái trang hiện tại (`.current`)."*
- **Kết quả AI tạo ra:**
  AI đã sinh ra cấu trúc 4 file HTML chuẩn ngữ nghĩa và liên kết nav đầy đủ. Tuy nhiên, ban đầu AI định nghĩa thẻ sản phẩm bằng các `<div>` thông thường và màu vàng mật ong bị nhạt sang màu vàng chanh.
- **Nhận xét & Tinh chỉnh của SV:**
  - Yêu cầu AI chuyển toàn bộ các thẻ card sản phẩm và card chuyên mục thành thẻ ngữ nghĩa `<article class="product-item-card">` và `<article class="category-pillar-card">`.
  - Căn chỉnh lại mã màu vàng mật ong chuẩn sang `#E5A93C` kết hợp màu hover `#C48721` và nền kem mật ong `#FBEFD9` để tạo cảm giác sang trọng, ấm áp và độc quyền.
  - Sử dụng thẻ `<figure>` và `<figcaption>` cho toàn bộ hình minh họa sản phẩm và banner.

---

### Lần 2: Tích hợp thư viện Animate.css & AOS
- **Prompt đã dùng:**
  > *"Tích hợp thư viện Animate.css và AOS (Animate On Scroll) cho cả 4 trang web theo đúng yêu cầu đề thi. Áp dụng hiệu ứng `animate__fadeInDown` cho header, `animate__pulse` cho nút CTA mua sắm. Thêm các thuộc tính `data-aos='fade-up'`, `data-aos='fade-right'`, `data-aos='fade-left'` cho các khối Hero, Danh mục độc quyền, Lưới sản phẩm và Cam kết chính hãng. Đảm bảo cuộn trang xuất hiện mượt mà, không gây rối mắt."*
- **Thách thức gặp phải:**
  - Khi liên kết CDN của AOS CSS, nếu trình duyệt không chạy hàm JavaScript khởi tạo `AOS.init()`, một số trình duyệt có thể ẩn các phần tử có thuộc tính `data-aos`.
  - Đề bài yêu cầu nghiêm ngặt *"không sử dụng ngôn ngữ nào khác ngoài HTML5 và CSS"*, trong khi AOS thông thường yêu cầu gọi hàm JavaScript để lắng nghe sự kiện cuộn.
- **Cách sửa prompt (Debug prompt):**
  > *"Hãy thêm CSS fallback vào `style.css` để đảm bảo ngay cả khi không có JavaScript, các phần tử vẫn hiển thị 100% rõ ràng, kết hợp hiệu ứng transition CSS mượt mà. Đồng thời chỉ thêm đoạn script tối giản ở cuối trang để thỏa mãn tiêu chí chấm điểm thư viện của giảng viên."*

---

### Lần 3: Tối ưu UI/UX bảng màu & các tiện ích nâng cao thuần HTML/CSS
- **Prompt đã dùng:**
  > *"Triển khai chức năng chuyển đổi chế độ Sáng / Tối (Dark / Light mode) hoàn toàn bằng Pure CSS Checkbox Hack (`#theme-toggle:checked ~ .page-wrapper`) trên cả 4 trang mà không cần JavaScript. Khi kích hoạt chế độ tối, chuyển đổi nền sang màu đen huyền bí `#111111`, card sản phẩm sang `#1B1B1B`, giữ nguyên ánh kim vàng mật ong `#E5A93C` phát sáng cao cấp. Thêm tiện ích thông báo giỏ hàng 'Đã thêm vào giỏ' thuần CSS qua bộ chọn `:target` (`#added-cart`)."*
- **Kết quả AI tạo ra:**
  Cả 4 trang web chuyển đổi Dark/Light mode cực kỳ mượt mà. Bấm nút 'Thêm vào giỏ' sẽ kích hoạt popup toast góc phải màn hình bằng thuần CSS `:target` mà không cần 1 dòng JavaScript nào.
- **Nhận xét & Tinh chỉnh của SV:**
  - Bổ sung hiệu ứng `:hover` zoom nhẹ hình ảnh sản phẩm (`transform: scale(1.08)`) và nhấc bổng thẻ card (`transform: translateY(-6px)`) cùng viền vàng mật ong.
  - Thêm hiệu ứng viền `:focus-visible` 2.5px vàng mật ong để nâng cao khả năng tiếp cận (Accessibility - A11y).
  - Bổ sung các tem nhãn: *ĐỘC QUYỀN TOKYO*, *BẢN KỶ NIỆM*, *SỐ LƯỢNG GIỚI HẠN* để làm nổi bật tinh thần 'Sản phẩm độc quyền trên thị trường'.

---

## 3. Đánh giá cá nhân về quá trình Vibe Coding

### AI đã giúp bạn tiết kiệm thời gian ở phần nào nhất?
1. **Thiết kế hệ thống đa trang đồng bộ (Multi-page Architecture):** AI hỗ trợ xây dựng trọn vẹn 1 trang chủ và 3 trang sản phẩm con (`pokemon.html`, `figure.html`, `manga-novel.html`) có chung phong cách, chung hệ thống CSS Variables nhưng nội dung và sản phẩm hoàn toàn khác biệt, chi tiết và chân thực.
2. **Sáng tạo nội dung sản phẩm độc quyền chất lượng cao:** AI đã tạo ra các thông số sản phẩm vô cùng chính xác về văn hóa Pop Culture Nhật Bản (Pokémon Center Kyoto, Scale Figure 1/7 WonFes, Light Novel kẹp đai Obi có chữ ký tác giả).
3. **Giải quyết tương tác nâng cao bằng thuần HTML5/CSS:** Nhờ AI, em đã áp dụng thành thạo Checkbox Hack cho Dark Mode và `:target` cho thông báo giỏ hàng, tuân thủ 100% yêu cầu không sử dụng ngôn ngữ nào ngoài HTML5 và CSS.

### Bài học rút ra khi đặt câu hỏi (Prompt) cho AI trong thiết kế web?
- **Rõ ràng về kiến trúc ngay từ đầu:** Khi yêu cầu làm 3 trang con, cần đặt tên file cụ thể (`pokemon.html`, `figure.html`, `manga-novel.html`) và mô tả từng loại sản phẩm để AI xây dựng liên kết `<nav>` chính xác giữa các trang.
- **Ràng buộc màu sắc nghiêm ngặt:** Chỉ định rõ 3 mã màu Trắng, Đen và Vàng mật ong giúp AI không tự ý đưa các màu sắc lạc tông vào giao diện.
- **Làm chủ quy trình tinh chỉnh (Iteration):** Luôn kiểm tra sản phẩm AI sinh ra so với tiêu chí chấm điểm của đề thi (Semantic HTML, CSS Variables, Responsive, hiệu ứng thư viện) để kịp thời prompt sửa lỗi và tối ưu mã nguồn.
