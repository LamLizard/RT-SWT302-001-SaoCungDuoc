# Kiểm chứng RQ — phần của Tùng

**RQ:** FA26-EXT-12 · **Ngày đối chiếu:** 2026-10-18 (Asia/Saigon).  
**Nguồn phụ trách:** IEEE Xplore và snowballing (#1–5), cộng ba paper OpenAlex được phân công bổ sung (#7–9).  
**Phạm vi:** 8 nghiên cứu nền (#1–5, #7–9) trong [bảng bằng chứng hợp nhất](../../team-synthesis/evidence-table-merged.md) và 4 nghiên cứu bổ sung tại §2. Số thứ tự nghiên cứu nền giữ theo bảng hợp nhất.  

## 0. RQ và chuẩn đối chiếu

### Câu hỏi nghiên cứu

> Trên 45 yêu cầu của RESTestBench, phân hoạch tương đương kết hợp phân tích giá trị biên, so với sinh dữ liệu ngẫu nhiên đồng đều cùng ngân sách, khác nhau thế nào về số mutant riêng biệt bị phát hiện theo từng dạng yêu cầu, khi một mutant chỉ được tính nếu test vượt qua bản gốc nhưng thất bại trên mutant theo oracle của benchmark?

| Thành phần | Giá trị cần đối chiếu |
| --- | --- |
| P | 45 yêu cầu RESTestBench, 15 yêu cầu từ mỗi dịch vụ; yêu cầu, schema, dịch vụ thực thi và mutant tương ứng. |
| I | Kỹ thuật không AI kết hợp EP và BVA để chọn giá trị tham số request từ yêu cầu và schema. |
| C | Sinh dữ liệu ngẫu nhiên đồng đều, cùng số request cho từng yêu cầu. |
| O | Số mutant riêng biệt được phát hiện; test phải pass bản gốc và fail mutant theo oracle requirements-based; báo cáo tổng thể và theo dạng yêu cầu/kiểu tham số. |
| S (thiết kế nghiên cứu) | 10 lần chạy với seed cố định cho mỗi kỹ thuật–yêu cầu; cùng ngân sách request; Wilcoxon signed-rank trên số mutant theo yêu cầu, hiệu chỉnh Holm cho các nhóm yêu cầu. |

### Cách chấm và giới hạn của rubric nhóm

- Ký hiệu theo [ma trận bằng chứng §1](../../team-synthesis/rq-evidence-map.md): **✓** = đạt tiêu chí đối chiếu của nhóm; **◐** = gần; **—** = không khớp hoặc chưa có bằng chứng đáp ứng. Chỉ ✓ được tính vào tổng; S là thông tin bổ sung, không tính vào điểm /4.
- **✓r tại cột C** xác nhận có đối chứng ngẫu nhiên cùng ngân sách theo tiêu chí nhóm; **tính đồng đều của phân phối đầu vào chưa được xác minh**. Vì vậy, ✓r chưa biểu thị sự tương ứng đầy đủ với C của RQ.
- Rubric nhóm cho I✓ khi EP **và/hoặc** BVA là kỹ thuật chính, trong khi thẻ yêu cầu **kết hợp cả hai**. Tám bài này không có I✓ nên khác biệt chưa làm thay đổi kết luận.
- O◐ ghi nhận dữ liệu failures/bugs liên quan đến phát hiện lỗi. Các đơn vị failure occurrence, unique response, stack trace, developer-confirmed bug và source-code mutant không tương đương; O◐ chưa xác nhận nghiên cứu đã đếm lỗi riêng biệt.
- **PDFn** = trang thứ n của file PDF trong repo, tính từ 1; số trang in trên bài có thể khác. Trích dẫn dưới đây giữ nguyên lời tác giả, chỉ nối dòng và chuẩn hóa ligature khi trích xuất.

## 1. Bảng đối chiếu nghiên cứu nền

| Nghiên cứu (# bảng hợp nhất) | P | I | C | O | Hạn chế do tác giả nêu | Chi tiết |
| --- | --- | --- | --- | --- | --- | --- |
| **#1 · K162 / bBOXRT** — A Black Box Tool for Robustness Testing of REST Services (2021) | ◐: 52 REST services, có các dịch vụ chạy được; không RESTestBench (§IV-A, PDF7–8). | ◐: fault model có miền/biên và invalid inputs; không có phép so sánh EP+BVA kết hợp (§III-B, PDF5–6, Table 1). | —: random workload là bước chuẩn bị cho faultload, không nhánh random đối chứng độc lập (§III-B, PDF5; §IV-A, PDF8). | ◐: 24.372 robustness problems theo fault type × parameter × operation, bỏ lặp injection; không mutant IDs (§IV-B, PDF8). **Bất nhất trong paper gốc:** §I, PDF2 ghi 24.373; giữ 24.372 theo §IV-B, PDF8, khớp 23.764 Abort + 608 Hindering. | Phân loại robustness có tính chủ quan; workload có thể coverage thiếu hoặc thiên lệch (**Q01a–b**, §V, PDF14–15). | **0/4 ✓**. [PDF](../../Paper-source/01-K162-bBOXRT.pdf). Request mutation không phải mutation testing trên mã nguồn. |
| **#2 · K52 / P53** — Specification and Automated Analysis of Inter-Parameter Dependencies in Web APIs (2022 theo bảng gộp) | —: HTTP evaluation trên 3 APIs thương mại Stripe/Yelp/YouTube; không RESTestBench (§6, PDF11, Table 3). | ◐: IDLReasoner/CSP xử lý dependencies. EP/BVA ở 203 test kiểm thử chính thư viện, không chứng minh can thiệp EP+BVA cho HTTP requests (§5.3–6, PDF10). | ✓r: random/IDLReasoner cùng 1.000 requests ở §6.1 và 2.000 ở §6.2; chưa xác nhận đồng đều (PDF11). | ◐: failures/HTTP 500/OAS disconformities; 67 so với 1.209 failure occurrences, không số mutant (§6.2, PDF11, Table 5). | Dependencies được nhận diện thủ công, có thể bỏ sót/phân loại sai; thí nghiệm HTTP chỉ 3 APIs (**Q02a–b**, §7.1–7.2, PDF11–12). | **1/4 ✓ theo rubric; yếu tố C tính đồng đều chưa xác minh.** [PDF](../../Paper-source/02-K52-P53.pdf). 40 APIs/2.557 operations là khảo sát dependencies, không cỡ mẫu HTTP experiment. |
| **#3 · P12 / K81 / K55** — Automated Test Generation for REST APIs: No Time to Rest Yet (2022) | ◐: 20 REST services Java/Kotlin mã mở, 675 operations; không RESTestBench (§4.1, PDF5, Table 2). | — theo cách chấm hiện hành của bảng gộp: Tcases là một công cụ được so sánh; each-choice/combinatorial không tự chứng minh EP+BVA là can thiệp chính (§3, PDF4). | ◐: so sánh 10 công cụ/cấu hình, 1 giờ × 10 trials, thêm lượt 24 giờ; không nhánh uniform-random độc lập cùng request budget (§4.2, PDF5). | ◐: unique HTTP 500 theo stack trace, UFP, ULFP; không mutant kills (§4, PDF4–5). | Benchmark 20 services có thể không khái quát; OpenAPI specifications có thể thiếu, làm giảm coverage/tìm bug (**Q03a–b**, §4.6, PDF10). | **0/4 ✓**. [PDF](../../Paper-source/03-P12-K81-K55.pdf). Unique errors, UFP và ULFP là các đơn vị khác nhau, không cộng gộp thành số lỗi; kết quả Table 3 là trung bình trên services/trials. |
| **#4 · P17 / K84** — Enhancing REST API Testing with NLP Techniques (2023) | ◐: 9 services, chỉ 4 services mã mở đo được coverage; không RESTestBench (§4.2, PDF8). | — theo bảng gộp: can thiệp là nâng OpenAPI bằng NLP/restW2V và rule validation; việc dùng Tcases không chứng minh EP+BVA là can thiệp chính (§3, PDF3–7; §4.2.2, PDF8). | ◐: original/enhanced specifications cho 8 tools, 1 giờ × 10 lần; không uniform-random arm riêng (§4.2–4.3, PDF8–10). | ◐: frequency HTTP 2XX/4XX/5XX và unique server responses; không mutant count (§4.3.4, PDF10). | Rule validation loại rules dẫn đến 5XX dù có thể hữu ích tìm lỗi; tập restW2V có thể không đại diện (**Q04a–b**, §6/§4.4.2, PDF11). | **0/4 ✓**. [PDF](../../Paper-source/04-P17-K84.pdf). Coverage chỉ trên 4 SUT; 56,8→59 unique server errors trung bình không tương đương unique mutant kills. |
| **#5 · P38 / K108** — TestGPT-Server: Automatically Testing Microservices with Large Language Models at ByteDance (2025) | —: 1.002 PSMs/14.366 APIs nội bộ, gồm REST và RPC; không RESTestBench (§3.2, PDF7). | ◐: legal/illegal và in/out-bound request mutators, kết hợp LLM và guided stochastic fuzzing; chưa chứng minh EP+BVA không AI như RQ (§2; Table 1, PDF7). | ◐: baseline traffic/manual requests và ablations targeted/fuzzing; không uniform random cùng request budget (§3.2–3.3, PDF8). | ◐: 52 developer-confirmed bugs, không source-code mutants (§3.3.3, PDF8–9, Table 4). | API có thể phản hồi >20 giây, hạn chế fuzzing; request thiếu ngữ nghĩa gây khó chẩn đoán (**Q05a–b**, §4.2–4.3, PDF9). | **0/4 ✓**. [PDF](../../Paper-source/05-P38-K108.pdf). 298/704 là số PSMs REST/RPC, không số APIs. Paper không tách 52 lỗi được xác nhận riêng cho nhóm REST. |
| **#7 · K90** — RESTest: Black-Box Constraint-Based Testing of RESTful Web APIs (2020) | —: 9 operations từ 6 APIs thương mại; không RESTestBench (§4.1, PDF8–9, Table 1). | ◐: rời rạc hóa miền thành random values + constraint solving; không EP+BVA kết hợp là can thiệp chính (§4.2, PDF9–10). | ✓r: RT/CBT cùng 1.000 nominal tests ở experiment 1, 2.000 tests ở experiment 2; đồng xác suất chọn optional parameters không chứng minh đồng đều joint input space (§4.2–4.4, PDF9–12). | ◐: 2.920/4.278 failures; tác giả nói khó biết distinct faults; không mutant count (§4.4, PDF12). | Thiếu repetitions/statistical analysis do quota; khó xác định số distinct faults từ black-box failures (**Q07a–b**, §5 PDF13; §4.4 PDF12). | **1/4 ✓ theo rubric; C tính đồng đều chưa xác minh.** [PDF](../../Paper-source/07-K90.pdf). CBT dùng thêm oracles 2XXD/4XX; không quy toàn bộ chênh lệch failures cho generator. |
| **#8 · K34** — RESTest: automated black-box testing of RESTful web APIs (2021) | —: offline 3 operations Stripe/Yelp/YouTube; online 15 services/7 APIs; không RESTestBench (§4.1–4.2, PDF3). | ◐: constraint-based valid/invalid tests và request mutation, không thí nghiệm EP+BVA như RQ (§3.2–3.3, PDF2–3). | ✓r: offline cùng 2.000 test/service/strategy RT/CBT; tính đồng đều chưa xác minh. Online không dùng để chứng minh equal-budget (§4.1, PDF3). | ◐: failures theo status/spec/validity; >90K tests online, khoảng 30% uncover failures, không mutant score (§4, PDF3). | Online phải điều chỉnh tránh quota; non-functional testing là hướng mở rộng (**Q08a–b**, §4.2 PDF3; §6 PDF4). | **1/4 ✓ theo rubric; C tính đồng đều chưa xác minh.** [PDF](../../Paper-source/08-K34.pdf). Không có mục Threats riêng; hạn chế được trích từ ràng buộc vận hành và hướng nghiên cứu tiếp theo của tác giả. |
| **#9 · K102 / ARTE** — ARTE: Automated Generation of Realistic Test Inputs for Web APIs (2022) | —: HTTP evaluation 14 operations/6 industrial APIs; input extraction 140 operations/48 APIs; không RESTestBench (§5.2–5.3, PDF8–10). | ◐: semantic retrieval từ DBpedia + regex refinement và RESTest constraints; không EP+BVA là can thiệp chính (§3–4, PDF3–7). | ✓r: 6 strategies, 1.000 calls/operation mỗi strategy; có nhánh random, chưa xác nhận uniform joint inputs (§5.1 PDF7; §5.3.1 PDF10). | ◐: 149 failures, validity và API input/output coverage, không mutant count (§5.3.2, PDF10–11, Table 5). | Domain-specific inputs cần manual dictionaries; quota hạn chế thí nghiệm; tên/mô tả thiếu thông tin làm khó sinh input (**Q09a–c**, §5.4.1 PDF11–12; §6 PDF13). | **1/4 ✓ theo rubric; C tính đồng đều chưa xác minh.** [PDF](../../Paper-source/09-K102.pdf). Fuzzing bỏ dependencies trong khi các nhánh còn lại xử lý chúng: baseline còn khác điều kiện (§5.3.1, PDF10). |

### 1.1. Trích dẫn hạn chế từ bản toàn văn

Mỗi mã Q tương ứng với một hạn chế tại bảng §1. Nhận xét về mức độ tương ứng với RQ được trình bày riêng trong các cột P/I/C/O và §1.3, phân biệt với hạn chế do tác giả nêu.

**Q01a — #1, §V Threats to Validity, PDF14 (trang in 24751).** Nhận diện vấn đề robustness có tính chủ quan.

> The identification of robustness issues can be subjective

**Q01b — #1, §V Threats to Validity, PDF15 (trang in 24752).** Workload có thể coverage thiếu hoặc thiên lệch; đoạn này đang nói về random workload/configuration của bBOXRT.

> which may not provide sufficient coverage, or may provide a biased coverage

**Q02a — #2, §7.1 Internal Validity, PDF11.** Dependencies trong tài liệu API có thể bị phân loại sai hoặc bỏ sót.

> Some dependencies might have been misclassified or simply overlooked.

**Q02b — #2, §7.2 External Validity, PDF12.** Cỡ mẫu HTTP evaluation nhỏ, khác khảo sát 40 APIs.

> we only tested three APIs.

**Q03a — #3, §4.6 Threats to Validity, PDF10 (trang in 298).** Giới hạn khái quát từ benchmark 20 services.

> because our evaluation is based on a benchmark of 20 RESTful services, the results may not generalize.

**Q03b — #3, §4.6 Threats to Validity, PDF10 (trang in 298).** Đặc tả đầu vào chưa đầy đủ có thể ảnh hưởng testing tools.

> for some services, the specification is incomplete

**Q04a — #4, §6 Conclusion and Future Work, PDF11 (trang in 1242).** Cơ chế validation đang bỏ các rules dẫn đến server errors; tác giả nói các rules đó có thể hữu ích tìm lỗi.

> our rule validation approach currently filters out rules that result in 5XX errors.

**Q04b — #4, §4.4.2 Internal Validity, PDF11 (trang in 1242).** Tính đại diện của dữ liệu huấn luyện restW2V.

> the training set for the restW2V model might not be representative

**Q05a — #5, §4.2 Handling Slow APIs, PDF9 (trang in 200).** Latency của API hạn chế khả năng gọi nhiều requests.

> some microservice APIs exhibit long response times due to complex logic or limited resources, with response times exceeding 20 seconds in some cases.

**Q05b — #5, §4.3 Generating Semantically Meaningful Test Requests, PDF9 (trang in 200).** Request khó hiểu làm khó chẩn đoán bug; không suy ra bug không tồn tại.

> the unintelligibility of these test requests complicates diagnosis.

**Q07a — #7, §5 Threats to Validity, PDF13.** Thiếu lặp và phân tích thống kê; ngay sau câu này tác giả giải thích do quota của commercial APIs.

> A thorough evaluation should have included more repetitions per experiment (e.g., 10-30) and statistical analysis.

**Q07b — #7, §4.4 Experiment 2, PDF12.** Failure count chưa cho biết số distinct faults.

> it is difficult to know the exact number of distinct faults causing these failures.

**Q08a — #8, §4.2 Online Testing, PDF3.** Ràng buộc vận hành do API quota, không phải kết luận hệ thống chưa chạy được.

> We configured the test runners accordingly so that the quota limitations would never be exceeded

**Q08b — #8, §6 Conclusion and Future Work, PDF4.** Phần hỗ trợ non-functional testing được nêu ở tương lai; khác bài toán mutant detection của RQ.

> we intend to support non-functional testing of RESTful APIs

**Q09a — #9, §5.4.1 Discussion, PDF12.** Domain-specific inputs còn cần chuẩn bị thủ công.

> we resorted to manually-created data dictionaries, and therefore we could not achieve full automation.

**Q09b — #9, §6 Threats to Validity, PDF13.** Quota/rate limits cản trở chạy nhiều requests; đọc cùng phần repetitions ở PDF12.

> Industrial APIs impose restrictive quota limitations

**Q09c — #9, §5.4.1 Discussion, PDF11.** Một nguyên nhân ARTE không sinh được valid input là thiếu thông tin trong tên/mô tả.

> the name and the description of the parameter are not descriptive enough

### 1.2. Kết luận phản chứng phần cá nhân

**Trong 8 nghiên cứu nền đã đối chiếu, không có nghiên cứu đáp ứng đầy đủ P/I/C/O của RQ FA26-EXT-12.** Không nghiên cứu nào đạt 3/4 hoặc 4/4 theo tiêu chí nhóm; mức cao nhất là **1/4 ✓** ở #2, #7, #8, #9, đều thuộc C. Tính đồng đều của đối chứng ngẫu nhiên trong các nghiên cứu này chưa được xác minh. Các ô ◐ không được tính là tiêu chí đáp ứng.

Cả tám nghiên cứu đều không sử dụng RESTestBench và không báo cáo số mutant riêng biệt theo yêu cầu với điều kiện test vượt qua bản gốc nhưng thất bại trên mutant. Do đó, **chưa có bằng chứng phản chứng đầy đủ RQ trong tập 8 nghiên cứu nền**. Kết luận sau khi bổ sung nghiên cứu gần đây được trình bày tại §2.5; kết quả đối chiếu này không đủ để khẳng định tính mới ngoài phạm vi tài liệu đã xét.

**Đối chiếu nhãn tính mới:** trong phạm vi các tài liệu đã phân tích, RQ FA26-EXT-12 được đề xuất phân loại theo hướng **`extension` (mở rộng)**. Cơ sở của đề xuất là kế thừa benchmark, oracle và thước đo phát hiện mutant của RESTestBench, đồng thời bổ sung phép so sánh EP+BVA không sử dụng AI với sinh dữ liệu ngẫu nhiên đồng đều trong cùng ngân sách request và phân tích kết quả theo dạng yêu cầu (§2.5). Ký hiệu `EXT` trong mã RQ chưa được xác minh về ý nghĩa phân loại chính thức. Đề xuất này dựa trên nội dung kế thừa và mở rộng, không suy ra trực tiếp từ số tiêu chí P/I/C/O khớp hoặc khẳng định tính mới ngoài phạm vi tài liệu đã xét.

### 1.3. Hạn chế liên quan đến khoảng trống nghiên cứu

Các hạn chế dưới đây được tổng hợp trong phạm vi phần cá nhân. Đây là dữ liệu đầu vào cho tổng hợp nhóm, chưa phải kết luận về độ mạnh của gap. Theo hướng dẫn RBL-2, các nghiên cứu cùng nhóm tác giả được tính là một nhóm bằng chứng; phát biểu gap ban đầu cần được lưu trước bước tổng hợp và đếm.

| Tín hiệu cụ thể | Căn cứ tác giả | Liên hệ với RQ và giới hạn |
| --- | --- | --- |
| Số lần xuất hiện failure chưa xác định được số lỗi riêng biệt. | #7 Q07b. | Liên quan đến thước đo O và định danh mutant (GAP-M). Chỉ #7 nêu trực tiếp hạn chế này trong danh mục; chưa đủ căn cứ xác định gap mạnh. |
| Hạn ngạch API thương mại hạn chế số lần lặp hoặc số request. | #7 Q07a và ngữ cảnh §5; #8 Q08a; #9 Q09b. | #7/#8/#9 thuộc cùng nhóm tác giả RESTest/ARTE, được tính là một nhóm bằng chứng. Việc vận hành RESTestBench cục bộ có thể giảm phụ thuộc hạn ngạch nhưng chưa được kiểm nghiệm trong hồ sơ này. |
| Thông tin đặc tả chưa đầy đủ hoặc chưa chính xác ảnh hưởng đến sinh test. | #2 Q02a; #3 Q03b; #9 Q09c. | Gồm ba cơ chế khác nhau: nhận diện phụ thuộc, thiếu schema và thiếu ngữ nghĩa tên/mô tả. Chưa đủ cơ sở gộp thành một hạn chế đồng nhất để đếm gap. |
| Cơ chế validation có thể loại quy tắc hữu ích để kích hoạt phản hồi 5XX. | #4 Q04a. | Hạn chế riêng của NLPtoREST; phép so EP+BVA–random trong RQ không trực tiếp giải quyết thuật toán validation này. |

**Nhận định từ đối chiếu:** tám nghiên cứu chưa đánh giá kết hợp RESTestBench, EP+BVA không AI, đối chứng ngẫu nhiên đồng đều cùng ngân sách request và số mutant riêng biệt được oracle xác nhận theo dạng yêu cầu. Đây là khác biệt của thiết kế dự kiến, không phải hạn chế được cả tám tác giả trực tiếp thừa nhận. RESTestBench bổ sung bằng chứng về benchmark và thước đo mutant tại §2; các thành phần kế thừa này không được xem là khoảng trống mới.

## 2. Tìm kiếm bổ sung và rà 12 tháng gần nhất

### 2.1. Các nghiên cứu bổ sung được lựa chọn

Ba nghiên cứu chính và một bài dự phòng được lựa chọn để đối chiếu với RQ, theo thứ tự ưu tiên: mức tương ứng về bài toán/thước đo, thiết kế đánh giá và thời điểm công bố. Truy vấn, ngày tìm, nguồn phát hiện và kết quả loại trùng được trình bày riêng trong [search-log.md](search-log.md#rbl-2--tiếp-nhận-kết-quả-và-kiểm-chứng-full-text-18102026).

| ID · paper · PDF | Ngày và venue đã kiểm độc lập | Quyết định và căn cứ so với bài gần nhất |
| --- | --- | --- |
| **R2R-01 · RESTestBench** · [PDF R2R-01](update-paper/R2R-01-RESTestBench-2026.pdf), 10 trang, arXiv v1 | [arXiv](https://arxiv.org/abs/2604.25862): **28/04/2026**; [chương trình EASE](https://conf.researchr.org/details/ease-2026/ease-2026-ai-models---data/9/RESTestBench-A-Benchmark-for-Evaluating-the-Effectiveness-of-LLM-Generated-REST-API-): **AI Models / Data**, trình bày 09/06/2026, không thuộc main research track. | **Bài chính, ưu tiên 1.** Trực tiếp cung cấp benchmark và thước đo của RQ, có mức tương ứng cao hơn MioHint và bài amplification ở P/O. |
| **R2R-02 · MioHint: LLM-Assisted Request Mutation for Whitebox REST API Testing** · [PDF R2R-02](update-paper/R2R-02-MioHint-2026.pdf), 12 trang, arXiv v4 | [arXiv](https://arxiv.org/abs/2504.05738): v1 **08/04/2025**, v3 **07/01/2026**, v4 **05/03/2026**; tên bản preprint v4 là *MioHint: LLM-assisted Mutation for Whitebox API Testing*. [ICSE 2026 Research Track](https://conf.researchr.org/details/icse-2026/icse-2026-research-track/186/MioHint-LLM-Assisted-Request-Mutation-for-Whitebox-REST-API-Testing), trình bày **16/04/2026**; [artifact tác giả](https://github.com/lijia73/MioHint) ghi DOI `10.1145/3744916.3773228`. | **Bài chính.** Xét bản conference tháng 4/2026 theo lựa chọn của người phụ trách; preprint đầu **08/04/2025** nằm ngoài cửa sổ. Có đối chứng, ablation và 10 lần chạy, cung cấp thiết kế so sánh sinh request rộng hơn bài amplification; không đánh giá mutant kills. |
| **R2R-03 · RESTOR** · [PDF R2R-03](update-paper/R2R-03-RESTOR-2026.pdf), 22 trang, arXiv v1 | [arXiv](https://arxiv.org/abs/2607.23963): **27/07/2026**, ghi nhận accepted ISSTA 2026; [chương trình ISSTA Research papers](https://conf.researchr.org/track/issta-2026/issta-2026-research-papers) xác nhận bài. PDF1–2 ghi PACMSE 3, ISSTA094, **10/2026**, DOI `10.1145/3832185`; nguồn chỉ xác định tháng xuất bản. | **Bài chính.** Đánh giá oracle trên tập kiểm thử độc lập, nghiên cứu chuyên gia và triển khai công nghiệp, rộng hơn bài amplification về thiết kế đánh giá oracle. Training/evaluation chỉ có một lần chạy và không có artifact công khai. |
| **R2R-04 · Prompt-Based REST API Test Amplification in Industry: An Experience Report** · [PDF R2R-04](update-paper/R2R-04-Prompt-Based-REST-API-Test-Amplification-in-Industry-2026.pdf), 8 trang, arXiv v1 | [arXiv](https://arxiv.org/abs/2601.17903): **25/01/2026**, trong cửa sổ. PDF có header FSE ’26 nhưng citation/footer còn `2018`, `Conference`/DOI placeholder; chỉ xác nhận **preprint**, chưa xác nhận track/ấn bản FSE từ nguồn chính thức. | **Bài dự phòng, đã phân tích toàn văn.** 1 microservice/6 endpoints, structural API coverage và effort; không mutation testing. Ít gần O và thiết kế so sánh hẹp hơn các bài chính. Việc kế thừa phương pháp cùng tác giả không đồng nghĩa trùng nghiên cứu PetStore năm 2025. |

Danh sách lựa chọn giới hạn trong tập tài liệu đã tiếp cận, không biểu thị đã bao quát toàn bộ nghiên cứu trong 12 tháng. #5 TestGPT-Server công bố tháng 6/2025 nằm ngoài cửa sổ rà mới.

### 2.2. Đối chiếu P/I/C/O/S từ bản toàn văn

Ký hiệu ✓ tiếp tục theo **rubric nhóm ở evidence map §1**. Riêng **P✓ của RESTestBench chỉ là dùng đúng benchmark**, không chứng minh mẫu 45/15 mỗi dịch vụ. **O✓ là killed mutations/mutation score** theo rubric, không đồng nghĩa paper đã báo cáo đúng unique count theo dạng yêu cầu của thẻ. S ghi riêng, không cộng thành yếu tố thứ năm trong điểm /4.

| Nghiên cứu | P | I | C | O | Thiết kế nghiên cứu (S) và kết luận |
| --- | --- | --- | --- | --- | --- |
| **R2R-01 RESTestBench** | **✓ theo rubric**: đúng benchmark; **106 requirements/228 mutations**, 63/14/29 yêu cầu và 141/22/65 mutations theo FastAPI/TodoApp/RealWorld (Table 3, PDF6). Không phải mẫu 45/15 mỗi dịch vụ. | —: 10 LLMs, single-step vs refinement; precise/vague requirements; không EP+BVA không AI (§4, PDF6–8). | —: single-step là baseline cho refinement, không uniform random cùng request budget (§4.1–4.2, PDF7–8). | **✓ theo rubric**: requirements-based mutation score, số killed mutations trong tử số; singleton test/requirement, `MS_phi = k_phi / card(M)`; nhánh mutant-generated dùng **trung bình** số kills, không union (§3.3–3.4, PDF5–6). Artifact xác nhận pass-valid/fail-mutant (§2.3 dưới). | **2/4 ✓**, chưa là ứng viên ≥3/4. 3 runs/experiment, báo trung bình và max deviation 3,4 điểm %, phân tích precise/vague và theo service; chưa thấy 10 fixed-seed runs, Wilcoxon–Holm theo dạng yêu cầu (§4/PDF7, §6/PDF9). Ba vòng refinement trong một lần sinh test được phân biệt với ba lần chạy thí nghiệm. |
| **R2R-02 MioHint** | ◐: 16 SUTs EMB được liệt kê; 14 từ GitHub + 2 artificial APIs. **8 SUTs** còn trong Table 2 kết quả chính sau loại do runtime/target scope (§4.1, Table 1/PDF8; Table 2/PDF9); không RESTestBench. | —: MIO + static data dependency analysis + GPT-4o hướng dẫn **request mutation** (§3, PDF5–8), không EP+BVA kết hợp. | ◐: EvoMaster 3.2.0 và no-value-expansion ablation; cùng 1 giờ/session, không nhánh uniform random độc lập và không cùng số requests (§4.1/PDF8; §4.3/Table 3/PDF9; §4.4/Table 4/PDF10). | —: bytecode line coverage, target coverage, mutation hit rate, số lần sửa request và thời gian; **mutation hit rate = tỷ lệ sửa input chạm target**, không killed program mutants (§4.1/PDF8). 48,51→53,46% line coverage là **+4,95 điểm %**, không 4,95% mutant detection (Table 2/PDF9). | **0/4 ✓**. 10 repetitions, 1 giờ × 3 settings × 16 SUTs = 480 giờ theo cấu hình tác giả mô tả; Mann–Whitney–Wilcoxon **U** và Vargha–Delaney A12, không signed-rank theo requirement/nhóm Holm như RQ (§4.1–4.2, PDF8–9). Chưa xác minh fixed seeds. Trung bình Table 2 áp dụng cho 8 SUT được báo cáo; §1/PDF2 ghi 4,92%, khác chênh lệch 4,95 điểm phần trăm tính từ Table 2. |
| **R2R-03 RESTOR** | —: >2.300 traces từ >1.500 REST APIs, 246 services/15 business lines tại ByteDance, không RESTestBench (§5.1.2, PDF10). | —: GRPO fine-tune Doubao-Seed-1.6-flash để sinh **assertions** từ một request–response, không sinh request bằng EP+BVA (§3–4, PDF4–9). | —: base Doubao và DeepSeek-V3.1-Terminus cùng prompt/input, không uniform random requests (§5.1.3, PDF10–11). | —: field precision/recall/F1, expert assertion categories, adoption; 85,42% là F1 field identification, 663 là Exact Match assertions, không mutants (§5.1.4–5.2, PDF11–12). **Kill Rate** ở reward áp dụng cho synthetic **response bodies** dương/âm, không mutant SUT (§3.1.3/PDF7; §3.2.2/PDF9). | **0/4 ✓**. Split 8:1:1, held-out 229 samples; expert study 48 cases/13 QA engineers/11 lines; training/evaluation **1 run**. One-tailed Wilcoxon signed-rank N=229 trên field metrics; không 10 seeds hoặc Holm theo dạng yêu cầu (§4/PDF9; §5/PDF10–16). |
| **R2R-04 amplification (bổ sung)** | —: 1 microservice logistics, 6 endpoints nội bộ (§3/PDF2–3). | ◐: LLM amplification có boundary/error cases, không isolated EP+BVA không AI (§4.1/PDF3–4). | —: seed happy-path test và 3 prompt strategies, không random cùng budget (§4/PDF3–4). | —: structural API coverage/edited LoC; anomalies không thành mutant kills (§4.3–5/PDF4–6). | **0/4 ✓**. Không tìm thấy 10 runs/fixed seeds/Wilcoxon–Holm trong full text. Table 3/PDF5 nêu 4/5/11 generated tests theo prompt; đây không phải số repetitions. Bài được dùng bổ sung cho RBL-2, không thêm vào tập included của RBL-1. |

### 2.3. Đối chiếu RESTestBench: dữ liệu, oracle và đơn vị đo

**Nguồn đối chiếu ngày 18/10/2026:** paper gốc, [README artifact](https://github.com/casablancahotelsoftware/RESTestBench#dataset), [danh sách TodoApp](https://github.com/casablancahotelsoftware/RESTestBench/tree/master/data/requirements/todoapp) và [mã `Evaluator.evaluate_test`](https://github.com/casablancahotelsoftware/RESTestBench/blob/master/src/evaluator.py#L52-L118). Phạm vi kiểm chứng là phân tích tĩnh trên nhánh `master` công khai; chưa cố định commit hoặc cài/chạy benchmark, nên các URL này chưa đại diện cho snapshot thực nghiệm.

| Nội dung | Bằng chứng và tác động |
| --- | --- |
| **106 trong paper vs 103 trên README** | Table 3/PDF6: FastAPI **63**, TodoApp **14**, RealWorld **29** = **106**; mutations **141 + 22 + 65 = 228**. README Dataset: **63 + 14 + 26 = 103**. Hai nguồn được trình bày riêng; nguyên nhân chênh lệch 3 yêu cầu RealWorld chưa xác minh. Chưa có cơ sở gán 228 mutations cho artifact 103 yêu cầu. |
| **Không đủ 15 TodoApp** | Paper và README cùng 14; directory TodoApp hiển thị `requirement_1.json`…`requirement_14.json`. Hai variant precise/vague của cùng requirement (§3.2/PDF4) không phải hai yêu cầu độc lập. Nguồn đã kiểm chưa hỗ trợ 15 yêu cầu TodoApp riêng biệt; precise/vague không phải hai đơn vị mẫu độc lập. |
| **Điều kiện oracle** | `evaluate_test`, mã nguồn L86–118: lấy kết quả context `valid`, ghi `passes_on_valid`; duyệt từng index mutant và ghi killed khi test fail; nếu không pass-valid thì xóa killed và cho score=0. Xác nhận trực tiếp quy tắc của thẻ. Đây là hành vi từ phân tích tĩnh evaluator; chưa kiểm tra end-to-end hoặc nguyên nhân nghiệp vụ của mọi failure. |
| **Đơn vị mutant** | §3.3–3.4/PDF5–6: mutants gắn với từng requirement/property; code lưu `requirement_id` và `mutants_killed` là index. Với suite nhiều test, khóa định danh tối thiểu được đề xuất là `(service, requirement_id, mutant_index)` và phép hợp mutant trong từng run/requirement để tránh đếm lặp; chưa xác minh cross-requirement mutants có trùng patch hay không. Đây là nhận định thiết kế từ đối chiếu, không phải kết quả thực nghiệm của paper. |
| **Oracle/assertions dùng chung hai nhánh** | §3.2/PDF4 có golden test mỗi requirement pass-original; §3.4/PDF6 nói golden tests đạt full mutation score và reset SUT trước mỗi generation/execution. Paper không cung cấp phép so riêng generator EP+BVA vs random với cùng oracle; cách thay input, giữ assertions/setup và xử lý stateful/dependencies chưa được xác định trong phép so của nhóm. Golden tests chưa bảo đảm tính hợp lệ của mọi request được sinh độc lập. |
| **Singleton vs request budget** | Paper đánh giá **một executable test/requirement** (§3.4/PDF5), nhưng một test có thể là nhiều requests/stateful steps (§3.2/PDF4). Cách tính ngân sách B cho setup/authentication hoặc candidate inputs chưa xác định; replay executions cần phân biệt với generated requests. Một test không tương đương một HTTP request. |

**Bất nhất P:** các nguồn đã kiểm chưa hỗ trợ điều kiện 15 yêu cầu riêng biệt từ TodoApp. Câu RQ và cỡ mẫu được giữ nguyên trong hồ sơ; việc lựa chọn snapshot, định danh yêu cầu hoặc điều chỉnh P thuộc quyết định của người phụ trách/nhóm. Chưa đủ căn cứ xác nhận điều kiện lấy mẫu 45 yêu cầu, 15 yêu cầu mỗi dịch vụ.

### 2.4. Trích dẫn hạn chế của các nghiên cứu bổ sung

Các trích dẫn được đối chiếu với trang PDF tương ứng. Phần liên hệ với RQ là nhận định từ đối chiếu, tách biệt với lời tác giả.

**QR01a — RESTestBench, §6 Conclusion Validity, PDF9.** Chỉ ba repetitions, không phải bằng chứng đã có thiết kế 10 runs.

> Each experiment was executed only three times, limiting the statistical robustness of our findings.

**QR01b — RESTestBench, §6 External Validity, PDF9.** Độ bao phủ dịch vụ còn hạn chế; EP+BVA trên cùng benchmark không tự khắc phục external validity.

> Our benchmark includes only three services

**QR02a — MioHint, §5 External, PDF10.** Coverage không thay được khả năng phát hiện lỗi.

> fuzzers best at achieving coverage, may not be best at finding bugs

**QR02b — MioHint, §5 External, PDF10.** Evaluation giới hạn Java và GPT-4o; danh sách và tiêu chí loại trừ tại §4.1 giới hạn kết quả chính còn 8 SUT.

> which only focus on open-source services written in Java

**QR03a — RESTOR, §4 Implementation, PDF9.** Tác giả giải thích chi phí training/evaluation là lý do chỉ chạy một lần.

> the training and evaluation processes were conducted in a single run.

**QR03b — RESTOR, §7.2 Generalizability of Source Data, PDF19.** Nguồn dữ liệu cùng một doanh nghiệp; 246 services không đồng nghĩa 246 tổ chức độc lập.

> Our dataset originates entirely from ByteDance’s production environment

**QR04 — bài amplification dự phòng, §7.3 Construct Validity, PDF7.** Ngay trước câu này là structural API coverage; PDF có cả heading §7.2 và §7.3 cùng tên, giữ locator theo nơi chứa đoạn.

> However, it does not directly measure fault detection or overall test adequacy.

Các hạn chế khác có căn cứ nhưng không trích thêm: RESTestBench manual mutants/proxy correctness và OAS mismatch (§6/PDF9); MioHint target selection loại bốn programs và cần source access (§5/PDF10); RESTOR subjective annotation (§7.1/PDF18), Python-only (§7.2/PDF19), không công khai source/data/trained models (Data Availability/PDF20). Không gộp các hạn chế này thành một gap mạnh khi chưa đối chiếu các nguồn của nhóm.

### 2.5. Khác biệt về phép đo và kết luận phần cá nhân

| Nghiên cứu | Đã đo | Phép đo của RQ chưa được nghiên cứu đánh giá |
| --- | --- | --- |
| RESTestBench | Killed requirements-based mutations/mutation score, ảnh hưởng precise/vague và feedback valid/mutated SUT, theo model/service; 3 runs. | **Chênh lệch EP+BVA không AI vs uniform random cùng B requests/requirement**, unique kills trong mỗi run, phân tầng **dạng yêu cầu** và 10 fixed-seed runs/Wilcoxon–Holm trên mẫu đã xác minh. Benchmark, metric và oracle là các thành phần **kế thừa**. |
| MioHint | Coverage và tỷ lệ request mutation chạm hard target; so EvoMaster và ablation. | Chưa đánh giá cùng I/C và O trên RESTestBench; không thể chuyển 4,95 điểm % coverage hoặc 67× mutation accuracy thành kỳ vọng số mutant kills của RQ. |
| RESTOR | Oracle field F1/semantic accuracy/adoption; reward phân biệt response variants. | Chưa đo hiệu quả hai **input generators** trên mutant SUT theo oracle benchmark. RQ giữ oracle chung để kiểm generator, không phải đề xuất thuật toán sinh oracle cạnh tranh RESTOR. |
| Amplification | API coverage và effort tích hợp tests ở một dịch vụ. | Chưa đo oracle-confirmed distinct mutant kills, equal-request random comparison hay repeated paired evaluation theo requirement. |

**Trong 8 nghiên cứu nền và 4 nghiên cứu bổ sung (3 chính, 1 dự phòng), không có nghiên cứu đạt ≥3/4 ✓ theo tiêu chí nhóm hoặc đáp ứng đầy đủ P/I/C/O/S của RQ.** RESTestBench đạt **2/4** và bổ sung bằng chứng quan trọng: **đã có nghiên cứu dùng đúng benchmark và mutation metric requirements-based**. Vì vậy, kết luận không sử dụng RESTestBench và không đo mutant tại §1.2 chỉ áp dụng cho tám nghiên cứu nền.

Kết quả đối chiếu cho thấy **phép so I/C và phân tích theo dạng yêu cầu** là các khía cạnh chưa được đánh giá trong các nghiên cứu đã xét. Đây là cơ sở cho đề xuất **extension** tại §1.2. Chưa có kết quả thực nghiệm để kết luận EP+BVA có hiệu quả cao hơn hoặc thấp hơn đối chứng ngẫu nhiên. Các khác biệt tại bảng trên là nhận định từ toàn văn, chưa đủ để xác định gap mạnh theo tiêu chí nhiều nhóm tác giả cùng nêu hạn chế. Đồng thời, bất nhất P tại §2.3 chưa cho phép xác nhận điều kiện lấy mẫu hiện tại; nhãn phân loại chính thức của RQ chưa được xác minh.

## 3. Thông tin thực nghiệm tham khảo

Mục này ghi nhận thông tin thực nghiệm từ tài liệu để hỗ trợ diễn giải phép đối chiếu; chưa đánh giá tính khả thi bằng số liệu chạy thực tế của nhóm.

| Nghiên cứu | Thông tin tác giả báo cáo | Liên hệ với thiết kế RQ và giới hạn |
| --- | --- | --- |
| #1 bBOXRT | WL_REP=10, FL_REP=3, time limits=0 (§IV-A, PDF8); tool/results tại ref. [21], PDF15. | Có thể tham khảo fault model và biên, nhưng lặp injection không phải 10 trials độc lập; phân loại phản hồi thủ công phát sinh công sức. URL công bố chưa được tải/chạy trong lượt này. |
| #2 IDLReasoner | 1.000 requests/arm/operation để đo validity; 2.000 để tìm failures (§6, PDF11). 203 JUnit tests chạy khoảng 130–140 giây trên i5/16 GB cho chính thư viện (§5.3, PDF10); RESTest, IDLReasoner và supplementary refs. [20], [40], [43], PDF14. | Có code tham khảo và equal-request setup; 130–140 giây không phải thời gian HTTP experiment của nhóm. Việc dùng chung oracle và xử lý dependency giữa hai nhánh cần được xác định trong thiết kế thực nghiệm. |
| #3 No Time to Rest Yet | 20 services; 1 giờ × 10 trials/tool/service, thêm lượt 24 giờ; máy e2-standard-4/16 GB (§4.2, PDF5). Replication package ref. [45], PDF12. | Tham khảo seed/lặp và setup có thể tái lập; so sánh toàn bộ công cụ chưa cô lập tác động của EP/BVA. Quy mô 20 services không phải yêu cầu cỡ mẫu của RQ. |
| #4 NLPtoREST | 9 services, 8 tools, 1 giờ × 10 lần; coverage chỉ trên 4 SUT (§4.2, PDF8). Repo `codingsoo/nlp2rest`, ref. [30], PDF12. | API auth/rate limits khiến loại dịch vụ; local benchmark cần được kiểm chạy thực tế. NLP không thuộc can thiệp I của RQ hiện tại. |
| #5 TestGPT-Server | 14.366 APIs × 24 giờ = 344.784 machine-hours (§3.2, PDF8); hệ thống dùng nền tảng nội bộ (§3.1, PDF7); không thấy công bố public artifact trong PDF. | Quy mô công nghiệp chưa cung cấp ước lượng ngân sách thực nghiệm của nhóm. API chậm >20 giây là cảnh báo cần đo trong pilot. Table 3, PDF8 có bất nhất giữa LoC/%/improvement: chưa đủ căn cứ làm ngưỡng định lượng của RQ. |
| #7 RESTest 2020 | Experiment trên i5/16 GB/Windows 10/Java 8 (§4.3, PDF10); RT/CBT cùng 2.000 tests ở experiment 2 (§4.4, PDF11–12). Supplementary `isa-group/icsoc-2020-supplementary-material`, ref. [21], PDF16. | Có thể tham khảo random baseline; quota từng ngăn repetitions/statistics (§5, PDF13). Phân phối đầu vào, ngân sách request và oracle cần tương ứng giữa hai nhánh; tổng failures không phải ngưỡng số mutant. |
| #8 RESTest 2021 | Offline 2.000 tests/strategy/service; online 10 instances/15 services/7 APIs trong 5 ngày, >90K tests (§4, PDF3); repo `isa-group/RESTest`, footnote ở PDF1. | Thiết kế offline cùng số test là nguồn tham khảo; kết quả online được trình bày riêng. URL/code availability chưa chứng minh cài chạy thành công. |
| #9 ARTE | i7-6700/16 GB/Windows 10/Java 8 (§5, PDF7); 14 operations × 6 strategies × 1.000 calls = 84.000 calls (§5.3.1, PDF10); replication DOI `10.5281/zenodo.5792081` (Verifiability và ref. [23], PDF14). | Có hướng setup CPU, không cần mặc định GPU; thời gian 17 phút/operation của ARTE phụ thuộc latency APIs (§5.3.2, PDF11), không ngoại suy trực tiếp sang 45 yêu cầu. DBpedia/ARTE không thuộc I của RQ hiện tại. |

**Thông tin từ RESTestBench:** §3.4/PDF6 công bố interface `generate_test`/`execute_test`, reset SUT và golden tests; [artifact Setup](https://github.com/casablancahotelsoftware/RESTestBench#setup) nêu Docker/Python 3.11+/Git. Mới kiểm tĩnh, chưa cài/chạy. Theo thiết kế RQ hiện tại: 10 runs × 45 yêu cầu × 2 kỹ thuật = **900 lượt kỹ thuật–yêu cầu**; nếu B requests/lượt thì 900B request được sinh trước replay, với điều kiện B được định nghĩa trên tổng request của mỗi lượt. **Phép tính này có điều kiện, chưa xác nhận đủ 45/15 mỗi dịch vụ:** TodoApp chỉ 14 ở các nguồn đã kiểm (§2.3). Số HTTP executions còn phụ thuộc mutants/replay, setup/reset/retry; chưa có B/runtime nên chưa dự toán hoặc chấm khả thi.

## 4. Kiểm tra hồ sơ cá nhân

- [x] Đối chiếu 8 nghiên cứu nền (#1–5, #7–9) với P/I/C/O; mỗi nghiên cứu có dẫn chứng hạn chế và mục/trang PDF.
- [x] Phân biệt điểm ✓ theo tiêu chí nhóm với mức đáp ứng đầy đủ RQ; S không tính vào điểm /4.
- [x] Phân tích 3 nghiên cứu bổ sung chính (RESTestBench, MioHint, RESTOR) và 1 dự phòng; trình bày phép đo từng nghiên cứu chưa đánh giá so với RQ.
- [x] Ghi truy vấn, ngày tìm, nguồn phát hiện, thời điểm công bố/phiên bản và lý do ưu tiên. MioHint được xét theo bản conference tháng 4/2026; ngày preprint đầu 08/04/2025 được giữ để phân biệt.
- [x] Đối chiếu CSV/workbook 139 ID, membership 3/72/68 và căn cứ triage từng bản ghi; ghi nhận xác nhận của người phụ trách về loại trùng 185 → 139.
- [x] Ghi nhận đề xuất extension có căn cứ kế thừa/mở rộng; phân biệt với nhãn chính thức chưa xác minh.
- [x] Ghi nhận bất nhất P (TodoApp 14 yêu cầu; tổng 106 trong paper so với 103 trên README); giữ nguyên RQ.
