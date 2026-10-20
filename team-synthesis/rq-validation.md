# Kiểm chứng RQ — FA26-EXT-12 · SaoCungDuoc

**Cập nhật:** 20/10/2026. Giữ 6 mục của [mẫu RBL-2](RBL-2-Kiem-chung-RQ-full.md). Đầu vào: [merge 59 bài](evidence-table-merged.md), [map PICO](rq-evidence-map.md) và các PDF gốc được dẫn tại từng đối chiếu. Đây là bản đồng bộ theo quyết định của nhóm, chưa xác nhận toàn bộ RBL-2 hoàn tất.

**Quyết định của nhóm:** giữ hướng nghiên cứu; tự xác định và đề xuất GAP-T từ đối chiếu 59 tài liệu; bổ sung bằng chứng thực nghiệm cho phép so EP+BVA–uniform random trên RESTestBench. Nhóm kế thừa benchmark, dataset và thước đo, không đề xuất thuật toán EP/BVA mới. Quyết định chọn đề tài không đồng nghĩa đã đáp ứng rubric gap mạnh hoặc đã được giảng viên chấp thuận cách xác lập gap này.

## 1. RQ (nguyên văn trên thẻ) + PICO

**RQ nhóm đã chốt:** Trên cùng tập yêu cầu REST API của RESTestBench, EP+BVA và sinh dữ liệu ngẫu nhiên đồng đều khác nhau thế nào về số mutant riêng biệt bị phát hiện theo từng dạng yêu cầu, dưới cùng ngân sách request?

**Trạng thái thẻ RQ:** câu trên là nội dung nhóm chốt cho tài liệu này; chưa xác minh bản thẻ đã được cập nhật nguyên văn.

| Yếu tố | Nội dung |
|---|---|
| **P** | Tập yêu cầu REST API được chọn từ RESTestBench. |
| **I** | Sinh dữ liệu bằng phân hoạch tương đương kết hợp phân tích giá trị biên (**EP+BVA**). |
| **C** | Sinh dữ liệu ngẫu nhiên đồng đều (**uniform random**), cùng ngân sách request. |
| **O** | Số mutant riêng biệt được oracle xác nhận là bị phát hiện, phân tích theo từng dạng yêu cầu. |

**Điều kiện dùng chung dự kiến:** cùng yêu cầu, schema, assertions nghiệp vụ và quy tắc tính budget cho hai chiến lược sinh dữ liệu. Chỉ tính một mutant bị phát hiện khi test pass bản gốc và fail mutant theo oracle benchmark. Miền uniform, B, precise/vague, cách phân loại yêu cầu và cách xử lý reset/retry/timeout còn cần xác định. Kế hoạch cũ có 10 lượt/kỹ thuật/yêu cầu; đây chưa phải thiết kế đã khóa hoặc kết quả thực nghiệm.

**Kế hoạch cỡ mẫu đang lưu:** **45 = 16 FastAPI + 15 NestJS RealWorld + 14 TodoApp**, từng thay cho phương án 15 yêu cầu/dịch vụ. Đây là kế hoạch cũ, chưa khóa snapshot/commit và requirement IDs; không coi là tập đã chọn. Paper GV-02 có **106 requirements/228 mutants** (Table 3/PDF6); không đồng nhất quy mô paper với mẫu dự kiến của nhóm. Chưa xác minh ngày báo giảng viên hoặc bản thẻ cập nhật P.

**Phần mở rộng protocol dự kiến:** GV-02 dùng một test cho mỗi requirement (§3.4/PDF5–6). Nếu nhóm sinh nhiều test rồi lấy hợp các mutant IDs bị phát hiện, phải đặc tả phép hợp theo từng requirement, kỹ thuật và lượt chạy; đó là phần mở rộng protocol so với paper. Mutant kills không đồng nhất với số bug thực tế. Runner/oracle chưa được kiểm bằng code và nhóm chưa chạy thực nghiệm.

## 2. Bằng chứng làm nền (N = 59 paper evidence)

### 2.1. Phạm vi đầu vào và 5 cổng P1–P5

| Phạm vi | Số bài | Cách sử dụng |
|---|---:|---|
| INCLUDE qua screening của các nguồn, sau khử trùng | **42** | Merge #1–#42; giữ số liệu và quyết định IC/EC theo [PRISMA](prisma-team.md). |
| Bài nền do leader bổ sung | **17** | GV-01–GV-17, merge #43–#59; đọc phần toàn văn liên quan và audit PICO, chưa mặc nhiên INCLUDE theo IC/EC. |
| Bộ evidence của merge/map | **59 = 42 + 17** | Theo đối chiếu DOI/arXiv và tên đã ghi trong merge: 0 bài trùng giữa hai tập. |
| Phản chứng bổ sung ngoài ma trận | Không cộng vào 59 | Guo 2024 và MioHint/R2R-02 được xét riêng ở §3. |

**Bước 1:** kế thừa xác nhận của người phụ trách rằng các thành viên đã kiểm các cổng trước gộp; lượt đồng bộ này kiểm lại nội dung ô và số hàng của bảng hiện có, không tái screening hoặc xác minh lại toàn bộ 42 PDF.

| Cổng | Trên tập screening 42 bài | Kiểm thêm bộ evidence 59 bài |
|---|---|---|
| P1 — ≥12 INCLUDE | **Đạt: 42 ≥12.** | 17 bài nền không được dùng thay số INCLUDE. Không phát sinh nhánh thiếu số lượng L1–L3. |
| P2 — ≥90% có Tool/LLM | **Đạt: 42/42 = 100%.** | 59/59 có mô tả tool/kỹ thuật; không đồng nghĩa tất cả dùng LLM. |
| P3 — ≥50% có kết quả số | **Đạt: 42/42 = 100% có số trong bảng.** | **58/59 có kết quả định lượng được ghi**; GV-17 chỉ mô tả định tính. Số trang, số hình hay số mục không phải kết quả số; tính nhất quán của từng kết quả vẫn theo cảnh báo nguồn. |
| P4 — ≥50% có hạn chế | **Đạt: 42/42 có dữ liệu hạn chế.** | 59/59 có nội dung hạn chế, nhưng phải tách AUTHOR_STATED khỏi REVIEWER_INFERRED; không suy mọi dòng đều nêu cùng gap. |
| P5 — metric cụ thể | **Đạt ở mức bảng: 42/42 ghi metric cụ thể.** | 58 bài có metric thực nghiệm được mô tả; GV-17 chưa có phép đo định lượng xác minh được. Không tuyên bố cả 59 bài vượt mọi tiêu chí screening. |

