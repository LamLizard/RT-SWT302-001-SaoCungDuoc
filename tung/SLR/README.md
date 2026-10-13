# Bộ SLR đã đối chiếu và hợp nhất — 13/10/2026

Nhóm SaoCungDuoc · RQ FA26-EXT-12 · ngày dừng của bản hợp nhất: **13/10/2026 (UTC+7)**.

**Trạng thái: DOSSIER_INCOMPLETE.** Bản này đồng bộ định danh, provenance, metadata và quyết định giữa tool lọc bài với tool snowball. Có **4 bài INCLUDE hiện hành**; vẫn còn 37 bài snowball chưa lọc, 5 REVIEW cần chốt, 46 nhãn không lấy được full-text chưa có audit truy cập độc lập và coverage forward 12 tháng chưa xác minh. Không coi đây là tập SLR đã chốt.

## Các tập dữ liệu

| File | Dòng dữ liệu | Cách đọc |
|---|---:|---|
| [01_all_records.csv](01_all_records.csv) | 150 | Catalog duy nhất: 68 bài từ tool chính + 82 bài mới từ snowball. |
| [02_after_screening_v1.csv](02_after_screening_v1.csv) | 150 | Giữ toàn bộ catalog và route: 68 có quyết định V1, 45 snowball chuyển thẳng full-text, 37 snowball chưa được review. |
| [04_fulltext_screening.csv](04_fulltext_screening.csv) | 95 | Ledger kết quả sau V1 hoặc full-text trực tiếp; gồm 46 reports chưa lấy được toàn văn và 49 reports thực sự đã đánh giá toàn văn. |
| [03_final_included.csv](03_final_included.csv) | 4 | Chỉ 4 quyết định INCLUDE hiện hành; không chứa EXCLUDE hoặc REVIEW. |
| [03_included_only.csv](extras/03_included_only.csv) | 4 | Bản sao tập INCLUDE để đối chiếu công cụ. |
| [matching-crosswalk.csv](extras/matching-crosswalk.csv) | 150 | Nối ID chính với alias K của ledger snowball và alias P của screening PDF. |
| [origins.csv](extras/origins.csv) | 289 | Provenance của các lượt xuất hiện và quan hệ seed/direction đã hợp nhất. |
| [screening-history.csv](extras/screening-history.csv) | 335 | Lưu lịch sử export và các quyết định đối chiếu; xem ledger hiện hành khi xác định kết quả cuối. |

68 bài tool chính có V1: **18 EXCLUDE + 1 INCLUDE + 49 UNSURE**. 45 PDF snowball được đánh giá trực tiếp ở full-text; không ghi nhận một vòng title/abstract riêng chưa thực hiện. 95 outcomes gồm **86 EXCLUDE + 4 INCLUDE + 5 REVIEW**; 86 EXCLUDE gồm **46 chưa lấy được full-text + 40 loại sau khi đọc full-text**. 37 bài còn lại được giữ là chưa review.

Bốn bài INCLUDE:

| Bài | DOI | Alias snowball |
|---|---|---|
| A Black Box Tool for Robustness Testing of REST Services | `10.1109/access.2021.3056505` | K02 |
| Automated Test Generation for REST APIs: No Time to Rest Yet | `10.1145/3533767.3534401` | K81 / P12 |
| Enhancing REST API Testing with NLP Techniques | `10.1145/3597926.3598131` | K84 / P17 |
| TestGPT-Server: Automatically Testing Microservices with Large Language Models at ByteDance | `10.1145/3696630.3728545` | K108 / P38 |

INCLUDE được hiểu theo [IC/EC dùng chung của nhóm](extras/team-criteria-source.md): EP **và/hoặc** BVA trong kiểm thử REST request. Độ gần RQ/PICO được ghi riêng trong [evidence-table.md](evidence-table.md); INCLUDE không chứng minh một paper đã nghiên cứu đúng toàn bộ 45 yêu cầu RESTestBench, EP kết hợp BVA, random đồng ngân sách và unique mutants.

## Đối chiếu và truy vết

- [PRISMA](prisma-flow.md) phân biệt raw occurrences, catalog duy nhất, reports chưa lấy được và full-text thực sự đã đánh giá.
- [search-log.md](search-log.md) ghi nguồn, seed và giới hạn của discovery.
- [crosscheck.md](crosscheck.md) ghi kiểm tra tính nhất quán của file; đây không phải xác nhận kiểm chéo độc lập của nhóm.
- [matching-changes.md](matching-changes.md) ghi các thay đổi so với bản gốc.
- [course-checklist.md](extras/course-checklist.md) giữ các công việc chưa hoàn tất.
- [export-manifest.json](extras/export-manifest.json) mô tả snapshot hợp nhất hiện hành.

Các CSV và Markdown gốc được lưu tại [extras/original-export](extras/original-export). PDF đã đóng gói trong [paper](paper) và [snowballing/paper-snowball-2](snowballing/paper-snowball-2); các đường dẫn evidence của bản hợp nhất dùng đường dẫn tương đối. Bộ đếm toàn cục identified/duplicates của discovery vẫn chưa xác minh; **72 − 4 = 68** chỉ áp dụng cho các search đã truy được provenance, không cộng 99 snowball papers duy nhất với 72 search hits thô.
