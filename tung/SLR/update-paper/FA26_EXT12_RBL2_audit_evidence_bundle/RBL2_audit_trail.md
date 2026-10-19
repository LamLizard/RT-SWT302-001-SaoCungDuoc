# FA26-EXT-12 — Bằng chứng tìm kiếm và triage RBL-2

**Ngày tìm:** 18/10/2026, 16:33–16:34 (Asia/Saigon).  
**Nguồn:** Google Scholar qua SerpAPI, sử dụng RBL Paper Harvester.  
**Phạm vi:** truy vết 139 bản ghi sau loại trùng và phân biệt bước triage với bước phân tích toàn văn.

## 1. Nhật ký truy vấn

Số liệu dưới đây được ghi theo [log Harvester](RBL2_log_Harvester_trich_tu_chat.md). Không bổ sung lượt tìm kiếm ngoài log.

| Lượt | Chuỗi theo log Harvester | Nguồn/trường | Bộ lọc | Thời điểm | Hits báo | Lấy về | ID có membership trong CSV | Lượt API báo |
| --- | --- | --- | --- | --- | ---: | ---: | ---: | ---: |
| Q1 / v1 | `"RESTestBench"` | Google Scholar (SerpAPI) | `as_ylo=2025` | 18/10/2026 16:33 | 3 | 3 | 3 | 1 |
| Q2 / v2 | `("REST API" OR "RESTful API" OR "web API") ("mutation testing" OR "mutation score" OR "mutant detection" OR "mutant killing")` | Google Scholar (SerpAPI) | `as_ylo=2025` | 18/10/2026 16:33 | 62 | 100 | 72 | 5 |
| Q3 / v3 | `("REST API" OR "RESTful API" OR "web API") ("equivalence partitioning" OR "boundary value analysis" OR "boundary-value analysis" OR "boundary testing")` | Google Scholar (SerpAPI) | `as_ylo=2025` | 18/10/2026 16:34 | 90 | 82 | 68 | 5 |

Q2/Q3 trong trường `query` của CSV có thêm `AND` giữa hai khối so với log. Chưa có căn cứ xác định khác biệt do chuẩn hóa truy vấn hay do cấu hình nguồn. Q2 báo 62 hits nhưng lấy về 100 bản ghi; nguyên nhân và cấu hình phân trang/sắp xếp chưa được xác minh. Các số liệu được giữ theo log, không suy ra tổng mức bao phủ tìm kiếm.

## 2. Loại trùng và kiểm kê CSV

**Kết quả loại trùng được người phụ trách xác nhận ngày 18/10/2026:** công cụ xử lý 185 bản ghi, loại 46 bản trùng và giữ 139 bản ghi. Bước loại trùng thuộc phạm vi xử lý của người phụ trách; không yêu cầu kiểm lại 185 bản ghi như điều kiện hoàn tất hồ sơ cá nhân.

Các kiểm tra trực tiếp trên CSV:

- 139 dòng dữ liệu, 139 ID `ma` riêng biệt.
- Membership Q1/Q2/Q3: **3/72/68**; bốn ID thuộc hai lượt là NEW01, NEW02, NEW05, NEW15. Vì vậy, **3 + 72 + 68 − 4 = 139**.
- Phân bố theo truy vấn đại diện: **3/70/66**. Đây là cách đếm khác với membership.
- Không phát hiện trùng chính xác theo tiêu đề chuẩn hóa, URL hoặc DOI không rỗng. Kiểm tra này không thay thế hoặc tái dựng quy trình dedup của công cụ.
- Các trường metadata và nhãn triage được đối chiếu giữa CSV và hai workbook.

## 3. Quy tắc triage

Triage sử dụng tiêu đề và snippet, không phải đánh giá đủ IC/EC hay toàn văn. Các nhận xét ban đầu được lưu trong hai workbook để truy vết:

1. **R1-PREVIOUS-OVERRIDE:** 17 ID có nhận xét riêng, được ghi cùng căn cứ từng bản ghi trong sheet `139 bang chung` của workbook audit.
2. **R2-TITLE-REST:** tiêu đề chứa `rest api`, `restful api`, `restful web` hoặc `web api testing`, chưa thuộc R1.
3. **R3-NO-DIRECT-MATCH:** các bản ghi còn lại, chưa có đủ tín hiệu để ưu tiên theo bài toán và thước đo của RQ.

| Nhãn triage ban đầu | Số bản ghi | Phạm vi diễn giải |
| --- | ---: | --- |
| ƯU TIÊN 1 | 1 | Ưu tiên kiểm tra nguồn công bố và toàn văn. |
| DỰ PHÒNG | 2 | Ứng viên bổ sung trong CSV. |
| LIÊN QUAN GIÁN TIẾP | 14 | Chỉ có liên hệ phương pháp hoặc bối cảnh từ metadata/snippet. |
| CẦN KIỂM NẾU CÒN THIẾU | 4 | Cần kiểm abstract chính thức trước khi quyết định toàn văn. |
| CHƯA ƯU TIÊN | 118 | Chưa phải quyết định EXCLUDE theo IC/EC. |
| **Tổng** | **139** | Phân bố triage, không phải số included/excluded của PRISMA. |

