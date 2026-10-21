# Review Protocol — nhóm 1 (SaoCungDuoc) · RQ FA26-EXT-12

Mọi thay đổi sau khi ban hành: ghi vào search-log.md kèm lý do + ngày (không sửa lặng lẽ).

## 1. Câu hỏi nghiên cứu

- RQ (VN): Trên 106 yêu cầu bản vague của RESTestBench, prompt có hướng dẫn kỹ thuật EP+BVA và prompt single-step gốc của benchmark khác nhau thế nào về MS_φ, khi dùng cùng một mô hình ngôn ngữ và cùng temperature?
- H0 (phát biểu định hướng, đặc tả kiểm định cần khóa trước chạy chính): Không có khác biệt về MS_φ giữa prompt có hướng dẫn EP+BVA và prompt single-step gốc, với cùng mô hình, cùng temperature và cùng 106 yêu cầu.
- H1 (phát biểu định hướng): Có khác biệt về MS_φ giữa hai prompt dưới cùng điều kiện.
- PICO: P = **106 yêu cầu bản vague** của RESTestBench (**63 FastAPI + 29 NestJS RealWorld + 14 TodoApp**) · I = prompt có hướng dẫn EP+BVA · C = prompt single-step gốc của benchmark · O = **MS_φ** trên 228 mutant · S = cùng model, cùng temperature, 3 lần chạy, so sánh paired theo requirement.

Nhãn `extension` theo bảng căn hàng GV-02/RESTestBench: P/C/O trùng, I khác. Thiết kế hiện hành và các điều kiện chưa khóa: [rq-validation §1](rq-validation.md). Chưa có pilot; chưa xác nhận thay đổi P đã được cập nhật trên thẻ/GV.

## 2. Nguồn & phân công
| Thành viên | Nguồn |
|---|---|
| Tung | IEEE Xplore |
| Lam | ACM Digital Library |
| Khoi | OpenAlex |
| T.Duy | Semantic Scholar + Google Scholar (seed & bổ sung) |
| K.Duy |Springer |

## 3. Phạm vi tìm

- Trường tìm: Title / Abstract / Keywords
- Khoảng năm: từ 2020 (theo IC-Y)
- **String A (CHÍNH THỨC — dán nguyên văn, giữ đủ ngoặc/ký tự):** ("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing") AND ("fault detection" OR "mutant detection" OR "bugs found")
- String B/C (dùng khi cần nới — giữ bản nháp cũ làm dự phòng, bổ sung từ đồng nghĩa khi chạy): ("REST API" OR "RESTful API" OR "web API" OR "web service") AND ("boundary value analysis" OR "boundary value" OR "boundary testing" OR "equivalence partitioning") AND ("mutation testing" OR "mutants" OR "mutation score")
- Quy tắc chạy: >500 kết quả → AND thêm tên dataset ("RESTestBench"); <20 → bỏ khối O trước; ghi MỌI phiên bản chuỗi + số kết quả vào search-log.
- Chạy chính để đếm: IEEE / ACM / OpenAlex. Google Scholar & Semantic Scholar KHÔNG đếm vào PRISMA.

## 4. Tiêu chí lọc

Theo `team-synthesis/ie_criteria.md`, với quy trình bổ sung sau:

- Bước 1: thu thập `01_all_records.csv` từ các query chính; trước khi screening, bỏ trùng theo DOI (nếu thiếu DOI thì theo title + năm); giữ một bản ghi cho mỗi paper.
- Bước 2: vòng 1 screening trên title + abstract; mỗi record gán `v1_decision` = `INCLUDE / EXCLUDE / Unsure` và `v1_reason` theo mã IC/EC.
- Bước 3: vòng 2 screening trên full-text; chỉ xét record có `INCLUDE` hoặc `Unsure` ở V1; gán `v2_decision` và `v2_reason`.
- Bước 4: snowballing áp dụng cùng quy trình V1–V2; record mới được thêm vào PRISMA như record bình thường và không được bỏ qua.
- Bước 5: kiểm chéo 20% số paper hoặc tối thiểu 1 paper per reviewer/ vòng; ghi vào `search-log.md` kèm ngày và lý do.

PRISMA đầu ra theo thứ tự: `01_all_records.csv` → `02_after_screening_v1.csv` → `03_final_included.csv`.

## 5. Cột Evidence Table

Paper (tên + năm + venue + DOI) · Tool/LLM · Dataset · Metric · Kết quả · Code · Hạn chế · Gần RQ.

## 6. Xử lý bất đồng

- Lọc: lưỡng lự ghi Unsure ở V1; bất đồng nhiều → PL làm rõ IC/EC cho cả nhóm.
- Trích xuất: lệch > 10% số ô được kiểm → người trích xuất rà lại toàn bộ bảng; không tự thống nhất được → hỏi PL.

## 7. Mốc thời gian

- Ngày dừng search: **23:59 05/10/2026** · Snowballing: Ngày 3–4 (1 vòng bắt buộc, tối đa 2) · Screening xong: Ngày 4 · Evidence table + kiểm chéo: Ngày 4–5 · Gộp nhóm: cuối tuần.
