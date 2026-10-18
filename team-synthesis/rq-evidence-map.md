# Bản đồ bằng chứng cho RQ — nhóm 1 (SaoCungDuoc) · RQ FA26-EXT-12

*Bước 12 (cả nhóm) · bản 3 — 16/10/2026 (commit `6482a9`) · nguồn: `team-synthesis/evidence-table-merged.md` (N = 42; 4 bản EC-D trên 3 cặp đã gộp 1 dòng).*

**RQ (nguyên văn):** Trên 45 yêu cầu của RESTestBench, phân hoạch tương đương kết hợp phân tích giá trị biên, so với sinh dữ liệu ngẫu nhiên đồng đều cùng ngân sách, khác nhau thế nào về số mutant riêng biệt bị phát hiện theo từng dạng yêu cầu?

**PICO:** P = 45 yêu cầu RESTestBench (15/dịch vụ) · I = EP + BVA · C = random đồng đều cùng ngân sách · O = số mutant riêng biệt được oracle xác nhận.

## 1. Quy tắc chấm (chuẩn hoá toàn nhóm)

| Yếu tố | ✓ = khớp ĐÚNG giá trị RQ | ◐ = gần (không tính vào "Số yếu tố") | Trống |
|---|---|---|---|
| P · dataset | Dùng RESTestBench | Dịch vụ REST mã mở/công khai chạy được (gieo mutant được như RESTestBench) | API thương mại/online, hệ nội bộ |
| I · can thiệp | EP và/hoặc BVA là kỹ thuật chính | Phân hoạch/miền, combinatorial, giá trị biên/không hợp lệ, phân lớp theo kiểu | Không có |
| C · đối chứng | So với sinh ngẫu nhiên **cùng ngân sách** (số test/lời gọi/thời gian) | So công cụ fuzz/random khác, hoặc có biến thể random nhưng không nêu cùng ngân sách | Không có baseline |
| O · thước đo | Số mutant bị giết / mutation score | Đếm lỗi/failure/bug riêng biệt | Chỉ coverage, accuracy… |

**Số yếu tố** = số ô ✓. **Chạm** = số ô ✓ hoặc ◐ (xếp hạng phụ). **≥ 3 ô ✓ = ứng viên phản chứng** (theo bảng mẫu bước 12).

*Chuẩn hoá 15/10: 34 bài nguồn OpenAlex giữ cách chấm của Khôi (bản thử 13/10 — cùng quy tắc này); bài các nguồn khác được chấm lại theo cùng quy tắc từ bảng gộp. Điểm gốc từng người (Tùng: thang 0–2/chiều = /8; T.Duy/K.Duy: định tính) giữ nguyên trong `SLR/` của họ. Bản thử đầy đủ của Khôi: `khoi/SLR/rq-evidence-map.md`.*

## 2. Bảng tổng theo yếu tố

