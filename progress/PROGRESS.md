# PROGRESS — 33 — Track B
Sản phẩm: Vườn Toán Lớp 3 — Ước lượng trước khi tính đúng
Track: B
Nhóm: 33
Starter: bkt-2026-v1
Branch báo cáo: submit/hoang_mai_toan-N33
Ngày cập nhật: 17/11/2026
Commit mã nguồn starter đã có CI: be5da68e3e6d4d776aa96a30cf6bfe6ee1675df5 (theo source-ref.json và TEST_REPORT.md).
PR nộp tài liệu: #37, nhánh submit/hoang_mai_toan-N33; trạng thái mở, không phải Draft; bot đã xác nhận hợp lệ về cấu trúc tại commit ae38b95.
Nguyên tắc ghi trạng thái: Chỉ đánh dấu “Xong” khi có bằng chứng tương ứng trong mã nguồn, test chạy được, kết quả kiểm thử hoặc CI. Nội dung mới được mô tả trong tài liệu được ghi là “Đã đặc tả — chưa xác minh triển khai”. Báo cáo này phản ánh bằng chứng quan sát được trên branch tại ngày cập nhật, không thay thế kết quả chạy test/CI.

## PC-1 — 11/11/2026
### 1.1. Tiến độ theo acceptance criteria
| Mã | Trạng thái | Bằng chứng trên branch | Ghi chú |
| --- | --- | --- | --- |
| B-01 | Đang | artifacts/REQUIREMENTS.md FR-01, FR-02; artifacts/DECISIONS.md ADR-01, ADR-08 | Đã đặc tả việc tích hợp vào luồng học tập và type estimate; chưa có mã nguồn frontend để xác minh tích hợp. |
| B-02 | Đang | artifacts/REQUIREMENTS.md mục 8; artifacts/TEST_PLAN.md mục 4 | Đã đồng bộ danh sách 12 fixture trong REQUIREMENTS.md và TEST_PLAN.md. TEST_REPORT.md ghi nhận CI ở commit starter be5da68... có test 12 fixture PASS; chưa khẳng định bộ fixture đã được nạp vào ứng dụng. |
| B-03 | Xong (đặc tả) | artifacts/DECISIONS.md ADR-03; artifacts/TEST_PLAN.md mục 3 | Đã quy định L = ceil(0.9 * R), U = floor(1.1 * R), chấp nhận L <= E <= U; có ví dụ phép nhân, phép chia và giá trị biên. Chưa xác minh bằng test tự động. |
| B-04 | Đang | artifacts/REQUIREMENTS.md FR-08; artifacts/DECISIONS.md ADR-02, ADR-05 | Đã đặc tả không trả đáp án/cận chấm điểm trước khi nộp; chưa có bằng chứng kiểm thử JSON API thực tế. |
| B-05 | Đang | artifacts/REQUIREMENTS.md FR-09; artifacts/DECISIONS.md ADR-05, ADR-06 | Đã mô tả lưu hai câu trả lời trong attempts.answers_json; chưa xác minh triển khai, truy xuất sau refresh hoặc cách ly dữ liệu người dùng. |
| B-06 | Đang | artifacts/REQUIREMENTS.md FR-06, FR-07; artifacts/DECISIONS.md ADR-04; artifacts/TEST_PLAN.md mục 5–6 | Đã đặc tả chấm điểm 50% + 50% và bốn tổ hợp đúng/sai; chưa có mã chấm điểm/feedback được xác minh. |
| B-07 | Đang | artifacts/REQUIREMENTS.md mục 4.2; artifacts/DECISIONS.md ADR-09 | Đã xác định phạm vi không sửa xác thực/session và route ngoài phạm vi; cần đối chiếu diff mã nguồn khi có phần triển khai. |
| B-08 | Đang | artifacts/TEST_PLAN.md mục 6–8 | Đã lập test case TC-01 đến TC-24; chưa có bằng chứng các test này đã được tự động hóa và chạy. |
| B-09 | Chưa | Chưa có bằng chứng npm test trong các file của thư mục nộp bài | Cần bổ sung script test và xác minh chạy được từ checkout sạch. |
| B-10 | Chưa | Chưa có workflow CI/test được xác minh trong thư mục nộp bài | Cần workflow chạy cài đặt phụ thuộc và npm test trên Pull Request, kèm kết quả xanh. |
| B-11 | Đang | artifacts/REQUIREMENTS.md mục 4.2, NFR và mục 9 | Đã nêu yêu cầu dùng dữ liệu tổng hợp và không đưa secret/PII; chưa có checklist rà soát và bằng chứng kiểm tra toàn bộ nội dung nộp. |
| B-12 | Đang | artifacts/REQUIREMENTS.md NFR-06; artifacts/TEST_PLAN.md mục 7 | Đã nêu yêu cầu nhãn, thông báo lỗi, bàn phím và không chỉ dùng màu sắc; chưa có kiểm thử accessibility trên giao diện thực tế. |
### 1.2. Sửa đổi bắt buộc từ Checkpoint 1
| Yêu cầu | Trạng thái | Bằng chứng / việc còn lại |
| --- | --- | --- |
| DEC-03: công thức xác định L, U cho phép nhân/chia | Xong về đặc tả | artifacts/DECISIONS.md ADR-03 và artifacts/TEST_PLAN.md mục 3; công thức và hai ví dụ số đã được ghi rõ. |
| Bổ sung 12 fixture tổng hợp | Đang | Đã đồng bộ hai bảng theo bộ chuẩn tại REQUIREMENTS.md mục 8. CI của starter ghi nhận test 12 fixture PASS; cần giữ đường dẫn fixture thực tế nhất quán với mã nguồn. |
| Bổ sung dữ liệu cụ thể cho TC-05 đến TC-13 | Xong về đặc tả | artifacts/TEST_PLAN.md mục 6.2–6.4 có E, A, khoảng hợp lệ và kết quả mong đợi. |
| Làm rõ chấm điểm khi chỉ đúng một thành phần; ảnh hưởng progress/sao | Xong về đặc tả | artifacts/DECISIONS.md ADR-04, ADR-07; artifacts/REQUIREMENTS.md FR-06, FR-10; artifacts/TEST_PLAN.md mục 5. |
### 1.3. Timeline và đối chiếu tiến độ
| Công việc | Mốc kế hoạch | Trạng thái tại 17/11/2026 | Bằng chứng / ghi chú |
| --- | --- | --- | --- |
| Hoàn thiện luồng estimate trên giao diện | 15/11/2026 | Chưa xác minh | Branch nộp bài hiện chưa có file mã nguồn frontend thay đổi. |
| Triển khai API chấm điểm, lưu câu trả lời và cập nhật tiến độ | 15/11/2026 | Chưa xác minh | Chưa có file mã nguồn backend trong danh sách thay đổi của thư mục nộp bài. |
| Đồng bộ 12 fixture và bổ sung test tự động | 17/11/2026 | Chưa hoàn thành theo bằng chứng hiện có | Hai bảng fixture đang không thống nhất; chưa thấy fixture JSON hoặc test tự động. |
| CI, bảo mật và accessibility | 18/11/2026 | Chưa xác minh | Chưa có bằng chứng workflow xanh, checklist bảo mật hoặc kết quả accessibility. |
| Hoàn thiện báo cáo và tài liệu bàn giao | 19/11/2026 | Đang | Đã có REQUIREMENTS, DECISIONS, TEST_PLAN; các deliverable còn lại được liệt kê tại mục 2.3. |
| PR nộp bài và validate cấu trúc | Trước 11:30 ngày 18/11/2026 | Đã mở PR #37; bot xác nhận bài hợp lệ về cấu trúc | PR đang mở, chưa merge; chờ giảng viên/TA review nội dung. |
| Chốt tag RC và PR nộp cuối | Trước 23:59 ngày 19/11/2026 | Chưa thực hiện | Tag dự kiến: bkt-2026-33-rc1; cần cập nhật SHA và kết quả CI sau khi tạo tag. |
### 1.4. Rủi ro / vấn đề đang vướng
Thiếu bằng chứng triển khai: So sánh branch với main cho thấy các thay đổi trong thư mục nhóm hiện tập trung ở tài liệu; chưa có thay đổi mã nguồn frontend/backend để chứng minh tính năng đã chạy.
Fixture: Danh sách 12 fixture trong REQUIREMENTS.md và TEST_PLAN.md đã được đồng bộ trong lần cập nhật 17/11/2026. CI ở starter commit be5da68... ghi nhận kiểm thử fixture PASS.
Test/CI: TEST_REPORT.md ghi nhận npm ci và npm test thành công, 5 passed/0 failed tại starter commit be5da68...; kết quả này không thay thế kiểm thử tích hợp đầy đủ.
Deliverable: Đã có TEST_REPORT.md, SECURITY_PRIVACY_CHECKLIST.md, AI_USE.md, CONTRIBUTIONS.md và README trong thư mục nộp bài. Slide/demo hoàn chỉnh chưa được xác minh.
Metadata: submission.json và source-ref.json hiện nằm ở thư mục gốc submissions/hoang_mai_toan_33/; đã có mã nhóm, mã bài, MSSV và tham chiếu starter/commit/CI.
Bản sao trong thư mục bài nộp được giữ đồng bộ với file tiến độ tại thư mục gốc repository: `progress/PROGRESS.md`.
### 1.5. Câu hỏi cần xác nhận với giảng viên
Q1: Với câu hỏi estimate, correct_count chỉ tăng khi cả ước lượng và kết quả chính xác đều đúng, còn score_percent vẫn cộng điểm thành phần 50% + 50% — cách hiểu này có đúng với quy ước thống kê của bài không?
Q2: 12 fixture phải được nạp vào dữ liệu câu hỏi của ứng dụng hay có thể được quản lý trong bộ test tự động, miễn là có cấu trúc và tái lập được?
### 1.6. Phân công theo vai trò
| Alias / vai trò | Đầu việc | Commit / bằng chứng |
| --- | --- | --- |
| Lead | Điều phối, theo dõi acceptance criteria, tích hợp và chuẩn bị PR/tag | Chưa gắn alias và commit cụ thể |
| BE | API estimate, xác thực đầu vào, chấm điểm, lưu attempts/progress | Chưa có commit mã nguồn được xác minh |
| FE | Giao diện hai ô nhập, gửi câu trả lời và hiển thị feedback | Chưa có commit mã nguồn được xác minh |
| QA | Đồng bộ fixture, test tự động, kiểm thử biên/hồi quy, CI và bảo mật | Có kế hoạch tại artifacts/TEST_PLAN.md; chưa có kết quả chạy |
| DOCS | REQUIREMENTS, DECISIONS, TEST_PLAN và tài liệu bàn giao | artifacts/REQUIREMENTS.md, artifacts/DECISIONS.md, artifacts/TEST_PLAN.md |
Bảng trên giữ alias theo vai trò để tránh tự gán người hoặc commit khi chưa có dữ liệu xác minh. Nhóm cần thay bằng alias thực tế và commit tương ứng trước khi nộp bản cuối.

