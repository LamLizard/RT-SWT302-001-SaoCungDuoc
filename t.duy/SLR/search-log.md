# Search log - T.Duy - Semantic Scholar + Google Scholar - 15/10/2026

Đợt **tìm trực tiếp qua trình duyệt**, thay báo cáo web-discovery cũ. Source HTML được lưu dưới `audit`; không đổi nguồn thành ACM/OpenAlex. Chuỗi cố định:

```text
("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing") AND ("fault detection" OR "mutant detection" OR "bugs found")
```

## Các lượt thực hiện

| Phiên | Nguồn / thao tác | Query thực tế | Số nguồn báo / số thực thu | Chứng cứ |
|---|---|---|---|---|
| GS-A | Google Scholar, không giới hạn năm khi lấy; IC-Y áp khi lọc | Nguyên văn A | Ước lượng đầu 37; trang cuối xác nhận 27; thực thu 10+10+7+0=27 | gs-A-0/10/20/30.json |
| S2-A | Semantic Scholar, gửi nguyên văn A | A | Site báo không tìm thấy khớp nguyên văn, tự gợi ý without quotes; header 250 thuộc gợi ý | s2-A-0.json |
| S2-A-relaxed | Gợi ý của site, không phải exact A | A bỏ dấu ngoặc kép theo site | Lưu 10 record đầu; **chưa lấy hết 250 gợi ý** | s2-A-0.json |
| S2-seed | Tra cứu trực tiếp title seed | "Combining TSL and LLM to Automate REST API Testing" | One result; thực thu 1 | s2-seed-title.json |
| SB-F-GS | Citations của seed DOI 10.5753/sbes.2025.9670 | cites=8789738611449933692 | 2 / 2 | gs-forward-0.json |
| SB-F-S2 | Citations của cùng seed | Trang seed, citing-papers | 5 / 5 | s2-forward-0.json |
| SB-B-S2 | References của cùng seed | Trang seed, cited-papers; đã mở trang 1..5 | Header 50; thực thu 10+10+6+1+0=27 | s2-backward-1..5.json |
| SB-B-PDF | Bổ sung references thiếu trên site bằng PDF seed | References [1]..[57] | 57 / 57 citation entries | Bản seed arXiv, pp10-11 |

Mọi số hit của nguồn là số hiển thị tại thời điểm chạy, không đảm bảo là số bài thực có. References S2 có metadata sai/thiếu; không báo đã lấy đủ 50. 57 entries PDF gồm paper, sách và web/repo; tất cả vẫn qua cùng IC/EC. Không coi TLDR là abstract, không lấy DOI trong snippet/reference của bài khác gắn cho paper.

## Snowballing một vòng, hai hướng

Seed: RestTSLLM, SBES 2025, DOI 10.5753/sbes.2025.9670. Lý do chọn: đã có PDF và Include đề xuất; sát EP/Category-Partition và mutation metric. Đây là lượt chạy thăm dò trên seed đang chờ T.Duy duyệt, không tự nhận seed đã được người duyệt xác nhận.

| Seed DOI | Vòng | Hướng | Lượt ghi nhận trước bỏ trùng | Ghi chú |
|---|---:|---|---:|---|
| 10.5753/sbes.2025.9670 | 1 | Lùi | 27 S2 + 57 PDF = 84 | Cùng citation có thể xuất hiện cả hai; EC-D ở 02 |
| 10.5753/sbes.2025.9670 | 1 | Tiến | 2 GS + 5 S2 = 7 | Hai nguồn có giao nhau; không đếm thành 7 unique papers |

Chỉ một vòng. Không snowball tiếp từ paper mới. Tra cứu title seed là provenance riêng, không đếm thành paper mới nếu trùng GS.

## Lọc và kiểm tra dữ liệu

