# REQUIREMENTS.md

# TÀI LIỆU PHÂN TÍCH YÊU CẦU PHẦN MỀM
## KTPMUD Hack Marathon 2026 – Track B: Vườn Toán Lớp 3

---

## 1. Giới thiệu

### 1.1. Mục đích tài liệu

Tài liệu này xác định các yêu cầu chức năng, yêu cầu phi chức năng, phạm vi và tiêu chí chấp nhận của việc mở rộng hệ thống Vườn Toán Lớp 3 với dạng bài luyện tập mới có tên **“Ước lượng trước khi tính đúng”**.

Tài liệu được sử dụng làm cơ sở cho các hoạt động:
- Phân tích yêu cầu phần mềm.
- Thiết kế giải pháp mở rộng hệ thống.
- Xây dựng và kiểm thử chức năng.
- Đánh giá mức độ hoàn thành sản phẩm.
- Bàn giao và phát triển hệ thống trong tương lai.

Các yêu cầu trong tài liệu phải được đối chiếu với đặc tả chính thức của starter repository tại `docs/architecture-reference.md`.

### 1.2. Thông tin dự án

| Thuộc tính | Nội dung |
|---|---|
| Tên dự án | Vườn Toán Lớp 3 |
| Cuộc thi | KTPMUD Hack Marathon 2026 |
| Track | Track B |
| Phiên bản starter | `bkt-2026-v1` |
| Stack công nghệ | Node.js 18+, Express, SQLite, JavaScript, HTML, CSS |
| Loại dự án | Mở rộng hệ thống phần mềm hiện có |
| Dạng bài mới | Ước lượng trước khi tính đúng |

### 1.3. Bối cảnh dự án

Hệ thống Vườn Toán Lớp 3 là một nền tảng hỗ trợ người học thực hành các phép toán cơ bản.

Trong phạm vi Hack Marathon 2026, nhóm phát triển cần bổ sung một dạng bài mới nhằm khuyến khích người học thực hiện bước ước lượng trước khi tính toán chính xác.

Thay vì chỉ đưa ra đáp án cuối cùng, người học cần:
1. Đọc câu hỏi toán học.
2. Đưa ra kết quả ước lượng hoặc khoảng giá trị hợp lý.
3. Thực hiện phép tính chính xác.
4. Nhận phản hồi về tính hợp lý của ước lượng và tính chính xác của phép tính.

Chức năng mới phải tích hợp vào luồng học tập hiện có, không được phát triển thành một ứng dụng độc lập.

---

## 2. Mục tiêu hệ thống

### 2.1. Mục tiêu chính

- Bổ sung dạng bài “Ước lượng trước khi tính đúng” vào hệ thống hiện có.
- Khuyến khích người học hình thành tư duy ước lượng trong toán học.
- Đảm bảo quy tắc tạo câu hỏi và chấm điểm có tính tất định.
- Đảm bảo kết quả được xử lý và lưu trữ ở phía server.
- Cung cấp phản hồi rõ ràng, dễ hiểu cho người học.
- Đảm bảo chức năng mới có thể kiểm thử và bảo trì.

### 2.2. Mục tiêu kỹ thuật

- Tích hợp với kiến trúc hiện có thay vì viết lại hệ thống.
- Tận dụng các API, cơ sở dữ liệu và luồng xử lý phù hợp đã có.
- Không làm ảnh hưởng đến các chức năng hiện tại.
- Bổ sung kiểm thử tự động và CI.
- Đảm bảo khả năng chạy lại dự án từ clean checkout.

---

## 3. Phạm vi dự án

### 3.1. Trong phạm vi

Dự án bao gồm các chức năng:

- Truy cập dạng bài mới từ luồng học hiện tại.
- Hiển thị câu hỏi phép nhân hoặc phép chia.
- Nhập kết quả ước lượng hoặc khoảng giá trị.
- Nhập kết quả tính chính xác.
- Kiểm tra và chấm kết quả.
- Hiển thị phản hồi.
- Lưu kết quả học tập.
- Khôi phục trạng thái đã lưu khi người học tải lại trang.
- Kiểm thử chức năng, dữ liệu và giao diện.

### 3.2. Ngoài phạm vi

Dự án không bao gồm:

