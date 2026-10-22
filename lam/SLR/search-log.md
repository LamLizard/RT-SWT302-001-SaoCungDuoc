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

## 7. Bổ sung paper nền do giảng viên cung cấp — 20/10/2026

- **Đầu vào:** 20 link do người phụ trách chuyển từ giảng viên: 1 SLR + 2 nền tảng + 16 mới + 1 liên quan khác. Đây là nguồn cung cấp có chủ đích, không phải 20 kết quả tìm kiếm ACM.
- **Thao tác:** thử mở từng link DOI/Semantic Scholar; khi bị lỗi, tìm đúng bài trên publisher, trang tác giả, repository trường hoặc arXiv; đọc phương pháp, kết quả và hạn chế ở các bản toàn văn truy cập được. Không tải/chạy artifact thực nghiệm.
- **Kết quả trích xuất:** thêm GV-01–GV-20 vào `evidence-table.md`, giữ nguyên 2 dòng ACM cũ; 13 bài đọc được các phần liên quan trong toàn văn, 6 bài chỉ abstract/preview, 1 bài chỉ metadata. Ghi nguồn, phiên bản và locator tại [teacher-papers-audit.md](teacher-papers-audit.md).
- **Hiệu chỉnh có nguồn:** GV-03 giữ issue year 2025 (đầu vào ghi 2024); GV-01 tách issue 2025/online 2026; GV-15 dùng 39 endpoints/7 services theo thân bài; GV-19 chưa thấy kết quả định lượng đáp ứng IC-E. Phân biệt program mutants với input/response mutation và các metric proxy.
- **Phạm vi:** bổ sung nền vào bảng Lâm trên nhánh `Lam`; chưa đổi 42 paper đã screening, PRISMA, CSV hoặc RQ. Nguồn ABS/META không tự coi đã qua V2. Nguồn ngoài IC-Y/IC-P/IC-I vẫn được giữ với nhãn nền theo chỉ định, chưa tự nới protocol.
- **Khử trùng:** đối chiếu DOI/arXiv đầu vào với bảng gộp hiện tại không thấy trùng dòng chính; RESTestBench, RESTOR và Prompt-Based đã có bản PDF/tài liệu RBL-2 ở Tùng, phải gộp thành một paper khi tích hợp tiếp.

## 8. Đối chiếu lại 17 PDF người phụ trách tải về — 20/10/2026

- **Đầu vào:** 17 file hiện có trong `Paper-source`, số #43–#59. Khớp tên/tác giả/DOI hoặc arXiv với danh sách 20 bài, không dùng tên file làm bằng chứng duy nhất. Đọc lại phương pháp, số liệu và hạn chế; render và xem các bảng cần kiểm cột/đơn vị của AGORA+, Nüwa, IoT và Crowdsourced.
- **Trạng thái mới:** **17 FT + 2 ABS + 1 META**. Nâng GV-07 (AGORA+), GV-13 (Nüwa), GV-16 (Crowdsourced), GV-17 (IoT) từ ABS sang FT. Còn thiếu PDF GV-01/GV-03/GV-20; các mức 13/6/1 tại §7 là lịch sử lượt đầu.
- **Hiệu chỉnh chính:** AGORA+ precision 68%/80% tương ứng 50/10K calls, 32 bugs có 17 confirmed; Meta ACH 31.677 generated và 9.095 buildable mutants; Nüwa tách 55 reported bugs ở bug-finding khỏi số 56 ở phép so Table II. IoT ghi đúng time-to-first-crash qua 3 lần, không suy thành số unique bugs; Crowdsourced ghi QWK theo app/dimension và giới hạn reference tree/taxonomy dùng chung.
- **Metadata/artifact:** RESTOR PDF có DOI 10.1145/3832185 và PACMSE/ISSTA October 2026; bổ sung link paper dẫn cho RESTCov, ArrayDiff, Nüwa, DualMine và YAKUSU. How Far PDF dẫn Zenodo 21102431, khác record 21295460 đã tìm trên web; ghi rõ khác biệt, chưa tự gán quan hệ phiên bản. METFORD local vẫn là preprint; ITA local 9 trang vẫn chưa có kết quả định lượng IC-E.
- **PICO:** chấm lại 4 bài mới có toàn văn; Nüwa C✓ theo rubric rộng (random syntax generator cùng 24h), không coi là uniform REST input. Giữ tách biệt output/input mutations với killed source-code mutants; RQ ban đầu không đổi.
- **Tệp cập nhật:** `evidence-table.md` (22 dòng, 17 link PDF local), `teacher-papers-audit.md` (mapping và locator từng file), nhật ký này. Không nhập thêm paper vào tập 42/PRISMA; không thay tên/nội dung PDF hoặc thao tác Git commit/push.

