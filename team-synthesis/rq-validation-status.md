# Trạng thái rq-validation — checklist review

**Cập nhật:** 20/10/2026 · **Buổi review dự kiến:** 21/10/2026.
**Tài liệu chi tiết:** [rq-validation.md](rq-validation.md). Đây là bản tóm tắt để đối chiếu cùng leader.

## 1. Đã xử lý

- Đã thống nhất P: **45 yêu cầu = 16 FastAPI + 15 RealWorld + 14 TodoApp**; giữ câu RQ và I/C/O.
- Đối chiếu điểm từng mã giữa bảng gộp và ma trận: **42 paper = 35 bài 0/4 + 6 bài 1/4 + 1 bài 2/4**; sửa điểm tổng hợp cá nhân Tùng/K.Duy.
- Sửa mâu thuẫn phản chứng, suy luận từ H0 và các khẳng định khả thi chưa có số đo; bổ sung nguồn/mục/trang.
- GAP-D: đã truy vết đoạn hạn chế trực tiếp ở **9 paper**, chưa kết luận số nhóm tác giả độc lập. RQ hiện tại không giải quyết GAP-D.
- Đồng bộ tài liệu chung và ghi [nhật ký đối chiếu](../lam/SLR/search-log.md).

**Trạng thái triển khai:** đã chỉnh tài liệu; chưa có bằng chứng generator/harness chạy đúng, chưa chạy Docker/benchmark/pilot. Chưa screening lại toàn văn 42 bài theo IC/EC.

## 2. Thiếu sót cần đối chiếu trong buổi review

- [ ] **Nhãn/thẻ/GV:** `extension` mới là nhãn làm việc theo rubric rộng (Guo 3/4); đối chiếu thẻ/phản hồi gốc và ghi nhận thay đổi P.
- [ ] **Bằng chứng tài liệu:** rà tính phù hợp IC/EC của tập 42; xác minh nguồn/điểm Req2REST-Guard; thống nhất cách dùng rubric rộng so với mức khớp đầy đủ RQ. Không coi khớp số đếm là đã xác nhận chất lượng toàn bộ nguồn.
- [ ] **Gap:** giữ GAP-T trong phạm vi tài liệu đã đối chiếu; nếu dùng số nhóm tác giả cho GAP-D thì chốt quy tắc gộp, xử lý chồng lấn tác giả/lab. Không gọi gap mạnh khi chưa đủ căn cứ.

## 3. Công việc trước lần chạy chính

| Thứ tự | Việc cần làm | Đầu ra cần có |
|---|---|---|
| 1 | Khóa dữ liệu và chọn mẫu 16–15–14; đối chiếu chênh lệch README 103/paper 106 | Commit benchmark, danh sách 45 ID, tổng mutant thực tế, quy tắc chọn mẫu/seed |
| 2 | Định nghĩa dạng yêu cầu; chọn precise hoặc vague, giữ cùng thông tin cho hai kỹ thuật | Ánh xạ ID → dạng; biến thể mô tả dùng trong thí nghiệm |
| 3 | Đặc tả EP+BVA và random | B, miền uniform, cách chọn lớp/biên, lịch seed, quy tắc budget/reset/retry/timeout và oracle |
| 4 | Triển khai hai generator/harness, dựng dịch vụ và pilot dự kiến 5 yêu cầu trên cả 3 dịch vụ | Log chạy, kiểm pass bản gốc/fail mutant, runtime và lỗi thực tế; điều chỉnh thiết kế trước chạy chính |
| 5 | Khóa kế hoạch phân tích sau pilot, trước chạy chính | Đơn vị phân tích, kiểm định phù hợp, ties/zeros/phụ thuộc, alpha/Holm, effect size, CI và θ |

**Lưu ý:** 900 = 45×2×10 là số lượt kỹ thuật–yêu cầu cho **một điều kiện mô tả**, chưa phải số HTTP executions. Nếu chạy cả precise/vague phải tính lại khối lượng. Không cộng kills qua các lượt thành số mutant riêng biệt.

## 4. Cần chốt sau buổi review

- [ ] Mỗi mục còn mở có người phụ trách và hạn hoàn thành.
- [ ] Mỗi mục đánh dấu xong có nguồn, quyết định hoặc log kiểm chứng đi kèm.
- [ ] Cập nhật quyết định vào rq-validation và nhật ký; giữ rõ phần chưa xác minh.
