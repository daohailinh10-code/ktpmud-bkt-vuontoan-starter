# TEST_PLAN.md

# KẾ HOẠCH KIỂM THỬ
## Dự án: Vườn Toán Lớp 3 – Ước lượng trước khi tính đúng

**Phiên bản:** 1.0  
**Trạng thái:** Kế hoạch kiểm thử  
**Phạm vi:** Track B – Vườn Toán Lớp 3

---

## 1. Mục đích

Tài liệu này mô tả kế hoạch kiểm thử cho tính năng **“Ước lượng trước khi tính đúng”** được phát triển trong hệ thống Vườn Toán Lớp 3.

Mục tiêu kiểm thử là xác nhận tính năng hoạt động đúng theo yêu cầu, bảo đảm học sinh có thể:
- Truy cập bài tập từ luồng học tập hiện có.
- Đưa ra ước lượng trước khi thực hiện phép tính chính xác.
- Nhận phản hồi riêng biệt về kết quả ước lượng và kết quả tính toán.
- Gửi câu trả lời và lưu kết quả trên máy chủ.
- Xem lại trạng thái đã lưu sau khi tải lại trang.

Ngoài ra, kế hoạch kiểm thử tập trung vào tính ổn định của API, độ chính xác của quy tắc chấm điểm, khả năng xử lý dữ liệu không hợp lệ, bảo mật dữ liệu và khả năng truy cập bằng bàn phím.

## 2. Phạm vi kiểm thử

### 2.1. Nội dung nằm trong phạm vi

| Nhóm kiểm thử | Nội dung |
|---|---|
| Giao diện | Truy cập bài tập, hiển thị câu hỏi, nhập câu trả lời và phản hồi |
| Tạo câu hỏi | Kiểm tra bộ câu hỏi giả lập và dữ liệu được cung cấp |
| Ước lượng | Kiểm tra khoảng ước lượng và quy tắc chấp nhận |
| Chấm điểm | Kiểm tra kết quả ước lượng và phép tính chính xác |
| API | Kiểm tra dữ liệu gửi lên, dữ liệu trả về và xử lý lỗi |
| Cơ sở dữ liệu | Kiểm tra lưu và truy xuất kết quả |
| Tích hợp | Kiểm tra tính năng trong luồng học tập hiện có |
| Bảo mật | Kiểm tra việc không tiết lộ đáp án và không sử dụng dữ liệu cá nhân thật |
| Khả năng truy cập | Kiểm tra thao tác bằng bàn phím và thông báo lỗi |
| CI | Kiểm tra khả năng cài đặt và chạy test tự động |

### 2.2. Nội dung ngoài phạm vi

Các nội dung sau không thuộc phạm vi kiểm thử của tính năng trong phiên bản này:
- Xây dựng chương trình học hoặc giáo trình mới.
- Thay đổi hệ thống xác thực và session.
- Thay đổi tài khoản mẫu.
- Tích hợp dữ liệu học sinh hoặc giáo viên thật.
- Sử dụng mô hình ngôn ngữ lớn để chấm điểm.
- Kiểm thử hệ thống triển khai production mới.

## 3. Chiến lược kiểm thử

Nhóm sử dụng kết hợp kiểm thử tự động và kiểm thử thủ công.

### 3.1. Unit Testing – Kiểm thử đơn vị

Kiểm tra từng thành phần xử lý riêng biệt, tập trung vào:
- Quy tắc tạo hoặc xác định khoảng ước lượng.
- Hàm kiểm tra câu trả lời ước lượng.
- Hàm kiểm tra đáp án chính xác.
- Hàm kiểm tra dữ liệu đầu vào.
- Hàm tạo phản hồi cho học sinh.

Mục tiêu là bảo đảm mỗi hàm thực hiện đúng chức năng và cho kết quả ổn định với cùng một đầu vào.

### 3.2. Integration Testing – Kiểm thử tích hợp

Kiểm tra sự phối hợp giữa các thành phần:
- Giao diện và API.
- API và phần xử lý nghiệp vụ.
- Phần xử lý nghiệp vụ và SQLite.
- Quá trình gửi bài, chấm điểm và lưu kết quả.
- Quá trình truy xuất kết quả đã lưu.

Mục tiêu là bảo đảm các thành phần hoạt động đúng khi kết hợp với nhau.

### 3.3. UI/Manual Testing – Kiểm thử giao diện và thủ công

