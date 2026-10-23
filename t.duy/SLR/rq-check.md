# Kiểm chứng RQ — phần của T.Duy

## Hiện hành — cập nhật 22/10/2026

**RQ chính:** Trong điều kiện sinh single-step với cùng mô hình, cấu hình và ngân sách kiểm thử được quy định trước, việc bổ sung hướng dẫn EP+BVA vào prompt gốc ảnh hưởng như thế nào đến MS_φ trên các yêu cầu vague của RESTestBench tại phiên bản đóng băng?

**PICO:** P = 106 vague/228 mutant, commit `4decc1e36ea3dd41b64ce3e3ac6a85bc72df36ae`; I = prompt C + EP+BVA có căn cứ; C = single-step gốc; O = MS_φ. Model được chọn: DeepSeek-V4.1-Flash-1017, DeepSeek API chính thức; ngân sách tổng 3 USD.

Đối chiếu nghiên cứu gần nhất, gồm GV-18/Rodríguez, ở [rq-validation §2](../../team-synthesis/rq-validation.md#2-bằng-chứng-và-nghiên-cứu-gần-nhất); thiết kế ở [experiment-design](../../team-synthesis/experiment-design.md). Bản cập nhật hiện hành không phải tái chấm paper của cá nhân; các dấu P/I/C/O bên dưới giữ nguyên bằng chứng/phiên bản cũ. Không dùng tổng điểm cũ để kết luận RQ mới có tính mới.

## Hồ sơ đối chiếu trước 22/10/2026 — lịch sử hướng cũ

Các RQ 45 requirement, EP+BVA truyền thống so random, số lần chạy và kết luận phía dưới là hồ sơ trước đổi hướng, không phải điều kiện thực nghiệm hiện hành. Chưa chạy lại screening hoặc thực nghiệm trong lượt đồng bộ này.


**Nguồn phụ trách:** Semantic Scholar + Google Scholar (bài #39 TD-0002, #40 TD-0015 trong bảng gộp)  
**Phân công đọc tập gộp Bước 2:** bài **#31–#38** (K93, K100, K127, K136, K166, K168, K191, K192) theo số hàng của `team-synthesis/evidence-table-merged.md`  
**Ngày thực hiện / cập nhật:** 2026-10-18 (rà soát & chuẩn hóa form 19/10/2026)

**RQ của nhóm (FA26-EXT-12):**
> Trên 45 yêu cầu của RESTestBench, phân hoạch tương đương kết hợp phân tích giá trị biên, so với sinh dữ liệu ngẫu nhiên đồng đều cùng ngân sách, khác nhau thế nào về số mutant riêng biệt bị phát hiện theo từng dạng yêu cầu?

**PICO:**
- **P (Population):** 45 yêu cầu chức năng của RESTestBench (15 yêu cầu / dịch vụ trên 3 dịch vụ REST API chạy Docker).
- **I (Intervention):** Phân hoạch tương đương kết hợp phân tích giá trị biên (EP + BVA) trên miền tham số request, không dùng AI.
- **C (Comparison):** Sinh dữ liệu ngẫu nhiên đồng đều (uniform random), cùng ngân sách request, cùng seed cố định và lặp lại ≥ 10 lần.
- **O (Outcome):** Số mutant riêng biệt (unique mutants) bị phát hiện theo từng dạng yêu cầu, được xác nhận bởi oracle của RESTestBench (pass bản gốc, fail bản mutant).

---

## Mục 1 · Bảng đối chiếu paper với RQ (P/I/C/O + hạn chế cụ thể)

Theo rubric `team-synthesis/rq-evidence-map.md` §1:
- **✓ (Khớp):** Khớp đúng tiêu chí của RQ.
- **◐ (Gần):** Liên quan một phần (P: REST API mở/chạy được; I: ràng buộc/miền giá trị; C: fuzzing/random chưa khớp budget; O: bug/5XX/coverage).
- **— (Không):** Khác hoặc không có.
- **Ngưỡng phản chứng:** Paper đạt ≥ 3 ô ✓ (chạm 3/4 hoặc 4/4).

### 1.1 Bảng đối chiếu P/I/C/O (8 bài phân công #31–#38 và 2 bài nguồn cá nhân #39–#40)

| # | Mã | Paper (Tác giả, năm, venue, DOI) | P | I | C | O | Số ✓ | Hạn chế paper nêu (tóm tắt) |
|---|---|---|---|---|---|---|---|---|
| 31 | K93 | **DynER** — Dynamic Error-Feedback REST API Testing (Electronics 2024), [DOI](https://doi.org/10.3390/electronics13173476) | ◐ | — | ◐ | ◐ | 0/4 | Số lượng dịch vụ thử nghiệm ít (chỉ 2 dịch vụ: WordPress, GitLab); khả năng khái quát bị giới hạn |
| 32 | K100 | **FDRRestTest** — Feedback-Driven Logical Testing for REST APIs (ESEM 2026), [DOI](https://doi.org/10.4230/LIPIcs.ESEM.2026.20) | ◐ | — | ◐ | ◐ | 0/4 | Benchmark loại trừ các API cấp doanh nghiệp; oracle logic có thể có false positives khi đánh giá |
| 33 | K127 | **Basis Path Testing on E-OBE Application** (bit-Tech 2026), [DOI](https://doi.org/10.32877/bt.v9i1.4098) | — | — | — | ◐ | 0/4 | Không đạt được độ đa dạng lỗi mới; lặp trạng thái; chỉ thử trên 1 ứng dụng nội bộ nhỏ |
| 34 | K136 | **SBFT Tool Competition 2026: REST League** (SBFT 2026), [DOI](https://doi.org/10.1145/3786155.3795704) | ◐ | — | ◐ | ◐ | 0/4 | Branch coverage của các công cụ còn rất thấp (không vượt quá 23%); khó chạm tới logic nghiệp vụ sâu |
| 35 | K166 | **Deep Learning-Based Prediction of Test Input Validity** (DeepTest 2021), [DOI](https://doi.org/10.1109/DeepTest52559.2021.00008) | — | ◐ | — | — | 0/4 | Chỉ kiểm chứng trên 5 API thương mại nhỏ; rủi ro gán nhãn dữ liệu và độ đa dạng input không hợp lệ |
| 36 | K168 | **Automated Black-Box Testing of Mass Assignment Vulnerabilities** (ICSE 2023), [DOI](https://doi.org/10.1109/ICSE48619.2023.00213) | ◐ | — | — | ◐ | 0/4 | Chỉ đánh giá trên 5 dự án mã mở; ground truth lỗi cấy thủ công; chưa kiểm chứng trên hệ thống công nghiệp |
| 37 | K191 | **Automated REST API Black-box Test Generation in Practice** (ICST 2026), [DOI](https://doi.org/10.1109/ICST69053.2026.00064) | — | — | ◐ | ◐ | 0/4 | Kết quả trong 1 doanh nghiệp (SES) có thể không khái quát sang domain khác; không phân tích false negatives |
| 38 | K192 | **RESTing-LLAMA: Large Language Model based REST API Fuzzing** (ASIA CCS 2026), [DOI](https://doi.org/10.1145/3779208.3785383) | ◐ | — | ◐ | ◐ | 0/4 | Đặc tả API vượt quá giới hạn token ngữ cảnh của LLM; phát hiện lỗi phụ thuộc xác thực thủ công |
| 39 | TD-0002 | **RestTSLLM: Combining TSL and LLM to Automate REST API Testing** (SBES 2025), [DOI](https://doi.org/10.5753/sbes.2025.9670) | ◐ | **✓** | — | **✓** | **2/4** | Chỉ 6 dự án .NET; temperature=1 và prompt bias; đánh giá thủ công; mutation score chưa tách unique mutants |
| 40 | TD-0015 | **Orchestration Architecture of AI Agents for Automated API Testing** (Tech. Audit 2026), [DOI](https://doi.org/10.15587/2706-5448.2026.360928) | ◐ | **✓** | — | — | **1/4** | Chỉ 1 dịch vụ FastAPI nhỏ (5 endpoints); 1 model GPT-4; outcome chỉ đo coverage yêu cầu, không đo mutant |

*Ghi chú:* Ô ◐ lấy từ cột "Gần RQ" của bảng gộp `team-synthesis/evidence-table-merged.md`. Cả 8 bài phân công (#31–#38) đều đạt 0/4 ✓ (chỉ chạm 1–3/4 ◐). Hai bài nguồn cá nhân T.Duy: TD-0002 đạt 2/4 ✓ (I, O) — *cao nhất toàn bảng gộp*, TD-0015 đạt 1/4 ✓ (I).

---

### 1.2 Hạn chế cụ thể paper nêu, kèm trích nguyên văn và mục/trang

| # | Mã | Hạn chế paper tự nêu (AUTHOR_STATED) | Trích nguyên văn | Mục / trang PDF |
|---|---|---|---|---|
| 31 | K93 | Cỡ mẫu ít (2 SUT: WordPress, GitLab); khả năng khái quát hạn chế | *"the limited number of services tested... which may affect the generalizability of our findings"* | §7.1 Threats, tr. 21 |
| 32 | K100 | Benchmark không bao gồm hệ thống doanh nghiệp lớn; oracle có false positives | *"The benchmark excludes enterprise-level APIs, and logical oracles may introduce false positives during automated checking."* | §5 Threats, tr. 17 |
| 33 | K127 | Không mở rộng được độ đa dạng lỗi hay độ phủ endpoint; lặp trạng thái | *"without achieving new defect diversity or broader endpoint coverage due to state saturation"* | Discussion, tr. 8 |
| 34 | K136 | Branch coverage của các fuzzer hiện nay còn rất thấp, không công cụ nào vượt 23% | *"none exceeded 23% branch coverage, indicating that deep business logic remains difficult to trigger"* | §3.2, tr. 4 |
| 35 | K166 | Chỉ kiểm nghiệm trên 5 API; dữ liệu gán nhãn thủ công có rủi ro thiên lệch | *"Our approach has been validated on five subject APIs, which might limit external validity"* | §V Threats, tr. 7 |
| 36 | K168 | Chỉ dùng open-source; ground truth lỗi cấy tay; chưa kiểm chứng trên API quy mô công nghiệp | *"we only considered open-source projects, and the seeded vulnerabilities may not reflect all real-world patterns"* | §IV.E Threats, tr. 8 |
| 37 | K191 | Chỉ thử nghiệm tại một doanh nghiệp SES; quy tắc gom cụm lỗi dựa trên heuristic tùy biến | *"findings may not generalize to APIs in other domains... bucketing heuristics rely on custom similarity thresholds"* | §V.D Threats, tr. 8 |
| 38 | K192 | OpenAPI spec quá lớn vượt cửa sổ ngữ cảnh LLM; phát hiện lỗi phụ thuộc xác thực thủ công | *"specifications exceeded the maximum token limits, necessitating truncation that could omit dependencies"* | Appendix C, tr. 14 |
| 39 | TD-0002 | Chỉ 6 REST API .NET; phụ thuộc prompt LLM; mutation score đo bằng Stryker không tách theo dạng yêu cầu | *"evaluated in a set of 6 .NET REST APIs... prompt bias and LLM stochasticity can influence results"* | §6 Threats, tr. 9–10 |
| 40 | TD-0015 | Chỉ 1 dịch vụ FastAPI (5 endpoints); chỉ dùng 1 model; chỉ đo coverage yêu cầu C(T) | *"investigation was conducted on a single medium-complexity service; does not measure bug-finding effectiveness"* | §4 Limitations, tr. 6–7 |

*Ghi chú phân biệt:* Các trích dẫn trên là do **tác giả bài báo tự nêu (AUTHOR_STATED)**. Nhận xét về việc thiếu nhánh random đồng đều cùng request budget hoặc thiếu đo lường mutant riêng biệt theo từng dạng yêu cầu là nhận định của người đối chiếu (REVIEWER_INFERRED), không đưa vào bảng đếm hạn chế của tác giả.

---

### 1.3 Đối chiếu với `evidence-table-merged.md` và `rq-evidence-map.md`

| Mã | # Bảng gộp | # Bản đồ Map | Gần RQ (Bảng gộp) | Ma trận P/I/C/O (Map) | Đánh giá cá nhân | Trạng thái đối soát |
|---|---|---|---|---|---|---|
| K93 | 31 | 32 | 0/4 ✓ · chạm 3/4 | ◐ · ◐ ◐ | Khớp | Hoàn toàn thống nhất |
| K100 | 32 | 14 | 0/4 ✓ · chạm 3/4 | ◐ · ◐ ◐ | Khớp | Hoàn toàn thống nhất |
| K127 | 33 | 41 | 0/4 ✓ · chạm 1/4 | · · · ◐ | Khớp | Hoàn toàn thống nhất |
| K136 | 34 | 15 | 0/4 ✓ · chạm 3/4 | ◐ · ◐ ◐ | Khớp | Hoàn toàn thống nhất |
| K166 | 35 | 37 | 0/4 ✓ · chạm 1/4 | · ◐ · · | Khớp | Hoàn toàn thống nhất |
| K168 | 36 | 28 | 0/4 ✓ · chạm 2/4 | ◐ · · ◐ | Khớp | Hoàn toàn thống nhất |
| K191 | 37 | 29 | 0/4 ✓ · chạm 2/4 | · · ◐ ◐ | Khớp | Hoàn toàn thống nhất |
| K192 | 38 | 16 | 0/4 ✓ · chạm 3/4 | ◐ · ◐ ◐ | Khớp | Hoàn toàn thống nhất |
| TD-0002 | 39 | 7 | **2/4 ✓ (I, O)** · chạm 3/4 | ◐ **✓** · **✓** | Khớp | Bài có số ✓ cao nhất toàn tập |
| TD-0015 | 40 | 25 | **1/4 ✓ (I)** · chạm 2/4 | ◐ **✓** · · | Khớp | Hoàn toàn thống nhất |

---

### 1.4 Kết luận phần của tôi

1. **Về phản chứng:** **KHÔNG CÓ PHẢN CHỨNG**.
   - Trong 8 bài được phân công (#31–#38), không bài nào đạt ≥ 3/4 ô ✓ (cả 8 bài đều 0/4 ✓).
   - Trong 2 bài nguồn cá nhân (#39–#40), TD-0002 đạt 2/4 ✓ (I, O), TD-0015 đạt 1/4 ✓ (I); không bài nào đạt ≥ 3/4 ô ✓.
   - Không có bất kỳ bài nào trùng hoàn toàn 4/4 với RQ của nhóm.
   - **Kết luận:** RQ đứng vững trong phạm vi tài liệu đã rà soát (thuộc trường hợp *"Không paper nào giống đủ 4 yếu tố"*).

2. **Gợi ý hạn chế cho việc tổng hợp khoảng trống nghiên cứu (gap):**
   - **GAP-D (Dữ liệu / SUT):** K93 (2 SUT), K127 (1 SUT), K166 (5 SUT), K168 (5 SUT), TD-0015 (1 SUT) đều thừa nhận mẫu thử nghiệm nhỏ, giới hạn khả năng khái quát. Chưa bài nào sử dụng benchmark chuẩn hóa kèm yêu cầu ngôn ngữ tự nhiên như RESTestBench.
   - **GAP-I (Kỹ thuật can thiệp):** Đa số các nghiên cứu tập trung vào fuzzing ngẫu nhiên mở rộng hoặc dùng LLM (K93, K191, K192, TD-0002, TD-0015); chưa có bài nào khảo sát kỹ lưỡng và độc lập vai trò của kỹ thuật hộp đen cổ điển kết hợp (EP + BVA) trên tham số HTTP REST API.
   - **GAP-C (Nhánh đối chứng & kiểm soát ngân sách):** Các bài so sánh chủ yếu dùng ngân sách thời gian (time budget) hoặc số lần chạy lặp, không cố định số lượng HTTP requests đồng đều giữa các kỹ thuật; thiếu nhánh đối chứng uniform random cùng request budget.
   - **GAP-M (Thước đo & Oracle):** Hầu hết các bài chỉ đo độ phủ (branch coverage < 23% ở K136), tỷ lệ lỗi server HTTP 5XX (K93, K191, K192), hoặc bug tự cấy tay (K168). Chưa bài nào đo khả năng phát hiện mutant mã nguồn riêng biệt (unique mutants) phân tầng theo từng dạng yêu cầu nghiệp vụ.

---

## Mục 2 · Lớp tìm kiếm bổ sung

1. **Rà soát trích dẫn tiến L2 (ngày 18/10/2026):**
   - Tra cứu trên Semantic Scholar (S2) cho các seed mới nhất trong tập: K33 (online 07/10/2026) và K100 (05/10/2026) đều trả về `0 record / No Papers Found` do bài quá mới, S2 chưa kịp lập chỉ mục.
   - Thử nghiệm trên seed K191 thu được **1/1 citation** → bài TD-0158 (Overlay), toàn văn 10 trang, đã đọc và loại ở V2 theo tiêu chí **IC-I** (không thực hiện can thiệp sinh test). Không có bài Include mới từ L2.

2. **Dò kết quả âm (Negative Results) ngày 18/10/2026:**
   - Thực hiện trên Google Scholar nhằm tìm kiếm các bài báo chỉ ra EP hoặc BVA thất bại / không cải thiện trên REST API:
     * Query 1 (rộng): `"REST API" ("negative result" OR "did not improve" OR "fails") ("equivalence partitioning" OR "boundary value")` → khoảng 88 kết quả / thu 10 bài trang đầu.
     * Query 2 (chặt): `"REST API" ("negative result" OR "did not improve") ("equivalence partitioning" OR "boundary value")` → thu trọn vẹn **7/7 kết quả**.
   - **Kết quả:** Cả 7 bài không chứa bất kỳ thí nghiệm âm trực tiếp nào phủ nhận hiệu quả của EP kết hợp BVA so với random trên REST API (TD-0159 phân tích failure mode của LLM; TD-0160 phân tích prompt context). Không có phản chứng tiêu cực đối với RQ.

3. **Đối soát số liệu PRISMA cá nhân T.Duy:**
   - Toàn bộ hồ sơ cá nhân: 175 lượt thu thập nguồn − 39 trùng = **136 bài**.
   - Sàng lọc V1: Loại 76 bài → Cần đọc toàn văn V2: 60 bài (đã đọc 59, thiếu 1 do không có toàn văn).
   - Sàng lọc V2: Loại 55 bài, 2 bài Unsure → **Chính thức Included = 2 bài (TD-0002, TD-0015)**.
   - Khớp 100% giữa `03_final_included.csv`, `evidence-table.md` và `prisma-flow.md`.

---

## Mục 3 · Ghi chú khả thi từ các paper tôi đọc

Bảng tổng hợp từ các bài #31–#38 và #39–#40 nhằm cung cấp dữ liệu thực tế cho Bước 3 (Rà soát tính khả thi):

| Hạng mục | Dữ liệu thực tế từ paper | Khó khăn họ báo & Lưu ý cho nhóm | Khuyến nghị cho Bước 3 |
|---|---|---|---|
| **Code / Harness** | K93: [DynER](https://github.com/starrychen1122/DynER); K100: [Zenodo](https://doi.org/10.5281/zenodo.21964240); K136: [RESTgym](https://github.com/SeUniVr/RESTgym); K168: [RestTestGen](https://github.com/SeUniVr/RestTestGen); TD-0002: [RestTSLLM](https://github.com/uffsoftwaretesting/RestTSLLM); K166: link Verifiability | Nhiều repo phụ thuộc môi trường cũ hoặc không kèm dataset đầy đủ; K100 chỉ công bố artifact trích đoạn | **Không phụ thuộc vào code của họ.** Nhóm chỉ cần clone repo chính thức của RESTestBench và tự viết script sinh test EP+BVA và Uniform Random |
| **Ngân sách & Lặp lại** | K100: 600s × 10 lần và cap 1.000/3.000/6.000 requests; K136: 1h × 10 lần; K191: 200 requests/op × 10 lần (40.800 reqs/run); TD-0015: 20 lần chạy | K100 báo cáo đo bằng thời gian gây chênh lệch số request do độ trễ mạng/máy; K192 throughput không tương đồng lỗi | **Bắt buộc dùng Request Budget cố định (B)** thay vì chạy theo thời gian; thực hiện **≥ 10 lần chạy với seed cố định** để kiểm định thống kê |
| **Oracle & Đếm mutant** | K100: kiểm định thủ công 80% mẫu; K127: schema tự viết gây lỗi giả; K191: gom lỗi 5XX bằng Jaccard; TD-0002: Stryker.NET tính mutation score chung | Lỗi 5XX hay mutation score gộp không phân tách được số lượng mutant riêng biệt do từng ca test phát hiện | Dùng trực tiếp **Requirements-based Mutation Oracle của RESTestBench** (kiểm tra test pass bản gốc và fail bản mutant); đếm unique mutants |
| **Môi trường & Chi phí** | K136: Docker worker 8 cores / 16GB RAM; K191: snapshot dữ liệu production; K192 & TD-0002: chi phí gọi API LLM lớn | Chi phí token cao và tính bất định của LLM là rào cản lớn trong K192 và TD-0002 | RQ của nhóm dùng kỹ thuật thuần thuật toán (EP+BVA vs Random), chạy local Docker nên **chi phí API = $0**, máy tính cá nhân 16GB RAM chạy tốt |

---

## Mục 4 · Nhãn tính mới (bước cá nhân 3)

### 4.1 Nhãn trên thẻ RQ
- **Trạng thái trên thẻ:** Thẻ đăng ký ghi mã **FA26-EXT-12**. Trên giao diện thẻ không có trường nhãn tường minh (`new` / `extension` / `replication`). Nhóm đang gửi mail xác nhận với giảng viên về quy ước ký hiệu "EXT".
- **Nhãn đề xuất của tôi (theo bảng "Bốn kết luận"): `new` (trong phạm vi tài liệu đã xét).**

### 4.2 Căn cứ và lý do xác định nhãn `new`

| Tiêu chí đối chiếu theo RBL-0 | Kết quả đối chiếu | Kết luận phân loại |
|---|---|---|
| **Số paper giống đủ 4/4 (P/I/C/O)** | **0 / 10 paper** (cả 8 bài phân công và 2 bài cá nhân đều không có bài nào giống 4/4) | Loại trừ **Trùng lặp hoàn toàn** |
| **Số paper giống 3/4 có P khác (Replication)** | **0 / 10 paper** (không có bài nào làm đúng I, C, O trên tập dữ liệu khác) | Loại trừ **Replication** |
| **Số paper giống ≥ 3/4 yếu tố (Extension)** | **0 / 8 paper** trong tập phân công (#31–#38: 0/4 ✓); **0 / 2 paper** trong tập nguồn cá nhân (TD-0002 cao nhất chỉ đạt **2/4 ✓ (I, O)**; TD-0015 đạt **1/4 ✓ (I)**) | Chưa đủ điều kiện gán **Extension** theo rubric định lượng |
| **Toàn bộ bảng gộp nhóm (N = 42)** | Bài cao nhất toàn bảng gộp là TD-0002 với **2/4 ✓**; không bài nào đạt 3/4 hay 4/4 | Thống nhất toàn tập dữ liệu |
| **Các nghiên cứu mới nhất 12 tháng** | RESTestBench (EASE 2026): **2/4 ✓ (P, O)**; Req2REST-Guard (2026): **2/4 ✓ (P, O)**; MASTOR (2026): **1/4 ✓ (O)** | Không bài nào chạm ngưỡng ≥ 3/4 ✓ |

**Lý do chi tiết:**
1. Trong 8 bài được phân công đọc sâu (#31–#38), không bài nào có ô ✓ nào (tất cả 0/4 ✓).
2. Trong 2 bài Include từ nguồn cá nhân của tôi:
   - **TD-0002 (RestTSLLM):** Đạt 2/4 ✓ (I: có áp dụng EP/BVA trong prompt; O: đo mutation score). Tuy nhiên, thiếu hoàn toàn C (không có nhánh uniform random cùng ngân sách request) và P khác (6 dự án .NET thay vì 45 yêu cầu RESTestBench).
   - **TD-0015 (Moskalenko 2026):** Đạt 1/4 ✓ (I: module Python sinh test bằng EP+BVA). Tuy nhiên, thiếu C (không có random đối chứng) và O chỉ đo coverage yêu cầu C(T), không đo mutant.
3. Vì **không có bất kỳ bài báo nào giống từ 3/4 yếu tố trở lên**, theo đúng quy tắc 4 kết luận của học phần RBL, kết luận chính thức là: **RQ đứng vững, nhãn tính mới là `new`**.

*Ghi chú mở (chuyển PL):* Nếu giảng viên hoặc nhóm quy ước rằng việc kế thừa Population P (RESTestBench) và Thước đo O (requirements-based mutation score) từ Kogler et al. (EASE 2026) được tính là một nghiên cứu phát triển mở rộng (đổi can thiệp I sang EP+BVA không AI và bổ sung nhánh đối chứng C uniform random cùng budget), nhóm có thể linh hoạt chuyển nhãn sang **`extension`**. Khi có chỉ đạo chính thức từ giảng viên, nhãn sẽ được cập nhật kèm lý do điều chỉnh.

---

## Mục 5 · Rà nghiên cứu mạnh nhất 12 tháng gần đây (bước cá nhân 4)

### 5.1 Các truy vấn đã thực hiện (cửa sổ 18/10/2025 – 18/10/2026)
Thực hiện trên Google Scholar và Semantic Scholar, ưu tiên bài toán REST API, kỹ thuật sinh test và thước đo mutant:
1. `"REST API" "test generation" "mutation score"` (2025–2026) → Rà soát các bài tiếp cận mutation testing trên REST API.
2. `"RESTestBench"` (2025–2026) → Rà soát toàn bộ các bài trích dẫn hoặc sử dụng benchmark RESTestBench.
3. Tra cứu trực tiếp các nghiên cứu hàng đầu vừa công bố: K100 (ESEM 2026), K136 (SBFT 2026), K192 (ASIA CCS 2026), TD-0002 (SBES 2025).

---

### 5.2 Bảng đối chiếu các nghiên cứu mạnh nhất 12 tháng gần đây

| Paper tiêu biểu | Venue / Xuất bản | Vì sao chọn | P / I / C / O | RQ của nhóm đo thêm điều gì họ chưa đo |
|---|---|---|---|---|
| **RESTestBench: A Benchmark for Evaluating LLM-Generated REST API Test Cases** (Kogler et al., 2026) | EASE 2026 / arXiv 2604.25862 | Đúng benchmark nguồn của P; định nghĩa thước đo requirements-based mutation | **✓ / — / — / ✓ (2/4)**. 3 dịch vụ, 106 yêu cầu, 228 mutants; đánh giá 10 LLMs | Chỉ đánh giá các mô hình LLM; **hoàn toàn không có phép so sánh giữa kỹ thuật truyền thống (EP+BVA) với uniform random cùng request budget**; không phân tích sâu số mutant riêng biệt theo từng dạng yêu cầu |
| **Requirement-Aware LLM Testing for Backend REST APIs (Req2REST-Guard)** (Xue et al., 2026) | ResearchGate 2026 (6 trang) | Bài duy nhất dùng lại benchmark RESTestBench và đo mutation score | **✓ / — / ◐ / ✓ (2/4)** (chạm 3/4). Dùng RESTestBench, GPT-4o, mutation score 61% | Chỉ đánh giá LLM kết hợp assertion checker; đối chứng với EvoMaster/Manual; **không kiểm chứng kỹ thuật phi AI (EP+BVA)**, không kiểm soát ngân sách request đồng đều, không đếm unique mutants theo dạng yêu cầu |
| **RestTSLLM: Combining TSL and LLM to Automate REST API Testing** (Barradas et al., 2025) | SBES 2025 · DOI 10.5753/sbes.2025.9670 | Bài gần RQ nhất toàn bảng gộp; kết hợp TSL/EP/BVA và đo mutation score | **◐ / ✓ / — / ✓ (2/4)** (chạm 3/4). 6 dự án .NET; mutation score 40,8% | Áp dụng EP/BVA qua prompt LLM; **không có nhánh đối chứng uniform random cùng request budget**; không dùng RESTestBench; mutation score chưa tách thành số lượng mutant riêng biệt được oracle xác nhận |
| **FDRRestTest: Feedback-Driven Logical Testing for REST APIs** (K100, 2026) | ESEM 2026 · DOI 10.4230/LIPIcs.ESEM.2026.20 | Venue hàng đầu ESEM; kiểm soát ngân sách theo cả thời gian và số request (1k/3k/6k) | **◐ / — / ◐ / ◐ (0/4)** (chạm 3/4). 12 services, 5 baselines | Kỹ thuật dựa trên feedback/repair và logic constraints; **không kiểm chứng EP+BVA**; metric là FRE và response yield, không đo lường mutant mã nguồn |

---

### 5.3 Kết luận mục 5

1. **RQ của nhóm đo được điều các nghiên cứu mới nhất chưa đo:**
   - Đánh giá năng lực của **kỹ thuật kiểm thử hộp đen kinh điển không dùng AI (EP + BVA)** được thiết kế một cách bài bản, có cấu trúc trên tham số REST API.
   - Thiết lập nhánh đối chứng chuẩn mực: **sinh dữ liệu ngẫu nhiên đồng đều (uniform random) dưới cùng một ngân sách request cố định (request budget)**.
   - Thước đo chất lượng sâu: **số lượng mutant riêng biệt (unique mutants)** được oracle của RESTestBench xác nhận (pass bản gốc, fail bản mutant), được phân tầng và bóc tách cụ thể **theo từng dạng yêu cầu nghiệp vụ**.
2. **Lưu ý cần thông báo cho PL và nhóm:**
   - Paper gốc của RESTestBench và blog của tác giả ghi nhận **106 yêu cầu trên 3 dịch vụ** (FastAPI: 63, TodoApp: 14, RealWorld: 29) với 228 mutants, trong khi README repo ghi 103 yêu cầu.
   - Thẻ RQ của nhóm đăng ký **45 yêu cầu (15 yêu cầu / dịch vụ)**: Đây là tập con do nhóm tự chọn. Nhóm cần xác định và tài liệu hóa rõ ràng **quy tắc chọn mẫu 15 yêu cầu/dịch vụ** (chọn ngẫu nhiên có seed cố định hay chọn phân tầng theo độ phức tạp) trong Proposal để bảo đảm tính hợp lệ bên trong (internal validity).
