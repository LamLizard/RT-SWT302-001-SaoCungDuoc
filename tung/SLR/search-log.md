# Search log — Tùng · IEEE Xplore và snowballing

Nhóm SaoCungDuoc · RQ FA26-EXT-12 · Đợt tìm mới 12–13/10/2026, múi giờ **Asia/Saigon (UTC+7)**. Matching ngày **13/10/2026**; kết hợp log IEEE với catalog và full-text screening snowball từ công cụ khác.

## Cách chạy và đọc số

- Bảng chính gồm **5 lượt tìm kiếm**: A đầy đủ → A bỏ Outcome → B/C bỏ Outcome → mở rộng biến thể EP/BVA → mở rộng sinh/kiểm thử REST API. Các lượt chạy trùng và đối chiếu mọi năm không tạo dòng search bổ sung.
- Nguồn tìm kiếm là **IEEE API**, dùng `querytext`, không gắn trường riêng. Giữ bộ lọc từ năm **2020** ở cả 5 lượt; loại ấn phẩm được xét khi screening.
- “Số kết quả” là số bài tìm được trong phạm vi từ 2020. “Số sau bỏ trùng” là số paper duy nhất **trong từng lượt**; số paper mới và tổng tích lũy được trình bày ở phần tổng hợp.
- Ghi chú nêu kết quả của từng lượt và lý do điều chỉnh search string cho lượt tiếp theo.

## Bảng log chính

| # | Query đã sử dụng | CSDL | Trường tìm | Bộ lọc thực tế | Ngày | Số kết quả | Số sau bỏ trùng | Ghi chú |
|---|---|---|---|---|---|---:|---:|---|
| Q1 | `("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing") AND ("fault detection" OR "mutant detection" OR "bugs found")` | IEEE API | `querytext` | Từ 2020 | 12/10/2026 | 0 | 0 | String A đầy đủ không tìm thấy kết quả; bỏ khối Outcome theo quy tắc dưới 20 kết quả. |
| Q2 | `("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing")` | IEEE API | `querytext` | Từ 2020 | 12/10/2026 | 0 | 0 | String A bỏ Outcome vẫn không tìm thấy kết quả; chuyển sang String B/C bỏ Outcome để mở rộng từ đồng nghĩa. |
| Q3 | `("REST API" OR "RESTful API" OR "web API" OR "web service") AND ("boundary value analysis" OR "boundary value" OR "boundary testing" OR "equivalence partitioning")` | IEEE API | `querytext` | Từ 2020 | 12/10/2026 | 2 | 2 | Thu được 2 bài; bổ sung biến thể và thuật ngữ gần cho khối P/I để tăng độ phủ tìm kiếm, giữ nguyên năm tối thiểu và IC/EC. |
| Q4 | `("REST API" OR "RESTful API" OR "web API" OR "web service" OR "RESTful web service" OR "HTTP API") AND ("boundary value analysis" OR "boundary-value analysis" OR "boundary value" OR "boundary testing" OR "equivalence partitioning" OR "equivalence class partitioning" OR "input partitioning" OR "input domain partitioning" OR "boundary analysis")` | IEEE API | `querytext` | Từ 2020 | 12/10/2026 | 2 | 2 | Mở rộng biến thể EP/BVA vẫn chỉ thu được 2 bài, trùng tập đã có; bổ sung nhánh sinh test, black-box, robustness và random testing cho REST API. |
| Q5 | `("REST API" OR "RESTful API" OR "RESTful web service" OR "web API") AND ("test generation" OR "test case generation" OR "test amplification" OR "black-box testing" OR "black box testing" OR "robustness testing" OR "random testing")` | IEEE API | `querytext` | Từ 2020 | 13/10/2026 | 68 | 68 | Nhánh tìm kiếm rộng thu được 68 bài; giữ chuỗi này để screening theo IC/EC và khử trùng với các lượt trước. |

## Tổng hợp đợt tìm mới

