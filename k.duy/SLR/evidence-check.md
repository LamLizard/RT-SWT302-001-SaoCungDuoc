# evidence-check — K.Duy · Mục E (Springer Nature)

**Phạm vi:** chỉ Bước 1 (kiểm tra 5 cổng P1–P5). Chưa làm Bước 2.
**Nguồn đối chiếu:** `team-synthesis/evidence-table-merged.md`, Mục E, 2 dòng của K.Duy: #41 (K02), #42 (K33). PDF gốc: `Paper-source/41-K02.pdf`, `Paper-source/42-K33.pdf`.
**P1** (≥ 12 paper) là cổng cấp nhóm, đã được thông qua, không xét lại ở đây.

## 1. Kết quả 5 cổng (trên 2 dòng của K.Duy)

| Cổng | Pass khi | Kết quả | Kết luận | Fail → làm gì |
|---|---|---|---|---|
| P1 | ≥ 12 paper included | — | Đã thông qua | — |
| P2 | Cột Tool/LLM: ≥ 90% hàng có dữ liệu | 2/2 (100%) | **Pass** (nên bổ sung model cho K02) | Đọc lại Section 3 |
| P3 | Cột Kết quả: ≥ 50% hàng có con số | 0/2 (0%) | **FAIL** | Đọc lại Table/Figure |
| P4 | Cột Hạn chế: ≥ 50% hàng có dữ liệu | 2/2, nhưng nội dung yếu | **Pass, nên sửa** | Đọc Threats to Validity / Future Work |
| P5 | Cột Metric: tên cụ thể | 2/2 | **Pass** (K02 nên cụ thể hơn) | Đọc lại Evaluation Metrics |

**Điều kiện sang Bước 2:** qua đủ 5 cổng. Hiện P3 đang Fail, nên chưa sang Bước 2 được cho đến khi sửa 2 dòng dưới đây.

## 2. Chi tiết từng dòng

### #41 · K02 — Test Amplification for REST APIs via Single and Multi-agent LLM Systems

Dòng hiện tại trong bảng gộp được lấy từ abstract.

| Cột | Đang ghi trong bảng gộp | Đối chiếu PDF | Cổng | Cần sửa |
|---|---|---|---|---|
| Tool/LLM | LLM đơn/đa tác tử khuếch đại test suite REST API | Có thêm model và khung: OpenAI GPT-4o mini (Sec. 6.4), đơn tác tử ReAct, đa tác tử LangGraph (Sec. 3, Fig. 1–2) | P2 | Bổ sung |
| Dataset | "REST API; không nêu số lượng/tên API" | **PetStore**, 20 endpoint, 3 lần chạy lấy trung bình (Sec. 4, 6.3) | — | **Sai**, sửa |
| Metric | API coverage; phát hiện bug; chi phí, năng lượng | Số test sinh/pass/fail/bug-exposing (Table 1); độ phủ cấu trúc API (Table 3); thời gian, token, chi phí, năng lượng (Table 4) | P5 | Làm cụ thể |
| Kết quả | "không nêu số cụ thể (abstract)" | Table 1: test sinh **118** (đơn) vs **145** (đa); bug-exposing **32 (27%)** vs **43 (30%)**. Table 3: phủ Parameter 11% → **56%** vs **82%**; Response Type **51%** vs **88%**; Request Type **73%** vs **97%**; Operation **95%** vs **100%**. Table 4: chi phí **$0,01848** vs **$0,05213**; thời gian **351 s** vs **1149 s**; năng lượng **4,27** vs **9,74 Wh** | P3 | **Fail**, điền số |
| Code | "Không nêu" | Có reproduction package (figshare) — theo evidence-table cá nhân; link: https://figshare.com/s/6c0d66b47181b0874305?file=56376179 | — | Cần sửa, xác nhận link |
| Hạn chế | "Không nêu số liệu, danh sách API và chi tiết baseline" (đây là chỗ bài thiếu thông tin, không phải hạn chế tác giả nêu) | Sec. 6: (6.1) coverage cao không đảm bảo test đúng phần quan trọng, mọi bug tính ngang nhau; (6.2) LLM có thể đã biết PetStore; (6.3) chỉ 1 ứng dụng; (6.4) LLM không tất định, chỉ 1 model, chấm khả đọc bằng đánh giá chủ quan của tác giả | P4 | Thay bằng hạn chế thật |

### #42 · K33 — Integrated Executive Dashboard, PPMPP Portal (Politeknik Negeri Bali)