- Owner T.Duy; 01 có 157 lượt ghi nhận; canonical unique 124; EC-D 33.
- V1 loại 67 unique; tìm full-text 57; đã đọc 56; chưa lấy được 1.
- Toàn văn đã lưu: 52 PDF + 4 text; còn 5 bài chưa lưu binary PDF (có thể đã có text). Không cộng text vào số PDF.
- V2 loại 53; Unsure đã có PDF 1; Include đề xuất 2.
- Chưa lấy được PDF không tự kết luận EC-A. Các quyết định/chứng cứ nằm ở 02; 03 chỉ hai Include đề xuất.
- Cột raw_title/raw_year/raw_doi/raw_metadata giữ dữ liệu nguồn; các sửa có chứng cứ ở audit/metadata-corrections.csv.
- Đã sửa năm luận văn Sidiropoulos 2025→2024 theo trang bìa. Đã sửa venue RESTTESTGEN từ nhãn sai trên S2 sang IEEE ICST 2020 theo reference [52] và DOI. RestTSLLM dùng DOI hội nghị, không giữ arXiv DOI như bài khác.
- Đối chiếu metadata 12 DOI của references bằng Crossref: 11 trả metadata, 1 báo lỗi; chỉ sửa title/venue khi DOI và độ khớp title >=0,85. Responses lưu trong audit, không đổi discovery source sang Crossref. Hai URL IGI có article/tid=409971 được gộp, không gộp mọi title bắt đầu SmartSE.
- Req2Test không bị loại chỉ vì từ 'unit' trong title: đã đọc §2-4 và xác nhận Entity/UseCase/mocked Controller, không request-level EP/BVA của RQ.

## IC/EC áp dụng không thay đổi

IC-L English; IC-T conference/journal; IC-E có số kết quả trong Table/Figure; IC-Y >=2020; IC-P REST HTTP requests gắn mutant/coverage; IC-I black-box EP và/hoặc BVA cho request parameters. EC-D duplicate; EC-A confirmed full-text inaccessible; EC-S <4 pages; EC-N không thực nghiệm; EC-O UI/E2E web, package-level unit tests, thuần bug report/fault localization. Thiếu chứng cứ=Unsure. Không tự nới năm/tiêu chí để tăng Include.

PICO giữ nguyên: P=45 yêu cầu RESTestBench (15/dịch vụ), I=EP+BVA, C=uniform random cùng request budget, O=unique mutants được oracle xác nhận. Paper RESTestBench Table 3 có 106 yêu cầu, repo có TodoApp 14: nhóm cần chốt commit và danh sách 45 IDs, đặc biệt kiểm tra điều kiện 15 TodoApp. Không đổi PICO ngầm.

## Chỉnh tool và chạy lại

1. Semantic Scholar adapter: bỏ cắt truy vấn 10 từ; bỏ fallback OpenAlex ngầm; lỗi citations/references trả lỗi để log thay vì giả 0; bỏ năm kết thúc hardcode 2026.
2. Bộ cào native: giữ capture/source/page/query; nhận ra site tự bỏ quotes; tách snippet/TLDR khỏi abstract; parse ngày bằng cl-paper-pubdates; nhận PDF URL dạng download/aspx.
3. PDF parser: giữ ranh giới dòng/section và nối từ bị ngắt cuối dòng như equiv- alence. Đã parse lại tất cả PDF tải trong đợt này.
4. Rebuild bằng `python -X utf8 -m slr_pipeline.native_scholar .review/native-scholar .review/native-scholar-parsed.json`, sau đó `python -X utf8 -m slr_pipeline.build_tduy_slr`.

## Phạm vi PRISMA

GS/S2 chỉ nhánh bổ sung theo phân công nhóm; **không cộng vào search chính IEEE/ACM/OpenAlex**. Không gộp số 80/61 của Lâm vào đợt này. Bộ trước chỉ dùng metadata/PDF đã xác minh, không tạo thêm lượt tìm mới. Giữ toàn bộ capture phục vụ tái lập.

## Đợt 2: bổ sung full-text và duyệt lại Unsure — lịch sử 15/10/2026