## 9. Loại nguồn không có PDF và đổi tên file — 20/10/2026

- **Yêu cầu người phụ trách:** không tải được PDF được coi là không đọc được, bỏ khỏi evidence table; đổi tên các bài đọc được để map bảng Lâm.
- **Loại 3 nguồn khỏi tập hiện hành:** Software Testing on Microservices-Based Systems: A Systematic Literature Review and Thematic Analysis (vị trí gốc 1 / mã cũ GV-01); Evaluating large language models for software testing (vị trí gốc 3 / mã cũ GV-03); Research on Software Fault Injection Testing Technology (vị trí gốc 20 / mã cũ GV-20). Lý do chung: không có toàn văn PDF local, tương ứng không tiếp tục dùng bằng chứng abstract/metadata; không kết luận các bài không liên quan.
- **Tập còn lại:** 17 bài GV có toàn văn; bảng Lâm **19 dòng = 2 ACM cũ + 17 GV**, không giữ hàng ABS/META/chờ tải. RQ không đổi.
- **Mã mới:** GV-01–GV-17 liên tục theo thứ tự các bài còn lại. Các mã GV trong §7–8 là mã lịch sử theo danh sách 20 nguồn, không phải mã hiện hành. Mapping vị trí gốc ↔ mã mới ↔ dòng Lâm ↔ PDF được ghi ở `teacher-papers-audit.md`.
- **Tên PDF mới:** `43-GV-01-YAKUSU.pdf` đến `59-GV-17-Intelligent-Test-Automation.pdf`, theo đúng thứ tự dòng #3–#19 của evidence table. Chỉ đổi tên 17 PDF bổ sung trong Paper-source; xác minh SHA256 trước/sau khớp toàn bộ, không thay nội dung PDF. Giữ các file #01–#42.
- **Đồng bộ:** sửa link PDF và các tham chiếu mã hiện hành trong evidence table/audit; bỏ bảng lịch sử web khỏi audit hiện hành, giữ lịch sử thao tác ở nhật ký này. Không đổi tập 42/PRISMA hoặc commit/push.

## 10. Đồng bộ tài liệu sau đổi hướng RQ — 21/10/2026 (Asia/Saigon)

