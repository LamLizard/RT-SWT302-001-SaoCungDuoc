# PRISMA flow — bản hợp nhất 13/10/2026

Nhóm SaoCungDuoc · RQ FA26-EXT-12 · ngày dừng **13/10/2026 (UTC+7)** · **DOSSIER_INCOMPLETE**.

## Nhận diện và gộp record

| Phạm vi | Số lượng | Ý nghĩa |
|---|---:|---|
| Q1 — A đầy đủ | 0 | Search đã biết. |
| Q2 — A bỏ Outcome | 0 | Search đã biết. |
| Q3 — B/C bỏ Outcome | 2 | 2 bài mới. |
| Q4 — mở rộng biến thể EP/BVA | 2 | 2 bài đã có; 0 bài mới. |
| Q5 — mở rộng sinh/kiểm thử REST API | 68 | 66 bài mới. |
| Search hits truy được provenance | 72 lượt xuất hiện | 2 + 2 + 68. |
| Lượt lặp trong search đã biết | 4 | Hai DOI lặp giữa Q3/Q4/Q5. |
| Bài search duy nhất | 68 | 72 − 4. |
| Bài duy nhất có provenance snowball | 99 | 17 trùng tập search + 82 mới. |
| Catalog hợp nhất | 150 | 68 + 99 − 17 = 150. |
| Raw identified toàn hồ sơ | Chưa xác minh | Thiếu raw totals đã mất khi import. |
| Raw duplicates toàn hồ sơ | Chưa xác minh | 4 lượt lặp search và 17 bài overlap không đủ phục hồi tổng raw duplicates. |

Số **99** đếm paper snowball duy nhất trong ledger, không phải raw retrieval hits. Không cộng 99 với 72 rồi gọi kết quả là raw identified. Các record không có DOI được đối chiếu bằng metadata/crosswalk; DOI trống không tạo thành một nhóm duplicate.

12 PDF bổ sung đều khớp DOI/title với records IEEE đã có; chỉ bổ sung toàn văn và mở lại screening của 12 V1 exclusions. Tổng catalog và số nhận diện không đổi.

## Luồng screening hiện hành

```text
Catalog hợp nhất (150 papers)
├─ Tập từ tool chính: V1 screened (68)
│  ├─ EXCLUDE ở V1 (18)
│  │  ├─ Chỉ V1, chưa mở lại (6)
│  │  └─ Bổ sung PDF, mở lại full-text (12)
│  │     ├─ EXCLUDE sau full-text (11)
│  │     └─ INCLUDE (1: K52 / P53)
│  └─ INCLUDE V1 (1) + UNSURE V1 (49) → 50 reports cần full-text
│     ├─ Chưa lấy được full-text: nhãn EC-A import (46)
│     └─ Đã đánh giá full-text từ đợt trước (4)
│        ├─ EXCLUDE sau full-text (3)
│        └─ INCLUDE (1: bBOXRT)
└─ Snowball mới (82)
   ├─ Chuyển trực tiếp full-text, đã đánh giá (45)
   │  ├─ EXCLUDE sau full-text (37)
   │  ├─ INCLUDE (3)
   │  └─ REVIEW chưa chốt (5)
   └─ Chưa screening / chưa có quyết định full-text (37)

Ledger outcomes sau V1 hoặc full-text trực tiếp (107)
├─ Chưa lấy được full-text (46)
└─ Thực sự đã đánh giá full-text (61 = 4 + 12 + 45)
   ├─ EXCLUDE sau full-text (51 = 3 + 11 + 37)
   ├─ INCLUDE hiện hành (5 = 1 + 1 + 3)
   └─ REVIEW cần chốt (5)
```

Kiểm số học: **150 = 6 + 107 + 37**; **68 = 18 + 1 + 49** (V1 lịch sử); **18 = 6 + 12**; **107 = 46 + 61**; **61 = 51 + 5 + 5**; **107 = 97 EXCLUDE + 5 INCLUDE + 5 REVIEW**. Trong 97 EXCLUDE, chỉ 51 là quyết định loại sau khi đã đọc toàn văn; 46 còn lại là nhãn chưa lấy được full-text.

45 bài snowball có quyết định ở mức full-text trực tiếp. Không tính 45 bài này là đã qua một vòng title/abstract V1 độc lập. 37 bài snowball mới còn lại được giữ là chưa review, không tự chuyển sang EXCLUDE hoặc EC-A. 12 records V1 EXCLUDE được mở lại bằng PDF bổ sung, giữ V1 lịch sử và ghi quyết định V2; không tính là 12 paper snowball mới hoặc một vòng V1 mới.