### 2.2. Tổng hợp PICO theo bộ 59

| Yếu tố | ✓ | ◐ | · | ? | Điều có thể kết luận |
|---|---:|---:|---:|---:|---|
| P | 1 | 28 | 29 | 1 | GV-02 dùng RESTestBench; P của GV-13 chưa xác minh deployment/source của SUT được thử. |
| I | 2 | 27 | 30 | 0 | TD-0002 và TD-0015 có EP/BVA; các ô gần không chứng minh intervention EP+BVA kết hợp. |
| C | 7 | 26 | 26 | 0 | 5 bài cũ và GV-07/GV-11 đạt rubric random cùng budget; hai bài mới dùng time budget ngoài REST. |
| O | 5 | 39 | 15 | 0 | TD-0002, GV-02/GV-06/GV-08/GV-10 có program-mutation metric; chưa đồng nhất suite-level unique kills theo dạng yêu cầu. |

**Phân bố số ✓:** **46 bài × 0/4, 11 bài × 1/4, 2 bài × 2/4**; hai bài cao nhất trong 59 là TD-0002 và GV-02. Tập 42 cũ giữ phân bố 35/6/1; 17 bài thêm đóng góp 11/5/1 tương ứng. **67/68 ô của 17 bài đã phân loại, 1 ô GV-13/P? còn mở**; không đổi `?` thành `·`, không cộng vào số chạm đã xác nhận.