Kiểm tra trực tiếp trên trình duyệt:
- Khả năng truy cập bài tập.
- Cách hiển thị câu hỏi và hướng dẫn.
- Thao tác nhập ước lượng và đáp án chính xác.
- Cách hiển thị phản hồi.
- Khả năng sử dụng bàn phím.
- Khả năng nhận biết và sửa lỗi nhập liệu.

### 3.4. CI Testing – Kiểm thử tích hợp liên tục

Thiết lập quy trình CI để tự động:
1. Cài đặt các gói phụ thuộc bằng `npm ci`.
2. Chạy bộ kiểm thử bằng `npm test`.
3. Báo kết quả thành công hoặc thất bại trên Pull Request.

Kiểm thử phải chạy được từ trạng thái mã nguồn sạch, không phụ thuộc vào dữ liệu hoặc gói cài đặt chỉ tồn tại trên máy của một thành viên.

## 4. Môi trường và công cụ kiểm thử

### 4.1. Môi trường

| Thành phần | Yêu cầu |
|---|---|
| Hệ điều hành | Windows, macOS hoặc Linux |
| Runtime | Node.js phiên bản 18 trở lên |
| Backend | Express |
| Cơ sở dữ liệu | SQLite |
| Trình duyệt | Chrome hoặc trình duyệt hiện đại tương thích |
| Quản lý mã nguồn | Git và GitHub |
| CI | GitHub Actions |

### 4.2. Công cụ

Nhóm sử dụng các công cụ có sẵn hoặc được cấu hình trong starter repository:
- Công cụ kiểm thử JavaScript phù hợp với dự án.
- Công cụ gửi request API để kiểm tra endpoint.
- Trình duyệt để kiểm thử giao diện.
- SQLite để kiểm tra dữ liệu được lưu.
- GitHub Actions để chạy kiểm thử tự động.

**Lưu ý:** Tên thư viện kiểm thử cụ thể cần được xác nhận theo `package.json` và cấu trúc starter repository. Không cài thêm một framework kiểm thử khác nếu dự án đã có công cụ phù hợp.

## 5. Dữ liệu kiểm thử

Nhóm cần chuẩn bị tối thiểu 12 câu hỏi/bộ dữ liệu giả lập có thể tái lập, đáp ứng yêu cầu B-02.

Các dữ liệu này cần:
- Bao gồm cả phép nhân và phép chia.
- Có kết quả chính xác được xác định trước.
- Có khoảng ước lượng hợp lý.
- Có mã định danh riêng.
- Có thể sử dụng lặp lại trong các lần kiểm thử.
- Không chứa thông tin cá nhân thật.

### 5.1. Các nhóm dữ liệu cần có

| Nhóm | Mục đích |
|---|---|
| Phép nhân cơ bản | Kiểm tra ước lượng và tính toán với phép nhân |
| Phép nhân có kết quả lớn hơn | Kiểm tra khoảng ước lượng với giá trị lớn hơn |
| Phép chia cơ bản | Kiểm tra ước lượng và tính toán với phép chia |
| Phép chia có kết quả nguyên | Kiểm tra phép chia có thương nguyên |
| Giá trị ước lượng ở cận dưới | Kiểm tra tính chấp nhận tại cận dưới |
| Giá trị ước lượng ở cận trên | Kiểm tra tính chấp nhận tại cận trên |
| Giá trị nằm ngoài khoảng | Kiểm tra trường hợp ước lượng không hợp lý |
| Đáp án chính xác đúng | Kiểm tra chấm điểm phần tính toán |
| Đáp án chính xác sai | Kiểm tra phản hồi khi tính sai |
| Dữ liệu không hợp lệ | Kiểm tra khả năng từ chối dữ liệu sai |

Mỗi câu hỏi phải được xác định rõ dữ liệu đầu vào, kết quả chính xác và khoảng ước lượng hợp lý. Nhóm không được tạo khoảng ước lượng tùy tiện chỉ để làm cho câu trả lời dễ được chấp nhận.

## 6. Danh sách trường hợp kiểm thử

### 6.1. Kiểm thử tích hợp và luồng học tập

| Mã test | Nội dung | Thao tác / Dữ liệu | Kết quả mong đợi | Yêu cầu |
|---|---|---|---|---|
| TC-01 | Truy cập bài tập | Mở hệ thống và đi đến khu vực học tập | Bài tập ước lượng xuất hiện trong luồng học tập hiện có | B-01 |
| TC-02 | Hiển thị câu hỏi | Chọn một bài tập | Câu hỏi, hướng dẫn và vùng nhập liệu hiển thị đầy đủ | B-01, B-12 |
| TC-03 | Bộ dữ liệu câu hỏi | Kiểm tra danh sách câu hỏi giả lập | Có ít nhất 12 câu hỏi có thể tái lập | B-02 |
| TC-04 | Chuyển bước bài tập | Hoàn thành một câu và chuyển sang câu tiếp theo theo luồng được thiết kế | Câu hỏi tiếp theo được hiển thị đúng, không làm mất trạng thái đã lưu | B-01, B-05 |

