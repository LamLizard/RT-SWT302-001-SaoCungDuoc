# Search log — Lâm · nguồn phụ trách: ACM Digital Library
*Nhóm 1 — SaoCungDuoc · RQ FA26-EXT-12 · Cập nhật: 04/10/2026*

## 1. Nhật ký chạy query (ghi MỌI phiên bản chuỗi + số kết quả)

| Lần | Chuỗi tìm (nguyên văn) | CSDL | Trường tìm | Bộ lọc | Ngày chạy | Số kết quả | Ghi chú |
|---|---|---|---|---|---|---|---|
| **V1** | `("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing") AND ("fault detection" OR "mutant detection" OR "bugs found")` | ACM DL | AllField (mặc định) | Không đặt lọc | 04/10/2026 | **6** | < 20 kết quả → theo quy tắc: bỏ khối O để nới (bản V2) |
| **V2** | `("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing")` | ACM DL | AllField (mặc định) | Không đặt lọc | 04/10/2026 | **10** | Vẫn < 20 → tiếp tục nới bằng từ đồng nghĩa (String B/C) |
| **V3** | `("REST API" OR "RESTful API" OR "REST API testing" OR RESTest OR RESTestBench) AND ("equivalence partitioning" OR "equivalence class partitioning" OR "boundary value analysis" OR "boundary value testing" OR "boundary testing") AND ("fault detection" OR "faults found" OR "bug detection" OR "bugs found" OR defects OR failures OR "mutation testing" OR "mutation score" OR "mutant detection")` | ACM DL | AllField (mặc định) | Không đặt lọc | 04/10/2026 | **52** | ✅ Chuỗi chạy chính — bộ record chính của nguồn ACM |

*Ghi chú kiểm chứng: (1) Ngày chạy tạm ghi 04/10/2026 — sửa nếu thực tế khác. (2) Trường tìm/bộ lọc ghi theo mặc định khi chạy — sửa nếu có đặt cụ thể.*

## 2. Xử lý đặc biệt trong quá trình tìm

1. **ACM trả về nhiều record dạng "tập kỷ yếu" (proceedings)** — không phải bài báo đơn. Cách xử lý:
   - Các tập kỷ yếu **vẫn ghi nhận trong 01_all_records.csv** và **loại ở vòng lọc V1 với mã EC-N** (kèm ghi chú rõ).
   - Đồng thời **mở mục lục** các tập liên quan (trong ACM DL) để **tách các bài bên trong**: đã quét **20 tập** → **1.846 tiêu đề** → lọc theo từ khóa chủ đề → **120 bài khớp** → chọn **16 bài sát chủ đề nhất** đưa vào sàng lọc như record thường.
2. **03 DOI bổ sung ngoài bản export**: `10.1145/3491038`, `10.1145/3540250.3549144`, `10.1145/3540250.3559080` — rất sát RQ, giữ lại với nhãn "V3 (bổ sung)".
3. **Tổng hợp số**: V1 6 + V2 10 + V3 52 + bổ sung 3 + mục lục 16 = **87 record thô** → sau loại trùng (EC-D): **73 record** (khớp `01_all_records.csv`).
4. Tra cứu bổ trợ (DOI.org / Crossref / OpenAlex) chỉ dùng để lấy metadata phục vụ ghi nhận & sàng lọc — **không tạo record mới** ngoài danh sách trên.

## 3. Thay đổi so với protocol

| Ngày | Thay đổi | Lý do |
|---|---|---|
| 04/10/2026 | Dời ngày dừng search: 04/10 → **23:59 05/10/2026** | Cần thêm thời gian hoàn tất chạy & tổng hợp (sửa lý do cho đúng thực tế) |

## 4. Snowballing — vòng 1 (bổ sung 08/10/2026, làm theo hướng dẫn A2b/A3)