- **Đầu vào:** nhánh Lam, commit `6658a63de7250dd7a41bbd6d140b3cdb3f9f5f51`; working tree sạch trước sửa. Commit này đã đổi RQ sang prompt-guided EP+BVA vs single-step, chưa phải triển khai thí nghiệm.
- **Phạm vi được phép:** đồng bộ tài liệu theo phản hồi GV và các lỗi đã kiểm; giữ RQ mới. Người dùng chọn **giữ nguyên điểm nền, ghi rõ chỗ chưa đồng nhất**, không tái chấm 59 paper theo RQ mới. Đồng bộ TD-0015 ở merge về nhãn map đang lưu (0✓, chạm 2), giữ TD-0002 2✓/chạm 3; sắp thứ tự theo ✓ rồi chạm và sửa số tổng hợp nhãn.
- **Nội dung:** sửa bảng căn hàng GV-02 thành refinement vs single-step, làm rõ paper có cả precise/vague; bổ sung pass-valid/fail-mutant, công thức từng run/trung bình mô tả ba run và mẫu số dịch vụ; sửa full hai arm thành 636 lượt sinh, 636 valid, 1.368 mutant trước setup/reset/retry. Ghi phân tích có cụm/ba run còn chưa chốt, nguồn email của 15 mutant và giới hạn suy luận.
- **Protocol:** giữ nguyên chuỗi, tiêu chí và mốc cũ dưới nhãn lịch sử; protocol/IC-EC bổ sung phù hợp RQ mới chưa khóa. README và phần hiện hành của notes theo RQ mới; giữ các quyết định cũ theo ngày. Không chạy query thu thập/screening mới, không thay 42 INCLUDE + 17 bài nền hoặc PRISMA/CSV.
- **Nguồn đối chiếu trong đợt này:** paper RESTestBench §3.2–4.2/Table 3; `src/evaluator.py` và prompt single-step tại snapshot benchmark `4decc1e36ea3dd41b64ce3e3ac6a85bc72df36ae`; các phần liên quan của PDF TD-0002; abstract Durkalski et al. (2003), DOI 10.1002/sim.1438. Kiểm kê 106 JSON/228 mutant kế thừa lượt rà trước, không ghi thành kiểm kê mới của đợt này.
- **Trạng thái:** chỉ sửa tài liệu; chưa Docker/golden tests, chưa LLM/pilot/thí nghiệm, chưa kiểm lại toàn văn 59 bài hoặc có phê duyệt GV. Không stage/commit/push.

## 11. Mục 1 — cập nhật nền tảng theo mail cô — 22/10/2026 (Asia/Saigon)

- **Ủy quyền:** người dùng yêu cầu dùng một skill phù hợp và làm mục 1 rồi mục 2, dừng để review trước mục 3; đã xác nhận “triển khai đi”. Skill sử dụng: experimental-design v1.5. Không dùng subagent.
- **Nhánh/đầu vào:** Lam, HEAD `80a246d`; hai file người dùng cung cấp chưa được track: PDF60 và file chat chứa mail. Không coi đây là mail xác thực độc lập qua hộp thư.
- **Tra cứu web có hướng, không phải query CSDL:** công cụ web search, ngày 22/10/2026, bốn chuỗi nguyên văn:
  1. `"REST API" "equivalence partitioning" "large language" -site:researchgate.net -site:reddit.com`
  2. `"RESTestBench" "boundary" -site:pith.science -site:reddit.com`
  3. `"RESTOR" "REST API" 2026`
  4. `"Prompt-Based REST API Test Amplification in Industry"`
- Công cụ không cung cấp tổng hit/screening hợp lệ cho từng CSDL; không ghi số records, không sửa CSV/PRISMA bằng các kết quả này. Không dùng bản tổng hợp AI/nhận xét bên thứ ba làm bằng chứng về kết quả nghiên cứu.
- **Nguồn chính sử dụng:** PDF60/arXiv2505.09830 (phương pháp/kết quả/threats); PDF44/arXiv2604.25862; PDF39/RestTSLLM; PDF45/arXiv2601.17903; PDF46/arXiv2607.23963 và DOI10.1145/3832185 trong PDF. GV-02/GV-03/GV-04 là ba nguồn 2026 đã có, được chọn theo mức liên quan và có định vị khác biệt; không khẳng định là ba bài mạnh nhất toàn lĩnh vực. Kết quả tìm khác, gồm bài về textual API description/MADS, chưa được đọc toàn văn/tái thẩm định và chưa đưa vào corpus hoặc dùng kết luận gap.
- **GV-18:** thêm đúng một nguồn nền, DOI/arXiv/title khác 59 nguồn trước. Mapping PDF60, hash, locator và giới hạn tại teacher-papers-audit. Bộ evidence hiện hành 60 = 42 INCLUDE lịch sử + 18 nguồn nền; final screening vẫn 42. Nguồn phương pháp của skill không cộng vào corpus nghiên cứu thực nghiệm.
- **Tài liệu:** cập nhật rq-validation theo RQ cô, phân biệt bằng chứng/suy luận/chưa biết; thêm câu hỏi phân tích và đóng góp. Bổ sung protocol tìm phù hợp LLM/prompt và phân tuyến IC/EC; bảo toàn tiêu chí, phễu và nhãn cũ. Đồng bộ phần hiện hành của năm rq-check, giữ phần đối chiếu cũ có nhãn lịch sử.
- **Giới hạn:** chưa systematic screening mới theo A1–A3, chưa tái chấm toàn bộ 59 bài, chưa chấm độc lập; chưa golden/pilot/LLM. Không ghi thành GV chốt RQ; không commit/push.