- Xây dựng lại toàn bộ hệ thống Vườn Toán Lớp 3.
- Thêm chương trình Toán hoặc nội dung sách giáo khoa mới.
- Thay đổi cơ chế authentication hoặc authorization.
- Sửa hệ thống session.
- Thay đổi tài khoản mẫu.
- Thay đổi deployment.
- Kết nối với hệ thống production.
- Sử dụng dữ liệu học sinh hoặc giáo viên thật.
- Sử dụng LLM để sinh đáp án hoặc chấm điểm khi chương trình đang chạy.
- Triển khai hệ thống lên môi trường public như một yêu cầu bắt buộc.

---

## 4. Các bên liên quan và đối tượng sử dụng

### 4.1. Người học

Người học là đối tượng trực tiếp sử dụng dạng bài mới.

Nhu cầu:
- Dễ dàng truy cập bài tập.
- Hiểu rõ yêu cầu của câu hỏi.
- Có thể nhập kết quả ước lượng và kết quả chính xác.
- Nhận phản hồi rõ ràng.
- Tiếp tục bài học sau khi tải lại trang.

### 4.2. Nhóm phát triển

Nhóm phát triển chịu trách nhiệm:
- Phân tích yêu cầu.
- Thiết kế giải pháp mở rộng.
- Xây dựng chức năng.
- Kiểm thử và sửa lỗi.
- Bảo đảm an toàn dữ liệu.
- Viết tài liệu và bàn giao.

### 4.3. Người kiểm thử

Người kiểm thử chịu trách nhiệm:
- Kiểm tra chức năng theo acceptance criteria.
- Kiểm tra các trường hợp hợp lệ và không hợp lệ.
- Kiểm tra tính chính xác của scoring.
- Kiểm tra khả năng lưu và khôi phục dữ liệu.
- Kiểm tra khả năng sử dụng bằng bàn phím.

---

## 5. User Stories

### US-01: Truy cập bài luyện tập

Là người học, tôi muốn truy cập dạng bài “Ước lượng trước khi tính đúng” từ hệ thống học tập hiện tại để có thể luyện tập mà không phải chuyển sang một ứng dụng khác.

### US-02: Đưa ra kết quả ước lượng

Là người học, tôi muốn nhập kết quả ước lượng hoặc khoảng giá trị hợp lý trước khi thực hiện phép tính chính xác để rèn luyện khả năng ước lượng.

### US-03: Kiểm tra kết quả

Là người học, tôi muốn hệ thống đánh giá kết quả ước lượng và kết quả chính xác riêng biệt để biết mình đã hiểu bài đến đâu.

### US-04: Nhận phản hồi

Là người học, tôi muốn nhận phản hồi dễ hiểu sau khi nộp bài để biết kết quả của mình và hiểu cách cải thiện.

### US-05: Lưu tiến trình

Là người học, tôi muốn kết quả của mình được lưu lại để không bị mất tiến trình khi tải lại trang.

---

## 6. Yêu cầu chức năng

### FR-01: Truy cập dạng bài mới

**Mô tả:**

Hệ thống phải cung cấp khả năng truy cập dạng bài “Ước lượng trước khi tính đúng” từ luồng học hiện có.

**Điều kiện:**
- Người học đang sử dụng hệ thống hiện tại.
- Dạng bài mới được tích hợp vào luồng học hiện có.

**Kết quả mong đợi:**
- Người học truy cập được dạng bài.
- Chức năng không tồn tại dưới dạng trang demo độc lập.

**Tiêu chí kiểm chứng:**
- Kiểm tra đường dẫn hoặc thao tác truy cập trong luồng học hiện có.
- Kiểm tra chức năng sau khi khởi động hệ thống từ clean checkout.

### FR-02: Hiển thị câu hỏi

**Mô tả:**

Hệ thống phải hiển thị câu hỏi luyện tập sử dụng các phép nhân hoặc phép chia đã có trong chương trình.

**Yêu cầu:**
- Câu hỏi phải được tạo từ dữ liệu synthetic.
- Nội dung câu hỏi phải có thể tái lập.
- Câu hỏi phải có dữ liệu đáp án được xác định bằng code.
- Hệ thống phải có tối thiểu 12 fixture/câu hỏi synthetic.

**Tiêu chí kiểm chứng:**
- Kiểm tra số lượng fixture.
- Kiểm tra nội dung câu hỏi.
- Kiểm tra tính tái lập của dữ liệu.

### FR-03: Nhập kết quả ước lượng

**Mô tả:**

Hệ thống phải cho phép người học nhập kết quả ước lượng hoặc khoảng giá trị hợp lý trước khi thực hiện bước tính chính xác.

**Yêu cầu:**
- Có giao diện nhập kết quả ước lượng.
- Dữ liệu đầu vào được kiểm tra hợp lệ.
- Hệ thống không tiết lộ đáp án chính xác trước khi người học nộp bài.
- Quy tắc đánh giá ước lượng phải được mô tả rõ ràng.

