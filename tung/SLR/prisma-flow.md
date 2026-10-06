# PRISMA flow — Tùng · IEEE Xplore

Nhóm SaoCungDuoc · RQ FA26-EXT-12 · Đóng gói ngày 05/10/2026.


## Nhận diện

| Lượt | Kết quả | Tính vào tập chính |
|---|---:|---|
| Q0 — A, All Metadata | 0 | Không; lượt kiểm tra |
| Q1 — A, đúng trường tìm | 0 | Có |
| Q2 — A bỏ Outcome | 0 | Có |
| Q3 — B/C | 0 | Có |
| Q4a — B/C bỏ Outcome, mọi năm | 14 | Không; audit trước lọc năm, 12 bài trước 2020 |
| Q4b — B/C bỏ Outcome, từ 2020 | 2 | Có; tập chính |
| Q4c — chạy lại Q4b | 2 | Không cộng lại |
| Tổng records trong phạm vi trước dedup | 2 | Q1 + Q2 + Q3 + Q4b |
| Trùng nội bộ bị loại | 0 | Theo DOI/article number |
| Records sau dedup | 2 | 01_all_records.csv |

## Luồng sàng lọc

```text
Records identified từ IEEE trong phạm vi (n = 2)
  → Loại trùng nội bộ (n = 0)
Records screened V1 (n = 2)
  → Exclude V1 (n = 0); Unsure V1 (n = 0)
Reports sought for retrieval (n = 2)
  → Không lấy được toàn văn (n = 0)
Reports retrieved / assessed V2 (n = 2)
  → Exclude V2 (n = 0); Unsure V2 (n = 0)
Reports / studies included, bản AI (n = 2)
  → Awaiting-team-review (2/2); Near_RQ = Indirect (2/2)
```

## Đối chiếu các file

| File | Số dòng dữ liệu | Nội dung |
|---|---:|---|
| [01_all_records.csv](01_all_records.csv) | 2 | Toàn bộ records của tập chính |
| [02_after_screening_v1.csv](02_after_screening_v1.csv) | 2 | Toàn bộ records và quyết định V1; Include 2, Exclude 0, Unsure 0 |
| [03_final_included.csv](03_final_included.csv) | 2 | Chỉ V2 Include; giữ trạng thái chờ review |
| [evidence-table.md](evidence-table.md) | 2 | Một hàng cho mỗi V2 Include, đủ 8 mục của protocol |

Kiểm cộng trừ: 2 − 0 = 2 screened; 2 − 0 = 2 sought; 2 − 0 = 2 assessed; 2 − 0 − 0 = 2 Include.

## Ghi chú

- Paper 001 có toàn văn dạng webtext; paper 002 có PDF bản xuất bản. Không coi việc chưa tải được PDF 001 là thiếu toàn văn.
- Không cộng các lượt audit, rerun, truy metadata/full-text vào số identified. Mỗi Record_ID hiện đại diện một report/một study.
- Snowballing cá nhân: 0 lượt, không thực hiện trong phần IEEE này. Snowballing nhóm do K.Duy phụ trách; không hiểu số 0 là nhóm không có snowballing.
- Chưa dedup với ACM/OpenAlex và các nguồn khác. Không cộng thẳng 2 vào số studies cuối của nhóm.
- Đủ file để bàn giao không xác nhận đạt chỉ tiêu 6 bài/người: tập hiện tại có 2 bài Include ở bản AI và đang chờ kiểm chéo.
