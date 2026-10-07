# Evidence Table — K.Duy (SpringerLink)

*Nhóm 1 — SaoCungDuoc · RQ FA26-EXT-12 · Bản tạm ngày 07/10/2026.*

**Lưu ý:** R04 là ứng viên UNSURE, không phải bài đã xác nhận include. Chỉ có thể trích xuất thông tin công khai trên trang Springer và abstract; toàn văn là nội dung subscription trong phiên kiểm tra này. Không suy đoán số liệu hoặc thiết kế thực nghiệm chưa quan sát được.

| # | Paper (tên + năm + venue + DOI) | Tool/LLM | Dataset | Metric | Kết quả | Code | Hạn chế | Gần RQ |
|---|---|---|---|---|---|---|---|---|
| 1 — PENDING | Test Amplification for REST APIs via Single and Multi-agent LLM Systems (2026; ICTSS 2025; DOI 10.1007/978-3-032-05188-2_11) | Hệ thống LLM đơn tác tử và đa tác tử để khuếch đại test suite hiện có | Không nêu trong abstract Springer có thể truy cập | API coverage; hiệu quả phát hiện bug; chi phí tính toán; năng lượng | Abstract nêu coverage tăng và phát hiện nhiều bug nhưng không đưa con số; ghi **N/A (chưa xác minh từ toàn văn)** | Không xác minh được từ abstract/trang metadata | Chưa kiểm tra được threats/limitations trong toàn văn; phụ thuộc test suite đầu vào; kết quả số liệu chưa xác minh | Liên quan P/O và kiểm thử edge case; **chưa xác nhận EP/BVA hoặc baseline random** — chờ đọc full text và quyết định IC-I |

## Bài gần chủ đề nhưng không đưa vào evidence (đã loại theo IC-I)

**RESTest: Black-Box Constraint-Based Testing of RESTful Web APIs** (2020; ICSOC 2020; DOI [10.1007/978-3-030-65310-1_33](https://link.springer.com/chapter/10.1007/978-3-030-65310-1_33)) so sánh constraint-based testing với random testing trên 9 operations của 6 REST APIs thương mại. Bài báo cáo CBT phát hiện 4.278 failures trên cả 9 dịch vụ, còn random phát hiện 2.920 failures ở 5/9 dịch vụ. Dù RESTest có hỗ trợ boundary-value generators, toàn văn mô tả thí nghiệm chính là CBT-vs-random; không xác nhận EP/BVA là biến can thiệp. Vì vậy giữ làm tài liệu nền, không tính là study included theo IC-I hiện tại.
