# Search log — K.Duy · phụ trách: Snowballing lùi + tiến

Ngày truy vấn được ghi trong raw response: 05/10/2026 (UTC+07:00). Đây là lượt thăm dò; seed và candidate chưa được nhóm xác nhận qua screening, vì vậy không được tính là included.

## Bảng log chính

| # | Query nguyên văn | CSDL | Trường tìm | Bộ lọc | Ngày | Số kết quả | Số sau bỏ trùng | Ghi chú |
|---|---|---|---|---|---|---:|---:|---|
| 1 | `https://api.semanticscholar.org/graph/v1/paper/DOI%3A10.48550%2FarXiv.2604.25862/references?fields=title,year,externalIds,venue&limit=100&offset=0` | Semantic Scholar Graph API | References: title, year, externalIds, venue | limit=100; offset=0 | 05/10/2026 | 37 | 37 | Lấy đủ trang; lưu `raw/restestbench_references.json`. |
| 2 | `https://api.semanticscholar.org/graph/v1/paper/DOI%3A10.48550%2FarXiv.2604.25862/citations?fields=title,year,externalIds,venue&limit=100&offset=0` | Semantic Scholar Graph API | Citations: title, year, externalIds, venue | limit=100; offset=0 | 05/10/2026 | 1 | 1 | Lưu `raw/restestbench_citations.json`. |
| 3 | `https://api.semanticscholar.org/graph/v1/paper/DOI%3A10.48550%2FarXiv.2601.17903/references?fields=title,year,externalIds,venue&limit=100&offset=0` | Semantic Scholar Graph API | References: title, year, externalIds, venue | limit=100; offset=0 | 05/10/2026 | 16 | 16 | Thay lượt OpenAlex trước; lưu `raw/prompt-based_references.json`. |
| 4 | `https://api.semanticscholar.org/graph/v1/paper/DOI%3A10.48550%2FarXiv.2601.17903/citations?fields=title,year,externalIds,venue&limit=100&offset=0` | Semantic Scholar Graph API | Citations: title, year, externalIds, venue | limit=100; offset=0 | 05/10/2026 | 1 | 1 | Lưu `raw/prompt-based_citations.json`; Google Scholar đối chiếu không thu được số Cited by (xem ghi chú dưới). |
| 5 | `https://api.semanticscholar.org/graph/v1/paper/DOI%3A10.1145%2F3832185/references?fields=title,year,externalIds,venue&limit=100&offset=0` | Semantic Scholar Graph API | References: title, year, externalIds, venue | limit=100; offset=0 | 05/10/2026 | 42 | 42 | Lưu `raw/restor_references.json`. |
| 6 | `https://api.semanticscholar.org/graph/v1/paper/DOI%3A10.1145%2F3832185/citations?fields=title,year,externalIds,venue&limit=100&offset=0` | Semantic Scholar Graph API | Citations: title, year, externalIds, venue | limit=100; offset=0 | 05/10/2026 | 1 | 1 | Lưu `raw/restor_citations.json`; lượt mới đã xác minh, thay trạng thái 429 trước đó. |
| 7 | `https://api.semanticscholar.org/graph/v1/paper/DOI%3A10.1134%2Fs0361768825700422/references?fields=title,year,externalIds,venue&limit=100&offset=0` | Semantic Scholar Graph API | References: title, year, externalIds, venue | limit=100; offset=0 | 05/10/2026 | Không có data | Không áp dụng | API không trả danh sách reference; không xem đây là 0 references. Dùng Crossref làm nguồn danh sách bên dưới. |
| 8 | `https://api.semanticscholar.org/graph/v1/paper/DOI%3A10.1134%2Fs0361768825700422/citations?fields=title,year,externalIds,venue&limit=100&offset=0` | Semantic Scholar Graph API | Citations: title, year, externalIds, venue | limit=100; offset=0 | 05/10/2026 | 0 | 0 | Response thành công nhưng danh sách `data` rỗng; lưu `raw/microservices-slr_citations.json`. |
| 9 | `https://api.crossref.org/works/10.1134/s0361768825700422` | Crossref | Reference list của DOI seed | Đọc đủ mảng `reference` trong work record | 05/10/2026 | 110 | 110 | Rà 110 tiêu đề; 101 DOI được resolve bằng OpenAlex. Dữ liệu gốc ở `raw/microservices-slr_crossref_work.json`, kết quả resolve ở `raw/microservices-slr_openalex_resolved.json`. |
| 10 | `https://api.semanticscholar.org/graph/v1/paper/DOI%3A10.1145%2F3726524/references?fields=title,year,externalIds,venue&limit=100&offset=0` | Semantic Scholar Graph API | References: title, year, externalIds, venue | limit=100; offset=0 | 05/10/2026 | Không enumerable | Không áp dụng | `data:null`; publisher elide references. Không ghi thành 0; chưa rà được references của seed này. |
| 11 | `https://api.semanticscholar.org/graph/v1/paper/DOI%3A10.1145%2F3726524/citations?fields=title,year,externalIds,venue&limit=100&offset=0` | Semantic Scholar Graph API | Citations: title, year, externalIds, venue | limit=100; offset=0 | 05/10/2026 | 11 | 11 | Lưu `raw/test-oracle_citations.json`. |
| 12 | `https://api.semanticscholar.org/graph/v1/paper/DOI%3A10.1109%2Fase63991.2025.00116/references?fields=title,year,externalIds,venue&limit=100&offset=0` | Semantic Scholar Graph API | References: title, year, externalIds, venue | limit=100; offset=0 | 05/10/2026 | 82 | 82 | Lưu `raw/satori_references.json`. |
| 13 | `https://api.semanticscholar.org/graph/v1/paper/DOI%3A10.1109%2Fase63991.2025.00116/citations?fields=title,year,externalIds,venue&limit=100&offset=0` | Semantic Scholar Graph API | Citations: title, year, externalIds, venue | limit=100; offset=0 | 05/10/2026 | 7 | 7 | Lưu `raw/satori_citations.json`; lượt mới đã xác minh. |
| 14 | `https://api.crossref.org/works/{doi}` cho 44 DOI ứng viên, từng DOI một | Crossref | Title, publication date, container title, page, type | DOI chính xác; 1 request/DOI | 05/10/2026 | 39 HTTP 200; 5 HTTP 404 | 39 record metadata | 5 DOI 404 đều là arXiv DOI. Toàn bộ DOI/query status trong `raw/candidate_metadata_crossref.json`; HTTP 404 không được diễn giải là bài không tồn tại. |
| 15 | `https://api.crossref.org/works/10.1109/icst46399.2020.00023` | Crossref | Metadata DOI của QuickREST | DOI chính xác | 05/10/2026 | 1 | 1 | Crossref xác nhận 2020, ICST, pp. 131–141; sửa năm thư mục suy ra từ năm preprint 2019. Raw ở `raw/metadata_10_1109_icst46399_2020_00023.json`. |
| 16 | `https://api.crossref.org/works/10.1007/978-3-032-05188-2_11` | Crossref | Metadata DOI của bản xuất bản Test Amplification | DOI chính xác | 05/10/2026 | 1 | 1 | Xác nhận năm 2025, LNCS / Testing Software and Systems, pp. 161–177; gắn với preprint cùng tiêu đề, không cộng thêm như một sighting. Raw ở `raw/metadata_10_1007_978_3_032_05188_2_11.json`. |
| 17 | Crossref `query.title` = `APITestGenie: Automated API Test Generation through Generative AI` | Crossref | Tra venue theo tiêu đề | 3 kết quả hàng đầu; kiểm tra đối sánh tiêu đề | 05/10/2026 | 3 kết quả trả về | Không có đối sánh tiêu đề chính xác | Chưa xác minh venue chính thức; giữ là preprint và đánh dấu rủi ro IC-T. |
| 18 | Crossref `query.title` = `Agentic LLMs for REST API Test Amplification: A Comparative Study Across Cloud Applications` | Crossref | Tra venue theo tiêu đề | 3 kết quả hàng đầu; kiểm tra đối sánh tiêu đề | 05/10/2026 | 3 kết quả trả về | Không có đối sánh tiêu đề chính xác | Venue chưa xác minh ngoài arXiv. |
| 19 | Crossref `query.title` = `Evaluating LLMs on Sequential API Call Through Automated Test Generation` | Crossref | Tra venue theo tiêu đề | 3 kết quả hàng đầu; kiểm tra đối sánh tiêu đề | 05/10/2026 | 3 kết quả trả về | Không có đối sánh tiêu đề chính xác | Venue chưa xác minh ngoài arXiv. |
| 20 | Crossref `query.title` = `Independent Test Generation for RESTful APIs` | Crossref | Tra venue theo tiêu đề | 3 kết quả hàng đầu; kiểm tra đối sánh tiêu đề | 05/10/2026 | 3 kết quả trả về | Không có đối sánh tiêu đề chính xác | Chưa xác minh DOI/venue; giữ làm candidate vì tiêu đề gần RQ. |
| 21 | Crossref `query.title` = `RESTCov: A Tool for Measuring Structural REST API Coverage` | Crossref | Tra venue theo tiêu đề | 3 kết quả hàng đầu; kiểm tra đối sánh tiêu đề | 05/10/2026 | 3 kết quả trả về | Không có đối sánh tiêu đề chính xác | Venue/DOI chưa xác minh; giữ candidate để nhóm kiểm tra loại ấn phẩm và IC-T. |
| 22 | Crossref `query.title` = `RESTCov: A Tool for Structural Coverage Analysis of REST APIs` | Crossref | Tra venue theo tiêu đề | 3 kết quả hàng đầu; kiểm tra đối sánh tiêu đề | 05/10/2026 | 3 kết quả trả về | Không có đối sánh tiêu đề chính xác | Venue/DOI chưa xác minh; giữ candidate để nhóm kiểm tra loại ấn phẩm và IC-T. |
| 23 | Crossref `query.title` = `Test Amplification for REST APIs via Single and Multi-Agent LLM Systems` | Crossref | Tra venue theo tiêu đề | 3 kết quả hàng đầu; kiểm tra đối sánh tiêu đề | 05/10/2026 | 3 kết quả trả về | 1 đối sánh tiêu đề chính xác | Bản xuất bản DOI 10.1007/978-3-032-05188-2_11 được xác minh; chỉ tính một bài sau dedup. |
| 24 | Crossref `query.title` = `MASTOR: A Multi-Agent Approach to Semantic Test Oracle Generation for RESTful APIs` | Crossref | Tra venue theo tiêu đề | 3 kết quả hàng đầu; kiểm tra đối sánh tiêu đề | 05/10/2026 | 3 kết quả trả về | Không có đối sánh tiêu đề chính xác | Chưa xác minh venue ngoài arXiv. |
| 25 | `https://api.semanticscholar.org/graph/v1/paper/DOI%3A10.48550%2FarXiv.2604.25862/references?fields=title,year,externalIds,venue&limit=100&offset=0` (chạy lại) | Semantic Scholar Graph API | References: title, year, externalIds, venue | Cùng query, cùng limit/offset | 05/10/2026 | 37 | 37 | Lần trước 37; chạy lại 37. Raw response: `raw/verification_repeat_restestbench_references.json`. |
| 26 | `https://scholar.google.com/scholar?hl=en&q=%22Prompt-Based+REST+API+Test+Amplification+in+Industry%3A+An+Experience+Report%22&btnG=` | Google Scholar | Tìm tiêu đề seed / kiểm tra Cited by | Exact-title query | 05/10/2026 | Không xác minh được | Không áp dụng | HTML được fetch nhưng công cụ cắt ở 10 KB trước phần kết quả; không có số Cited by đáng tin cậy. Không kết luận là 0. |