- Q1 = 0, Q2 = 0, Q3 = 2, Q4 = 2, Q5 = 68 → **72 lượt xuất hiện**, tương ứng **68 paper duy nhất** của đợt IEEE; catalog nguồn được giữ tại [01 IEEE](extras/original-export/01_all_records.csv).
- Hai paper `10.1109/MS.2025.3559664` và `10.1109/ACCESS.2021.3056505` đều xuất hiện ở Q3, Q4 và Q5, tạo **4 lượt xuất hiện lặp**. Số paper mới ở Q1–Q5 lần lượt là **0, 0, 2, 0, 66**; tổng tích lũy **riêng đợt IEEE** là **68**.
- Không cộng các lượt chạy trùng, lượt đối chiếu mọi năm hoặc occurrences do import V1/V2 vào tổng tìm kiếm. Tổng discovery/duplicates toàn hồ sơ chưa được manifest phục hồi; 72/4 là số lượt xuất hiện và số lặp của các search trong đợt này.
- Q5 chạy lúc 00:02:54 ngày 13/10 theo UTC+7, trong khi [protocol nguồn](extras/original-export/extras/review-protocol.md) ghi `stopDate=2026-10-12`. [Protocol của bản matching](extras/review-protocol.md) ghi mốc thực tế 13/10/2026 và nguồn điều chỉnh; không đổi timestamp của lượt chạy.

## Thay đổi so với protocol

1. **Q1 → Q2:** String A trả 0 kết quả; bỏ khối Outcome theo quy tắc dưới 20 kết quả.
2. **Q2 → Q3:** String A bỏ Outcome vẫn trả 0 kết quả; chuyển sang B/C bỏ Outcome để mở rộng từ đồng nghĩa.
3. **Q3 → Q4:** Thu được 2 bài; bổ sung RESTful web service, HTTP API, equivalence class partitioning, input partitioning, input domain partitioning và boundary analysis; giữ mốc năm 2020 và IC/EC.
4. **Q4 → Q5:** Mở rộng biến thể EP/BVA vẫn chỉ có 2 bài; bổ sung nhánh test generation, test amplification, black-box, robustness và random testing để tăng tập ứng viên.

Các query mở rộng phục vụ thu thập ứng viên; paper vẫn cần đạt IC/EC khi screening. Bản export gốc được lưu tại [search-log-export-original.md](extras/original-export/extras/search-log-export-original.md).

## Kiểm chứng

- **Q3:** Đối chiếu IEEE thủ công: 14 bài mọi năm → **2 bài từ 2020**, khớp kết quả tool. Log nguồn trước matching dẫn raw response `raw-raw_5573fa34-e289-426d-8422-d9c986f617bc.json`, ghi `start_year=2020`, `total_records=2` và hai DOI. Raw file đó không có trong gói hiện tại; provenance còn truy được qua [origins.csv](extras/origins.csv).
- **Q4:** Provenance ghi đúng query mở rộng có `input partitioning` và `boundary analysis`; kết quả vẫn là **2 bài** của lượt trước. Query được lưu trong [origins.csv](extras/origins.csv).
- **Q5:** Đối chiếu IEEE: 76 bài mọi năm → **68 bài từ 2020**, khớp kết quả tool. Lượt mọi năm chỉ dùng đối chiếu; tám bài ngoài phạm vi năm không tính thành tám bài loại V1.
- Kết quả tìm kiếm và bộ lọc năm đã được kiểm tra trong quá trình thực hiện.

## Snowballing từ công cụ khác — trạng thái hiện hành

Đối chiếu [catalog snowball nguồn](extras/original-export/snowballing/01_all_records.csv) với [catalog hợp nhất](01_all_records.csv), sau đó nối với [45 full-text screening results](snowballing/screening_results.csv) bằng DOI và metadata. Định danh catalog K và định danh PDF P được giữ để truy vết; số records catalog không phải tổng hits/citations của provider.

| Seed được ghi trong catalog nguồn | DOI | Ghi chú |
|---|---|---|
| A Black Box Tool for Robustness Testing of REST Services | `10.1109/ACCESS.2021.3056505` | INCLUDE hiện hành; P12/K81, P17/K84, P38/K108 có provenance forward từ seed này |
| LLM-Driven, Self-Improving Framework for Security Test Automation… | `10.1109/ACCESS.2025.3554960` | Seed discovery được giữ theo tool; quyết định screening hiện hành của seed là EXCLUDE — IC-I |
| Test Amplification for REST APIs: Using “Out-of-the-Box” Large Language Models | `10.1109/MS.2025.3559664` | Seed discovery được giữ theo tool; quyết định screening hiện hành của seed là EXCLUDE — IC-I |

