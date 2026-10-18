# PRISMA flow — Duy · nguồn phụ trách: Springer Nature 
*Nhóm 1 — SaoCungDuoc · RQ FA26-EXT-12 · Cập nhật: 16/10/2026 · tạo bởi RBL Paper Harvester*

## Nhánh 1 — Tìm trong CSDL

```
[Paper từ Springer Nature (N = 63)]         ← search-log: V1 3 + V2 10 + V3 18 + V4 12 + V5 10 + V6 10
        ↓                                   
[Sau dedup (N = 35)]                        ← bỏ 28 bản trùng
        ↓
[Vào 01 → screening V1 (N = 35)]            ← = số dòng của nhánh này trong 01_all_records.csv
        ↓
[Loại V1 (N = 27): IC-P = 20, EC-N = 5, IC-I = 2] ← EXCLUDE trong 02_after_screening_v1.csv (mã chính)
        ↓
[Full-text đọc (N = 8)]                     ← INCLUDE 8 + Unsure 0 ở 02 = số dòng trong 03
        ↓
[Loại V2 (N = 5): EC-A = 5]                 
        ↓
[Included (N = 3)]                          ← INCLUDE trong cột v2_decision của 03_final_included.csv
```

**Kiểm cộng trừ:** 63 − 28 = 35 · 35 − 0 = 35 · 35 − 27 = 8 · 8 − 5 = 3 ✓

### Lý do loại ở V1

| Mã chính | Số bài | Bài |
|---|---|---|
| IC-P (không về kiểm thử REST API mức request) | 20 | K03, K06, K07, K09, K10, K12, K13, K14, K15, K16, K17, K18 … (+8) |
| EC-N (không có thực nghiệm) | 5 | K05, K11, K26, K30, K31 |
| IC-I (không dùng EP/BVA) | 2 | K01, K32 |

### Lý do loại ở V2

| Mã chính | Số bài | Bài |
|---|---|---|
| EC-A (không có full text) | 5 | K04, K08, K19, K24, K27 |

## Nhánh 2 — Snowballing vòng 1

Seed: 2 bài (INCLUDE của nhánh 1) · lấy bài từ năm 2020 ở cả hai hướng

```
[Tìm được qua snowballing (N = 12)]         ← lùi + tiến, SB1 0 + SB1 12
        ↓                                   
[Sau dedup (N = 12)]                        ← bỏ 0 bản trùng (trùng nhau hoặc đã có ở bước trước)
        ↓
[Vào 01 → screening V1 (N = 12)]            ← = số dòng của nhánh này trong 01_all_records.csv
        ↓
[Loại V1 (N = 11): IC-I = 7, IC-P = 2, IC-T = 2] ← EXCLUDE trong 02_after_screening_v1.csv (mã chính)
        ↓
[Full-text đọc (N = 1)]                     ← INCLUDE 1 + Unsure 0 ở 02 = số dòng trong 03
        ↓
[Loại V2 (N = 0)]                           
        ↓
[Included (N = 1)]                          ← INCLUDE trong cột v2_decision của 03_final_included.csv
```

**Kiểm cộng trừ:** 12 − 0 = 12 · 12 − 0 = 12 · 12 − 11 = 1 · 1 − 0 = 1 ✓

### Lý do loại ở V1

| Mã chính | Số bài | Bài |
|---|---|---|
| IC-I (không dùng EP/BVA) | 7 | K36, K37, K38, K40, K43, K46, K47 |
| IC-P (không về kiểm thử REST API mức request) | 2 | K41, K42 |
| IC-T (không phải hội nghị/tạp chí) | 2 | K44, K45 |

## Tổng

- Included cuối = nhánh 1 (3) + snowballing vòng 1 (1) + snowballing vòng 2 (0) = **4**
- Tất cả phép kiểm cộng trừ: ✓ khớp
