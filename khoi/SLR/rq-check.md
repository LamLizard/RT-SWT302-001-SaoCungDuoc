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
- **Nhãn trên thẻ RQ: chưa xác định.** Thẻ chỉ ghi mã FA26-EXT-12, loại và độ khó, không hiển thị nhãn new / extension / replication. Ý nghĩa của "EXT" trong mã chưa được xác nhận (các đề khác có mã W4, W5…); nhóm đã mail hỏi giảng viên ngày 18/10.
- **Nhãn theo bảng "Bốn kết luận": new (trong phạm vi tài liệu đã xét).** Lý do:
  - 8 bài của tôi: không bài nào có ô ✓ (0/4).
  - Toàn bảng gộp 42 bài: cao nhất 2/4 ✓ (TD-0002).
  - Paper gốc RESTestBench (mục 5): khớp 2/4 (P, O), khác I và C.
  - Req2REST-Guard (mục 5, bài duy nhất tìm được dùng RESTestBench): 2/4 (P, O); I là LLM, C là Manual/EvoMaster/GPT, không có random đồng đều cùng ngân sách.
  - Không paper nào giống từ 3/4 trở lên → chưa đủ điều kiện extension theo bảng.
- **Ghi chú:** RQ dùng lại benchmark và thước đo của RESTestBench, chỉ đổi I (EP + BVA) và C (random đồng đều cùng ngân sách). Nếu giảng viên xác định nhãn theo nghĩa "mở rộng một nghiên cứu có sẵn" thì có thể đổi sang extension; khi có trả lời sẽ cập nhật và ghi lý do thay đổi.

## 5. Rà nghiên cứu mạnh nhất 12 tháng gần đây (bước cá nhân 4)
Khôi tự chạy trên **Google Scholar**, ngày 2026-10-18, lọc **2025–2026**, sắp theo relevance (đã ghi vào `search-log.md` mục 8):
1. `"REST API" "test generation" "mutation score"` → khoảng 44 kết quả.
2. `"RESTestBench"` → 5 kết quả.

Thứ tự ưu tiên khi chọn: cùng bài toán và metric trước, rồi đến venue/benchmark lớn, cuối cùng mới xét độ mới.

| Paper | Vì sao chọn | P / I / C / O | RQ của nhóm đo thêm điều gì họ chưa đo |
|---|---|---|---|
| **RESTestBench: A Benchmark for Evaluating the Effectiveness of LLM-Generated REST API Test Cases from NL Requirements** — Kogler et al., arXiv 2604.25862 (04/2026, tác giả ghi được nhận ở EASE 2026) | Đúng bài toán và đúng metric của RQ; là nguồn của P | ✓ / — / — / ✓ → **2/4**. 3 dịch vụ, 106 yêu cầu, 228 mutant; 10 LLM; requirements-based mutation score (Eq. 1, Table 3) | Chỉ thử LLM, **không** có baseline EP/BVA hay random cùng ngân sách. Tác giả tự nêu: "Our benchmark includes only three services" và "Each experiment was executed only three times" (§6) |
| **Requirement-Aware LLM Testing for Backend REST APIs (Req2REST-Guard)** — Xue, Ying, Ding, Wang, Qing, Hu, 2026, bản PDF trên ResearchGate (6 trang, không ghi venue) | Bài duy nhất trong kết quả **dùng RESTestBench** và đo mutation score | ✓ / — / ◐ / ✓ → **2/4**, chạm 3/4. P: "three REST services from the RESTestBench benchmark … 106 … requirements … 228 … mutations" (§IV-B, tr. 4). I: GPT-4o + bộ kiểm tra assertion. C: Manual, EvoMaster, GPT-OAS, GPT-NL (§IV-C, tr. 4), không có random đồng đều cùng ngân sách. O: "percentage of requirement-based mutants killed", MS 61,0% (Table I, tr. 4) | Không thử kỹ thuật không dùng AI (EP + BVA), không có đối chứng random cùng ngân sách, không đếm mutant theo dạng yêu cầu. Tác giả tự nêu: "has not yet been validated on large-scale real-world REST APIs" (§VII, tr. 6) |
| **MASTOR: A Multi-Agent Approach to Semantic Test Oracle Generation for RESTful APIs** — Deng et al., ACM 2026 (arXiv 2606.10465) | Cùng metric (mutation score bằng PITest), 13 API mã mở | — / — / — / ✓ → 1/4 | Tập trung vào **oracle**, không phải thiết kế input. RQ của nhóm cố định oracle và so sánh kỹ thuật sinh input (EP + BVA vs random) |