## 12. Mục 2 — thiết kế review với DeepSeek và 3 USD — 22/10/2026

- **Bổ sung từ người dùng:** model DeepSeek-V4.1-Flash-1017, trần 3 USD; trả lời xác nhận dùng DeepSeek API chính thức. Đủ để soạn thiết kế review; chưa chứng minh khả thi runtime hoặc đủ tiền thực tế cho toàn panel.
- **Nguồn chính thức đọc:** `https://api-docs.deepseek.com/updates/` xác nhận update1017/API alias deepseek-flash; `https://api-docs.deepseek.com/quick_start/pricing/` xác nhận cache-miss input0.15/0.30 và output0.60/1.20 USD/1M token (off-peak/peak); `https://api-docs.deepseek.com/api/create-chat-completion/` xác nhận thinking mặc định enabled và temperature không hiệu lực trong thinking mode. Thiết kế dùng explicit disabled/temperature0.2/max_tokens2048 cho cả C/I; chưa gọi thử API.
- **Artifact:** benchmark-manifest.json tạo từ 106 JSON đã đọc trong lượt kiểm kê ngày22/10 ở cùng chat, định danh git blob và 228 native mutant indices. Đọc OAS/source metadata tại commit khóa qua GitHub connector; không clone/build service hoặc chạy benchmark. C trích đúng DEFAULT_PROMPT_TEMPLATE (config benchmark không override prompt); I giữ toàn bộ C và nối sáu chỉ dẫn. Run-schedule660 slot là kế hoạch, không phải execution log.
- **Ngân sách:** 24 slot pilot + 636 main dự kiến R3. Envelope16k input/2048 output, cache-miss/off-peak: 2.395008 USD trước retry; peak4.790016 nên không mặc định phù hợp3USD. Phân bổ0.15 pilot/2.45 main/0.40 dự phòng. Phải có cận trên token, reserve cả cặp/attempt theo peak, ghi unknown charges và hard guard trước khi dispatch. File config chưa triển khai guard/runner.
- **Phương pháp:** ghép requirement/run, xen kẽ thứ tự C/I và service, không pseudoreplication; báo effect/độ biến động, không chốt p-value confirmatory hoặc equivalence. Mẫu qualitative12 requirement (72 output nếu main đủ), hai người chấm độc lập chưa được nhóm chỉ định. Codebook phân biệt căn cứ oracle với đúng theo benchmark.
- **Skill và ghi nhận:** chỉ dùng experimental-design v1.5 trong lượt triển khai; nguồn thư viện Kassis et al.2026/arXiv2609.00065 được kiểm metadata (v2, authors/title) và ghi ở experiment-design. Không cộng nguồn phương pháp này vào corpus60.
- **Kiểm tra offline:** C khớp từng byte với literal nguồn pinned; I có C làm tiền tố và đúng ba placeholder; manifest106/228 và SHA256 khớp; schedule660 slot/330 cặp liền nhau, mỗi main run106 requirement đủC/I và53 cặp mỗi thứ tự; 59 dòng nghiên cứu cũ giữ nguyên ở merge/map; link file local có đích tồn tại. Kiểm whitespace/diff và đọc lại tài liệu trước bàn giao. Không chạy unit/integration test vì không triển khai bộ chạy trong phạm vi này.
- **Trạng thái bàn giao:** cập nhật README/notes, mục1 và hồ sơ mục2 để người dùng review. `execution_permitted=false`, main/prompt/schedule chưa final-freeze. Chưa có môi trường lock, token count thật, API usage, golden/pilot/main hoặc GV duyệt. Không chi DeepSeek, không commit/push và không chuyển sang mục3.