- Đã thử đủ **32 bài thiếu PDF ở bản trước**, qua link gốc/PDF đã biết, tra bản mở và tra cứu bổ sung theo title/DOI. Kết quả: **22 PDF mới**, **1 record gộp trùng SmartSE**, **9 bài còn chờ lưu PDF xác minh**. Đối chiếu từng ID ở `audit/followup/retrieval-followup32.csv`; link đã thử và lỗi nằm trong `audit/fulltext-extractions`.
- Crossref + ScienceDirect publisher record xác nhận SmartSE ngắn và title dài cùng DOI **10.4018/IJERTCS.409971** (IGI title ID 409971). Vì vậy tổng unique giảm 98→97, duplicate tăng 31→32; không phải bỏ mất record. 01/02 vẫn 129 dòng.
- Duyệt lại 5 Unsure cũ: MINER, MuCoREST, LlamaRestTest và Empirical Comparison loại IC-I theo phương pháp toàn văn; xem trang/mục cụ thể trong 02 và `audit/followup/review-followup5.md`. Agentic LLMs giữ Unsure IC-T: có preprint nhưng chưa xác minh bản conference/journal; DOI Zenodo của reproduction package không thay DOI xuất bản.
- Kết thúc đợt 2: **44 PDF**; V2 loại **41**, Unsure **1**, Include đề xuất **2**. Trạng thái hiện tại sau các đợt bổ sung tiếp theo xem phần cuối nhật ký và PRISMA.
- Sửa chế độ ưu tiên PDF: luôn giữ trang bài làm phương án tiếp theo khi URL PDF thiếu/hỏng. Bộ chạy follow-up không còn bỏ qua tiêu đề thiếu chữ REST/API. Giữ lịch sử lần thử; chỉ chấp nhận alias title đã chỉ rõ trong plan khi phiên bản arXiv đổi title. Không dùng TLDR/description quảng cáo ProQuest làm abstract nghiên cứu.
- Lượt lấy toàn văn này **không tạo lượt discovery mới**: snowballing vẫn 84 lùi + 7 tiến, 63 canonical mới ngoài search/seed; không cộng lại 91 lượt vào 01.
- Chưa tải được PDF không tự gán EC-A. Tại đợt 2, Trailer of the ACM 2030 Roadmap có bản PDF đọc được qua chỉ mục web nhưng bộ tải trả 403 và chưa lưu được; đây là trạng thái lịch sử, không tuyên bố paper không có full-text.
- Kiểm tra: backend build PASS; 8 tests PDF/OA/provenance PASS; 5 native-parser tests PASS; đối chiếu CSV/PRISMA và SHA-256 toàn bộ PDF PASS. Chứng cứ kiểm tra ở `audit/verification.json` và `audit/tool-verification.md`.

## Đợt 3: tìm tiếp 9 toàn văn và xác minh xuất bản — trạng thái tại đợt 3


Baseline: 9 canonical papers without an archived PDF; 1 retrieved paper Unsure IC-T.

- All nine known records were checked using original links and new author/institution/publisher leads. Per-URL attempt logs and cached previous errors are retained; a failed source is never represented as zero search results.
- New PDF: The Trailer of the ACM 2030 Roadmap for Software Engineering, 10 pages, from coauthor Niccolò Puccinelli. Title/authors match; excluded V2 EC-N as a research-roadmap/workshop report, not an original EP/BVA REST experiment.
- Four eligibility decisions resolved before full-text: Contract-Based (thesis, indexed academic abstract), Industrial QA (thesis, indexed Theseus abstract), Evolutionary Robustness (MSc thesis explicitly identified by the VALU3S project), Managing API Evolution (published pages 195-197 = 3, verified DOI metadata). These are V1 exclusions after metadata enrichment, not fabricated full-text retrievals. V1 excluded therefore changes 44 to 48; full-text sought changes 53 to 49.
- Four papers remain pending a verified PDF: SmartSE; E-OBE; Karate DSL security framework; LLMs for Intelligent Software Testing. Primary PDF/repository links have failed or require access verification. No CAPTCHA was bypassed, no inaccessible record was automatically assigned EC-A.
- Agentic LLMs: two Google Scholar versions are arXiv and ADS mirrors of the same preprint. arXiv API has only v1 and no journal_ref/article DOI; OpenAlex calls it a preprint; Crossref returns no sufficiently matching title among eight candidates. Semantic Scholar API returned 429 and DBLP API returned 500, not empty-success evidence. Journal/conference publication remains unverified, so IC-T stays Unsure under the unchanged protocol. Dataset DOI 10.5281/zenodo.19251015 does not prove article publication.
- Discovery is unchanged: 129 occurrences, 97 unique, 32 duplicates. Snowballing is unchanged: 84 backward + 7 forward occurrences, 63 unique papers additional to search/seed. No retrieval attempt is counted as a new discovery occurrence.

