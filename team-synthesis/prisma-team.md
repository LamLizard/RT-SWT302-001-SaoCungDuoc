# PRISMA nhóm — nhóm 1 (SaoCungDuoc) · RQ FA26-EXT-12

> **Đối soát hiện hành 22/10/2026:** thêm GV-18/Rodríguez theo mail cô vào lớp nguồn nền, thành **60 nguồn evidence = 42 INCLUDE lịch sử + 18 nguồn nền**. Không có lượt screening CSDL mới hoặc INCLUDE mới trong cập nhật này. Toàn bộ số 59/17 và phễu phía dưới là hồ sơ ngày 20/10 được giữ để truy vết; PRISMA final vẫn 42.

**Cập nhật:** 20/10/2026. Phân biệt **42 bài INCLUDE qua screening** với **17 bài nền bổ sung**: [bảng merge](evidence-table-merged.md) và [map](rq-evidence-map.md) hiện có **59 bài evidence duy nhất**. Đợt này đồng bộ cách báo cáo; không screening lại IC/EC hoặc đổi quyết định INCLUDE của các nguồn.

## Phễu screening nhóm — giữ số liệu 42 bài

```text
[IEEE Xplore n1 = 2] [ACM DL n2 = 2] [OpenAlex n3 = 28] [Scholar n4 = 2] [Included từ snowballing n5 = 10] [Springer bổ sung = 3]
        ↓  cộng lại (N = 2 + 2 + 28 + 2 + 10 + 3 = 47)
[Bỏ trùng giữa các nguồn (N = 42)]   ← 5 bản EC-D trên 4 cặp bài: bBOXRT (n1 × Khôi-snowball) · No Time to Rest Yet ×2 (n3 × Tùng-snowball × K.Duy-snowball) · RESTest K22≡K90 (n3 × Springer) · EmRest R391≡K101 (n2 × n3)
        ↓
[Final included qua screening (N = 42)]   ← = các dòng #1–#42 trong evidence-table-merged.md
```

## Số nhập form kiểm (hộp "Kiểm số PRISMA nhóm")

| Ô | Số |
|---|---:|
| IEEE Xplore, final (n1) | 2 |
| ACM DL, final (n2) | 2 |
| OpenAlex/Scopus, final (n3) | 28 |
| Scholar, final (n4) | 2 |
| Included từ snowballing (n5) | 10 |
| Springer (bổ sung — ngoài 5 ô gốc của form) | 3 |
| Sau bỏ trùng giữa nguồn | 42 |
| Final included nhóm | 42 |

Các ô form trên chỉ phản ánh nhánh screening cũ. **Không điền 59 vào ô Final included** khi 17 bài nền chưa có quyết định IC/EC tương ứng được xác minh.

## Bài nền bổ sung và đối soát bộ evidence

| Phạm vi | Số bài | Nguồn và cách tính |
|---|---:|---|
| Records INCLUDE của các nguồn trước khử trùng liên nguồn | 47 | 2 + 2 + 28 + 2 + 10 + 3; không phải tổng records tìm được ban đầu. |
| Bản trùng liên nguồn bị gộp | 5 | 4 nhóm paper: bBOXRT (1), No Time to Rest Yet (2), RESTest K22≡K90 (1), EmRest R391≡K101 (1). |
| Paper INCLUDE sau screening và khử trùng | 42 | 47 − 5 = 42; các dòng #1–#42 của bảng merge. |
| Paper nền do leader bổ sung, đã đọc phần toàn văn liên quan | 17 | GV-01–GV-17; các dòng #43–#59 của bảng merge, truy vết qua [nguồn Lâm](../lam/SLR/evidence-table.md) và PDF gốc được dẫn ở từng dòng. |
| Trùng giữa 17 bài nền và 42 bài screening | 0 | Theo đối chiếu DOI/arXiv và tên paper đã ghi trong bảng merge; không gộp hai nghiên cứu chỉ vì cùng tác giả hoặc công cụ. |
| Bộ evidence dùng đối chiếu RQ | **59** | **42 + 17 − 0 = 59** dòng merge/map; không đồng nghĩa 59 bài đã INCLUDE theo IC/EC. |