| Yếu tố | Giá trị trong RQ | Paper làm nền (từ bảng gộp) | Còn thiếu / cần kiểm |
|---|---|---|---|
| P · dataset | 45 yêu cầu RESTestBench (15/dịch vụ) | ✓ **chưa có** — 0 bài dùng RESTestBench. ◐ (nhiều): bBOXRT (52 dịch vụ), K49 (19 API), P12 (20 dịch vụ), K46 (4 API mã mở), K90 (9 API thật)… — xem ma trận §3 | **nền P = 0** — yếu tố yếu nhất; cần L1/L3 soi |
| I · can thiệp | EP + BVA (kết hợp) | ✓ (2, mức prompt/agent — cần kiểm chứng thêm): **TD-0002** (EP/BVA trong TSL+LLM), **TD-0015** (module G sinh EP+BVA). ◐: K101 (biên 0/1/−1), K90/K162/K34 (constraint/robustness), K66/K97/K103 (combinatorial/domain), K167 (mutation gần biên), K56 (phân lớp kiểu)… | Chưa bài nào làm can thiệp EP+BVA kết hợp **đúng nghĩa trên tham số request** + có đối chứng |
| C · đối chứng | Random đồng đều cùng ngân sách | ✓ (3): **K90** (RT vs CBT, mỗi bên 1.000 test), **K49** (random vs evolutionary, cùng thời gian — Table 8), **K102** (random vs ARTE, mỗi chiến lược 1K lời gọi) | Nền C mỏng: 3 bài; chưa bài nào uniform-random hoá + cùng request budget **trên RESTestBench** |
| O · thước đo | Số mutant riêng biệt được oracle xác nhận | ✓: **TD-0002** (mutation score 40,8% — đã qua V2; chưa tách unique/theo dạng yêu cầu) | **Chưa bài nào đếm unique oracle-confirmed mutants** trên REST. Nguồn ngưỡng dự kiến: Case 1 / 2 / 3 — ⚠️ **chưa chốt** (form lệch Case 3 vs Case 1; phải chốt trước lần chạy chính W7) |

## 3. Ma trận P · I · C · O (42 bài — N sau gộp)

