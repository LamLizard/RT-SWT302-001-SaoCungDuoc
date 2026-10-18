# Search log — Khôi · nguồn phụ trách: OpenAlex
*Nhóm 1 — SaoCungDuoc · RQ FA26-EXT-12 · Cập nhật: 13/10/2026*
*Công cụ lấy dữ liệu: RBL Paper Harvester (extension Chrome tự viết, gọi API OpenAlex) — xem mục 6 "Kiểm chứng".*

## 1. Bảng log chính (lần chạy chính thức, dùng cho PRISMA)

| # | Query nguyên văn | CSDL | Trường tìm | Bộ lọc | Ngày | Số kết quả | Số sau bỏ trùng | Ghi chú |
|---|---|---|---|---|---|---|---|---|
| V1 | `("REST API" OR "RESTful API" OR "RESTful web service" OR "web API" OR "OpenAPI") AND ("equivalence partitioning" OR "boundary value" OR "boundary testing" OR "black-box testing" OR "black box testing" OR "test generation" OR "test case generation" OR "test amplification" OR "random testing" OR "fuzzing" OR "test oracle") AND ("mutation" OR "mutant" OR "mutation score" OR "fault detection")` | OpenAlex (API, `title_and_abstract.search`) | title-abstract | year ≥ 2020 | 13/10/2026 01:58 | **30** (web OQL: 19) | 30 | Độ phủ bài nền của RQ chỉ 1/6 → khối O quá hẹp, mở rộng O (V2) |
| V2 | `("REST API" OR "RESTful API" OR "RESTful web service" OR "web API" OR "OpenAPI") AND ("equivalence partitioning" OR "boundary value" OR "boundary testing" OR "black-box testing" OR "black box testing" OR "test generation" OR "test case generation" OR "test amplification" OR "random testing" OR "fuzzing" OR "test oracle") AND ("mutation" OR "mutant" OR "fault" OR "bug" OR "defect" OR "failure" OR "coverage")` | OpenAlex (API, `title_and_abstract.search`) | title-abstract | year ≥ 2020 | 13/10/2026 01:59 | **166** | 159 (gộp V1 + V2) | Trong ngưỡng 20–500, độ phủ bài nền 5/6 → **chuỗi chạy chính** |

**Kiểm tra độ phủ (6 bài nền trên thẻ RQ):** V2 tìm thấy RESTestBench (K23), SATORI (K52), *Test Oracle Generation for REST APIs* (K44), *Prompt-Based REST API Test Amplification* (K77), DualMine (K113) = 5/6; thiếu RESTOR (chỉ xuất hiện khi bỏ khối O).

## 2. Tổng hợp

- Tổng trước dedup: 30 + 166 = **196** · Sau dedup: **159** (bỏ 37: 30 bài V1 nằm trọn trong V2 + 7 bản trùng trong kết quả OpenAlex) = số dòng nhánh CSDL trong `01_all_records.csv` (K01–K159) — khớp hộp PRISMA.
- Cộng nhánh snowballing (mục 4): 01 có **194** dòng (K01–K194).
- Chênh lệch tool–web ở V1 (30 so với 19): API OpenAlex có stemming (khớp số nhiều/biến thể như "REST APIs", "mutants", "fuzz"), tab OQL khớp đúng cụm. Tập kết quả web nằm trọn trong tập của tool.

## 3. Lịch sử thử nghiệm trước khi chốt chuỗi (không dùng cho PRISMA, giữ để minh bạch)

| Ngày | Chuỗi | Cách chạy | Kết quả | Kết luận |
|---|---|---|---|---|
| 05/10 | String A (protocol), có/không khối O | web tab Advanced | 10 / 283 | **Không hợp lệ**: giao diện Advanced bỏ dấu nháy kép, cụm từ bị tìm như từ đơn (trang 1 toàn bài ngoài chủ đề) |
| 05/10 | String A đầy đủ / bỏ O | web tab OQL | 0 / 0 | Cú pháp OQL đã kiểm (`title-abstract has ("RESTestBench")` → 1 bài đúng) → 0 là số thật |
| 05/10 | String B đầy đủ / bỏ O | web tab OQL | 0 / 7 | < 20 → báo PL |
| 13/10 00:18–00:26 | String A đầy đủ / bỏ O, String B đầy đủ / bỏ O | tool (API) | 0 / 1 / 0 / 12 | Khớp web (khác ở String B bỏ O: 12 vs 7, do stemming; 7 bài web nằm trọn trong 12). Vẫn < 20 |
| 13/10 00:32 | `(REST API…) AND (test generation… OR random testing)` (gợi ý của thành viên) | tool | 294 | Cho thấy bài nền dùng thuật ngữ "test generation/fuzzing", không phải EP/BVA → thiết kế lại chuỗi theo PICO |
| 13/10 ~01:05 | Chuỗi mới bỏ hẳn khối O | tool | 398 (độ phủ 6/6) | Không dùng: V2 đã trong ngưỡng 20–500 (quy tắc dừng); bài thiếu (RESTOR) xử lý qua snowballing |