Current flow: 129 - 32 = 97; 97 - 48 = 49; 49 - 4 = 45; 45 - 42 - 1 = 2 Include proposals.

The previous followup32 and review-followup5 ledgers are historical snapshots. This round's retrieval-followup9.csv is the current reconciliation for the nine-record baseline.

## Đợt 4 — lịch sử: bổ sung toàn văn text và xác minh Agentic

Baseline: four canonical papers lacked an archived full-text; one retrieved paper remained Unsure IC-T.

- Checked all four primary PDF/source links again. No new binary PDF was saved; the direct downloads remain unavailable. Per-URL errors and previous attempts are retained in the extraction JSON.
- Retrieved two complete publicly indexed full-texts as UTF-8 text: SmartSE (publisher-supplied full-text) and Karate DSL (accepted author manuscript). These are not PDF downloads and do not preserve PDF layout or figure images. Numeric results were read from explicit text tables; no Include is inferred from text alone. Article body line ranges were checked for continuity through the methods, results, conclusion and references, then archived with SHA-256, source URL and line-map provenance. Direct ResearchGate access displayed device verification, which was not solved or bypassed; the archived input is the public search index text.
- SmartSE: Module 4 explicitly uses EP/BVA heuristics but retrieves codebase context and generates JUnit/pytest tests for Kafka/Firefox/OpenMRS. Exclude V2 IC-P because the experiment is not HTTP REST request-level testing. Table 3 reports branch coverage 88.7% and mutation score 74.3%; neither is a unique mutant count.
- Karate-BOLA-Guard: methodology and metrics concern BOLA authorization boundaries and LLM-generated security tests, not request-parameter EP/BVA. Exclude V2 IC-I. Quality ratings and generation/runtime metrics do not become oracle-confirmed unique mutant counts. The accepted manuscript contains a placeholder header DOI; the correct DOI 10.1109/ACCESS.2025.3554960 is verified in repeated accepted-manuscript footers and publisher/Crossref metadata and remains unchanged.
- Two records still lack full-text: E-OBE and LLMs for Intelligent Software Testing. All four records still lack binary PDFs; two of those now have text. No missing text is converted into automatic EC-A.
- Refreshed Agentic verification: arXiv remains v1 (2025-10-31) without journal_ref/article DOI; Crossref top 10 has no sufficiently matching publication; OpenAlex labels the matching record preprint. Keep Unsure IC-T. This does not prove that the work has never been published; the Zenodo reproduction dataset DOI is not article publication evidence.
- Current outcome: 129 occurrences - 32 duplicates = 97 unique; 97 - 48 V1 exclusions = 49 sought; 49 - 2 without full-text = 47 assessed; 47 - 44 V2 exclusions - 1 Unsure = 2 Include proposals.
- Format reconciliation: 47 full-texts = 45 PDF + 2 indexed text. pdf_file/pdf_pages remain empty for text-only archives. fulltext-manifest.json verifies all 47; pdf-manifest.json verifies only 45 PDFs. pending-requests.json tracks the two missing full-texts; pending-pdf-requests.json preserves the four missing binaries.
- Discovery and snowballing did not change: 84 backward + 7 forward occurrences, with 63 additional unique papers. Full-text retries and text retrievals are not new discovery records.

