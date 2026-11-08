# DECISIONS.md

# TÀI LIỆU QUYẾT ĐỊNH THIẾT KẾ
## Dự án: Vườn Toán Lớp 3 – Ước lượng trước khi tính đúng

**Phiên bản:** 1.0  
**Trạng thái:** Draft – cần đối chiếu với `docs/architecture-reference.md` trước khi triển khai  
**Phạm vi:** Track B – Vườn Toán Lớp 3

---

## 1. Mục đích tài liệu

Tài liệu này ghi lại các quyết định thiết kế quan trọng trong quá trình phát triển tính năng **“Ước lượng trước khi tính đúng”** cho hệ thống Vườn Toán Lớp 3.

Mục đích của tính năng là giúp học sinh hình thành khả năng ước lượng kết quả của phép nhân và phép chia trước khi thực hiện phép tính chính xác. Thay vì chỉ yêu cầu học sinh nhập đáp án đúng, hệ thống sẽ yêu cầu học sinh đưa ra một giá trị ước lượng hoặc một khoảng giá trị hợp lý, sau đó mới thực hiện phép tính chính xác.

Các quyết định được đưa ra nhằm bảo đảm tính năng:
- Phù hợp với luồng học tập hiện có của hệ thống.
- Có quy tắc tạo câu hỏi và chấm điểm rõ ràng, nhất quán.
- Không tiết lộ đáp án chính xác trước khi học sinh gửi bài.
- Lưu được kết quả học tập và duy trì dữ liệu sau khi tải lại trang.
- Có thể kiểm thử tự động, dễ bảo trì và không ảnh hưởng đến chức năng hiện có.

Tài liệu này cần được sử dụng cùng với `REQUIREMENTS.md`, `TEST_PLAN.md` và tài liệu kiến trúc `docs/architecture-reference.md`.

## 2. Nguyên tắc ra quyết định

Nhóm sử dụng các nguyên tắc sau khi lựa chọn giải pháp:

1. **Ưu tiên tích hợp:** Tính năng mới phải được tích hợp vào luồng học tập hiện có, không xây dựng thành một ứng dụng hoặc trang demo độc lập.
2. **Đơn giản và phù hợp lứa tuổi:** Giao diện, nội dung câu hỏi và cách phản hồi cần dễ hiểu đối với học sinh lớp 3.
3. **Tính xác định:** Cùng một dữ liệu đầu vào và cùng một quy tắc chấm điểm phải tạo ra cùng một kết quả.
4. **Xử lý phía máy chủ:** Máy chủ chịu trách nhiệm kiểm tra dữ liệu, tính điểm và lưu kết quả.
5. **Bảo vệ đáp án:** Không gửi đáp án chính xác về trình duyệt trước khi học sinh hoàn thành và gửi câu trả lời.
6. **Bảo vệ dữ liệu:** Chỉ sử dụng dữ liệu giả lập, không thu thập thông tin cá nhân thật của học sinh.
7. **Không phá vỡ hệ thống:** Không chỉnh sửa `server/auth.js`, cơ chế session, tài khoản mẫu hoặc cấu hình triển khai hiện có.

## 3. Danh sách quyết định thiết kế

### DEC-01: Tích hợp tính năng vào luồng học tập hiện có

**Bối cảnh:**

Đề bài yêu cầu tính năng ước lượng phải xuất hiện trong luồng học tập hiện tại của Vườn Toán Lớp 3. Nếu xây dựng một trang riêng không liên kết với hệ thống, tính năng sẽ không đáp ứng yêu cầu tích hợp.

**Quyết định:**

Nhóm lựa chọn tích hợp bài tập ước lượng vào giao diện và luồng điều hướng học tập hiện có. Học sinh có thể truy cập bài tập từ khu vực học tập phù hợp mà không cần tạo một hệ thống đăng nhập hoặc ứng dụng mới.

**Lý do lựa chọn:**
- Đáp ứng tiêu chí B-01.
- Giữ trải nghiệm sử dụng thống nhất.
- Hạn chế việc tạo thêm các thành phần trùng lặp.
- Giảm ảnh hưởng đến các chức năng sẵn có.

**Ảnh hưởng:**

Cần kiểm tra cấu trúc giao diện và cách điều hướng hiện tại trong tài liệu kiến trúc trước khi xác định chính xác vị trí tích hợp.

**Yêu cầu liên quan:** B-01.

### DEC-02: Sử dụng bộ câu hỏi giả lập có thể tái lập

**Bối cảnh:**

