# Search log — Lâm · nguồn phụ trách: ACM Digital Library

## 1. Nhật ký chạy query (ghi MỌI phiên bản chuỗi + số kết quả)

| Lần | Chuỗi tìm (nguyên văn) | CSDL | Trường tìm | Bộ lọc | Ngày chạy | Số kết quả | Ghi chú |
|---|---|---|---|---|---|---|---|
| **V1** | `("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing") AND ("fault detection" OR "mutant detection" OR "bugs found")` | ACM DL | AllField (mặc định) | Không đặt lọc | 13/10/2026 | **8** | < 20 kết quả → theo quy tắc: bỏ khối O để nới (bản V2) |
| **V2** | `("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing")` | ACM DL | AllField (mặc định) | Không đặt lọc | 13/10/2026 | **12** | Vẫn < 20 → tiếp tục nới bằng từ đồng nghĩa (String B/C) |
| **V3** | `("REST API" OR "RESTful API" OR "REST API testing" OR RESTest OR RESTestBench) AND ("equivalence partitioning" OR "equivalence class partitioning" OR "boundary value analysis" OR "boundary value testing" OR "boundary testing") AND ("fault detection" OR "faults found" OR "bug detection" OR "bugs found" OR defects OR failures OR "mutation testing" OR "mutation score" OR "mutant detection")` | ACM DL | AllField (mặc định) | Không đặt lọc | 13/10/2026 | **60** | Chuỗi chạy của nguồn ACM |
| **V4** | `("REST API" OR "RESTful API" OR "web API" OR "web service" OR "RESTful web service" OR "HTTP API") AND ("boundary value analysis" OR "boundary-value analysis" OR "boundary value" OR "boundary testing" OR "equivalence partitioning" OR "equivalence class partitioning" OR "input partitioning" OR "input domain partitioning" OR "boundary analysis")` | ACM DL | AllField (mặc định) | Không đặt lọc | 13/10/2026 | **209** | Chuỗi chạy của nguồn ACM |
| **V5** | `("REST API" OR "RESTful API" OR "RESTful web service" OR "web API") AND ("test generation" OR "test case generation" OR "test amplification" OR "black-box testing" OR "black box testing" OR "robustness testing" OR "random testing")` | ACM DL | AllField (mặc định) | Không đặt lọc | 13/10/2026 | **599** | Chuỗi chạy của nguồn ACM |

## 2. Xử lý đặc biệt trong quá trình tìm

1. **Tổng hợp số (bộ redo 13/10/2026):** V1 8 + V2 12 + V3 60 + V4 209 + V5 599 = **888 record thô** → loại trùng **EC-D: 261 dòng** → **627 record** bước vào sàng lọc V1 (261 dòng trùng vẫn giữ trong `01/02` kèm quyết định `EC-D`).
2. Tra cứu bổ trợ (DOI.org / Crossref / OpenAlex) chỉ dùng để lấy metadata phục vụ ghi nhận & sàng lọc — **không tạo record mới** ngoài danh sách trên.

## 3. Thay đổi so với protocol

| Ngày | Thay đổi | Lý do |
|---|---|---|
| 04/10/2026 | Dời ngày dừng search: 04/10 → **23:59 05/10/2026** | Cần thêm thời gian hoàn tất chạy & tổng hợp |
| 13/10/2026 | Dời ngày dừng search: 05/10 → **23:59 13/10/2026** | Cần thêm thời gian hoàn tất chạy & tổng hợp |

## 4. Snowballing — vòng 1 · 1 seed (cập nhật 13/10/2026, theo hướng dẫn A2b/A3)

**Seed — chọn theo 4 bước:**
1. **Điều kiện cần:** chỉ xét bài đã INCLUDE ở vòng 2 (`03_final_included.csv`) — bộ hiện tại đủ điều kiện: **R021 · `10.1145/3698062.3698065`** ✓.
2. **Độ sát RQ:** R021 khớp khối **P** (`restful`, `api test`, `openapi`); nội dung: sinh test script cho **RESTful API** từ OpenAPI + thiết kế **dữ liệu test từ ràng buộc CSDL** — cùng hướng "sinh test cho API" với RQ. Khối **I**: chưa thấy trong tiêu đề/abstract (ưu tiên thấp, không loại).
3. **Loại paper:** bài hội nghị (WSSE 2024, nguồn ACM); danh mục tham khảo **13 mục** — đủ cho 1 lượt lùi.
4. **Số trích dẫn:** **0** (nguồn OpenAlex, 13/10/2026 — bài mới) — thấp hơn khuyến nghị 10–200; chấp nhận vì là bài **duy nhất đủ điều kiện** trong bộ hiện tại; sẽ xét lại khi bộ dữ liệu mở rộng.

