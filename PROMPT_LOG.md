# NHẬT KÝ PROMPT ENGINEERING (VIBE CODING LOG)

- **Họ và tên:** Mai Huy Phong
- **MSSV:** 125000312
- **Tên đề tài Website:** Web giúp luyện tập và dò CV (CVCheckAI - Nền tảng luyện viết và rà soát lỗi hồ sơ xin việc chuẩn ATS)
- **Công cụ AI đã sử dụng:** Gemini 3.8 Flash (Google DeepMind Antigravity)

---

## 1. Yêu cầu ban đầu (System/Initial Prompt)

> *"Tôi muốn làm website với tiêu đề 'Web giúp luyện tập và dò CV' (CVCheckAI). Dựa trên yêu cầu của đề thi thiết kế web, sử dụng 2 ngôn ngữ chính là HTML5 và CSS3, tuyệt đối không dùng ngôn ngữ lập trình nào khác. Thiết kế giao diện chuyên nghiệp với bảng màu chỉ định gồm 4 mã màu: `#393E46` (xám đậm/than chì), `#00ADB5` (xanh mòng két chủ đạo), `#AAD8D3` (xanh bạc hà pastel dịu mắt), và `#EEEEEE` (nền sáng thanh lịch). Hệ thống phải đáp ứng chuẩn Semantic HTML5 (header, nav, main, section/article, footer), khai báo CSS Variables tại `:root`, áp dụng Flexbox/Grid responsive. Các tiện ích chính gồm: Trang chủ (giới thiệu tổng quan và số liệu), Cộng đồng (blog chia sẻ bí quyết viết CV và các bài đánh giá tích cực bằng tiếng Anh từ HR/Dev quốc tế), Giới thiệu (sứ mệnh, các thắc mắc thường gặp và giải pháp website đem lại), Sửa CV (gồm trang thông tin người dùng điền CV với 3 nút Lưu, Chỉnh sửa, Xóa; Chatbot AI phân tích CV cập nhật; gợi ý sửa lỗi CV trực quan). Thêm tiện ích chuyển đổi chế độ Sáng / Tối (Dark/Light mode) thuần CSS."*

---

## 2. Quá trình tinh chỉnh & Giải quyết sự cố (Iteration Iterations)

### Lần 1: Dựng khung Semantic HTML & CSS Variable
- **Prompt đã dùng:**
  > *"Hãy thiết lập cấu trúc Semantic HTML5 chuẩn W3C cho website Luyện tập & Dò CV. Hạn chế tối đa việc lạm dụng thẻ `<div>` vô nghĩa, thay vào đó hãy sử dụng thẻ `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>`, `<figure>`, `<time>`, `<details>`, `<summary>` và `<footer>`. Khai báo bảng màu `#393E46`, `#00ADB5`, `#AAD8D3`, `#EEEEEE` vào `:root` bằng CSS Variables. Xây dựng form thông tin người dùng điền CV có đủ các trường: Họ tên, Vị trí, Email, SĐT, Tóm tắt mục tiêu, Kinh nghiệm, Kỹ năng, Học vấn cùng 3 nút chức năng: 'Lưu', 'Chỉnh sửa', 'Xóa'."*
- **Kết quả AI tạo ra:**
  AI đã sinh ra khung layout đầy đủ các thẻ ngữ nghĩa và khai báo biến màu trong `:root`. Tuy nhiên, ban đầu AI vẫn bao bọc các khối card bằng nhiều thẻ `<div>` lồng nhau và các nút bấm chưa có trạng thái phản hồi trực quan.
- **Nhận xét & Tinh chỉnh của SV:**
  - Nhắc nhở AI thay thế các `<div>` bài viết và card đánh giá thành `<article class="blog-card">` và `<article class="review-card">`.
  - Sử dụng thẻ `<figure>` và `<figcaption>` cho hình minh họa hero section.
  - Tận dụng cơ chế thuần HTML5 `type="reset"` cho nút "Xóa" để xóa form tự nhiên mà không cần đến JavaScript.
  - Sử dụng CSS `:target` (với ID `#save-notification`) để hiển thị thông báo "Lưu thành công" một cách mượt mà và trực quan.

---

### Lần 2: Tích hợp thư viện Animate.css & AOS
- **Prompt đã dùng:**
  > *"Tích hợp thư viện Animate.css và AOS (Animate On Scroll) theo đúng yêu cầu đề bài. Áp dụng hiệu ứng `animate__fadeInDown` cho header, `animate__pulse` cho nút CTA chính. Thêm các thuộc tính `data-aos='fade-up'`, `data-aos='fade-right'`, `data-aos='fade-left'` cho các khối Hero, Features, Form CV, Chatbot AI và Blog cộng đồng. Đảm bảo giao diện cuộn trang xuất hiện sinh động nhưng mượt mà, không rối mắt."*
- **Thách thức gặp phải:**
  - Khi liên kết file CDN của thư viện AOS CSS, nếu trình duyệt tắt JavaScript hoặc khi trang web chưa kích hoạt hàm `AOS.init()`, một số trình duyệt có thể giữ trạng thái ẩn các phần tử có thuộc tính `data-aos`.
  - Đề bài yêu cầu nghiêm ngặt *"không sử dụng ngôn ngữ nào khác ngoài HTML5 và CSS"*, trong khi AOS thông thường yêu cầu gọi hàm JavaScript khởi tạo.