### 6.2. Kiểm thử quy tắc ước lượng và chấm điểm

Giả sử câu hỏi có kết quả chính xác \(R\), khoảng ước lượng hợp lý là \([L,U]\), câu trả lời ước lượng là \(E\), và đáp án chính xác do học sinh nhập là \(A\).

| Mã test | Nội dung | Dữ liệu kiểm thử | Kết quả mong đợi | Yêu cầu |
|---|---|---|---|---|
| TC-05 | Ước lượng nằm trong khoảng | \(L \leq E \leq U\) | Phần ước lượng được đánh giá là hợp lý | B-03 |
| TC-06 | Ước lượng tại cận dưới | \(E=L\) | Được chấp nhận nếu quy tắc quy định hai cận đều bao gồm | B-03, B-08 |
| TC-07 | Ước lượng tại cận trên | \(E=U\) | Được chấp nhận nếu quy tắc quy định hai cận đều bao gồm | B-03, B-08 |
| TC-08 | Ước lượng thấp hơn khoảng | \(E<L\) | Phần ước lượng không được chấp nhận | B-03, B-08 |
| TC-09 | Ước lượng cao hơn khoảng | \(E>U\) | Phần ước lượng không được chấp nhận | B-03, B-08 |
| TC-10 | Đáp án chính xác đúng | \(A=R\) | Phần tính toán chính xác được đánh giá đúng | B-03, B-06 |
| TC-11 | Đáp án chính xác sai | \(A\neq R\) | Phần tính toán chính xác được đánh giá sai | B-03, B-06 |
| TC-12 | Ước lượng đúng nhưng tính sai | \(L\leq E\leq U\), \(A\neq R\) | Hệ thống ghi nhận ước lượng hợp lý nhưng phép tính chính xác chưa đúng | B-06 |
| TC-13 | Ước lượng sai nhưng tính đúng | \(E<L\) hoặc \(E>U\), \(A=R\) | Hệ thống ghi nhận phép tính chính xác đúng nhưng ước lượng chưa hợp lý | B-06 |

**Lưu ý:** Các công thức trên là quy tắc kiểm thử tổng quát. Giá trị \(L\), \(U\) và cách xây dựng khoảng ước lượng cụ thể phải thống nhất với thuật toán được nhóm lựa chọn và ghi trong `DECISIONS.md`.

### 6.3. Kiểm thử API và dữ liệu đầu vào

| Mã test | Nội dung | Thao tác / Dữ liệu | Kết quả mong đợi | Yêu cầu |
|---|---|---|---|---|
| TC-14 | Gửi câu trả lời hợp lệ | Gửi đầy đủ dữ liệu theo định dạng API | Máy chủ tiếp nhận, kiểm tra và trả kết quả phù hợp | B-03, B-05 |
| TC-15 | Thiếu trường dữ liệu | Gửi request thiếu trường bắt buộc | Máy chủ từ chối và trả thông báo lỗi rõ ràng | B-08, B-12 |
| TC-16 | Sai kiểu dữ liệu | Gửi chuỗi hoặc kiểu dữ liệu không phù hợp ở trường cần số | Máy chủ không chấm điểm sai và trả lỗi phù hợp | B-08, B-12 |
| TC-17 | Giá trị không hợp lệ | Gửi số âm, giá trị ngoài giới hạn hoặc dữ liệu không thuộc phạm vi bài tập | Máy chủ xử lý theo quy tắc xác thực đã xác định, không gây lỗi hệ thống | B-08 |
| TC-18 | Kiểm tra đáp án trước khi nộp | Gọi API lấy câu hỏi và kiểm tra toàn bộ dữ liệu phản hồi | Không có đáp án chính xác hoặc dữ liệu nội bộ chấm điểm trong phản hồi | B-04 |

### 6.4. Kiểm thử lưu trữ và bảo mật

| Mã test | Nội dung | Thao tác / Dữ liệu | Kết quả mong đợi | Yêu cầu |
|---|---|---|---|---|
| TC-19 | Lưu và truy xuất kết quả | Nộp bài hợp lệ, tải lại trang và truy xuất trạng thái | Kết quả đã nộp vẫn được lưu và hiển thị đúng | B-05 |
| TC-20 | Bảo vệ xác thực và dữ liệu | Kiểm tra thay đổi mã nguồn, dữ liệu mẫu và cấu hình | Không chỉnh sửa `server/auth.js`, session, tài khoản mẫu; không có dữ liệu cá nhân thật hoặc secret | B-07, B-11 |

