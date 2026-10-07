# PRISMA flow — K.Duy · SpringerLink

*Nhóm 1 — SaoCungDuoc · RQ FA26-EXT-12 · Bản tạm ngày 07/10/2026. Số liệu tính từ các lượt tìm V1–V4 trong `search-log.md`; R04 còn UNSURE nên chưa chốt final inclusion.*

## Nhận diện (Identification)

| Nguồn/lượt tìm | Records tìm được |
|---|---:|
| V1 — String A | 1 |
| V2 — String A bỏ khối O | 3 |
| V3 — synonyms mở rộng | 11 |
| V4 — String B | 12 |
| **Tổng lượt tìm trước dedup** | **27** |
| Bản ghi trùng giữa các lượt | **5** |
| **Records duy nhất sau dedup** | **22** |

## Sàng lọc (Screening)

| Giai đoạn | Số lượng |
|---|---:|
| Records được sàng lọc tiêu đề/tóm tắt | 22 |
| Loại tại V1 | 21 |
| Qua V1 / cần xác minh thêm | 1 (R04 — UNSURE) |
| Toàn văn truy xuất/đọc được trong phiên này | 0 |
| R04 chờ kiểm tra toàn văn và quyết định IC-I | 1 |
| **Final included đã xác nhận** | **0** |

## Snowballing

| Vòng | Seed | Số quan hệ citation đã kiểm tra | Record mới sau dedup | Ghi chú |
|---|---|---:|---:|---|
| 1 | TUNG-IEEE-002 (10.1109/MS.2025.3559664; trạng thái V2 Include trong danh sách Tung) | 1 | 0 | R04 có trích dẫn seed và đã xuất hiện trong kết quả V3; không thêm record trùng. Đây là kiểm tra citation link đã xác minh, chưa phải quét đầy đủ forward citations trên mọi nền tảng. |

## Đối chiếu số

- `01_all_records.csv`: 22 record Springer đã dedup.
- `02_after_screening_v1.csv`: 22 record — 21 EXCLUDE, 1 UNSURE.
- `03_final_included.csv`: 1 ứng viên UNSURE/PENDING, **0 bài xác nhận final included**.
- Cân bằng V1: 22 = 21 loại + 1 cần xác minh. Sau khi nhóm quyết định R04 và kiểm tra toàn văn, cập nhật lại flow này.

## Lưu ý

- Các tổng V1–V4 là tổng số lượt truy vấn trên SpringerLink, không cộng vào PRISMA toàn nhóm nếu protocol không quy định.
- R04 có abstract về REST API test amplification nhưng hiện chưa xác nhận EP/BVA theo IC-I. Không tính R04 là included cho tới khi nhóm chốt và đối chiếu toàn văn.
- Không tính các lượt thăm dò rộng V5–V7 vào tập chính vì chưa gộp/khử trùng lặp toàn bộ kết quả các lượt này.
