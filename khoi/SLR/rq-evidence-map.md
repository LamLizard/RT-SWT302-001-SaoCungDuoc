# Bản đồ bằng chứng cho RQ — bản thử (Khôi · OpenAlex)
*Nhóm 1 — SaoCungDuoc · RQ FA26-EXT-12 · 13/10/2026 · **BẢN THỬ**: chỉ gồm 34 bài INCLUDE của nguồn OpenAlex (Khôi); chưa gộp bảng của thành viên khác.*
*Nguồn chấm: toàn văn PDF của từng bài (xem `khoi/SLR/evidence_table.md`), AI (Claude) hỗ trợ đọc, Khôi kiểm lại.*

## 1. Quy tắc chấm

RQ (theo `review-protocol.md`): **P** = 45 yêu cầu RESTestBench (15/dịch vụ) · **I** = EP + BVA · **C** = sinh ngẫu nhiên đồng đều, cùng ngân sách · **O** = số mutant riêng biệt được oracle xác nhận.

| Yếu tố | ✓ = khớp đúng giá trị RQ | ◐ = gần (không tính vào "Số yếu tố") | Trống |
|---|---|---|---|
| P · dataset | Dùng RESTestBench | Dịch vụ REST mã mở chạy cục bộ (có mã nguồn → gieo mutant được như RESTestBench) | API thương mại/online, hệ nội bộ |
| I · can thiệp | Kỹ thuật chính là EP và/hoặc BVA | Phân hoạch/ràng buộc miền, combinatorial theo tham số, giá trị biên/không hợp lệ, phân lớp theo kiểu | Không có |
| C · đối chứng | So với sinh ngẫu nhiên **cùng ngân sách** (số test/lời gọi/thời gian) | So với công cụ fuzz/random khác, hoặc có biến thể random nhưng không nêu cùng ngân sách | Không có baseline |
| O · thước đo | Số mutant bị giết / mutation score | Đếm lỗi/failure/bug riêng biệt | Chỉ coverage, accuracy… |

**Số yếu tố** = số ô ✓ (đúng luật của bảng mẫu). Cột **Chạm** = số ô ✓ hoặc ◐, chỉ để xếp hạng phụ.

## 2. Bảng tổng theo yếu tố

| Yếu tố | Giá trị trong RQ | Paper làm nền | Còn thiếu / cần kiểm |
|---|---|---|---|
| P · dataset | 45 yêu cầu RESTestBench (15/dịch vụ) | ✓: **chưa có**. ◐ (24 bài): K49, K46, K66, K101, K167, K162, K07, K21, K55, K68, K69, K82, K89, K93, K100, K136, K192, K32, K67, K37, K60, K127, K168, K43 | Không bài nào dùng RESTestBench → **nền P = 0** |
| I · can thiệp | EP + BVA | ✓: **chưa có**. ◐ (11 bài): K90, K46, K66, K101, K167, K34, K56, K76, K162, K97, K103 | Chưa bài nào dùng EP + BVA đúng nghĩa giáo trình; gần nhất K101 (giá trị biên 0/1/−1, chuỗi rỗng), K162 (biên/không hợp lệ), K90/K34 (ràng buộc miền) |
| C · đối chứng | Random đồng đều, cùng ngân sách | ✓ (3 bài): **K90, K49, K102**. ◐ (20 bài): K46, K66, K101, K167, K34, K56, K76, K07, K21, K55, K68, K69, K82, K89, K93, K100, K136, K192, K32, K67 | Nền C mỏng: 3 bài |
| O · thước đo | Số mutant riêng biệt được oracle xác nhận | ✓: **chưa có**. ◐ (28 bài): K90, K49, K102, K46, K66, K101, K167, K34, K56, K76, K162, K07, K21, K55, K68, K69, K82, K89, K93, K100, K136, K192, K37, K60, K127, K168, K45, K191 | Không bài nào đếm mutant (K49 nêu chưa có công cụ mutation cho system test REST) → **nền O = 0**. Nguồn ngưỡng dự kiến: Case 1 / 2 / 3 — *chưa có tài liệu định nghĩa, để trống* |

## 3. Ma trận P · I · C · O (34 bài, xếp theo Số yếu tố ✓ rồi số ô chạm)