→ **Seed: R021 · `10.1145/3698062.3698065`** — "Generating RESTful API Test Scripts with Database Constraints using OpenAPI Specification" (WSSE 2024).

**Bảng seed (6 cột, vòng 1 — mỗi seed đúng 1 lượt lùi + 1 lượt tiến, không snowball tiếp từ bài mới INCLUDE):**

| Seed (DOI) | Vòng | Hướng (lùi/tiến) | Số đã lướt | Số thêm vào 01 | Số include cuối |
|---|---:|---|---:|---:|---:|
| 10.1145/3698062.3698065 (R021) | 1 | Lùi | 6 | 6 | 0 |
| 10.1145/3698062.3698065 (R021) | 1 | Tiến | 0 | 0 | 0 |

- **Tổng:** rà **6 tiêu đề** (lượt lùi; lượt tiến không có mục nào); **thêm 6 dòng vào `01_all_records.csv`** (R889–R894); **include cuối = 0**.
- **Nguồn lùi:** danh sách References trên trang bài OpenAlex. **Lượt tiến:** bài chưa ghi nhận trích dẫn (0) và tab Citations → 0.
- **Kết quả sàng lọc (đủ 2 vòng):** 6 → loại V1 **5** (IC-P 1 · IC-Y 4) → vòng 2: **1** (R893) → loại V2 **1** (EC-A — không tìm thấy bản mở) → **giữ 0**. Chi tiết từng dòng: `02_after_screening_v1.csv` (vòng 1) + `03_final_included.csv` (vòng 2).

## 5. Rà soát cho Bước 2 RBL-2 (18/10/2026)

- **Mục đích:** tìm 2–3 paper mạnh nhất trong 12 tháng gần nhất cùng chủ đề (yêu cầu RBL-2 Bước 2 — mục “Rà nghiên cứu mạnh nhất gần đây”).
- **Truy vấn:** Semantic Scholar Graph API — `query=REST API mutation testing`, `year=2025-2026`, `fields=title,year,venue,externalIds,citationCount`, ngày chạy **2026-10-18** → **12 kết quả**; kiểm tra chéo venue/năm/citation bằng OpenAlex theo DOI (cùng ngày).
- **Đã chọn (thứ tự: cùng bài toán/metric → venue/benchmark lớn → mới nhất):**
  - **LlamaRestTest** — FSE 2025, DOI `10.1145/3715737` (12 real-world services; so RESTGPT, RESTler, MoRest, EvoMaster, ARAT-RL).
  - **RESTestBench** — EASE 2026, arXiv `2604.25862` (3 dịch vụ; 106 yêu cầu/228 mutation theo Table 3; benchmark cho LLM-generated tests).
  - **MioHint** — ICSE 2026, DOI `10.1145/3744916.3773228` (whitebox, LLM-assisted request mutation).
- **Kết quả kiểm tra:** cả 3 **không** so EP+BVA với uniform random cùng request budget; **không** báo cáo số mutant riêng biệt theo từng dạng yêu cầu; **không** dùng RESTestBench làm P → **không có phản chứng mới** cho RQ FA26-EXT-12.

## 6. Đối chiếu và sửa tổng hợp RQ — 20/10/2026 (Asia/Saigon)

