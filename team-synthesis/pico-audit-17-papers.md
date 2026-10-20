# Kiểm chứng PICO trực tiếp từ17 PDF bổ sung

Ngày20/10/2026 (Asia/Saigon). Phạm vi: GV-01–GV-17; kiểm từng yếu tố bằng phương pháp, thiết kế đối chứng và outcome được báo cáo, sau đó hiệu chỉnh merge/map/rq-check. Đây không phải lần làm lại rq-validation hoặc tái screening IC/EC.

## Kết quả

- Đã kiểm17 bài/68 ô: **67 ô phân loại được,1 ô chưa xác minh** (P củaGV-13).
- **4 ô thay đổi trên3 bài**;14 bài giữ dấu. Số✓ toàn nhóm vẫn P1/I2/C7/O5.
- **5 bài chạm0/4** GV-04/12/14/16/17 giữ···· sau kiểm trực tiếp; lý do từngô ở các mục tương ứng bên dưới.
- Đã đồng bộ59dòng merge/map,25dòng rq-check Lâm và17dòng trích xuất nguồn.42 bài cũ không được tái chấm trong đợt này.
- Chưa chạy code/benchmark/artifacts; chưa đánh giá hiệu quả EP+BVA và chưa làm lại rq-validation.

## Quy tắc và giới hạn áp dụng

