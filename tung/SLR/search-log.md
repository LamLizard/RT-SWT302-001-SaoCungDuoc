# Search log — Tùng · IEEE Xplore

Phiên ngày **03/10/2026**, múi giờ **Asia/Saigon (UTC+7)**. Bắt đầu 21:03:17; hạn phiên 21:23:17. Phạm vi: tìm paper và ghi log; chưa screening hoặc Evidence Table.

## Cách chạy và đọc số

- String A nguyên văn được chạy đầu tiên. IEEE Command Search mặc định là All Metadata; lượt này chỉ dùng audit.
- Các lượt chính gắn từng cụm từ với `Document Title`, `Abstract`, `Index Terms` rồi giữ nguyên quan hệ Boolean. `Index Terms` gồm Author Keywords, IEEE Terms và MeSH Terms theo [trợ giúp IEEE](https://ieeexplore.ieee.org/Xplorehelp/searching-ieee-xplore/command-search).
- Mục tiêu năm: từ 2020 đến thời điểm truy cập 03/10/2026. Với lượt 0 kết quả mọi năm, trang không hiện bộ lọc năm; số từ 2020 cũng là 0 theo quan hệ tập con, **không phải thao tác lọc năm đã được thực hiện**.
- “Số sau bỏ trùng” là số bản ghi duy nhất trong từng lượt; tổng hợp liên-query sẽ dùng DOI chuẩn hóa, rồi IEEE article number, rồi title chuẩn hóa + năm. Giữ toàn bộ Search IDs. Không gộp số lượt audit/rerun vào PRISMA.

## Bảng log chính

| # | Query nguyên văn đã gửi | CSDL | Trường tìm | Bộ lọc thực tế | Ngày | Số kết quả | Số sau bỏ trùng | Ghi chú |
|---|---|---|---|---|---|---:|---:|---|
| Q0 | `("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing") AND ("fault detection" OR "mutant detection" OR "bugs found")` | IEEE Xplore | All Metadata (mặc định) | Mọi năm; chưa áp dụng loại ấn phẩm; 2020+ là tập con rỗng suy ra | 03/10/2026 | 0 | 0 | String A nhập nguyên văn; lượt kiểm tra mặc định All Metadata, không tính bổ sung PRISMA. |
| Q1 | `("Document Title":"REST API testing" OR "Abstract":"REST API testing" OR "Index Terms":"REST API testing" OR "Document Title":"natural language requirement" OR "Abstract":"natural language requirement" OR "Index Terms":"natural language requirement" OR "Document Title":"RESTestBench" OR "Abstract":"RESTestBench" OR "Index Terms":"RESTestBench") AND ("Document Title":"equivalence partitioning" OR "Abstract":"equivalence partitioning" OR "Index Terms":"equivalence partitioning" OR "Document Title":"boundary-value analysis" OR "Abstract":"boundary-value analysis" OR "Index Terms":"boundary-value analysis" OR "Document Title":"boundary testing" OR "Abstract":"boundary testing" OR "Index Terms":"boundary testing") AND ("Document Title":"fault detection" OR "Abstract":"fault detection" OR "Index Terms":"fault detection" OR "Document Title":"mutant detection" OR "Abstract":"mutant detection" OR "Index Terms":"mutant detection" OR "Document Title":"bugs found" OR "Abstract":"bugs found" OR "Index Terms":"bugs found")` | IEEE Xplore | Document Title OR Abstract OR Index Terms | Mọi năm; chưa áp dụng loại ấn phẩm; 2020+ là tập con rỗng suy ra | 03/10/2026 | 0 | 0 | String A gắn trường theo cú pháp IEEE; không có kết quả mọi năm. |
| Q2 | `("Document Title":"REST API testing" OR "Abstract":"REST API testing" OR "Index Terms":"REST API testing" OR "Document Title":"natural language requirement" OR "Abstract":"natural language requirement" OR "Index Terms":"natural language requirement" OR "Document Title":"RESTestBench" OR "Abstract":"RESTestBench" OR "Index Terms":"RESTestBench") AND ("Document Title":"equivalence partitioning" OR "Abstract":"equivalence partitioning" OR "Index Terms":"equivalence partitioning" OR "Document Title":"boundary-value analysis" OR "Abstract":"boundary-value analysis" OR "Index Terms":"boundary-value analysis" OR "Document Title":"boundary testing" OR "Abstract":"boundary testing" OR "Index Terms":"boundary testing")` | IEEE Xplore | Document Title OR Abstract OR Index Terms | Mọi năm; chưa áp dụng loại ấn phẩm; 2020+ là tập con rỗng suy ra | 03/10/2026 | 0 | 0 | A bỏ khối O vì Q1 <20; không có kết quả mọi năm. |
| Q3 | `("Document Title":"REST API" OR "Abstract":"REST API" OR "Index Terms":"REST API" OR "Document Title":"RESTful API" OR "Abstract":"RESTful API" OR "Index Terms":"RESTful API" OR "Document Title":"web API" OR "Abstract":"web API" OR "Index Terms":"web API" OR "Document Title":"web service" OR "Abstract":"web service" OR "Index Terms":"web service") AND ("Document Title":"boundary value analysis" OR "Abstract":"boundary value analysis" OR "Index Terms":"boundary value analysis" OR "Document Title":"boundary value" OR "Abstract":"boundary value" OR "Index Terms":"boundary value" OR "Document Title":"boundary testing" OR "Abstract":"boundary testing" OR "Index Terms":"boundary testing" OR "Document Title":"equivalence partitioning" OR "Abstract":"equivalence partitioning" OR "Index Terms":"equivalence partitioning") AND ("Document Title":"mutation testing" OR "Abstract":"mutation testing" OR "Index Terms":"mutation testing" OR "Document Title":"mutants" OR "Abstract":"mutants" OR "Index Terms":"mutants" OR "Document Title":"mutation score" OR "Abstract":"mutation score" OR "Index Terms":"mutation score")` | IEEE Xplore | Document Title OR Abstract OR Index Terms | Mọi năm; chưa áp dụng loại ấn phẩm; 2020+ là tập con rỗng suy ra | 03/10/2026 | 0 | 0 | String B/C dự phòng của protocol, bổ sung các từ đồng nghĩa; không có kết quả mọi năm. |
| Q4a | `("Document Title":"REST API" OR "Abstract":"REST API" OR "Index Terms":"REST API" OR "Document Title":"RESTful API" OR "Abstract":"RESTful API" OR "Index Terms":"RESTful API" OR "Document Title":"web API" OR "Abstract":"web API" OR "Index Terms":"web API" OR "Document Title":"web service" OR "Abstract":"web service" OR "Index Terms":"web service") AND ("Document Title":"boundary value analysis" OR "Abstract":"boundary value analysis" OR "Index Terms":"boundary value analysis" OR "Document Title":"boundary value" OR "Abstract":"boundary value" OR "Index Terms":"boundary value" OR "Document Title":"boundary testing" OR "Abstract":"boundary testing" OR "Index Terms":"boundary testing" OR "Document Title":"equivalence partitioning" OR "Abstract":"equivalence partitioning" OR "Index Terms":"equivalence partitioning")` | IEEE Xplore | Document Title OR Abstract OR Index Terms | Mọi năm (audit trước lọc năm) | 03/10/2026 | 14 | 14 | B bỏ khối O vì Q3 <20; đủ 14 article numbers khác nhau trên 1 trang; 12 bài trước 2020. |
| Q4b | `("Document Title":"REST API" OR "Abstract":"REST API" OR "Index Terms":"REST API" OR "Document Title":"RESTful API" OR "Abstract":"RESTful API" OR "Index Terms":"RESTful API" OR "Document Title":"web API" OR "Abstract":"web API" OR "Index Terms":"web API" OR "Document Title":"web service" OR "Abstract":"web service" OR "Index Terms":"web service") AND ("Document Title":"boundary value analysis" OR "Abstract":"boundary value analysis" OR "Index Terms":"boundary value analysis" OR "Document Title":"boundary value" OR "Abstract":"boundary value" OR "Index Terms":"boundary value" OR "Document Title":"boundary testing" OR "Abstract":"boundary testing" OR "Index Terms":"boundary testing" OR "Document Title":"equivalence partitioning" OR "Abstract":"equivalence partitioning" OR "Index Terms":"equivalence partitioning")` | IEEE Xplore | Document Title OR Abstract OR Index Terms | Year 2020–2025 do IEEE tự chặn cận trên về năm lớn nhất của tập kết quả; All Results; không lọc loại ấn phẩm | 03/10/2026 | 2 | 2 | Đã nhập 2020–2026; URL và Filters Applied xác nhận 2020–2025. Tập Q4a không có bài 2026, nên hai bản ghi là toàn bộ tập 2020+ hiện quan sát. |
| Q4c | `("Document Title":"REST API" OR "Abstract":"REST API" OR "Index Terms":"REST API" OR "Document Title":"RESTful API" OR "Abstract":"RESTful API" OR "Index Terms":"RESTful API" OR "Document Title":"web API" OR "Abstract":"web API" OR "Index Terms":"web API" OR "Document Title":"web service" OR "Abstract":"web service" OR "Index Terms":"web service") AND ("Document Title":"boundary value analysis" OR "Abstract":"boundary value analysis" OR "Index Terms":"boundary value analysis" OR "Document Title":"boundary value" OR "Abstract":"boundary value" OR "Index Terms":"boundary value" OR "Document Title":"boundary testing" OR "Abstract":"boundary testing" OR "Index Terms":"boundary testing" OR "Document Title":"equivalence partitioning" OR "Abstract":"equivalence partitioning" OR "Index Terms":"equivalence partitioning")` | IEEE Xplore | Document Title OR Abstract OR Index Terms | Rerun đúng URL Q4b; Year 2020–2025; All Results | 03/10/2026 | 2 | 2 | Hai title và số lượng không đổi; không cộng lần nữa vào PRISMA. |

## Tổng hợp phiên search 03/10/2026

- Q0: audit phạm vi rộng, 0 records.
- Q1–Q3: 0 records trước dedup và 0 sau dedup.
- Q4a: 14 bài mọi năm, chỉ audit; không cộng 14 vào PRISMA 2020+.
- Q4b: **2 trước dedup, 2 sau dedup (= 2 dòng 01_all_records.csv)**; DOI và article number khác nhau, 0 bản ghi trùng nội bộ.
- Q4c rerun 2: không cộng thêm; Q0 và Q4a là audit. Chưa dedup với các nguồn khác của nhóm.
- Tại cuối phiên search 03/10 chưa screening. Cập nhật 04/10: hai bài V2 Include ở bản AI; snowballing nhóm do K.Duy phụ trách.

## Thay đổi / ánh xạ so với protocol

- 03/10/2026: giữ String A nguyên văn ở Q0 và bổ sung field qualifiers ở Q1 để khớp Title/Abstract/Keywords. Không bỏ hoặc thêm khái niệm ở Q1.
- 03/10/2026: Q2 bỏ khối O theo quy tắc <20.
- 03/10/2026: Q3 dùng B/C dự phòng đã có trong protocol do Q2 vẫn <20.
- 03/10/2026: dùng Index Terms làm Keywords; xem [decisions-for-review.md](../decisions-for-review.md) để nhóm duyệt ánh xạ.

## Kiểm chứng

- Kết quả được đọc trực tiếp từ UI IEEE sau khi hết trạng thái Getting results; không dùng số ước lượng từ Google/Bing.
- Trợ giúp IEEE qua web fetch báo HTTP 418; cùng trang đọc được trong trình duyệt. Không dùng lỗi fetch làm kết quả tìm.
- Không dùng crawler/API tự viết, không dùng dữ liệu fixture/DEMO.

## Hồ sơ bàn giao

- Danh sách 2 records: [01_all_records.csv](01_all_records.csv); quyết định V1: [02_after_screening_v1.csv](02_after_screening_v1.csv).
- Kết quả V2 Include: [03_final_included.csv](03_final_included.csv); bằng chứng: [evidence-table.md](evidence-table.md); số đếm: [prisma-flow.md](prisma-flow.md). Screening/extraction đã làm ngày 04/10; còn chờ nhóm kiểm chéo.

## Cập nhật 04/10/2026 — screening và bàn giao

- Đã xử lý tuần tự metadata, V1, full-text/V2, extraction, appraisal/AI đối chiếu và handoff trên đúng 2 records gốc. Không chạy thêm query IEEE hoặc cộng thêm records từ web/Crossref/kho tác giả/Figshare.
- Bảng chính đã bỏ hai dòng trống tách Q4a/Q4c; nguyên văn query, bộ lọc và counts của 7 lượt giữ nguyên.
- Bản AI: V1 Include 2; reports retrieved/assessed 2; V2 Include 2, Exclude 0, Unsure 0. Cả hai Near_RQ = Indirect; reviewer nhóm và dedup liên nguồn còn chờ.
- IC-T002 và cách áp dụng IC-P đã được Tùng chấp nhận trong phiên04/10; chi tiết tại [decisions-for-review.md](../decisions-for-review.md). Keywords cuối của002 chưa xác minh; không lấy từ preprint.
- Nguồn current metadata/full-text được thu ngày04/10, không gọi là native export hay snapshot gốc03/10. Tổng identified trước/sau dedup nội bộ vẫn2/2; xem [ieee-handoff.md](../ieee-handoff.md).

## Đóng gói bộ nộp — 05/10/2026

- Chuẩn hóa từ dữ liệu hiện có; không chạy query mới và không thay đổi query, ngày chạy, bộ lọc hoặc số kết quả.
- Bộ nộp gồm 3 CSV và 3 Markdown trong thư mục này. Các CSV dùng Record_ID thống nhất, UTF-8 BOM, một hàng cho mỗi bài; bỏ 5 hàng rỗng và cột không tên của bản screening gốc.
- Abstract/keywords gốc trong 01 được giữ nguyên nhãn Paraphrase/Unverified. Nguồn xác minh và Metadata_Status nằm trong 02; bài 002 vẫn Partial.