| # | Mã | Paper (năm) | Nhánh | P | I | C | O | Số yếu tố (✓) | Chạm | Lý do từng ô (P · I · C · O) |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | K90 | RESTest: Black-Box Constraint-Based Testing of RESTful Web APIs (2020) | CSDL | · | ◐ | ✓ | ◐ | 1 | 3/4 | 9 API thương mại online (không gieo mutant được) · constraint-based (miền + ràng buộc) · **RT vs CBT, mỗi bên 1.000 test** · đếm failure |
| 2 | K49 | Open Problems in Fuzzing RESTful APIs: A Comparison of Tools (2023) | CSDL | ◐ | · | ✓ | ◐ | 1 | 3/4 | 19 API mã mở (EMB) · — · **random search vs evolutionary, cùng ngân sách thời gian** (Table 8) · đếm fault |
| 3 | K102 | ARTE: Automated Generation of Realistic Test Inputs for Web APIs (2022) | CSDL | · | · | ✓ | ◐ | 1 | 2/4 | API thương mại · input thực tế từ tri thức (không phải phân hoạch) · **random vs ARTE, mỗi chiến lược 1K lời gọi** · đếm failure |
| 4 | K46 | Black-Box and White-Box Test Case Generation for RESTful APIs: Enemies… (2021) | CSDL | ◐ | ◐ | ◐ | ◐ | 0 | 4/4 | 4 API mã mở · RESTest constraint-based · so EvoMaster (hộp trắng) + cấu hình hộp đen ngẫu nhiên · lỗi 5XX |
| 5 | K66 | Combinatorial testing of RESTful APIs (2022) | CSDL | ◐ | ◐ | ◐ | ◐ | 0 | 4/4 | GitLab chạy cục bộ + Bing Maps · combinatorial (covering array tham số) · so RESTler · bug |
| 6 | K101 | Effective REST APIs Testing with Error Message Analysis (2025) | CSDL | ◐ | ◐ | ◐ | ◐ | 0 | 4/4 | 16 API · giá trị biên (chuỗi rỗng; 0, 1, −1) + combinatorial · so 5 công cụ · bug duy nhất |
| 7 | K167 | DeepREST: Automated Test Case Generation for REST APIs Exploiting Deep… (2024) | SB1 | ◐ | ◐ | ◐ | ◐ | 0 | 4/4 | 11 API benchmark (đo code coverage) · mutation giá trị gần biên · cùng ngân sách số lời gọi với RestTestGen, ARAT-RL… · fault 5XX |
| 8 | K34 | RESTest: automated black-box testing of RESTful web APIs (2021) | CSDL | · | ◐ | ◐ | ◐ | 0 | 3/4 | API thương mại · constraint-based · RT vs CBT (bài demo, không nêu ngân sách) · failure |
| 9 | K56 | Bootstrapping Automated Testing for RESTful Web Services (2021) | CSDL | · | ◐ | ◐ | ◐ | 0 | 3/4 | 27 dịch vụ thương mại · phân lớp kiểu/định dạng tham số · so fuzzer SOTA · bug |
| 10 | K76 | Online testing of RESTful APIs: promises and challenges (2022) | CSDL | · | ◐ | ◐ | ◐ | 0 | 3/4 | API công nghiệp online · bot CBT · bot ART/fuzzing, mỗi bot cùng số test · failure/fault |
| 11 | K162 | A Black Box Tool for Robustness Testing of REST Services (2021) | SB1 | ◐ | ◐ | · | ◐ | 0 | 3/4 | 52 dịch vụ (có hệ chạy cục bộ) · giá trị biên/không hợp lệ theo kiểu · không có baseline · lỗi robustness |
| 12 | K07 | REST API Fuzzing by Coverage Level Guided Blackbox Testing (2021) | CSDL | ◐ | · | ◐ | ◐ | 0 | 3/4 | Spree, Magento · mutation fuzzing · so RESTler · bug |
| 13 | K21 | Feedback-Guided API Fuzzing of 5G Network (2025) | CSDL | ◐ | · | ◐ | ◐ | 0 | 3/4 | free5GC · fuzzing tiến hoá · so công cụ hộp đen khác · lỗ hổng/CVE |
| 14 | K55 | Automated test generation for REST APIs: no time to rest yet (2022) | CSDL | ◐ | · | ◐ | ◐ | 0 | 3/4 | 20 dịch vụ mã mở · — · so 10 công cụ, cùng thời gian · failure duy nhất |
| 15 | K68 | APIRL: Deep Reinforcement Learning for REST API Fuzzing (2025) | CSDL | ◐ | · | ◐ | ◐ | 0 | 3/4 | API mã mở (VAmPI…) · mutation học bằng RL · có biến thể Rand-APIRL · bug duy nhất |
| 16 | K69 | Deriving Semantics-Aware Fuzzers from Web API Schemas (2022) | CSDL | ◐ | · | ◐ | ◐ | 0 | 3/4 | 16 dịch vụ mã mở · property-based · so 8 fuzzer · defect |
| 17 | K82 | REST API Fuzzing Using API Dependencies and Large Language Models (2026) | CSDL | ◐ | · | ◐ | ◐ | 0 | 3/4 | EMB + GitLab · LLM sinh giá trị · so RESTler · API phủ 5XX |
| 18 | K89 | Spec2SeqFuzz: A Category Prediction-Guided Approach for Stateful Multi… (2026) | CSDL | ◐ | · | ◐ | ◐ | 0 | 3/4 | GitLab, WordPress · fuzzing nhiều bước · so MINER · lỗi tái hiện |
| 19 | K93 | DynER: Optimized Test Case Generation for Representational State Trans… (2024) | CSDL | ◐ | · | ◐ | ◐ | 0 | 3/4 | WordPress, GitLab · sửa giá trị theo error · so foREST/RESTler · bug |
| 20 | K100 | FDRRestTest: Feedback-Driven Logical Testing for REST APIs (2026) | CSDL | ◐ | · | ◐ | ◐ | 0 | 3/4 | 12 dịch vụ · kiểm thử logic · so 5 công cụ, cùng 600 giây · phát hiện logic/crash |
| 21 | K136 | SBFT Tool Competition 2026: REST League (2026) | CSDL | ◐ | · | ◐ | ◐ | 0 | 3/4 | RESTgym · — · so RestTestGen baseline · fault detection |
| 22 | K192 | RESTing-LLAMA: Large Language Model based REST API Fuzzing (2026) | SB1 | ◐ | · | ◐ | ◐ | 0 | 3/4 | 15 ứng dụng mã mở · LLM + random value · so 6 công cụ · lỗ hổng |
| 23 | K32 | Empirical Comparison of Black-box Test Case Generation Tools for RESTf… (2021) | CSDL | ◐ | · | ◐ | · | 0 | 2/4 | 14 dịch vụ chạy cục bộ · — · so 4 công cụ · chỉ robustness/coverage, không đếm lỗi |
| 24 | K67 | Exploring behaviours of RESTful APIs in an industrial setting (2024) | CSDL | ◐ | · | ◐ | · | 0 | 2/4 | 8 SUT (EMB) · property-based · so EvoMaster · chỉ coverage |
| 25 | K37 | QuickREST: Property-based Test Generation of OpenAPI-Described RESTful… (2020) | CSDL | ◐ | · | · | ◐ | 0 | 2/4 | GitLab + hệ công nghiệp · property-based ngẫu nhiên · không baseline · bug 500 |
| 26 | K60 | FuzzTheREST: An Intelligent Automated Black-Box RESTful API Fuzzer (2025) | CSDL | ◐ | · | · | ◐ | 0 | 2/4 | Petstore · fuzzing RL · không baseline · lỗ hổng |
| 27 | K127 | Automated Black-Box and Manual Basis Path Testing on E-OBE Application (2026) | CSDL | ◐ | · | · | ◐ | 0 | 2/4 | 1 ứng dụng · EvoMaster hộp đen · không baseline · lỗi |
| 28 | K168 | Automated Black-Box Testing of Mass Assignment Vulnerabilities in REST… (2023) | SB1 | ◐ | · | · | ◐ | 0 | 2/4 | case study mã mở · template tấn công · không baseline · lỗ hổng (TP) |
| 29 | K97 | Automated Specification-Based Testing of REST APIs (2021) | CSDL | · | ◐ | · | · | 0 | 1/4 | API công khai · domain testing + combinatorial · không baseline · chỉ coverage |
| 30 | K103 | Research and application of RESTful API interface testing technology b… (2025) | CSDL | · | ◐ | · | · | 0 | 1/4 | hệ mô phỏng · combinatorial · so 4 cách sinh khác (không random) · coverage/hiệu năng |
| 31 | K43 | WuppieFuzz: Coverage-Guided, Stateful REST API Fuzzing (2026) | CSDL | ◐ | · | · | · | 0 | 1/4 | Petstore · mutation fuzzing · so chế độ hộp đen/hộp trắng của chính nó · chỉ response coverage |
| 32 | K45 | Intelligent REST API data fuzzing (2020) | CSDL | · | · | · | ◐ | 0 | 1/4 | dịch vụ Azure · fuzz payload theo luật · không baseline · bug |
| 33 | K191 | Automated REST API Black-box Test Generation in Practice: An Experienc… (2026) | SB1 | · | · | · | ◐ | 0 | 1/4 | hệ nội bộ công ty · RestTestGen/DeepREST · không baseline · lỗi |
| 34 | K166 | Deep Learning-Based Prediction of Test Input Validity for RESTful APIs (2021) | SB1 | · | · | · | · | 0 | 0/4 | API thương mại · bộ lọc tính hợp lệ cho input random · không baseline sinh test · accuracy |
| | | **Paper làm nền** | | 0 ✓ · 24 ◐ | 0 ✓ · 11 ◐ | 3 ✓ · 20 ◐ | 0 ✓ · 28 ◐ | | | |