**Tiêu chí kiểm chứng:**
- Kiểm tra khả năng nhập dữ liệu.
- Kiểm tra dữ liệu hợp lệ.
- Kiểm tra dữ liệu không hợp lệ.
- Kiểm tra API không trả đáp án trước khi nộp bài.

### FR-04: Nhập kết quả tính chính xác

**Mô tả:**

Hệ thống phải cho phép người học nhập kết quả tính toán chính xác sau bước ước lượng.

**Yêu cầu:**
- Người học có thể nhập đáp án chính xác.
- Dữ liệu đầu vào được kiểm tra hợp lệ.
- Đáp án chính xác được kiểm tra bằng quy tắc xác định trong code.
- Không sử dụng LLM làm nguồn đáp án.

**Tiêu chí kiểm chứng:**
- Kiểm tra đáp án đúng.
- Kiểm tra đáp án sai.
- Kiểm tra dữ liệu thiếu hoặc không hợp lệ.

### FR-05: Kiểm tra kết quả ước lượng

**Mô tả:**

Server phải kiểm tra tính hợp lý của kết quả ước lượng dựa trên quy tắc đã được nhóm xác định và công bố.

**Yêu cầu:**
- Quy tắc chấm ước lượng phải rõ ràng.
- Quy tắc chấm phải tất định.
- Cùng một đầu vào và dữ liệu câu hỏi phải tạo ra cùng một kết quả.
- Không sử dụng LLM để đánh giá kết quả.

**Tiêu chí kiểm chứng:**
- Kiểm tra các trường hợp ước lượng hợp lý.
- Kiểm tra các trường hợp ước lượng không hợp lý.
- Kiểm tra các trường hợp biên.
- Kiểm tra khả năng tái lập kết quả.

### FR-06: Chấm kết quả chính xác

**Mô tả:**

Server phải thực hiện kiểm tra đáp án chính xác của người học.

**Yêu cầu:**
- Việc chấm điểm phải được thực hiện phía server.
- Đáp án phải được xác định bằng code.
- Kết quả phải tất định.
- Không phụ thuộc vào LLM hoặc dịch vụ bên ngoài.

**Tiêu chí kiểm chứng:**
- Đáp án đúng được xác định chính xác.
- Đáp án sai được xác định chính xác.
- Client không thể tự quyết định kết quả chấm.

### FR-07: Hiển thị phản hồi

**Mô tả:**

Hệ thống phải hiển thị phản hồi sau khi người học nộp bài.

**Yêu cầu:**
- Phản hồi về ước lượng phải được phân biệt với phản hồi về kết quả chính xác.
- Nội dung phản hồi dễ hiểu.
- Thông báo không gây nhầm lẫn giữa hai loại kết quả.
- Không hiển thị đáp án chính xác trước khi nộp bài.

**Tiêu chí kiểm chứng:**
- Kiểm tra phản hồi khi ước lượng hợp lý.
- Kiểm tra phản hồi khi ước lượng không hợp lý.
- Kiểm tra phản hồi khi đáp án chính xác đúng.
- Kiểm tra phản hồi khi đáp án chính xác sai.

### FR-08: Lưu kết quả học tập

**Mô tả:**

Hệ thống phải lưu kết quả học tập của người học ở phía server.

**Yêu cầu:**
- Kết quả được lưu bằng cơ chế dữ liệu hiện có hoặc phần mở rộng phù hợp.
- Việc lưu dữ liệu phải tương thích với cơ sở dữ liệu SQLite hiện tại.
- Không lưu dữ liệu cá nhân thật.
- Kết quả phải được khôi phục khi tải lại trang.

**Tiêu chí kiểm chứng:**
- Kiểm tra dữ liệu sau khi nộp bài.
- Kiểm tra dữ liệu trong cơ sở dữ liệu.
- Tải lại trang và xác nhận kết quả vẫn còn.
- Kiểm tra lỗi khi lưu dữ liệu.

### FR-09: Xử lý dữ liệu đầu vào không hợp lệ

**Mô tả:**

Hệ thống phải xử lý các dữ liệu đầu vào không hợp lệ một cách an toàn.

Các trường hợp:
- Không nhập dữ liệu.
- Nhập sai định dạng.
- Nhập dữ liệu không thuộc miền giá trị cho phép.
- Gửi request thiếu trường bắt buộc.
- Gửi request có kiểu dữ liệu không đúng.