## Tập giữ lại và REVIEW

| DOI / bài | Quyết định hiện hành | Ghi chú |
|---|---|---|
| `10.1109/access.2021.3056505` — bBOXRT | INCLUDE | BVA thực tế; INCLUDE từ tool chính. |
| `10.1109/tsc.2021.3050610` — K52 / P53 | INCLUDE | Bổ sung toàn văn; operational EP có suy luận từ lớp request hợp lệ/không hợp lệ và CSP chọn đại diện. Gần RQ HIGH_PARTIAL; chưa chứng minh BVA hoặc unique mutants. |
| `10.1145/3533767.3534401` — K81 / P12 | INCLUDE | Operational EP; quyết định từ full-text snowball. |
| `10.1145/3597926.3598131` — K84 / P17 | INCLUDE | EP qua công cụ và evidence đối chiếu; không khẳng định có BVA riêng. |
| `10.1145/3696630.3728545` — K108 / P38 | INCLUDE | EP được suy luận từ lớp đầu vào thực dùng; không khẳng định BVA hoặc kết quả riêng cho REST. |
| `10.1145/3540250.3549144` — K85 / P25 | REVIEW | Cần chốt IC-P / IC-I. |
| `10.1145/3765744` — K106 / P31 | REVIEW | Cần chốt cấu hình NL và EP/BVA. |
| `10.1145/3460319.3469082` — K133 / P32 | REVIEW | Cần xác nhận NL và cấu hình EP/BVA. |
| `10.1007/978-3-030-65310-1_33` — K77 / P33 | REVIEW | Cần xác nhận EP/BVA thực dùng. |
| `10.1145/3611643.3613888` — K95 / P39 | REVIEW | Cần xác nhận IC-I; EPs trong Table 1 là endpoints. |

Hai seed `10.1109/ms.2025.3559664` và `10.1109/access.2025.3554960` hiện **EXCLUDE**, theo quyết định trong CSV nguồn hiện hành. Nhãn UNSURE ở các events lịch sử cũ được giữ để truy vết, không dùng thay quyết định mới. Một bài root khác `10.1145/3644032.3644449` EXCLUDE vì EC-S; tổng root full-text thực đọc hiện là 16 = 14 EXCLUDE + 2 INCLUDE (bBOXRT và K52), gồm 4 bài cũ và 12 bài được mở lại.

## File đối chiếu

| File | Dòng dữ liệu | Vai trò |
|---|---:|---|
| [01_all_records.csv](01_all_records.csv) | 150 | Catalog sau matching. |
| [02_after_screening_v1.csv](02_after_screening_v1.csv) | 150 | Giữ V1 lịch sử, thêm V2/current, route mở lại full-text và các record chưa review. |
| [04_fulltext_screening.csv](04_fulltext_screening.csv) | 107 | Outcomes: EXCLUDE 97, INCLUDE 5, REVIEW 5. |
| [03_final_included.csv](03_final_included.csv) | 5 | Chỉ INCLUDE; thêm K52 / P53. |
| [03_included_only.csv](extras/03_included_only.csv) | 5 | Tập INCLUDE đồng nhất với CSV 03. |
| [matching-crosswalk.csv](extras/matching-crosswalk.csv) | 150 | Nối canonical ID, K và P. |
| [evidence-table.md](evidence-table.md) | 5 bài INCLUDE | Evidence và độ gần PICO. |

## Những phần chưa chốt

- Nhãn EC-A của 46 reports có nguồn từ history import; chưa có audit truy cập độc lập từng bài. Không diễn giải là 46 PDF đã đọc và bị loại.
- 37 bài mới snowball chưa có quyết định; 5 full-text REVIEW còn mở.
- Forward và coverage 12 tháng chưa có bằng chứng bao phủ đầy đủ. Ledger có kết quả forward không đồng nghĩa coverage đã hoàn tất.
- Raw discovery totals/duplicates toàn bộ hồ sơ chưa phục hồi. Không dùng bộ đếm snapshot cũ để thay số dòng hiện hành.
- Matching/kiểm tra máy không thay thế kiểm chéo V1 hoặc Evidence bởi thành viên khác.
- INCLUDE dùng [IC/EC nhóm](extras/team-criteria-source.md), EP **và/hoặc** BVA. RQ nghiên cứu vẫn là EP kết hợp BVA trên 45 yêu cầu; độ gần RQ được ghi riêng.
