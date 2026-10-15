# Evidence Table — T.Duy (Semantic Scholar + Google Scholar)

**2 bài Include.** Các bài loại/chờ và lịch sử thẩm định xem file 02; chỉ trích bằng chứng của bài Include trong bảng này.

| # | Paper (tên + năm + DOI) | Tool/LLM | Dataset | Metric | Kết quả | Code | Hạn chế | Gần RQ |
|---|---|---|---|---|---|---|---|---|
| 1 | Combining TSL and LLM to Automate REST API Testing: A Comparative Study (2025, DOI: 10.5753/sbes.2025.9670) | RestTSLLM; 8 LLM | 6 dự án REST API | Mutation score; branch coverage; success rate | Claude 3.5 Sonnet: 40,8%; 71,7%; 100% tương ứng (Table 3, p8). | [GitHub](https://github.com/uffsoftwaretesting/RestTSLLM/tree/4e0a93e55131e18592623bfdd2999e206d540cb4) | EP/BVA ở prompt và HTTP tests (§3, p4); chưa có ablation, random cùng budget hoặc số mutant riêng biệt. | P ✓; I ✓ EP/BVA; O: mutation score, chưa phải unique mutants |
| 2 | Development and verification of an orchestration architecture of AI agents for automated API testing with a unified representation of requirements (2026, DOI: 10.15587/2706-5448.2026.360928) | GPT-4 trích yêu cầu; G sinh EP+BVA | FastAPI: 5 endpoints, 18 tham số; 20 lần chạy | Coverage yêu cầu C(T), % | phương pháp 90,2%; specification 75,1%; LLM 68,3% (Table 3, p6). | Chưa xác minh | Một service; chưa có random cùng budget hoặc số mutant riêng biệt. | P ✓; I ✓ EP+BVA; O: coverage yêu cầu, chưa phải unique mutants |

Snowballing: 1 vòng từ RestTSLLM; 84 lượt lùi + 7 lượt tiến, 63 bài mới sau bỏ trùng; 0 Include mới. Chi tiết: search-log.md.

Hai bài trên là Include, nguồn Google Scholar. Bài loại/Unsure xem 02_after_screening_v1.csv. Không thay unique mutants bằng mutation score/coverage.