### 6.5. Kiểm thử khả năng truy cập và CI

Ngoài các trường hợp trên, nhóm cần thực hiện các bước kiểm tra bổ sung sau:

| Mã test | Nội dung | Cách thực hiện | Kết quả mong đợi | Yêu cầu |
|---|---|---|---|---|
| TC-21 | Điều khiển bằng bàn phím | Dùng Tab, Shift + Tab, Enter và phím phù hợp để thao tác | Có thể truy cập và thao tác các thành phần chính mà không cần chuột | B-12 |
| TC-22 | Hiển thị thông báo lỗi | Nhập dữ liệu sai hoặc bỏ trống trường bắt buộc | Lỗi được thông báo rõ ràng, người học biết cách sửa | B-12 |
| TC-23 | Cài đặt sạch | Chạy `npm ci` từ trạng thái repository sạch | Cài đặt phụ thuộc thành công | B-09, B-10 |
| TC-24 | Chạy bộ kiểm thử | Chạy `npm test` | Bộ kiểm thử chạy thành công và kết quả được báo rõ ràng | B-09 |
| TC-25 | Kiểm tra CI trên Pull Request | Tạo hoặc cập nhật Pull Request | CI tự động chạy `npm ci` và `npm test` | B-10 |

## 7. Kiểm thử khả năng sử dụng

Nhóm thực hiện kiểm thử thủ công theo luồng học tập hoàn chỉnh:

1. Mở hệ thống Vườn Toán Lớp 3.
2. Truy cập khu vực học tập có tích hợp bài tập ước lượng.
3. Mở một câu hỏi phép nhân hoặc phép chia.
4. Đọc đề bài và nhập kết quả ước lượng.
5. Thực hiện phép tính chính xác và nhập đáp án.
6. Gửi câu trả lời.
7. Quan sát phản hồi của hệ thống.
8. Tải lại trang và kiểm tra kết quả đã lưu.
9. Thực hiện lại các bước bằng bàn phím.

**Tiêu chí đạt:**
- Người học nhận biết được bước ước lượng và bước tính chính xác.
- Không thể xem đáp án chính xác trước khi gửi bài.
- Phản hồi phân biệt rõ hai phần.
- Thông báo lỗi dễ hiểu và có hướng dẫn sửa.
- Kết quả đã lưu không bị mất khi tải lại trang.
- Các thành phần chính có thể thao tác bằng bàn phím.

## 8. Tiêu chí chấp nhận kiểm thử

Tính năng được xem là đạt yêu cầu kiểm thử khi đáp ứng các điều kiện sau:

1. Có thể truy cập từ luồng học tập hiện có.
2. Có tối thiểu 12 câu hỏi/bộ dữ liệu giả lập có thể tái lập.
3. Quy tắc ước lượng và chấm điểm được xác định rõ, có thể kiểm thử.
4. API không tiết lộ đáp án chính xác trước khi học sinh gửi bài.
5. Máy chủ thực hiện chấm điểm và lưu kết quả.
6. Kết quả đã lưu vẫn được truy xuất sau khi tải lại trang.
7. Phản hồi phân biệt được ước lượng hợp lý và đáp án chính xác.
8. Có kiểm thử cho trường hợp bình thường, trường hợp biên, dữ liệu không hợp lệ và quy tắc chấm điểm.
9. Lệnh `npm test` chạy thành công.
10. CI tự động chạy `npm ci` và `npm test` trên Pull Request.
11. Không có thay đổi trái phép đối với xác thực, session, tài khoản mẫu hoặc cấu hình triển khai.
12. Không sử dụng dữ liệu cá nhân thật hoặc để lộ thông tin bí mật.
13. Các thao tác chính có thể thực hiện bằng bàn phím và thông báo lỗi rõ ràng.

## 9. Quy trình thực hiện kiểm thử

Nhóm thực hiện kiểm thử theo thứ tự:

**Bước 1 – Chuẩn bị**
- Kiểm tra mã nguồn và tài liệu kiến trúc.
- Chuẩn bị môi trường Node.js.
- Cài đặt phụ thuộc bằng `npm ci`.
- Chuẩn bị bộ dữ liệu giả lập.

