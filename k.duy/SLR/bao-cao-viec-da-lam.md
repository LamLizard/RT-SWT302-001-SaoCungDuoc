# Báo cáo công việc snowballing vòng 1 — FA26-EXT-12

**Người phụ trách:** K.Duy (RW)  
**Phạm vi:** Snowballing lùi và tiến từ sáu seed được nêu cho FA26-EXT-12. Chỉ rà tiêu đề để phân luồng candidate; chưa quyết định bài nào được include.  
**Ngày truy vấn theo raw response:** 05/10/2026 (UTC+07:00)

## Tóm tắt kết quả

- Semantic Scholar Graph API trả 198 record có tiêu đề; Crossref cung cấp 110 reference của seed SLR microservices. Tổng 308 lượt thấy có thể kiểm tra.
- Bỏ trùng theo DOI, hoặc tiêu đề chuẩn hóa + năm khi không có DOI, còn 276 bài duy nhất; 32 lượt thấy là trùng.
- Title-screen đưa 47 candidate vào [01_all_records.csv](./01_all_records.csv) và 229 mục bị loại vào [02_screened_out.csv](./02_screened_out.csv). 47 + 229 = 276.
- Chưa đọc toàn văn để hoàn tất IC/EC; không có bài nào được đánh dấu included. Sáu seed cũng cần nhóm xác nhận trạng thái screening trước khi snowballing được xem là chính thức.
- Lý do chạy sau hạn chưa được cung cấp; để K.Duy điền và chờ PL (Lam) xác nhận. Chưa chạy vòng 2, không push hoặc merge.

## Cách phân biệt bằng chứng và nhận định

| Nhãn | Nội dung |
|---|---|
| **Đã chạy thật** | Semantic Scholar references/citations, Crossref reference list và DOI/title lookups, một truy vấn Semantic Scholar lặp lại, Google Scholar title query. Raw response được lưu dưới `raw/`. |
| **Đọc từ nguồn metadata** | Tiêu đề, năm, DOI, venue và trang lấy từ Crossref hoặc OpenAlex DOI resolution khi nguồn trả được dữ liệu. OpenAlex được dùng để resolve DOI references của SLR; không dùng để suy ra danh sách citation còn thiếu. |
| **Suy luận title-screen** | Phân luồng candidate/loại theo tiêu đề và IC/EC. Đây không phải quyết định include và không xác nhận nội dung bài, experimental outcome, ngôn ngữ, tải full-text hoặc số trang nếu chưa có metadata. |
| **Cần người xác nhận** | Seed đã include hay chưa; các candidate “Unsure”; lý do chạy trễ; suitability theo IC-I, IC-E, IC-T và EC-N sau khi đọc abstract/full text. |

## Tiến độ theo 10 việc

### 1. Chạy lại citation search và lưu dữ liệu thô

- **Đã làm:** Truy vấn References và Citations cho sáu seed bằng Semantic Scholar Graph API. Các danh sách có dưới 100 kết quả được lấy từ `limit=100`, `offset=0`; không có trang kế tiếp cần lấy. Các lần thử cũ gặp 429 đã được thay bằng lượt truy vấn mới; lượt mới lưu được dữ liệu và không ghi lỗi thành 0.
- **Cách làm:** Lấy trường `title,year,externalIds,venue`; retry exponential backoff khi gặp 429/5xx; kiểm tra biến môi trường API key nhưng không có key được cấu hình hay lưu.
- **Kết quả/file:** Mỗi seed/hướng có raw JSON trong [raw/](./raw/). RESTestBench: 37 References, 1 Citation; Prompt-Based: 16/1; RESTOR: 42/1; SLR microservices: Semantic Scholar không trả References, Citations trả danh sách rỗng; Test Oracle Generation: References là `data:null`, Citations 11; SATORI: 82/7.
- **Vì sao phù hợp protocol:** Phân trang đầy đủ và lưu response cho phép kiểm lại nguồn; các seed đều là các bài được nêu cho đề tài EXT-12.
- **Giới hạn:** Semantic Scholar không cung cấp References của SLR microservices và publisher elide References của Test Oracle Generation. Với SLR, danh sách references được lấy từ Crossref (110 entries). `data:null` không được hiểu là không có references.

### 2. Bỏ trùng