Latest per-record ledger: audit/round4/retrieval-followup4.csv. Previous round ledgers are historical snapshots. Build/export verification checks the latest state against 01, 02, 03, Evidence Table and PRISMA, including all hashes and complete text provenance.

## Đợt 5 — lịch sử: hoàn tất hai toàn văn còn thiếu

**Kiểm tra ngày 15/10/2026; trạng thái hiện tại sau đợt 5.**

- Đã lấy và lưu **2/2 PDF còn thiếu**: TD-0018 E-OBE (10 trang), TD-0044 LLMs for Intelligent Software Testing (8 trang). Bộ tải HTTP vẫn bị 403; trình duyệt mở được trang chính thức sau khi trang tải xong, không tương tác CAPTCHA. Lấy bằng Download chính thức của publisher viewer/eReader, giữ URL nguồn và SHA-256. Không lấy cookie hay dùng luận văn khác thay paper.
- E-OBE dùng đúng liên kết Download lộ ra trong publisher viewer: `/article/download/4098/2249/29342`. ACM dùng Download PDF từ eReader: `/doi/pdf/10.1145/3659677.3659749?download=true`. Tool thêm chế độ import PDF theo plan đã xác minh, kiểm tra chữ ký PDF, title và pages trước khi lưu cache; giữ lịch sử lỗi cũ.
- TD-0018 loại V2 **IC-I**: §III/PDF p4 dùng EvoMaster/MIO và stochastic input, không triển khai EP/BVA; EP trong reference [9] không phải kỹ thuật thực nghiệm. Table 5/PDF p7: 22 schema mismatches + 4 HTTP 500 + 1 authentication = 27 occurrences thuộc 3 categories; không đổi thành số mutant riêng biệt được oracle xác nhận. Không loại nhầm thành UI testing.
- TD-0044 loại V2 **EC-N**: §2/PDF p2 và Figure 1 tổng hợp 12 papers từ Scopus, §3-4 phân loại, §5/PDF p8 kết luận synthesis; không có thực nghiệm gốc REST request EP/BVA. Đã lưu toàn văn HTML ACM đối chiếu riêng, nhưng manifest tính PDF một lần.
- Agentic: tra mới arXiv API, Crossref **20 candidates**, OpenAlex (phản hồi thành công lưu nguyên bản). arXiv vẫn v1, chưa journal_ref/DOI conference-journal; OpenAlex preprint; Crossref chưa khớp title. **Unsure IC-T**; không coi kết quả tìm kiếm âm tính là bằng chứng chưa xuất bản. Không thay DOI bằng Zenodo reproduction package.
- Kết quả: **49 toàn văn = 47 PDF + 2 text**, **0 thiếu toàn văn**, V2 loại **46**, Unsure đã đọc **1**, Include đề xuất **2**. Hai text SmartSE/Karate chưa có PDF binary; giữ phân biệt rõ.
- PRISMA: **129−32=97; 97−48=49; 49−0=49; 49−46−1=2**. 01/02 vẫn 129 dòng, 03 vẫn 2 đề xuất cần thẩm định. Không chuyển Unsure thành Include tự động.
- Snowballing vẫn **84 lùi + 7 tiến = 91 lượt**, 64 canonical trong nhánh, giao search/seed 1, mới 63; search/seed unique 34; **34+63=97**. Đây là follow-up truy cập, không phải iteration discovery mới.
- Bằng chứng: browser-pdfs.json, các DOM capture, publication-verification.json, retrieval-followup2.csv, PDF-extracted text và ảnh render trang phương pháp. Nguồn GS/S2 là bổ sung; không cộng các lượt vào PRISMA search chính IEEE/ACM/OpenAlex.

- Sửa metadata venue của RestTSLLM từ nhãn arXiv trong search result thành SBES 2025 theo running header PDF và seed detail; raw_metadata/provenance vẫn giữ nguyên, không đổi quyết định hay số lượng.

## Đợt 6 — lịch sử: xác minh Agentic và hai Include đề xuất

**Thẩm định ngày 15/10/2026 — đợt hiện tại.**

