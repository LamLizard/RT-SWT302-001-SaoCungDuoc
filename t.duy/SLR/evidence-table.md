# Evidence Table — T.Duy (Semantic Scholar + Google Scholar)

Tự rà soát: **18/10/2026**. Chỉ ghi **2 bài Include**; số liệu đối chiếu với toàn văn và bảng kết quả.

**Tự kiểm P2–P5 ngày 18/10/2026 — 2 bài Include:**

| Cổng | Yêu cầu | Kết quả cá nhân |
|---|---|---|
| P2 · Tool/LLM | ≥90% hàng có dữ liệu | **Đạt: 2/2 (100%)**. RestTSLLM/8 LLM; GPT-4 + bộ sinh Python G |
| P3 · Kết quả | ≥50% hàng có con số | **Đạt: 2/2 (100%)**. Table 3 của từng bài, lần lượt PDF p8 và p6; số gắn đúng model, baseline và metric |
| P4 · Hạn chế | ≥50% hàng có dữ liệu | **Đạt: 2/2 (100%)**. Hạn chế tác giả nêu, có mục/trang; tách riêng nhận xét của người đọc |
| P5 · Metric | Tên cụ thể, có đơn vị/ý nghĩa | **Đạt: 2/2**. Mutation score (%), branch coverage (%), test success rate (%); C(T) là tỷ lệ yêu cầu chức năng được bao phủ (%) |

P1 (≥12 Include) xét trên **bảng gộp nhóm**, không áp thành chỉ tiêu 12 bài cho cá nhân. Kết quả trên là tự kiểm nội dung; kiểm chéo độc lập vẫn chờ xác nhận.

| # | Paper (tên + năm + DOI) | Tool/LLM | Dataset | Metric | Kết quả | Code | Hạn chế | Gần RQ |
|---|---|---|---|---|---|---|---|---|
| 1 | [Combining TSL and LLM to Automate REST API Testing: A Comparative Study](https://doi.org/10.5753/sbes.2025.9670) (2025, SBES 2025; DOI: 10.5753/sbes.2025.9670) | RestTSLLM; 8 LLM từ xa; Category-Partition/TSL → .NET/xUnit; Stryker.NET Advanced (§3/p 4, §4.6/pp 7–8) | 6 REST API .NET: todo, supermarket, books, hotels, restaurants, shortener (Table 2, PDF p 7) | Stryker.NET mutation score (%); branch coverage (%); test success rate (%) (§4.3, PDF p 6) | Claude 3.5 Sonnet, trung bình trên 6 dự án: mutation score **40,8%**; branch coverage **71,7%**; success rate **100%** (Table 3, PDF p 8) | [Code, prompts và tests](https://github.com/uffsoftwaretesting/RestTSLLM/tree/4e0a93e55131e18592623bfdd2999e206d540cb4) | Tác giả nêu: 6 dự án .NET, đánh giá thủ công, temperature=1 và prompt bias (§6, pp 9–10). Nhận xét đối chiếu: EP/BVA ở prompt chưa có ablation riêng hoặc uniform random cùng request budget; mutation score chưa tách unique mutants theo dạng yêu cầu | Gián tiếp: REST request + EP/BVA + mutation score; không phải 45 yêu cầu RESTestBench |
| 2 | [Development and verification of an orchestration architecture of AI agents for automated API testing with a unified representation of requirements](https://doi.org/10.15587/2706-5448.2026.360928) (2026, Technology Audit and Production Reserves, 3(2(89)); DOI: 10.15587/2706-5448.2026.360928) | GPT-4 (gpt-4-0125-preview) trích yêu cầu; G là Python sinh EP+BVA xác định, không gọi LLM (§3.2, PDF pp 5–6) | 1 FastAPI: 5 endpoints, 18 tham số, 24 response schemas; OpenAPI + 12 business rules văn bản → 42 yêu cầu chức năng; 20 lần chạy/mỗi cách (§2.2–2.3, PDF p 3) | C(T), % yêu cầu chức năng được ≥1 scenario bao phủ; không phải branch coverage (§2.3, PDF p 3) | C(T) trung bình: kiến trúc tích hợp **90,2%**; chỉ OpenAPI **75,1%**; GPT-4 từ tài liệu **68,3%** (Table 3/Fig. 2, PDF p 6, trang in 36) | NOT_REPORTED: không thấy URL mã nguồn/replication của prototype hoặc SUT trong PDF; GitHub Issues là nguồn yêu cầu trong thiết kế | Tác giả nêu: 1 API nhỏ, 1 model; issue agent chưa thử; LLM làm R biến đổi, G chỉ xác định khi R cố định (pp 6–8). Nhận xét đối chiếu: baseline thiếu 3 business rules nên không quy chênh coverage riêng cho EP/BVA; không uniform-random hoặc mutant outcome | Gián tiếp: NL + OpenAPI → EP+BVA cho HTTP requests; outcome là coverage yêu cầu, không phải unique mutants |

Số trang PDF tính từ trang đầu file. Tài liệu đối chiếu: bảng tái xây dựng 42 PDF ngày 16/10, hàng 39–40 và explain cùng số; đã mở lại PDF, không sao chép các cột Evidence vào bảng nộp. Code/artifact chưa chạy tái lập trong lượt này. Mutation score, branch coverage và coverage yêu cầu không thay cho số mutant riêng biệt được oracle xác nhận; hai bài chưa kiểm định trực tiếp H0/H1 của RQ.

Snowballing: 1 vòng từ TD-0002 · 10.5753/sbes.2025.9670; 84 lượt lùi + 7 lượt tiến → 63 bài mới sau bỏ trùng → **0 Include mới**. L2 ngày 18/10 thêm 1 citation từ K191, loạiV2 IC-I; tổng snowball 92 lượt, đóng góp 64 bài mới, vẫn 0 Include mới. Tổng: **2 search + 0 snowball = 2 Include**, khớp 03 và PRISMA.

Đính chính explain #40: Table 5, PDF p 7 của TD-0015 ghi M_maint **65,7% specification / 46,7% GPT-4 / 17,7% tích hợp**. Cụm “17,7% so LLM 65,7%” trong tài liệu tham khảo bị nhầm baseline; không dùng làm kết quả.

Đối soát 18/10:01/02=136 paper(175 lượt−39 trùng); Include 03/evidence/luồng cá nhân=2/2/2. Tìm kết quả âm bổ sung 17 lượt không có Include mới. Kiểm chéo độc lập:CHỜ; tự rà không thay xác nhận thành viên khác.
