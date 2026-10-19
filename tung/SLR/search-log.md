# Search log — Tùng · IEEE Xplore và snowballing

Nhóm SaoCungDuoc · RQ FA26-EXT-12 · Đợt tìm mới 12–13/10/2026, múi giờ **Asia/Saigon (UTC+7)**. Matching ngày **13/10/2026**; kết hợp log IEEE với catalog và full-text screening snowball từ công cụ khác.

## Cách chạy và đọc số

- Bảng chính gồm **5 lượt tìm kiếm**: A đầy đủ → A bỏ Outcome → B/C bỏ Outcome → mở rộng biến thể EP/BVA → mở rộng sinh/kiểm thử REST API. Các lượt chạy trùng và đối chiếu mọi năm không tạo dòng search bổ sung.
- Nguồn tìm kiếm là **IEEE API**, dùng `querytext`, không gắn trường riêng. Giữ bộ lọc từ năm **2020** ở cả 5 lượt; loại ấn phẩm được xét khi screening.
- “Số kết quả” là số bài tìm được trong phạm vi từ 2020. “Số sau bỏ trùng” là số paper duy nhất **trong từng lượt**; số paper mới và tổng tích lũy được trình bày ở phần tổng hợp.
- Ghi chú nêu kết quả của từng lượt và lý do điều chỉnh search string cho lượt tiếp theo.

## Bảng log chính

| # | Query đã sử dụng | CSDL | Trường tìm | Bộ lọc thực tế | Ngày | Số kết quả | Số sau bỏ trùng | Ghi chú |
| :--- | :--- | :--- | :--- | :--- | :--- | ---: | ---: | :--- |
| **Q1** | `("REST API testing" OR "natural language requirement" OR "RESTestBench")`<br>`AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing")`<br>`AND ("fault detection" OR "mutant detection" OR "bugs found")` | IEEE API | `querytext` | Từ 2020 | 12/10/2026 | **0** | **0** | String A đầy đủ không tìm thấy kết quả; bỏ khối Outcome theo quy tắc dưới 20 kết quả. |
| **Q2** | `("REST API testing" OR "natural language requirement" OR "RESTestBench")`<br>`AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing")` | IEEE API | `querytext` | Từ 2020 | 12/10/2026 | **0** | **0** | String A bỏ Outcome vẫn không tìm thấy kết quả; chuyển sang String B/C bỏ Outcome để mở rộng từ đồng nghĩa. |
| **Q3** | `("REST API" OR "RESTful API" OR "web API" OR "web service")`<br>`AND ("boundary value analysis" OR "boundary value" OR "boundary testing" OR "equivalence partitioning")` | IEEE API | `querytext` | Từ 2020 | 12/10/2026 | **2** | **2** | Thu được 2 bài; bổ sung biến thể và thuật ngữ gần cho khối P/I để tăng độ phủ tìm kiếm, giữ nguyên năm tối thiểu và IC/EC. |
| **Q4** | `("REST API" OR "RESTful API" OR "web API" OR "web service" OR "RESTful web service" OR "HTTP API")`<br>`AND ("boundary value analysis" OR "boundary-value analysis" OR "boundary value" OR "boundary testing" OR "equivalence partitioning" OR "equivalence class partitioning" OR "input partitioning" OR "input domain partitioning" OR "boundary analysis")` | IEEE API | `querytext` | Từ 2020 | 12/10/2026 | **2** | **2** | Mở rộng biến thể EP/BVA vẫn chỉ thu được 2 bài, trùng tập đã có; bổ sung nhánh sinh test, black-box, robustness và random testing cho REST API. |
| **Q5** | `("REST API" OR "RESTful API" OR "RESTful web service" OR "web API")`<br>`AND ("test generation" OR "test case generation" OR "test amplification" OR "black-box testing" OR "black box testing" OR "robustness testing" OR "random testing")` | IEEE API | `querytext` | Từ 2020 | 13/10/2026 | **68** | **68** | Nhánh tìm kiếm rộng thu được 68 bài; giữ chuỗi này để screening theo IC/EC và khử trùng với các lượt trước. |

