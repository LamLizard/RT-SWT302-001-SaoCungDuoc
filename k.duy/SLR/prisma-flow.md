# PRISMA flow — K.Duy · Springer Nature

Cập nhật 13/10/2026 theo các CSV hiện hành do K.Duy cập nhật: 01 có 35 records, 02 có 8, 03 có 8. Giữ nguyên các quyết định ở 03. Springer là nguồn phụ của K.Duy, không tự cộng vào PRISMA tổng IEEE/ACM/OpenAlex của nhóm.

## Identification và screening

| Giai đoạn | Số | Căn cứ / trạng thái |
|---|---:|---|
| Records trong 01_all_records.csv | 35 | Export Springer Nature sau gộp. |
| Records có trong 02_after_screening_v1.csv | 8 | Tệp hiện tại chỉ có 8 dòng metadata. |
| Records có trong 03_final_included.csv | 8 | Cả 8 mang `v1_decision=INCLUDE`. |
| Records trong 01 nhưng không có trong 02/03 | 27 | Không có quyết định/lý do V1 trong hai tệp hiện tại; giữ là disposition chưa ghi nhận, không tự gán lý do loại. |
| V2 decision đã ghi | 0 | Cột `v2_decision` đang trống cho cả 8. |
| V2 đang chờ | 8 | Chưa có quyết định full-text được ghi nhận. |
| Included cuối cùng xác nhận | 0 | Chưa hoàn tất V2; không tính V1 INCLUDE thành final included. |

```text
Records identified in 01 (n = 35)
  ├─ Records present in 02/03 with V1 INCLUDE (n = 8)
  │    └─ V2 decision recorded (n = 0)
  │         └─ V2 pending (n = 8)
  └─ Not present in 02/03; V1 disposition not recorded (n = 27)

Studies included after full-text/V2 (n = 0 confirmed)
```

### V1 fields recorded in 03

| V1 label | Count | Note |
|---|---:|---|
| INCLUDE | 8 | K02, K04, K08, K19, K22, K24, K27, K33. |
| EXCLUDE / Unsure | 0 in 03 | No such labels appear in the current 03 file. This does not establish the status of the other 27 records. |
| V2 pending | 8 | `v2_decision` and `v2_reason` blank. |

## Snowballing

`snowball-seeds.txt` currently contains 13 DOI seeds. No retrieved snowball records, citation counts, or seed/result links are recorded in 01–03 or the available run log. Snowballing totals remain unverified and are not added to the 35 Springer records.

## File consistency

| File | Data rows | Status |
|---|---:|---|
| `01_all_records.csv` | 35 | Metadata export. |
| `02_after_screening_v1.csv` | 8 | Eight metadata rows; no V1 decision/reason columns. |
| `03_final_included.csv` | 8 | Eight V1 INCLUDE; V2 pending for all. |
| `evidence-table.md` | 8 | Abstract/metadata extraction for the eight 03 records. |
| `snowball-seeds.txt` | 13 | Current seed list. |