17 bài nền được bổ sung để kiểm tra RQ và gap, không đi ngược qua phễu CSDL/snowballing cũ. Audit PICO có **67/68 ô phân loại được**, còn **GV-13/P?**; việc đọc PDF và chấm PICO không thay cho screening. Ví dụ GV-01 là bài Android năm 2018, GV-17 chưa có kết quả định lượng trong bản đọc: không mặc nhiên coi mọi bài nền đều thỏa IC-Y/IC-P/IC-E. Đợt này không gán mới mã loại cho chúng.

**Khử trùng alias:** GV-02 = R2R-01 (RESTestBench), GV-03 = R2R-04 (Prompt-Based), GV-04 = R2R-03 (RESTOR) ở hồ sơ Tùng; mỗi nghiên cứu chỉ có một dòng trong 59. Bản preprint/conference và bản PDF lưu ở hai thư mục không được tính thành hai paper. **Guo 2024 và MioHint/R2R-02 nằm ngoài ma trận 59**; vẫn được xét ở [phản chứng của nhóm](rq-validation.md), nhưng không cộng vào phễu hoặc số dòng merge.

Đây là sơ đồ tổng hợp nguồn của nhóm, chưa phải một phễu PRISMA đầy đủ cho cả 59 bài: không có số records tìm/screen/loại theo IC/EC riêng cho nhánh 17 bài nền. Các số phễu cá nhân dưới đây được giữ theo hồ sơ nguồn; không suy ra số liệu screening chưa ghi nhận.

## Phễu từng nguồn (tóm tắt — bản đầy đủ trong `prisma-flow.md` của từng người)

- **n1 · IEEE Xplore (Tùng):** catalog hợp nhất 150 (68 bài search + 82 snowball mới) → phễu chính: 2 INCLUDE (**bBOXRT**, **K52/P53**); nhánh snowball riêng: 3 INCLUDE (P12/K81, P17/K84, P38/K108) → n5. REVIEW: 5 bài đã chốt bỏ (16/10). Còn mở: 37 record chưa review + 46 EC-A (không tính vào N). *(Tùng cập nhật evidence table 17/10 — không đổi số include.)*
- **n2 · ACM DL (Lâm):** 888 → bỏ 261 trùng → 627 → loại V1 555 (IC-P 440 · IC-Y 98 · EC-O 7 · EC-O(1) 9 · EC-O(2) 1) → full-text 72 → loại V2 70 (IC-I 46 · IC-P 14 · EC-S 6 · EC-N 2 · EC-O 1 · EC-A 1) → **2 INCLUDE (R021, R391)**; **R391 ≡ K101 (Khôi · OpenAlex) → EC-D**. Snowball (seed R021): 6 → loại V1 5 → 1 → EC-A 1 → 0.
- **n3 · OpenAlex (Khôi):** 196 → bỏ 37 trùng → 159 → loại V1 100 (IC-T 48 · IC-I 32 · IC-L 9 · IC-P 8 · EC-N 3) → full-text 59 → loại V2 31 → **28 INCLUDE (nhánh CSDL)**. Snowball SB1 (seed K90): 57 → −22 → 35 → … → **6 INCLUDE** (K167, K162, K192, K168, K191, K166). *(Khôi double-check 17/10: 34 dòng — không đổi số include; sửa venue/năm/tác giả + số liệu K43/K68/K162.)*
- **n4 · Scholar (T.Duy):** 66 → −5 → 61 → loại V1 31 → đọc 29 (+1 chưa lấy full-text) → loại V2 26 → **2 INCLUDE (TD-0002, TD-0015)**. Snowball vòng 1 (seed TD-0002): 91 lượt → 63 bài mới → 0 INCLUDE.
- **n5 · Snowballing (tổng KK):** Tùng 3 + Khôi 6 + Lâm 0 + T.Duy 0 + K.Duy 1 (K39) = **10**. *(K39 ≡ No Time to Rest Yet — gộp EC-D vào dòng mục A.)*
- **Springer (bổ sung) — K.Duy:** 63 → −28 → 35 → loại V1 27 → 8 full-text → **loại V2 5 (EC-A) → 3 INCLUDE (K02, K22, K33)**; snowball vòng 1 (seed K02 + K33): 12 record → loại V1 11 → 1 full-text → **1 INCLUDE (K39 — EC-D)**. *(K.Duy evidence-check 17/10: K02/K33 đã điền đủ số — P3 từ fail → pass.)*