**Lưu ý về độ tin cậy của Req2REST-Guard (nhận xét của người đọc):**
- Tên 3 dịch vụ trong bài (Features-Service, REST-Countries, CatFactAPI) **khác** 3 dịch vụ trong paper RESTestBench gốc (FastAPI template, TodoApp, RealWorld), dù tổng 106 yêu cầu và 228 mutant trùng khớp.
- Table I có cột bị lệch so với văn bản. Ví dụ văn bản ghi EvoMaster "highest executability (95.2%) … only 25.6% requirement coverage", nhưng trong bảng hai số này nằm ngược cột. Dòng GPT-NL trong bảng cũng không khớp số trong văn bản (58,5 / 51,2 / 20,8).
- Bài chưa có venue, nhiều tài liệu tham khảo không liên quan tới kiểm thử.
→ Chỉ dùng bài này để đối chiếu tính mới, **không dùng làm nguồn số liệu chính**.

**Đã loại:**
- Combining TSL and LLM… (Barradas et al., 2025): đã có trong bảng gộp (TD-0002).
- Req2test (França et al., 2026): sinh unit test từ user story, khác bài toán.
- A Comparative Survey of Mutation Testing… (Falah & Routaib, 2025) và LLM-Based Test Generation: Information Sources… (Liang et al., 2026): bài survey.
- Bài tiếng Ukraina (Хацько, Назарова), Multi-level testing of conversational AI systems (Masserini, 2026), A quantized LLM driven framework… (Ahmed, 2026), luận án Sue (2025), TestPrism (Li et al., 2026), TestSuiteBench (Egashira et al., 2026): khác bài toán (không phải sinh test REST API đo bằng mutant).
- RESTOR (ISSTA 2026): không xuất hiện trong 2 truy vấn Scholar trên; bản nháp trước có nhắc nhưng đã bỏ vì dùng dữ liệu công nghiệp nội bộ và không đo mutant.

**Kết luận mục 5:** không paper nào trong 12 tháng gần đây giống RQ từ 3/4 yếu tố trở lên. Hai bài dùng RESTestBench (RESTestBench, Req2REST-Guard) đều chỉ thử LLM; RQ của nhóm đo điều họ chưa đo: **kỹ thuật thiết kế input không dùng AI (EP + BVA) so với random đồng đều cùng ngân sách**, trên cùng benchmark và cùng thước đo mutant.

⚠️ **Cần báo PL:** paper gốc RESTestBench có **106 yêu cầu trên 3 dịch vụ**, không phải "45 yêu cầu, 15 mỗi dịch vụ" như trong P của nhóm. Cần xác nhận 45 = 15×3 là **tập con nhóm tự chọn** và ghi rõ cách chọn.

Nguồn: [RESTestBench (arXiv)](https://arxiv.org/pdf/2604.25862) · [EASE 2026 (blog tác giả)](https://research.casablanca.at/post/restestbench-evaluating-llm-generated-api-tests--our-latest-paper-accepted-at-ease-2026) · [Req2REST-Guard (ResearchGate)](https://www.researchgate.net/publication/407162719_Requirement-Aware_LLM_Testing_for_Backend_REST_APIs) · [MASTOR (arXiv)](https://arxiv.org/pdf/2606.10465)