Đề bài yêu cầu có tối thiểu 12 bộ dữ liệu/câu hỏi giả lập có thể tái lập để phục vụ kiểm thử và trình diễn. Việc tạo câu hỏi hoàn toàn ngẫu nhiên có thể gây khó khăn khi so sánh kết quả giữa các lần kiểm thử.

**Quyết định:**

Nhóm sử dụng một bộ dữ liệu câu hỏi được xác định trước, có mã định danh và thông tin đầu vào rõ ràng. Bộ dữ liệu bao gồm các bài toán nhân và chia phù hợp với phạm vi kiến thức lớp 3.

Mỗi câu hỏi cần có các thông tin phục vụ việc tạo bài tập và chấm điểm, chẳng hạn:
- Mã câu hỏi.
- Phép tính hoặc dữ liệu đầu vào.
- Phép toán cần thực hiện.
- Giá trị hoặc khoảng ước lượng được chấp nhận.
- Đáp án chính xác dùng cho bước kiểm tra kết quả.
- Thông tin giải thích hoặc phản hồi sau khi nộp bài.

**Lý do lựa chọn:**
- Đáp ứng yêu cầu tối thiểu 12 câu hỏi.
- Kết quả kiểm thử có thể lặp lại.
- Dễ kiểm tra các trường hợp thông thường và trường hợp biên.
- Hạn chế tình trạng dữ liệu thay đổi khiến kết quả kiểm thử không ổn định.

**Ảnh hưởng:**

Bộ câu hỏi phải được quản lý tập trung để tránh việc quy tắc chấm điểm ở giao diện và máy chủ không thống nhất.

**Yêu cầu liên quan:** B-02, B-03, B-08.

### DEC-03: Sử dụng quy tắc ước lượng và chấm điểm xác định

**Bối cảnh:**

Học sinh cần ước lượng kết quả trước khi thực hiện phép tính chính xác. Nếu không có quy tắc đánh giá cụ thể, hệ thống có thể đưa ra kết quả không nhất quán.

**Quyết định:**

Nhóm lựa chọn phương pháp chấm điểm dựa trên các quy tắc toán học được xác định trước, không sử dụng mô hình ngôn ngữ lớn (LLM) để đánh giá câu trả lời.

Hệ thống phân biệt hai nội dung:
- **Đánh giá ước lượng:** Xác định câu trả lời ước lượng có nằm trong khoảng giá trị hợp lý đã được quy định hay không.
- **Đánh giá phép tính chính xác:** Xác định kết quả tính chính xác của học sinh có trùng với đáp án đúng hay không.

Một câu trả lời có thể có ước lượng hợp lý nhưng kết quả tính chính xác chưa đúng. Vì vậy, hệ thống cần phản hồi riêng cho từng phần thay vì gộp thành một kết quả đúng/sai duy nhất.

**Quy tắc cơ bản:**

Với một phép tính có kết quả chính xác là \(R\), nhóm xác định một khoảng ước lượng hợp lý:

\[
[L,U]
\]

Trong đó:
- \(L\): Cận dưới của khoảng ước lượng.
- \(U\): Cận trên của khoảng ước lượng.
- \(R\): Kết quả chính xác của phép tính.

Câu trả lời ước lượng \(E\) được chấp nhận khi:

\[
L \leq E \leq U
\]

Câu trả lời chính xác \(A\) được chấp nhận khi:

\[
A=R
\]

Các giá trị \(L\), \(U\) và \(R\) được xác định từ dữ liệu câu hỏi và quy tắc tạo bài tập. Nhóm cần kiểm tra để bảo đảm khoảng ước lượng thực sự phù hợp với từng phép tính, không quá rộng khiến mọi câu trả lời đều được chấp nhận.

**Lý do lựa chọn:**
- Kết quả có thể dự đoán và kiểm thử.
- Không phụ thuộc vào dịch vụ AI bên ngoài.
- Dễ giải thích cho học sinh và ban giám khảo.
- Phân biệt được năng lực ước lượng và năng lực tính toán chính xác.

**Ảnh hưởng:**

Quy tắc chấm điểm phải được triển khai thống nhất ở phía máy chủ. Phía giao diện chỉ hiển thị câu hỏi, nhận dữ liệu và trình bày phản hồi.

**Yêu cầu liên quan:** B-03, B-06, B-08.

### DEC-04: Không cung cấp đáp án chính xác trước khi học sinh nộp bài

**Bối cảnh:**

Nếu API gửi đáp án chính xác về trình duyệt ngay khi tải câu hỏi, học sinh có thể xem được đáp án trước khi hoàn thành bài tập thông qua dữ liệu mạng hoặc mã nguồn phía trình duyệt.

