## Nhật ký chạy query (tạo bởi RBL Paper Harvester)

| Lần | Chuỗi gửi đi (nguyên văn) | CSDL | Trường tìm | Bộ lọc | Ngày chạy | Số kết quả nguồn báo | Số lấy về | Ghi chú |
|---|---|---|---|---|---|---|---|---|
| V1 | `("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing") AND ("fault detection" OR "mutant detection" OR "bugs found")` | Springer Nature | q (metadata Springer Nature) | year ≥ 2020 (lọc sau khi lấy) | 16/10/2026 11:37 | 7 | 3 | ngoài 3 nguồn đếm PRISMA của protocol — hỏi PL trước khi đếm; bỏ 4 bản ghi trước năm 2020 (Springer không lọc năm trong query) |
| V2 | `("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing")` | Springer Nature | q (metadata Springer Nature) | year ≥ 2020 (lọc sau khi lấy) | 16/10/2026 11:38 | 18 | 10 | ngoài 3 nguồn đếm PRISMA của protocol — hỏi PL trước khi đếm; bỏ 8 bản ghi trước năm 2020 (Springer không lọc năm trong query) |
| V3 | `("REST API" OR "RESTful API" OR RESTest OR RESTestBench) AND ("equivalence partitioning" OR "equivalence class partitioning" OR "boundary value analysis" OR "boundary value testing" OR "boundary testing") AND ("fault detection" OR "faults found" OR "bug detection" OR "bugs found" OR defects OR failures OR "mutation testing" OR "mutation score" OR "mutant detection")` | Springer Nature | q (metadata Springer Nature) | year ≥ 2020 (lọc sau khi lấy) | 16/10/2026 11:38 | 18 | 18 | ngoài 3 nguồn đếm PRISMA của protocol — hỏi PL trước khi đếm |
| V4 | `("REST API" OR "RESTful API" OR "web API" OR "web service") AND ("boundary value analysis" OR "boundary value" OR "boundary testing" OR "equivalence partitioning") AND ("mutation testing" OR "mutants" OR "mutation score")` | Springer Nature | q (metadata Springer Nature) | year ≥ 2020 (lọc sau khi lấy) | 16/10/2026 11:38 | 40 | 12 | ngoài 3 nguồn đếm PRISMA của protocol — hỏi PL trước khi đếm; bỏ 28 bản ghi trước năm 2020 (Springer không lọc năm trong query) |
| V5 | `"REST API" AND "equivalence partitioning"` | Springer Nature | q (metadata Springer Nature) | year ≥ 2020 (lọc sau khi lấy) | 16/10/2026 11:39 | 10 | 10 | ngoài 3 nguồn đếm PRISMA của protocol — hỏi PL trước khi đếm |
| V6 | `"REST API" AND "boundary value analysis"` | Springer Nature | q (metadata Springer Nature) | year ≥ 2020 (lọc sau khi lấy) | 16/10/2026 11:39 | 10 | 10 | ngoài 3 nguồn đếm PRISMA của protocol — hỏi PL trước khi đếm |

## Snowballing

| Seed (DOI) | Vòng | Hướng | Qua API | Số đã lướt | Số thêm vào 01 | Số include cuối | Ghi chú |
|---|---|---|---|---|---|---|---|
| 10.2991/978-94-6239-805-4_13 | 1 | lùi | OpenAlex | 0 | 0 | 0 | OpenAlex ghi nhận 0 tài liệu tham khảo của seed |
| 10.2991/978-94-6239-805-4_13 | 1 | tiến | OpenAlex | 0 | 0 | 0 |  |
| 10.1007/978-3-032-05188-2_11 | 1 | lùi | OpenAlex | 10 | 10 | 1 | OpenAlex ghi nhận 14 tài liệu tham khảo của seed; không lấy 4 reference trước năm 2020 (hoặc OpenAlex không có) |
| 10.1007/978-3-032-05188-2_11 | 1 | tiến | OpenAlex | 2 | 2 | 0 |  |

## Tổng hợp

- Tổng trước dedup: 75 · Sau dedup: 47 (bỏ 28 bản trùng) · Đã chọn xuất vào 01: 47
- Ghi chú: bản ghi từ Semantic Scholar / Google Scholar (SerpAPI) KHÔNG đếm vào PRISMA theo review-protocol.md §3.
