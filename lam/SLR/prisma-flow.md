# PRISMA (cá nhân) — Lâm · nguồn: ACM Digital Library

## PHỄU CHÍNH (chốt trước, số không đổi)
```text
[Paper từ ACM Digital Library (N = 87)]
        ↓
[Sau dedup (N = 73)]  ← = số dòng source=search trong 01_all_records_v2.csv
        ↓
[Loại V1 (N = 56): EC-N = 44, IC-P = 7, IC-I = 4, EC-O = 1]
        ↓
[Full-text đọc (N = 17)]
        ↓
[Loại V2 (N = 4): EC-S = 3, EC-A = 1]
        ↓
[Final phễu chính (N = 13)]  ← = dòng Include, source = search
```

## NHÁNH SNOWBALLING (vòng 1 — mỗi seed đủ 1 lượt lùi + 1 lượt tiến)
```text
[Snowballing (N = 172)]  ← SS = tổng "Số thêm vào 01" của bảng seed (search-log §4): 13 seed INCLUDE × 2 hướng → 394 tiêu đề đã rà (297 lùi + 97 tiến) → 172 dòng mới thêm vào 01. Đã bỏ 5 dòng khi thêm (3 trùng + 2 tài liệu — không tính vào SS).
        ↓
[Loại V1 (N = 107): IC-P = 68, IC-I = 13, EC-O = 12, EC-N = 9, IC-T = 3, IC-L = 2]
        ↓
[Full-text đọc (N = 65): INCLUDE 64 + UNSURE 1]
        ↓
[Loại V2 (N = 4): EC-S = 3 (SN-017, SN-146, SN-176 — bản 2–3 trang), IC-T = 1 (SN-047)]
        ↓
[Included từ snowballing (N = 61)]  ← KK = tổng "Số include cuối" của bảng seed
```

**TỔNG: Final included = 13 (search) + 61 (snowball, đề xuất) = 74** → = số dòng Include trong `03_final_included.csv` đếm theo cột `source`; sau khi nhóm gộp (bỏ trùng theo DOI) sẽ cập nhật lại.