- Giữ **TD-0002 RestTSLLM** và **TD-0015 orchestration** là **Include đề xuất (PROPOSED)** sau khi kiểm tra lại đủ IC-L/T/E/Y/P/I và EC-D/A/S/N/O, không thay người dùng chốt Include. Bảng lý giải từng tiêu chí và trang/mục nằm ở `audit/round6/review-two-includes.md`; review ledger có hash PDF và kết quả từng bài.
- RestTSLLM: DOI chuyển thành công đến publisher SBC, xác nhận SBES2025, ngày22/09/2025, pp71–81. Ngoài PDF §3/p4, đã đọc prompt và output test thật của repo tác giả, pin commit `4e0a93e55131e18592623bfdd2999e206d540cb4`. Có Category-Partition/EP/boundaries, HttpClient requests, test username/password min/max. Không chỉ suy luận từ keyword. Không chạy lại experiment tác giả trong lượt này.
- Orchestration: publisher/Crossref xác nhận journal, ngày29/05/2026, pp31–40. PDF §2.2/p3 và §3.2/p5-6 xác nhận FastAPI request parameters, NL+OpenAPI, EP+BVA, generator G không gọi LLM; Table3/p6 là coverage theo functional requirements.
- Giới hạn: cả hai không uniform random cùng budget và không báo outcome unique oracle-confirmed mutants của RQ. Giữ mutation score và requirements coverage đúng bản chất. Không thêm những điều kiện này thành IC/EC mới. Code công khai xác minh được ở RestTSLLM; chưa xác minh code public của orchestration.
- Agentic vẫn **Unsure IC-T**. arXiv/Crossref/OpenAlex phản hồi mới thành công, chưa journal_ref/DOI xuất bản. Crossref20 kết quả không khớp; query phụ title rút gọn+Besjes chỉ trả1 bài vật lý không liên quan. DBLP202 là challenge HTML, không phải thành công XML. Không nhầm bài tiền thân đã xuất bản hoặc Zenodo dataset. Thiếu kết quả không chứng minh tuyệt đối chưa xuất bản.
- **Không đổi số liệu**: 129 lượt, 32 trùng, 97 unique; V1 loại48; 49 toàn văn (47PDF+2text); V2 loại46; Unsure1; Include đề xuất2. Không còn thiếu toàn văn; SmartSE/Karate vẫn thiếu binaryPDF nhưng có text.
- PRISMA: **129−32=97; 97−48=49; 49−0=49; 49−46−1=2**. Snowballing **84 lùi+7 tiến**, 64 canonical trong nhánh, overlap1, mới63; **34+63=97**. Đây là xác minh, không thêm discovery hay lượt snowball.

## Đợt 7 — lịch sử: tìm bổ sung EP/BVA/random/budget

**Lượt bổ sung ngày15/10/2026.**

Giữ nguyên StringA và IC/EC; không nới năm. Vì cần tìm comparator random/budget sát RQ, dùng thêm các query dưới đây, phân loại là tìm bổ sung B-derived/targeted lookup, không gắn nhãn nguyên văn A/B chính thức.

| Nguồn/lượt | Query thực tế | Hits hiển thị / records thu | Phạm vi và capture |
|---|---|---|---|
| Google Scholar B-derived | `("REST API" OR "RESTful API") ("equivalence partitioning" OR "boundary value") random` | about206 /10 | Chỉ trang đầu, không tuyên bố vét cạn206; gs-B-random-0.json |
| Semantic Scholar B-derived | `REST API equivalence partitioning boundary value random` |25 /10 | Chỉ trang đầu; s2-B-random-0.json. Có nhiều kết quả lệch chủ đề; giữ đủ records và loại theo IC/EC, không dùng TLDR làm abstract |
| Google Scholar targeted lookup | `"Automated functional and robustness testing of microservice architectures"` | Best result1 /1 | Candidate từ web-discovery, kiểm chứng lại trên GS; gs-title-macrohive.json |
| Google Scholar all-terms budget | `("REST API" OR "RESTful API") "equivalence partitioning" "boundary value" "budget" "random"` |7 /7 | Đã thu đủ cả7 kết quả; gs-budget-all7.json. Không có paper trực tiếp đáp ứng toàn bộ RQ được xác minh |

