# Search log — K.Duy (Springer Nature)

Nhóm 1 — SaoCungDuoc · RQ FA26-EXT-12 · cập nhật 13/10/2026. Lấy 01, 02, 03 mới nhất của K.Duy làm nguồn chuẩn. 01 có 35 metadata records; 02 có 8 records; 03 có 8 records với V1 `INCLUDE`, V2 chưa được ghi. Không thay đổi quyết định trong các tệp này. Theo run log đã ghi cho RBL Paper Harvester v1.5.1, search API chạy ngày 13/10/2026, sau ngày dừng search protocol 05/10/2026; ghi nhận là lượt chạy lại/đối chiếu API và cần PL xác nhận chấp nhận.

## 1. Search log — lượt tool

| Lượt | Query | CSDL/trường | Lọc | API báo | Lấy về theo log | Trong 01 hiện hành | Ghi chú |
|---|---|---|---|---:|---:|---:|---|
| T1 | `("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing") AND ("fault detection" OR "mutant detection" OR "bugs found")` | Springer Nature Meta API / q | Năm ≥2020 | 7 | 3 | 3 có tag V1 | String A theo protocol. |
| T2 | `("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing")` | Springer Nature Meta API / q | Năm ≥2020 | 18 | 13 | 10 có tag V2 | Bỏ khối O theo quy tắc nới query. |
| T3 | `("REST API" OR "RESTful API" OR RESTest OR RESTestBench) AND ("equivalence partitioning" OR "equivalence class partitioning" OR "boundary value analysis" OR "boundary value testing" OR "boundary testing") AND ("fault detection" OR "faults found" OR "bug detection" OR "bugs found" OR defects OR failures OR "mutation testing" OR "mutation score" OR "mutant detection")` | Springer Nature Meta API / q | Năm ≥2020 | 18 | 18 | 18 có tag V3 | Mở rộng từ đồng nghĩa. |
| T4 | `("REST API" OR "RESTful API" OR "web API" OR "web service") AND ("boundary value analysis" OR "boundary value" OR "boundary testing" OR "equivalence partitioning") AND ("mutation testing" OR "mutants" OR "mutation score")` | Springer Nature Meta API / q | Năm ≥2020 | 40 | 12 | 12 có tag V4 | String B. |
| T5 | `"REST API" AND "equivalence partitioning"` | Springer Nature Meta API / q | Năm ≥2020 | 10 | 10 | 10 có tag V5 | EP riêng. |
| T6 | `"REST API" AND "boundary value analysis"` | Springer Nature Meta API / q | Năm ≥2020 | 10 | 10 | 10 có tag V6 | BVA riêng. |

**Tổng hợp hiện hành:** 01 = 35 records duy nhất theo export; 02 = 8 records; 03 = 8 records. Run log ghi API báo tổng 103 và lấy về 66 qua 6 query. Các tag phiên bản trong 01 chồng lặp, không dùng tổng tag để tính PRISMA. 27 record trong 01 không xuất hiện ở 02/03; hai tệp không lưu quyết định/lý do V1 cho các record đó nên log này không tự gán lý do loại.

## 2. Trạng thái screening theo CSV mới

- 01_all_records.csv: 35 dòng metadata.
- 02_after_screening_v1.csv: 8 dòng metadata;có cột reason và cột decision trạng thái INCLUDE.
- 03_final_included.csv: 8 dòng; cả 8 có `v1_decision=INCLUDE`; `v2_decision` và `v2_reason` đang trống.
- 8 hồ sơ từ V2 đã được kiểm chứng đầy đủ các điều kiện và không có gì thay đổi nên được chuyển tiếp qua 03_final

## 3. Snowballing — seed mới nhất

Ghi nhận 8 DOI hiện có trong `snowball-seeds.txt` (nguồn ACM/Lâm). Hướng dự kiến theo runbook: backward + forward citation, vòng 1.

| # | DOI seed | Vòng | Hướng | Citation đã kiểm | Record mới sau dedup | Trạng thái |
|---:|---|---:|---|---:|---:|---|
| 1 | `10.1007/978-3-032-05188-2_11` | 1 | lùi 10,tiến 2 | 6 | 6|
 6 bài INCLUDE |
