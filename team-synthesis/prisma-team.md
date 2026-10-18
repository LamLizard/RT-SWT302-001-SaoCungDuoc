# PRISMA nhóm — nhóm 1 (SaoCungDuoc) · RQ FA26-EXT-12

## Phễu nhóm

```text
[IEEE Xplore n1 = 2] [ACM DL n2 = 1] [OpenAlex n3 = 28] [Scholar n4 = 2] [Included từ snowballing n5 = 10] [Springer bổ sung = 3]
        ↓  cộng lại (N = 2 + 1 + 28 + 2 + 10 + 3 = 46)
[Bỏ trùng giữa các nguồn (N = 42)]   ← 4 bản EC-D trên 3 cặp bài: bBOXRT (n1 × Khôi-snowball) · No Time to Rest Yet ×2 (n3 × Tùng-snowball × K.Duy-snowball) · RESTest K22≡K90 (n3 × Springer)
        ↓
[Final included của nhóm (N = 42)]   ← = 42 dòng bảng chính trong evidence-table-merged.md ✓
```

## Số nhập form kiểm (hộp "Kiểm số PRISMA nhóm")

| Ô | Số |
|---|---:|
| IEEE Xplore, final (n1) | 2 |
| ACM DL, final (n2) | 1 |
| OpenAlex/Scopus, final (n3) | 28 |
| Scholar, final (n4) | 2 |
| Included từ snowballing (n5) | 10 |
| Springer (bổ sung — ngoài 5 ô gốc của form) | 3 |
| Sau bỏ trùng giữa nguồn | 42 |
| Final included nhóm | 42 |

## Phễu từng nguồn (tóm tắt — bản đầy đủ trong `prisma-flow.md` của từng người)

- **n1 · IEEE Xplore (Tùng):** catalog hợp nhất 150 (68 bài search + 82 snowball mới) → phễu chính: 2 INCLUDE (**bBOXRT**, **K52/P53**); nhánh snowball riêng: 3 INCLUDE (P12/K81, P17/K84, P38/K108) → n5. REVIEW: 5 bài đã chốt bỏ (16/10). Còn mở: 37 record chưa review + 46 EC-A (không tính vào N). *(Bản tinh chỉnh 16/10: chuẩn hoá trình bày; số liệu không đổi.)*
- **n2 · ACM DL (Lâm):** 80 → bỏ 19 trùng → 61 → loại V1 60 → full-text 1 → loại V2 0 → **1 INCLUDE (R021)**. Snowball (seed R021): 6 → loại V1 5 → 1 → EC-A 1 → 0.
- **n3 · OpenAlex (Khôi):** 196 → bỏ 37 trùng → 159 → loại V1 100 (IC-T 48 · IC-I 32 · IC-L 9 · IC-P 8 · EC-N 3) → full-text 59 → loại V2 31 → **28 INCLUDE (nhánh CSDL)**. Snowball SB1 (seed K90): 57 → −22 → 35 → … → **6 INCLUDE** (K167, K162, K192, K168, K191, K166).
- **n4 · Scholar (T.Duy):** 66 → −5 → 61 → loại V1 31 → đọc 29 (+1 chưa lấy full-text) → loại V2 26 → **2 INCLUDE (TD-0002, TD-0015)**. Snowball vòng 1 (seed TD-0002): 91 lượt → 63 bài mới → 0 INCLUDE.
- **n5 · Snowballing (tổng KK):** Tùng 3 + Khôi 6 + Lâm 0 + T.Duy 0 + K.Duy 1 (K39) = **10**. *(K.Duy: snowball vòng 1 đã bổ sung + đối chiếu 16/10 — 12 record → 1 INCLUDE; K39 ≡ No Time to Rest Yet, gộp EC-D vào dòng mục A.)*
- **Springer (bổ sung) — K.Duy:** 63 → −28 → 35 → loại V1 27 → 8 full-text → **loại V2 5 (EC-A) → 3 INCLUDE (K02, K22, K33)**; snowball vòng 1 (seed K02 + K33): 12 record → loại V1 11 → 1 full-text → **1 INCLUDE (K39)**.
