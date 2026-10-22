# notes.md — quyết định kỹ thuật & error log · nhóm 1 (SaoCungDuoc)

## Thiết kế hiện hành — bản review 22/10/2026

- **RQ:** theo nguyên văn cô đề xuất, có điều kiện cùng model/cấu hình/ngân sách; thêm RQ phân tích input, tiền điều kiện và oracle. Canonical: [rq-validation](team-synthesis/rq-validation.md).
- **Quyết định người dùng:** DeepSeek-V4.1-Flash-1017 qua DeepSeek API chính thức; tổng chi phí API tối đa 3 USD, gồm pilot/main/retry. API ID là alias `deepseek-flash`, không phải snapshot bất biến.
- **Mục 1:** 60 nguồn = 42 INCLUDE lịch sử + 18 nguồn nền, thêm GV-18/PDF60; giữ PRISMA 42 và 59 dòng điểm nền. Năm rq-check có phần hiện hành và lịch sử; chưa systematic search/screening mới hoặc tái chấm cả tập cũ.
- **Mục 2:** [experiment-design](team-synthesis/experiment-design.md), hai prompt C/I, config, manifest tĩnh 106/228 và lịch dự kiến 660 slot. R=3 là phương án nguồn lực cần review, không bảo đảm power. Envelope 16k input/2048 output off-peak cho 660 call là 2.395008 USD trước retry; chưa đo token thật.
- **Trạng thái:** chỉ tài liệu/design artifacts. Chưa runner, budget guard, environment lock, golden tests, pilot hoặc gọi DeepSeek. Không commit/push. Dừng trước bước 3 để người dùng review.
- **Cần xác minh trước main:** tokenizer/cost upper bound và giá hiện hành, model mapping, môi trường/reset/patch/evaluator/mất output, request-cap instrumentation, pilot và độ biến động, hai người chấm độc lập/deadline. Không điền dữ liệu giả vào phần thiếu.
- **Giữ nguyên:** precise/golden/mutant không là đầu vào LLM; một test/requirement/arm/run, single-step; cùng hướng dẫn assertion gốc; metric pass-valid/fail-mutant và mẫu số manifest.

## Lịch sử — thử khả thi RQ FA26-EXT-12 trước đổi hướng (không còn là thiết kế hiện hành)

Các mục 45 yêu cầu, không dùng LLM và oracle tự xây dưới đây thuộc hướng EP+BVA truyền thống so với random; giữ để truy vết, không dùng làm yêu cầu chạy hiện tại.

1. **Dữ liệu**: clone `github.com/casablancahotelsoftware/RESTestBench`; khóa commit, kiểm kê requirements + mutants, mở 1 yêu cầu kiểm định dạng. Đủ 45 yêu cầu (**16 FastAPI + 15 RealWorld + 14 TodoApp**, thống nhất 20/10/2026)? → ⬜ kết quả thật: snapshot + danh sách ID + số mutant thực tế + ✅/❌; chưa chạy kiểm chứng.
2. **Công cụ đo chạy được**: Docker Desktop (WSL2); dựng 3 dịch vụ; chạy thử 1 ca; xem công cụ repo tính mutation score. → ⬜ kết quả thật
3. **LLM**: RQ không dùng LLM → N/A (can thiệp là kỹ thuật không AI).
4. **Chỉ số tính được**: oracle requirements-based trả pass/fail cho mutant trên 1 yêu cầu mẫu? → ⬜ kết quả thật
5. **Tài liệu đủ?**: chạy String A trên 1 CSDL, lướt tiêu đề đếm ≥ 12 paper gần chủ đề? → ⬜ kết quả thật (ghi luôn vào search-log người chạy)
6. **Nhóm làm nổi?**: Docker + thống kê + thời gian — tự đánh giá. → ⬜ kết quả thật
→ **Kết luận: GIỮ RQ / ĐỔI RQ** (❌ ở câu 1–3 → huỷ đăng ký, đổi RQ ngay). Ngày: ⬜___

## Lịch sử — ghi chú W7 về ngưỡng & kiểm định của thiết kế cũ (giữ để truy vết)
- Tiêu chí chấp nhận thực tiễn (KHÔNG nằm trong H0): ngưỡng θ xác định bằng mini-pilot 5–10 mẫu — chốt TRƯỚC lần chạy chính, báo cáo kèm khoảng tin cậy 95%.
- ⚠️ Chốt lại cho khớp: form ghi "θ sẽ xác định bằng mini-pilot" nhưng ô "nguồn ngưỡng" chọn "Case 1: paper trích dẫn" → chọn 1 hướng (mini-pilot → Case 3; theo paper → Case 1 + con số cụ thể).
- Đề xuất ở thiết kế cũ: tổng hợp 10 lượt thành một giá trị/kỹ thuật/requirement rồi ghép cặp theo requirement; Wilcoxon–Holm còn phụ thuộc giả định. Gợi ý cũ dùng Mann–Whitney U mặc định cho các lượt đã bỏ vì không xét cấu trúc ghép cặp; chưa có kết quả kiểm định/CI/power. Kế hoạch hiện hành ba run còn phải khóa theo [rq-validation §4](team-synthesis/rq-validation.md#4-khả-thi-của-gap-đang-cân-nhắc).

## Nhật ký quyết định
- 02/10/2026 — Nhóm chốt RQ FA26-EXT-12 ("Giá trị biên vs ngẫu nhiên trên mutant REST API"); tạo repo RT-SWT302-001-SaoCungDuoc; chốt vai + chia nguồn (A0).
- 02/10/2026 — Đăng ký RQ thành công trên hệ thống (nhóm 1).
- 20/10/2026 — Thống nhất mẫu P 45 yêu cầu gần cân bằng: 16 FastAPI + 15 RealWorld + 14 TodoApp, thay 15/dịch vụ. Sửa rq-validation theo đối chiếu nguồn; chưa khóa artifact/ID/B/miền random hoặc chạy pilot; chưa xác minh cập nhật thẻ/GV. Nhật ký chi tiết tại lam/SLR/search-log.md.
- 21/10/2026 — Commit `6658a63de7250dd7a41bbd6d140b3cdb3f9f5f51` trên nhánh Lam đổi RQ/gap sang prompt-guided EP+BVA vs single-step, P = 106 vague. Đợt đồng bộ tài liệu tiếp theo sửa bảng căn hàng, số lượt, định nghĩa outcome và giới hạn bằng chứng; người dùng chọn giữ điểm nền, chỉ ghi rõ chỗ chưa đồng nhất. Chưa chạy thí nghiệm hoặc xác minh GV phê duyệt.

- 22/10/2026 — Theo người dùng cho phép, cập nhật mục 1 bằng skill experimental-design, bổ sung GV-18 và protocol RQ mới, bảo toàn điểm/screening cũ; tiếp đó soạn mục 2 với DeepSeek-V4.1-Flash-1017/API chính thức/3 USD. Chỉ tạo hồ sơ để review; chưa làm bước 3/golden/pilot/main, chưa chi phí DeepSeek. Chi tiết nguồn/thay đổi ở search-log §11–12.