- **Loại công việc:** rà tính nhất quán/nguồn của tài liệu tổng hợp; không phải lượt tìm kiếm hệ thống mới. Không thay N=42, screening decisions hoặc PRISMA.
- **Quyết định đã được chấp nhận:** giữ 45 yêu cầu, đổi P từ 15/dịch vụ sang **16 FastAPI + 15 NestJS RealWorld + 14 TodoApp**. Cập nhật rq-validation, review-protocol, rq-evidence-map và notes; chưa khóa commit benchmark/danh sách ID hoặc cập nhật thẻ/GV.
- **Kiểm ma trận:** tính lại 42 hàng §3: P ✓/◐/· = 0/28/14; I = 2/21/19; C = 5/25/12; O = 1/32/9. Điểm paper: 35 bài 0, 6 bài 1, 1 bài 2. Sửa bảng cá nhân: Tùng 4 bài 1/4 + 4 bài 0/4; K.Duy K49 1/4 + 7 bài 0/4.
- **Guo 2024:** đọc toàn văn chính thức https://link.springer.com/article/10.1007/s11219-023-09659-9 (§5.2, §5.4–5.6). Giữ 3/4 theo rubric rộng; phân biệt với RQ đầy đủ vì nguồn biên từ mã, random theo phân hoạch, oracle đường thực thi. Bỏ câu “chỉ khác P” và quy tắc tự hạ điểm vì uniform mà không đổi rubric cho các bài khác. `extension` là nhãn làm việc theo rubric; chưa xác minh thẻ/GV gốc.
- **RESTestBench:** đối chiếu paper https://arxiv.org/html/2604.25862v1 (Table 3/§3/§6), README Dataset và src/evaluator.py trên repo tác giả. Paper ghi 106 yêu cầu/228 mutations; README 103 yêu cầu, TodoApp 14. Không nội suy ~97 mutant thành số mutant của mẫu. Chưa lấy được snapshot/manifest qua lần kiểm này, chưa chạy benchmark.
- **PDF trong repo:** đối chiếu các mục cụ thể của K46/PDF10, K32/PDF9, P12/PDF10, TD-0015/PDF8, K02/PDF14, K89/PDF27, K93/PDF21, K166/PDF7 cho GAP-D; K49/PDF17 cho GAP-M; TD-0002/PDF4/6–8 và TD-0015/PDF6 cho I/O. Không tuyên bố screening lại toàn bộ 42 bài. Tám paper GAP-D không đồng nghĩa tám nhóm tác giả độc lập; bỏ số đếm 11 nhóm chưa đủ truy vết/gộp nhóm.
- **Nguồn bổ sung:** ghi rõ Req2REST-Guard có P/điểm chưa xác nhận, do rq-check Khôi nêu tên dịch vụ không khớp; ghi ngày rà Khôi là 18/10/2026, không nhầm với mốc xuất bản 04–06/2026. Giữ phân biệt nguồn đã đọc trực tiếp và điểm kế thừa rq-check.
- **Thống kê:** đối chiếu SciPy 1.17 `wilcoxon` và ASA P-Value Statement. Sửa diễn giải bác bỏ H0 theo chiều hiệu ứng; không suy tương đương từ không bác bỏ H0, không suy tính khái quát từ p-value; bỏ khuyến nghị tăng lượt tùy kết quả. Đánh dấu phương án tổng hợp/kiểm định, B/miền uniform/CI/θ là điều kiện cần khóa trước chạy chính, không bịa số pilot.
- **Giới hạn:** các file rq-check cá nhân giữ như nguồn lịch sử; chưa tái kiểm chính thức thẻ W6/ý kiến GV, chưa screening IC/EC lại toàn tập, chưa triển khai generator hoặc chạy Docker/pilot. Xem rq-validation §6–7 để biết trạng thái hiện hành.

### Double-check lần hai — 20/10/2026

- Kiểm lại bảng gộp: 42 mã khác nhau, số thứ tự #1–#42; đối chiếu điểm từng mã với ma trận, không chỉ kiểm tổng. Không đổi N hoặc điểm nguồn.
- Bổ sung K66 cho GAP-D: §5/PDF10 nêu giới hạn đánh giá 11 REST APIs, rào cản authentication/quota và khả năng khác hiệu năng ở API/miền khác. Tổng hiện hành là **9 paper có đoạn trực tiếp**, không phải 9 nhóm độc lập; phần ghi 8 paper ở lượt trước là lịch sử đối chiếu.
- Sửa locator K49: đoạn mutation tool nằm trong **§4.5.1/PDF17**, không phải §4.4; locator TD-0015 là PDF8, đoạn giới hạn thực nghiệm trước §3.4.
- Bổ sung điều kiện precise/vague chưa khóa: cùng biến thể cho hai nhánh; 900 lượt là cho một điều kiện mô tả, không mặc định chạy cả hai. Không tạo dữ liệu chạy hoặc quyết định thực nghiệm mới.
- Thu hẹp câu O trong rq-evidence-map về đúng phạm vi 42 bài và mức chưa xác nhận đầy đủ O của RQ.
