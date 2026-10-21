# Kiểm chứng RQ — FA26-EXT-12 · SaoCungDuoc

Tài liệu giữ 6 mục của [mẫu RBL-2](RBL-2-Kiem-chung-RQ-full.md). Đầu vào: [merge 59 bài](evidence-table-merged.md), [map PICO](rq-evidence-map.md) và các PDF gốc được dẫn tại từng đối chiếu. Bộ evidence gồm **42 bài INCLUDE qua screening + 17 bài nền GV-01–GV-17 = 59 bài**; 17 bài nền không cộng vào PRISMA final.

## 1. RQ + PICO

**RQ nhóm:** Trên 106 yêu cầu bản vague của RESTestBench, prompt có hướng dẫn kỹ thuật EP+BVA và prompt single-step gốc của benchmark khác nhau thế nào về **MS_φ**, khi dùng cùng một mô hình ngôn ngữ và cùng temperature?

**H0:** Không có khác biệt về MS_φ giữa prompt có hướng dẫn EP+BVA và prompt single-step gốc, với cùng mô hình, cùng temperature và cùng 106 yêu cầu.

**H1:** Có khác biệt về MS_φ giữa hai prompt dưới cùng điều kiện.

| Yếu tố | Nội dung |
|---|---|
| **P** | **106 yêu cầu bản vague** của RESTestBench: 63 FastAPI + 29 NestJS RealWorld + 14 TodoApp. |
| **I** | Prompt yêu cầu LLM phân hoạch tương đương và chọn giá trị biên từ requirement + OpenAPI schema trước khi viết một test. |
| **C** | Prompt single-step gốc của RESTestBench, không có bước EP/BVA. |
| **O** | **MS_φ** = số mutant được test tương ứng pass-valid/fail-mutant phát hiện / **228 mutant**; mẫu số theo dịch vụ là **141/65/22**. Báo cáo từng run và trung bình mô tả ba run theo §1.1. |
| **S** | Cùng một model, cùng temperature, **3 lần chạy độc lập**; so sánh paired theo requirement. |

**Điều kiện dùng chung:** mỗi requirement sinh **một test**, `INTERACTIVE=False` (không gọi SUT khi sinh), cùng model/temperature/max token, cùng phần hướng dẫn assertion gốc; chỉ khác phần hướng dẫn EP/BVA. Dùng bản vague, không trộn precise. Không đổi O hoặc cách tính MS_φ sau khi xem kết quả.