## 4. Snowballing

| Seed (DOI) | Vòng | Hướng (lùi/tiến) | Qua API | Số đã lướt | Số thêm vào 01 | Số include cuối | Ghi chú |
|---|---|---|---|---|---|---|---|
| 10.1007/978-3-030-65310-1_33 (K90 — RESTest: Black-Box Constraint-Based Testing of RESTful Web APIs, ICSOC 2020) | 1 | lùi | OpenAlex | 4 | 1 | 0 | OpenAlex ghi nhận 19 reference của seed; bỏ 15 reference trước năm 2020 (IC-Y) |
| 10.1007/978-3-030-65310-1_33 (K90) | 1 | tiến | OpenAlex | 53 | 34 | 6 | K162 bBOXRT, K166 dự đoán tính hợp lệ input, K167 DeepREST, K168 mass-assignment black-box, K191 RestTestGen/DeepREST trong công nghiệp, K192 RESTing-LLAMA |

- Tổng snowballing: 57 bài lướt → 35 bài mới vào 01 (22 bài đã có ở nhánh CSDL hoặc trùng nhau) → V1 loại 21 → V2 (14 bài): **6 INCLUDE**, 8 EXCLUDE (IC-I 3, EC-S 2, EC-N 2, EC-A 1).
- Lý do chọn 1 gốc K90: bài sát RQ nhất trong các bài INCLUDE của nhánh CSDL — so sánh trực tiếp constraint-based (gần phân hoạch) với random testing trên 9 API (100% vs 40,1% test hợp lệ; 4.278 vs 2.920 failure).
- Snowballing làm 1 vòng, 1 gốc theo quyết định của nhóm cho tuần 6.

## 5. Thay đổi so với protocol

| Ngày | Thay đổi | Lý do |
|---|---|---|
| 05/10/2026 | Trường tìm: protocol ghi Title / Abstract / Keywords → OpenAlex dùng `title-abstract` | OpenAlex không có trường Keywords riêng |
| 13/10/2026 | **Thay String A/B bằng chuỗi mới (V1/V2 mục 1)**, thiết kế theo PICO: P = REST API; khối kỹ thuật = I (EP, BVA, black-box) + C (random testing, fuzzing) + thuật ngữ các bài nền (test generation, amplification, oracle); O = mutation/fault | String A/B cho < 20 kết quả ở mọi biến thể (mục 3); 6 bài nền trên thẻ RQ đều không dùng thuật ngữ EP/BVA trong abstract → String A/B không tìm ra chúng. Đã báo PL |
| 13/10/2026 | Áp **IC-I** theo nghĩa: bài sinh dữ liệu đầu vào hộp đen cho REST API theo hướng phân hoạch/biên/ràng buộc/combinatorial (khối I) **hoặc** ngẫu nhiên/fuzzing (khối C) | RQ so sánh EP+BVA với random; hiểu IC-I đúng nghĩa đen (chỉ EP/BVA) cho 0 INCLUDE ở mọi chuỗi. Cần PL/nhóm xác nhận để các nguồn lọc thống nhất |
| 13/10/2026 | Lấy dữ liệu và snowballing bằng tool tự viết (thay mục cũ "export web, không tự viết tool; snowballing không áp dụng") | Gom nhiều lượt chạy, loại trùng, snowballing 2 hướng có lọc năm; đã kiểm chứng (mục 6) |
| 13/10/2026 | Screening V1 dùng bộ luật tự động của tool + người rà lại; V2 có **AI hỗ trợ (Claude)** | Khối lượng 159 + 35 bài; mọi quyết định tự động/AI được ghi nhãn trong `v1_note` / `v2_reason` (mục 7) |
| 13/10/2026 | V2: bài **không tải được toàn văn → EXCLUDE · EC-A** (áp thống nhất cho mọi bài) | Đúng định nghĩa EC-A; tránh INCLUDE bài chỉ dựa trên abstract. 27/73 bài không tải được (24 EC-A + 3 giữ mã IC-L/EC-S đã xác định từ metadata) |

## 6. Kiểm chứng (tool tự viết lấy metadata)

1. **Số bản ghi khớp số trang web báo?** V1: tool 30, web OQL 19 (cùng chuỗi, 13/10). Chênh do API OpenAlex có stemming; 19 bài web nằm trọn trong 30 bài của tool. Các chuỗi cũ: String A 0 = 0, String B bỏ O tool 12 / web 7 (7 bài web nằm trọn trong 12).
2. **5 bản ghi đối chiếu tiêu đề/năm/DOI** (chọn ngẫu nhiên, đối chiếu bản ghi OpenAlex `api.openalex.org/works/doi:…`, 13/10/2026):

