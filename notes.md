# notes.md — quyết định kỹ thuật & error log · nhóm 1 (SaoCungDuoc)

## Thiết kế hiện hành — đồng bộ tài liệu 21/10/2026

- **RQ:** prompt có hướng dẫn EP+BVA so với prompt single-step gốc trên **106 yêu cầu vague** của RESTestBench (63 FastAPI + 29 RealWorld + 14 TodoApp), outcome **MS_φ**, cùng model/temperature, ba run. Xem [rq-validation §1](team-synthesis/rq-validation.md).
- **Khối lượng full dự kiến:** 636 lượt sinh test, 636 lượt kiểm valid, 1.368 lượt mutant (684/arm), trước setup/reset/retry; không phải số lượt đã chạy.
- **Giữ nguyên:** evaluator/harness, một test/requirement/run/arm, không gọi SUT lúc sinh, cùng hướng dẫn assertion; model vẫn sinh assertions, golden tests không làm đáp án cho LLM.
- **Chưa chốt:** prompt I, model/cấu hình cụ thể, môi trường, xử lý lỗi/retry, phân tích cụm requirement/ba run, CI/kiểm định, phân công và thời gian. Bootstrap/McNemar đang là phương án, không phải kế hoạch đã được duyệt; không dùng 10 lượt/Wilcoxon–Holm của thiết kế cũ làm mặc định.
- **Chưa thực hiện:** Docker/golden tests, pilot, LLM hoặc thí nghiệm; chưa có kết quả và chưa xác minh thẻ/GV duyệt. Con số 15 mutant là thông tin email GV, chưa có ID hoặc phân loại độc lập của nhóm.

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