Rubric theo [map§1](rq-evidence-map.md#1-quy-tắc-chấm-chuẩn-hoá-toàn-nhóm): ✓ đạt rubric rộng;◐ gần;· khác/không đáp ứng trong thiết kế được đọc. **? là thiếu bằng chứng để phân loại**, không phải·, không được cộng như◐. Chạm là số ✓/◐ đã xác nhận; DualMine ghi `2/4 + ?P`.

- P◐ cần chứng cứ SUT REST chạy/sửa được, không chỉ tênGitLab hoặc một public trace dataset. APIs online/source unavailable ởAGORA+/SATORI thuộc·. DualMine chưa xác minh tested-instance/deployment nên giữ?.
- I✓ cần EP/BVA primary; I◐ cho request generation theo miền/kiểu thật sự triển khai (AGORA+§4.1.1), kể cả chỉ phục vụ thu corpus, nhưng không coi đó là EP+BVA arm. Tái dùng corpus của nghiên cứu khác (SATORI), output constraints hoặc response augmentation (RESTOR) không tự tạo I◐. Đây là adjudication theo mức rộng đang áp dụng choK37/K166, không thay tiêu chí I✓.
- C xét random/fuzz **generator comparator**; random sampling/data split hoặc random action bên trong phương pháp không tự làC. C✓ có thể cùng TIME budget theo rubric, chưa chứng minh uniform REST requests cùng B.
- O✓ cần program mutation/killed mutants; O◐ cho evaluated bugs/failures/response-mutation detection. Input dataset counts, report-quality scores, flaky-class F1 hoặc KillRate chỉ dùng trong training reward không tự làO.

## Các ô thay đổi

| Mã | Ô | Trước | Sau | Căn cứ trực tiếp |
|---|---|---|---|---|
| GV-05 | P | ◐ | · | 25 operations thuộc20 freely accessible industrial APIs được gọi online; §4.3.1 nêu không có mã nguồn của các industrial APIs được dùng. Tên GitLab/LanguageTool không chứng minh chạy evaluation bằng mã nguồn local. Không phải RESTestBench hoặc bộ REST services mã mở có thể gieo program mutants trong evaluation. (§4.1/PDF17–19; Table3/PDF18; §4.3.1/PDF25) |
| GV-05 | I | · | ◐ | Actual evaluation input construction triển khai RESTest với sáu strategies cho224 input parameters: dictionaries, enum domains, random numbers trong min/max, words, Boolean và bounded dates. Đạt rubric gần miền/phân lớp theo kiểu ở bước tạo corpus, chưa phải EP/BVA là intervention chính; AGORA+ chính nhận sẵn requests/responses để suy invariant. (§3/PDF8; §4.1.1/PDF19–20; §6/PDF30) |
| GV-09 | P | ◐ | · | OKAMI gồm 17 operations của 12 industrial APIs; tác giả nêu không có source của API SUT nên chỉ mutation trực tiếp API responses. GitLab được gọi như online API, không có locally runnable source/snapshot control được dùng trong thiết kế này. Theo bucket online/commercial của rubric, không đủ P◐; tên GitLab tự nó không chứng minh gieo program mutants được. (§II-A, PDF3; §IV-A1a, PDF5; §IV-B1d, PDF8) |
| GV-13 | P | ◐ | ? | Paper thử 39 endpoint thuộc GitLab, GitHub, Canada Holidays, OMDb, Spotify, Yelp và YouTube. Paper gọi GitLab/GitHub là các nền tảng mã mở, nhưng mô tả đó chưa chứng minh phiên bản dịch vụ được thử có mã mở, chạy cục bộ được và sửa/gieo mutant được. PDF gốc chưa có bằng chứng về instance thử nghiệm, triển khai hoặc phiên bản mã nguồn đủ để xác nhận P◐ theo rubric REST chạy được đã nêu. Mức liên quan đến REST là chắc chắn; khả năng gieo mutant của bản triển khai chưa được xác minh. (§V Datasets, Setup and Table I/PDF6; §IV-D3 live target API execution/PDF6; Data Availability/PDF11) |

## Tổng hợp17 bài

| Mã | Paper | P | I | C | O | ✓ | Chạm xác nhận |
|---|---|---|---|---|---|---|---|
| GV-01 | [Automatically translating bug reports into test cases for mobile apps](https://doi.org/10.1145/3213846.3213869), ISSTA **2018** | · | · | · | ◐ | 0 | 1/4 |
| GV-02 | [RESTestBench: A Benchmark for Evaluating the Effectiveness of LLM-Generated REST API Test Cases from NL Requirements](https://doi.org/10.48550/arxiv.2604.25862), arXiv v1 / EASE **2026** | ✓ | · | · | ✓ | 2 | 2/4 |
| GV-03 | [Prompt-Based REST API Test Amplification in Industry: An Experience Report](https://doi.org/10.48550/arxiv.2601.17903), arXiv **2026** | · | ◐ | · | · | 0 | 1/4 |
| GV-04 | [RESTOR: Automated Test Oracle Generation for RESTful APIs via Reinforcement Learning](https://www.semanticscholar.org/paper/24ae5ce2bbca7adfd049482b4cd7199d2e4d8faf), PACMSE 3/ISSTA, Article ISSTA094, **10/2026**, DOI [10.1145/3832185](https://doi.org/10.1145/3832185); arXiv:2607.23963 | · | · | · | · | 0 | 0/4 |
| GV-05 | [Test Oracle Generation for REST APIs](https://doi.org/10.1145/3726524), ACM TOSEM 35(1), Article 19, **12/2025** | · | ◐ | · | ◐ | 0 | 2/4 |
| GV-06 | [METFORD - Mutation tEsTing Framework fOR anDroid](https://doi.org/10.1016/j.jss.2024.112332), JSS 222:112332, **2025**; đọc preprint 2501.02875v1 | · | · | · | ✓ | 1 | 1/4 |
| GV-07 | [LLM-Assisted Input-Requirement-Aware Differential Testing of Array Programming Frameworks](https://doi.org/10.1145/3808162), PACMSE/FSE **2026** | · | ◐ | ✓ | ◐ | 1 | 3/4 |
| GV-08 | [YATE: The Role of Test Repair in LLM-Based Unit Test Generation](https://doi.org/10.48550/arxiv.2507.18316), arXiv v1 **2025** | · | · | · | ✓ | 1 | 1/4 |
| GV-09 | [SATORI: Static Test Oracle Generation for REST APIs](https://doi.org/10.1109/ase63991.2025.00116), ASE **2025**; arXiv v2 | · | · | · | ◐ | 0 | 1/4 |
| GV-10 | [Mutation-Guided LLM-based Test Generation at Meta](https://doi.org/10.1145/3696630.3728544), FSE Companion **2025**; arXiv v1 | · | · | · | ✓ | 1 | 1/4 |
| GV-11 | [Nüwa: Enhancing MLIR Fuzzing with LLM-Driven Generation and Adaptive Mutation](https://doi.org/10.1109/icsme64153.2025.00055), ICSME **2025** | · | ◐ | ✓ | ◐ | 1 | 3/4 |
| GV-12 | [BEYOND FLAKY TEST DETECTION: USING THE MODEL CONTEXT PROTOCOL FOR INTELLIGENT TEST FAILURE DIAGNOSIS IN CI/CD](https://doi.org/10.65237/2336-3630-2026-8%281%29-3), Central European Journal of Science and Research **2026** | · | · | · | · | 0 | 0/4 |
| GV-13 | [DualMine: Static-Dynamic REST API Constraint Discovery with Dual Validation](https://www.semanticscholar.org/paper/cd2cc4779b1e786dfffb33db3457ea89fed8d74a), arXiv:2609.27806v1, **2026** | ? | ◐ | · | ◐ | 0 | 2/4 + ?P |
| GV-14 | [Multi-dimensional Assessment of Crowdsourced Testing Reports via LLMs](https://doi.org/10.1109/ASE63991.2025.00150), ASE **2025** | · | · | · | · | 0 | 0/4 |
| GV-15 | [LLM-based Fuzzing Method Using UI-based Input Value Generation for IoT Devices](https://doi.org/10.1109/icce-berlin67488.2025.11277733), ICCE-Berlin **2025**, pp.16–20 | · | ◐ | ◐ | ◐ | 0 | 3/4 |
| GV-16 | [How Far Are We from Detecting Flaky Tests? On the Limits of Code-Based Detection](https://www.semanticscholar.org/paper/65c6bd70ee701d825b5e06deaba07b24e0538379), arXiv:2607.09345v1, **2026** | · | · | · | · | 0 | 0/4 |
| GV-17 | [Intelligent Test Automation: A Multi-Agent LLM Framework for Dynamic Test Case Generation and Validation](https://doi.org/10.71097/ijsat.v16.i1.2232), IJSAT 16(1), **2025** | · | · | · | · | 0 | 0/4 |

## Thống kê sau hiệu chỉnh

| Phạm vi | Yếu tố | ✓ | ◐ | · | ? | Tổng |
|---|---|---:|---:|---:|---:|---:|
| Map nhóm | P | 1 | 28 | 29 | 1 | 59 |
| Map nhóm | I | 2 | 27 | 30 | 0 | 59 |
| Map nhóm | C | 7 | 26 | 26 | 0 | 59 |
| Map nhóm | O | 5 | 39 | 15 | 0 | 59 |
| Rq-check Lâm | P | 1 | 6 | 17 | 1 | 25 |
| Rq-check Lâm | I | 0 | 12 | 13 | 0 | 25 |
| Rq-check Lâm | C | 2 | 7 | 16 | 0 | 25 |
| Rq-check Lâm | O | 4 | 13 | 8 | 0 | 25 |

Histogram số ✓ của59 bài vẫn46 bài×0,11 bài×1,2 bài×2; một dấu? được công khai riêng, không được hiểu như đánh giá đã hoàn tất điều kiện P. Kết quả này không thay cho rà nguồn ngoài tập.

## Căn cứ theo từng paper

Mỗi mục ghi đúng các trang PDF đã đọc, tính từ1; không đồng nghĩa đã đọc lại mọi trang của mọi PDF. SHA256 khóa chính file được kiểm. Các trang kết quả quan trọng đã được render để kiểm cột/đơn vị; ảnh trung gian không thay cho PDF nguồn.

### GV-01

[PDF nguồn](../Paper-source/43-GV-01-YAKUSU.pdf) · 12 trang. Trang đã đọc: 1, 2, 3, 4, 5, 6, 7, 8, 9.

SHA256: `140495041cd05d02c1c18f0e574e141183409a1ad9ba3996cb213a081824f618`.

| Ô | Trước | Sau | Căn cứ trực tiếp và suy luận | Locator PDF | Mức chắc chắn |
|---|---|---|---|---|---|
| P | · | · | SUT là các ứng dụng Android có mã nguồn trên GitHub và bug reports; giao diện UI/Espresso là đối tượng kiểm thử, không phải REST SUT hoặc RESTestBench. | §3/PDF3–7; §4 và §5.1/PDF7 | high |
| I | · | · | Phương pháp chính dùng ontology, NLP và tìm kiếm ánh xạ abstract steps sang UI actions. Không triển khai EP/BVA, phân hoạch miền hoặc kiểu giá trị input. Random UI actions chỉ lấp bước thiếu trong bug report. | §3.1–3.3/PDF3–7; Algorithm2/PDF6 | high |
| C | · | · | Đánh giá effectiveness và thời gian chạy của Yakusu trên các bug reports đã tái hiện thủ công; không có nhánh đối chứng random/fuzz. Chọn issue ngẫu nhiên và random actions nội bộ không phải comparator. | §5.1/PDF7; §5.2/PDF8–9; Table1/PDF9 | high |
| O | ◐ | ◐ | Tái hiện thành công 37/62 issues thực tế; xác minh hành động và stack trace thủ công. Đây là bug/failure reproduction, không phải mutation score hay program mutants. | §5.2.1/PDF8; Table1/PDF9 | high |

- 12/37 issues thành công chỉ cần khởi chạy ứng dụng; Table1 trình bày25 trường hợp không tầm thường.

- Không có LLM: đây là NLP/program-analysis tool; không suy I từ mọi phép phân loại abstract steps.

### GV-02

[PDF nguồn](../Paper-source/44-GV-02-RESTestBench.pdf) · 10 trang. Trang đã đọc: 1, 2, 3, 4, 5, 6, 7, 8, 9.

SHA256: `f815d03a915df859167846fc4bcb16bd183171172dbac3f8622905a5e19db6f3`.

| Ô | Trước | Sau | Căn cứ trực tiếp và suy luận | Locator PDF | Mức chắc chắn |
|---|---|---|---|---|---|
| P | ✓ | ✓ | Đề xuất và thực nghiệm chính trên RESTestBench, ba dịch vụ FastAPI/TodoApp/NestJS RealWorld. Table3 dùng106 yêu cầu và228 mutations, khác mẫu45 dự kiến của nhóm. | §3/PDF3–6; Table2/PDF4; Table3/PDF6 | high |
| I | · | · | Can thiệp là single-step LLM generation so với refinement loop, biến thể precise/vague requirements và10 LLMs. Không có EP/BVA hay generator phân hoạch/biên được triển khai thành kỹ thuật của phép so. | §4/PDF6; §4.1–4.2/PDF7–8; Listings4–5/PDF7–8 | high |
| C | · | · | Đối chứng single-step/refinement và valid/mutated SUT, không có random/fuzz generator arm; cùng artifacts/evaluation không tự tạo random comparator. | §4/PDF6; §4.1–4.2/PDF7–8; Fig3/PDF7 | high |
| O | ✓ | ✓ | Requirements-based mutation score trên chương trình SUT bị chỉnh mã có chủ đích; Listing3 sửa hàm FastAPI, §3.4 định nghĩa số mutants bị giết và MS. Mỗi requirement có singleton test; refinement trên mutated SUT còn lấy trung bình các mutant-specific tests, chưa đồng nghĩa union unique killed IDs của một suite. | §3.3–3.4 và Listings2–3/PDF5; tiếp §3.4/PDF6; Fig3/PDF7 | high |

- Từ random trong example requirement nghĩa là tạo hai user khác nhau; không phải random baseline.

- Tỷ lệ MS trên228 mutations không chuyển trực tiếp thành số unique mutants bị phát hiện của mẫu45.

- Kiểm ảnh PDF5: Đã xem Listing3 sửa source implementation và Eq1 mutation score; xác nhận program mutation, không chỉ sửa JSON responses sau thực thi.

### GV-03

[PDF nguồn](../Paper-source/45-GV-03-Prompt-Based-REST-API-Amplification.pdf) · 8 trang. Trang đã đọc: 1, 2, 3, 4, 5, 6, 7.

SHA256: `71717d020fa57dd25bd01608548961e2f118f9803ec7d3cc9397ac3c49883fa4`.

| Ô | Trước | Sau | Căn cứ trực tiếp và suy luận | Locator PDF | Mức chắc chắn |
|---|---|---|---|---|---|
| P | · | · | SUT thực nghiệm là microservice warehouse-management độc quyền của công ty logistics, sáu endpoints bị ẩn đường dẫn vì bảo mật; PetStore mã mở thuộc nghiên cứu trước, không phải evaluation subject hiện tại. | §3.1–3.3/PDF2–3; Table1/PDF3 | high |
| I | ◐ | ◐ | Prompt amplification yêu cầu thêm tests cho boundary conditions, erroneous inputs và alternative paths từ seed happy-path; có can thiệp gần biên/invalid domain nhưng không thiết kế EP+BVA chính hay thí nghiệm kết hợp riêng. | §4.1/PDF3–4; §5.1/PDF4 | high |
| C | · | · | Đối chiếu baseline suite với ba prompt designs; không có random/fuzz generation comparator. So ngữ cảnh industrial và nghiên cứu PetStore trước cũng không phải random arm. | §4.1/PDF3–4; Tables2–3/PDF5 | high |
| O | · | · | Kết quả đo structural API coverage, số tests generated/executable/merged và edited LoC. Observations/anomalies tại§5.3 là định tính, chủ yếu helper methods/state/flakiness/auth/tooling; không báo distinct detected bugs/mutants. §7.3 và kết luận chỉ rõ coverage chưa đo fault detection và để fault-detection adequacy cho future work. | §4.3/PDF4; Tables2–3 và§5.3/PDF5–6; §7.3,§8/PDF7 | high |

- Đây là arXiv/preprint có ACM template placeholders trên trang1; metadata quality không thay đổi điểm PICO.

- Không dùng lời giới thiệu revealing anomalies để nâng O khi phần kết quả không đo fault-detection outcome.

### GV-04

[PDF nguồn](../Paper-source/46-GV-04-RESTOR.pdf) · 22 trang. Trang đã đọc: 1, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16.

SHA256: `35b3402277f78f994925f81a8ecec96e02673b0a71b93dc45c9e6c4980dddab3`.

| Ô | Trước | Sau | Căn cứ trực tiếp và suy luận | Locator PDF | Mức chắc chắn |
|---|---|---|---|---|---|
| P | · | · | §5.1.2 mô tả traffic từ nền tảng nội bộ ByteDance: hơn1500 APIs/246 services, test229 traces. Đây là SUT/dữ liệu nội bộ, không RESTestBench hoặc bộ REST public chạy/mutate được. | §3.1.1/PDF6; §5.1.1–5.1.2/PDF10 | high |
| I | · | · | Phương pháp sinh assertion từ một request-response và GRPO. Ba valid/invalid variants mỗi key field ở Table1 là RESPONSE bodies để huấn luyện oracle; không phải EP/BVA hay domain-based REQUEST input generator. | §3.1.3/Table1/PDF6–7; §3.2/PDF7–9 | high |
| C | · | · | Baselines là Doubao-Seed-1.6-flash chưa fine-tune và DeepSeek-V3.1-Terminus, cùng prompt/input. Random train/test split hoặc sampling policy không phải nhánh random/fuzz input generator. | §5.1.2–5.1.3/PDF10–11 | high |
| O | · | · | KillRate ở Eq5 là thành phần reward trên response variants. Các outcome thực nghiệm là key-field P/R/F1, expert categories của assertion và adoption rate; không báo program mutant score hoặc distinct SUT bugs/failure detection yield. | §3.2.2/Eq5/PDF9; §5.1.4/PDF11; Figs3–4/PDF12; §5.3/PDF14–15; §5.4/Fig7/PDF16 | high |

- Giữ cả bốn dấu· sau đọc trực tiếp; không suy từ việc nghiên cứu oracle rằng O phải đạt.

- Sửa locator: Fig3 và Fig4 thực tế ở PDF12; PDF11 là đoạn phân tích F1.

- Kiểm ảnh PDF7: Table1 là valid/invalid RESPONSE values.

- Kiểm ảnh PDF12: Fig3 P/R/F1 và Fig4 expert assertion categories; không mutant outcomes.

### GV-05

[PDF nguồn](../Paper-source/47-GV-05-AGORA-Plus.pdf) · 37 trang. Trang đã đọc: 1, 2, 3, 4, 5, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31.

SHA256: `ccd1de2d26444f56735d68462e91971c90d05ab4f501108c7f3f375204dbebbe`.

| Ô | Trước | Sau | Căn cứ trực tiếp và suy luận | Locator PDF | Mức chắc chắn |
|---|---|---|---|---|---|
| P | ◐ | · | 25 operations thuộc20 freely accessible industrial APIs được gọi online; §4.3.1 nêu không có mã nguồn của các industrial APIs được dùng. Tên GitLab/LanguageTool không chứng minh chạy evaluation bằng mã nguồn local. Không phải RESTestBench hoặc bộ REST services mã mở có thể gieo program mutants trong evaluation. | §4.1/PDF17–19; Table3/PDF18; §4.3.1/PDF25 | high |
| I | · | ◐ | Actual evaluation input construction triển khai RESTest với sáu strategies cho224 input parameters: dictionaries, enum domains, random numbers trong min/max, words, Boolean và bounded dates. Đạt rubric gần miền/phân lớp theo kiểu ở bước tạo corpus, chưa phải EP/BVA là intervention chính; AGORA+ chính nhận sẵn requests/responses để suy invariant. | §3/PDF8; §4.1.1/PDF19–20; §6/PDF30 | medium-high |
| C | · | · | Baselines là AGORA và default Daikon để so oracle inference; random generation/chọn subsets chỉ tạo corpus chung. Không có random/fuzz generation comparator dù các oracle engines nhận cùng requests. | §4.1.1/PDF19; §4.2.1/PDF20–21; §4.3.1/PDF25–26 | high |
| O | ◐ | ◐ | Đo48% detection của2.5M errors gieo trực tiếp vào JSON responses bằng JSONMutator và báo32 domain-specific real bugs (17confirmed). §4.3.1 phân biệt rõ với seeding defects vào source program; từ mutants trong Fig8 không làm O thành✓. | §4.3.1/PDF25–26; Table4 và§4.3.2/PDF27; §5/PDF28–30 | high |

**Quyết định áp dụng rubric:** Giữ I◐ ở mức gần của rubric rộng vì tác giả thực sự cấu hình và chạy generators theo miền/kiểu cho224 tham số để thu corpus; không nâng I✓ hoặc coi đây là can thiệp EP+BVA chính. Áp dụng cùng mức rộng đang dùng cho K37/K166; việc tái dùng corpus có sẵn như SATORI không đủ bằng chứng I.

- §3.2–3.3/PDF12–15 số học/bounds là oracle invariants; không dùng những bounds này làm bằng chứng BVA input generation.

- Boundary operators/PDF26–27 mutate output response strings, không phải request input BVA.

- 50/100/500/1K/10K requests là các kích thước dữ liệu học invariants; không có random arm đối chứng với input generator mới.

- Kiểm ảnh PDF18: Đã xem bảng xoay Table3:25 operations và các cột AGORA+/AGORA/Daikon precision với nhiều input counts; không phải random generation comparison.

- Kiểm ảnh PDF27: Table4 xác nhận1,369 assertions và48% FDR; phần dưới mô tả mutation response fields, không source program mutants.

### GV-06

[PDF nguồn](../Paper-source/48-GV-06-METFORD.pdf) · 25 trang. Trang đã đọc: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19.

SHA256: `66b046ea4297806f94554b934428c41338b2cb6f05143e6f32cc57d6ebaabd6d`.

| Ô | Trước | Sau | Căn cứ trực tiếp và suy luận | Locator PDF | Mức chắc chắn |
|---|---|---|---|---|---|
| P | · | · | Đối tượng thực nghiệm là sáu ứng dụng Android native Java có Android instrumented tests; không phải REST APIs hay RESTestBench. Việc ứng dụng có source mở không đủ đạt P◐ khi đơn vị kiểm thử là Android UI/application. | §4.1, PDF13–14; Table 7, PDF14 | high |
| I | · | · | Can thiệp so sánh cách biểu diễn/thực thi program mutants: mutant schemata và traditional mutation. Dùng cùng bộ Android instrumented tests có sẵn; không có can thiệp sinh test input theo EP/BVA, phân hoạch hay miền. Các operator có randomness tạo mutant ở mã nguồn, không phải phương pháp random test-input generation. | §3.1, PDF4; §3.4/Table 6, PDF8–9; §3.6.1, PDF11–13; §4.2, PDF15–17 | high |
| C | · | · | Đối chứng là traditional mutation với cùng test suite và các mutant tương ứng để so behavior/time/space; không có nhánh random-generation comparator. Random seed của ba mutation operators dùng để tạo cùng program mutants giữa hai strategy, không tạo random tests đối chứng. | §3.4/Table 6, PDF9; §4.2, PDF15–17; §4.3/Table 13, PDF17 | high |
| O | ✓ | ✓ | Có thực thi test trên program mutants, ghi killing matrix, số dead mutants và mutation score. Table 12 báo SC/TR average mutation scores 15.6%/17.5%; discrepancy do flakiness được rerun và phân tích, không phải response/input mutation. | §3.6.1/Figures 8–12, PDF11–13; §4.2/Table 12, PDF16–17 | high |

- Giữ P· I· C· O✓ sau kiểm chứng độc lập; căn cứ từng yếu tố khác nhau, không suy C/O từ việc ngoài REST.

- 15.6% và 17.5% là average scores của hai cách thực thi cùng test suite; không phải EP/BVA và random hay chênh lệch chất lượng hai generator.

- Locator §5/PDF18–19 đang có trong map không bao hết threats: §5 bắt đầu cuối PDF18 rồi tiếp tục sau các trang hình. Với PICO nên trỏ trực tiếp method/case-study locators ở trên.

- Kiểm ảnh PDF16: Table 12 headers, generated/alive/dead counts, SC/TR scores, flakiness footnote and full two-column explanation; confirms O✓.

### GV-07

[PDF nguồn](../Paper-source/49-GV-07-ArrayDiff.pdf) · 24 trang. Trang đã đọc: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20.

SHA256: `90e052b5cbf2357013f6030a7261de06ccb8898b696781f866d5a66d6903a4a7`.

| Ô | Trước | Sau | Căn cứ trực tiếp và suy luận | Locator PDF | Mức chắc chắn |
|---|---|---|---|---|---|
| P | · | · | Đánh giá năm cặp phiên bản triển khai của các framework mảng NumPy, CuPy và Octave; chuỗi API là lời gọi thư viện mảng, không phải dịch vụ REST hoặc RESTestBench. | §4.2 Subjects and Table 3/PDF13; §3/PDF6–11 | cao |
| I | ◐ | ◐ | Can thiệp là sinh lời gọi có nhận biết yêu cầu đầu vào: ràng buộc dtype/shape, miền giá trị vô hướng hợp lệ và bộ lọc ngữ nghĩa, sau đó sinh chuỗi bằng thuật toán ngẫu nhiên có phản hồi hoặc thuật toán di truyền. Đây là xử lý miền đầu vào, chưa phải EP/BVA là phương pháp chính. | §3.1 and Table 1/PDF6–7; §3.2 and Algorithm 3/PDF8; §3.3/PDF10–11 | cao |
| C | ✓ | ✓ | Thuật toán RA thực sự sinh test ngẫu nhiên có phản hồi và được so với các biến thể có ngữ nghĩa cùng GA dưới cùng ngân sách tìm kiếm 10 giờ, lặp năm lần. Cùng thời gian đáp ứng rubric rộng; RA không lấy mẫu đồng đều trên các request REST. Bằng chứng cùng ngân sách áp dụng cho các biến thể ArrayDiff, không áp dụng cho ngân sách riêng theo từng API của TitanFuzz/Ghostwriter. | §3.3.1/PDF10 and Algorithm 4/PDF9; §4.2 Evaluated Approaches/PDF13; §4.2 Methodology/PDF15 | cao |
| O | ◐ | ◐ | Hiệu quả được đo bằng số khác biệt giữa các triển khai sau khử trùng, rồi kiểm chứng thủ công để phân biệt bug, thay đổi API và dương tính giả. Đây là khác biệt quan sát được và bug thực đã xác minh, không phải program mutant bị giết. 19 bug đã xác minh trong Table 7 thuộc nhóm khác biệt với đầu vào hợp lệ; hai bug với đầu vào không hợp lệ được xác nhận ở phần trước không được tự ý cộng vào Table 7. | §4.2 Evaluation Metrics/PDF15–16; §4.3/PDF18–19 and Table 7/PDF19; invalid-input confirmations/PDF17 | cao |

- Cả bốn dấu được kiểm chứng độc lập từ phương pháp và đánh giá, không chỉ kế thừa điểm cũ.

- Bổ sung locator C đến PDF15, nơi nêu rõ ngân sách 10 giờ và năm lần chạy. Các baseline bên ngoài nhận ngân sách theo từng API (400 giây/API), vì vậy không khẳng định mọi phương pháp được đánh giá có cùng tổng ngân sách.

- O phân biệt 47 khác biệt với đầu vào hợp lệ/39 khác biệt với đầu vào không hợp lệ do ArrayDiff phát hiện, 19 bug với đầu vào hợp lệ đã xác minh, và cách diễn đạt rộng hơn về bug/vấn đề tài liệu được xác nhận trong abstract.

- Kiểm ảnh PDF19: Table 7: 19 bug đã xác minh, 8 thay đổi API, 10 dương tính giả, 37 khác biệt với đầu vào hợp lệ đã rà soát. Phân biệt các nhóm này với mutant bị giết.

### GV-08

[PDF nguồn](../Paper-source/50-GV-08-YATE.pdf) · 12 trang. Trang đã đọc: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10.

SHA256: `18de1155be54f15f07a0a0471482489331c6c00f660dc826da2cc0881d434f58`.

| Ô | Trước | Sau | Căn cứ trực tiếp và suy luận | Locator PDF | Mức chắc chắn |
|---|---|---|---|---|---|
| P | · | · | Thực nghiệm unit-test generation trên 393 Java classes/3657 methods từ sáu repositories. Binance connector là Java client được unit-test, không phải thí nghiệm chạy REST API SUT hoặc RESTestBench. | §4.2/Table 1, PDF6; §3.1/Listing 1, PDF3 | high |
| I | · | · | YATE gồm chain-of-thought initial generation, compilation fixing bằng static analysis/dependencies, oracle fixing theo execution và coverage-based augmentation. Method hướng branch coverage và sửa test; không triển khai EP/BVA, partition/domain hoặc boundary/invalid-input generator theo rubric. | §3.1–3.6, PDF3–5; Figure 1, PDF4; §5.3/Table 6, PDF8 | high |
| C | · | · | Baselines là LLM-Plain và HITS/SymPrompt/TestSpark/Coverup, cùng component ablations và các LLM. §4.3 nói rõ dùng nhánh LLM của TestSpark, không dùng nhánh EvoSuite. Không có random-generation comparator; số LLM calls là measured cost chứ không chứng minh random same-budget arm. | §4.1, PDF5–6; §4.3, PDF6; §5.3, PDF8; §5.5/Tables 9–10, PDF9–10 | high |
| O | ✓ | ✓ | Mutation score của generated test suites được đo bằng default PiTest/PIT trên Java programs. Có kết quả mutation score và so baseline, ngoài line/branch coverage; Table 9 total YATE class/method 41.6%/47.9%. | §4.4, PDF6; §5.2/Table 4, PDF7–8; §5.5/Table 9, PDF9–10 | high |

- Giữ P· I· C· O✓ sau kiểm chứng độc lập.

- Table 9/PDF10 total 41.6%/47.9% khớp evidence-table hiện có; Table 4/PDF8 lại ghi 41.39%/47.99%. Không hoán đổi hai bảng hoặc nói đây là một giá trị chính xác duy nhất; đây là bất nhất nhỏ nội bộ paper.

- Table 10/PDF10 ghi tổng YATE calls 4296/21249; phần prose PDF9 có con số 23429 ở so HITS, không khớp table. Ưu tiên bảng có locator khi cần thuật lại cost.

- Kiểm ảnh PDF10: Table 9 mutation score columns and Total/Average rows; Table 10 total requests; confirms 41.6%/47.9% and 4296/21249, no random comparator.

### GV-09

[PDF nguồn](../Paper-source/51-GV-09-SATORI.pdf) · 13 trang. Trang đã đọc: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10.

SHA256: `77630ab65ca932fd498b2355e66aa61eb994f1c7704dd8d8df051d1ca3559beb`.

| Ô | Trước | Sau | Căn cứ trực tiếp và suy luận | Locator PDF | Mức chắc chắn |
|---|---|---|---|---|---|
| P | ◐ | · | OKAMI gồm 17 operations của 12 industrial APIs; tác giả nêu không có source của API SUT nên chỉ mutation trực tiếp API responses. GitLab được gọi như online API, không có locally runnable source/snapshot control được dùng trong thiết kế này. Theo bucket online/commercial của rubric, không đủ P◐; tên GitLab tự nó không chứng minh gieo program mutants được. | §II-A, PDF3; §IV-A1a, PDF5; §IV-B1d, PDF8 | high |
| I | · | · | Can thiệp là static oracle inference từ OAS RESPONSE field names/descriptions, rồi chuyển thành assertions. Number min/max hoặc string specific values là output oracles, không phải EP/BVA/domain generation cho request inputs. Random request corpus được tái dùng từ AGORA+ làm evaluation data, không phải thành phần can thiệp SATORI. | §III-A–C/Table I, PDF3–5; §IV-A1b, PDF6; §IV-B1c, PDF8 | high |
| C | · | · | So các LLM, SATORI vs AGORA+ unary/binary, kết hợp oracles và ground-truth upper bound. 10k requests/10×50 pairs là input cho dynamic comparator và 1k holdout pairs làm tập đánh giá, không có nhánh sinh test input ngẫu nhiên đối chứng riêng với generator can thiệp. | §IV-A1b, PDF5–6; §IV-B1a–c, PDF8; §IV-C1, PDF9 | high |
| O | ◐ | ◐ | Có failure detection ratio trên response mutations bằng JSONMutator và real-bug outcomes: SATORI phát hiện 18 bugs; tổng union SATORI+AGORA+ 22 unique bugs. Paper nói rõ không áp dụng traditional source-code mutation vì source không có. Vì vậy O gần theo failure/response detection, chưa O✓ program mutant kills. | §IV-B1d–e/Table III, PDF8; §IV-C1–2/Table IV, PDF9–10 | high |

- Final P· I· C· O◐ = 0✓, chạm 1/4 (trước là chạm 2/4).

- Tách rõ public OKAMI oracle dataset và public SATORI implementation khỏi khả năng truy cập/mutate program source của API SUT.

- Cần đồng bộ P◐→· và lý do trong merge, map, rq-check Lâm; cập nhật số P◐/P· và xếp hạng phụ của map nếu áp dụng.

- Numeric boundary assertions ở output không phải evidence I◐ cho EP/BVA request input generation.

- Kiểm ảnh PDF8: Complete experimental setup including explicit lack of SUT source, JSONMutator response-only mutation, holdout request selection, FDR definition and Table III; confirms P· and O◐.

### GV-10

[PDF nguồn](../Paper-source/52-GV-10-Mutation-Guided-Meta.pdf) · 12 trang. Trang đã đọc: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10.

SHA256: `571de921086ad4f900059c8a2b51c7e0eb04ce8275a4374ec3823fbdc8094967`.

| Ô | Trước | Sau | Căn cứ trực tiếp và suy luận | Locator PDF | Mức chắc chắn |
|---|---|---|---|---|---|
| P | · | · | Triển khai ACH trên 10795 Android Kotlin classes của các platforms nội bộ Meta và cross-app products. Không thí nghiệm REST APIs hoặc RESTestBench. | §2–3, PDF2–4; Table 2, PDF5 | high |
| I | · | · | ACH sinh program faults theo privacy concerns, lọc equivalent mutants rồi prompt LLM sinh unit tests kill mutant. Prompts không yêu cầu EP/BVA, partitions/domains, hoặc boundary input generation; nhận xét hậu nghiệm rằng tests xử lý corner cases/special values không đủ chứng minh một kỹ thuật can thiệp như rubric. | §2/Figure 1/Table 1, PDF2–3; §4.1–4.2, PDF4–5; §6, PDF8–9 | high |
| C | · | · | Có đối chiếu TestGen-LLM tăng coverage với ACH mutation-guided tests. Randomness trong §§4–5 là chọn test/mutant samples cho human review/equivalence assessment, không random-generation comparator. Không nhánh random test input hay random unit-test generator đối chứng trong thiết kế được báo cáo. | §4.2, PDF4–6; §5.2, PDF6–7; §6/Table 8, PDF8–9 | high |
| O | ✓ | ✓ | Program mutants từ Kotlin source, generated tests phải pass original và kill mutant mà existing tests không kill; Table 8 đo mutant-killing tests và kill rates, so với TestGen-LLM. Có 571 mutant-killing tests, 277 không tăng line coverage. Equivalent-mutant estimates và 4660 candidates không được coi mặc định là killed mutants. | §1 assurances, PDF2; §2/Table 1, PDF3; §4.1, PDF4; §6/Table 8, PDF8–9 | high |

- Giữ P· I· C· O✓ sau kiểm chứng độc lập.

- Table 2/PDF5 phân biệt 31677 generated; 9095 build AND pass existing tests; 4660 được agent tin non-equivalent. Dùng đúng nhãn của ba mẫu số.

- Abstract nói 7 platforms, Table 2 có 8 rows do có cross-app products; không tự sửa thành 8 platforms.

- O✓ là rubric rộng về program-mutant outcomes; chưa chứng minh suite-level unique mutant IDs theo dạng REST requirement như RQ nhóm.

- Kiểm ảnh PDF9: Table 8 headers, belief/estimated non-equivalence denominators, mutant-killing tests and kill rates vs TestGen-LLM; 571 total and 277 (49%) no-coverage tests.

### GV-11

[PDF nguồn](../Paper-source/53-GV-11-Nuwa.pdf) · 12 trang. Trang đã đọc: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11.

SHA256: `a6d4a97fffb318566fa259f5b51f07427808454db7b71e28a275dd971df9d3da`.

| Ô | Trước | Sau | Căn cứ trực tiếp và suy luận | Locator PDF | Mức chắc chắn |
|---|---|---|---|---|---|
| P | · | · | Phần mềm được kiểm thử là hạ tầng trình biên dịch MLIR tại các commit LLVM được nêu, không phải benchmark REST API. | §IV-C/PDF7; §II-A/PDF2–3 | cao |
| I | ◐ | ◐ | Quá trình sinh mã hóa đặc tả operation, gồm kiểu đầu vào/đầu ra và miền số chiều, rồi tổng hợp chương trình tuân thủ ràng buộc dữ liệu/điều khiển. Adaptive mutation kết hợp các thành phần IR. Đây là sinh có nhận biết kiểu/miền/ràng buộc, chưa có EP/BVA là phương pháp chính. | §III-C, Figure 4 and Algorithm 1/PDF4; §III-C3–D/PDF5–6 | cao |
| C | ✓ | ✓ | Baseline MLIRSmith được mô tả rõ là tạo chương trình ngẫu nhiên bằng khởi tạo template theo cú pháp. Mỗi thí nghiệm có ngân sách mặc định 24 giờ và lặp năm lần; sinh ngẫu nhiên cùng thời gian vì vậy đạt rubric rộng. Nüwa-random chỉ ngẫu nhiên hóa việc chọn ví dụ few-shot và không phải căn cứ của dấu ✓ này. | §IV-C Experimental Configurations and §IV-D Compared Work/PDF7; §V-B/Table II/PDF8; distinction from Nüwa-random in §V-C/Table III/PDF9 | cao |
| O | ◐ | ◐ | Crash trình biên dịch được khử trùng theo thông báo lỗi, sau đó xác minh/báo cáo kèm lệnh thực thi và backtrace. Table II so sánh số crash bug; mutation trên chương trình test là sinh đầu vào, không phải mutation testing trên mã nguồn trình biên dịch. | §IV-E and §V-A/PDF7; §V-B/Table II/PDF8 | cao |

- Cả bốn dấu đã được kiểm chứng độc lập.

- Giữ riêng 55 bug mới báo cáo trên commit mới nhất bab01ae với 56 bug trong Table II trên commit đánh giá bec839. Đây là hai bối cảnh thí nghiệm khác nhau, không phải tổng source-code mutant.

- Dùng MLIRSmith cùng cấu hình ngân sách thời gian làm bằng chứng cho C; không dùng lựa chọn pass ngẫu nhiên hoặc ablation chọn few-shot ngẫu nhiên.

- Kiểm ảnh PDF8: Table II ghi MLIRSmith=16, MLIRod=18, NNSmith=26, Nüwa-Gen=38, Nüwa-Mut=47, Nüwa=56 crash bug; nhãn cột phân biệt bug và coverage.

### GV-12

[PDF nguồn](../Paper-source/54-GV-12-Beyond-Flaky-Test.pdf) · 23 trang. Trang đã đọc: 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20.

SHA256: `a58fce737528447574c7cc29fa9e5922153cf8d49d4ebe5ffa40ca1808a34862`.

| Ô | Trước | Sau | Căn cứ trực tiếp và suy luận | Locator PDF | Mức chắc chắn |
|---|---|---|---|---|---|
| P | · | · | Đơn vị nghiên cứu là CI build/test records trên một TeamCity production instance. TeamCity REST API chỉ cung cấp dữ liệu chẩn đoán, không là dịch vụ REST SUT để sinh test/gieo mutant. | Methods/PDF9–12; Evaluation procedure/PDF13 | high |
| I | · | · | Pipeline thu thập context rồi phân loại code-change/flaky/infrastructure dựa trên commit và lịch sử pass/fail. Ba diagnostic classes không phải equivalence classes của request input; không có input generator EP/BVA. | Fig2 và Three-category classification/PDF10–11; System scope/PDF12 | high |
| C | · | · | Đối chứng vận hành là điều tra thủ công trên failures tương tự, cùng bảng capability comparison. Không có nhánh random/fuzz input generation hoặc random diagnostic comparator được thí nghiệm. | Evaluation procedure/PDF13; Table1/PDF14; Table2/PDF15; Table3/PDF18 | high |
| O | · | · | Outcome là khoảng diagnostic time. 167 là analysis sessions (có sessions không lỗi); 52/31/17% là ước lượng phân loại không giữ per-session logs, chưa ground-truth accuracy. Đây không phải số distinct defects bị một generator phát hiện hoặc program mutation score. | Results/PDF13–14; Tables1–2/PDF14–15; limitations/PDF19–20 | high |

- Giữ····; case studies ba lỗi vận hành minh họa diagnosis, không biến thành số unique bugs của một chiến dịch fault finding.

- Kiểm ảnh PDF14: Table1 so thời gian manual/MCP theo độ phức tạp; footnote ghi ranges calibrated.

### GV-13

[PDF nguồn](../Paper-source/55-GV-13-DualMine.pdf) · 12 trang. Trang đã đọc: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11.

SHA256: `cc00d9fa95b4d98d04c00c37cb836dca2a00904c51aad60e0fe1c20b4e6c6bb1`.

| Ô | Trước | Sau | Căn cứ trực tiếp và suy luận | Locator PDF | Mức chắc chắn |
|---|---|---|---|---|---|
| P | ◐ | ? | Paper thử 39 endpoint thuộc GitLab, GitHub, Canada Holidays, OMDb, Spotify, Yelp và YouTube. Paper gọi GitLab/GitHub là các nền tảng mã mở, nhưng mô tả đó chưa chứng minh phiên bản dịch vụ được thử có mã mở, chạy cục bộ được và sửa/gieo mutant được. PDF gốc chưa có bằng chứng về instance thử nghiệm, triển khai hoặc phiên bản mã nguồn đủ để xác nhận P◐ theo rubric REST chạy được đã nêu. Mức liên quan đến REST là chắc chắn; khả năng gieo mutant của bản triển khai chưa được xác minh. | §V Datasets, Setup and Table I/PDF6; §IV-D3 live target API execution/PDF6; Data Availability/PDF11 | cao về miền REST; chưa xác minh triển khai chạy được và sửa/gieo mutant được |
| I | ◐ | ◐ | Giai đoạn tổng hợp constraint phân loại giả thuyết theo quan hệ miền, rồi LLM sinh request có mục tiêu để thách thức các biên đang tranh chấp hoặc hành vi đầu vào không hợp lệ. Cách làm này gần kỹ thuật miền/biên đầu vào; can thiệp chính là khám phá constraint kết hợp hai nguồn với dual validation, chưa phải EP/BVA. | §IV-D1–2/PDF5; §IV-D3/PDF6; §V-C/PDF9 | cao |
| C | · | · | Các đối chứng là AGORA+ khai thác oracle động, SATORI và RBCTest khai thác oracle tĩnh, cùng các biến thể bỏ dual validation/counterexample. Vai trò thí nghiệm của chúng là so sánh khám phá oracle, không phải sinh đầu vào ngẫu nhiên. Bộ sinh có mục tiêu chủ động phân biệt các giả thuyết; các phần phương pháp/đánh giá này không đánh giá đối chứng sinh ngẫu nhiên. | §IV-D2/PDF5; §V Baselines/PDF6; §V-B–C/Table IV/PDF8–9 | cao |
| O | ◐ | ◐ | RQ5 báo cáo 48 fault thực. Các vi phạm lặp có cùng endpoint, trường response, constraint và nguyên nhân gốc được gom thành một fault. Độ chính xác TP/FP của oracle là metric riêng; đánh giá fault thực hỗ trợ O◐ nhưng không phải program mutation testing. | §V-E Fault Detection and Figure 2/PDF10; TP/FP definitions in §V Setup/PDF6 | cao |

- Chỉ chốt P khi có bằng chứng về instance GitLab, mã nguồn hoặc cách triển khai được thử; thiếu chi tiết này là tình trạng chưa xác minh, không phải bằng chứng dịch vụ là độc quyền.

- Paper có 39 endpoint thuộc bảy dịch vụ, không phải 39 dịch vụ độc lập.

- C· dựa trên định nghĩa đối chứng thực tế và toàn bộ đánh giá, không dựa vào việc không tìm thấy từ khóa.

- Kiểm ảnh PDF6: Table I liệt kê bảy dịch vụ và tổng 39 operation; phần Datasets bên cạnh mô tả nền tảng công khai/thương mại nhưng không nêu phiên bản triển khai cục bộ hoặc mã nguồn.

### GV-14

[PDF nguồn](../Paper-source/56-GV-14-Crowdsourced-Report-Assessment.pdf) · 13 trang. Trang đã đọc: 1, 3, 4, 6, 7, 8, 9, 10.

SHA256: `2524f52604f0d7922913ba95d7f1ca7b51346f3aa712cfc9c76d47b477691fe3`.

| Ô | Trước | Sau | Căn cứ trực tiếp và suy luận | Locator PDF | Mức chắc chắn |
|---|---|---|---|---|---|
| P | · | · | Dataset là reports từ64 crowdworkers trên ba mobile apps; 1588 test cases và235 defect reports là dữ liệu đầu vào. Không REST APIs/RESTestBench. | §V-A1/PDF7 | high |
| I | · | · | Ba agents chấm textuality, requirement coverage và competitiveness của reports có sẵn; phân cấp requirement/defect clusters không sinh request inputs hay áp dụng EP/BVA. | §III/PDF3; §IV-A/PDF4; §IV-C–D/PDF6–7 | high |
| C | · | · | Baselines đánh giá là sáu chuyên gia và các cách tổng hợp expert ratings; so thời gian sequential/concurrent/human. Không random/fuzz test-generation arm. | §V-A3–A4/PDF7–8; §V-B/TableIV/PDF9; TablesV–VI/PDF10 | high |
| O | · | · | Thí nghiệm đo ICC, weighted kappa, Spearman/Kendall và thời gian đánh giá. Competitiveness dùng rarity của clusters defect reports đã thu; 235 reports không phải lỗi mới mà phương pháp phát hiện, không mutation/fault-yield outcome. | §IV-D/Eq5/PDF7; §V-A3–A4/PDF8; TableIV/PDF9; TablesV–VI/PDF10 | high |

- Giữ····; đã phân biệt unique defect taxonomy hỗ trợ chấm report với outcome phát hiện distinct SUT faults.

- Đọc lại§V-A1:64 là crowdworkers, không ghi nhập nhằng64 reports/crowdworkers.

- Kiểm ảnh PDF9: TableIV là agreement theo app/dimension, Avg so mean human scores.

- Kiểm ảnh PDF10: TableV sensitivity/correlation; TableVI assessment time, không mutant count.

### GV-15

[PDF nguồn](../Paper-source/57-GV-15-IoT-UI-Fuzzing.pdf) · 5 trang. Trang đã đọc: 1, 2, 3, 4, 5.

SHA256: `d63402725e935c0ea95568f9bdc338eaae001a2d045755db11e27628ecf96b2f`.

| Ô | Trước | Sau | Căn cứ trực tiếp và suy luận | Locator PDF | Mức chắc chắn |
|---|---|---|---|---|---|
| P | · | · | Kiểm thử nhắm vào bộ điều khiển bóng đèn màu IoT do nhóm tác giả triển khai cục bộ qua Web UI và một trang XSS của DVWA. Đây là kiểm thử IoT/Web qua UI; đối tượng thí nghiệm không phải RESTestBench hoặc dịch vụ REST. | §IV-A–B1 and Figure 3/PDF3; §IV-B2 and Figures 4–5/PDF4 | cao |
| I | ◐ | ◐ | Phương pháp sinh chuỗi hướng đến lỗ hổng, sửa lỗi định dạng theo thông báo UI và kéo dài các đoạn tùy ý của chuỗi đã lưu để kích hoạt buffer overflow. Đây là fuzzing liên quan đến miền/đầu vào không hợp lệ, chưa phải chiến lược EP/BVA chính được xác định rõ. | §III-B/PDF2–3; §III-C/PDF3; §IV-B1/PDF4 | trung bình đến cao theo rubric rộng về đầu vào không hợp lệ |
| C | ◐ | ◐ | Đối chứng [4] là phương pháp fuzzing trước đó chỉ sinh đầu vào bằng LLM, chạy trong cùng môi trường. Đây là đối chứng bằng công cụ fuzz khác theo rubric rộng. Ba lần lặp đo thời gian đến crash đầu tiên, không phải các ngân sách giới hạn bằng nhau. Sinh/mutation ngẫu nhiên không phải đối chứng độc lập được đánh giá; chọn mode nội bộ ngẫu nhiên không phải căn cứ của dấu này. | §II-B/PDF1; §IV-B1 and Table II/PDF4; comparator reference [4]/PDF5 | cao |
| O | ◐ | ◐ | Đánh giá minh họa phát hiện lỗi buffer overflow được cố ý cài và XSS được gieo sẵn trong DVWA, với thời gian đến overflow crash đầu tiên được đo ba lần. Đây là bằng chứng quan sát failure được gieo, không phải số bug riêng biệt phát hiện được hoặc program-mutant score. | §IV-B1/PDF3–4 and Table II/PDF4; §IV-B2 and Figures 4–5/PDF4 | trung bình đến cao về bằng chứng failure một phần; không có metric số bug riêng biệt |

- Giữ các dấu theo cách hiểu rộng về công cụ fuzz khác và đầu vào không hợp lệ; sửa diễn giải để nêu rõ không có đối chứng ngẫu nhiên, không có bằng chứng cùng ngân sách và không có metric số bug riêng biệt.

- Table II đo số giây đến crash đầu tiên, không phải giây cho mỗi test hoặc toàn bộ ngân sách thí nghiệm.

- Thời gian phương pháp đề xuất: 16.02, 30.17, 36.91 giây; baseline: 237.07, 192.52, 854.71 giây. Đây là ba lần lặp trên một kịch bản overflow được gieo sẵn.

- Buffer overflow và XSS trong DVWA được minh họa; phát biểu tổng quát về null-pointer exception trong đoạn văn không phải một bug phát hiện được đã được đánh giá độc lập khác.

- Kiểm ảnh PDF4: Table II ghi thời gian cần để phát hiện crash theo giây qua ba lần chạy; Figures 4–5 minh họa phát hiện reflected-XSS được gieo trong DVWA.

### GV-16

[PDF nguồn](../Paper-source/58-GV-16-How-Far-Flaky-Tests.pdf) · 15 trang. Trang đã đọc: 4, 5, 7, 8, 9, 10, 11.

SHA256: `2f5a3feff80c7d3efe28cfa0ef15f6d3bd3c2247a6fc85c3f56f6a8d319cd30f`.

| Ô | Trước | Sau | Căn cứ trực tiếp và suy luận | Locator PDF | Mức chắc chắn |
|---|---|---|---|---|---|
| P | · | · | RQ1/2 dùng JVM test-source datasets, RQ3 dùng Cypress/Playwright E2E tests và GitHub Actions logs. Không RESTestBench hoặc request-level REST service testing; một case HTTP503 không đổi đơn vị nghiên cứu. | §III/RQ1–3/TableI/PDF4–5; §IV-C/PDF8–9; §VI-B/PDF11 | high |
| I | · | · | Can thiệp là tái lập CodeBERT detectors, sửa labeling/leakage, project-disjoint protocol và chẩn đoán flakiness. Label stratification/CV không phải phân hoạch tương đương miền request, không BVA input generation. | §III/RQ1–3/PDF4–5; §IV-B/PDF7–8 | high |
| C | · | · | Đối chứng constant always-flaky/always-non-flaky và các detectors, cùng các evaluation protocols. Random cross-validation là cách chia dữ liệu, không random generator để so với EP/BVA. | §III/RQ1–2/PDF4–5; TableV/PDF8; TableVII/PDF10 | high |
| O | · | · | Đo flaky-class precision/recall/F1, weightedF1 và tỷ lệ36/86 truy nguyên được cause. Flaky/non-flaky labels và số tests là đơn vị phân loại/dataset, không killed program mutants hoặc bugs tìm ra bằng generator. | §III/PDF4–5; TableV/PDF8; TableVI/PDF9; §VI-C–D/PDF11 | high |

- Giữ····. Không biến random data split thành C◐ và không biến số flaky tests được phân loại thành mutant kills.

- Kiểm ảnh PDF8: TableV classifier baselines và F1; CV rows là protocol, không random input generation.

### GV-17

[PDF nguồn](../Paper-source/59-GV-17-Intelligent-Test-Automation.pdf) · 9 trang. Trang đã đọc: 1, 2, 3, 4, 5, 6.

SHA256: `b75eee98bc188fce96f595a89013ca21be48ccc36df6d4a9e11451a78ea37d56`.

| Ô | Trước | Sau | Căn cứ trực tiếp và suy luận | Locator PDF | Mức chắc chắn |
|---|---|---|---|---|---|
| P | · | · | Demo sinh calculator.py và Python unittest từ requirement PDF. API endpoint/OAI_CONFIG_LIST là cấu hình gọi LLM, không REST API SUT của nghiên cứu. | §3/PDF2; AppendixA.1–A.6/PDF5–6 | high |
| I | · | · | TCGA/TCMA/TCVA sinh/sửa/validate tests và cả implementation. Paper nói edge cases ở discussion nhưng không đặc tả hay thí nghiệm EP/BVA, partitions hoặc boundary request generator. | §3/PDF2; §4/PDF2–3; §5/PDF4; AppendixA.4–A.6/PDF6 | high |
| C | · | · | §4 và appendix chỉ mô tả setup, agents và vòng sửa đến pass; không báo thí nghiệm có random/fuzz comparator. Temperature điều khiển randomness của LLM không phải một nhánh đối chứng. | §4/PDF2–3; AppendixA.2–A.6/PDF5–6 | high |
| O | · | · | §4 nêu định tính high coverage/adaptability; Figs1–2 là workflow, không có mutation score, distinct bugs/failures yield hoặc bảng kết quả định lượng. Pass/fail của generated tests và sửa cả SUT không đủ chứng minh fault detection. | §3/Fig1/PDF2; §4/Fig2/PDF3; §5/PDF4; AppendixA.5–A.6/PDF6 | high |

- Giữ···· sau đọc phương pháp/evaluation/appendix. Không suy độ chắc từ câu quảng bá abstract.

- Kiểm ảnh PDF3: §4 chỉ mô tả định tính vàFig2 workflow; không bảng results.

## Vấn đề chưa xác minh và cách tiếp tục

**GV-13/P?**: biết chắc paper dùng39 REST endpoints/7 services và không dùngRESTestBench; chưa đủ căn cứ quyết định SUT GitLab trong thí nghiệm đáp ứng P◐ hay thuộc APIonline P·. Cần evidence về tested-instance URL/deployment, source version và khả năng chạy/sửa implementation trong chính evaluation. Không suy proprietariness từ việc thiếu thông tin; không dùng nhãn“open-source platform” thay cho chứng cứ triển khai. Điểm✓ không tăng vì RESTestBench đã được loại trừ.

Các điều kiện thiết kế45IDs, B, miềnuniform, assertions/oracle chung, mutant manifest, reset/retry/flaky và runtime pilot vẫn chưa khóa. Bước tiếp theo là làm lại rq-validation trên evidence đã hiệu chỉnh và các phản chứng ngoài tập; chưa thực hiện tại đây.

## Dữ liệu kiểm chứng

[JSON17 bài/68 ô và SHA256](pico-audit-17-papers.json) · [Checkpoint để tiếp tục](pico-audit-checkpoint.md). Chỉ đọc PDF local; không có lượt tìm kiếm mới hoặc tải/chạy artifacts trong đợt này.