- Thêm28 occurrences TD-0130..TD-0157; giữ nguyên129 ID cũ và provenance. Sau gộp:27 canonical mới,1 trùng bài Role of Test Automation đã có. **157 lượt,124unique,33trùng**.
- Sàng lọc: V1 loại67; tìm toàn văn57; đã lưu53 =51PDF+2text; còn4 mới chờ (TD-0133/0135/0136/0137). V2 loại50; Unsure đã đọc1 (Agentic); Include đề xuất2. Kiểm **157−33=124;124−67=57;57−4=53;53−50−1=2**.
- Thêm4 PDF đã xác minh title/pages: Inter-parameter dependencies14p, RESTest16p, RESTful DB scripts12p, MacroHive14p. Bộ tải HTTP lấy2; browser download chính thức lấy2 còn lại rồi import bằng tool với kiểm tra signature/title/hash. Publisher HTML Robot Framework được lưu làm bằng chứng V1 EC-O, không tính full-text assessed của nhánh sauV1.
- **MacroHive giữ làm nền, loại V2 IC-P**: có EP request classes và REST coverage nhưng generator dựa formal schema, không NL+schema của protocol; không phải bằng chứng EP+BVA-vs-random cùng budget. Cụ thể phương pháp, số liệu và giới hạn ở rq-proximity.md.
- RESTest có equal test counts nhưng intervention không EP+BVA; DB scripts có robust BVA nhưng thực nghiệm chỉ đếm cases, không API mutant/coverage. Không ép Include để tăng số bài; giữ metric đúng bản chất và quyết định từng record ở screening-overrides/ledger.
- MADS có EP+BVA/REST và coverage trong abstract nhưng PDF được publisher ghi Ukrainian nên loại IC-L; không lấy ngôn ngữ English của trang web làm ngôn ngữ bài. Bài Reid1997 về EP/BVA/random nằm ngoài IC-Y, không nới năm ngầm.
- Chưa xác minh bài đáp ứng đủ EP+BVA + uniform random + equal request budget + unique oracle-confirmed mutants. Không kết luận rằng toàn bộ literature không có; đây là phạm vi query/trang đã thu ở bảng trên.
- Agentic tra mới arXiv/Crossref20/OpenAlex HTTP200; chưa journal_ref/article DOI, vẫn preprint. Giữ Unsure IC-T; audit/round7/publication-verification.json.
- Snowballing không có iteration mới: vẫn84lùi+7tiến=91lượt;64canonical trong nhánh;overlap1;63bài mới so với search. Search/seed hiện61unique; **61+63=124**.28lượt mới là supplementary search, không snowball, không cộng vào primary IEEE/ACM/OpenAlex PRISMA của nhóm.

## Đợt 8 — lịch sử: lấy lại bốn toàn văn

# Kết quả đợt 8 — 15/10/2026

- Tìm lại đúng 4 bài thiếu; không thêm discovery hay snowball occurrence.
- TD-0133: tải PDF publisher 13 trang qua Download của OJS; backend parse và kiểm title thành công. Sửa venue từ nguồn thứ cấp sang SEMNASIF2021. Nội dung chính Bahasa Indonesia: EXCLUDE V2 IC-L; giữ V1 và lịch sử sought.
- TD-0135: toàn văn text công khai do publisher cung cấp trên ResearchGate, 14 trang xuất bản, DOI10.4018/IJSSMET.399173. Lưu liên tục lines61-1037 và hash; PDF chưa tải được. EXCLUDE V2 IC-P (thực nghiệm mobile functions/GUI, không HTTP request NL+schema).
- TD-0137: toàn văn text tác giả/publisher công khai trên ResearchGate, 17 trang xuất bản. Lưu liên tục lines73-2775 và hash; PDF chưa tải được. Có numeric-boundary request faults nên không đánh trượt IC-I thiếu căn cứ; EXCLUDE V2 IC-P vì chỉ formal interface, không NL+schema theo protocol cố định.
- TD-0136 FAMRES: IC-T xác nhận conference paper, published citation2026/first-online2025. Springer còn subscription preview; OpenAlex không OA; hai repo tác giả không có PDF/doc/tex. Chưa lấy được toàn văn, giữ UNSURE; không tự gán EC-A chỉ vì lỗi truy cập. Mã nguồn không thay cho toàn văn.
- Agentic TD-0006 giữ Unsure IC-T theo xác minh đợt7. Hai Include đề xuất vẫn PROPOSED, không có Include mới.