- **Đã làm:** Gộp các lượt thấy theo DOI; khi không có DOI, dùng tiêu đề chuẩn hóa và năm. Bản preprint và bản Springer chính thức của cùng bài Test Amplification được gộp sau khi Crossref xác nhận tiêu đề.
- **Cách làm:** Chuẩn hóa chữ hoa/thường, dấu câu và khoảng trắng; đối chiếu DOI/tên bài xuyên các seed trước khi lập hai CSV.
- **Kết quả/file:** 308 lượt thấy có tiêu đề → 276 bài duy nhất, tức 32 lượt trùng.
- **Vì sao phù hợp protocol:** Bỏ trùng trước khi báo số candidate giúp tránh đếm một bài nhiều lần do nhiều seed.
- **Giới hạn:** Metadata của một số reference không có DOI hoặc venue; các mục đó vẫn được dedup theo title + year và được giữ trạng thái chưa xác minh.

### 3. Rà tiêu đề theo IC/EC

- **Đã làm:** Rà 276 tiêu đề; giữ tạm các bài có khả năng liên quan kiểm thử REST/web API từ 2020 trở đi, gồm test generation, input/constraint/fuzzing, oracle hoặc coverage. Loại các mục rõ ràng ngoài chủ đề, tài liệu API không phải nghiên cứu, UI/E2E và unit-test thư viện.
- **Cách làm:** Dùng các tiêu chí chính thức trong `team-synthesis/ie_criteria.md`: IC-Y, IC-P, IC-I, IC-T, IC-E và EC-O/EC-N. Title-screen không thay cho kiểm tra toàn văn.
- **Kết quả/file:** 47 candidate ở 01; 229 loại có lý do ở 02.
- **Vì sao phù hợp protocol:** Mục tiêu vòng hiện tại là không bỏ sót bài tiềm năng liên quan REST API testing/EP-BVA; tiêu chí IC-I, IC-E và loại ấn phẩm cần kiểm tra tiếp.
- **Giới hạn:** Chưa xác minh nội dung EP/BVA thực sự được dùng; cũng chưa xác minh có kết quả thực nghiệm trong bảng/hình, full-text access, tiếng Anh hay số trang. Các survey, preprint và tool-paper vẫn là candidate/Unsure khi tiêu đề chưa đủ căn cứ loại.

### 4. Tạo danh sách screened-out

- **Đã làm:** Ghi tất cả 229 mục bị loại sau dedup vào [02_screened_out.csv](./02_screened_out.csv), mỗi dòng có `rejection_reason`.
- **Cách làm:** Lý do nêu mã tiêu chí có thể áp dụng, ví dụ IC-Y cho năm trước 2020, IC-P cho tiêu đề không chỉ ra REST/web API request testing, EC-O cho UI/E2E hoặc unit testing thư viện, và EC-N/IC-T cho tài liệu không phải nghiên cứu.
- **Kết quả/file:** 229 dòng; không có dòng nào thiếu lý do loại.
- **Vì sao phù hợp protocol:** Bảo toàn dấu vết loại để người screening có thể kiểm tra thay vì làm mất các mục không được giữ.
- **Giới hạn:** Một số reference không DOI/venue chỉ có citation string; lý do dựa trên tiêu đề, không khẳng định đã thẩm định toàn văn.

### 5. Cập nhật danh sách candidate và metadata

- **Đã làm:** Giữ nguyên mã SB-001 đến SB-008; bổ sung candidate mới theo thứ tự SB tiếp theo. Không đánh dấu record nào included.
- **Cách làm:** Tra Crossref trực tiếp theo DOI cho các candidate có DOI; dùng OpenAlex để resolve DOI trong 110 references của SLR; tra Crossref theo tiêu đề cho tám trường hợp còn thiếu/không rõ venue.
- **Kết quả/file:** [01_all_records.csv](./01_all_records.csv) có 47 dòng. SB-001 được sửa 2025 → 2026, ICSE 2026 proceedings, pp. 24–28 theo DOI 10.1145/3774748.3787598. SB-007 được xác nhận 2025, ICSE 2025, pp. 1409–1421. QuickREST được xác nhận năm xuất bản 2020 (ICST, pp. 131–141), không dùng năm preprint 2019. Bản Test Amplification chính thức được ghi DOI Springer và giữ arXiv DOI làm định danh thay thế. SB-003 vẫn là arXiv 2024; chưa xác nhận được venue chính thức.
- **Vì sao phù hợp protocol:** DOI/year/venue được sửa chỉ khi có nguồn metadata và được ghi giải thích trong log.
- **Giới hạn:** Crossref trả 404 cho năm arXiv DOI; đây không chứng minh bài không tồn tại hay không có phiên bản chính thức. RESTCov, Independent Test Generation, DualMine và một số title khác chưa có venue/DOI xác minh được; đã ghi “Not verified”.

### 6. Khôi phục search log đúng template

