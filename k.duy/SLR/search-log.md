# Search log — K.Duy · nguồn phụ trách: SpringerLink

*RQ FA26-EXT-12 · Các truy vấn chạy ngày 07/10/2026. Search field mặc định của SpringerLink; không áp dụng bộ lọc năm/loại tài liệu trên giao diện.*

## 1. Nhật ký chạy query

| Lần | Chuỗi tìm (nguyên văn) | CSDL | Trường tìm | Bộ lọc | Ngày chạy | Số kết quả | Ghi chú |
|---|---|---|---|---|---|---:|---|
| V1 | `("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing") AND ("fault detection" OR "mutant detection" OR "bugs found")` | SpringerLink | Mặc định | Không đặt | 07/10/2026 | 1 | Query String A theo protocol. DOI hiển thị: 10.1007/s42979-024-03134-3. |
| V2 | `("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing")` | SpringerLink | Mặc định | Không đặt | 07/10/2026 | 3 | Bỏ khối O theo quy tắc nới query; kết quả gồm battery passport, “On the Impact of Input Models...” (R01) và requirements-driven model checking. |
| V3 | `("REST API" OR "RESTful API" OR RESTest OR RESTestBench) AND ("equivalence partitioning" OR "equivalence class partitioning" OR "boundary value analysis" OR "boundary value testing" OR "boundary testing") AND ("fault detection" OR "faults found" OR "bug detection" OR "bugs found" OR defects OR failures OR "mutation testing" OR "mutation score" OR "mutant detection")` | SpringerLink | Mặc định | Không đặt | 07/10/2026 | 11 | Mở rộng từ đồng nghĩa theo hướng Lam dùng ở ACM; có trùng kết quả giữa các lượt tìm. |
| V4 | `("REST API" OR "RESTful API" OR "web API" OR "web service") AND ("boundary value analysis" OR "boundary value" OR "boundary testing" OR "equivalence partitioning") AND ("mutation testing" OR "mutants" OR "mutation score")` | SpringerLink | Mặc định | Không đặt | 07/10/2026 | 12 | String B theo protocol. |
| V5 | `REST API equivalence partitioning` | SpringerLink | Mặc định | Không đặt | 07/10/2026 | 428 | Thử nghiệm thăm dò không dùng toán tử/ngoặc; quá rộng nên không dùng làm tập record chính. Trang chỉ hiển thị 20 kết quả đầu. |
| V6 | `"REST API" AND "equivalence partitioning"` | SpringerLink | Mặc định | Không đặt | 07/10/2026 | 6 | Truy vấn tập trung EP; kết quả hiển thị vẫn có mục lạc chủ đề. |
| V7 | `"REST API" AND "boundary value analysis"` | SpringerLink | Mặc định | Không đặt | 07/10/2026 | 6 | Truy vấn tập trung BVA; kết quả hiển thị vẫn có mục lạc chủ đề. |

## 2. Kết quả đáng chú ý để đối chiếu/sàng lọc