| # | Mã (gộp) | Paper (năm) | Nguồn (ai · CSDL) | P | I | C | O | ✓ | Chạm | Lý do từng ô / ghi chú |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | K90 | RESTest: Black-Box Constraint-Based Testing of RESTful Web APIs (2020) | Khôi · OpenAlex (+ K22 EC-D — K.Duy · Springer) | · | ◐ | ✓ | ◐ | 1 | 3/4 | 9 API thương mại online (không gieo mutant được) · constraint-based (miền + ràng buộc) · **RT vs CBT, mỗi bên 1.000 test** · đếm failure · K22 (K.Duy · Springer) cùng paper — EC-D, gộp 1 dòng |
| 2 | K49 | Open Problems in Fuzzing RESTful APIs: A Comparison of Tools (2023) | Khôi · OpenAlex | ◐ | · | ✓ | ◐ | 1 | 3/4 | 19 API mã mở (EMB) · — · **random search vs evolutionary, cùng ngân sách thời gian** (Table 8) · đếm fault |
| 3 | K102 | ARTE: Automated Generation of Realistic Test Inputs for Web APIs (2022) | Khôi · OpenAlex | · | · | ✓ | ◐ | 1 | 2/4 | API thương mại · input thực tế từ tri thức (không phải phân hoạch) · **random vs ARTE, mỗi chiến lược 1K lời gọi** · đếm failure |
| 4 | K46 | Black-Box and White-Box Test Case Generation for RESTful APIs: Enemies… (2021) | Khôi · OpenAlex | ◐ | ◐ | ◐ | ◐ | 0 | 4/4 | 4 API mã mở · RESTest constraint-based · so EvoMaster (hộp trắng) + cấu hình hộp đen ngẫu nhiên · lỗi 5XX |
| 5 | K66 | Combinatorial testing of RESTful APIs (2022) | Khôi · OpenAlex | ◐ | ◐ | ◐ | ◐ | 0 | 4/4 | GitLab chạy cục bộ + Bing Maps · combinatorial (covering array tham số) · so RESTler · bug |
| 6 | K101 | Effective REST APIs Testing with Error Message Analysis (2025) | Khôi · OpenAlex | ◐ | ◐ | ◐ | ◐ | 0 | 4/4 | 16 API · giá trị biên (chuỗi rỗng; 0, 1, −1) + combinatorial · so 5 công cụ · bug duy nhất |
| 7 | K167 | DeepREST: Automated Test Case Generation for REST APIs Exploiting Deep… (2024) | Khôi · OpenAlex (snowball K90) | ◐ | ◐ | ◐ | ◐ | 0 | 4/4 | 11 API benchmark (đo code coverage) · mutation giá trị gần biên · cùng ngân sách số lời gọi với RestTestGen, ARAT-RL… · fault 5XX |
| 8 | K34 | RESTest: automated black-box testing of RESTful web APIs (2021) | Khôi · OpenAlex | · | ◐ | ◐ | ◐ | 0 | 3/4 | API thương mại · constraint-based · RT vs CBT (bài demo, không nêu ngân sách) · failure |
| 9 | K56 | Bootstrapping Automated Testing for RESTful Web Services (2021) | Khôi · OpenAlex | · | ◐ | ◐ | ◐ | 0 | 3/4 | 27 dịch vụ thương mại · phân lớp kiểu/định dạng tham số · so fuzzer SOTA · bug |
| 10 | K76 | Online testing of RESTful APIs: promises and challenges (2022) | Khôi · OpenAlex | · | ◐ | ◐ | ◐ | 0 | 3/4 | API công nghiệp online · bot CBT · bot ART/fuzzing, mỗi bot cùng số test · failure/fault |
| 11 | K162 / bBOXRT | A Black Box Tool for Robustness Testing of REST Services (2021) | Tùng · IEEE + Khôi (EC-D) | ◐ | ◐ | · | ◐ | 0 | 3/4 | 52 dịch vụ (có hệ chạy cục bộ) · giá trị biên/không hợp lệ theo kiểu · không có baseline · lỗi robustness |
| 12 | K07 | REST API Fuzzing by Coverage Level Guided Blackbox Testing (2021) | Khôi · OpenAlex | ◐ | · | ◐ | ◐ | 0 | 3/4 | Spree, Magento · mutation fuzzing · so RESTler · bug |
| 13 | K21 | Feedback-Guided API Fuzzing of 5G Network (2025) | Khôi · OpenAlex | ◐ | · | ◐ | ◐ | 0 | 3/4 | free5GC · fuzzing tiến hoá · so công cụ hộp đen khác · lỗ hổng/CVE |
| 14 | P12 / K81 / K55 / K39 | Automated test generation for REST APIs: no time to rest yet (2022) | Tùng · IEEE (sb) + Khôi + K.Duy (sb K39 — EC-D) | ◐ | · | ◐ | ◐ | 0 | 3/4 | 20 dịch vụ mã mở · — · so 10 công cụ, cùng thời gian · failure duy nhất |
| 15 | K68 | APIRL: Deep Reinforcement Learning for REST API Fuzzing (2025) | Khôi · OpenAlex | ◐ | · | ◐ | ◐ | 0 | 3/4 | API mã mở (VAmPI…) · mutation học bằng RL · có biến thể Rand-APIRL · bug duy nhất |
| 16 | K69 | Deriving Semantics-Aware Fuzzers from Web API Schemas (2022) | Khôi · OpenAlex | ◐ | · | ◐ | ◐ | 0 | 3/4 | 16 dịch vụ mã mở · property-based · so 8 fuzzer · defect |
| 17 | K82 | REST API Fuzzing Using API Dependencies and Large Language Models (2026) | Khôi · OpenAlex | ◐ | · | ◐ | ◐ | 0 | 3/4 | EMB + GitLab · LLM sinh giá trị · so RESTler · API phủ 5XX |
| 18 | K89 | Spec2SeqFuzz: A Category Prediction-Guided Approach for Stateful Multi… (2026) | Khôi · OpenAlex | ◐ | · | ◐ | ◐ | 0 | 3/4 | GitLab, WordPress · fuzzing nhiều bước · so MINER · lỗi tái hiện |
| 19 | K93 | DynER: Optimized Test Case Generation for Representational State Trans… (2024) | Khôi · OpenAlex | ◐ | · | ◐ | ◐ | 0 | 3/4 | WordPress, GitLab · sửa giá trị theo error · so foREST/RESTler · bug |
| 20 | K100 | FDRRestTest: Feedback-Driven Logical Testing for REST APIs (2026) | Khôi · OpenAlex | ◐ | · | ◐ | ◐ | 0 | 3/4 | 12 dịch vụ · kiểm thử logic · so 5 công cụ, cùng 600 giây · phát hiện logic/crash |
| 21 | K136 | SBFT Tool Competition 2026: REST League (2026) | Khôi · OpenAlex | ◐ | · | ◐ | ◐ | 0 | 3/4 | RESTgym · — · so RestTestGen baseline · fault detection |
| 22 | K192 | RESTing-LLAMA: Large Language Model based REST API Fuzzing (2026) | Khôi · OpenAlex (snowball K90) | ◐ | · | ◐ | ◐ | 0 | 3/4 | 15 ứng dụng mã mở · LLM + random value · so 6 công cụ · lỗ hổng |
| 23 | K32 | Empirical Comparison of Black-box Test Case Generation Tools for RESTf… (2021) | Khôi · OpenAlex | ◐ | · | ◐ | · | 0 | 2/4 | 14 dịch vụ chạy cục bộ · — · so 4 công cụ · chỉ robustness/coverage, không đếm lỗi |
| 24 | K67 | Exploring behaviours of RESTful APIs in an industrial setting (2024) | Khôi · OpenAlex | ◐ | · | ◐ | · | 0 | 2/4 | 8 SUT (EMB) · property-based · so EvoMaster · chỉ coverage |
| 25 | K37 | QuickREST: Property-based Test Generation of OpenAPI-Described RESTful… (2020) | Khôi · OpenAlex | ◐ | · | · | ◐ | 0 | 2/4 | GitLab + hệ công nghiệp · property-based ngẫu nhiên · không baseline · bug 500 |
| 26 | K60 | FuzzTheREST: An Intelligent Automated Black-Box RESTful API Fuzzer (2025) | Khôi · OpenAlex | ◐ | · | · | ◐ | 0 | 2/4 | Petstore · fuzzing RL · không baseline · lỗ hổng |
| 27 | K127 | Automated Black-Box and Manual Basis Path Testing on E-OBE Application (2026) | Khôi · OpenAlex | ◐ | · | · | ◐ | 0 | 2/4 | 1 ứng dụng · EvoMaster hộp đen · không baseline · lỗi |
| 28 | K168 | Automated Black-Box Testing of Mass Assignment Vulnerabilities in REST… (2023) | Khôi · OpenAlex (snowball K90) | ◐ | · | · | ◐ | 0 | 2/4 | case study mã mở · template tấn công · không baseline · lỗ hổng (TP) |
| 29 | K97 | Automated Specification-Based Testing of REST APIs (2021) | Khôi · OpenAlex | · | ◐ | · | · | 0 | 1/4 | API công khai · domain testing + combinatorial · không baseline · chỉ coverage |
| 30 | K103 | Research and application of RESTful API interface testing technology b… (2025) | Khôi · OpenAlex | · | ◐ | · | · | 0 | 1/4 | hệ mô phỏng · combinatorial · so 4 cách sinh khác (không random) · coverage/hiệu năng |
| 31 | K43 | WuppieFuzz: Coverage-Guided, Stateful REST API Fuzzing (2026) | Khôi · OpenAlex | ◐ | · | · | · | 0 | 1/4 | Petstore · mutation fuzzing · so chế độ hộp đen/hộp trắng của chính nó · chỉ response coverage |
| 32 | K45 | Intelligent REST API data fuzzing (2020) | Khôi · OpenAlex | · | · | · | ◐ | 0 | 1/4 | dịch vụ Azure · fuzz payload theo luật · không baseline · bug |
| 33 | K191 | Automated REST API Black-box Test Generation in Practice: An Experienc… (2026) | Khôi · OpenAlex (snowball K90) | · | · | · | ◐ | 0 | 1/4 | hệ nội bộ công ty · RestTestGen/DeepREST · không baseline · lỗi |
| 34 | K166 | Deep Learning-Based Prediction of Test Input Validity for RESTful APIs (2021) | Khôi · OpenAlex (snowball K90) | · | · | · | · | 0 | 0/4 | API thương mại · bộ lọc tính hợp lệ cho input random · không baseline sinh test · accuracy |
| 35 | K52 / P53 | Specification and Automated Analysis of Inter-Parameter Dependencies in Web APIs (2022) | Tùng · IEEE | ◐ | ◐ | ◐ | ◐ | 0 | 4/4 | 3 operation thương mại · EP vận hành (½ request không hợp lệ) · random vs IDLReasoner cùng 1.000 req/nhánh (uniform chưa xác nhận) · failures 67/1.209 |
| 36 | P17 / K84 | Enhancing REST API Testing with NLP Techniques (2023) | Tùng · IEEE (sb) | ◐ | ◐ | · | ◐ | 0 | 3/4 | 9 dịch vụ · EP vận hành qua Tcases (chạy thật) · so schema gốc vs tăng cường (không nhánh random) · 2XX 21,8→26,2% · coverage |
| 37 | P38 / K108 | TestGPT-Server: Testing Microservices with LLMs at ByteDance (2025) | Tùng · IEEE (sb) | ◐ | ◐ | ◐ | ◐ | 0 | 4/4 | 14.366 API ByteDance · lớp giá trị semantic (EP vận hành) · ablation targeted/fuzzing/combined (không phải uniform random) · 52 bugs dev-xác nhận |
| 38 | R021 | Generating RESTful API Test Scripts with DB Constraints using OpenAPI (2024) | Lâm · ACM | ◐ | · | · | · | 0 | 1/4 | REST API + OpenAPI + ràng buộc DB · chưa thấy EP/BVA trong dữ liệu trích xuất · chưa có baseline · bằng chứng mỏng (chờ bổ sung) |
| 39 | TD-0002 | Combining TSL and LLM to Automate REST API Testing: A Comparative Study (2025) | T.Duy · Scholar | ◐ | ✓ | · | ✓ | 2 | 3/4 | 6 dự án REST API mã nguồn mở · **EP/BVA ở prompt + HTTP tests** · chưa có nhánh random cùng ngân sách · **mutation score 40,8%** |
| 40 | TD-0015 | Orchestration architecture of AI agents for automated API testing (2026) | T.Duy · Scholar | ◐ | ✓ | · | · | 1 | 2/4 | FastAPI 5 endpoint/18 tham số · **module G sinh EP+BVA** · không có nhánh random · coverage yêu cầu 90,2% |
| 41 | K02 | Test Amplification for REST APIs via Single and Multi-agent LLM Systems (2026) | K.Duy · Springer | · | · | · | ◐ | 0 | 1/4 | REST API · coverage/bug detection (không số liệu trong abstract) |
| 42 | K33 | Integrated Executive Dashboard on the PPMPP Portal (2026) | K.Duy · Springer | ◐ | ◐ | · | · | 0 | 2/4 | dashboard dùng RESTful API · EP ở mức kịch bản chức năng |

