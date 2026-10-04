# Review Protocol — nhóm 1 (SaoCungDuoc) · RQ FA26-EXT-12
Mọi thay đổi sau khi ban hành: ghi vào search-log.md kèm lý do + ngày (không sửa lặng lẽ).

## 1. Câu hỏi nghiên cứu
- RQ (VN): Trên 45 yêu cầu của RESTestBench, phân hoạch tương đương kết hợp phân tích giá trị biên, so với sinh dữ liệu ngẫu nhiên đồng đều cùng ngân sách, khác nhau thế nào về số mutant riêng biệt bị phát hiện theo từng dạng yêu cầu?
- H0: Số lỗi/mutant riêng biệt được oracle xác nhận (số đếm) của Phân hoạch tương đương kết hợp phân tích giá trị biên với ngân sách request cố định KHÔNG khác kỹ thuật/công cụ đối chứng không dùng AI.
- H1: Số lỗi/mutant riêng biệt được oracle xác nhận (số đếm) của Phân hoạch tương đương kết hợp phân tích giá trị biên với ngân sách request cố định khác kỹ thuật/công cụ đối chứng không dùng AI.
- ⚠️ H0/H1 trên đọc từ panel "xem H0/H1" — khi dán vào file, mở trang copy lại NGUYÊN VĂN cho chắc.
- PICO: P = 45 yêu cầu RESTestBench (15/dịch vụ) · I = EP + BVA · C = random đồng đều cùng budget · O = số mutant riêng biệt được oracle xác nhận.

## 2. Nguồn & phân công
| Thành viên | Nguồn |
|---|---|
| Tung | IEEE Xplore |
| Lam | ACM Digital Library |
| Khoi | OpenAlex |
| T.Duy | Semantic Scholar + Google Scholar (seed & bổ sung) |
| K.Duy | IEEE Xplore |

## 3. Phạm vi tìm
- Trường tìm: Title / Abstract / Keywords
- Khoảng năm: từ 2020 (theo IC-Y)
- **String A (CHÍNH THỨC — dán nguyên văn, giữ đủ ngoặc/ký tự):**
  ("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing") AND ("fault detection" OR "mutant detection" OR "bugs found")
- String B/C (dùng khi cần nới — giữ bản nháp cũ làm dự phòng, bổ sung từ đồng nghĩa khi chạy): ("REST API" OR "RESTful API" OR "web API" OR "web service") AND ("boundary value analysis" OR "boundary value" OR "boundary testing" OR "equivalence partitioning") AND ("mutation testing" OR "mutants" OR "mutation score")
- Quy tắc chạy: >500 kết quả → AND thêm tên dataset ("RESTestBench"); <20 → bỏ khối O trước; ghi MỌI phiên bản chuỗi + số kết quả vào search-log.
- Chạy chính để đếm: IEEE / ACM / OpenAlex. Google Scholar & Semantic Scholar KHÔNG đếm vào PRISMA.

## 4. Tiêu chí lọc
Theo `team-synthesis/ie_criteria.md`.

## 5. Cột Evidence Table
Paper (tên + năm + venue + DOI) · Tool/LLM · Dataset · Metric · Kết quả · Code · Hạn chế · Gần RQ.

## 6. Xử lý bất đồng
- Lọc: lưỡng lự ghi Unsure ở V1; bất đồng nhiều → PL làm rõ IC/EC cho cả nhóm.
- Trích xuất: lệch > 10% số ô được kiểm → người trích xuất rà lại toàn bộ bảng; không tự thống nhất được → hỏi PL.

## 7. Mốc thời gian
- Ngày dừng search: **23:59 04/10/2026** · Snowballing: Ngày 3–4 (1 vòng bắt buộc, tối đa 2) · Screening xong: Ngày 4 · Evidence table + kiểm chéo: Ngày 4–5 · Gộp nhóm: cuối tuần.