**Quy ước:** ✓ là đạt [rubric rộng của map](rq-evidence-map.md#1-quy-tắc-chấm-chuẩn-hoá-toàn-nhóm), không bảo đảm khớp đầy đủ RQ. P✓ chưa xác nhận đúng tập requirement IDs nhóm sẽ chọn; I✓ chấp nhận EP và/hoặc BVA; C✓ chấp nhận cùng số test/lời gọi/thời gian; O✓ chấp nhận mutation score. Không ghép các yếu tố của nhiều paper để tạo một paper phản chứng.

Nguồn cá nhân: [Lâm](../lam/SLR/rq-check.md), [Khôi](../khoi/SLR/rq-check.md), [Tùng](../tung/SLR/rq-check.md), [T.Duy](../t.duy/SLR/rq-check.md), [K.Duy](../k.duy/SLR/rq-check.md). **Ba nguồn từng được dẫn nhưng hiện thiếu:** `rq-validation-audit.md`, `rq-validation-source-check.csv`, `gap-ban-dau.txt`. Không dùng các đường dẫn thiếu để khẳng định đã có sổ quote, đã đối soát đủ 42 dòng hoặc đã lưu gap trước đếm; đợt này không tạo lại chúng bằng nội dung suy đoán.

## 3. Phản chứng tổng hợp mọi nguồn

### 3.1. Nhãn tính mới và kết luận phản chứng

**Nhãn nhóm: `extension`**, giữ theo quyết định của nhóm đã ghi trong hồ sơ. Nhóm mở rộng đánh giá trên nền benchmark có sẵn; không lấy việc không có paper ≥3✓ trong 59 để tự đổi thành `new`. Nhãn đang giữ không chứng minh bảng căn hàng đã đạt rubric, cũng không xác nhận giảng viên đã chấp thuận cách xác lập gap.

- **Trong 59:** TD-0002 và GV-02 cùng đạt cao nhất 2/4 theo rubric. TD-0002 có EP/BVA trong prompt và mutation score nhưng thiếu C của RQ; GV-02 có P/O nền nhưng thử LLM generation/refinement, không EP+BVA–random.
- **Ngoài 59:** Guo 2024 vẫn là ứng viên gần nhất theo rubric rộng (**3/4: I/C/O**); MioHint được rà thêm nhưng chỉ chạm P/C, không đạt I/O.
- **Kết luận có giới hạn:** chưa xác minh paper khớp đủ toàn bộ P/I/C/O của RQ trong tài liệu đã đối chiếu. Không có bằng chứng từ đối chiếu này rằng EP+BVA tốt hơn random; không suy gap mạnh từ phân bố điểm.

Phần đã có nghiên cứu: benchmark yêu cầu/oracle, mutation metric, request generation gần miền/biên và đối chiếu có budget. Phần nhóm dự kiến bổ sung: **ước lượng chênh lệch unique mutant kills của hai cách sinh input cụ thể dưới cùng request budget, theo dạng yêu cầu**, giữ oracle/assertions chung. Đây là đóng góp đánh giá thực nghiệm dự kiến, không phải đề xuất một thuật toán EP/BVA mới hay tuyên bố mutation testing cho REST chưa tồn tại.

### 3.2. Rà 2–3 nghiên cứu mạnh trong 12 tháng gần nhất

**Cửa sổ:** 20/10/2025–20/10/2026; ưu tiên cùng bài toán/metric, rồi venue/quy mô, sau đó độ mới. Kế thừa lượt rà 18/10 được ghi trong [search-log của Tùng](../tung/SLR/search-log.md) và [bảng full-text](../tung/SLR/rq-check.md#22-đối-chiếu-picos-từ-bản-toàn-văn); kiểm có mục tiêu ngày 20/10 bằng PDF và nguồn chính thức. Ba bài dưới đây là lựa chọn trong phạm vi đã rà, không bảo đảm mạnh nhất toàn ngành.

| Paper và lý do chọn | P/I/C/O theo rubric | Hạn chế trực tiếp; phần RQ chưa được đánh giá |
|---|---|---|
| **GV-02/RESTestBench**, EASE 2026 AI Models/Data; [arXiv v1 28/04/2026](https://arxiv.org/abs/2604.25862), đúng benchmark/metric. [PDF](../Paper-source/44-GV-02-RESTestBench.pdf), §3–4/PDF3–8 | ✓ / · / · / ✓ — **2/4** | §6/PDF9: “Our benchmark includes only three services”; “Each experiment was executed only three times”. Đánh giá LLM single-step/refinement, chưa đánh giá phép so I/C của nhóm. |
| **MioHint**, [ICSE 2026 Research](https://conf.researchr.org/details/icse-2026/icse-2026-research-track/186/MioHint-LLM-Assisted-Request-Mutation-for-Whitebox-REST-API-Testing); bản conference 04/2026. [PDF](../tung/SLR/update-paper/R2R-02-MioHint-2026.pdf), §3–5/PDF5–10 | ◐ / · / ◐ / · — **0/4** | §5/PDF10: “fuzzers best at achieving coverage, may not be best at finding bugs”. Coverage và request-mutation hit rate không phải source-mutant kills; chưa đánh giá I/C/O của RQ. |
| **FDRRestTest/K100**, [ESEM, 05/10/2026](https://doi.org/10.4230/LIPIcs.ESEM.2026.20); sát black-box REST, có fixed-request comparison và nhiều baseline. [PDF](../Paper-source/32-K100.pdf), §4–6/PDF8–18 | ◐ / · / ◐ / ◐ — **0/4** | PDF17: “The benchmark excludes enterprise-level APIs”. Logical-oracle findings/FRE không phải source-mutant kills; equal-request comparison đã có, nhưng chưa phải EP+BVA–uniform random. |

GV-02 và K100 đã có trong 59, không cộng lại; MioHint ngoài ma trận. [Lịch sử arXiv MioHint](https://arxiv.org/abs/2504.05738) phân biệt v1 08/04/2025 ngoài cửa sổ với v4 05/03/2026 và bản conference trong cửa sổ. RESTOR/GV-04, AGORA+/GV-05 và DualMine/GV-13 cũng được xét ở §3.3; chủ yếu đánh giá oracle/constraint nên không thay thế ba đối chiếu trên. LlamaRestTest 06/2025 nằm ngoài cửa sổ. Các ứng viên chỉ từng nhắc trong nhật ký đang thiếu, như Req2REST-Guard/MASTOR, chưa được dùng làm căn cứ kết luận ở bản đồng bộ này.

**Log kiểm bổ sung 20/10/2026** (ghi tại đây để không sửa file cá nhân): tìm web với `"FDRRestTest" "2026"` → xác nhận nguồn xuất bản K100; `"REST API" "equivalence partitioning" "boundary value" "mutation" random` → chưa xác minh thêm paper đánh giá đúng phép so; `"REST API testing" "negative result" random boundary` → chưa xác minh kết quả âm trực tiếp. Kết quả ngoài bài toán hoặc chỉ hướng dẫn thực hành không dùng làm phản chứng. Đây là lượt dò có mục tiêu, không phải screening hệ thống mới và không thêm records vào PRISMA. Lượt kết quả âm cũ có tại [search-log T.Duy](../t.duy/SLR/search-log.md).

### 3.3. Đối chiếu đủ 17 bài nền mới với RQ

P/I/C/O dưới đây kế thừa kết quả kiểm chứng PDF đã ghi trong hồ sơ; hạn chế tác giả được tóm tắt từ cột AUTHOR_STATED của merge/nguồn Lâm, kèm locator. **Cột cuối là suy luận đối chiếu của nhóm**, không phải câu tác giả thừa nhận thiếu đúng RQ. Mã paper liên kết trực tiếp tới PDF gốc; lượt format này không tái audit các PDF.

| Paper | P/I/C/O | Đã nghiên cứu | Hạn chế tác giả và locator | Chưa đánh giá đúng điều kiện nào của RQ |
|---|---|---|---|---|
| [GV-01 · YAKUSU](../Paper-source/43-GV-01-YAKUSU.pdf) | ·/·/·/◐ | Dịch bug reports Android thành UI tests, tái hiện 37/62 issues (§5.2/PDF8–9). | Chỉ app mã mở, hạn chế khái quát (§5.3/PDF9–10). | Ngoài REST; không EP+BVA–random hay mutation metric. |
| [GV-02 · RESTestBench](../Paper-source/44-GV-02-RESTestBench.pdf) | ✓/·/·/✓ | 106 yêu cầu/228 mutations; mutation score cho LLM generation/refinement (§3–4/PDF3–8). | 3 dịch vụ, 3 lần chạy; mutants là proxy correctness (§6/PDF9). | Chưa so I/C; mẫu 45 và union unique kills theo dạng yêu cầu khác phép tổng hợp của paper. |
| [GV-03 · Prompt-Based](../Paper-source/45-GV-03-Prompt-Based-REST-API-Amplification.pdf) | ·/◐/·/· | Amplify tests với boundary/error cases; đo API coverage/effort (§4–5/PDF3–6). | Một microservice, post-processing thủ công; coverage không đo fault detection (§7/PDF7). | Gần I, nhưng không nhánh EP+BVA riêng, random cùng B hoặc mutant outcome. |
| [GV-04 · RESTOR](../Paper-source/46-GV-04-RESTOR.pdf) | ·/·/·/· | GRPO sinh assertions; đánh giá F1/assertion/adoption (§3–5/PDF4–17). | Một lần training/evaluation, dữ liệu ByteDance, Python-only (§4/PDF9; §7/PDF18–19). | KillRate là reward trên response variants; không outcome program mutants hay phép so input generators. |
| [GV-05 · AGORA+](../Paper-source/47-GV-05-AGORA-Plus.pdf) | ·/◐/·/◐ | Domain/type generators tạo corpus; suy oracle và đo response-error detection (§4/PDF17–28). | Input diversity, OAS thủ công, annotation bias và 25 operations (§6/PDF30–31). | I◐ không phải EP/BVA primary; response mutation không phải source-mutant kills; không random arm. |
| [GV-06 · METFORD](../Paper-source/48-GV-06-METFORD.pdf) | ·/·/·/✓ | Mutation schemata/traditional trên 6 app Android (Tables12–13/PDF16–17). | Flakiness, tập app/operators/JDK hạn chế (§4.2; §5 từ PDF18). | Có mutation metric ngoài REST; hai cách chạy cùng suite không phải hai generator của RQ. |
| [GV-07 · ArrayDiff](../Paper-source/49-GV-07-ArrayDiff.pdf) | ·/◐/✓/◐ | Sinh theo input requirements; differential testing và random baseline cùng time budget (§4/PDF13–19). | Có thể bỏ sót khi cả hai crash; ngưỡng số thực; 5 cặp frameworks (§5.2/PDF20). | Không REST, không uniform requests cùng B, không program-mutant metric. |
| [GV-08 · YATE](../Paper-source/50-GV-08-YATE.pdf) | ·/·/·/✓ | Repair LLM unit tests, đo mutation score trên Java (§4/PDF6–10). | Tool/model, Spoon và data leakage (§7/PDF10–11). | Không REST hay EP+BVA–random; không chuyển score thành expected kills của nhóm. |
| [GV-09 · SATORI](../Paper-source/51-GV-09-SATORI.pdf) | ·/·/·/◐ | Oracle từ OAS; response-mutation detection và bugs (§IV/PDF5–10). | OAS errors, annotation bias, phạm vi API/oracle (§V/PDF10). | Corpus tái dùng không thành input intervention; không program-mutant evaluation hoặc random generator arm. |
| [GV-10 · Meta/ACH](../Paper-source/52-GV-10-Mutation-Guided-Meta.pdf) | ·/·/·/✓ | Kotlin source mutants; tests pass original và kill mutant (Table8/PDF9). | Mutant relevance chưa đo ổn định; regression oracle không tìm existing faults (§8/PDF10). | Có nguyên tắc pass-original/kill-mutant, nhưng ngoài REST và không phép so I/C. |
| [GV-11 · Nüwa](../Paper-source/53-GV-11-Nuwa.pdf) | ·/◐/✓/◐ | MLIR generation/mutation; so random MLIRSmith cùng 24h (§IV–V/PDF7–9). | MLIR version, model/config (§VI-B/PDF10). | Mutate test inputs không phải mutate mã SUT; time budget không phải B HTTP requests. |
| [GV-12 · Beyond Flaky](../Paper-source/54-GV-12-Beyond-Flaky-Test.pdf) | ·/·/·/· | Chẩn đoán CI failures; thời gian điều tra (Methods/Results/PDF9–15). | Không giữ per-session logs, chưa ground-truth accuracy; baseline khoảng (PDF19–20). | TeamCity REST API là nguồn context, không REST SUT để so generator/mutants. |
| [GV-13 · DualMine](../Paper-source/55-GV-13-DualMine.pdf) | ?/◐/·/◐ | Khám phá constraints, targeted counterexamples; 48 deduplicated faults (§IV–V/PDF3–10). | Phụ thuộc prompts/specs/traces (§V-F/PDF10). | Chưa xác minh P; không random arm/source mutants. 39 là endpoints thuộc 7 services. |
| [GV-14 · Crowd Reports](../Paper-source/56-GV-14-Crowdsourced-Report-Assessment.pdf) | ·/·/·/· | Chấm reports bằng ICC/κ/correlation và thời gian (§V/PDF7–10). | Subjectivity, clustering bias, indicator weights (§V-C/PDF10). | Reports là đầu vào được đánh giá, không distinct faults do generator tìm ra. |
| [GV-15 · IoT UI Fuzzing](../Paper-source/57-GV-15-IoT-UI-Fuzzing.pdf) | ·/◐/◐/◐ | String extension; đo time-to-first crash trên lỗi gieo (§IV/PDF3–4). | Mới dùng string-extension mutation (§IV-C/PDF4–5). | Không REST; fuzz baseline không chứng minh uniform cùng budget; 3 lần đo crash không là unique kill count. |
| [GV-16 · How Far Flaky](../Paper-source/58-GV-16-How-Far-Flaky-Tests.pdf) | ·/·/·/· | Phân loại flaky tests và chẩn đoán cause từ CI (§III–IV/PDF4–9). | Dataset selection, cửa sổ log 90 ngày, mẫu CI nhỏ (§VI/PDF10–11). | RandomCV là data split, không random input comparator; F1 không là mutant outcome. |
| [GV-17 · Intelligent Test Automation](../Paper-source/59-GV-17-Intelligent-Test-Automation.pdf) | ·/·/·/· | Demo requirement → calculator/unittest (§3–4/PDF2–3; Appendix/PDF5–7). | Overhead, rõ nghĩa yêu cầu, scalability (§6/PDF4–5). | Không kết quả định lượng xác minh được, không REST/mutation/random-arm evaluation. |

**Tổng hợp theo vai trò:** GV-02 cung cấp hạ tầng P/O; GV-06/08/10 cho biết mutation đã được dùng ngoài bài toán này; GV-03/05/07/11/13/15 có kỹ thuật gần miền/biên; GV-07/11 có random comparator cùng thời gian. GV-04/09 tập trung oracle, GV-12/14/16 nghiên cứu diagnosis/report quality, GV-01/17 ngoài thiết kế REST của nhóm. Vì vậy, điểm thiếu còn xét là **tổ hợp phép so cụ thể**, không phải thiếu từng thành phần nói chung. Chưa xác nhận limitation tác giả nào trong 17 nêu đầy đủ đúng gap đó.

### 3.4. Paper gần nhất và bảng căn hàng

**Guo, Okamura & Dohi (2024), [Optimal test case generation for boundary value analysis](https://link.springer.com/article/10.1007/s11219-023-09659-9): 3/4 theo rubric rộng, P·/I✓/C✓/O✓.** Ngoài 59 và cửa sổ mới; giữ làm ứng viên phương pháp gần nhất.

| Yếu tố | Guo 2024 | RQ nhóm | Khác ở đâu, căn cứ |
|---|---|---|---|
| P | 5 chương trình non-REST (§5.4) | Tập yêu cầu REST API được chọn từ RESTestBench | Khác P; mẫu 45 chỉ là kế hoạch cũ chưa khóa. |
| I | Tối ưu BCD từ biên phân tích mã (§5.4–5.5) | EP+BVA từ yêu cầu/schema | Khác cách xây biên. |
| C | Random theo phân hoạch, cùng cỡ test (§5.2/5.5) | Uniform random cùng request budget | Không đồng nhất baseline. |
| O | Kill rate theo khác biệt đường thực thi (§5.1) | Unique kills theo oracle và dạng yêu cầu | Khác oracle/tổng hợp. |

§6 nêu “reliance on manual analysis for boundary point identification” và khó định nghĩa biên phi số. RQ chưa chứng minh khắc phục tự động hóa đó. **Bảng còn mở:** khác nhiều yếu tố; chưa đủ bằng chứng GAP-T hoặc lý do đổi theo để đạt quy tắc căn hàng. Không ghi “=” giả tạo hay đổi nhãn đã xác nhận chỉ theo số ✓.

**Neo benchmark riêng:** GV-02/RESTestBench là nguồn kế thừa P và nguyên tắc oracle/mutant, không được chọn thay paper gần nhất chỉ để tăng mức giống. Phép so I/C và tổng hợp O của nhóm vẫn cần đặc tả; đổi sang cùng benchmark không tự chứng minh đóng góp chỉ khác một yếu tố. Bằng chứng trực tiếp của paper về 3 dịch vụ/3 repetitions hỗ trợ ghi giới hạn thiết kế, không chứng minh thiếu EP+BVA–random là limitation tác giả đã nêu.

## 4. Khả thi của từng gap đang cân nhắc (Bước 3)

Chỉ đánh giá **A — GAP-T do nhóm đề xuất + RQ đang giữ**. GAP-M/GAP-D ở §5 là bằng chứng tham khảo và giới hạn, không phải các RQ thay thế đang cân nhắc. Các số dưới đây là nguồn sẵn có hoặc kế hoạch cũ để dự toán, **không phải kết quả pilot**; không lấy runtime của paper làm runtime của nhóm.

| Tiêu chí | A — GAP-T: số liệu/căn cứ hiện có | Chấm | Việc cần xử lý |
|---|---|---|---|
| Dataset | Nguồn public; kế hoạch cũ **45=16+15+14**. Hồ sơ trước ghi README 103, paper GV-02/Table3/PDF6 ghi **106 yêu cầu/228 mutants**; chưa khóa snapshot/45 ID/mutant. | ⚠️ | Chốt commit, kiểm kê đúng phiên bản, tiêu chí hợp lệ, ID/seed và dạng yêu cầu; không sửa số paper thành số mẫu. |
| API/Tool | Dự kiến **0 lời gọi API LLM trả phí**, **3 dịch vụ cục bộ**; cần Docker, Python và Git. | ⚠️ | Xác nhận môi trường máy nhóm và chạy golden tests trên cả 3 dịch vụ. |
| Tính toán | **900 lượt kỹ thuật–yêu cầu/1 điều kiện**; chưa có số đo CPU/RAM/runtime trên máy nhóm. | ⚠️ | Ghi cấu hình máy, pilot đo tài nguyên; ưu tiên chạy tuần tự trước khi ước lượng toàn bộ. |
| Ground truth | Có golden tests và mutant/oracle; dự kiến **0 giờ gán nhãn ground truth mới**. | ✅ về nguồn sẵn có | Kiểm oracle, assertions dùng chung và định danh mutant. |
| Code base | **1 framework upstream**, **2 generator cần tích hợp**; chưa có bằng chứng generator nhóm chạy đúng. | ⚠️ | Kiểm sinh input, budget, pass-valid/fail-mutant và chính sách lỗi chạy. |
| Kỹ năng | **5 thành viên**; chưa có log xác nhận tích hợp được hai generator hoặc dự toán giờ công. | ⚠️ | Chốt người phụ trách/từng đầu việc; pilot dự kiến **5 yêu cầu trên đủ 3 dịch vụ**, chưa phải mẫu pilot đã khóa. |
| Thời gian | **45×2×10=900 lượt**; chưa chốt B, runtime và hạn triển khai cụ thể. | ⚠️ | Dự toán từ pilot; bố trí **≥3 ngày dự phòng** hoặc đề xuất downscope. |

**Đếm A: 0 ❌ / 6 ⚠️ / 1 ✅ → rủi ro cao.** Một ✅ chỉ xác nhận có nguồn ground truth để kế thừa, chưa xác nhận oracle chạy đúng trên máy nhóm. Chưa có ❌ được xác định không đồng nghĩa đủ bằng chứng khả thi. Không thêm cột B hoặc RQ mới để đáp ứng hình thức.

**Kế hoạch xử lý có đầu ra kiểm được:** (1) danh sách requirement IDs của tập được chọn, commit và mutant manifest — nếu giữ kế hoạch cũ thì khóa đúng 45 ID; (2) đặc tả hai generator, miền uniform hữu hạn/phân phối trên từng kiểu, B và cách tính requests phụ; (3) log golden tests/assertions dùng chung, pass-original/fail-mutant, reset/retry/timeout/flakiness; (4) pilot đo thời gian, RAM và lỗi chạy; (5) dự toán giờ máy/giờ người, hạn hoàn thành và ≥3 ngày dự phòng. Người phụ trách và ngày chốt từng đầu ra chưa được phân công trong lượt sửa tài liệu này.

Trước hết cân nhắc một điều kiện precise hoặc vague với cùng thông tin cho hai kỹ thuật; chưa tự khóa lựa chọn. Nếu pilot cho thấy vượt nguồn lực, trình phương án giảm mẫu/số lượt hoặc thu hẹp dạng yêu cầu cho GV, kèm hệ quả phương pháp; chưa áp dụng downscope.

**Cơ sở phép tính có điều kiện:** nếu giữ kế hoạch cũ 45 yêu cầu và 10 lượt, 45×2×10 = 900 lượt kỹ thuật–yêu cầu cho một điều kiện. Nếu B là tổng requests sinh mỗi lượt, có 900B requests trước replay; nếu chạy cả precise và vague, số lượt tăng gấp đôi. Replay trên mutant, setup/reset/retry tính riêng. B, số mutant áp dụng cho từng requirement và runtime đều chưa khóa nên chưa tính tổng HTTP executions hoặc giờ chạy. Nguồn artifact: [README benchmark](https://github.com/casablancahotelsoftware/RESTestBench#setup), [evaluator](https://github.com/casablancahotelsoftware/RESTestBench/blob/master/src/evaluator.py); URL sẵn có không phải bằng chứng đã chạy thành công.

## 5. Gap mà RQ lấp (kết quả Bước 2)

**Gap nhóm chọn: GAP-T — đánh giá so sánh kỹ thuật sinh dữ liệu kiểm thử.** Nhóm tự xác định gap qua đối chiếu 59 tài liệu; mức đáp ứng rubric được trình bày riêng với quyết định giữ đề tài.

### 5.1. Gap RQ ban đầu và kết quả đối chiếu

**Câu giả định lịch sử — giữ để truy vết, không dùng làm kết luận hiện hành:** câu dưới đây đã có trong hồ sơ trước đợt format này; chưa có bản ghi gốc chứng minh đã lưu trước khi tổng hợp và đếm:

> Chưa có nghiên cứu nào so sánh trực tiếp EP+BVA với sinh dữ liệu ngẫu nhiên đồng đều dưới cùng ngân sách request trong kiểm thử REST API dựa trên yêu cầu.

**Ghi nhận trong hồ sơ ngày 20/10/2026, sau tổng hợp paper**, không phải bản ghi đã có trước khi đếm. Nhóm giữ nguyên câu lịch sử để truy vết, thay kết luận hiện hành bằng phát biểu giới hạn trong corpus tại §5.3. Chưa có bằng chứng giảng viên chấp thuận cách xác lập gap này; không ghi ngày chấp thuận hoặc sửa lịch sử hồi tố.

**Đối chiếu theo bốn trường hợp của mẫu:** hiện phù hợp trạng thái **“chưa có paper nêu, là giả định của nhóm”**, vì chưa có tập limitation trực tiếp khớp đầy đủ gap để điền bảng đếm. Đây là trạng thái căn cứ hiện có, không phải kết quả một phép đếm bằng 0 trên 59 bài. Nhóm đề xuất gap từ đối chiếu thiết kế, không kế thừa một limitation được tác giả phát biểu trực tiếp. Vì vậy chưa xếp gap này là mạnh hoặc yếu theo số paper cùng nêu.

### 5.2. Bảng hạn chế, kiểm đã giải quyết và độ mạnh

**Không đổi cơ học mẫu số limitation từ 42 thành 59.** Cột hạn chế hiện có dữ liệu ở 59 dòng, nhưng chưa có sổ đếm chung đã chuẩn hóa, gạch phần được giải quyết và gộp tác giả cho toàn bộ 59. Thống kê **18/42, 10 cụm** của GAP-D là kết quả kế thừa bản tổng hợp trước; sổ quote `rq-validation-audit.md` hiện thiếu nên lượt này không xác nhận lại tử số hoặc cách gộp cụm đó. Hai đối chiếu trực tiếp được mở lại từ PDF là P12 và GV-03; giữ mẫu số/phạm vi riêng.

| Hạn chế | Paper nêu | Paper đã giải quyết | Còn lại | Mạnh/yếu | Loại |
|---|---|---|---|---|---|
| Thiếu đánh giá phép so EP+BVA–uniform random trên cùng yêu cầu RESTestBench, cùng request budget, theo số mutant riêng biệt ở từng dạng yêu cầu | Nhóm xác định qua đối chiếu 59 tài liệu; chưa có tập quote + locator của tác giả cùng nêu đầy đủ limitation này | Trong 59 tài liệu đã đối chiếu, chưa tìm thấy nghiên cứu thực hiện đầy đủ phép so; không gán nhận định này cho GV-02 | Chưa có tử số x về limitation trực tiếp; không suy từ các ô PICO thiếu | **Gap do nhóm đề xuất**; chưa xếp mạnh/yếu theo đếm | GAP-T |
| Giới hạn số lượng/phạm vi dịch vụ làm hạn chế khái quát | **18/42 paper, 10 cụm — số kế thừa, chưa xác minh lại sổ quote**; danh sách giữ dưới bảng | K191 có công nghiệp nhưng vẫn một tổ chức; GV-02/03/04 cũng có giới hạn phạm vi riêng. Không gạch hạn chế của một phương pháp chỉ vì phương pháp khác có nhiều dịch vụ | Chưa có tử số đã kiểm lại cho 59; không đổi thành 18/59 | Chủ đề lặp lại trong bản cũ; chưa chứng minh một gap cụ thể mà RQ này lấp | GAP-D |
| Chưa đánh giá mutation cho phép so 10 công cụ của P12 | **P12/K81/K55**, [PDF11/§6](../Paper-source/03-P12-K81-K55.pdf): “using mutation to further evaluate the tools’ fault-detection ability” | GV-02 đánh giá LLM, chưa chứng minh đánh giá lại đúng 10 công cụ của P12 với mutation | **1/42 paper được xác nhận trực tiếp ở dòng này**; không phải đếm mới toàn bộ 42 | Yếu trong phạm vi căn cứ đang giữ | GAP-M |
| Coverage chưa đo trực tiếp fault detection của LLM-amplified tests | **GV-03**, [PDF7/§7.3](../Paper-source/45-GV-03-Prompt-Based-REST-API-Amplification.pdf): “it does not directly measure fault detection or overall test adequacy” | GV-02/TD-0002 có mutation trong thiết kế khác; chưa xác minh đánh giá fault adequacy của đúng suite amplification này | **1/17 bài nền** được xác nhận cho phát biểu cụ thể này; không gộp tự động với dòng P12 | Yếu; hỗ trợ chọn outcome, không chứng minh thiếu phép so I/C | GAP-M |
| ~~Chưa có mutation testing cho REST API nói chung~~ | Khái quát hóa của người tổng hợp, không phải limitation chung đã xác nhận | **GV-02** đã có requirements-based mutation; **TD-0002** đã có mutation score | Bỏ mệnh đề khái quát; giữ câu hỏi về phép so cụ thể | Bị phản chứng | GAP-M |
| ~~Chưa có so sánh REST testing cùng request budget~~ | Khái quát hóa quá rộng | K52/P53, K90 và K100 đã có đối chiếu cùng số requests trong thiết kế của chúng | Không dùng equal-request budget đơn lẻ làm novelty | Bị phản chứng ở mức khái quát; vẫn phải kiểm đúng I/C | GAP-T |

**Danh sách GAP-D kế thừa:** K46/K76/K166; P12/P17/K32/K167/K168/K191; K66/K101; K37; K89; K93; TD-0015; K02; TD-0002; K100. Muốn dùng số 18/42 và 10 cụm trong proposal phải khôi phục/kiểm lại quote, locator và quan hệ tác giả; dữ liệu cột hạn chế đơn thuần chưa chứng minh cách gộp cụm.

K49 (§4.5.1/PDF17) bàn thiếu mutation tool cấp system tại thời điểm bài viết, không cộng với P12 như cùng một hạn chế. MioHint cảnh báo coverage không bảo đảm bug finding nhưng chưa nêu thiếu đúng mutation evaluation của P12/GV-03; không dùng ba chủ đề gần nhau để tự kết luận gap mạnh. Tương tự, số requests/endpoints/người tham gia không thay được số dịch vụ. **RQ vẫn dùng 3 dịch vụ, không nhận là lấp GAP-D.**

### 5.3. Đối chiếu gap và RQ theo mẫu

**Gap A — GAP-T, phát biểu nhóm đã chốt:**

> Trong 59 tài liệu đã đối chiếu, nhóm chưa tìm thấy nghiên cứu so sánh trực tiếp EP+BVA với sinh dữ liệu ngẫu nhiên đồng đều trên cùng các yêu cầu REST API của RESTestBench, với cùng ngân sách request, về số mutant riêng biệt bị phát hiện theo từng dạng yêu cầu.

**RQ lấp gap A:**

> Trên cùng tập yêu cầu REST API của RESTestBench, EP+BVA và sinh dữ liệu ngẫu nhiên đồng đều khác nhau thế nào về số mutant riêng biệt bị phát hiện theo từng dạng yêu cầu, dưới cùng ngân sách request?

**So với hướng RQ ban đầu:** giữ phép so I/C và outcome; chuẩn hóa câu chữ P thành tập yêu cầu được chọn, không coi kế hoạch 45 yêu cầu là mẫu đã khóa. Cỡ mẫu và snapshot còn phải chốt trước thực nghiệm. Đây là hai chiến lược sinh dữ liệu kiểm thử, không phải hai phương pháp đo thủ công.

**Bài báo nền và phần kế thừa:** [GV-02/RESTestBench](../Paper-source/44-GV-02-RESTestBench.pdf), §3–4/PDF3–8, cung cấp benchmark, requirements và mutants gắn với yêu cầu; thực nghiệm minh họa đánh giá sinh test bằng LLM theo single-step và refinement. Nhóm kế thừa nền tảng đó để mở rộng đánh giá sang EP+BVA và uniform random. Đây là vai trò bài nền, phân biệt với đối chiếu paper gần nhất theo rubric rộng ở §3.4.

**Đóng góp dự kiến:** bổ sung bằng chứng thực nghiệm về chênh lệch số mutant riêng biệt được phát hiện theo dạng yêu cầu dưới cùng request budget; không đề xuất thuật toán EP/BVA mới. Dataset, benchmark và thước đo là phần kế thừa; GAP-D và GAP-M không phải đóng góp chính. Các limitation P12/GV-03 ở §5.2 hỗ trợ lựa chọn outcome, không chứng minh đúng phép so I/C còn thiếu hoặc thay thế gap đã chọn.

**Cơ sở lựa chọn:**

1. Trong 59 tài liệu đã đối chiếu, chưa tìm thấy phép so đáp ứng đầy đủ thiết lập nêu trong phát biểu gap.
2. Phép so phù hợp mục tiêu đánh giá khả năng phát hiện mutant gắn với yêu cầu.
3. EP+BVA có thể cho kết quả tốt hơn, tương đương hoặc kém hơn uniform random; nhóm không giả định trước hướng kết quả. Kết luận tương đương, nếu có, cần thiết kế phân tích phù hợp, không suy từ việc chưa thấy khác biệt.
4. Có benchmark để kế thừa, giảm công sức xây dựng nền tảng từ đầu; khả thi thực tế chưa được pilot xác nhận.

**Mức đáp ứng rubric:** số 59 là quy mô corpus đối chiếu, không phải một phép đếm x/N tác giả cùng nêu limitation. Nhóm chưa có tập bằng chứng gồm x/N, tên paper, quote và locator cho đúng gap này; không bịa x hoặc gán cho GV-02 lời thừa nhận thiếu phép so EP+BVA–uniform random. Phát biểu trên chưa đáp ứng đầy đủ mẫu gap mạnh của giảng viên và chưa có bằng chứng được giảng viên chấp thuận. Quyết định giữ đề tài được ghi riêng với giới hạn này; không suy tính mới toàn lĩnh vực hoặc tự mở lại vòng chọn RQ.

### 5.4. Vì sao gap còn trống

**GAP-T:** nguyên nhân chưa được xác nhận. RESTestBench mới công bố năm 2026 cung cấp hạ tầng phù hợp, nhưng chưa chứng minh tính mới của dữ liệu là nguyên nhân thiếu phép so. Chi phí thiết lập miền input, oracle và replay là vấn đề phải đo trong pilot, chưa có số liệu nhóm để kết luận gap trống vì quá khó/tốn kém.

Đã xem các nguồn chạm ≥2 yếu tố, gồm TD-0002, GV-02/05/07/11/13/15 và các đối chiếu ngoài tập. GV-02 (§5/PDF8–9) có trường hợp refinement/tiếp xúc SUT lỗi làm giảm mutation score; đây là kết quả bất lợi cho một thiết kế LLM, **không phải kết quả EP+BVA–random**. Lượt dò kết quả âm của T.Duy ngày 18/10 và lượt 20/10 ghi ở §3.2 chưa xác minh kết quả âm trực tiếp cho đúng phép so. Chỉ kết luận **“chưa thấy trong phạm vi tài liệu đã tìm”**; nếu thực nghiệm nhóm không thấy khác biệt, đó vẫn là kết quả hợp lệ.

Nghiên cứu này mở rộng đánh giá hai chiến lược sinh dữ liệu; chưa chứng minh khắc phục hiện tượng LLM thích nghi với SUT lỗi.

**GAP-M tham khảo:** P12/GV-03 nêu hướng đánh giá tiếp, chưa xác nhận nguyên nhân chưa thực hiện; nhận định thiếu tool của K49 chỉ là bối cảnh. **GAP-D:** một số nguồn nêu chi phí, quota và khó triển khai; không suy mọi paper có cùng nguyên nhân hoặc RQ ba dịch vụ giải quyết được chúng.

### 5.5. Lợi ích của cặp GAP-T + RQ hiện tại

Nhóm muốn biết chênh lệch khả năng phát hiện mutant giữa EP+BVA và uniform random dưới cùng budget để giúp kỹ sư kiểm thử lựa chọn cách sinh input theo dạng yêu cầu; hiện chưa có kết quả đối chiếu phù hợp trong phạm vi tài liệu đã kiểm. Nếu EP+BVA có lợi thế thực tiễn thì cân nhắc ưu tiên EP+BVA; nếu random có lợi thế thì cân nhắc random; nếu chưa đủ bằng chứng khác biệt thì báo cáo bất định, không kết luận hai kỹ thuật tương đương. Lợi ích giới hạn trong mẫu, oracle và ngân sách đã đánh giá.

## 6. Quyết định: giữ RQ / đổi I hoặc C

**Quyết định hiện hành của nhóm: giữ hướng RQ tại §1 và nhãn `extension`.** Gap nhóm chọn là **GAP-T — đánh giá so sánh kỹ thuật sinh dữ liệu kiểm thử**, do nhóm xác định qua đối chiếu 59 tài liệu; đóng góp dự kiến là bằng chứng thực nghiệm. GAP-M/GAP-D chỉ hỗ trợ bàn luận hoặc ghi giới hạn, không phải phương án thay thế đang cân nhắc. Không đổi H0/H1 trong lượt này. Quyết định này không được ghi thành chấp thuận của giảng viên.

**Trạng thái P:** **45 = 16 FastAPI + 15 NestJS RealWorld + 14 TodoApp** là kế hoạch cũ chưa khóa snapshot/IDs; **chưa xác nhận ngày báo GV**. Chênh lệch README 103/paper 106 cần được xử lý bằng phiên bản benchmark và kiểm kê mẫu thực tế; 228 mutants của paper không phải số mutant đã chọn cho nhóm.

**Trạng thái:** đã đồng bộ phạm vi **42 screening + 17 nền = 59 evidence**; Bước 1 giữ kết quả trên tập screening và nêu rõ giới hạn bộ bổ sung. Bước 2 có đối chiếu 17 bài, phản chứng ngoài tập, gap nhóm đề xuất và lợi ích; chưa đủ căn cứ gọi GAP-T là gap mạnh hoặc đóng bảng căn hàng. Bước 3 giữ mức rủi ro cao với kế hoạch xử lý, chưa có pilot/số đo nhóm. **Hoàn tất đồng bộ tài liệu không đồng nghĩa hoàn tất toàn bộ RBL-2**; cũng không đòi chạy toàn bộ thực nghiệm mới được hoàn tất RBL-2.

**Đối chiếu checklist cuối hướng dẫn:**

| Hạng mục của mẫu RBL-2 | Trạng thái và giới hạn |
|---|---|
| Mỗi người có bảng P/I/C/O và hạn chế | Có 5 file cá nhân liên kết ở §2; 17 bài mới có audit riêng. Chưa tái xác minh mọi quote/locator của 42 bài cũ. |
| Gap ban đầu ghi trước đếm và có kết quả đối chiếu | **Chưa đạt trình tự lịch sử**; §5.1 giữ nguyên câu và ghi thời điểm bổ sung muộn, không hồi tố. Hướng xử lý hiện tại giữ RQ đã được người phụ trách làm rõ. |
| Bảng gap, gạch phần đã giải quyết, phân loại gap mạnh | §5.2 có bảng và gạch các mệnh đề quá rộng; chưa xác nhận gap mạnh khớp RQ hoặc phép đếm chung 59. |
| Nếu N<12: L1/L2/L3 | **Không áp dụng:** 42 INCLUDE ≥12, không dùng 17 bài nền để vượt cổng. |
| Nhãn tính mới có lý do, so nhãn thẻ | Giữ `extension` theo xác nhận người phụ trách; lý do/giới hạn ở §3.1. Chưa kiểm trực tiếp bản thẻ sau cập nhật P. |
| Paper gần nhất và căn hàng có bằng chứng/lý do đổi theo | Có Guo và bảng §3.4; **còn mở** vì mức khớp rộng không tạo bảng chỉ đổi một yếu tố của RQ đầy đủ. |
| So 2–3 nghiên cứu mạnh 12 tháng gần đây | Có 3 đối chiếu và lý do chọn ở §3.2, log nguồn/truy vấn; không nhận là tìm kiếm bao phủ toàn ngành. |
| Khả thi có số nhóm cho từng cặp đang cân nhắc | A có 0 ❌ / 6 ⚠️ / 1 ✅ và kế hoạch; **chưa chốt** B, máy, giờ công, runtime, hạn hoàn thành/dự phòng từ số đo. |
| Phát biểu mỗi gap mạnh đúng mẫu, có nguyên nhân | GAP-T do nhóm đề xuất, chưa có x/N limitation trực tiếp và chưa đạt đầy đủ mẫu gap mạnh; các GAP-M yếu và GAP-D tham khảo không được ghi thành gap mạnh đã chọn. Nguyên nhân còn chưa xác nhận (§5.4). |
| Câu lợi ích, kể cả không bác bỏ H0 | Có §5.5, nêu người dùng và các hướng kết quả; không suy không khác biệt thành tương đương. |
| Mỗi gap mạnh đang cân nhắc có RQ đủ PICO, O số | Chỉ giữ cặp A với RQ §1; không có gap mạnh khác đang chọn để lập RQ nháp. Thiết kế vận hành còn cần khóa. |
| Mọi thay đổi RQ báo GV trước khóa | **Chưa xác minh ngày/bản thẻ cập nhật P**; không bịa ngày hoặc coi xác nhận nhãn là xác nhận mọi thông số. |

**Việc tiếp theo:** nhóm hoàn thiện biện minh GAP-T/bảng căn hàng theo hướng giữ RQ; xác nhận cập nhật thẻ P, cách xác lập gap và cách ghi lệch trình tự với GV; khóa dữ liệu, B/miền random, assertions/oracle, mutant manifest, dạng yêu cầu và phần mở rộng protocol nếu dùng nhiều test; chốt máy/nhân lực/thời gian, kiểm hai generator rồi pilot. Kế hoạch phân tích thống kê hoàn thiện trước chạy chính. Trạng thái và các giới hạn đang mở được tổng hợp ngay trong mục này.
