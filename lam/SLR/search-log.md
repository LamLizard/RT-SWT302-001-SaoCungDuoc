# Search log — Lâm · nguồn phụ trách: ACM Digital Library

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
| 04/10/2026 | Dời ngày dừng search: 04/10 → **23:59 05/10/2026** | Cần thêm thời gian hoàn tất chạy & tổng hợp |

## 4. Snowballing — vòng 1 · 1 seed (bổ sung 08/10/2026, theo hướng dẫn A2b/A3)

**Seed — chọn theo 4 bước:**
1. **Điều kiện cần:** chỉ xét 13 bài đã INCLUDE ở vòng 2 (`03_final_included.csv`) ✓.
2. **Độ sát RQ:** cột "Gần RQ" của cả 13 bài tối đa **2/4** (đạt P và/hoặc O). Hai yếu tố **I** (EP/BVA cho tham số request) và **C** (đối chứng với random) chưa xuất hiện nên chưa bài nào đạt ≥3/4; chốt theo các tiêu chí còn lại (mức sát nhất khả dụng trong nguồn ACM).
3. **Loại paper:** ưu tiên bài nền có danh mục tham khảo dài (tốt cho lùi) / bài mới 3 năm (tốt cho tiến).
4. **Số trích dẫn (10–200):** **#1 = 31 ✓ · #2 = 34 ✓ · #12 = 15 ✓**; các bài ICSE/AST/SBFT 2026 có citation 0–2 → hướng tiến gần như rỗng.

→ **Seed: #1 · `10.1145/3491038` — "On the Faults Found in REST APIs by Automated Test Generation" (TOSEM 2022, mã R55)** — 31 citation, 30 mục tham khảo, là bài nền về fault/mutant của RQ; cho kết quả tốt nhất trong lượt chạy (thêm 24 · include 15). Không trùng seed thành viên khác đã biết (đối chiếu bảng seed của K.Duy).

**Bảng seed (6 cột, vòng 1 — mỗi seed đúng 1 lượt lùi + 1 lượt tiến, không snowball tiếp từ bài mới INCLUDE):**

| Seed (DOI) | Vòng | Hướng (lùi/tiến) | Số đã lướt | Số thêm vào 01 | Số include cuối |
|---|---:|---|---:|---:|---:|
| 10.1145/3491038 (#1 · R55) | 1 | Lùi (References, OpenAlex) | 30 | 3 | 3 |
| 10.1145/3491038 (#1 · R55) | 1 | Tiến (Citations, OpenAlex) | 31 | 21 | 12 |

- **Tổng:** đã rà **61 tiêu đề** (30 lùi + 31 tiến); **thêm 24 dòng vào `01_all_records.csv`**; **include cuối = 15** (sau đúng 2 vòng screening với cùng IC/EC như paper tìm bằng search string).
- **Bộ lọc năm:** tab Citations đã lọc năm ≥ 2020 (IC-Y); seed có 31 citation (< 200) → không cần lọc từ khoá P/I bổ sung.
- **Nguồn:** OpenAlex (References + Citations); metadata đối chiếu Crossref (vd QuickREST — ICST, tr. 131–141).
- **Kết quả sàng lọc (đủ 2 vòng):** 24 → loại V1 **9** (IC-P 5 · EC-N 2 · EC-O 1 · IC-T 1) → full-text **15** → loại V2 **0** → **giữ 15**. Chi tiết từng dòng: `02_after_screening_v1.csv` (vòng 1) + `03_final_included.csv` (vòng 2).
- **Ứng viên phản chứng (đã rà title/abstract hướng tiến, mới nhất):** SN-045 (JSS'26), SN-110, SN-118, SN-119, SN-120, SN-160 (2025)... Sơ bộ **chưa bài nào đạt ≥3/4** theo P/I/C/O (thiếu I/C đặc thù RQ) → **danh sách ứng viên phản chứng hiện: trống** — sẽ chốt lại khi nhóm gộp và làm evidence.