*Ô "·" = paper khác RQ ở yếu tố đó.*

## 4. Ứng viên phản chứng

Theo luật bảng mẫu (hàng có ≥ 3 ô ✓): **không có bài nào** — tối đa chỉ đạt 1/4 ✓, vì P và O chưa có nền. Đây là phát hiện chính: các bài hiện có **không trực tiếp trả lời RQ** trên RESTestBench với thước đo mutant → khoảng trống của RQ còn nguyên.

Xếp hạng phụ (có ≥ 1 ✓ và chạm ≥ 3/4, hoặc chạm 4/4):

| Hạng | Mã | ✓ | Chạm | Vì sao đáng kiểm ở RBL-2 | Nguồn |
|---|---|---|---|---|---|
| 1 | **K90** | C | 3/4 | Cấu trúc thí nghiệm giống RQ nhất: kỹ thuật thiết kế input có cấu trúc (CBT) vs random, **cùng 1.000 test**, đếm failure (100% vs 40,1% test hợp lệ; 4.278 vs 2.920 failure) | Khôi · OpenAlex |
| 2 | K49 | C | 3/4 | Random search vs evolutionary **cùng ngân sách thời gian** trên 19 API mã mở (45,4% vs 52,9% line coverage; 36,5 vs 39,9 fault — Table 8); nhưng can thiệp là tìm kiếm hộp trắng, không phải EP/BVA | Khôi · OpenAlex |
| 3 | K102 | C | 2/4 | Random vs ARTE cùng 1K lời gọi/operation (20% vs 57,3% lời gọi hợp lệ) | Khôi · OpenAlex |
| 4–7 | K46, K66, K101, K167 | — | 4/4 (◐) | Chạm đủ 4 yếu tố ở mức gần; K101 gần I nhất (giá trị biên) | Khôi · OpenAlex (K167 từ snowballing) |

## 5. Chọn gốc snowballing

Quy tắc: gốc phải là bài INCLUDE của **nhánh CSDL**; xếp theo (1) số ✓, (2) số ô chạm, (3) nếu hoà: bài có ô I chạm đứng trước (I là can thiệp chính của RQ).
- K90 và K49 hoà ở (1) 1 ✓ và (2) 3/4 ô chạm; ở (3) K90 có I ◐ (constraint-based gần phân hoạch), K49 ô I trống → **K90 đứng đầu**.
- Kết luận: **giữ K90 làm gốc** snowballing vòng 1 như đã chạy — không cần chạy lại nhánh 2 của PRISMA.

## 6. Việc còn lại

- Gộp bảng của các thành viên khác (IEEE, ACM, Semantic/Google Scholar, snowballing của K.Duy) khi nhóm dùng chung file này.
- Hỏi giảng viên định nghĩa "Case 1 / 2 / 3" cho ngưỡng của O.
- Kiểm chéo cách chấm ✓/◐ với PL (đặc biệt cột P: "dịch vụ mã mở chạy cục bộ" có được coi là gần RESTestBench không).
