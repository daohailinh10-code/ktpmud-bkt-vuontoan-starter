# REQUIREMENTS.md
# VƯỜN TOÁN LỚP 3 – ƯỚC LƯỢNG TRƯỚC KHI TÍNH ĐÚNG
---

## 1. Giới thiệu

### 1.1. Mục đích tài liệu

Tài liệu này xác định các yêu cầu chức năng, yêu cầu phi chức năng và tiêu chí chấp nhận đối với việc mở rộng hệ thống Vườn Toán Lớp 3 bằng cách bổ sung dạng bài tập “Ước lượng trước khi tính đúng”.

Mục tiêu của chức năng là giúp học sinh lớp 3 rèn luyện khả năng ước lượng kết quả phép tính trước khi thực hiện phép tính chính xác. Qua đó, học sinh không chỉ luyện tập kỹ năng tính toán mà còn phát triển tư duy số học, khả năng dự đoán và kiểm tra tính hợp lý của kết quả.

Tài liệu được sử dụng làm cơ sở cho thiết kế, triển khai và kiểm thử trong các giai đoạn tiếp theo.

### 1.2. Bối cảnh

Hệ thống Vườn Toán Lớp 3 hiện hỗ trợ bốn loại câu hỏi:

- `multiple-choice`: Câu hỏi trắc nghiệm.
- `input`: Câu hỏi nhập đáp án.
- `compare`: Câu hỏi so sánh.
- `paint`: Câu hỏi tô màu.

Các dạng câu hỏi hiện tại chưa hỗ trợ việc đánh giá đồng thời khả năng ước lượng và khả năng tính toán chính xác.

Vì vậy, nhóm đề xuất bổ sung dạng câu hỏi mới có tên `estimate`, trong đó học sinh phải thực hiện hai nhiệm vụ: nhập kết quả ước lượng và nhập kết quả tính toán chính xác.

### 1.3. Đối tượng sử dụng

- **Học sinh lớp 3:** Trực tiếp làm bài tập và nhận kết quả đánh giá.
- **Giáo viên:** Sử dụng hệ thống để tổ chức nội dung luyện tập và theo dõi kết quả học tập.

---

## 2. Phạm vi dự án

### 2.1. Trong phạm vi

Chức năng mới bao gồm:

1. Bổ sung loại câu hỏi `estimate`.
2. Hỗ trợ bài tập ước lượng kết quả phép nhân và phép chia.
3. Cho phép học sinh nhập kết quả ước lượng.
4. Cho phép học sinh nhập kết quả tính toán chính xác.
5. Xác định khoảng ước lượng hợp lệ theo quy tắc sai số 10%.
6. Chấm điểm độc lập hai thành phần trả lời.
7. Lưu kết quả làm bài vào hệ thống hiện tại.
8. Cập nhật điểm số, tiến độ và sao theo cơ chế sẵn có.
9. Bổ sung dữ liệu mẫu và các trường hợp kiểm thử.
10. Bảo đảm các dạng câu hỏi hiện có tiếp tục hoạt động bình thường.

### 2.2. Ngoài phạm vi

Các chức năng sau không thuộc phạm vi thực hiện:

- Thay đổi hệ thống đăng nhập và xác thực người dùng.
- Thay đổi chức năng quản trị và quản lý giáo viên.
- Xây dựng lại toàn bộ giao diện hệ thống.
- Thay đổi cấu trúc cơ sở dữ liệu nếu không thực sự cần thiết.
- Bổ sung các dạng phép tính khác ngoài phép nhân và phép chia trong phạm vi phiên bản này.
- Thay đổi cơ chế tính sao và cập nhật tiến độ hiện có.

---

## 3. Mô tả chức năng

### 3.1. Quy trình làm bài

Một câu hỏi `estimate` có quy trình như sau:

1. Hệ thống hiển thị phép tính cần thực hiện.
2. Học sinh quan sát phép tính và nhập kết quả ước lượng.
3. Học sinh tiếp tục thực hiện phép tính và nhập kết quả chính xác.
4. Học sinh gửi câu trả lời.
5. Backend kiểm tra tính hợp lệ của dữ liệu.
6. Hệ thống xác định kết quả ước lượng đúng hay sai.
7. Hệ thống xác định kết quả tính toán chính xác đúng hay sai.
8. Hệ thống tính điểm cho câu hỏi.
9. Hệ thống lưu kết quả và cập nhật tiến độ học tập.