| Phần đối chiếu | Số paper duy nhất | Diễn giải |
|---|---:|---|
| Catalog IEEE ban đầu | 68 | Q1–Q5: 72 occurrences − 4 repeated hits |
| Records có provenance snowball | 99 | Unique records từ catalog đã giao; có backward và forward |
| Trùng giữa IEEE và snowball | 17 | Gộp provenance vào cùng paper, không thêm 17 records |
| Paper mới từ snowball | 82 | 99 − 17 |
| Catalog hợp nhất | 150 | 68 + 99 − 17 = 150 |
| Full-text snowball đã đánh giá | 45 | 37 EXCLUDE + 3 INCLUDE + 5 REVIEW; tất cả nối được với catalog |
| Records snowball mới chưa screening | 37 | 82 − 45; giữ NOT_REVIEWED, không tự gán EXCLUDE/EC-A |

**Ba INCLUDE thêm vào tập evidence:** P12/K81 (`10.1145/3533767.3534401`), P17/K84 (`10.1145/3597926.3598131`), P38/K108 (`10.1145/3696630.3728545`). Xem căn cứ EP/BVA và kết quả số tại [evidence-table.md](evidence-table.md). Năm REVIEW chưa tính included.

Log OpenAlex nguồn từng ghi session bBOXRT mở **03:07:05 ngày 13/10/2026 UTC+7**, backward QUEUED/fetched 49/reported 64, forward QUEUED/fetched 0. Đây là [snapshot của công cụ đầu](extras/original-export/extras/search-log-export-original.md), không đại diện tiến độ catalog/full-text đã làm ở công cụ khác. Không thay 99 unique catalog records bằng số reported của provider, không tự cộng 49 pending references thành 49 paper mới.

**Giới hạn truy vết:** gói chưa có raw provider log đầy đủ cho công cụ snowball thứ hai. Vì vậy chưa xác minh tổng citations/references available, số pages provider, hoàn tất từng hướng hoặc coverage forward 12 tháng. Không diễn giải thiếu log hoặc số 0 của snapshot thành không có citation. Matching records và đồng bộ quyết định không tự hoàn tất coverage snowball.

## Hồ sơ bàn giao hiện hành

- [01_all_records.csv](01_all_records.csv): **150 paper duy nhất**, trong đó 68 IEEE ban đầu và 82 snowball mới.
- [02_after_screening_v1.csv](02_after_screening_v1.csv): 150 records cho bàn giao; **68 đã V1** (1 INCLUDE, 49 UNSURE, 18 EXCLUDE), **45 FULL_TEXT_DIRECT** đã lọc từ PDF, **37 NOT_REVIEWED**. Không giả lập quyết định V1 cho đợt lọc trực tiếp toàn văn.
- [04_fulltext_screening.csv](04_fulltext_screening.csv): **95 records**; **4 INCLUDE + 5 REVIEW + 86 EXCLUDE**. EXCLUDE gồm **46 EC-A import** và **40 full-text EXCLUDE**. Có **49 full-text đã đánh giá = 4 IEEE + 45 snowball**; 46 chưa lấy được toàn văn không tính assessed.
- [03_final_included.csv](03_final_included.csv) và [03_included_only.csv](extras/03_included_only.csv): đúng **4 INCLUDE**, không chứa EXCLUDE/REVIEW.
- [evidence-table.md](evidence-table.md) có bốn hàng INCLUDE; [prisma-flow.md](prisma-flow.md) dùng cùng catalog và quyết định. [Archive nguồn](extras/original-export/) giữ log, manifest, quyết định và review trước matching. Tập dữ liệu đã đồng bộ nhưng **chưa finalized**: còn 37 NOT_REVIEWED, 5 REVIEW, coverage/provider logs và kiểm chéo độc lập.