- **Đã làm:** Cập nhật [search-log.md](./search-log.md), giữ đủ cột của `search-log-template.md` và thêm bảng snowballing theo đúng sáu cột: seed DOI, vòng, hướng, số đã lướt, số thêm vào 01, số include cuối.
- **Cách làm:** Ghi URL/query, CSDL, trường tìm, limit/offset, ngày, số trả về, dedup và ghi chú cho truy vấn mới; `Số thêm vào 01` gán mỗi candidate một lần theo nguồn xuất hiện đầu tiên. Seed/hướng phụ được liệt kê trong CSV để giữ provenance.
- **Kết quả/file:** Log thể hiện tổng 308 → 276 → 47 + 229. Cột “Số include cuối” ghi “Chưa screening”.
- **Vì sao phù hợp protocol:** Giữ khả năng tái lập và không biến kết quả snowballing thành kết luận screening.
- **Giới hạn:** Số Google Scholar Cited by chưa xác minh được; HTML fetch bị công cụ cắt trước phần kết quả.

### 7. Kiểm chứng metadata, truy vấn lặp và số dòng

- **Đã làm:** Đối chiếu năm bản ghi SB-001, SB-002, SB-004, SB-005 và SB-007 với Crossref; chạy lại một truy vấn Semantic Scholar; kiểm tra số dòng và mã CSV.
- **Cách làm:** So sánh title/year/DOI và venue/pages; lặp lại RESTestBench References với cùng `limit=100`, `offset=0`.
- **Kết quả/file:** Năm đối chiếu và phép lặp 37/37 được ghi trong mục Kiểm chứng của [search-log.md](./search-log.md). CSV arithmetic: 47 + 229 = 276; mã candidate không trùng; mọi 02 có lý do; không có status included.
- **Vì sao phù hợp protocol:** Đây là các kiểm tra định lượng trực tiếp trên dữ liệu và metadata đã thu.
- **Giới hạn:** Kiểm tra truy vấn lặp chứng minh số trả về ổn định ở thời điểm lặp, không chứng minh chỉ mục không thay đổi theo thời gian. Google Scholar không cung cấp số citation xác minh được trong nội dung nhận về.

### 8. Ghi thay đổi protocol và hạn

- **Đã làm:** Ghi protocol cutoff 23:59 ngày 04/10/2026 và ngày truy vấn thực tế 05/10/2026; ghi các thay đổi metadata có nguồn.
- **Cách làm:** Không tự điền lý do trễ khi lý do chưa được K.Duy cung cấp; yêu cầu K.Duy bổ sung và PL (Lam) xác nhận.
- **Kết quả/file:** Các điểm này nằm ở “Thay đổi so với protocol” trong [search-log.md](./search-log.md).
- **Vì sao phù hợp protocol:** Tránh tạo lý do hoặc thay đổi metadata không có bằng chứng.
- **Giới hạn/cần người quyết định:** K.Duy phải ghi lý do thật; Lam cần xác nhận xử lý lượt chạy sau cutoff.

### 9. Ghi chú vòng 2

- **Đã làm:** Chỉ ghi điều kiện/kế hoạch; chưa chạy vòng 2.
- **Cách làm:** Chờ nhóm xác nhận seed đã include, sau đó chọn seed có nội dung request parameter, EP/BVA/input constraint/boundary và outcome mutant/coverage phù hợp.
- **Kết quả/file:** Ghi chú trong `search-log.md`.
- **Vì sao phù hợp protocol:** Seed cho snowballing chính thức phải đến từ bài đã include.
- **Giới hạn/cần người quyết định:** Nhóm screening phải xác nhận seed trước; 47 dòng ở 01 hiện chỉ là candidate.

### 10. Version control

- **Đã làm:** Chuẩn bị các thay đổi chỉ trong `k.duy/SLR/`; không sửa `team-synthesis/`, `notes.md` hay thư mục thành viên khác trong lượt cập nhật này.
- **Cách làm:** Raw hiện khoảng 0.8 MB và chỉ chứa response metadata/citation công khai, không chứa API key; có thể commit cùng evidence để tái lập. Các commit cần chỉ định rõ file trong `k.duy/SLR/` để không kéo theo thay đổi staged ngoài phạm vi.
- **Kết quả/file:** `raw/`, hai CSV, `search-log.md` và báo cáo này là các file thuộc phạm vi. Commit/push status sẽ được báo riêng sau khi commit xong.
- **Vì sao phù hợp protocol:** Người dùng yêu cầu không push/merge và không commit thay đổi ngoài `k.duy/SLR/`.
- **Giới hạn:** Chưa push; staged thay đổi bên ngoài `k.duy/SLR/` phải được giữ nguyên và không đưa vào commit.

## Trước và sau