| DOI | Tiêu đề | Thông tin quan sát được | Nhận xét ban đầu theo IC/EC |
|---|---|---|---|
| [10.1007/978-3-030-65310-1_33](https://link.springer.com/chapter/10.1007/978-3-030-65310-1_33) | RESTest: Black-Box Constraint-Based Testing of RESTful Web APIs | ICSOC 2020, LNCS 12571, pp. 459–475; Alberto Martin-Lopez, Sergio Segura, Antonio Ruiz-Cortés. 9 operations thuộc 6 API thương mại. So sánh constraint-based testing (CBT) với random testing (RT): CBT tìm 4,278 failures trên cả 9 dịch vụ; RT tìm 2,920 trên 5/9; hai oracle mới của CBT phát hiện 2,063 failures. | P/O và đối chứng random khớp tốt. Tuy nhiên thí nghiệm đánh giá CBT, không EP/BVA: CBT rút mẫu giá trị ngẫu nhiên từ miền rồi dùng constraint solver. RESTest có hỗ trợ boundary-value generator, nhưng bài không nói generator đó được dùng trong so sánh. EP chỉ được dùng để kiểm thử chính các công cụ. Khuyến nghị loại theo IC-I nghiêm ngặt; giữ làm tài liệu nền ngoài tập include. |
| [10.1007/978-3-032-05188-2_11](https://link.springer.com/chapter/10.1007/978-3-032-05188-2_11) | Test Amplification for REST APIs via Single and Multi-agent LLM Systems | ICTSS 2025; first online 16/09/2025. So sánh single-agent và multi-agent LLM trên coverage, bug detection, chi phí và năng lượng; abstract không nêu con số cụ thể. | REST API/bug detection phù hợp một phần; abstract không cho thấy EP/BVA hoặc baseline random. |
| [10.1007/s42979-024-03134-3](https://link.springer.com/article/10.1007/s42979-024-03134-3) | On the Impact of Input Models on the Fault Detection Capabilities of Combinatorial Testing | SN Computer Science, 2024; black-box combinatorial testing, mutation testing và structural coverage. | Loại theo IC-P/IC-I: không nghiên cứu REST API, không nêu EP/BVA cho tham số request. |
| [10.1007/s13042-024-02527-3](https://link.springer.com/article/10.1007/s13042-024-02527-3) | ChatHTTPFuzz: large language model-assisted IoT HTTP fuzzing | Bài báo năm 2025; IoT HTTP fuzzing. | Có thể loại theo IC-P/EC-O nếu không kiểm thử REST API ở mức request như phạm vi RQ. |

## 3. Tổng hợp và lưu ý

- V1–V4 có 27 kết quả cộng gộp và 22 tiêu đề duy nhất sau khử trùng lặp, được ghi trong `01_all_records.csv` và sàng lọc tại `02_after_screening_v1.csv`. Đây là union kết quả Springer, không phải tổng PRISMA của cả nhóm.
- V5 là truy vấn thăm dò quá rộng; V6–V7 là truy vấn EP/BVA bổ trợ. Có trùng/lạc chủ đề nên không gộp vào tập chính V1–V4.
- Đã kiểm tra DOI RESTest trong các records nhóm hiện có qua tìm kiếm văn bản: chưa thấy bản ghi trùng DOI.
- Đã kiểm tra toàn văn RESTest. Threats to validity nêu số lần lặp và phân tích thống kê bị giới hạn bởi quota API thương mại; cần đưa lưu ý này vào phần hạn chế nếu nhóm giữ bài làm tài liệu nền.

## Snowballing (1 vòng)

| Seed (DOI) | Vòng | Hướng (lùi/tiến) | Số đã lướt | Số thêm vào 01 | Số include cuối |
|---|---:|---|---:|---:|---:|
| 10.1109/MS.2025.3559664 (TUNG-IEEE-002, V2 Include) | 1 | Tiến — đối chiếu bài Springer trích dẫn seed | 1 | 0 (DOI đã có ở V3, R04) | 0 (UNSURE, chờ nhóm chốt IC-I) |

Springer chapter R04 trích dẫn seed TUNG-IEEE-002 (“Test amplification for REST APIs using out-of-the-box large language models”, 2025). DOI R04 đã có trong kết quả V3 nên không tạo record trùng. Đây là citation link đã xác minh; chưa phải danh sách đầy đủ mọi bài forward-citing trên các nền tảng.

## Thay đổi so với protocol

- 07/10/2026 — Chạy V2 bằng cách bỏ khối O do V1 trả dưới 20 kết quả; tiếp tục mở rộng từ đồng nghĩa, chạy String B và hai truy vấn EP/BVA riêng. Mọi query và số kết quả đều được ghi ở bảng trên.
- 07/10/2026 — Chạy thêm V5 thăm dò, nhưng không dùng làm tập record do truy vấn trả 428 kết quả và quá rộng.
- 07/10/2026 — Đọc toàn văn RESTest và đối chiếu IC-I: dù framework có boundary-value generator và nhóm tác giả dùng equivalence partitioning để kiểm thử chính công cụ, kỹ thuật được so sánh trong thí nghiệm API là constraint-based testing với random testing. Ghi khuyến nghị loại theo IC-I để không nhầm kỹ thuật kiểm thử công cụ với biến can thiệp.
- 07/10/2026 — Tạo tập record Springer, sàng lọc theo IC/EC và ghi citation liên quan tìm được trong vòng snowballing.