**Seed — chọn theo 4 bước:**
1. **Điều kiện cần:** chỉ xét 13 bài đã INCLUDE ở vòng 2 (`03_final_included.csv`) ✓.
2. **Độ sát RQ:** cột "Gần RQ" hiện tại của cả 13 bài tối đa **2/4** (đạt P và/hoặc O). Hai yếu tố **I** (EP/BVA cho tham số request) và **C** (đối chứng với random) hầu như chưa xuất hiện trong các bài INCLUDE — nên chưa bài nào đạt ≥3/4; chốt theo các tiêu chí còn lại (mức sát nhất khả dụng trong nguồn ACM).
3. **Loại paper:** ưu tiên bài có danh mục tham khảo dài (tốt cho lùi) hoặc bài mới 3 năm gần đây (tốt cho tiến).
4. **Số trích dẫn (10–200):** **#1 = 31 ✓ · #2 = 34 ✓ · #12 = 15 ✓**; các bài ICSE/AST/SBFT 2026 có citation 0–2 → hướng tiến gần như rỗng.

→ **Seed chính: #1 · `10.1145/3491038` — "On the Faults Found in REST APIs by Automated Test Generation" (TOSEM 2022, mã R55)** — 31 citation, 30 mục tham khảo, là bài nền về fault/mutant của RQ; cho kết quả tốt nhất trong lượt chạy (thêm 24 · include 15). **Dự phòng: #2, #12.**.
*Lượt chạy phủ cả 13 bài INCLUDE từ nguồn ACM của tôi (bảng dưới ghi đủ); mỗi seed đúng 1 lượt lùi + 1 lượt tiến; không snowball tiếp từ bài mới INCLUDE. Nếu cần đúng 1 seed/người theo checklist, dùng riêng 2 dòng của #1 (lùi 30 → thêm 3 → include 3; tiến 31 → thêm 21 → include 12).*

**Bảng seed 6 cột (vòng 1):**