### 3.2. Ví dụ minh họa

Với câu hỏi:

\[
12\times4=?
\]

Hệ thống xác định kết quả chính xác là 48 và khoảng ước lượng hợp lệ là từ 44 đến 52.

Học sinh cần nhập hai giá trị:

- Kết quả ước lượng: 48.
- Kết quả tính chính xác: 48.

Nếu học sinh nhập kết quả ước lượng là 50 và kết quả chính xác là 48 thì cả hai thành phần đều được tính đúng.

Nếu học sinh nhập kết quả ước lượng là 43 nhưng kết quả tính chính xác là 48 thì học sinh chỉ được ghi nhận điểm của thành phần tính chính xác.

---

## 4. Yêu cầu chức năng

### FR-01. Nhận diện loại câu hỏi mới

Hệ thống phải hỗ trợ loại câu hỏi mới có giá trị:

`type = "estimate"`

Loại câu hỏi này phải được phân biệt với các loại câu hỏi hiện có và có cách hiển thị, thu thập dữ liệu và chấm điểm riêng.

### FR-02. Hiển thị nội dung câu hỏi

Hệ thống phải hiển thị đầy đủ nội dung phép tính cần thực hiện.

Đối với câu hỏi `estimate`, giao diện phải có hai ô nhập riêng biệt:

- Ô nhập kết quả ước lượng.
- Ô nhập kết quả tính toán chính xác.

Hai ô nhập phải có nhãn hướng dẫn rõ ràng, dễ hiểu và phù hợp với học sinh lớp 3.

### FR-03. Nhập kết quả ước lượng

Hệ thống phải cho phép học sinh nhập một số nguyên không âm làm kết quả ước lượng.

Giá trị nhập phải được kiểm tra tính hợp lệ trước khi gửi đến máy chủ.

### FR-04. Nhập kết quả tính toán chính xác

Hệ thống phải cho phép học sinh nhập kết quả chính xác của phép tính dưới dạng số nguyên không âm.

Kết quả này được sử dụng để đánh giá khả năng thực hiện phép tính của học sinh.

### FR-05. Xác định khoảng ước lượng hợp lệ

Hệ thống phải xác định khoảng ước lượng dựa trên kết quả chính xác của phép tính.

Gọi:

- \(R\): Kết quả chính xác.
- \(L\): Giới hạn dưới.
- \(U\): Giới hạn trên.

Công thức xác định khoảng:

\[
L=\lceil0.9R\rceil
\]

\[
U=\lfloor1.1R\rfloor
\]

Giá trị ước lượng \(E\) được chấp nhận khi:

\[
L\leq E\leq U
\]

Trong đó:

- Sai số tương đối tối đa được lựa chọn là 10%.
- Giới hạn dưới và giới hạn trên đều được tính là giá trị hợp lệ.
- Các giá trị nằm ngoài khoảng không được chấp nhận.

Quy tắc này được áp dụng thống nhất cho phép nhân và phép chia có kết quả nguyên không âm.

### FR-06. Chấm điểm kết quả ước lượng

Hệ thống phải kiểm tra kết quả ước lượng của học sinh có nằm trong khoảng hợp lệ hay không.

- Nếu nằm trong khoảng hợp lệ: Thành phần ước lượng được tính đúng.
- Nếu nằm ngoài khoảng hợp lệ: Thành phần ước lượng được tính sai.

### FR-07. Chấm điểm kết quả tính toán chính xác

Hệ thống phải so sánh kết quả học sinh nhập với đáp án chính xác được lưu trong dữ liệu câu hỏi.

- Nếu hai giá trị bằng nhau: Thành phần tính toán được tính đúng.
- Nếu hai giá trị khác nhau: Thành phần tính toán được tính sai.

### FR-08. Tính điểm câu hỏi

Mỗi câu hỏi `estimate` được chia thành hai thành phần có tỷ trọng bằng nhau:

| Thành phần | Tỷ lệ điểm |
|---|---:|
| Ước lượng | 50% |
| Tính toán chính xác | 50% |
| Tổng | 100% |

Gọi \(P\) là điểm tối đa của câu hỏi.

Điểm đạt được được tính theo công thức:

