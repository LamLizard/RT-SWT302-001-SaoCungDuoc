# PRISMA flow — Khôi · nguồn phụ trách: OpenAlex
*Nhóm 1 — SaoCungDuoc · RQ FA26-EXT-12 · Cập nhật: 13/10/2026 · khung số liệu tạo bởi RBL Paper Harvester (tool tự viết), V2 cập nhật theo `03_final_included.csv`*

## Nhánh 1 — Tìm trong CSDL

```
[Paper từ OpenAlex (N = 196)]               ← search-log: V1 30 + V2 166
        ↓                                   
[Sau dedup (N = 159)]                       ← bỏ 37 bản trùng
        ↓
[Vào 01 → screening V1 (N = 159)]           ← = số dòng của nhánh này trong 01_all_records.csv
        ↓
[Loại V1 (N = 100): IC-T = 48, IC-I = 32, IC-L = 9, IC-P = 8, EC-N = 3] ← EXCLUDE trong 02_after_screening_v1.csv (mã chính)
        ↓
[Full-text đọc (N = 59)]                    ← INCLUDE 42 + Unsure 17 ở 02 = số dòng trong 03
        ↓
[Loại V2 (N = 9): IC-I = 3, EC-N = 2, EC-S = 2, IC-E = 1, EC-D = 1]
        ↓
[Included (N = 42)]                         ← INCLUDE trong cột v2_decision của 03_final_included.csv
```

**Kiểm cộng trừ:** 196 − 37 = 159 · 159 − 0 = 159 · 159 − 100 = 59 · 59 − 9 − 8 chưa quyết = 42 ✓

### Lý do loại ở V1

| Mã chính | Số bài | Bài |
|---|---|---|
| IC-T (không phải hội nghị/tạp chí) | 48 | K05, K06, K09, K16, K20, K23, K28, K29, K30, K35, K38, K48 … (+36) |
| IC-I (không dùng EP/BVA) | 32 | K03, K04, K10, K11, K15, K18, K19, K22, K24, K27, K40, K41 … (+20) |
| IC-L (không phải tiếng Anh) | 9 | K12, K115, K118, K130, K131, K141, K143, K156, K157 |
| IC-P (không về kiểm thử REST API mức request) | 8 | K26, K58, K114, K123, K135, K137, K138, K144 |
| EC-N (không có thực nghiệm) | 3 | K13, K117, K125 |

### Lý do loại ở V2

| Mã chính | Số bài | Bài |
|---|---|---|
| IC-I (không phải sinh input hộp đen) | 3 | K25, K63, K80 |
| EC-N (không có thực nghiệm) | 2 | K88, K99 |
| EC-S (dưới 4 trang) | 2 | K69 (2 tr, poster ICSE Companion), K126 (2 tr, SBFT) |
| IC-E (không có kết quả định lượng) | 1 | K81 |
| EC-D (trùng) | 1 | K106 (chép nội dung K94) |

## Nhánh 2 — Snowballing vòng 1

Seed: 1 bài INCLUDE của nhánh 1 — K90 *RESTest: Black-Box Constraint-Based Testing of RESTful Web APIs* (ICSOC 2020, DOI 10.1007/978-3-030-65310-1_33) · lấy bài từ năm 2020 ở cả hai hướng

```
[Tìm được qua snowballing (N = 57)]         ← lùi + tiến, SB1 57
        ↓                                   
[Sau dedup (N = 35)]                        ← bỏ 22 bản trùng (trùng nhau hoặc đã có ở bước trước)
        ↓
[Vào 01 → screening V1 (N = 35)]            ← = số dòng của nhánh này trong 01_all_records.csv
        ↓
[Loại V1 (N = 21): IC-I = 10, IC-P = 10, EC-N = 1] ← EXCLUDE trong 02_after_screening_v1.csv (mã chính)
        ↓
[Full-text đọc (N = 14)]                    ← INCLUDE 6 + Unsure 8 ở 02 = số dòng trong 03
        ↓
[Loại V2 (N = 7): IC-I = 4, EC-N = 2, EC-S = 1]
        ↓
[Included (N = 4)]                          ← INCLUDE trong cột v2_decision của 03_final_included.csv
```

**Kiểm cộng trừ:** 57 − 22 = 35 · 35 − 0 = 35 · 35 − 21 = 14 · 14 − 7 − 3 chưa quyết = 4 ✓

### Lý do loại ở V1

| Mã chính | Số bài | Bài |
|---|---|---|
| IC-I (không dùng EP/BVA) | 10 | K160, K164, K170, K171, K179, K182, K183, K187, K190, K193 |
| IC-P (không về kiểm thử REST API mức request) | 10 | K163, K169, K172, K174, K175, K177, K178, K184, K189, K194 |
| EC-N (không có thực nghiệm) | 1 | K161 |

### Lý do loại ở V2

| Mã chính | Số bài | Bài |
|---|---|---|
| IC-I (không phải sinh input hộp đen) | 4 | K165, K166, K181, K185 |
| EC-N (không có thực nghiệm) | 2 | K186, K188 |
| EC-S (dưới 4 trang) | 1 | K176 (3 tr, bản SRC; bản đầy đủ là K102) |

## Ghi chú phương pháp

- **V1** dùng bộ luật sàng tự động của RBL Paper Harvester (8 luật, xem nút "Xem các luật" trong tool), mỗi bài ghi luật đã áp vào `v1_note` dạng `[tự động] …`; người thực hiện rà lại các bài INCLUDE/Unsure.
- **IC-I** được áp theo nghĩa: bài sinh dữ liệu đầu vào hộp đen cho REST API theo hướng phân hoạch/biên/ràng buộc/combinatorial (khối I) hoặc ngẫu nhiên/fuzzing (khối C của RQ). Hộp trắng (cần mã nguồn), chỉ dùng LLM, chỉ sinh oracle → loại.
- **V2** do Khôi thực hiện, có AI (Claude) hỗ trợ tìm bản toàn văn mở (arXiv, kho trường), trang nhà xuất bản/metadata OpenAlex và trích bằng chứng (số trang, mục thực nghiệm, số liệu) vào cột `v2_reason` của `03_final_included.csv`. Mức bằng chứng ghi ngay trong `v2_reason` của từng bài: 12 bài đối chiếu toàn văn, 9 bài theo trang nhà xuất bản/số trang OpenAlex, 52 bài theo abstract + metadata (đang đọc toàn văn để xác nhận). Quyết định V2 cuối cùng do Khôi chịu trách nhiệm.

## Tổng

- Included cuối = nhánh 1 (42) + snowballing vòng 1 (4) = **46**
- Snowballing: 1 vòng, 1 gốc (K90), theo quyết định của nhóm cho tuần 6
- Tất cả phép kiểm cộng trừ: ✓ khớp

## ⚠ Chưa hoàn tất

- Nhánh 1 — Tìm trong CSDL: 8 bài chưa quyết ở V2 (K14, K17, K42, K60, K67, K136, K146, K149) — chưa lấy được toàn văn/abstract đủ để kết luận
- Nhánh 2 — Snowballing vòng 1: 3 bài chưa quyết ở V2 (K173, K180, K191) — OpenAlex không có abstract