## Tổng hợp

- Semantic Scholar trả 198 result rows có tiêu đề; Crossref trả 110 reference entries của seed SLR microservices. Tổng lượt thấy có thể kiểm chứng bằng tiêu đề: **308**.
- Bỏ trùng theo DOI; khi một bản không có DOI thì dùng tiêu đề chuẩn hóa + năm. Ghép DOI preprint và DOI bản xuất bản khi Crossref xác nhận cùng tiêu đề: **32 sighting trùng**, còn **276 bài duy nhất**.
- Sau title-screen: **47 candidate vào `01_all_records.csv`**, **229 mục vào `02_screened_out.csv`**; 47 + 229 = 276. Đây không phải số bài include cuối.
- Có 2 truy vấn References không thể kiểm đếm thành danh sách: SLR seed References từ Semantic Scholar không có data (đã thay bằng Crossref references); Test Oracle References là `data:null` do publisher elide. Cả hai không được tính là zero references. SLR Citations là response thành công với danh sách rỗng.
- Các cột “Số thêm vào 01” dưới đây gán mỗi candidate đúng một lần theo nguồn/seed xuất hiện đầu tiên; provenance bổ sung vẫn được ghi trong CSV. Tổng các cột này = 47.

## Snowballing

| Seed (DOI) | Vòng | Hướng (lùi/tiến) | Số đã lướt | Số thêm vào 01 | Số include cuối |
|---|---:|---|---:|---:|---|
| 10.48550/arXiv.2604.25862 | 1 | Lùi (Semantic Scholar) | 37 | 8 | Chưa screening |
| 10.48550/arXiv.2604.25862 | 1 | Tiến (Semantic Scholar) | 1 | 1 | Chưa screening |
| 10.48550/arXiv.2601.17903 | 1 | Lùi (Semantic Scholar) | 16 | 4 | Chưa screening |
| 10.48550/arXiv.2601.17903 | 1 | Tiến (Semantic Scholar) | 1 | 1 | Chưa screening |
| 10.1145/3832185 | 1 | Lùi (Semantic Scholar) | 42 | 4 | Chưa screening |
| 10.1145/3832185 | 1 | Tiến (Semantic Scholar) | 1 | 1 | Chưa screening |
| 10.1134/s0361768825700422 | 1 | Lùi (Crossref reference list) | 110 | 1 | Chưa screening |
| 10.1134/s0361768825700422 | 1 | Tiến (Semantic Scholar) | 0 title; response rỗng | 0 | Chưa screening |
| 10.1145/3726524 | 1 | Lùi (Semantic Scholar) | Chưa xác định (`data:null`) | Chưa xác định | Chưa screening |
| 10.1145/3726524 | 1 | Tiến (Semantic Scholar) | 11 | 6 | Chưa screening |
| 10.1109/ase63991.2025.00116 | 1 | Lùi (Semantic Scholar) | 82 | 19 | Chưa screening |
| 10.1109/ase63991.2025.00116 | 1 | Tiến (Semantic Scholar) | 7 | 2 | Chưa screening |