\[
C=C_E+C_X
\]

Trong đó:

\[
C_E=
\begin{cases}
0.5P & \text{nếu ước lượng đúng}\\
0 & \text{nếu ước lượng sai}
\end{cases}
\]

\[
C_X=
\begin{cases}
0.5P & \text{nếu tính chính xác đúng}\\
0 & \text{nếu tính chính xác sai}
\end{cases}
\]

Các trường hợp cụ thể:

| Ước lượng | Tính chính xác | Điểm |
|---|---|---:|
| Đúng | Đúng | 100% |
| Đúng | Sai | 50% |
| Sai | Đúng | 50% |
| Sai | Sai | 0% |

Một câu hỏi chỉ được tính là câu trả lời đúng hoàn toàn khi cả hai thành phần đều đúng.

### FR-09. Lưu kết quả làm bài

Hệ thống phải lưu được cả hai giá trị mà học sinh đã nhập.

Dữ liệu câu trả lời được lưu trong trường `answers_json` của bảng `attempts` theo cấu trúc:

```json
{
  "estimate-01": {
    "estimate": 48,
    "exact": 48
  }
}
```

Các thông tin về điểm số, số câu đúng, tổng số câu và thời gian làm bài tiếp tục được lưu theo cấu trúc hiện có.

### FR-10. Cập nhật tiến độ và sao

Sau khi học sinh hoàn thành bài tập, hệ thống phải:

- Lưu kết quả lần làm bài.
- Cập nhật điểm số theo cơ chế hiện tại.
- Cập nhật điểm cao nhất trong `progress` nếu kết quả đáp ứng điều kiện hiện có.
- Cập nhật trạng thái hoàn thành theo quy tắc hiện tại.
- Tính sao thưởng theo cơ chế hiện tại.

Việc bổ sung dạng câu hỏi `estimate` không được tạo ra một cơ chế cập nhật tiến độ hoặc tính sao riêng.

### FR-11. Bảo vệ đáp án

Hệ thống không được trả về đáp án chính xác hoặc khoảng ước lượng hợp lệ trong API lấy danh sách câu hỏi dành cho học sinh.

Các thông tin `lower`, `upper`, `exact` chỉ được sử dụng ở phía backend trong quá trình chấm điểm.

### FR-12. Tương thích với các loại câu hỏi hiện có

Việc bổ sung `estimate` không được làm thay đổi cơ chế xử lý của các loại câu hỏi:

- `multiple-choice`.
- `input`.
- `compare`.
- `paint`.

Các dạng câu hỏi hiện tại phải tiếp tục hoạt động như trước khi bổ sung chức năng mới.

---

## 5. Yêu cầu phi chức năng

### NFR-01. Tính chính xác

Các phép tính xác định giới hạn dưới và giới hạn trên phải tuân thủ đúng công thức đã quy định.

Kết quả chấm điểm phải nhất quán với dữ liệu đáp án được lưu trong cơ sở dữ liệu.

### NFR-02. Tính dễ sử dụng

Giao diện phải đơn giản, trực quan và phù hợp với khả năng tiếp nhận của học sinh lớp 3.

Hai ô nhập phải được phân biệt rõ ràng để tránh nhầm lẫn giữa kết quả ước lượng và kết quả tính toán chính xác.

### NFR-03. Tính tương thích

Chức năng mới phải hoạt động trên kiến trúc hiện có của dự án, sử dụng Node.js, Express, SQLite, HTML, CSS và JavaScript.

Không yêu cầu thay đổi toàn bộ hệ thống hoặc bổ sung công nghệ mới.

### NFR-04. Tính bảo mật

Đáp án chuẩn và khoảng ước lượng hợp lệ không được gửi đến frontend trước khi học sinh nộp bài.

Backend phải tự kiểm tra và chấm điểm, không phụ thuộc vào kết quả đánh giá do frontend gửi lên.

### NFR-05. Khả năng bảo trì

Mã nguồn bổ sung phải được tổ chức theo cấu trúc hiện có.

Nhánh xử lý câu hỏi `estimate` phải tách biệt với các nhánh xử lý câu hỏi cũ để hạn chế ảnh hưởng và thuận tiện cho việc bảo trì.

### NFR-06. Khả năng kiểm thử