- **Cách sửa prompt (Debug prompt):**
  > *"Hãy cấu hình CSS dự phòng (fallback) để đảm bảo nếu không có JavaScript hoặc trước khi AOS khởi chạy, các phần tử vẫn hiển thị 100% rõ ràng, kết hợp cùng hiệu ứng keyframes CSS thuần mượt mà. Đồng thời chỉ thêm đoạn khởi tạo thư viện AOS tối giản ở cuối trang để thỏa mãn thang điểm chấm hiệu ứng thư viện của đề thi."*

---

### Lần 3: Tối ưu UI/UX bảng màu & các tiện ích nâng cao thuần HTML/CSS
- **Prompt đã dùng:**
  > *"Hoàn thiện chức năng chuyển đổi chế độ Sáng / Tối (Dark / Light mode) hoàn toàn bằng Pure CSS Checkbox Hack mà không cần JavaScript. Khi kích hoạt chế độ tối, chuyển đổi bảng màu sang nền tối dịu mắt (#222831, #2D333B) nhưng vẫn giữ nguyên tính nhận diện của bộ màu chủ đạo (#00ADB5, #AAD8D3). Đồng thời thiết kế giao diện Chatbot AI tương tác nhắm vào CV cập nhật, hộp gợi ý sửa lỗi trực quan (so sánh Before vs After) và bảng câu hỏi thường gặp (FAQ) dạng Accordion bằng thẻ HTML5 `<details>` và `<summary>`."*
- **Kết quả AI tạo ra:**
  Giao diện hoàn chỉnh với độ hoàn thiện mỹ thuật cao. Chế độ Dark mode hoạt động trơn tru chỉ với bộ chọn `#theme-toggle:checked ~ .site-wrapper`. Hộp chatbot AI thể hiện rõ ngữ cảnh phản hồi dựa trên thông tin ứng viên Mai Huy Phong và vị trí Frontend Developer.
- **Nhận xét & Tinh chỉnh của SV:**
  - Bổ sung hiệu ứng `:hover` nâng nhẹ thẻ card (`transform: translateY(-6px)`) và hiệu ứng `:focus-visible` đường viền xanh 2.5px để nâng cao trải nghiệm người dùng (UX) và khả năng tiếp cận (Accessibility - A11y).
  - Tinh chỉnh typography với font `Plus Jakarta Sans` giúp tiếng Việt hiển thị sắc nét, không bị lỗi dấu.

---

## 3. Đánh giá cá nhân về quá trình Vibe Coding

### AI đã giúp bạn tiết kiệm thời gian ở phần nào nhất?
1. **Thiết kế & phối màu CSS hiện đại:** AI hỗ trợ khai báo hệ thống CSS Variables một cách bài bản, đồng bộ toàn bộ bảng màu `#393E46`, `#00ADB5`, `#AAD8D3`, `#EEEEEE` cho cả hai chế độ Light và Dark mode chỉ trong thời gian rất ngắn.
2. **Soạn thảo nội dung chuyên ngành (Content Generation):** AI tạo ra các đoạn nội dung chất lượng cao về chuẩn ATS, công thức viết CV Google X-Y-Z, các câu gợi ý sửa lỗi thực tế và 4 bài đánh giá tích cực bằng tiếng Anh rất chuẩn mực từ góc nhìn của các nhà tuyển dụng công nghệ quốc tế.
3. **Giải quyết bài toán tương tác không dùng JS:** AI gợi ý giải pháp Pure CSS Checkbox Hack và `:target` selector cực kỳ thông minh, giúp trang web có đầy đủ tương tác sống động (Dark mode, thông báo Lưu, Accordion FAQ) mà vẫn tuân thủ 100% ràng buộc đề tài.

### Bài học rút ra khi đặt câu hỏi (Prompt) cho AI trong thiết kế web?
- **Đặt câu hỏi có cấu trúc và ràng buộc rõ ràng (Constraint-first Prompting):** Khi đưa ra yêu cầu về kỹ thuật (ví dụ Semantic HTML5, không dùng JavaScript, bộ mã màu cụ thể), cần nhấn mạnh ngay ở đầu prompt để AI không tự ý thêm các thư viện hay ngôn ngữ nằm ngoài phạm vi đề bài.
- **Tư duy tinh chỉnh theo từng bước (Iterative Refinement):** Không nên kỳ vọng AI tạo ra sản phẩm hoàn hảo ngay từ prompt đầu tiên. Cách tiếp cận hiệu quả nhất là chia nhỏ thành từng chặng: Khung HTML ngữ nghĩa $\rightarrow$ Định kiểu CSS Variables & Layout $\rightarrow$ Tích hợp hiệu ứng thư viện $\rightarrow$ Rà soát UX và sửa lỗi chi tiết.
- **Kiểm soát và làm chủ mã nguồn:** Sinh viên đóng vai trò là "Kiến trúc sư trưởng" (Code Architect) - luôn đọc hiểu, đối chiếu với tiêu chí chấm điểm của giảng viên để kịp thời chỉ đạo AI sửa đổi các thẻ sai lệch, đảm bảo sản phẩm cuối cùng đạt chất lượng cao nhất.
