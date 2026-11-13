# PROGRESS — 33 — Track B

- Starter: `fossbk-spec/ktpmud-bkt-vuontoan-starter` · tag `bkt-2026-v1`
- Fork: https://github.com/daohailinh10-code/ktpmud-bkt-vuontoan-starter

## PC-1 — 11/11/2026

### 1.1. Tiến độ theo acceptance criteria

| Mã | Trạng thái (Chưa / Đang / Xong) | Bằng chứng (commit / CI / file) | Ghi chú |
|---|---|---|---|
| B-01 | Đang | `REQUIREMENTS.md`; `public/assets/js/pages/exercise.js` | Đã phân tích luồng hiện có; chưa xác nhận dạng bài mới được tích hợp vào luồng học. |
| B-02 | Đang | `DECISIONS.md` mục 4; `TEST_PLAN.md` mục 4 | Đã liệt kê 12 fixture synthetic trong tài liệu; cần xác nhận dữ liệu được đưa vào ứng dụng và tái lập được khi chạy. |
| B-03 | Xong | `REQUIREMENTS.md` FR-05; `DECISIONS.md` ADR-03; `TEST_PLAN.md` mục 3 | Đã quy định công thức tất định: L = ceil(0.9R), U = floor(1.1R), chấp nhận L ≤ E ≤ U; có ví dụ nhân/chia và giá trị biên. |
| B-04 | Đang | `REQUIREMENTS.md` FR-11; `DECISIONS.md` | Đã nêu yêu cầu bảo vệ đáp án; cần kiểm thử API thực tế để xác nhận không trả đáp án trước khi nộp. |
| B-05 | Đang | `REQUIREMENTS.md` FR-09, FR-10; `DECISIONS.md` | Đã xác định cách lưu câu trả lời và tiến độ; cần triển khai, kiểm thử server và refresh. |
| B-06 | Đang | `REQUIREMENTS.md` FR-06 đến FR-08; `TEST_PLAN.md` mục 5 | Đã đặc tả chấm điểm hai thành phần; cần triển khai feedback phân biệt hai kết quả trên giao diện. |
| B-07 | Đang | `docs/architecture-reference.md` mục 1; `server/auth.js` | Đã xác định authentication/session nằm ngoài phạm vi; cần rà soát diff cuối để xác nhận không sửa file và cấu hình bị cấm. |
| B-08 | Đang | `TEST_PLAN.md` mục 6 | Đã thiết kế các ca normal, boundary, invalid input và scoring; cần chuyển thành test tự động. |
| B-09 | Chưa | `package.json` | Hiện chưa có script `npm test`; cần bổ sung và chạy test từ clean checkout. |
| B-10 | Chưa | Chưa có workflow CI được xác nhận trong fork | Cần bổ sung CI chạy `npm ci` và `npm test` trên Pull Request. |
| B-11 | Đang | `README.md` mục cảnh báo dữ liệu; `data/seed.json` | Starter mô tả dữ liệu synthetic; cần rà soát toàn bộ thay đổi để xác nhận không đưa PII/secret vào bài nộp. |
| B-12 | Đang | `REQUIREMENTS.md` NFR-02; `TEST_PLAN.md` | Đã nêu yêu cầu UX; cần kiểm thử thao tác bàn phím và thông báo lỗi trên giao diện thực tế. |

### 1.2. Sửa đổi bắt buộc từ Checkpoint 1

| Mục | Trạng thái | Bằng chứng |
|---|---|---|
| DEC-03: bổ sung cách tính cụ thể L, U cho phép nhân/chia | Xong | `DECISIONS.md` ADR-03; `TEST_PLAN.md` mục 3. Công thức và ví dụ: 12 × 4 = 48 → [44, 52]; 84 ÷ 4 = 21 → [19, 23]. |
| Bổ sung 12 fixture synthetic | Đang | `DECISIONS.md` mục 4; `TEST_PLAN.md` mục 4. Đã có danh sách 12 fixture trong tài liệu; cần xác nhận fixture được dùng trong test/dữ liệu chạy. |
| Bổ sung dữ liệu đầu vào cụ thể cho TC-05 đến TC-13 | Xong | `TEST_PLAN.md` mục 6.2–6.4 có dữ liệu E, A, khoảng hợp lệ và kết quả mong đợi. |
| Làm rõ cách tính điểm khi chỉ đúng một trong hai thành phần; tiến độ/sao | Xong | `DECISIONS.md` mục 5; `REQUIREMENTS.md` FR-08 đến FR-10. Hai thành phần 50% + 50%; giữ cơ chế progress/sao hiện có. |

### 1.3. Timeline dự kiến đến khi hoàn thành

| Việc | Vai trò phụ trách | Mốc (CP2 15/11 · M3 · Freeze 19/11 · M4 20/11) | Ngày dự kiến |
|---|---|---|---|
| Hoàn thiện luồng câu hỏi estimate từ giao diện hiện có | FE | CP2 | 15/11/2026 |
| Triển khai API chấm điểm, lưu câu trả lời và cập nhật tiến độ | BE | CP2 | 15/11/2026 |
| Bổ sung 12 fixture và test tự động cho scoring/edge cases | QA | M3 | 17/11/2026 |
| Bổ sung CI, rà soát bảo mật và accessibility | QA / BE / FE | M3 | 18/11/2026 |
| Hoàn thiện báo cáo, checklist, AI-use và contributions | DOCS | Freeze | 19/11/2026 |
| Tạo tag RC và hoàn tất PR nộp bài | Lead | M4 | 20/11/2026 |

### 1.4. Rủi ro / đang vướng

