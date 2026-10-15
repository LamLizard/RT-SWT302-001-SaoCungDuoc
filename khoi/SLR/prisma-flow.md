# PRISMA flow — Khôi · nguồn phụ trách: OpenAlex
*Nhóm 1 — SaoCungDuoc · RQ FA26-EXT-12 · Cập nhật: 13/10/2026 · tạo bởi RBL Paper Harvester*

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
[Loại V2 (N = 31): EC-A = 23, IC-I = 2, IC-E = 2, EC-S = 2, IC-L = 1, EC-N = 1] 
        ↓
[Included (N = 28)]                         ← INCLUDE trong cột v2_decision của 03_final_included.csv
```

**Kiểm cộng trừ:** 196 − 37 = 159 · 159 − 0 = 159 · 159 − 100 = 59 · 59 − 31 = 28 ✓

### Lý do loại ở V1

| Mã chính | Số bài | Bài |
|---|---|---|
| IC-T (không phải hội nghị/tạp chí) | 48 | K05, K06, K09, K16, K20, K23, K28, K29, K30, K35, K38, K48 … (+36) |
| IC-I (không dùng EP/BVA) | 32 | K03, K04, K10, K11, K15, K18, K19, K22, K24, K27, K40, K41 … (+20) |
| IC-L (không phải tiếng Anh) | 9 | K12, K115, K118, K130, K131, K141, K143, K156, K157 |
| IC-P (không về kiểm thử REST API mức request) | 8 | K26, K57, K114, K123, K135, K137, K138, K144 |
| EC-N (không có thực nghiệm) | 3 | K13, K117, K125 |

### Lý do loại ở V2

| Mã chính | Số bài | Bài |
|---|---|---|
| EC-A (không có full text) | 23 | K01, K02, K14, K17, K25, K31, K33, K36, K39, K42, K59, K63 … (+11) |
| IC-I (không dùng EP/BVA) | 2 | K80, K91 |
| IC-E (không có kết quả định lượng) | 2 | K81, K106 |
| EC-S (dưới 4 trang) | 2 | K99, K126 |
| IC-L (không phải tiếng Anh) | 1 | K08 |
| EC-N (không có thực nghiệm) | 1 | K88 |

## Nhánh 2 — Snowballing vòng 1

Seed: 1 bài (INCLUDE của nhánh 1) · lấy bài từ năm 2020 ở cả hai hướng

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
[Loại V2 (N = 8): IC-I = 3, EC-S = 2, EC-N = 2, EC-A = 1] 
        ↓
[Included (N = 6)]                          ← INCLUDE trong cột v2_decision của 03_final_included.csv
```

**Kiểm cộng trừ:** 57 − 22 = 35 · 35 − 0 = 35 · 35 − 21 = 14 · 14 − 8 = 6 ✓

### Lý do loại ở V1

| Mã chính | Số bài | Bài |
|---|---|---|
| IC-I (không dùng EP/BVA) | 10 | K160, K164, K170, K171, K179, K182, K183, K187, K190, K193 |
| IC-P (không về kiểm thử REST API mức request) | 10 | K163, K169, K172, K174, K175, K177, K178, K184, K189, K194 |
| EC-N (không có thực nghiệm) | 1 | K161 |

### Lý do loại ở V2

| Mã chính | Số bài | Bài |
|---|---|---|
| IC-I (không dùng EP/BVA) | 3 | K165, K181, K185 |
| EC-S (dưới 4 trang) | 2 | K176, K180 |
| EC-N (không có thực nghiệm) | 2 | K186, K188 |
| EC-A (không có full text) | 1 | K173 |

## Tổng

- Included cuối = nhánh 1 (28) + snowballing vòng 1 (6) + snowballing vòng 2 (0) = **34**
- Tất cả phép kiểm cộng trừ: ✓ khớp

## Ghi chú phương pháp

- **V1** dùng bộ luật sàng tự động của RBL Paper Harvester (xem nút "Xem các luật" trong tool); mỗi bài ghi luật đã áp vào `v1_note` dạng `[tự động] …`; người thực hiện rà lại các bài INCLUDE/Unsure.
- **IC-I** được áp theo nghĩa: bài đề xuất hoặc đánh giá thực nghiệm kỹ thuật sinh input/test case **hộp đen** cho request REST — phân hoạch/kiểu/biên, ràng buộc, combinatorial, property-based (khối I) hoặc ngẫu nhiên/fuzzing/mutation (khối C của RQ), kể cả so sánh các công cụ như vậy. Loại: chỉ đóng góp oracle, chỉ sinh mã/đặc tả, sinh test từ UI. Cách hiểu này cần PL xác nhận.
- **V2 (full-text):** Khôi tự tải toàn văn — lấy được **46/73** PDF (bản nhà xuất bản hoặc bản arXiv/tác giả của bài đã đăng). **27 bài không tải được** → EXCLUDE: 24 bài mã **EC-A**; 3 bài giữ mã đã xác định từ metadata (K08 IC-L; K99, K180 EC-S).
- 46 PDF được **AI (Claude) hỗ trợ đọc** theo IC/EC (số trang, có Table/Figure chứa số, kỹ thuật sinh input, có thực nghiệm) và đề xuất INCLUDE/EXCLUDE kèm bằng chứng; Khôi rà và nhập quyết định cuối vào tool. Quyết định V2 cuối cùng do Khôi chịu trách nhiệm.
- **Ca ranh giới (đang INCLUDE, cần PL xác nhận):** K82, K93, K192 (có dùng LLM nhưng không chỉ LLM); K127 (nghiên cứu áp dụng EvoMaster hộp đen); K136 (báo cáo cuộc thi SBFT); K166 (bộ lọc tính hợp lệ của input sinh ngẫu nhiên); K168 (kiểm thử bảo mật hộp đen); K103 (tạp chí ngoài chuyên ngành).
