# PRISMA flow — K.Duy · Springer Nature

Cập nhật 16/10/2026 theo các CSV hiện hành và xác nhận của K.Duy: 01 có 35 records, 02 có 8, 03 có 8. Cả 8 bài đã được rà soát V2 khi chuyển từ 02 sang 03 và được giữ là included cuối cùng; các trường V2 để trống có chủ đích vì không có thay đổi quyết định. Springer là nguồn phụ của K.Duy, không cộng vào PRISMA tổng IEEE/ACM/OpenAlex của nhóm.

## Identification và screening

| Giai đoạn | Số | Căn cứ / trạng thái |
|---|---:|---|
| Records trong `01_all_records.csv` | 35 | Export Springer Nature sau gộp. |
| `02_after_screening_v1.csv` | 8 | Tám record V1 có quyết định INCLUDE và lý do. |
| `03_final_included.csv` | 8 | Tám bài included cuối cùng; V2 hoàn tất và không thay đổi quyết định. |
| Records trong 01 nhưng không có trong 02/03 | 27 | Không có quyết định/lý do V1 trong hai tệp hiện tại; giữ là disposition chưa ghi nhận, không tự gán lý do loại. |
| Quyết định V2 được ghi trong CSV | 0 | v2_decision/v2_reason để trống có chủ đích vì V2 không làm thay đổi quyết định. |
| Đã rà soát V2 | 8 | Theo xác nhận của K.Duy, cả 8 bài đã được kiểm tra từ 02 sang 03 và được giữ lại. |
| Included cuối cùng đã xác nhận | 8 | Cả 8 bài được giữ lại sau V2 theo xác nhận của K.Duy. |

```text
Records identified in 01 (n = 35)
  |- Có trong 02/03 với V1 INCLUDE (n = 8)
  |    `- Rà soát 02 -> 03, quyết định không đổi (n = 8)
  |         `- Studies included cuối cùng (n = 8)
  `- Không có trong 02/03; chưa ghi nhận disposition V1 (n = 27)
```

### V1 fields recorded in 03

| Nhãn V1 | Số lượng | Ghi chú |
|---|---:|---|
| INCLUDE | 8 | K02, K04, K08, K19, K22, K24, K27, K33. |
| EXCLUDE / Unsure | 0 trong 03 | File 03 hiện hành không có nhãn này. Điều này không xác định trạng thái của 27 record còn lại. |
| Đã rà soát V2; quyết định không đổi | 8 | Theo xác nhận của K.Duy; các trường V2 để trống vì không có thay đổi. |

## Snowballing

`snowball-seeds.txt` hiện có 13 DOI seed. Chưa có snowball record nào được ghi nhận trong 01–03 hoặc run log hiện có (số citation, liên kết seed/kết quả). Tổng snowballing chưa được kiểm chứng và không cộng vào 35 record Springer.

## File consistency

| File | Data rows | Status |
|---|---:|---|
| `01_all_records.csv` | 35 | Export metadata Springer Nature. |
| `02_after_screening_v1.csv` | 8 | Tám record V1 có quyết định INCLUDE và lý do. |
| `03_final_included.csv` | 8 | Tám bài included cuối cùng; V2 hoàn tất và không thay đổi quyết định. |
| `evidence-table.md` | 8 | Bảng evidence của 8 bài included cuối cùng trong 03. |
| `snowball-seeds.txt` | 13 | Danh sách seed hiện hành. |
