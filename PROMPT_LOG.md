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

### Lần 4: Khắc phục lỗi chữ menu bị xuống dòng & Tự động đồng bộ Dark Mode đa trang
- **Prompt đã dùng:**
  > *"Sửa lại 2 lỗi quan trọng: 1) Toàn bộ các văn bản của thanh menu điều hướng phải nằm trên cùng một hàng ngang với nhau, không được ngắt làm 2 dòng gây mất thẩm mỹ. 2) Chế độ Sáng / Tối phải được lưu và đồng bộ tự động giữa tất cả 4 trang web (Trang chủ, Pokemon, Figure, Manga/Novel) để khi người dùng chuyển sang trang con khác thì giao diện vẫn giữ nguyên chế độ tối/sáng mà không phải chỉnh lại."*
- **Thách thức gặp phải:**
  - Tiêu đề các mục menu dài ("Pokémon Độc Quyền", "Mô Hình Figure", "Light Novel & Manga") kèm icon bị ngắt dòng do giới hạn chiều rộng và thiếu thuộc tính `white-space: nowrap`.
  - Giữa các file HTML riêng biệt (`index.html`, `pokemon.html`, `figure.html`, `manga-novel.html`), trình duyệt mặc định nạp lại tài liệu mới khiến trạng thái checkbox `:checked` bị reset về mặc định nếu không lưu trữ trạng thái.
- **Cách sửa prompt (Debug prompt):**
  - Thêm `white-space: nowrap` vào `.nav-item-link` và `.nav-links`, tinh chỉnh kích thước logo và padding các phần tử để hàng menu trải dài thẳng tắp, cân đối hoàn hảo trên mọi kích thước màn hình.
  - Bổ sung cơ chế đồng bộ tức thì qua thuộc tính `html[data-theme="dark"]` kết hợp `localStorage.getItem('honeyvault_theme')` được thực thi ngay trong `<head>` để trang mới mở ra đã ở chế độ tối ngay lập tức mà không hề bị chớp giật màn hình (zero flicker).

### Lần 5: Khắc phục lỗi chữ logo bị chìm màu Dark Mode & mở rộng khung chống tràn viền toàn diện
- **Prompt đã dùng:**
  > *"1) Sửa lại chữ logo HONEY khi chuyển sang chế độ tối (Dark Mode) phải đọc được rõ ràng, không được để màu đen tàng hình trên nền đen. 2) Sửa lại tất cả các văn bản bị tràn khỏi khung viền trên toàn bộ website (đặc biệt là các khung nhãn 'POKÉMON CENTER JAPAN', 'BẢN ĐẶC BIỆT KÈM OBI', '100% ĐỘC QUYỀN' trong hình minh họa và thẻ card), đồng thời tăng kích thước chữ và khung viền cho thông thoáng, dễ đọc."*
- **Thách thức gặp phải:**
  - Thẻ `<img>` nạp file SVG từ bên ngoài không nhận thuộc tính CSS Dark Mode từ tài liệu chính, dẫn đến chữ `HONEY` giữ nguyên màu `#141414` bị chìm hoàn toàn vào nền đen header.
  - Các khung hình chữ nhật chứa nhãn trong SVG (`hero-banner.svg`, `pokemon-thumb.svg`) có chiều rộng cố định quá hẹp so với độ dài của chuỗi văn bản font in hoa 900, làm chữ tràn ra ngoài 2 cạnh khung.
- **Cách sửa prompt (Debug prompt):**
  - Chuyển logo thương hiệu sang dạng SVG Inline tích hợp trực tiếp trên Header của cả 4 trang, gán class `.logo-honey-word` chuyển sang màu trắng `#FFFFFF` sắc nét khi bật Dark Mode.
  - Mở rộng chiều rộng tất cả các khung viền (từ 150px lên 250px cho pill Pokemon, từ 145px lên 185px cho pill Limited, từ 150px lên 195px cho pill Độc quyền), tăng kích thước chữ hiển thị lớn hơn và bổ sung padding rộng rãi để văn bản nằm trọn vẹn 100% bên trong khung.

### Lần 6: Tăng kích thước cột bên phải và hình minh họa Hero to ngang bằng với cột bên trái
- **Prompt đã dùng:**
  > *"Cho cái bên phải to lên bằng với cột bên trái đi."*
- **Thách thức gặp phải:**
  - Cột bên trái có khối lượng nội dung lớn (Pill độc quyền + Tiêu đề H1 3 dòng lớn + Đoạn văn mô tả + 2 nút CTA + Thanh thống kê 3 chỉ số), trong khi cột bên phải chỉ chứa ảnh minh họa ở tỉ lệ cột hẹp `0.85fr` khiến khung hình bị nhỏ và để lại nhiều khoảng trống màu đen phía trên và phía dưới.