## Tổng hợp đợt tìm mới

- Q1 = 0, Q2 = 0, Q3 = 2, Q4 = 2, Q5 = 68 → **72 lượt xuất hiện**, tương ứng **68 paper duy nhất** của đợt IEEE
- Hai paper `10.1109/MS.2025.3559664` và `10.1109/ACCESS.2021.3056505` đều xuất hiện ở Q3, Q4 và Q5, tạo **4 lượt xuất hiện lặp**. Số paper mới ở Q1–Q5 lần lượt là **0, 0, 2, 0, 66**; tổng tích lũy **riêng đợt IEEE** là **68**.
- Không cộng các lượt chạy trùng, lượt đối chiếu mọi năm hoặc occurrences do import V1/V2 vào tổng tìm kiếm. Tổng discovery/duplicates toàn hồ sơ chưa được manifest phục hồi; 72/4 là số lượt xuất hiện và số lặp của các search trong đợt này.
- Q5 chạy lúc 00:02:54 ngày 13/10 theo UTC+7

## Thay đổi so với protocol

1. **Q1 → Q2:** String A trả 0 kết quả; bỏ khối Outcome theo quy tắc dưới 20 kết quả.
2. **Q2 → Q3:** String A bỏ Outcome vẫn trả 0 kết quả; chuyển sang B/C bỏ Outcome để mở rộng từ đồng nghĩa.
3. **Q3 → Q4:** Thu được 2 bài; bổ sung RESTful web service, HTTP API, equivalence class partitioning, input partitioning, input domain partitioning và boundary analysis; giữ mốc năm 2020 và IC/EC.
4. **Q4 → Q5:** Mở rộng biến thể EP/BVA vẫn chỉ có 2 bài; bổ sung nhánh test generation, test amplification, black-box, robustness và random testing để tăng tập ứng viên.

## Kiểm chứng

- **Q3:** Đối chiếu IEEE thủ công: 14 bài mọi năm → **2 bài từ 2020**, khớp kết quả tool. Log nguồn trước matching dẫn raw response `raw-raw_5573fa34-e289-426d-8422-d9c986f617bc.json`, ghi `start_year=2020`, `total_records=2` và hai DOI. Raw file đó không có trong gói hiện tại;
- **Q4:** Provenance ghi đúng query mở rộng có `input partitioning` và `boundary analysis`; kết quả vẫn là **2 bài** của lượt trước.
- **Q5:** Đối chiếu IEEE: 76 bài mọi năm → **68 bài từ 2020**, khớp kết quả tool. Lượt mọi năm chỉ dùng đối chiếu; tám bài ngoài phạm vi năm không tính thành tám bài loại V1.
- Kết quả tìm kiếm và bộ lọc năm đã được kiểm tra trong quá trình thực hiện.

| Seed được ghi trong catalog nguồn | DOI | Ghi chú |
| :--- | :--- | :--- |
| A Black Box Tool for Robustness Testing of REST Services | `10.1109/ACCESS.2021.3056505` | INCLUDE hiện hành; P12/K81, P17/K84, P38/K108 có provenance forward từ seed này |
| LLM-Driven, Self-Improving Framework for Security Test Automation… | `10.1109/ACCESS.2025.3554960` | Seed discovery được giữ theo tool; quyết định screening hiện hành của seed là EXCLUDE — IC-I |
| Test Amplification for REST APIs: Using “Out-of-the-Box” Large Language Models | `10.1109/MS.2025.3559664` | Seed discovery được giữ theo tool; quyết định screening hiện hành của seed là EXCLUDE — IC-I |