**Yêu cầu:**
- Không làm chương trình bị crash.
- Không lưu dữ liệu không hợp lệ.
- Trả thông báo lỗi phù hợp.
- Không tiết lộ thông tin nhạy cảm trong thông báo lỗi.

---

## 7. Yêu cầu phi chức năng

### NFR-01: Tính tất định

Quy tắc tạo câu hỏi, kiểm tra ước lượng và chấm đáp án phải tất định.

Với cùng dữ liệu đầu vào, hệ thống phải tạo ra cùng kết quả.

### NFR-02: Tính đúng đắn

Hệ thống phải đảm bảo kết quả chấm điểm phản ánh đúng quy tắc đã được nhóm xác định.

### NFR-03: Khả năng tích hợp

Chức năng mới phải tích hợp với luồng học, API và cơ sở dữ liệu hiện có.

Không được viết lại toàn bộ hệ thống.

### NFR-04: Khả năng bảo trì

- Code phải dễ đọc.
- Các chức năng phải có trách nhiệm rõ ràng.
- Tránh sao chép logic chấm điểm ở nhiều nơi.
- Quy tắc chấm phải được mô tả trong tài liệu.
- Các thay đổi phải dễ kiểm thử và bảo trì.

### NFR-05: Khả năng kiểm thử

- Các chức năng quan trọng phải có test tự động.
- Có test cho normal cases.
- Có test cho boundary cases.
- Có test cho invalid input.
- Có test cho scoring.

### NFR-06: Khả năng sử dụng

- Giao diện phải dễ hiểu với người học.
- Các thao tác chính phải sử dụng được bằng bàn phím.
- Các thông báo lỗi phải rõ ràng.
- Các trạng thái bài tập phải dễ nhận biết.

### NFR-07: Bảo mật và quyền riêng tư

- Không sử dụng dữ liệu học sinh hoặc giáo viên thật.
- Không chứa secret, token hoặc API key.
- Không kết nối production.
- Không thay đổi cơ chế authentication/session.
- Không ghi thông tin nhạy cảm vào log.

### NFR-08: Khả năng tái lập

Hệ thống phải có khả năng cài đặt, chạy và kiểm thử từ clean checkout theo hướng dẫn trong README.

### NFR-09: Tương thích môi trường

Hệ thống phải tương thích với stack công nghệ được quy định trong starter repository:
- Node.js 18 trở lên.
- Express.
- SQLite.
- JavaScript.
- HTML/CSS.

---

## 8. Acceptance Criteria

Các tiêu chí chấp nhận dưới đây được xây dựng theo yêu cầu bắt buộc của Track B trong đề thi.

| ID | Tiêu chí chấp nhận | Cách kiểm chứng |
|---|---|---|
| B-01 | Dạng bài mới truy cập được từ luồng học hiện có, không phải trang demo rời | Kiểm tra luồng học |
| B-02 | Có tối thiểu 12 fixture/câu hỏi synthetic tái lập được | Kiểm tra fixture và test |
| B-03 | Quy tắc tạo và chấm ước lượng được mô tả rõ, tất định và test được | Review tài liệu và test |
| B-04 | API không trả đáp án đúng trước khi người học nộp bài | Kiểm tra API response |
| B-05 | Server chấm và lưu kết quả; refresh không làm mất trạng thái đã lưu | Kiểm tra DB và refresh |
| B-06 | Có feedback phân biệt “ước lượng hợp lý” với “kết quả chính xác” | Kiểm tra giao diện |
| B-07 | Không sửa `server/auth.js`, session, tài khoản mẫu hoặc deployment | Code review |
| B-08 | Có test tự động cho normal, boundary, invalid input và scoring | Chạy test |
| B-09 | Bổ sung lệnh `npm test`; test đạt từ clean checkout | Chạy `npm test` |
| B-10 | CI chạy `npm ci` và `npm test` trên Pull Request | Kiểm tra GitHub Actions |
| B-11 | Không có PII/secret; chỉ dùng alias/tài khoản synthetic | Security review |
| B-12 | Giao diện dùng được bằng bàn phím cho luồng chính và có thông báo lỗi dễ hiểu | Kiểm thử UX/accessibility |

---

## 9. Yêu cầu kiểm thử

### 9.1. Kiểm thử chức năng

- Kiểm tra truy cập dạng bài.
- Kiểm tra hiển thị câu hỏi.
- Kiểm tra nhập kết quả ước lượng.
- Kiểm tra nhập đáp án chính xác.
- Kiểm tra chấm điểm.
- Kiểm tra phản hồi.
- Kiểm tra lưu kết quả.
- Kiểm tra khôi phục kết quả.