Các quy tắc tính khoảng, kiểm tra giá trị biên và tính điểm phải có thể kiểm thử bằng các dữ liệu đầu vào và đầu ra cụ thể.

---

## 6. Dữ liệu mẫu và tiêu chí chấp nhận

### 6.1. Dữ liệu mẫu cho phép nhân và phép chia

Hệ thống cần có tối thiểu 12 trường hợp dữ liệu mẫu để kiểm tra công thức xác định khoảng ước lượng.

Các giá trị trong bảng được xác định theo:

\[
L=\lceil0.9R\rceil,\qquad U=\lfloor1.1R\rfloor
\]

| Mã | Phép tính | Kết quả chính xác (R) | Giới hạn dưới (L) | Giới hạn trên (U) |
|---|---|---:|---:|---:|
| F01 | 12 × 4 | 48 | 44 | 52 |
| F02 | 15 × 3 | 45 | 41 | 49 |
| F03 | 24 × 3 | 72 | 65 | 79 |
| F04 | 18 × 5 | 90 | 81 | 99 |
| F05 | 25 × 4 | 100 | 90 | 110 |
| F06 | 32 × 3 | 96 | 87 | 105 |
| F07 | 48 ÷ 4 | 12 | 11 | 13 |
| F08 | 72 ÷ 6 | 12 | 11 | 13 |
| F09 | 84 ÷ 4 | 21 | 19 | 23 |
| F10 | 96 ÷ 4 | 24 | 22 | 26 |
| F11 | 120 ÷ 5 | 24 | 22 | 26 |
| F12 | 144 ÷ 6 | 24 | 22 | 26 |

Các dữ liệu trên là cơ sở để xây dựng bộ câu hỏi mẫu và kiểm thử chức năng chấm điểm.

### 6.2. Tiêu chí chấp nhận

**AC-01. Nhận diện câu hỏi**

Khi hệ thống nhận được câu hỏi có `type = estimate`, giao diện phải hiển thị đúng dạng bài ước lượng với hai ô nhập.

**AC-02. Nhập dữ liệu**

Học sinh có thể nhập hai giá trị riêng biệt. Hệ thống phải từ chối dữ liệu không hợp lệ như giá trị rỗng, số âm hoặc dữ liệu không phải số nguyên.

**AC-03. Kiểm tra khoảng ước lượng**

Với phép tính \(12\times4=48\), khoảng hợp lệ phải là từ 44 đến 52.

Các giá trị 44, 48 và 52 phải được chấp nhận; các giá trị 43 và 53 phải bị từ chối.

**AC-04. Kiểm tra phép chia**

Với phép tính \(84\div4=21\), khoảng hợp lệ phải là từ 19 đến 23.

Các giá trị 19, 21 và 23 phải được chấp nhận; các giá trị 18 và 24 phải bị từ chối.

**AC-05. Chấm điểm độc lập**

Hệ thống phải phân biệt được bốn trường hợp:

- Cả hai thành phần đúng: 100% điểm câu hỏi.
- Chỉ ước lượng đúng: 50% điểm câu hỏi.
- Chỉ tính chính xác đúng: 50% điểm câu hỏi.
- Cả hai thành phần sai: 0% điểm câu hỏi.

**AC-06. Lưu kết quả**

Sau khi nộp bài, hệ thống phải lưu được cả giá trị ước lượng và giá trị tính chính xác trong `answers_json`.

**AC-07. Cập nhật tiến độ**

Kết quả bài làm phải được lưu vào `attempts` và được sử dụng trong luồng cập nhật `progress` và tính sao hiện có.

**AC-08. Bảo mật đáp án**

API lấy danh sách câu hỏi không được trả về `correct_answer` hoặc các giới hạn ước lượng.

**AC-09. Tương thích ngược**

Bốn loại câu hỏi hiện có phải tiếp tục hoạt động bình thường sau khi bổ sung dạng `estimate`.

---

## 7. Yêu cầu kiểm thử

Các yêu cầu cần được kiểm thử bao gồm:

