# PRISMA (cá nhân) — Lâm · nguồn: ACM Digital Library

## PHỄU CHÍNH
```text
Paper từ nguồn (N = 80)
→ Sau bỏ trùng (N = 61) [bỏ 19 bản trùng]
→ Loại V1 (N = 60: EC-O=2 · EC-O(1)=1 · EC-O(2)=1 · IC-P=52 · IC-Y=4)
→ Full-text đọc (N = 1)
→ Loại V2 (N = 0: —)
→ Final phễu chính (N = 1)
```

## NHÁNH SNOWBALLING (vòng 1 — 1 seed: #1 · 10.1145/3491038, đủ 1 lượt lùi + 1 lượt tiến; lý do chọn: search-log §4)
```text
[Snowballing (N = 24)]  ← SS = tổng "Số thêm vào 01" của bảng seed (search-log §4): lùi rà 30 → thêm 3; tiến rà 31 → thêm 21
        ↓
[Loại V1 (N = 9): IC-P = 5, EC-N = 2, EC-O = 1, IC-T = 1]
        ↓
[Full-text đọc (N = 15)]
        ↓
[Loại V2 (N = 0)]
        ↓
[Included từ snowballing (N = 15)]  ← KK = tổng "Số include cuối" của bảng seed (3 lùi + 12 tiến)
```

**TỔNG: Final included = 13 (search) + 15 (snowball) = 28** → = số dòng Include trong `03_final_included.csv` đếm theo cột `source`; sau khi nhóm gộp (bỏ trùng theo DOI) sẽ cập nhật lại.
