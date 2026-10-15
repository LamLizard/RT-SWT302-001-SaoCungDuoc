# Runbook — chạy RBL Paper Harvester v1.5.1 cho phần K.Duy (Springer + snowballing nhóm)

Mục tiêu: lấy lại kết quả Springer bằng API chính thức (có abstract/DOI, tái lập được) và làm snowballing 1 vòng đúng protocol. Các ô ⬜ trong `search-log.md` / `prisma-flow.md` **chỉ điền số lấy từ log tool**, không ước lượng.

> ⚠ Các lượt này chạy sau ngày dừng search (23:59 05/10/2026) → báo PL và giữ dòng giải thích trong mục "Thay đổi so với protocol" của `search-log.md`.

## 0. Chuẩn bị (1 lần)

1. `chrome://extensions` → **Reload** extension (bản 1.5.1). Bỏ qua bước này sẽ gặp lỗi "không kết nối được tới server".
2. Tab **Cài đặt API key**: dán Springer Nature key (Meta API), OpenAlex key + email (`mailto`), Semantic Scholar key nếu có → **Lưu key**.
3. Tab **Search**: đặt **Tiền tố mã = `KD-SPR-`** và **Bắt đầu từ số = `23`** (22 mã đầu đã dùng). Phải đặt TRƯỚC khi chạy vì tool cấp mã ngay sau mỗi lần chạy.

## 1. Springer (6 lượt)

Mỗi lượt: dán chuỗi vào ô chuỗi tìm → bấm **Xem chuỗi dịch** kiểm tra → chỉ tick **Springer Nature** → **Từ năm = 2020**, **Tối đa = 500** → đặt nhãn → **Chạy search**. Chạy lần lượt, không song song (gói Basic giới hạn lượt/phút).

| Nhãn | Chuỗi tìm (dán nguyên văn) | Tương ứng thủ công |
|---|---|---|
| T1 | `("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing") AND ("fault detection" OR "mutant detection" OR "bugs found")` | V1 (web báo 1) — String A nguyên văn (protocol §3) |
| T2 | `("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing")` | V2 (web báo 3) — String A bỏ khối O |
| T3 | `("REST API" OR "RESTful API" OR RESTest OR RESTestBench) AND ("equivalence partitioning" OR "equivalence class partitioning" OR "boundary value analysis" OR "boundary value testing" OR "boundary testing") AND ("fault detection" OR "faults found" OR "bug detection" OR "bugs found" OR defects OR failures OR "mutation testing" OR "mutation score" OR "mutant detection")` | V3 (web báo 11) — Synonyms mở rộng |
| T4 | `("REST API" OR "RESTful API" OR "web API" OR "web service") AND ("boundary value analysis" OR "boundary value" OR "boundary testing" OR "equivalence partitioning") AND ("mutation testing" OR "mutants" OR "mutation score")` | V4 (web báo 12) — String B (protocol §3) |
| T5 | `"REST API" AND "equivalence partitioning"` | V6 (web báo 6) — Chỉ EP |
| T6 | `"REST API" AND "boundary value analysis"` | V7 (web báo 6) — Chỉ BVA |

Ghi từ nhật ký tool vào `search-log.md` (bảng tool): **Số kết quả (API báo)** = số sau dấu `/` ở dòng `✔ Springer Nature: lấy X/Y`; **Số lấy về (≥2020)** = X; số "bỏ N bản ghi trước năm 2020" nằm ở ghi chú.

- Nếu thấy ❌ "gói Basic không cho lấy sâu hơn ~200 kết quả": chuỗi quá rộng → không xảy ra với T1–T6 (web báo ≤ 12), nếu xảy ra hãy báo lại.
- Lệch giữa số web (V1–V7) và số API là bình thường (API tìm metadata, web có thể tìm cả full-text); phải **ghi và giải thích** ở mục Kiểm chứng.

## 2. Dedup + gộp với 22 bản ghi cũ

Tab 3 **Kết quả**: giữ tick các bài vào 01. Bản ghi trùng DOI/tiêu đề với 22 bản đã có thì **giữ mã cũ `KD-SPR-01…22`**, chỉ bản mới giữ mã `KD-SPR-23…`. (Gửi 3 file export cho tôi để gộp tự động và tránh đếm sai.)

## 3. Screening V1 cho bản ghi MỚI (tab 4)

Đây là quyết định học thuật của K.Duy theo `ie_criteria.md` — tool chỉ gợi ý (cột Gợi ý). Bản ghi cũ giữ nguyên quyết định ở `02_after_screening_v1.csv`. Bài INCLUDE/Unsure → V2 đọc toàn văn.

## 4. Snowballing vòng 1

1. Đổi **Tiền tố mã = `KD-SNW-`**, **Bắt đầu từ số = `1`** (snowballing dùng dãy mã riêng, không lẫn với Springer).
2. Tab **Snowballing**: dán toàn bộ `snowball-seeds.txt` (13 DOI — là các paper ACM đã INCLUDE sau V2 của Lâm; mỗi dòng một DOI) vào ô seed.
3. Tick **lùi** và **tiến**; API: **OpenAlex** + **Semantic Scholar** (+ **Crossref** chỉ lùi). **Vòng = 1**, **Chỉ lấy bài từ năm = 2020**, **Tối đa mỗi seed/hướng = 500** → **Chạy snowballing**.
4. Thêm khi đủ điều kiện: (a) 4 paper dẫn chứng trên thẻ RQ — cần DOI (không có trong repo; lấy từ thẻ RQ); (b) `10.1109/ACCESS.2021.3056505` và `10.1109/MS.2025.3559664` của Tùng **sau khi nhóm xác nhận INCLUDE**.
5. Mọi bài mới vào 01 và đi V1 → V2 (IC-S5). Điền bảng Snowballing trong `search-log.md`: số đã lướt = số bản ghi tool trả theo từng seed/hướng; số thêm vào 01 = sau dedup.

## 5. Xuất file (tab 5) và kiểm chứng

Xuất: `01_all_records.csv`, `02_after_screening_v1.csv`, `03_final_included.csv`, `prisma-flow.md`, đoạn `search-log.md`, và dữ liệu thô `.json` (làm bằng chứng gốc, không chứa key). **Sao lưu** trạng thái screening (.json) sau mỗi buổi.

Ghi 3 phép kiểm RBL-1 vào mục "Kiểm chứng" của `search-log.md`: (1) số bản ghi khớp số web báo; (2) mở ngẫu nhiên 5 bản ghi, đối chiếu tiêu đề/năm/DOI với link.springer.com; (3) chạy lại 1 lượt (vd T1) ra cùng số.

## 6. Kiểm chéo (IC-S6)

Nhờ reviewer khác rà các mã trong bảng ở mục 6 của `search-log.md` (đề xuất 5 bài), ghi ngày + kết quả.

## 7. Gửi lại để hoàn thiện

Gửi: 3 file CSV export + `.json` thô + log tool (copy khung nhật ký). Từ đó điền mọi ô ⬜ trong `search-log.md`, `prisma-flow.md` và `evidence-table.md` bằng số thật, tự kiểm cộng trừ.