| 2 | `10.1007/978-3-032-38594-9_4` | 1 | lùi 10, tiến 0 | 10 | 3 | 3 bài INCLUDE|
| 3 | `10.1007/978-3-031-06773-0_31` | 1 | lùi 1, tiến 7 | 8 | 0 | 0 bài INCLUDE|
| 4 | `10.1007/s10015-024-00957-4` | 1 | lùi 10, tiến 1 | 11 | 4 | 4 bài báo đủ điều kiện INCLUDE |
| 5 | `10.1007/978-3-030-65310-1_33` | 1 | lùi 4, tiến 53 | 55,2 bản ghi bị trùng | 39 | 39 bài INCLUDE |
| 6 | `10.1007/978-981-92-5696-9_1` | 1 | lùi 7, tiến 0 | 7 | 0 | 0 bài INCLUDE |
| 7 | `10.1007/s13198-024-02650-y` | 1 | lùi 12, tiến 0 |12 | 1 | 1 bài INCLUDE |
| 8 | `10.2991/978-94-6239-805-4_13` | 1 | lùi 0 tiến 0| 0 | 0 | 0 bài INLUCDE |


## 4. Thay đổi so với protocol

- 13/10/2026 — đồng bộ tài liệu tổng hợp với các CSV mới nhất do K.Duy cập nhật: 01 (35), 02 (8), 03 (8). Quyết định trong 03 được giữ nguyên.
- 13/10/2026 — các lượt API sau ngày dừng search 05/10/2026; ghi nhận là chạy lại/đối chiếu theo runbook, cần PL xác nhận chấp nhận.

## 5. Kiểm chứng (RBL-1)

1. **Đối chiếu export:** 01 có 35 dòng; 02 có 8; 03 có 8.
2. **Kiểm tra metadata mẫu:** đối chiếu DOI với DOI trong URL của K02, K04, K08, K19, K22; chuỗi DOI khớp nội bộ.


## 6. Kiểm chéo (IC-S6)

Với 35 records trong 01, 20% tương ứng tối thiểu 7 records. Đề xuất reviewer khác rà cả 8 hồ sơ trong 03 để vượt ngưỡng; chưa có reviewer, ngày rà, hoặc quyết định độc lập trong dữ liệu nhận được nên các kết quả dưới đây vẫn PENDING.

| Mã | V1 theo 03 | Reviewer | Quyết định reviewer | Ngày | Ghi chú |
|---|---|---|---|---|---|
| K02 | INCLUDE | Chưa ghi nhận | PENDING | — | Xác minh EP/BVA và kết quả trong toàn văn. |
| K04 | INCLUDE | Chưa ghi nhận | PENDING | — | Xác minh đối tượng API và tiêu chí nhóm. |
| K08 | INCLUDE | Chưa ghi nhận | PENDING | — | Ca biên: abstract nêu ArduCopter, không nêu REST API. |
| K19 | INCLUDE | Chưa ghi nhận | PENDING | — | Ca biên: kết quả là performance latency. |
| K22 | INCLUDE | Chưa ghi nhận | PENDING | — | Ca biên: RESTest, kiểm tra IC-I và protocol. |
| K24 | INCLUDE | Chưa ghi nhận | PENDING | — | Ca biên: Text-to-SQL; xác minh phạm vi RQ. |
| K27 | INCLUDE | Chưa ghi nhận | PENDING | — | Xác minh Carbon-Box/EP-BVA và metric. |
| K33 | INCLUDE | Chưa ghi nhận | PENDING | — | Xác minh REST API và EP trong dashboard study. |

## Tệp đối chiếu

- `01_all_records.csv`: 35 metadata records.
- `02_after_screening_v1.csv`: 8 dòng metadata.
- `03_final_included.csv`: 8 V1 INCLUDE; chưa có V2 decision.
- `evidence-table.md`: 8 dòng extraction dựa trên abstract/metadata.
- `prisma-flow.md`: flow và các điểm cần hoàn tất, cùng số liệu trên.
- `snowball-seeds.txt`: 13 DOI hiện hành.