- **Cách sửa prompt (Debug prompt):**
  - Điều chỉnh tỉ lệ CSS Grid `.hero-grid` thành `1fr 1fr` (chia đều 50-50 hoàn hảo), mở rộng kích thước ảnh `.hero-figure-wrap img` lên `max-width: 680px` và chiều cao tối thiểu `min-height: 480px`.
  - Nâng cấp file `assets/hero-banner.svg` sang kích thước `viewBox="0 0 620 540"`, mở rộng bục trưng bày hoàng gia, phóng lớn mô hình Scale Figure trung tâm, hộp thẻ bài Pokémon TCG và boxset Light Novel Obi, tạo nên sự cân xứng thị giác hoàn hảo giữa 2 cột.

---

### Lần 7: Chuẩn hóa kích thước web thông thường, chính tả & tính năng lấy ảnh / xem thông số
- **Prompt đã dùng:**
  > *"Chỉnh lại kích thước website về với cơ bản của các trang web thông thường. Kiểm tra lại chính tả của toàn bộ web, và các thuật ngữ đúng chuyên ngành. Cho phép truy cập vào các trang để lấy ảnh và thông tin của các sản phẩm hiện có."*
- **Thách thức gặp phải:**
  - Container 1360px và H1 3.1rem quá to so với màn hình máy tính thông dụng 1080p, làm giao diện bị phóng đại quá mức.
  - Một số chữ trong SVG bị đứt đuôi (như 'BẢN ĐẶC BIỆT KÈM OB' thiếu chữ I).
  - Chưa có cơ chế cho người dùng xem ảnh phóng to, tải ảnh gốc sản phẩm về máy và tra cứu bảng thông số kỹ thuật chi tiết của từng vật phẩm.
- **Cách sửa prompt (Debug prompt):**
  - Đưa `.container` về chuẩn `max-width: 1200px`, hạ H1 xuống `2.35rem`, H2 xuống `2.0rem`, ảnh hero về `max-width: 480px` hài hòa.
  - Sửa triệt để lỗi chính tả trong `hero-banner.svg` thành `BẢN ĐẶC BIỆT KÈM OBI` với đủ chữ `I` và căn giữa chuẩn mực.
  - Xây dựng hệ thống Popup Modal thuần CSS `:target` (`.product-modal-backdrop:target`) trên cả 4 trang HTML, trang bị nút `📥 Tải Ảnh Gốc (SVG)` (`<a href="..." download>`) và `🔍 Mở Ảnh Tab Mới`, kèm bảng thông số kỹ thuật nội địa Nhật chuẩn xác từng chi tiết (Mã SKU, Hãng chế tác, Tình trạng seal, Kích thước, Tem kiểm định 7 màu, v.v.).

---

### Lần 8: Bỏ nút 'Săn đồ độc quyền' chống tràn mép & Cân bằng bố cục toàn website
- **Prompt đã dùng:**
  > *"Bỏ cái săn đồ độc quyền đi, sửa lại web sao cho cân bằng website."*
- **Thách thức gặp phải:**
  - Nút 'Săn Đồ Độc Quyền' trên Header chiếm khoảng 180px bề ngang, khi kết hợp với Logo thương hiệu (340px) và 4 mục menu (520px) khiến tổng chiều rộng Header vượt quá không gian hiển thị trên màn hình laptop thông thường, làm nút bị tràn mép phải màn hình và bị cắt cụt chữ.
  - Trên các trang sản phẩm con, 6 sản phẩm hiển thị trên lưới 4 cột dẫn đến hàng 1 có 4 sản phẩm còn hàng 2 chỉ có 2 sản phẩm, tạo ra khoảng trống hụt hẫng (bất đối xứng thị giác).
- **Cách sửa prompt (Debug prompt):**
  - Xóa bỏ nút 'Săn Đồ Độc Quyền' (và các nút CTA thừa trên Header ở cả 4 file HTML), chỉ giữ lại nút đổi giao diện Sáng / Tối.
  - Tái cấu trúc Flexbox Header với tỷ lệ 3 phần hoàn mỹ: `.brand-box` (`flex: 1` căn trái), `nav.main-nav` (`flex: 0 0 auto` đặt ngay chính giữa trọng tâm website), `.header-right-tools` (`flex: 1` căn phải). Header thông thoáng 100%, không bao giờ bị tràn mép.
  - Xây dựng lưới `.products-grid-3` với 3 cột đều đặn cho các trang sản phẩm con: 6 sản phẩm chia đều thành 2 hàng &times; 3 cột, tạo nên bố cục cân bằng, đối xứng và chuyên nghiệp chuẩn mực.

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