## Kiểm chứng

### Năm bản ghi đối chiếu Crossref

| Record | Tiêu đề khớp | Năm | DOI | Venue / trang | Kết quả |
|---|---|---:|---|---|---|
| SB-001 | RESTifAI: LLM-Based Workflow for Reusable REST API Testing | 2026 | 10.1145/3774748.3787598 | ICSE 2026 proceedings, pp. 24–28 | Khớp; năm cũ 2025 đã sửa theo Crossref. |
| SB-002 | Combining TSL and LLM to Automate REST API Testing: A Comparative Study | 2025 | 10.5753/sbes.2025.9670 | SBES 2025, pp. 71–81 | Khớp. |
| SB-004 | AGORA: Automated Generation of Test Oracles for REST APIs | 2023 | 10.1145/3597926.3598114 | ISSTA 2023, pp. 1018–1030 | Khớp. |
| SB-005 | RESTest: automated black-box testing of RESTful web APIs | 2021 | 10.1145/3460319.3469082 | ISSTA 2021, pp. 682–685 | Khớp. |
| SB-007 | A Multi-Agent Approach for REST API Testing with Semantic Graphs and LLM-Driven Inputs | 2025 | 10.1109/ICSE55347.2025.00179 | ICSE 2025, pp. 1409–1421 | Khớp; venue/trang được bổ sung. |