Sheet `139 bang chung` trong [workbook audit](RBL2_bang_chung_tim_kiem_va_sang_loc.xlsx) lưu chỉ số dòng CSV, ID, membership, query, tiêu đề/snippet, năm, DOI/URL, nhãn, quy tắc và căn cứ triage. Các trường metadata gốc được giữ nguyên; NEW04 được cập nhật kết quả đọc toàn văn.

## 4. Phân tích toàn văn và nguồn phát hiện

| Nghiên cứu | Nguồn phát hiện | Lựa chọn sau toàn văn | Căn cứ và giới hạn |
| --- | --- | --- | --- |
| [RESTestBench](../R2R-01-RESTestBench-2026.pdf) | SEED-S1, ngoài CSV | Chính | Đúng benchmark, oracle và requirements-based mutation metric; arXiv 28/04/2026, EASE 2026 AI Models / Data. Chưa so EP+BVA với uniform random. |
| [MioHint](../R2R-02-MioHint-2026.pdf) | NEW04, Q2 | Chính | ICSE 2026 Research Track, trình bày 16/04/2026; v4 ngày 05/03/2026. V1 ngày 08/04/2025 ngoài cửa sổ; xét bản conference 2026 theo lựa chọn của người phụ trách. Table 1 có 16 SUT, Table 2 báo kết quả chính của 8 SUT. Đo request mutation/coverage, không đo killed program mutants. |
| [RESTOR](../R2R-03-RESTOR-2026.pdf) | SEED-S3, ngoài CSV | Chính | arXiv 27/07/2026, được chấp nhận tại ISSTA 2026; dữ liệu công nghiệp và đánh giá oracle. Một lần training/evaluation, không công khai source/data/model. |
| [Prompt-Based REST API Test Amplification in Industry](../R2R-04-Prompt-Based-REST-API-Test-Amplification-in-Industry-2026.pdf) | SEED-S2, ngoài CSV | Dự phòng | arXiv 25/01/2026; 1 microservice, 6 endpoints, đo API coverage và công sức tích hợp. Venue chính thức chưa xác minh. |
| NEW71 | Q2, trong CSV | Ứng viên dự phòng ban đầu | Chỉ có metadata/snippet trong bộ dữ liệu, chưa có toàn văn để đối chiếu đầy đủ. |

Các seed ngoài CSV không được cộng vào 139 hoặc gán cho Q1–Q3. Các phiên bản arXiv/conference của cùng nghiên cứu được tính là một nghiên cứu. [rq-check §2](../../rq-check.md#2-tìm-kiếm-bổ-sung-và-rà-12-tháng-gần-nhất) là nguồn phân tích P/I/C/O/S, dẫn chứng hạn chế và kết luận cá nhân hiện tại.

## 5. Giới hạn kết luận

- 139 bản ghi chưa được đánh giá toàn văn toàn bộ; nhãn triage không phải kết quả IC/EC.
- Có 41 bản ghi năm 2025, 95 năm 2026 và 3 thiếu năm. Bộ lọc `as_ylo=2025` không tự xác nhận ngày công bố trong cửa sổ 12 tháng.
- 104/139 bản ghi thiếu DOI; 135/139 có trường `abstract`, phần lớn là snippet bị cắt.
- Chênh lệch Q2 62/100, cách ghi `AND` và cấu hình phân trang/sắp xếp chưa được giải thích. Các giới hạn này không phủ nhận xác nhận dedup của người phụ trách.
- Ba bài chính là lựa chọn có căn cứ trong tập tài liệu đã tiếp cận, không phải kết luận đã bao quát toàn bộ nghiên cứu gần đây.
- Đợt Google Scholar/SerpAPI không tính vào PRISMA theo [review protocol §3](../../../../team-synthesis/review-protocol.md#3-phạm-vi-tìm).

## 6. Đối chiếu hồ sơ

[README](README.md) trình bày vai trò các tệp trong bộ hồ sơ. CSV lưu metadata/snippet nguồn; workbook triage ban đầu lưu nhận xét sơ bộ; workbook audit bổ sung quy tắc, căn cứ từng bản ghi và kết quả lựa chọn toàn văn.

Có thể kiểm tra tính nhất quán bằng cách đối chiếu ID, các trường metadata, membership và nhãn triage giữa CSV và hai workbook. Phép đối chiếu này không thay thế xác nhận loại trùng của người phụ trách hoặc đánh giá IC/EC từ toàn văn.