| Vấn đề | Trước lượt cập nhật | Sau lượt cập nhật |
|---|---|---|
| Forward search | Có kết quả cũ chưa xác minh và truy vấn 429 | Chạy lại Semantic Scholar cho cả sáu seed; kết quả mới được lưu; Google Scholar Cited by vẫn chưa xác minh |
| Backward search | Thiếu lần chạy, nguồn SLR chưa rà | Có 37/16/42/82 S2 references; SLR microservices rà đủ 110 Crossref references; Test Oracle `data:null` được ghi rõ |
| Mất dấu vết bị loại | Danh sách nhỏ, chưa có đầy đủ mục loại | 229 unique title-screen exclusions có rejection_reason |
| Bỏ trùng/số tổng | Số cũ ước tính chưa ổn định | 308 sightings, 32 trùng, 276 unique; số dòng 01+02 khớp |
| Metadata | SB-001 năm/venue chưa chính xác; một số venue còn mơ hồ | SB-001 sửa sang năm 2026 và pages; SB-007 được xác minh venue/pages; các chưa rõ ghi Not verified |
| Search log | Bảng không đủ cột và trạng thái dữ liệu chưa nhất quán | Khôi phục template, ghi query/source/count và snowballing table |
| Hạn, screening, vòng sau | Chưa ghi rõ lý do trễ; candidate có thể bị hiểu nhầm là include | Lý do trễ để K.Duy cung cấp; tất cả vẫn Candidate/Chưa screening; vòng 2 chưa chạy |

## Sơ đồ luồng bằng số liệu hiện có

```text
Semantic Scholar result rows (198)
            + Crossref SLR references (110)
            = 308 lượt thấy có tiêu đề
            - 32 lượt trùng theo DOI / title-year
            = 276 bài duy nhất
               ├── 47 candidate -> 01_all_records.csv
               └── 229 loại     -> 02_screened_out.csv

Included cuối cùng: chưa xác định; chờ screening của nhóm.
```

## Tóm tắt trình bày với nhóm/giảng viên

1. Em đã chạy citation search lùi và tiến cho sáu seed EXT-12 bằng Semantic Scholar; với seed SLR microservices, em lấy danh sách 110 references từ Crossref do Semantic Scholar không trả references.
2. Tổng lượt thấy có tiêu đề là 308; sau bỏ trùng theo DOI hoặc title-year còn 276 bài duy nhất.
3. Title-screen tạm thời giữ 47 candidate và ghi đủ 229 mục bị loại cùng lý do; đây chưa phải kết quả include cuối.
4. Em đã xác minh metadata Crossref cho năm bản ghi, sửa SB-001 thành 2026 và chạy lặp RESTestBench References được cùng kết quả 37.
5. Cần nhóm xác nhận seed/candidate, K.Duy bổ sung lý do chạy sau cutoff 04/10, Lam xác nhận thay đổi hạn; chưa chạy vòng 2.

## Câu hỏi có thể nhận được

**Vì sao 308 lượt thấy nhưng 276 bài duy nhất?**  
Có 32 lượt trùng giữa nguồn/seed; DOI được ưu tiên, còn bản không DOI được so bằng tiêu đề chuẩn hóa và năm. Một preprint và bản xuất bản cùng bài được gộp sau khi đối chiếu Crossref.

**47 bài trong 01 đã được include chưa?**  
Chưa. Chúng chỉ qua title-screen sơ bộ; abstract/full text và screening theo IC/EC của nhóm vẫn cần thực hiện.

**Có bao nhiêu citation từ Google Scholar cho Prompt-Based?**  
Chưa xác minh. HTML truy xuất bị cắt trước vùng kết quả, nên không báo số; Semantic Scholar trả một citing-paper record.

**Vì sao Test Oracle Generation References không phải 0?**  
Semantic Scholar trả `data:null` và thông báo publisher đã ẩn references. Không có danh sách để đếm; đây là “chưa xác định”, không phải zero.

**Vòng 2 sẽ bắt đầu khi nào?**  
Sau khi nhóm chốt bài nào đã include và xác nhận seed hợp lệ; hiện chưa chạy vòng 2.

## Việc cần người quyết định

1. **K.Duy:** điền lý do thực tế vì sao lượt snowballing diễn ra ngày 05/10 thay vì cutoff 04/10.
2. **PL (Lam):** xác nhận xử lý việc vượt cutoff và metadata changes ghi trong log.
3. **Nhóm screening:** xác nhận sáu seed có qua screening không; sàng lọc abstract/full text 47 candidate, đặc biệt các preprint, survey, tool-paper và record chưa xác minh venue.
4. **Nhóm:** xác nhận candidate nào đáp ứng IC-I (EP/BVA/input-boundary) và IC-E (có kết quả thực nghiệm); sau đó mới chọn seed vòng 2.
