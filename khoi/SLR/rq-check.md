# Kiểm chứng RQ — phần của Lâm Anh Khôi
**Nguồn phụ trách:** OpenAlex · bài #23–#30 trong `team-synthesis/evidence-table-merged.md`   **Lớp bổ sung:** không (PL không phân công L1–L3)   **Ngày:** 2026-10-18

RQ FA26-EXT-12 · PICO: **P** = 45 yêu cầu RESTestBench (15/dịch vụ) · **I** = EP + BVA · **C** = sinh ngẫu nhiên đồng đều, cùng ngân sách · **O** = số mutant riêng biệt được oracle xác nhận.
Ký hiệu: ✓ khớp đúng RQ · ◐ gần · — khác RQ (rubric `team-synthesis/rq-evidence-map.md` §1, bản 4 ngày 18/10; điểm từng bài khớp cột Gần RQ của `team-synthesis/evidence-table-merged.md` #23–#30 và `khoi/SLR/evidence-table-double-check.md`).

## 1. Bảng đối chiếu paper (ứng viên từ nguồn của tôi)

| # | Paper | P | I | C | O | Hạn chế paper nêu | Chi tiết (câu trích nguyên văn · mục/trang PDF) |
|---|---|---|---|---|---|---|---|
| 23 | K69 · Deriving Semantics-Aware Fuzzers from Web API Schemas (Schemathesis, ICSE-Companion 2022) | ◐ 16 dịch vụ mã mở trong container, không RESTestBench | ◐ property-based theo miền schema + negative testing, không EP/BVA | ◐ so 7 fuzzer khác, 30 lượt; không có nhánh random đồng đều | ◐ đếm defect duy nhất (Sentry), không đếm mutant | (a) Phát hiện lỗi không ổn định giữa các lượt chạy; (b) khi chấm phải dùng thêm log server để gộp lỗi trùng | (a) "APIFuzzer, Cats, and Schemathesis are less consistent for all but the easiest defects." · tr. 8 · (b) "our evaluation harness uses additional information from server logs to deduplicate internal errors" · tr. 8 |
| 24 | K76 · Online testing of RESTful APIs: promises and challenges (ESEC/FSE 2022) | ◐ 13 API công nghiệp online, có LanguageTool/Ohsome mã mở | ◐ bot CBT + nhiễu dữ liệu ngoài miền | ◐ có bot RT/ART/CBT nhưng tổng ngân sách khác nhau | ◐ failure → cụm lỗi → bug xác nhận tay, không mutant | (a) Mẫu API có thể chưa đại diện; (b) quota/bị chặn làm hỏng dữ liệu failure | (a) "We tested 13 industrial APIs comprising 189 operations in total, although this might not be a sufficiently representative sample." · §7 Threats, tr. 11 · (b) "all test cases started to fail at 60% of the overall test budget, because we were banned" · §4.1, tr. 6 |
| 25 | K103 · Research and application of RESTful API interface testing technology based on simulation environment construction (IJHSA 2025) | — hệ mô phỏng, không nêu tên/cỡ API | ◐ combinatorial (cây không gian nghiệm + tham lam) | — so 4 cách sinh khác, không có random | — chỉ coverage + hiệu năng | Chưa xử lý tình huống bất thường khi tải cao trong bước sinh test | "In the future, we can try to consider the abnormal situation in high concurrency scenarios in the test case generation stage" · §IV Conclusion, tr. 9 |
| 26 | K32 · Empirical Comparison of Black-box Test Case Generation Tools for RESTful APIs (SCAM 2021) | ◐ 14 dịch vụ mã mở chạy Docker | — bài so sánh 4 công cụ (quy tắc I theo can thiệp của chính bài) | ◐ so 4 công cụ cùng 10 phút; không có nhánh random đồng đều | — chỉ robustness + coverage spec, không đếm lỗi | (a) Spec phải sửa tay; (b) kết quả có thể không đúng với REST API khác | (a) "7 of them contained small errors in the specification … we manually fixed these errors" · §V, tr. 8 · (b) "we cannot assume that our results hold for any other arbitrary REST API. Additional experiments on new case studies are needed" · §V-E Threats, tr. 9 |
| 27 | K43 · WuppieFuzz: Coverage-Guided, Stateful REST API Fuzzing (ICISSP 2026) | ◐ chỉ Petstore (mã mở) | — fuzz bằng mutation, không EP/BVA | ◐ so chế độ hộp đen/hộp trắng + 6 scheduler của chính công cụ | — chỉ response coverage + số request | (a) Chưa tự rút gọn chuỗi request gây lỗi; (b) cần thêm thực nghiệm để so với công cụ khác | (a) "automated deriving of a minimal sequence of requests that leads to the same behaviour is of interest" · §6, tr. 10 · (b) "experiments in a white-box setting can improve insights in the effectiveness of the fuzzer compared to others" · §6, tr. 10 |
| 28 | K45 · Intelligent REST API data fuzzing (ESEC/FSE 2020) | — dịch vụ Azure online (thương mại) | ◐ luật fuzz vi phạm kiểu/miền schema (DROP/SELECT/TYPE/DUPLICATE) | ◐ so RESTler gốc + random search | ◐ 17 nhóm bug sau gộp tay, không mutant | (a) Nhiều biến thể bị gộp thành 1 bug; (b) chưa kiểm loại lỗ hổng thuộc tính (vd is_admin) | (a) "we grouped all these together for the sake of brevity" · §6.4, tr. 10 · (b) "In future work, we plan to explore how to extend our implementation to check for such vulnerabilities." · §6.5, tr. 11 |
| 29 | K82 · REST API Fuzzing Using API Dependencies and Large Language Models (Eng. Proc. 2025) | ◐ 9 dịch vụ EMB + GitLab | — LLM sinh giá trị + phụ thuộc tài nguyên, không EP/BVA | ◐ so RESTler cùng 6 giờ; không random đồng đều | ◐ số API trả 5XX, không mutant | (a) Mô tả tham số mơ hồ làm LLM sinh sai (String date); (b) chưa xử lý phụ thuộc xác thực/phân trang | (a) "the failure of the String Date was due to an ambiguous description that specified two conflicting formats" · tr. 9 (Table 3) · (b) "It is necessary to enhance API dependency inference … such as authentication/authorization requirements and pagination logic." · §5, tr. 12 |
| 30 | K89 · Spec2SeqFuzz: A Category Prediction-Guided Approach for Stateful Multi-Step REST API Fuzzing (Electronics 2026) | ◐ GitLab + WordPress (mã mở) | — dự đoán nhóm endpoint cho chuỗi nhiều bước, không EP/BVA | ◐ so MINER + ablation chuỗi ngẫu nhiên | ◐ lỗi tái hiện được, không mutant | Chỉ 2 hệ, 1 baseline chính, không lặp lại/không kiểm định thống kê | "A broader evaluation would ideally include more heterogeneous APIs, additional recent baselines, and repeated runs with appropriate statistical analysis." · §5.4, tr. 27 · "does not include repeated randomized trials or statistical testing yet" · "Scope of interpretation", tr. 17 |

**Kết luận phần của tôi:** **không có phản chứng.** Trong 8 bài, không bài nào có ô ✓ nào (0/4 ✓). Bài gần nhất chỉ "chạm" 4/4 ở mức ◐: K69 và K76.
- **Không bài nào dùng RESTestBench (P).**
- **Không bài nào đếm mutant (O).** Tất cả chỉ đếm failure, bug hoặc coverage.
- **Không bài nào có nhánh random đồng đều cùng ngân sách (C).**
- **Không bài nào lấy EP + BVA làm kỹ thuật chính (I).**

→ Theo bảng "Bốn kết luận", phần của tôi rơi vào trường hợp **"Không paper nào giống đủ 4 yếu tố"**: RQ đứng vững trong phạm vi tài liệu đã tìm.

**Gợi ý cho PL khi gộp bảng gap (chỉ là đề xuất, PL quyết định):**
- Hạn chế "chỉ đo failure/coverage, không đo mutant" có ở cả 8 bài. Nhưng các bài **không tự nêu** điều này, đây là nhận xét của người đọc (REVIEWER_INFERRED). Vì vậy **không được đếm** nó là "paper nêu hạn chế".
- K76 cùng nhóm tác giả với K90, K34, K46, K102, K52 (Martin-Lopez/Segura/Ruiz-Cortés), nên khi đếm gap thì tính chung là 1.
- K89 ("chỉ 2 hệ") và K32 ("chưa chắc đúng với API khác") có thể gộp vào dòng gap "ít SUT / khó khái quát" (loại GAP-D).

## 2. Lớp tìm kiếm bổ sung (nếu được phân công)
Không được phân công L1–L3. Bảng gộp có N = 42 ≥ 12, nên cổng P1 đã đạt.

## 3. Ghi chú khả thi từ các paper tôi đọc
| Paper | Code / artifact | Cỡ mẫu, ngân sách họ dùng | Khó khăn họ báo |
|---|---|---|---|
| K69 | github.com/schemathesis/web-api-fuzzing-project (16 dịch vụ trong container + dữ liệu thô) | 16 API × 30 lượt | Kết quả không ổn định giữa các lượt; phải dùng log server để gộp lỗi trùng |
| K76 | Zenodo 10.5281/zenodo.6941292 (RESTest, script) | 13 API, 15 ngày, 1.101.846 test | Quota, bị chặn API (DHL ở mốc 60% ngân sách) → **nên chạy SUT cục bộ, không gọi API online** |
| K103 | Không công bố | ≤ 50 test, 150–1.050 luồng | Không đủ thông tin để tái lập |
| K32 | Gói replication "to be disclosed" (chưa có link) | 14 API Docker, 10 phút × 10 lượt/công cụ | 7/14 spec lỗi phải sửa tay; RESTest chỉ chạy được 2/14 → **phải kiểm spec OpenAPI của RESTestBench trước khi chạy** |
| K43 | github.com/TNO-S3/WuppieFuzz (Apache 2.0) | Petstore, 10 phút/lượt | Coverage chững sau khoảng 27% |
| K45 | Không công bố (dựa trên RESTler) | 14.964 test / 232 phút (DNS) | Phải phân loại lỗi bằng tay |
| K82 | Không công bố | 6 giờ/dịch vụ, Llama-3-8B chạy cục bộ | Mô tả tham số mơ hồ làm sinh giá trị sai |
| K89 | github.com/horis-dev/Spec2SeqFuzz | 12 giờ/hệ, chạy trong VM có snapshot | Chưa lặp lại, chưa kiểm định thống kê |

**Rút ra cho Bước 3:**
- Nên đặt ngân sách theo **số request** (giống K90, K34, K191), không theo thời gian.
- Nên chạy **lặp ≥ 10 lần**, vì K69 cho thấy kết quả lệch giữa các lượt và K89 bị chính tác giả nêu là thiếu lặp lại.
- Cần **kiểm spec OpenAPI** của RESTestBench trước khi chạy, vì K32 phải sửa tay 7/14 spec.

## 4. Nhãn tính mới (bước cá nhân 3)
- Nhãn trên thẻ RQ: **extension** (mã thẻ FA26-**EXT**-12).
- Nhãn đề xuất từ phần của tôi: **extension**. Lý do: không bài nào trong 8 bài giống từ 3/4 yếu tố trở lên. Riêng paper gốc **RESTestBench (2026)**, xem mục 5, đã khớp đúng **P** (RESTestBench) và **O** (requirements-based mutation score). RQ của nhóm khác ở **I** (EP + BVA thay vì LLM) và **C** (random đồng đều cùng ngân sách). Paper đó **không có** baseline EP/BVA hay random.

## 5. Rà nghiên cứu mạnh nhất 12 tháng gần đây (bước cá nhân 4)
Truy vấn (tìm ngày 2026-10-18; ghi vào `search-log.md`):
1. `REST API test generation 2026 ICSE OR FSE OR ISSTA OR TOSEM black-box mutation score`
2. `RESTestBench mutation testing REST API test generation benchmark`

Thứ tự ưu tiên khi chọn: cùng bài toán và metric trước, rồi đến venue/benchmark lớn, cuối cùng mới xét độ mới.

| Paper | Vì sao chọn | Họ đo gì | RQ của nhóm đo thêm điều gì họ chưa đo |
|---|---|---|---|
| **RESTestBench: A Benchmark for Evaluating the Effectiveness of LLM-Generated REST API Test Cases from NL Requirements** — Kogler et al., arXiv 2604.25862 (04/2026, bài blog tác giả ghi được nhận ở EASE 2026) | Đúng bài toán và đúng metric của RQ; là nguồn của P | 3 dịch vụ, 106 yêu cầu, 228 mutant; 10 LLM; requirements-based mutation score (Eq. 1, Table 3) | Họ chỉ thử LLM. Họ **không** có baseline EP/BVA hay random cùng ngân sách. Tác giả tự nêu: "Our benchmark includes only three services" và "Each experiment was executed only three times" (§6) |
| **MASTOR: A Multi-Agent Approach to Semantic Test Oracle Generation for RESTful APIs** — Deng et al., ACM 2026 (arXiv 2606.10465) | Cùng metric (mutation score bằng PITest), 13 API mã mở | Oracle do LLM sinh, mutation score trung bình 75,4% | Họ tập trung vào **oracle**, không phải thiết kế input. RQ của nhóm cố định oracle và so sánh kỹ thuật sinh input (EP+BVA vs random) |
| **RESTOR: Automated Test Oracle Generation for RESTful APIs via Reinforcement Learning** — Zhou et al., ISSTA 2026 | Venue lớn, mới nhất | Assertion từ cặp request/response, F1 85,42%, dữ liệu công nghiệp | Họ dùng dữ liệu nội bộ, không đếm mutant, không so kỹ thuật sinh input |

Loại: MioHint (arXiv 2504.05738), vì đây là kiểm thử hộp trắng và xuất bản 04/2025, nằm ngoài 12 tháng gần nhất.

⚠️ **Cần báo PL ngay:** paper gốc RESTestBench có **106 yêu cầu trên 3 dịch vụ** (63 / 14 / 29), không phải "45 yêu cầu, 15 mỗi dịch vụ" như trong P của nhóm. Cần xác nhận 45 = 15×3 là **tập con nhóm tự chọn** và ghi rõ cách chọn. Nếu không ghi, giảng viên sẽ hỏi.

Nguồn: [RESTestBench (arXiv)](https://arxiv.org/pdf/2604.25862) · [EASE 2026 (blog tác giả)](https://research.casablanca.at/post/restestbench-evaluating-llm-generated-api-tests--our-latest-paper-accepted-at-ease-2026) · [MASTOR (arXiv)](https://arxiv.org/pdf/2606.10465) · [RESTOR (ISSTA 2026)](https://conf.researchr.org/details/issta-2026/issta-2026-research-papers/94/RESTOR-Automated-Test-Oracle-Generation-for-RESTful-APIs-via-Reinforcement-Learning)