- Phạm vi thay đổi phải giới hạn ở dạng bài estimate; tránh ảnh hưởng bốn loại câu hỏi hiện có.
- Cần bảo đảm đáp án và khoảng ước lượng chỉ được xử lý ở backend, không lộ qua API lấy câu hỏi.
- Rủi ro tiến độ: hiện tài liệu yêu cầu/thiết kế/kế hoạch test đã có nhưng chưa xác nhận đầy đủ phần triển khai, test tự động và CI.
- Cần kiểm tra lại khả năng truy cập bằng bàn phím và nội dung thông báo lỗi phù hợp học sinh lớp 3.

### 1.5. Câu hỏi cho GV

- Q1: Với câu hỏi estimate, `correct_count` nên chỉ tăng khi cả ước lượng và kết quả chính xác đều đúng, còn `score_percent` vẫn cộng điểm thành phần 50% + 50% — cách hiểu này có đúng với yêu cầu chấm điểm không?
- Q2: 12 fixture cần được nạp vào dữ liệu câu hỏi của ứng dụng, hay có thể được quản lý riêng trong bộ test tự động miễn bảo đảm tái lập?

### 1.6. Phân công (alias hoặc vai trò, KHÔNG ghi họ tên/MSSV)

| Alias / vai trò | Đầu việc chính | Commit/PR tiêu biểu |
|---|---|---|
| Lead | Điều phối, rà soát yêu cầu và tích hợp | Cập nhật sau khi nhóm đối chiếu lịch sử commit |
| BE | API, quy tắc chấm điểm, lưu dữ liệu | Cập nhật commit triển khai |
| FE | Giao diện câu hỏi estimate và feedback | Cập nhật commit triển khai |
| QA | Fixture, test tự động, kiểm thử biên | Cập nhật commit test |
| DOCS | Requirements, decisions, test plan và báo cáo | `REQUIREMENTS.md`, `DECISIONS.md`, `TEST_PLAN.md` |

> Bảng vai trò trên là phân công theo vai trò dự kiến; nhóm cần thay bằng alias thực tế và commit tương ứng trước khi xác nhận PC-1.

## PC-2 — 18/11/2026

### 2.1. Đối chiếu timeline PC-1

| Việc (theo bảng 1.3) | Kế hoạch | Thực tế | Lệch & lý do |
|---|---|---|---|
| Hoàn thiện luồng câu hỏi estimate | 15/11/2026 | Chưa cập nhật | |
| Triển khai API chấm điểm và lưu dữ liệu | 15/11/2026 | Chưa cập nhật | |
| Bổ sung fixture và test tự động | 17/11/2026 | Chưa cập nhật | |
| CI, bảo mật và accessibility | 18/11/2026 | Chưa cập nhật | |
| Hoàn thiện tài liệu bàn giao | 19/11/2026 | Chưa cập nhật | |
| Tag RC và PR nộp bài | 20/11/2026 | Chưa cập nhật | |

### 2.2. Tiến độ theo acceptance criteria (cập nhật toàn bộ bảng 1.1)

| Mã | Trạng thái | Bằng chứng | Ghi chú |
|---|---|---|---|
| B-01 | Chưa cập nhật | | |
| B-02 | Chưa cập nhật | | |
| B-03 | Chưa cập nhật | | |
| B-04 | Chưa cập nhật | | |
| B-05 | Chưa cập nhật | | |
| B-06 | Chưa cập nhật | | |
| B-07 | Chưa cập nhật | | |
| B-08 | Chưa cập nhật | | |
| B-09 | Chưa cập nhật | | |
| B-10 | Chưa cập nhật | | |
| B-11 | Chưa cập nhật | | |
| B-12 | Chưa cập nhật | | |

### 2.3. Sẵn sàng nộp bài (đề thi Mục 6)

| Deliverable | Có / Chưa | Đường dẫn |
|---|---|---|
| README.md (cài đặt / chạy / test) | Chưa cập nhật | |
| REQUIREMENTS.md | Có | `REQUIREMENTS.md` |
| DECISIONS.md / ADR | Có | `DECISIONS.md` |
| Test tự động + CI xanh | Chưa cập nhật | |
| TEST_REPORT.md | Chưa cập nhật | |
| SECURITY_PRIVACY_CHECKLIST.md | Chưa cập nhật | |
| AI_USE.md | Chưa cập nhật | |
| CONTRIBUTIONS.md | Chưa cập nhật | |
| Slide / demo script ≤ 7 phút | Chưa cập nhật | |
| Draft PR vào `ktpmud-project`, check `validate` xanh | Chưa cập nhật | |

### 2.4. Việc còn lại đến Freeze (23:59 19/11)

| Việc | Vai trò phụ trách | Hạn |
|---|---|---|
| Hoàn thiện các acceptance criteria chưa đạt và chạy test từ clean checkout | BE / FE / QA | 19/11/2026 |
| Rà soát PII/secret, accessibility và tài liệu bàn giao | QA / DOCS | 19/11/2026 |
| Chốt commit, tag `bkt-2026-33-rc1` và cập nhật source reference | Lead | 19/11/2026 |

### 2.5. Rủi ro / câu hỏi cho GV

- Chưa cập nhật; nhóm bổ sung sau Checkpoint 2.

## Kết quả cuối — Freeze 19/11/2026

- Tag: `bkt-2026-33-rc1` · SHA: Chưa cập nhật
- Trạng thái cuối từng mã AC: cập nhật tại bảng 2.2.
- Những việc trong timeline chưa hoàn thành và lý do: Chưa cập nhật.
