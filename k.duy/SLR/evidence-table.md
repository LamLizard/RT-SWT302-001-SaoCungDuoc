# Evidence table — K.Duy (Springer Nature)

| # | Mã (gộp) | Paper (tên + năm + venue + DOI) | Nguồn | Tool/LLM | Dataset | Metric | Kết quả | Code | Hạn chế | Gần RQ |
|---|---|---|---|---|---|---|---|---|---|---|
| 41 | K02 | **Test Amplification for REST APIs via Single and Multi-agent LLM Systems** (2026, Testing Software and Systems) · DOI 10.1007/978-3-032-05188-2_11 | K.Duy · Springer | LLM đơn/đa tác tử khuếch đại test suite REST API, OpenAI GPT-4o mini (Sec. 6.4), đơn tác tử ReAct, đa tác tử LangGraph (Sec. 3, Fig. 1–2) | PetStore, 20 endpoint, 3 lần chạy lấy trung bình (Sec. 4, 6.3) | Số test sinh/pass/fail/bug-exposing (Table 1); độ phủ cấu trúc API (Table 3); thời gian, token, chi phí, năng lượng (Table 4) | Table 1: test sinh 118 (đơn) vs 145 (đa); bug-exposing 32 (27%) vs 43 (30%). Table 3: phủ Parameter 11% → 56% vs 82%; Response Type 51% vs 88%; Request Type 73% vs 97%; Operation 95% vs 100%. Table 4: chi phí $0,01848 vs $0,05213; thời gian 351 s vs 1149 s; năng lượng 4,27 vs 9,74 Wh |Có reproduction package (figshare); link: https://figshare.com/s/6c0d66b47181b0874305?file=56376179| Sec. 6: (6.1) coverage cao không đảm bảo test đúng phần quan trọng, mọi bug tính ngang nhau; (6.2) LLM có thể đã biết PetStore; (6.3) chỉ 1 ứng dụng; (6.4) LLM không tất định, chỉ 1 model, chấm khả đọc bằng đánh giá chủ quan của tác giả | 0/4 ✓ · chạm 1/4 (◐ O) |
| 42 | K33 | **Implementation of an Integrated Executive Dashboard on the PPMPP Portal as a Digital Instrument for Institutional Quality Assurance at Politeknik Negeri Bali** (2026, ICOSTAS-EAS) · DOI 10.2991/978-94-6239-805-4_13 | K.Duy · Springer | Black-box testing với **EP**; RESTful APIs, JSON | PPMPP Portal (e-Monev/e-AMI); 14 người trả lời | Hoàn thành kịch bản chức năng định trước; IPA (Importance–Performance Analysis) | Fig. 5: toàn bộ kịch bản đạt, tỉ lệ đạt 100%. Fig. 6: IPA độ quan trọng trung bình 4,47, hiệu năng cảm nhận 4,20. | Không có  | Phần Discussion/Limitations: 100% chỉ là tỉ lệ đạt kịch bản định trước, không chứng minh khả năng mở rộng hay hiệu năng; IPA chỉ 14 người, là đánh giá ban đầu; không đo response time, throughput, số người dùng đồng thời, tài nguyên server | 0/4 ✓ · chạm 2/4 (◐ P, I) |




### Truy Vấn / Kết quả / Quyết định    trong bước 2 rq-check .
| # | Truy vấn | Kết quả | Quyết định |
|---|---|---|---|
| 1 | `RESTestBench LLM-generated REST API test cases natural language requirements mutation benchmark` | Bài RESTestBench (arXiv 2604.25862), gợi ý Vibe Testing | Giữ cả hai (cùng benchmark/metric) |
| 2 | `boundary value analysis equivalence partitioning REST API random testing 2026` | Chủ yếu blog; 1 bài học thuật từ 2020 (arXiv 2001.06652) | Loại: ngoài 12 tháng gần nhất |
| 3 | `Assessing REST API Test Generation Strategies with Log Coverage` | arXiv 2604.07073 | Giữ (cùng bài toán REST API, 04/2026) |