**Quyết định:**

Nhóm lựa chọn tách dữ liệu hiển thị câu hỏi khỏi dữ liệu dùng để chấm điểm.

Trước khi học sinh gửi câu trả lời, API chỉ trả về các thông tin cần thiết để hiển thị câu hỏi và hướng dẫn làm bài. Đáp án chính xác và dữ liệu nội bộ phục vụ chấm điểm không được đưa vào phản hồi này.

Sau khi học sinh gửi câu trả lời, máy chủ mới thực hiện kiểm tra và trả về kết quả cùng phản hồi phù hợp.

**Lý do lựa chọn:**
- Bảo đảm tính công bằng của bài tập.
- Hạn chế việc học sinh lấy đáp án từ dữ liệu trả về của API.
- Đáp ứng yêu cầu bảo vệ đáp án của đề bài.

**Ảnh hưởng:**

Cần kiểm tra cả nội dung phản hồi API, không chỉ kiểm tra giao diện có ẩn đáp án hay không.

**Yêu cầu liên quan:** B-04, B-08.

### DEC-05: Máy chủ chịu trách nhiệm chấm điểm và lưu kết quả

**Bối cảnh:**

Nếu chỉ lưu kết quả ở trình duyệt, dữ liệu có thể bị mất khi tải lại trang hoặc thay đổi thiết bị. Ngoài ra, việc chấm điểm hoàn toàn ở phía giao diện có thể khiến kết quả dễ bị thay đổi.

**Quyết định:**

Nhóm lựa chọn để máy chủ thực hiện việc kiểm tra câu trả lời, tính kết quả và lưu trạng thái bài làm vào cơ sở dữ liệu hiện có của hệ thống.

Khi học sinh hoàn thành bài tập:
1. Trình duyệt gửi câu trả lời đến máy chủ.
2. Máy chủ kiểm tra tính hợp lệ của dữ liệu.
3. Máy chủ đối chiếu câu trả lời với quy tắc chấm điểm.
4. Máy chủ lưu kết quả.
5. Máy chủ trả về phản hồi để giao diện hiển thị.

Khi người dùng tải lại trang, hệ thống cần có khả năng truy xuất trạng thái đã lưu theo cơ chế dữ liệu và nhận diện người dùng hiện có của dự án.

**Lý do lựa chọn:**
- Đáp ứng yêu cầu lưu kết quả phía máy chủ.
- Bảo đảm tính nhất quán của kết quả.
- Hạn chế mất dữ liệu khi tải lại trang.
- Tạo cơ sở để mở rộng thống kê kết quả học tập sau này.

**Ảnh hưởng:**

Cấu trúc lưu trữ và cách liên kết kết quả với người dùng phải tuân theo kiến trúc hiện có. Không tự ý thay đổi hệ thống xác thực hoặc session.

**Yêu cầu liên quan:** B-05, B-07.

### DEC-06: Sử dụng kiến trúc và công nghệ hiện có của dự án

**Bối cảnh:**

Tính năng mới cần được phát triển trong starter repository của cuộc thi. Việc thay đổi công nghệ hoặc xây dựng lại toàn bộ kiến trúc sẽ làm tăng thời gian triển khai và rủi ro ảnh hưởng đến hệ thống.

**Quyết định:**

Nhóm tiếp tục sử dụng các công nghệ được yêu cầu trong đề bài:
- Node.js phiên bản 18 trở lên.
- Express cho phía máy chủ.
- SQLite cho lưu trữ dữ liệu.
- JavaScript, HTML và CSS cho phần giao diện.

Nhóm ưu tiên tái sử dụng cấu trúc thư mục, quy ước API, cách truy cập cơ sở dữ liệu và các thành phần giao diện hiện có.

**Lý do lựa chọn:**
- Phù hợp với starter repository.
- Hạn chế cài đặt thêm công nghệ không cần thiết.
- Dễ tích hợp và kiểm thử.
- Giảm rủi ro ảnh hưởng đến các chức năng khác.

**Ảnh hưởng:**

Tên bảng, cấu trúc dữ liệu, endpoint và cách tổ chức module phải được xác định sau khi đọc `docs/architecture-reference.md`, không được tự ý tạo ra cấu trúc xung đột với hệ thống hiện có.

**Yêu cầu liên quan:** B-01, B-05, B-09.

### DEC-07: Bảo vệ hệ thống xác thực và dữ liệu người dùng

**Bối cảnh:**

Tính năng mới cần hoạt động cùng hệ thống hiện có nhưng không được làm thay đổi cơ chế xác thực, session hoặc tài khoản mẫu.

