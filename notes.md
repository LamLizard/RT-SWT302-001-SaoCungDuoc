# notes.md — quyết định kỹ thuật & error log · nhóm 1 (SaoCungDuoc)

## Thử khả thi RQ FA26-EXT-12 (làm thật — hạn cứng: chậm nhất buổi 2)
1. **Dữ liệu**: clone `github.com/casablancahotelsoftware/RESTestBench`; khóa commit, kiểm kê requirements + mutants, mở 1 yêu cầu kiểm định dạng. Đủ 45 yêu cầu (**16 FastAPI + 15 RealWorld + 14 TodoApp**, thống nhất 20/10/2026)? → ⬜ kết quả thật: snapshot + danh sách ID + số mutant thực tế + ✅/❌; chưa chạy kiểm chứng.
2. **Công cụ đo chạy được**: Docker Desktop (WSL2); dựng 3 dịch vụ; chạy thử 1 ca; xem công cụ repo tính mutation score. → ⬜ kết quả thật
3. **LLM**: RQ không dùng LLM → N/A (can thiệp là kỹ thuật không AI).
4. **Chỉ số tính được**: oracle requirements-based trả pass/fail cho mutant trên 1 yêu cầu mẫu? → ⬜ kết quả thật
5. **Tài liệu đủ?**: chạy String A trên 1 CSDL, lướt tiêu đề đếm ≥ 12 paper gần chủ đề? → ⬜ kết quả thật (ghi luôn vào search-log người chạy)
6. **Nhóm làm nổi?**: Docker + thống kê + thời gian — tự đánh giá. → ⬜ kết quả thật
→ **Kết luận: GIỮ RQ / ĐỔI RQ** (❌ ở câu 1–3 → huỷ đăng ký, đổi RQ ngay). Ngày: ⬜___

## ⬜ Dành cho W7 — Ngưỡng & kiểm định (đừng xoá)
- Tiêu chí chấp nhận thực tiễn (KHÔNG nằm trong H0): ngưỡng θ xác định bằng mini-pilot 5–10 mẫu — chốt TRƯỚC lần chạy chính, báo cáo kèm khoảng tin cậy 95%.
- ⚠️ Chốt lại cho khớp: form ghi "θ sẽ xác định bằng mini-pilot" nhưng ô "nguồn ngưỡng" chọn "Case 1: paper trích dẫn" → chọn 1 hướng (mini-pilot → Case 3; theo paper → Case 1 + con số cụ thể).
- Kiểm định cho thiết kế hiện hành: xem [rq-validation §1.2](team-synthesis/rq-validation.md). Đề xuất tổng hợp 10 lượt thành một giá trị/kỹ thuật/requirement rồi ghép cặp theo requirement; Wilcoxon–Holm còn phụ thuộc giả định và kế hoạch phải khóa trước chạy chính. Gợi ý cũ dùng Mann–Whitney U mặc định cho các lượt đã bỏ vì không xét cấu trúc ghép cặp; chưa có kết quả kiểm định/CI/power.

## Nhật ký quyết định
- 02/10/2026 — Nhóm chốt RQ FA26-EXT-12 ("Giá trị biên vs ngẫu nhiên trên mutant REST API"); tạo repo RT-SWT302-001-SaoCungDuoc; chốt vai + chia nguồn (A0).
- 02/10/2026 — Đăng ký RQ thành công trên hệ thống (nhóm 1).
- 20/10/2026 — Thống nhất mẫu P 45 yêu cầu gần cân bằng: 16 FastAPI + 15 RealWorld + 14 TodoApp, thay 15/dịch vụ. Sửa rq-validation theo đối chiếu nguồn; chưa khóa artifact/ID/B/miền random hoặc chạy pilot; chưa xác minh cập nhật thẻ/GV. Nhật ký chi tiết tại lam/SLR/search-log.md.
