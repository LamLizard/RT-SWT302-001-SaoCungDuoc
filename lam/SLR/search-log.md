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