**Quyết định:**

Nhóm không chỉnh sửa:
- `server/auth.js`.
- Cơ chế session hiện tại.
- Tài khoản mẫu.
- Cấu hình triển khai hiện có.

Đối với dữ liệu kiểm thử và trình diễn, nhóm chỉ sử dụng dữ liệu giả lập và tên đại diện tổng hợp. Không đưa thông tin cá nhân thật của học sinh, giáo viên hoặc người dùng vào mã nguồn, dữ liệu mẫu hay báo cáo.

**Lý do lựa chọn:**
- Hạn chế nguy cơ phát sinh lỗi xác thực.
- Bảo vệ dữ liệu người dùng.
- Đáp ứng yêu cầu bảo mật và quyền riêng tư của cuộc thi.

**Yêu cầu liên quan:** B-07, B-11.

### DEC-08: Kiểm thử tự động kết hợp kiểm thử thủ công

**Bối cảnh:**

Một số yêu cầu có thể kiểm tra bằng unit test hoặc integration test, trong khi các yêu cầu về trải nghiệm học tập, điều hướng và khả năng sử dụng bàn phím cần được kiểm tra trực tiếp trên giao diện.

**Quyết định:**

Nhóm sử dụng kết hợp:
- Kiểm thử tự động cho quy tắc ước lượng, chấm điểm, kiểm tra dữ liệu đầu vào và xử lý API.
- Kiểm thử tích hợp cho việc lưu và truy xuất kết quả.
- Kiểm thử thủ công cho luồng học tập, giao diện, bàn phím và thông báo lỗi.
- CI để tự động chạy kiểm thử khi có Pull Request.

Lệnh kiểm thử chính thức cần được tích hợp vào `npm test` và phải chạy được sau khi cài đặt sạch bằng `npm ci`.

**Lý do lựa chọn:**
- Phát hiện lỗi sớm.
- Có thể kiểm tra lại sau mỗi lần thay đổi.
- Đáp ứng yêu cầu kiểm thử và tích hợp liên tục.
- Bảo đảm khả năng bàn giao dự án.

**Yêu cầu liên quan:** B-08, B-09, B-10, B-12.

---

## 4. Các quyết định cần xác nhận sau khi đọc tài liệu kiến trúc

Trước khi triển khai chính thức, nhóm cần đối chiếu các nội dung dưới đây với `docs/architecture-reference.md` và source code hiện có:

| Nội dung | Việc cần xác nhận |
|---|---|
| Luồng giao diện | Vị trí phù hợp để tích hợp bài tập mới |
| API | Quy ước endpoint, phương thức HTTP và định dạng JSON |
| Cơ sở dữ liệu | Bảng hiện có, cách tạo migration và lưu kết quả |
| Người dùng/session | Cách xác định người dùng hiện tại mà không sửa auth |
| Cấu trúc mã nguồn | Vị trí đặt module, route, service và test |
| Kiểm thử | Công cụ test, cách chạy và quy ước đặt test |
| CI | Cấu hình GitHub Actions hiện có hoặc vị trí tạo workflow |

Những nội dung này chỉ được xem là đã chốt sau khi nhóm kiểm tra trực tiếp tài liệu kiến trúc và mã nguồn.

## 5. Quản lý thay đổi quyết định

Nếu trong quá trình triển khai nhóm thay đổi một quyết định đã ghi trong tài liệu, cần cập nhật lại nội dung tương ứng.

Mỗi thay đổi cần nêu rõ:
- Quyết định cũ.
- Quyết định mới.
- Lý do thay đổi.
- Ảnh hưởng đến yêu cầu, mã nguồn và kiểm thử.

Mọi thay đổi quan trọng cần được các thành viên liên quan xem xét trước khi hợp nhất vào nhánh chính.

## 6. Kết luận

Các quyết định thiết kế trên định hướng việc xây dựng tính năng “Ước lượng trước khi tính đúng” theo hướng đơn giản, có thể kiểm thử, bảo đảm tính chính xác và phù hợp với hệ thống Vườn Toán Lớp 3 hiện có.

Nhóm ưu tiên tích hợp thay vì xây dựng độc lập, sử dụng quy tắc chấm điểm xác định thay vì AI, xử lý và lưu kết quả ở phía máy chủ, đồng thời bảo vệ hệ thống xác thực và dữ liệu người dùng.

Đây là cơ sở để nhóm triển khai MVP, xây dựng bộ kiểm thử và đánh giá mức độ đáp ứng các tiêu chí của cuộc thi.