**Bước 2 – Kiểm thử đơn vị**
- Kiểm tra các hàm tạo khoảng ước lượng.
- Kiểm tra các hàm chấm điểm.
- Kiểm tra xác thực dữ liệu đầu vào.
- Kiểm tra phản hồi của hệ thống.

**Bước 3 – Kiểm thử tích hợp**
- Kiểm tra giao tiếp giữa giao diện và API.
- Kiểm tra xử lý dữ liệu phía máy chủ.
- Kiểm tra lưu và truy xuất kết quả từ SQLite.
- Kiểm tra khả năng tải lại trang mà không mất dữ liệu.

**Bước 4 – Kiểm thử thủ công**
- Thực hiện luồng học tập hoàn chỉnh.
- Kiểm tra giao diện và thông báo lỗi.
- Kiểm tra thao tác bằng bàn phím.
- Kiểm tra các tình huống người học có thể gặp.

**Bước 5 – Kiểm thử CI**
- Chạy `npm test`.
- Tạo Pull Request.
- Kiểm tra GitHub Actions thực hiện `npm ci` và `npm test`.
- Xử lý các lỗi được phát hiện trước khi hợp nhất mã nguồn.

**Bước 6 – Tổng hợp kết quả**
- Ghi nhận số lượng test đạt và không đạt.
- Ghi nhận lỗi đã phát hiện và cách xử lý.
- Đối chiếu kết quả với tiêu chí chấp nhận.
- Hoàn thiện `TEST_REPORT.md`.

## 10. Ghi nhận lỗi

Khi phát hiện lỗi, nhóm cần ghi lại các thông tin:

| Trường thông tin | Nội dung |
|---|---|
| Bug ID | Mã lỗi riêng |
| Test Case ID | Mã trường hợp kiểm thử liên quan |
| Mô tả lỗi | Hiện tượng xảy ra |
| Các bước tái hiện | Trình tự thao tác để tạo lại lỗi |
| Kết quả thực tế | Kết quả hệ thống đang trả về |
| Kết quả mong đợi | Kết quả đúng theo yêu cầu |
| Mức độ nghiêm trọng | Critical / High / Medium / Low |
| Trạng thái | Open / In Progress / Fixed / Verified |
| Người phụ trách | Thành viên xử lý |

Sau khi sửa lỗi, nhóm cần chạy lại test case liên quan và các test có khả năng bị ảnh hưởng.

## 11. Liên kết giữa yêu cầu và kiểm thử

Bảng dưới đây giúp kiểm tra xem các yêu cầu trong đề bài đã có trường hợp kiểm thử tương ứng hay chưa.

| Yêu cầu | Nội dung | Test case |
|---|---|---|
| B-01 | Tích hợp vào luồng học tập | TC-01, TC-02, TC-04 |
| B-02 | Tối thiểu 12 câu hỏi giả lập | TC-03 |
| B-03 | Quy tắc ước lượng và chấm điểm xác định | TC-05 đến TC-17 |
| B-04 | Không tiết lộ đáp án trước khi nộp | TC-18 |
| B-05 | Máy chủ chấm điểm và lưu kết quả | TC-14, TC-19 |
| B-06 | Phân biệt phản hồi ước lượng và tính chính xác | TC-10 đến TC-13 |
| B-07 | Không thay đổi xác thực, session, tài khoản mẫu và triển khai | TC-20 |
| B-08 | Kiểm thử bình thường, biên, dữ liệu sai và chấm điểm | TC-05 đến TC-17 |
| B-09 | Có lệnh `npm test` chạy thành công | TC-24 |
| B-10 | CI chạy `npm ci` và `npm test` trên Pull Request | TC-23, TC-25 |
| B-11 | Không sử dụng dữ liệu cá nhân thật hoặc secret | TC-20 |
| B-12 | Hỗ trợ bàn phím và thông báo lỗi rõ ràng | TC-02, TC-15, TC-16, TC-21, TC-22 |

## 12. Kết luận

Kế hoạch kiểm thử này được xây dựng nhằm bảo đảm tính năng “Ước lượng trước khi tính đúng” đáp ứng các yêu cầu chức năng, phi chức năng và tiêu chí chấp nhận của Track B.

Việc kết hợp kiểm thử đơn vị, kiểm thử tích hợp, kiểm thử thủ công và CI giúp nhóm phát hiện lỗi trong quá trình phát triển, kiểm tra tính ổn định của hệ thống và bảo đảm khả năng bàn giao.

Sau khi hoàn tất kiểm thử thực tế, nhóm sẽ sử dụng kết quả thu được để xây dựng `TEST_REPORT.md`. Kế hoạch kiểm thử này không thay thế báo cáo kết quả kiểm thử.