| Mã | DOI | Tiêu đề | Năm | Khớp |
|---|---|---|---|---|
| K14 | 10.1016/j.asoc.2021.107246 | A Discrete Dynamic Artificial Bee Colony with Hyper-Scout for RESTful web service API test suite generation | 2021 | ✓ |
| K40 | 10.1145/3491038 | On the Faults Found in REST APIs by Automated Test Generation | 2022 | ✓ |
| K86 | 10.1117/12.3056906 | Response relation model-driven approach for automated fuzz testing of RESTful Web APIs | 2025 | ✓ |
| K105 | 10.48550/arxiv.2604.08007 | Log-based, Business-aware REST API Testing | 2026 | ✓ |
| K176 | 10.1145/3468264.3473491 | Automated generation of realistic test inputs for web APIs | 2021 | ✓ |

3. **Chạy lại cùng query ra cùng số?** Cùng cặp chuỗi V1 + V2 chạy 2 lần: 13/10 00:48 và 13/10 01:58–01:59. Cả hai lần V1 = 30 và tập hợp V1 ∪ V2 sau dedup = **159 bài giống hệt nhau** (so theo DOI/tiêu đề: 159/159 trùng khớp).

## 7. Khai báo sử dụng AI

- **V1:** bộ luật sàng tự động của RBL Paper Harvester (IC-Y, IC-L, IC-T theo loại tài liệu/nơi đăng, EC-N, IC-P, IC-I theo từ khoá; không có abstract → Unsure). Mỗi bài ghi `[tự động] <luật đã áp>` trong `v1_note`; người thực hiện rà lại INCLUDE/Unsure.
- **V2:** Khôi tự tải toàn văn: lấy được **46/73** PDF (bản nhà xuất bản hoặc bản arXiv/tác giả của bài đã đăng); 27 bài không tải được → EXCLUDE (24 EC-A, K08 IC-L, K99/K180 EC-S). **AI (Claude) hỗ trợ đọc 46 PDF** theo IC/EC (số trang, Table/Figure có số, kỹ thuật sinh input, có thực nghiệm) và đề xuất quyết định kèm bằng chứng; Khôi rà và nhập quyết định cuối vào tool.
- **Kết quả V2:** 34 INCLUDE (nhánh CSDL 28 + snowballing 6), 39 EXCLUDE — khớp `03_final_included.csv` và `prisma-flow.md`. Các ca ranh giới cần PL xác nhận ghi ở cuối `prisma-flow.md`.
- Người thực hiện (Khôi) chịu trách nhiệm quyết định cuối; evidence table lập từ chính các PDF đã tải, có AI hỗ trợ trích số.

## 8. RBL-2 — Rà nghiên cứu mạnh nhất 12 tháng gần đây (18/10/2026)

Không dùng cho PRISMA (không thêm bài vào 01–03 CSV); chỉ để đối chiếu tính mới của RQ. Kết quả chi tiết: `rq-check.md` mục 5.

| # | Ngày | Công cụ | Truy vấn (nguyên văn) | Bộ lọc | Số kết quả | Bài chọn | Lý do chọn / loại |
|---|---|---|---|---|---|---|---|
| R1 | 18/10/2026 | Google Scholar (Khôi tự chạy) | `"REST API" "test generation" "mutation score"` | 2025–2026, sort by relevance | khoảng 44 | Req2REST-Guard (Xue et al., 2026); RESTestBench (Kogler et al., 2026); MASTOR (Deng et al., 2026) | Chọn: cùng bài toán REST API + metric mutation score. Loại: TSL+LLM (đã có, TD-0002); Req2test (unit test); survey Falah 2025; bài tiếng Ukraina; conversational AI (Masserini); quantized LLM (Ahmed); luận án Sue — khác bài toán hoặc là survey |
| R2 | 18/10/2026 | Google Scholar (Khôi tự chạy) | `"RESTestBench"` | 2025–2026, sort by relevance | 5 | RESTestBench; Req2REST-Guard | Chọn: dùng đúng benchmark của P. Loại: LLM-Based Test Generation survey (Liang et al., 2026), TestPrism, TestSuiteBench — survey/benchmark chung, không phải REST API |

Toàn văn Req2REST-Guard tải từ ResearchGate (6 trang, chưa có venue); đọc §IV–VII để chấm P/I/C/O. Bản nháp trước (web search do Claude chạy, cùng ngày) có thêm RESTOR (ISSTA 2026) — không xuất hiện trên Scholar với 2 truy vấn trên nên đã bỏ khỏi rq-check.