*Ô "·" = paper khác RQ ở yếu tố đó; nếu paper giống 3/4 thì khác biệt này là đóng góp của nhóm.*

*2 bài Springer (K.Duy, #41–42): trích xuất từ metadata/abstract; V2 chốt 16/10 — 5 bài khác của nguồn này bị loại (EC-A), K22/K39 đã gộp EC-D.*

## 4. Ứng viên phản chứng (Gần RQ ≥ 3 yếu tố ✓)

**Kết quả: KHÔNG có bài nào đạt ≥ 3 ô ✓** trong tập gộp 42 bài (kể cả 2 bài Springer ở bảng chính — cao nhất: TD-0002 đạt **2 ✓**).

- **Vì sao rỗng:** nền P = 0 ✓ (chưa ai dùng RESTestBench) và O ≈ 0 ✓ (chưa ai đếm mutant trên REST) → một bài muốn đạt ≥ 3 phải có I+C+O hoặc I+C+P cùng lúc, mà chưa bài nào kết hợp I với C/O trên cùng một thực nghiệm.
- **Hệ quả cho RBL-2:** không có ứng viên 4/4 (replication) hay 3/4 (extension) → **tính mới của RQ còn nguyên**; việc "kiểm phản chứng" Tuần 7 chuyển thành *săn tìm có mục tiêu* qua các lớp L1–L3 + soi danh sách ưu tiên §5.
- **Phạm vi:** tập include sau gộp 42 bài (bản 3 — 16/10 cuối: K.Duy chốt V2; loại 5 bài EC-A của K.Duy + 5 REVIEW của Tùng; K22≡K90 và K39≡No Time đã gộp; không đưa bài bị loại theo IC-T vào danh sách này). Mọi hàng ở §5 ghi rõ ai tìm ra (nguồn nào).

## 5. Danh sách ưu tiên kiểm ở RBL-2 (chạm ≥ 3/4 hoặc ≥ 2 ✓) — kèm người phụ trách

| Hạng | Mã | Paper | ✓ | Chạm | Vì sao đáng kiểm | Ai tìm (nguồn) |
|---|---|---|---|---|---|---|
| 1 | **TD-0002** | RestTSLLM — TSL+LLM | **2 (I, O)** | 3/4 | Cấu trúc gần nhất RQ: EP/BVA + **mutation score**; thiếu nhánh random cùng ngân sách | T.Duy · Scholar |
| 2 | K90 | RESTest CBT vs RT | 1 (C) | 3/4 | Thí nghiệm đối chứng giống nhất (CBT vs RT, mỗi bên 1.000 test; 100% vs 40,1% valid; 4.278 vs 2.920 failure) | Khôi · OpenAlex |
| 3 | K49 | Open Problems in Fuzzing RESTful APIs | 1 (C) | 3/4 | Random search vs evolutionary **cùng ngân sách thời gian** (52,9% vs 45,4%; 39,9 vs 36,5 lỗi — Table 8) | Khôi · OpenAlex |
| 4 | K102 | ARTE — realistic inputs | 1 (C) | 2/4 | Random vs ARTE cùng 1K lời gọi/operation (20% vs 57,3% valid) | Khôi · OpenAlex |
| 5 | K46, K66, K101, K167 | Enemies/Allies · RestCT · EmRest · DeepREST | 0 | 4/4 (◐) | Chạm đủ 4 yếu tố ở mức gần; **K101 gần I nhất** (giá trị biên 0/1/−1 + combinatorial) | Khôi · OpenAlex (K167: snowball) |
| 6 | K162 / bBOXRT | Robustness testing | 0 | 3/4 | BVA thực tế (min/max±1, Fig 3: 211/210) + robustness; **không có nhánh random cùng ngân sách** | Tùng · IEEE + Khôi (EC-D) |
| 7 | K52 / P53 | IDLReasoner inter-parameter deps | 0 | 4/4 | EP vận hành + random vs IDLReasoner cùng 1.000 request/bên | Tùng · IEEE |
| 8 | P12 / K81 / K55 / K39 | No Time to Rest Yet | 0 | 3/4 | Tcases (EP vận hành) trong 10 công cụ; so sánh công cụ cùng ngân sách thời gian | Tùng · IEEE (sb) + Khôi + K.Duy (sb) |
| 9 | P17 / K84 | NLPtoREST | 0 | 3/4 | EP qua Tcases; tăng cường schema bằng NLP | Tùng · IEEE (sb) |
| 10 | P38 / K108 | TestGPT-Server ByteDance | 0 | 4/4 | Lớp giá trị semantic (EP vận hành); 52 bugs dev-xác nhận | Tùng · IEEE (sb) |
| 11 | K76 | Online testing of RESTful APIs | 0 | 3/4 | >1 triệu test online; bot CBT vs ART; 254 bug | Khôi · OpenAlex |

## 6. Phân công Tuần 7 — bước 12 (*ĐỀ XUẤT — nhóm chốt khi họp cuối tuần*)

### 6.1 Kiểm phản chứng theo nguồn (mỗi người các bài ở §5 từ nguồn mình)

- **Khôi:** K90, K49, K102, K46, K66, K101, K167, K76 (8 bài — trọng tâm; ghi vào `khoi/SLR/rq-check.md`).
- **Tùng:** bBOXRT, K52, P12/K55, P17, P38 (5 bài).
- **T.Duy:** TD-0002 (1 — ưu tiên cao nhất toàn bảng).
- **Lâm:** nguồn ACM hiện không có ứng viên ≥ 3 (R021 mức theo dõi thấp) → kiểm chéo bảng + điều phối.
- **K.Duy:** V2 chốt 16/10 — loại 5 (K04, K08, K19, K24, K27), giữ K02/K22/K33; snowball K39 đã gộp. Không còn ứng viên riêng — nhận hỗ trợ kiểm chéo.

### 6.2 Lớp tìm kiếm bổ sung L1–L3 (theo RBL-2 — mỗi người +1 lớp)

| Người | Lớp | Việc cụ thể | Ghi gì |
|---|---|---|---|
| Tùng | **L1** (IEEE) | Search thẳng RQ: ("equivalence partitioning" OR "boundary value analysis") AND ("REST API" OR "web API") AND (mutant OR "mutation score" OR "fault detection") | Số kết quả + có phản chứng không |
| Lâm | **L1** (Scholar) | Cùng query trên Google Scholar (nửa còn lại của L1) | Số kết quả + có phản chứng không |
| T.Duy | **L2** | Semantic Scholar: chọn bài 2026 mới nhất trong tập gộp (đề xuất K136 hoặc K191), xem 10–15 bài cite nó — KHÔNG lặp lượt snowball Tuần 6 | Có bài nào trả lời RQ không |
| Khôi | **L3** | 1 survey/SLR 2023+: "systematic review" AND (REST API testing OR web API testing OR API mutation) | Survey có nhắc đúng cách tiếp cận của RQ không |
| K.Duy | không | Đã xong V2 + snowball bổ sung (16/10) — hỗ trợ kiểm chéo khi cần | — |

## 7. Xác nhận trước khi sang Tuần 7

- [x] **prisma-team.md khớp số dòng evidence-table-merged.md (≥ 12 paper)** — **42 = 42** (sau khi bỏ 4 bản EC-D trên 3 cặp; gồm 2 bài Springer unique — bản 3, 16/10).
- [x] **Mỗi yếu tố P, I, C, O có ít nhất 1 paper làm nền, hoặc ghi rõ "chưa có"** — P: *chưa có* (ghi rõ); I: TD-0002 + TD-0015 (mức prompt/agent); C: K90 + K49 + K102; O: TD-0002 (mutation score — đã qua V2).
- [ ] **Mọi ứng viên phản chứng đã có người phụ trách kiểm** — không có ứng viên ≥ 3 ✓; danh sách ưu tiên §5 đã gán người theo đề xuất §6 — *chờ nhóm chốt khi họp*.

---

*Bản 3 — cập nhật 16/10/2026 từ commit `6482a9`: K.Duy chốt V2 (loại 5 EC-A, giữ K02/K22/K33; snowball bổ sung K39 → EC-D) → N = 47 → 42; 5 bài REVIEW của Tùng chốt bỏ. Bản 2 (`64458e`): Tùng tinh chỉnh trình bày; K.Duy thông báo V2. Bản thử đầu tiên (chỉ nguồn OpenAlex): `khoi/SLR/rq-evidence-map.md`.*