- Repeat query: RESTestBench References trả 37 ở lượt gốc và 37 khi chạy lại (limit=100, offset=0).
- CSV arithmetic: 47 dòng dữ liệu trong 01 + 229 dòng trong 02 = 276 unique. Mã candidate không trùng; mọi dòng 02 có `rejection_reason`; không record nào được đánh dấu included.
- Thử Google Scholar không cho số Cited by: kết quả HTML nhận được bị cắt trước nội dung danh sách. Số forward Prompt-Based được báo cáo theo Semantic Scholar (1), không suy ra từ Google Scholar.
- Lượt gọi mới nhất không gặp 429. Các 429 ở lượt cũ đã được thay bằng kết quả mới; Test Oracle References `data:null` và SLR References thiếu data vẫn được ghi là chưa có dữ liệu, không chuyển thành 0.

## Thay đổi so với protocol

- Protocol ghi dừng search lúc 23:59 ngày 04/10/2026; raw response ghi nhận truy vấn ngày 05/10/2026. Lý do chạy trễ chưa được K.Duy cung cấp nên để trống chờ K.Duy ghi lý do thật; cần PL (Lam) xác nhận. Không tự suy đoán lý do.
- SB-001 đổi năm 2025 → 2026 và bổ sung ICSE proceedings, pp. 24–28 theo Crossref DOI record. SB-007 được đối chiếu lại năm 2025, venue ICSE 2025 và pp. 1409–1421; năm không đổi.
- SB-003 vẫn là arXiv preprint (2024); truy vấn DOI Crossref trả 404 và tìm theo tiêu đề không cho đối sánh chính xác trong 3 kết quả đầu. Chưa kết luận không có bản xuất bản; cần nhóm xác minh IC-T.
- `Test Amplification for REST APIs via Single and Multi-Agent LLM Systems` được nối với bản Springer chính thức DOI 10.1007/978-3-032-05188-2_11 (2025, pp. 161–177); arXiv DOI được giữ làm định danh thay thế, không tính thành bài thứ hai.
- Mọi metadata sửa/chuẩn hóa được ghi kèm nguồn Crossref/OpenAlex; các venue/DOI chưa tra được vẫn ghi “Not verified”, không đoán.

## Ghi chú vòng 2

Chưa chạy vòng 2. Chỉ sau khi nhóm xác nhận bài nào trong 01 đã được include, chọn trong số đó các seed phủ trực tiếp EP/BVA, input/constraint/boundary và mutant/coverage outcome; ưu tiên bài có nội dung request-parameter rõ ràng. Không tự dùng candidate hiện tại làm seed vòng 2 trước quyết định screening của nhóm.
