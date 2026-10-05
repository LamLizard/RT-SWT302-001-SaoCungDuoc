# PRISMA flow — Khôi · nguồn phụ trách: OpenAlex
*Nhóm 1 — SaoCungDuoc · RQ FA26-EXT-12 · Cập nhật: 05/10/2026*

```
[Paper từ OpenAlex (N = 7)]          ← search-log.md: V3 0 + V4 0 + V5 0 + V6 7 (V1, V2 không hợp lệ, không tính)
        ↓
[Sau dedup (N = 7)]                  ← = số dòng 01_all_records.csv (bỏ 0 bản trùng)
        ↓
[Loại V1 (N = 7): IC-L = 7]          ← EXCLUDE trong 02_after_screening_v1.csv (mã chính)
        ↓
[Full-text đọc (N = 0)]              ← = INCLUDE + Unsure ở 02 = số dòng 03
        ↓
[Loại V2 (N = 0)]
        ↓
[Final included (N = 0)]             ← = số dòng Include trong 03_final_included.csv
```

**Kiểm cộng trừ:** 7 − 0 = 7 · 7 − 7 = 0 · 0 − 0 = 0 ✓

## Chi tiết lý do loại ở vòng 1

| Mã chính | Số bài | Bài |
|---|---|---|
| IC-L (không phải tiếng Anh) | 7 | K01–K07 |

Lý do phụ (một bài có thể trượt nhiều tiêu chí, ghi đủ trong cột `v1_reason`):

| Mã | Số bài | Bài |
|---|---|---|
| IC-P (không về kiểm thử REST API) | 5 | K03, K04, K05, K06, K07 |
| IC-I (không dùng EP/BVA) | 2 | K03, K04 |
| EC-O (UI/E2E web testing) | 1 | K06 |

## Ghi chú
- K01, K02 đúng chủ đề (EP cho RESTful API) nhưng viết bằng tiếng Indonesia → loại chỉ vì IC-L.
- Nguồn OpenAlex không đóng góp paper nào vào evidence table của nhóm (dưới mức tối thiểu ≥ 6/người). Báo PL kèm search-log làm bằng chứng (05/10/2026).