**Dữ liệu:** tại snapshot benchmark [`4decc1e36ea3dd41b64ce3e3ac6a85bc72df36ae`](https://github.com/casablancahotelsoftware/RESTestBench/tree/4decc1e36ea3dd41b64ce3e3ac6a85bc72df36ae), `data/requirements/` có **106 file** (63/29/14), tất cả có `requirement_vague` không rỗng; tổng **228 mutant** (141/65/22 theo dịch vụ), theo kiểm kê từ lượt rà soát trước. README benchmark ghi 26 NestJS/tổng 103 khác dữ liệu và [paper GV-02, Table 3](https://arxiv.org/html/2604.25862#S3.T3) — giữ **106/228**. Snapshot đã đối chiếu chưa thay cho việc khóa artifact/môi trường thực nghiệm của nhóm.

### 1.1. Định nghĩa outcome và tổng hợp ba run

Với arm `a ∈ {I, C}`, run `r ∈ {1, 2, 3}`, requirement `i` có `m_i` mutant và một test được sinh, đặt `k_{a,r,i}` là số mutant của requirement đó mà test **pass trên bản valid và fail trên bản mutant**. Nếu test fail valid thì `k_{a,r,i} = 0`; không loại requirement hoặc mutant của nó khỏi mẫu số. Đây là validity gate có sẵn trong [`src/evaluator.py`, `Evaluator.evaluate_test`](https://github.com/casablancahotelsoftware/RESTestBench/blob/4decc1e36ea3dd41b64ce3e3ac6a85bc72df36ae/src/evaluator.py), không phải đề xuất sửa metric.

- Mỗi run: `MS_φ(a,r) = Σ_i k_{a,r,i} / 228`.
- Theo dịch vụ: chỉ cộng `k` thuộc dịch vụ đó, chia **141 FastAPI / 65 RealWorld / 22 TodoApp**.
- Báo cáo cả ba điểm từng run; trung bình mô tả là `mean_MS_φ(a) = (MS_φ(a,1) + MS_φ(a,2) + MS_φ(a,3)) / 3 = Σ_r Σ_i k_{a,r,i} / (3 × 228)`. Chênh lệch mô tả là `mean_MS_φ(I) − mean_MS_φ(C)`; nhân 100 để biểu diễn bằng điểm phần trăm.

Trung bình ba run không phải union mutant bị kill qua ba test, không phải trung bình không trọng số của 106 tỷ lệ theo requirement, và không biến 228 mutant thành 684 mutant khác nhau. Cách báo cáo mô tả này không chốt estimand hoặc phép kiểm suy luận ở §4. Quy tắc xử lý lượt thiếu do lỗi sinh/hạ tầng và retry còn phải khóa; không âm thầm bỏ dòng hoặc đổi mẫu số.

Hai arm giữ cùng **hướng dẫn assertion** gốc; model vẫn sinh test và assertions cụ thể. Golden tests chỉ dùng kiểm tra benchmark/pipeline, không cung cấp cho LLM làm đáp án. Giữ evaluator/harness gốc.

## 2. Bằng chứng làm nền (N = 59 paper evidence)

### 2.1. Phạm vi đầu vào và các cổng

| Phạm vi | Số bài | Cách sử dụng |
|---|---:|---|
| INCLUDE qua screening của các nguồn, sau khử trùng | **42** | Merge #1–#42; giữ số liệu và quyết định IC/EC theo [PRISMA](prisma-team.md). |
| Bài nền do leader bổ sung | **17** | GV-01–GV-17, merge #43–#59; đọc toàn văn phần liên quan và audit PICO, không mặc nhiên INCLUDE theo IC/EC. |
| Bộ evidence của merge/map | **59 = 42 + 17** | 0 bài trùng giữa hai tập. |
| Phản chứng ngoài ma trận | Không cộng vào 59 | Chỉ dùng để kiểm tra thêm, không đổi mẫu số. |

| Cổng | Kết quả |
|---|---|
| P1 — ≥12 INCLUDE | **Đạt: 42 ≥ 12.** 17 bài nền không dùng thay số INCLUDE. |
| P2 — ≥90% có Tool/LLM | **Đạt: 42/42 = 100%.** |
| P3 — ≥50% có kết quả số | **Đạt: 42/42 có số trong bảng**; 58/59 evidence có kết quả định lượng, GV-17 chỉ định tính. |
| P4 — ≥50% có hạn chế | **Đạt: 42/42 có dữ liệu hạn chế**; 59/59 có nội dung hạn chế nhưng phải tách AUTHOR_STATED khỏi REVIEWER_INFERRED. |
| P5 — metric cụ thể | **Đạt ở mức bảng: 42/42 ghi metric**; 58/59 evidence có metric thực nghiệm mô tả được. |

### 2.2. Đối chiếu PICO cho RQ hiện hành

Bảng đầy đủ 59 dòng nằm ở [evidence table](evidence-table-merged.md); dưới đây là đối chiếu nội dung của ba paper đã được rà phần liên quan. **Điểm nền được giữ để truy vết, chưa phải điểm theo một rubric hiện hành thống nhất** (xem [map §1](rq-evidence-map.md#1-quy-tắc-chấm-ma-trận-nền-giữ-điểm-đã-ghi)). Không ghép P/I/C/O của nhiều paper để tạo một phản chứng.

| Paper | P nền | I nền | C nền | O nền | ✓ nền giữ lại | Đối chiếu với RQ hiện hành |
|---|---|---|---|---|---|---|
| **GV-02 / RESTestBench** (EASE 2026) | ✓ | · | ✓ | ✓ | **3/4** | Có 106 yêu cầu, mỗi yêu cầu gồm bản precise và vague; điều kiện vague của paper trùng với P nhóm chọn. Có single-step và MS_φ; **không có prompt hướng dẫn EP/BVA**. C✓ đã được ghi theo baseline single-step, khác rubric random nền. |
| **TD-0002** — Combining TSL and LLM to Automate REST API Testing (2025) | ◐ | ✓ | · | ✓ | **2/4** | Có boundary testing/equivalence classes trong prompt và mutation score từ Stryker.NET; 6 dự án REST, không phải RESTestBench. Không có đối chứng single-step gốc; **O✓ nền không xác nhận MS_φ**. (§3/PDF4; §4.6/PDF7–8; Table 3/PDF8.) |
| **TD-0015** — Orchestration architecture of AI agents for automated API testing (2026) | ◐ | ◐ | · | · | **0/4** | Module G sinh EP+BVA nhưng không phải prompt-guided trên RESTestBench; outcome là coverage, không phải MS_φ. |

**Giới hạn kết luận:** GV-02 là nền trực tiếp cho P/C/O qua bảng căn hàng §3.1; TD-0002 hỗ trợ hướng dẫn kỹ thuật trong prompt, TD-0015 là tham chiếu về sinh test EP+BVA. Các điểm nền 3/4, 2/4, 0/4 không đủ xếp hạng độ khớp hiện hành của cả 59 bài. Chưa tái thẩm định cả 59 theo RQ mới nên không giữ khẳng định “không có paper nào khác đạt ≥2/4”.

**Quy ước đối chiếu hiện hành (không dùng tái chấm ma trận nền trong đợt này):** P xét đúng điều kiện 106 vague trên RESTestBench; I xét hướng dẫn EP+BVA trong prompt; C xét single-step gốc; O xét đúng MS_φ với validity gate. Mutation score nói chung không tự đáp ứng O này. Không suy nhãn hoặc ưu thế thực nghiệm chỉ từ tổng số ✓ nền.

## 3. Phản chứng và nhãn

### 3.1. Paper gần nhất và bảng căn hàng

**Nhãn nhóm: `extension`.**

Paper nền gần nhất nhóm chọn là **GV-02/RESTestBench**. Bảng sau căn hàng phép so refinement với single-step của paper và phép so nhóm dự kiến; nhóm kế thừa **nhánh single-step trong điều kiện vague**, không mô tả paper như so single-step với chính nó:

| Yếu tố | GV-02 | RQ nhóm | Giống/khác | Căn cứ |
|---|---|---|---|---|
| **P** | 106 yêu cầu, mỗi yêu cầu có precise và vague; paper đánh giá cả hai điều kiện | 106 yêu cầu bản vague | **Trùng điều kiện vague**, không phải toàn phạm vi paper | GV-02 §3.2, Table 3 và §4/PDF4–8. |
| **I** | Refinement loop: sinh rồi chạy test, dùng execution/HTTP trace để sửa | Prompt có hướng dẫn EP+BVA, không gọi SUT khi sinh | **Khác** | GV-02 §4.2/PDF7–8; nhóm không kế thừa refinement làm I. |
| **C** | Prompt single-step là baseline của paper | Prompt single-step gốc | **Giống** | GV-02 §4/PDF6–8; đây là đối chứng nguyên văn của RQ. |
| **O** | Nhánh single-step dùng MS_φ; refinement còn có MS_φ^valid và MS_φ^m | MS_φ của test sinh không tương tác; pass-valid/fail-mutant, tổng /228 và theo dịch vụ /141, /65, /22 | **Kế thừa O của single-step** | GV-02 §3.4/PDF5–6; `Evaluator.evaluate_test`; công thức từng run/trung bình ba run tại §1.1. |

Nhóm giữ nhãn **extension**: kế thừa P ở điều kiện vague, baseline single-step và outcome tương ứng, rồi thêm phép so prompt-guided EP+BVA. “Một yếu tố” nói về khác biệt prompt giữa hai arm **của nhóm**, không khẳng định giữ nguyên toàn thiết kế refinement của paper. Điểm nền của 59 bài không tự chứng minh novelty; chưa có tái chấm toàn bộ theo rubric hiện hành.

**Đóng góp dự kiến:** bổ sung bằng chứng thực nghiệm về việc **prompt-guided EP/BVA** có cải thiện MS_φ so với prompt single-step gốc hay không; không đề xuất thuật toán EP/BVA mới, không tuyên bố mutation testing cho REST chưa tồn tại. Kết quả có thể dương, âm hoặc không khác biệt; cả ba đều là kết quả hợp lệ.

## 4. Khả thi của gap đang cân nhắc

Chỉ đánh giá **GAP-T — prompt-guided EP/BVA + RQ tại §1**. Các số dưới đây là ước tính từ benchmark và repo, **chưa phải kết quả pilot**.

| Tiêu chí | Căn cứ hiện có | Chấm | Việc cần xử lý |
|---|---|---|---|
| Dataset | 106 requirement vague/228 mutant đã kiểm; dùng commit benchmark và `data/requirements`, không dùng README 103. | ✅ | Khóa commit, danh sách 106 ID và manifest mutant trước khi chạy. |
| API/Tool | Cần Docker cho 3 service và một API key/model cố định; repo có `single_step_tool` và evaluator. | ⚠️ | Dựng 3 service, chạy golden test 1 requirement, xác nhận model/temperature. |
| Tính toán | Kế hoạch full: **106 × 2 arm × 3 run = 636 lượt sinh test**, **636 lượt kiểm valid**, **228 × 2 × 3 = 1.368 lượt thực thi mutant** (**684/arm**), trước setup/reset/retry. | ⚠️ | Fail valid có thể dẫn tới skip mutant, retry có thể tăng số lượt; đo thực tế trên pilot, chưa có số đo nhóm. |
| Ground truth | Benchmark có golden tests, mutant theo requirement và evaluator MS_φ với validity gate. | ✅ | Kiểm pipeline và định danh mutant; không đưa golden tests cho LLM. Model vẫn sinh assertions từ cùng hướng dẫn gốc. |
| Code base | Chỉ cần **một tool mới** copy `single_step_tool`, thay prompt; không sửa evaluator/harness. | ⚠️ | Viết prompt I, kiểm `INTERACTIVE=False`, cùng interface. |
| Kỹ năng | 5 thành viên; chưa có log tích hợp prompt tool hoặc phân công giờ công. | ⚠️ | Chốt người phụ trách setup, prompt, chạy, phân tích. |
| Thời gian | Chưa có pilot; dự kiến pilot 10 requirement × 2 arm × 1 run, sau đó full 106 × 2 × 3. | ⚠️ | Đặt hạn pilot/full và ≥3 ngày dự phòng. |

**Đếm: 2 ✅ / 5 ⚠️ / 0 ❌ — rủi ro trung bình, chưa đủ để gọi “an toàn”.** Hai ✅ chỉ xác nhận có dữ liệu và ground truth để kế thừa, chưa xác nhận môi trường chạy.

**Kế hoạch xử lý có đầu ra kiểm được:**

1. Khóa commit benchmark, 106 requirement ID và mutant manifest.
2. Viết prompt I và tool wrapper; giữ nguyên prompt C, model, temperature, assertion instructions.
3. Pilot 10 requirement thuộc một service × 2 arm × 1 run: kiểm prompt adherence, test validity, pipeline; không dùng pilot để tuyên bố effect.
4. Full 106 × 2 arm × 3 run; lưu prompt hash, token count, output, cost.
5. Báo cáo MS_φ từng run, trung bình mô tả ba run, tổng và theo dịch vụ (§1.1); khóa kế hoạch suy luận dưới đây trước chạy chính. Subgroup 15 mutant chỉ xét khi có danh sách và căn cứ phân loại.

**Kế hoạch thống kê — chưa chốt:** dữ liệu quan sát phải giữ khóa service/requirement/mutant/arm/run; ghép I/C theo cùng requirement và lưu cả ba run, không chọn run tốt nhất. Các mutant cùng requirement dùng chung test nên tạo cụm phụ thuộc; ba run là đo lặp trên cùng tập requirement/mutant, không mặc định **228 mutant hoặc 684 mutant-run là các cặp độc lập**.

Paired bootstrap theo **cụm requirement** là phương án đang cân nhắc: nếu chọn, mỗi lần lấy mẫu phải giữ cả hai arm, toàn bộ mutant và ba run của requirement đó; tính lại tỷ số có trọng số mutant tương ứng §1.1, không mặc định trung bình không trọng số các tỷ lệ requirement. Chưa chốt estimand, cách tổng hợp/ghép ba run cho suy luận, có phân tầng service hay không, cách resample, số bootstrap, CI, xử lý lỗi/retry và multiple comparisons. **McNemar thông thường trên 228 mutant chưa được chốt**; muốn phân tích nhị phân phải xử lý cả cụm requirement và đo lặp. [Durkalski et al. (2003), DOI 10.1002/sim.1438 — abstract](https://pubmed.ncbi.nlm.nih.gov/12872299/) nêu giả định độc lập giữa các cặp và vấn đề matched-pair có cụm; nguồn này không tự quyết định phép kiểm cho thiết kế nhóm. Không ghi các phương án này như đã được nhóm phê duyệt.

**Giới hạn 15 mutant — thông tin từ email GV, chưa được nhóm phân loại độc lập:** chưa có danh sách ID/requirement. Chỉ trong giả định minh họa rằng I **chỉ thay đổi chọn input**, đúng 15 mutant đó có thể đổi kết quả và 213 mutant còn lại giữ nguyên, mức tăng tối đa mới là **15/228 = 6,58 điểm phần trăm**. Đây **không phải trần chung của prompt-guided EP+BVA**: prompt còn có thể ảnh hưởng setup và assertions. Ba run không tăng số mutant khác nhau.

Với giả định minh họa khác là **15 cặp discordant độc lập** và exact McNemar hai phía: **12 thắng/3 thua cho p = 0,03515625**, **10 thắng/5 thua cho p = 0,3017578125**. Đây không phải power hoặc p-value dự kiến của nghiên cứu có cụm/ba run. Chưa biết 15 mutant thuộc dịch vụ nào; nếu tập trung ở TodoApp, đóng góp vào tổng sẽ nhỏ do mẫu số dịch vụ là 22 so với FastAPI 141 và RealWorld 65. Báo per-service và cần xin danh sách ID từ GV; không kết luận hướng dẫn vô ích hoặc hai prompt tương đương từ kết quả không có ý nghĩa thống kê.

## 5. Gap mà RQ lấp

**Gap nhóm chọn: GAP-T — đánh giá prompt-guided EP/BVA trên RESTestBench.**

### 5.1. Phát biểu gap

> Trong bộ 59 tài liệu kế thừa và các phần bằng chứng đã rà, nhóm chưa ghi nhận nghiên cứu đánh giá **prompt có hướng dẫn EP+BVA** so với **prompt single-step gốc** của RESTestBench trên **106 yêu cầu bản vague**, đo **MS_φ** trên 228 mutant. Chưa tái thẩm định toàn bộ 59 theo RQ mới.

Đây là **giả định/đề xuất của nhóm**, không phải gap mạnh AUTHOR_STATED: không có tập x/N tác giả cùng nêu limitation này. GV-02 chỉ đánh giá single-step/refinement, không đánh giá prompt-guided EP/BVA; việc paper không thử không đồng nghĩa tác giả đã thừa nhận thiếu.

### 5.2. Bảng hạn chế và độ mạnh

| Hạn chế | Paper nêu | Paper đã giải quyết | Còn lại | Mạnh/yếu | Loại |
|---|---|---|---|---|---|
| Chưa đánh giá prompt-guided EP+BVA so với prompt single-step trên 106 yêu cầu vague, đo MS_φ | Chưa ghi nhận paper nêu trực tiếp trong bằng chứng đã rà; chưa tái thẩm định cả 59 theo RQ mới | GV-02 cung cấp điều kiện vague, single-step và MS_φ; **không có I guided** | Chưa có x/N; đây là giả định của nhóm | **Giả định**, chưa xếp mạnh/yếu theo đếm | GAP-T |
| Ít dịch vụ/khó khái quát | 18/42 paper, 10 cụm — số kế thừa, chưa kiểm lại sổ quote; K89/K32 có nêu trực tiếp | GV-02 chỉ có 3 dịch vụ; không giải quyết | RQ dùng 3 dịch vụ, **không lấp GAP-D** | Tham khảo | GAP-D |
| Coverage chưa đo fault detection | GV-03 §7.3: “does not directly measure fault detection or overall test adequacy” | GV-02/TD-0002 có mutation ở thiết kế khác | 1/17 bài nền; yếu | Yếu | GAP-M |

**GAP-D** giữ làm giới hạn/bàn luận, không phải đóng góp chính. **GAP-M** chỉ hỗ trợ chọn outcome, không chứng minh thiếu phép so I/C.

### 5.3. Đối chiếu gap và RQ

**Gap:** prompt-guided EP/BVA chưa được đánh giá trên 106 yêu cầu vague của RESTestBench, với MS_φ và baseline single-step.

**RQ:** Trên 106 yêu cầu bản vague của RESTestBench, prompt có hướng dẫn EP+BVA và prompt single-step gốc khác nhau thế nào về MS_φ, cùng model và temperature?

**So với GV-02:** kế thừa điều kiện vague của 106 yêu cầu, nhánh single-step và MS_φ; bổ sung phép so prompt-guided EP/BVA. Chỉ một yếu tố prompt khác giữa hai arm nhóm; không đồng nhất với phép so refinement của paper.

### 5.4. Vì sao gap còn trống

GV-02 tập trung vào single-step/refinement và chất lượng requirement; chưa thử một prompt hướng dẫn kỹ thuật EP/BVA. Tổ hợp này chưa được ghi nhận trong bằng chứng đã rà, nhưng chưa tái thẩm định cả 59 theo RQ mới. Nguyên nhân chưa được tác giả xác nhận; nhóm không khẳng định “chưa ai làm”.

### 5.5. Lợi ích

Kỹ sư kiểm thử cần bằng chứng về hiệu quả của hướng dẫn EP+BVA khi LLM sinh test trên yêu cầu vague. Kết quả cao hơn hoặc thấp hơn phải được diễn giải cùng độ bất định, chi phí và phạm vi benchmark. Kết quả không có ý nghĩa thống kê chỉ cho biết chưa đủ bằng chứng về khác biệt theo thiết kế/phép kiểm đã khóa; không chứng minh hai cách tương đương hoặc hướng dẫn không hiệu quả.

## 6. Quyết định

**Giữ RQ tại §1 và nhãn `extension`.** Gap đề xuất là **GAP-T — prompt-guided EP/BVA**; GV-02/RESTestBench là nền trực tiếp theo §3.1. Bộ evidence vẫn là 59, điểm nền giữ nguyên nhưng chưa có rubric hiện hành thống nhất cho toàn bộ. Không đổi H0/H1; chưa xác minh cập nhật thẻ hoặc được GV duyệt.

**Trạng thái dữ liệu:** P = **106 yêu cầu vague**, 228 mutant. Chưa có pilot; API key, Docker 3 service, prompt I, phân công và thời gian còn phải khóa.

**Việc tiếp theo:**

1. Khóa commit benchmark, 106 ID và mutant manifest.
2. Viết prompt I, kiểm tra bằng 10 requirement; giữ prompt C nguyên văn.
3. Pilot và ghi runtime/lỗi; nếu ổn, chạy full 106 × 2 arm × 3 run.
4. Khóa kế hoạch phân tích cụm requirement và ba run tại §4 trước chạy chính; lưu prompt/model/version, báo cáo MS_φ theo §1.1. Bootstrap/McNemar chưa phải quyết định đã duyệt.
5. Xin GV danh sách 15 mutant và đối chiếu ID/requirement; báo kết quả pilot khi có. Chưa thực hiện các bước này.