| Phần đối chiếu | Số paper duy nhất | Diễn giải |
| :--- | ---: | :--- |
| Catalog IEEE ban đầu | **68** | Q1–Q5: 72 occurrences − 4 repeated hits |
| Records có provenance snowball | **99** | Unique records từ catalog đã giao; có backward và forward |
| Trùng giữa IEEE và snowball | **17** | Gộp provenance vào cùng paper, không thêm 17 records |
| Paper mới từ snowball | **82** | 99 − 17 |
| Catalog hợp nhất | **150** | 68 + 99 − 17 = 150 |
| Full-text snowball đã đánh giá | **45** | 37 EXCLUDE + 3 INCLUDE + 5 REVIEW; tất cả nối được với catalog |
| Records snowball mới chưa screening | **37** | 82 − 45; giữ NOT_REVIEWED, không tự gán EXCLUDE/EC-A |

**Ba INCLUDE thêm vào tập evidence:** P12/K81 (`10.1145/3533767.3534401`), P17/K84 (`10.1145/3597926.3598131`), P38/K108 (`10.1145/3696630.3728545`). Xem căn cứ EP/BVA và kết quả số tại [evidence-table.md](evidence-table.md). Năm REVIEW chưa tính included.

**Giới hạn truy vết:** gói chưa có raw provider log đầy đủ cho công cụ snowball thứ hai. Vì vậy chưa xác minh tổng citations/references available, số pages provider, hoàn tất từng hướng hoặc coverage forward 12 tháng. Không diễn giải thiếu log hoặc số 0 của snapshot thành không có citation. Matching records và đồng bộ quyết định không tự hoàn tất coverage snowball.

## RBL-2 — tiếp nhận kết quả và kiểm chứng full text (18/10/2026)

**Mục đích:** rà nghiên cứu trong khoảng **18/10/2025–18/10/2026** để kiểm chứng RQ FA26-EXT-12. Nguồn: Google Scholar qua SerpAPI (RBL Paper Harvester), bộ lọc `as_ylo=2025`; kiểm ngày cụ thể khi chọn bài. **Không tính vào PRISMA** theo protocol §3.

### Nhật ký tìm kiếm

Số hits/lấy về theo [log Harvester chép từ chat](update-paper/FA26_EXT12_RBL2_audit_evidence_bundle/RBL2_log_Harvester_trich_tu_chat.md); cột cuối đếm từ CSV sau dedup.

| Lượt | Query theo log Harvester | Ngày/giờ Việt Nam | Hits báo | Lấy về báo | ID có nhãn lượt tìm |
| --- | --- | --- | ---: | ---: | ---: |
| Q1 / v1 | `"RESTestBench"` | 18/10/2026 16:33 | 3 | 3 | 3 |
| Q2 / v2 | `("REST API" OR "RESTful API" OR "web API") ("mutation testing" OR "mutation score" OR "mutant detection" OR "mutant killing")` | 18/10/2026 16:33 | 62 | 100 | 72 |
| Q3 / v3 | `("REST API" OR "RESTful API" OR "web API") ("equivalence partitioning" OR "boundary value analysis" OR "boundary-value analysis" OR "boundary testing")` | 18/10/2026 16:34 | 90 | 82 | 68 |

### Dedup và sàng lọc sơ bộ

- Công cụ đã loại **46 bản trùng từ 185 bản ghi**, giữ **139 bản ghi**; kết quả loại trùng được người phụ trách xác nhận ngày 18/10/2026. Bước này thuộc phạm vi xử lý của người phụ trách, không yêu cầu kiểm lại từng cặp trùng trong hồ sơ cá nhân.
- Nhãn lượt tìm trong CSV: **3 + 72 + 68 − 4 = 139**; bốn ID thuộc hai lượt là NEW01, NEW02, NEW05, NEW15. Cột query đại diện phân bố **3/70/66**, khác cách đếm nhãn lượt tìm. Cột `phien_ban` ghi membership truy vấn, không biểu thị phiên bản arXiv. CSV có 139 ID riêng biệt, khớp ID/title/query/year/DOI với workbook.
- Ưu tiên từ title/snippet: **1 ưu tiên, 2 dự phòng, 14 liên quan gián tiếp, 4 cần kiểm thêm, 118 chưa ưu tiên**. Đây là triage, chưa phải quyết định IC/EC; “chưa ưu tiên” không đồng nghĩa EXCLUDE.