| Cột | Đang ghi trong bảng gộp | Đối chiếu PDF | Cổng | Cần sửa |
|---|---|---|---|---|
| Tool/LLM | Black-box testing với EP; RESTful APIs, JSON | Khớp | P2 | Giữ |
| Dataset | PPMPP Portal; 14 người trả lời | Khớp: IPA có 14 người từ 7 khoa | — | Giữ |
| Metric | Hoàn thành kịch bản chức năng định trước; IPA | Khớp. Nên viết rõ: tỉ lệ kịch bản đạt; IPA (Importance–Performance Analysis) | P5 | Viết rõ viết tắt |
| Kết quả | "Toàn bộ kịch bản định trước chạy thành công; chưa đánh giá định lượng" | Fig. 5: toàn bộ kịch bản đạt, tỉ lệ đạt **100%**. Fig. 6: IPA độ quan trọng trung bình **4,47**, hiệu năng cảm nhận **4,20**. Cụm "chưa đánh giá định lượng" **không đúng**, bài có số | P3 | **Fail**, điền số, bỏ cụm sai |
| Code | Không nêu | Chưa thấy trong PDF | — | Giữ |
| Hạn chế | "Không nêu số kịch bản; không outcome về mutant" (nhận xét của người chấm, không phải của tác giả) | Phần Discussion/Limitations: 100% chỉ là tỉ lệ đạt kịch bản định trước, không chứng minh khả năng mở rộng hay hiệu năng; IPA chỉ 14 người, là đánh giá ban đầu; không đo response time, throughput, số người dùng đồng thời, tài nguyên server | P4 | Thay bằng hạn chế thật |

## 3. Chưa kiểm chứng

- Số trang của K33 và bản LNCS chính thức của K02: chưa đối chiếu, cần kiểm nếu dẫn số trang.
- Link figshare của K02: chưa xác nhận trực tiếp trong PDF.
- Số liệu K02 trong bảng này lấy từ PDF trong `Paper-source/41-K02.pdf`.
- Bước 2: chưa làm, chờ hướng dẫn Bước 2.

## 4. Tổng thay đổi 

| # | Mã (gộp) | Paper (tên + năm + venue + DOI) | Nguồn | Tool/LLM | Dataset | Metric | Kết quả | Code | Hạn chế | Gần RQ |
|---|---|---|---|---|---|---|---|---|---|---|
| 41 | K02 | **Test Amplification for REST APIs via Single and Multi-agent LLM Systems** (2026, Testing Software and Systems) · DOI 10.1007/978-3-032-05188-2_11 | K.Duy · Springer | LLM đơn/đa tác tử khuếch đại test suite REST API, OpenAI GPT-4o mini (Sec. 6.4), đơn tác tử ReAct, đa tác tử LangGraph (Sec. 3, Fig. 1–2) | PetStore, 20 endpoint, 3 lần chạy lấy trung bình (Sec. 4, 6.3) | Số test sinh/pass/fail/bug-exposing (Table 1); độ phủ cấu trúc API (Table 3); thời gian, token, chi phí, năng lượng (Table 4) | Table 1: test sinh 118 (đơn) vs 145 (đa); bug-exposing 32 (27%) vs 43 (30%). Table 3: phủ Parameter 11% → 56% vs 82%; Response Type 51% vs 88%; Request Type 73% vs 97%; Operation 95% vs 100%. Table 4: chi phí $0,01848 vs $0,05213; thời gian 351 s vs 1149 s; năng lượng 4,27 vs 9,74 Wh |Có reproduction package (figshare) — theo evidence-table cá nhân; link: https://figshare.com/s/6c0d66b47181b0874305?file=56376179| Sec. 6: (6.1) coverage cao không đảm bảo test đúng phần quan trọng, mọi bug tính ngang nhau; (6.2) LLM có thể đã biết PetStore; (6.3) chỉ 1 ứng dụng; (6.4) LLM không tất định, chỉ 1 model, chấm khả đọc bằng đánh giá chủ quan của tác giả | 0/4 ✓ · chạm 1/4 (◐ O) |
| 42 | K33 | **Implementation of an Integrated Executive Dashboard on the PPMPP Portal as a Digital Instrument for Institutional Quality Assurance at Politeknik Negeri Bali** (2026, ICOSTAS-EAS) · DOI 10.2991/978-94-6239-805-4_13 | K.Duy · Springer | Black-box testing với **EP**; RESTful APIs, JSON | PPMPP Portal (e-Monev/e-AMI); 14 người trả lời | Hoàn thành kịch bản chức năng định trước; IPA (Importance–Performance Analysis) | Fig. 5: toàn bộ kịch bản đạt, tỉ lệ đạt 100%. Fig. 6: IPA độ quan trọng trung bình 4,47, hiệu năng cảm nhận 4,20. Cụm "chưa đánh giá định lượng" không đúng, bài có số | Không có  | Phần Discussion/Limitations: 100% chỉ là tỉ lệ đạt kịch bản định trước, không chứng minh khả năng mở rộng hay hiệu năng; IPA chỉ 14 người, là đánh giá ban đầu; không đo response time, throughput, số người dùng đồng thời, tài nguyên server | 0/4 ✓ · chạm 2/4 (◐ P, I) |
