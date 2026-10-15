# Search log — T.Duy · Semantic Scholar + Google Scholar

## 1. Nhật ký query

| Lần | Chuỗi thực chạy (nguyên văn) | CSDL | Trường/bộ lọc | Ngày | Kết quả nguồn / thực thu | Ghi chú |
|---|---|---|---|---|---|---|
| S2-A (exact) | `("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing") AND ("fault detection" OR "mutant detection" OR "bugs found")` | Semantic Scholar | Tìm mặc định | 15/10/2026 | Site báo không khớp / 0 | 250 là số gợi ý sau nới, không phải exact A. |
| GS-A | `("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing") AND ("fault detection" OR "mutant detection" OR "bugs found")` | Google Scholar | Mặc định; IC-Y≥2020 áp khi lọc | 15/10/2026 | 27 (ước lượng đầu 37) | Đã lấy hết 27; trang tiếp theo 0. |
| S2-A-relaxed | `(REST API testing OR natural language requirement OR RESTestBench) AND (equivalence partitioning OR boundary-value analysis OR boundary testing) AND (fault detection OR mutant detection OR bugs found)` | Semantic Scholar | Mặc định; IC-Y≥2020 áp khi lọc | 15/10/2026 | 250 gợi ý / thu 10 | Site không khớp exact A, tự bỏ dấu nháy; chưa lấy hết gợi ý. |
| S2-seed | `"Combining TSL and LLM to Automate REST API Testing"` | Semantic Scholar | Mặc định; IC-Y≥2020 áp khi lọc | 15/10/2026 | 1 / thu 1 | Tra title seed; bản trùng vẫn ghi 01. |
| GS-B-random | `("REST API" OR "RESTful API") ("equivalence partitioning" OR "boundary value") random` | Google Scholar | Mặc định; IC-Y≥2020 áp khi lọc | 15/10/2026 | khoảng 206 / thu 10 | Mới lấy trang đầu. |
| S2-B-random | `REST API equivalence partitioning boundary value random` | Semantic Scholar | Mặc định; IC-Y≥2020 áp khi lọc | 15/10/2026 | 25 / thu 10 | Mới lấy trang đầu; không coi TLDR là abstract. |
| GS-MacroHive | `"Automated functional and robustness testing of microservice architectures"` | Google Scholar | Mặc định; IC-Y≥2020 áp khi lọc | 15/10/2026 | thu 1 | Tra cứu title từ đầu mối; không tạo nguồn mới ngoài GS. |
| GS-budget | `("REST API" OR "RESTful API") "equivalence partitioning" "boundary value" "budget" "random"` | Google Scholar | Mặc định; IC-Y≥2020 áp khi lọc | 15/10/2026 | 7 / thu 7 | Đã lấy hết 7 kết quả. |

## 2. Xử lý dữ liệu

Search/seed: 27+10+1+10+10+1+7=66 lượt → 61 bài sau bỏ trùng. Snowballing: 91 lượt → 63 bài mới. Tổng 01/02: 157 dòng; trùng EC-D 33; unique 124.

Giữ nguyên metadata nguồn và canonical_id trong 01/02. DOI/publisher/Crossref/OpenAlex và các lượt tìm lại full-text chỉ để xác minh; không cộng thành discovery mới. Không suy ra EC-A từ HTTP403/429/timeout. Bài loại/chờ giữ trong02; 03 chỉ Include.

## 3. Nới chuỗi và cập nhật toàn văn

Giữ nguyên String A ở GS-A và S2-A. S2 tự bỏ dấu nháy được ghi riêng; các query random/budget và title lookup ghi đúng chuỗi thực chạy ở bảng trên. Không sửa IC/EC; không đổi hạn search theo mẫu của Lâm.

Trạng thái cuối 15/10/2026: FAMRES chưa có toàn văn; Agentic có PDF nhưng chưa xác minh journal/conference (IC-T). Cả hai giữ Unsure. Có52PDF+4bản text đã đọc; hai bài Include được giữ nguyên.

## 4. Snowballing — vòng 1

Seed TD-0002 · 10.5753/sbes.2025.9670 · RestTSLLM (SBES2025): đã có PDF11trang và Include; sát Category-Partition/EP/BVA, có mutation metric. References từ S2 và PDF; citations từ GS và S2. Không chạy tiếp từ bài mới.

| Seed DOI | Vòng | Hướng | Số đã lướt/ghi nhận | Số thêm vào 01 | Include mới |
|---|---:|---|---:|---:|---:|
| 10.5753/sbes.2025.9670 | 1 | Lùi | 84 | 84 | 0 |
| 10.5753/sbes.2025.9670 | 1 | Tiến | 7 | 7 | 0 |

Lùi: S2 thu27 references (header50; chưa lấy đủ50) +57 entries trong References PDF. Tiến: GS2 +S2 5 citations. Cùng bài có thể lặp giữa nguồn; các số84/7 là lượt trước bỏ trùng.

Snowballing 91 lượt → 64 unique trong nhánh; giao search1 → mới63. Lọc: 63−36=27 đọc toàn văn; loạiV2 27; Include mới0. Search61+snowball mới63=124.

Số Include cuối và các lý do loại theo từng nhánh: prisma-flow.md; quyết định từng ID: 02_after_screening_v1.csv.