### 9.2. Kiểm thử normal cases

Các trường hợp đầu vào hợp lệ:
- Ước lượng hợp lý.
- Ước lượng không hợp lý.
- Đáp án chính xác đúng.
- Đáp án chính xác sai.
- Hoàn thành bài tập bình thường.

### 9.3. Kiểm thử boundary cases

- Giá trị ước lượng tại giới hạn cho phép.
- Giá trị gần giới hạn cho phép.
- Giá trị nằm sát ranh giới giữa hợp lý và không hợp lý theo quy tắc đã xác định.
- Giá trị nhỏ nhất hoặc lớn nhất trong miền dữ liệu câu hỏi.

### 9.4. Kiểm thử invalid input

- Dữ liệu bị thiếu.
- Dữ liệu sai kiểu.
- Dữ liệu không thuộc miền cho phép.
- Request không đầy đủ.
- Request có cấu trúc không hợp lệ.

### 9.5. Kiểm thử scoring

- Kết quả chấm đúng với quy tắc.
- Kết quả chấm tất định.
- Ước lượng và đáp án chính xác được đánh giá riêng biệt.
- Không thể thay đổi kết quả chấm chỉ bằng dữ liệu từ client.

### 9.6. Kiểm thử tích hợp

- Chức năng mới hoạt động trong luồng học hiện tại.
- API hoạt động với database hiện có.
- Dữ liệu được lưu và khôi phục.
- Không ảnh hưởng đến authentication/session.
- Không ảnh hưởng đến các chức năng cũ.

---

## 10. Traceability Matrix

Bảng này liên kết yêu cầu chức năng với acceptance criteria và kiểm thử.

| Requirement | Acceptance Criteria | Test |
|---|---|---|
| FR-01 | B-01 | Truy cập dạng bài |
| FR-02 | B-02 | Kiểm tra fixture |
| FR-03 | B-03, B-04 | Kiểm tra nhập ước lượng và API |
| FR-04 | B-03, B-08 | Kiểm tra nhập đáp án |
| FR-05 | B-03, B-08 | Kiểm tra scoring ước lượng |
| FR-06 | B-08 | Kiểm tra scoring chính xác |
| FR-07 | B-06 | Kiểm tra feedback |
| FR-08 | B-05 | Kiểm tra lưu và refresh |
| FR-09 | B-08, B-12 | Kiểm tra invalid input |

---

## 11. Giới hạn và giả định

### 11.1. Giới hạn

- Nhóm chỉ mở rộng một dạng bài.
- Phạm vi toán học giới hạn ở các phép nhân/chia đã có.
- Không thay đổi authentication/session.
- Không kết nối production.
- Không sử dụng dữ liệu thật.
- Không sử dụng LLM để sinh đáp án runtime.

### 11.2. Giả định

- Starter repository đã cung cấp hệ thống học hiện có.
- Các API và database hiện tại có thể được mở rộng theo kiến trúc được mô tả trong tài liệu chính thức.
- Người học sử dụng hệ thống thông qua giao diện hiện có.
- Các câu hỏi và dữ liệu kiểm thử sử dụng dữ liệu synthetic.
- Quy tắc chấm ước lượng sẽ được nhóm xác định, mô tả và kiểm chứng trong quá trình thiết kế.

---

## 12. Điều kiện hoàn thành

Chức năng được xem là hoàn thành khi:

1. Đáp ứng đầy đủ các acceptance criteria B-01 đến B-12.
2. Chức năng mới tích hợp vào luồng học hiện tại.
3. Server thực hiện scoring và lưu kết quả.
4. Có ít nhất 12 fixture/câu hỏi synthetic.
5. Có test tự động và lệnh `npm test`.
6. CI chạy test thành công trên Pull Request.
7. Không vi phạm các giới hạn về authentication, session, privacy và production.
8. Có tài liệu hướng dẫn cài đặt, chạy và kiểm thử.
9. Các thành viên trong nhóm có thể giải thích được yêu cầu và quyết định thiết kế.

---

## 13. Tài liệu tham khảo

1. KTPMUD Hack Marathon 2026 – Đề thi `KTPMUD-BKT-2026-PILOT`.
2. Starter repository: `fossbk-spec/ktpmud-bkt-vuontoan-starter`.
3. Starter tag: `bkt-2026-v1`.
4. Tài liệu đặc tả: `docs/architecture-reference.md`.