| Mã | Nội dung kiểm thử | Kết quả mong đợi |
|---|---|---|
| TC-01 | Hiển thị câu hỏi `estimate` | Có hai ô nhập riêng biệt |
| TC-02 | Nhập hai giá trị hợp lệ | Hệ thống tiếp nhận dữ liệu |
| TC-03 | Nhập dữ liệu không hợp lệ | Hệ thống từ chối dữ liệu |
| TC-04 | Kiểm tra công thức tính khoảng | Giới hạn được tính đúng |
| TC-05 | Nhập 48 cho phép tính 12 × 4 | Ước lượng hợp lệ |
| TC-06 | Nhập 44 cho phép tính 12 × 4 | Ước lượng hợp lệ |
| TC-07 | Nhập 52 cho phép tính 12 × 4 | Ước lượng hợp lệ |
| TC-08 | Nhập 43 cho phép tính 12 × 4 | Ước lượng không hợp lệ |
| TC-09 | Nhập 53 cho phép tính 12 × 4 | Ước lượng không hợp lệ |
| TC-10 | Nhập 48 ở phần tính chính xác | Tính chính xác đúng |
| TC-11 | Nhập 47 ở phần tính chính xác | Tính chính xác sai |
| TC-12 | Ước lượng 48, tính chính xác 47 | Đạt 50% điểm câu hỏi |
| TC-13 | Ước lượng 43, tính chính xác 48 | Đạt 50% điểm câu hỏi |
| TC-14 | Cả hai thành phần đều đúng | Đạt 100% điểm câu hỏi |
| TC-15 | Cả hai thành phần đều sai | Đạt 0% điểm câu hỏi |
| TC-16 | Lưu câu trả lời | Lưu đủ hai giá trị trong `answers_json` |
| TC-17 | Kiểm tra API lấy câu hỏi | Không trả về đáp án chuẩn |
| TC-18 | Kiểm tra cập nhật tiến độ | Tiến độ được cập nhật theo cơ chế hiện tại |
| TC-19 | Kiểm tra tính sao | Sao được tính theo cơ chế hiện tại |
| TC-20 | Kiểm thử hồi quy | Bốn loại câu hỏi cũ vẫn hoạt động |

Chi tiết từng bước thực hiện, dữ liệu đầu vào và kết quả mong đợi được trình bày trong `TEST_PLAN.md`.

---

## 8. Ràng buộc kỹ thuật

### 8.1. Công nghệ sử dụng

Chức năng mới phải sử dụng công nghệ và kiến trúc hiện có:

- Node.js.
- Express.
- SQLite.
- `better-sqlite3`.
- HTML, CSS và JavaScript thuần.

### 8.2. Các thành phần dự kiến thay đổi

| Thành phần | Đường dẫn | Nội dung thay đổi |
|---|---|---|
| Backend API | `server/api.js` | Bổ sung nhánh chấm điểm `estimate` trong `POST /api/submissions` |
| Frontend | `public/assets/js/pages/exercise.js` | Hiển thị hai ô nhập và thu thập dữ liệu |
| Dữ liệu câu hỏi | Bảng `questions` | Bổ sung type `estimate`, lưu JSON trong `correct_answer` |
| Dữ liệu kết quả | Bảng `attempts` | Lưu hai thành phần câu trả lời trong `answers_json` |

### 8.3. Các thành phần không được thay đổi

- `server/auth.js`.
- Các route `/api/auth/*`.
- Các route `/api/teacher/*`.
- Các route `/api/admin/*`.
- Cơ chế xử lý bốn loại câu hỏi hiện có.
- Cơ chế cập nhật tiến độ và tính sao hiện có.

---

## 9. Kết luận

Chức năng “Ước lượng trước khi tính đúng” được xây dựng nhằm bổ sung một phương pháp luyện tập giúp học sinh lớp 3 phát triển đồng thời khả năng ước lượng và kỹ năng tính toán chính xác.

Nhóm lựa chọn bổ sung loại câu hỏi `estimate`, áp dụng sai số tương đối 10% để xác định khoảng chấp nhận và chia điểm thành hai thành phần bằng nhau. Dữ liệu đáp án được lưu dưới dạng JSON trong trường `correct_answer` hiện có, trong khi kết quả làm bài tiếp tục được lưu trong cấu trúc `attempts` hiện tại.

Phương án này tận dụng kiến trúc sẵn có, hạn chế thay đổi cơ sở dữ liệu và bảo đảm khả năng tương thích với các chức năng hiện tại. Đây là cơ sở để nhóm triển khai, kiểm thử và đánh giá chức năng trong các giai đoạn tiếp theo.