### Paper chọn đọc full text

Bốn nghiên cứu bổ sung khác nhau về tiêu đề, tác giả và định danh; chưa phát hiện trùng tiêu đề/DOI với 42 dòng bảng hợp nhất và catalog của Tùng. Các bản arXiv/conference của cùng nghiên cứu được gộp thành một đơn vị.

Các nghiên cứu được ưu tiên theo độ gần bài toán/thước đo, thiết kế đánh giá/venue, sau đó đến ngày công bố. Ba bài chính và một bài dự phòng đã được phân tích toàn văn; đối chiếu PICO/S và trích dẫn tại [rq-check §2](rq-check.md#2-tìm-kiếm-bổ-sung-và-rà-12-tháng-gần-nhất).

| Paper | Nguồn | Quyết định và lý do |
| --- | --- | --- |
| [R2R-01 · RESTestBench](update-paper/R2R-01-RESTestBench-2026.pdf) | Seed S1, ngoài 139 records | **Chọn chính**: đúng benchmark và requirements-based mutation metric; arXiv 28/04/2026. |
| [R2R-02 · MioHint](update-paper/R2R-02-MioHint-2026.pdf) | NEW04, Q2 | **Chọn chính**: ICSE 2026 Research Track, có đối chứng và 10 lần chạy; đo request mutation và coverage. Xét bản conference tháng 04/2026; v4 ngày 05/03/2026 trong cửa sổ, v1 ngày 08/04/2025 ngoài cửa sổ. |
| [R2R-03 · RESTOR](update-paper/R2R-03-RESTOR-2026.pdf) | Seed S3, ngoài 139 records | **Chọn chính**: gần oracle, có held-out evaluation và đánh giá công nghiệp; arXiv 27/07/2026. |
| [R2R-04 · Prompt-Based REST API Test Amplification in Industry](update-paper/R2R-04-Prompt-Based-REST-API-Test-Amplification-in-Industry-2026.pdf) | Seed S2, ngoài 139 records | **Dự phòng**: arXiv 25/01/2026; chỉ đo API coverage/effort, 1 microservice/6 endpoints và chưa xác nhận venue chính thức; ít gần metric của RQ hơn RESTestBench, thiết kế đánh giá hẹp hơn MioHint/RESTOR. |

**Lựa chọn trong phạm vi cá nhân — 18/10/2026:** ba bài chính là **RESTestBench, MioHint, RESTOR**; bài amplification là dự phòng. MioHint được xét theo mốc bản conference năm 2026, theo lựa chọn đã được người phụ trách xác nhận; ngày preprint đầu tiên vẫn được ghi riêng. Mỗi bài có căn cứ lựa chọn, phân tích toàn văn và đối chiếu phép đo còn thiếu so với RQ. Danh sách ưu tiên không biểu thị kết quả đánh giá toàn văn toàn bộ 139 bản ghi.

**Giới hạn:** Q2 báo 62 hits nhưng lấy 100, chưa có raw JSON để giải thích; query Q2/Q3 trong CSV có thêm `AND` so với log. Chưa xác minh sort/phân trang hoặc screening toàn bộ 139 bài. Seed ngoài CSV không cộng vào 139.

Bằng chứng từng bản ghi và quy tắc triage: [nhật ký kiểm chứng](update-paper/FA26_EXT12_RBL2_audit_evidence_bundle/RBL2_audit_trail.md) và [workbook audit](update-paper/FA26_EXT12_RBL2_audit_evidence_bundle/RBL2_bang_chung_tim_kiem_va_sang_loc.xlsx). Quan hệ sử dụng lại và bổ sung so với RESTestBench được phân tích tại [rq-check §2.3](rq-check.md#23-thành-phần-dự-kiến-kế-thừa-và-bổ-sung-so-với-restestbench). **Nhãn extension chưa được xác thực**; ý nghĩa nhãn chính thức của mã RQ và kết luận gap cấp nhóm chưa được xác minh/tổng hợp.