| Seed (DOI) | Vòng | Hướng (lùi/tiến) | Số đã lướt | Số thêm vào 01 | Số include cuối |
|---|---:|---|---:|---:|---:|
| 10.1145/3491038 (#1 · R55) | 1 | Lùi (References, OpenAlex) | 30 | 3 | 3 |
| 10.1145/3491038 (#1 · R55) | 1 | Tiến (Citations, OpenAlex) | 31 | 21 | 12 |
| 10.1145/3540250.3549144 (#2 · R56) | 1 | Lùi (References, OpenAlex) | 35 | 9 | 4 |
| 10.1145/3540250.3549144 (#2 · R56) | 1 | Tiến (Citations, OpenAlex) | 34 | 27 | 6 |
| 10.1145/3793654.3793747 (#3 · R58) | 1 | Lùi (References, OpenAlex) | 41 | 7 | 7 |
| 10.1145/3793654.3793747 (#3 · R58) | 1 | Tiến (Citations, OpenAlex) | 0 | 0 | 0 |
| 10.1145/3793654.3793743 (#4 · R60) | 1 | Lùi (References, OpenAlex + S2) | 12 | 5 | 1 |
| 10.1145/3793654.3793743 (#4 · R60) | 1 | Tiến (Citations, OpenAlex + S2) | 2 | 2 | 0 |
| 10.1145/3744916.3773228 (#5 · R64) | 1 | Lùi (References, OpenAlex) | 26 | 18 | 6 |
| 10.1145/3744916.3773228 (#5 · R64) | 1 | Tiến (Citations, OpenAlex) | 0 | 0 | 0 |
| 10.1145/3744916.3787775 (#6 · R65) | 1 | Lùi (References, OpenAlex + S2) | 27 | 6 | 5 |
| 10.1145/3744916.3787775 (#6 · R65) | 1 | Tiến (Citations, OpenAlex + S2) | 5 | 5 | 0 |
| 10.1145/3744916.3787787 (#7 · R66) | 1 | Lùi (References, OpenAlex) | 19 | 6 | 1 |
| 10.1145/3744916.3787787 (#7 · R66) | 1 | Tiến (Citations, OpenAlex) | 1 | 0 | 0 |
| 10.1145/3744916.3787826 (#8 · R67) | 1 | Lùi (References, OpenAlex + S2) | 24 | 9 | 2 |
| 10.1145/3744916.3787826 (#8 · R67) | 1 | Tiến (Citations, OpenAlex + S2) | 0 | 0 | 0 |
| 10.1145/3744916.3773185 (#9 · R69) | 1 | Lùi (References, OpenAlex + S2) | 24 | 7 | 1 |
| 10.1145/3744916.3773185 (#9 · R69) | 1 | Tiến (Citations, OpenAlex + S2) | 5 | 3 | 1 |
| 10.1145/3786155.3795704 (#10 · R72) | 1 | Lùi (References, OpenAlex) | 12 | 9 | 8 |
| 10.1145/3786155.3795704 (#10 · R72) | 1 | Tiến (Citations, OpenAlex) | 2 | 1 | 0 |
| 10.1145/3793654.3793754 (#11 · R61) | 1 | Lùi (References, OpenAlex) | 18 | 13 | 0 |
| 10.1145/3793654.3793754 (#11 · R61) | 1 | Tiến (Citations, OpenAlex) | 2 | 2 | 0 |
| 10.1145/3597503.3608133 (#12 · R62) | 1 | Lùi (References, OpenAlex) | 19 | 3 | 1 |
| 10.1145/3597503.3608133 (#12 · R62) | 1 | Tiến (Citations, OpenAlex) | 14 | 11 | 1 |
| 10.1145/3786155.3788581 (#13 · R71) | 1 | Lùi (References, OpenAlex) | 10 | 5 | 2 |
| 10.1145/3786155.3788581 (#13 · R71) | 1 | Tiến (Citations, OpenAlex) | 1 | 0 | 0 |

- **Tổng:** đã rà **297 tiêu đề hướng lùi + 97 tiêu đề hướng tiến**; **thêm 172 dòng vào `01_all_records.csv`**; **include cuối = 61** (sau đúng 2 vòng screening với cùng IC/EC như paper tìm bằng search string).
- **Bộ lọc năm:** tab Citations đã lọc năm ≥ 2020 (IC-Y). Không seed nào vượt 200 citation (cao nhất: #2 = 34) → không cần lọc từ khoá P/I bổ sung.
- **Nguồn:** OpenAlex (References + Citations); riêng #4/#6/#8/#9 thiếu danh sách trên OpenAlex → bù bằng **Semantic Scholar**. Metadata đối chiếu **Crossref** (các chỗ từng lệch đã sửa: QuickREST ICST tr. 131–141; foREST → bản xuất bản ISSRE 2023; SN-017 = ICSE'22 Companion 2 trang; SN-176 = LNCS 3 trang; RESTestBench = accepted EASE 2026).
- **5 dòng đã bỏ, KHÔNG thêm vào 01** (không tính vào 172): SN-022 (≡ R63 đã có — EC-D), SN-147 (≡ R73 đã có — EC-D), SN-171 (bản arXiv của R64 — MioHint — EC-D), SN-134 (gói nhân bản SBFT — không phải bài), SN-142 (tài liệu bổ sung của R56 — không phải bài). Các dòng này vẫn xem được trong `Snowball.csv` (bảng mở rộng 177 phát hiện).
- **Kết quả sàng lọc (đủ 2 vòng):** 172 → loại V1 **107** (IC-P 68 · IC-I 13 · EC-O 12 · EC-N 9 · IC-T 3 · IC-L 2) → full-text **65** (64 INCLUDE + 1 UNSURE) → loại V2 **4** (EC-S 3: SN-017/SN-146/SN-176 · IC-T 1: SN-047) → **giữ 61**. Chi tiết từng dòng: `Snowball_02_v1.csv` + `Snowball_03_v2.csv`.
- **Ứng viên phản chứng (đã rà title/abstract hướng tiến, mới nhất 2025–2026):** SN-145 (ICST'26 — industrial experience), SN-146 (AutoRestTest @ SBFT'26), SN-158 (RESTestBench — accepted EASE 2026), SN-160 (case study ISSREW'25), SN-118/SN-045 (access-policy fuzzing), SN-110 (model-inference search), SN-138 (random test generation for string validation — có yếu tố I+C, đáng rà full-text). Sơ bộ **chưa bài nào đạt ≥3/4** theo P/I/C/O (thiếu I/C đặc thù RQ) → **danh sách ứng viên phản chứng hiện: trống** — sẽ chốt lại khi nhóm gộp và làm evidence.