PRISMA hiện tại: raw157 − trùng33 = unique124; 124 − loạiV1 67 = sought57; 57 − chưa lấy1 = assessed56; 56 − loạiV2 53 − Unsure đã đọc1 = Include đề xuất2.
Toàn văn assessed =52 PDF +4 indexed text. Thiếu PDF binary5 gồm FAMRES và4 bài đã có text. Snowballing vẫn84 lùi+7 tiến=91lượt,64unique trong nhánh, giao search1, đóng góp mới63; search61+63=124.

Audit: plan.json/clinic-plan.json, source-responses.json, browser-pdfs.json, text-manifest.json, các web-captures và indexed-source, new-pdf-manifest.json, baseline4.json, retrieval-followup4.csv, screening-review.md. HTTP429 của Crossref mobile là truy vấn lỗi, không phải không có DOI. Không dùng reported hits/retry counts làm số bài mới.

## Đợt 9 — hiện tại: FAMRES và Agentic

# Đợt 9 — xác minh FAMRES và Agentic, 15/10/2026

- TD-0136 FAMRES: tìm thêm trang công trình của tác giả Trần Hoàng Việt. Citation đúng DOI nhưng chỉ link về Springer; không có bản thảo đính kèm. Publisher indexed page vẫn subscription preview, ResearchGate ghi no full-text. HTTP200 trực tiếp của Springer thực chất Client Challenge, không phải toàn văn. OpenAlex trả1location khôngOA/khôngPDF; S2 exactDOI404 chỉ là lookup không thành công. Đã chạy lại tool với publisher+author URLs; không tải được PDF đúng title. Giữ UNSURE/chờ full-text, EC-A chưa xác nhận; code/abstract không thay toàn văn.
- TD-0006 Agentic: arXiv API mới trảv1, updated2025-10-31, không journal_ref và articleDOI. OpenAlex ghi preprint/submittedVersion. Crossref exact titleHTTP429: truy vấn lỗi, không ghi no match. Tìm alternate title+Besjes trả13 bài physics ATLAS không liên quan, không đủ loại trừ khả năng đổi tên khi xuất bản. DBLP XMLHTTP202/HTMLchallenge không coi là XML đã kiểm; indexed author page riêng ghi CoRR. DOI Zenodo dataset và paper tiền nhiệm khác tên không xác minh IC-T cho bài này. Giữ UNSURE IC-T.
- Không có PDF/toàn văn mới, không thêm discovery/snowballing, không đổi quyết định hai Include PROPOSED. Nội dung/nguồn cũ giữ nguyên, chỉ cập nhật lý do và audit xác minh.

PRISMA giữ:157−33=124;124−67=57;57−1=56;56−53−1=2. Trong57sought:52PDF+4indexedtext+1FAMRES chưa lấy; Agentic nằm trong56assessed nhưng Unsure. Snowballing84lùi+7tiến=91lượt;64unique trong nhánh, giao search1, đóng góp mới63; search61+63=124. Không cộng retry, API lookup hay trang tác giả vào lượt snowball mới.

Nguồn mới, raw responses và lỗi: source-responses.json, author-arxiv-web.txt, publisher-dblp-rg-web.txt, famres-author.html, publication-verification.json, famres-verification.json, plan.json. Bằng chứng trước đó ở audit/round7 và audit/round8 còn giữ; không thay thời điểm kiểm cũ bằng thời điểm mới.
