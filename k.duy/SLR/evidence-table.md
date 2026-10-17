# Evidence table — K.Duy (Springer Nature + snowballing vòng 1)

Cập nhật ngày 17/10 , evidence-table check lại được lưu lại ở mục 4. Check lại EVIDENCE-TABLE 

## 0. Đọc trước: những gì đã đổi so với bản cũ

| # | Bản cũ | Nguồn đối chiếu | Xử lý trong bản này |
|---|---|---|---|
| 1 | Liệt kê **8 bài** included (K02, K04, K08, K19, K22, K24, K27, K33) | `03_final_included.csv`: cột `v2_decision` có **4 INCLUDE** (K02, K22, K33, K39) và **5 EXCLUDE EC-A** (K04, K08, K19, K24, K27). `prisma-flow.md` ghi tổng included = 4 | Bảng chính chỉ giữ 4 bài. 5 bài kia chuyển xuống **Phụ lục A** (loại ở V2, chưa đọc full text) |
| 2 | **Thiếu K39** (Kim et al., ISSTA 2022) | K39 là INCLUDE ở 03 (snowball-back từ seed K02) | Đã thêm |
| 3 | Ghi `v2_decision`/`v2_reason` "để trống có chủ đích" | Thực tế 03 có điền đủ cả 9 dòng | Bỏ câu này |
| 4 | Dữ liệu chỉ từ abstract, nhiều ô "Không nêu" | Có toàn văn 4 bài | Điền số liệu, ghi vị trí trích để kiểm chứng |

**Giả định về RQ.** Zip không có `review-protocol.md`. Mình suy RQ từ mã sàng lọc (IC-P, IC-I, EC-N, EC-A, IC-T), ghi chú v1 và chuỗi tìm kiếm: *kỹ thuật sinh input hộp đen cho REST API (EP / BVA / ràng buộc) so với đối chứng ngẫu nhiên hoặc fuzzing, đo bằng khả năng phát hiện lỗi hoặc mutant*. Nếu RQ chính thức khác, mục 2 và cột "Liên hệ RQ" cần chấm lại.

**Lưu ý lệch với lượt trước.** Ở lượt trước mình đã giả định RQ thiên về LLM, nên chấm K02 là 4/4. Với RQ suy ra từ file của bạn (EP/BVA/ràng buộc), K02 chỉ còn 2/4 (xem mục 2).

## 1. Bảng chính

| Mã | Paper (năm; venue; DOI) | Tool / kỹ thuật | Dataset / đối tượng | Metric | Kết quả chính | Code | Hạn chế | Liên hệ RQ; trạng thái |
|---|---|---|---|---|---|---|---|---|
| K02 | Test Amplification for REST APIs via Single and Multi-agent LLM Systems (2026; LNCS 16107, ICTSS 2025, tr. 161–177; [10.1007/978-3-032-05188-2_11](https://doi.org/10.1007/978-3-032-05188-2_11)) | Khuếch đại test suite có sẵn bằng LLM (GPT-4o mini, temperature 0, LangGraph). **Đơn tác tử**: ReAct agent + 2 tool (OpenAPI Retriever, Local Executor). **Đa tác tử**: pipeline OpenAPI, Header, Parameter, Value, Planner, Test Writer, Executor, Repair | **PetStore** (20 endpoint, JSON/XML). Đầu vào là 1 test happy-path; chạy 3 lần lấy trung bình | Số test (sinh / pass / fail / bug-exposing); độ phủ cấu trúc API qua Restats (path, operation, status class, status, response type, request type, parameter); token, thời gian, chi phí, năng lượng; khả đọc (checklist) | Test sinh: **118** (đơn) vs **145** (đa). Bug-exposing: **32** (27%) vs **43** (30%). Phủ tham số: 11% (ban đầu) → **56%** vs **82%**; request type 73% vs 97%; response type 51% vs 88%; operation 95% vs 100%. Chi phí: $0,0185 vs $0,0521; thời gian 351 s vs 1149 s; năng lượng 4,27 vs 9,74 Wh | Có: reproduction package (figshare `15158c0adf43b5410188`); web appendix (figshare `6c0d66b47181b0874305`) | Chỉ 1 ứng dụng (PetStore), LLM có thể đã biết PetStore; phân loại test do 1 tác giả làm, 1 người kiểm lại; 1 mô hình duy nhất; mọi bug tính ngang nhau; chưa có vòng phản hồi độ phủ (Restats chưa tự động) | Có REST API + phát hiện bug. **Không có EP/BVA làm biến can thiệp** (biên chỉ xuất hiện trong prompt của Value Agent); đối chứng là agent đơn do nhóm tự xây, không phải random/fuzzing. Ghi chú v1 đã cảnh báo IC-I. Included (V2: tải được PDF) |
| K22 | RESTest: Black-Box Constraint-Based Testing of RESTful Web APIs (2020; LNCS 12571, ICSOC 2020, tr. 459–475; [10.1007/978-3-030-65310-1_33](https://doi.org/10.1007/978-3-030-65310-1_33)) | RESTest (mô hình hoá, IDL + IDLReasoner/MiniZinc). **Constraint-based testing (CBT)** vs **random testing (RT)**; 5 oracle (5XX, OAS, 2XXP, 2XXD, 4XX); sinh test bằng REST Assured | **9 service từ 6 API thương mại** (Foursquare, GitHub, Stripe ×2, Tumblr, Yelp, YouTube ×3); 1.000 test nominal + 1.000 test lỗi cho mỗi SUT và mỗi kỹ thuật | % test hợp lệ; thời gian sinh; số failure theo từng oracle | Test hợp lệ: RT **40,1%** (1,3%–89%) vs CBT **85,4%** (99,7% khi bổ sung ràng buộc thiếu). Failure: **4.278** (CBT, 9/9 service) vs **2.920** (RT, 5/9). Hai oracle mới (2XXD + 4XX) tìm 2.063 failure ở 8/9 service. Thời gian sinh: 104,5 s vs 2,0 s. Stripe-CP: RT >10 giờ và 73K test để có 1.000 response thành công, CBT 11 phút và 1K test | Có: mã nguồn mở RESTest; supplementary `github.com/isa-group/icsoc-2020-supplementary-material` | Số lần lặp ít, không kiểm định thống kê (hạn mức API, ví dụ YouTube-S 100 request/ngày); 6 API; tự viết OAS cho 3 service (Foursquare, Tumblr, Yelp); phải bổ sung 4 ràng buộc mới và sửa 9; hộp đen nên không biết số lỗi phân biệt | REST + lỗi + đối chứng random: đủ P/C/O. Can thiệp là **ràng buộc**, EP/BVA chỉ là một tuỳ chọn cấu hình (boundary-value generator), không được tách ra đánh giá. Included (V2: tải được PDF; open access) |
| K33 | Implementation of an Integrated Executive Dashboard on the PPMPP Portal as a Digital Instrument for Institutional Quality Assurance at Politeknik Negeri Bali (2026; ICOSTAS-EAS 2026, tr. 118–128; [10.2991/978-94-6239-805-4_13](https://doi.org/10.2991/978-94-6239-805-4_13)) | Phát triển dashboard (Waterfall, PHP CodeIgniter, MVC, RESTful API + JSON, staging DB). Kiểm thử **Black-Box với Equivalence Partitioning**; đánh giá IPA | Portal PPMPP tích hợp e-Monev và e-AMI. IPA: **14 người** từ 7 khoa (2 người/khoa), 8 tính năng | Tỉ lệ kịch bản chức năng đạt; IPA (mean quan trọng/hiệu năng cảm nhận, mức phù hợp) | **6/6 nhóm kiểm thử đạt 100%** (xác thực, trích e-Monev, trích e-AMI, nội dung web, repository, dữ liệu kiểm định). IPA: mean quan trọng **4,47**, hiệu năng **4,20**. Theo Hình 6: tính năng 3 (đồng bộ thời gian thực) và 4 (trực quan hoá) nằm góc "cần cải thiện" | Không nêu | Tác giả tự nêu: không đo response time, throughput, đồng thời, tài nguyên; IPA chỉ là đánh giá ban đầu; 100% chỉ là tỉ lệ đạt kịch bản định trước. **Không nêu số test case** | Yếu: EP chỉ để kiểm thử chức năng chính hệ thống đang xây; REST API là kiến trúc của hệ thống, không phải đối tượng kỹ thuật test; không có đối chứng, không có metric phát hiện lỗi. Ghi chú v1 ghi nhận "phát triển ứng dụng, chỉ kiểm thử chức năng" (IC-P). Included (V2: tải được PDF); **cần xác nhận lại** |
| K39 | Automated Test Generation for REST APIs: No Time to Rest Yet (2022; ISSTA '22, 13 tr.; [10.1145/3533767.3534401](https://doi.org/10.1145/3533767.3534401)) | Nghiên cứu thực nghiệm **10 công cụ**: EvoMasterWB (hộp trắng), EvoMasterBB, RESTler, RestTestGen, RESTest, Schemathesis, Tcases, Dredd, bBOXRT, APIFuzzer. **Tcases** dùng mô hình không gian đầu vào + each-choice (1-way combinatorial); Schemathesis dùng property-based | **20 RESTful service** Java/Kotlin (977.296 LOC; 675 operation). Chạy 1 giờ × 10 lần + 1 lần 24 giờ; JaCoCo | Độ phủ dòng/nhánh/method; số lỗi 500 duy nhất, failure point duy nhất, library failure point duy nhất; tương quan Pearson phủ–lỗi | Trong 1 giờ, EvoMasterWB tốt nhất (line 52,76%; branch 36,08%; 33,3 lỗi). Công cụ hộp đen tốt nhất về phủ: EvoMasterBB (45,41% / 28,21%), kế đó Schemathesis (43,01% / 25,29%). Về lỗi 500: Tcases **18,5**, EvoMasterBB 16,4, RESTler 15,1, Schemathesis 14,2; RESTest 7,2. Tương quan phủ–lỗi ≈ **0,788**. Tổ hợp tham số và đa dạng kiểu input giúp tìm thêm lỗi | Có: replication package Zenodo `10.5281/zenodo.6534554`; trang `bit.ly/RESTTestToolsStudy` | 20 service (khó khái quát); chạy cục bộ; chỉ Java/Kotlin; spec không khớp (~99% trong >1.000 spec trên apis.guru có sai lệch); RESTest cần bổ sung phụ thuộc thủ công; EvoMasterWB cần driver; dùng lỗi 500 làm proxy, **chưa dùng mutation** (nêu là việc sau) | Mạnh cho **C** (so các chiến lược random / sample-value / dictionary) và **O**. Kỹ thuật gần EP nhất là Tcases (each-choice), nhưng bài **không gọi là EP/BVA**; phần thảo luận gợi ý combinatorial ≥2-way là hướng triển vọng cho hộp đen. Included (V2: tải được PDF); đọc bản arXiv 2204.08348 |

**Ghi chú nguồn.** K02 được đọc từ bản arXiv v2 (2504.08113, 4/8/2025); cần đối chiếu số liệu với bản LNCS khi có. K22 và K33 đọc từ PDF chính thức (open access). K39 đọc từ bản tác giả (arXiv 2204.08348); cần đối chiếu số trang khi trích dẫn ISSTA. Số liệu K33 ở dòng quadrant đọc từ Hình 6, không có câu nêu rõ trong văn bản.

**Vị trí trích (để kiểm chứng).**

| Mã | Số liệu | Vị trí |
|---|---|---|
| K02 | Test sinh, bug | Bảng 1, 2 (§5) |
| K02 | Độ phủ | Bảng 3 (§5) |
| K02 | Token, chi phí, năng lượng | Bảng 4 (§5) |
| K22 | % hợp lệ, thời gian | Bảng 2 (§4.3) |
| K22 | Failure theo oracle | Bảng 3 (§4.4) |
| K33 | Kịch bản đạt | Hình 5 (§3.1) |
| K33 | IPA | Hình 6 (§3.2) |
| K39 | Độ phủ và lỗi trung bình | Bảng 3 (§4.3–4.4) |
| K39 | Tcases, tổ hợp tham số | §3.2, §4.4, §4.5.1 |

## 2. Đối chiếu P · I · C · O (theo mẫu ảnh)

Ký hiệu: ✓ = đạt; ◐ = một phần (không đếm vào tổng); ✗ = không.
- **P** = REST API làm đối tượng test.
- **I** = EP / BVA / ràng buộc.
- **C** = đối chứng random / fuzzing / sample-value.
- **O** = số lỗi hoặc mutant phát hiện.

| Paper | P | I | C | O | Số yếu tố ✓ | Ghi chú |
|---|---|---|---|---|---|---|
| K22 RESTest (2020) | ✓ | ✓ (ràng buộc) | ✓ | ✓ | **4/4** | I là ràng buộc, chưa phải EP/BVA đúng nghĩa |
| K39 Kim et al. (2022) | ✓ | ◐ | ✓ | ✓ | **3/4** | I: Tcases each-choice; O: lỗi 500, chưa có mutant |
| K02 Nooyens (2026) | ✓ | ◐ | ✗ | ✓ | **2/4** | I: biên chỉ trong prompt; C: baseline là agent đơn |
| K33 PPMPP (2026) | ✗ | ◐ | ✗ | ✗ | **0/4** | EP chỉ dùng kiểm thử chức năng hệ thống |
| **Paper làm nền** | 3 (K22, K39, K02) | **1** (K22) | 2 (K22, K39) | 3 (K22, K39, K02) | | |

- **Chỗ mỏng nhất là I**: chỉ 1 paper (K22) làm nền, và đó cũng là ràng buộc chứ không phải EP/BVA. **Không có paper nào tách EP hoặc BVA ra làm biến can thiệp có đối chứng.** Đây là khoảng trống cần báo giảng viên trước buổi 1 Tuần 7 (không tự đổi RQ).
- **Ứng viên phản chứng (≥3 ô)**: K22 (4/4) và K39 (3/4). Kiểm ở RBL-2.
- **Preprint đã loại IC-T ở snowballing**:
  - K44 (Qeios, *Agentic Systems…*): 0/4, không về kiểm thử.
  - K45 (*Restats*): abstract trong CSV chỉ là mô tả hội nghị, không đủ để chấm. Muốn xét thì cần full text (arXiv 2108.08209, ref [7] của K02). Nguồn: snowball-back từ seed K02 (OpenAlex).

## 3. Việc cần xác nhận trước khi sang Tuần 7

- [ ] **K33 có nên giữ không?** Ghi chú v1 của chính K.Duy cho thấy bài đúng tiêu chí loại IC-P (phát triển ứng dụng, chỉ kiểm thử chức năng), và bản đọc full text không đổi điều đó (không đối chứng, không metric lỗi).
- [ ] **K02**: ghi chú v1 ghi IC-I (chỉ dùng LLM). Cần thống nhất lại hoặc nới tiêu chí I.
- [ ] **K22**: thống nhất "ràng buộc" có thuộc I hay không (ghi chú v1 ghi I gồm EP/BVA/ràng buộc).
- [ ] Các dòng v1 `INCLUDE` nhưng mang mã loại (K02 IC-I, K33 IC-P): kiểm tra cột `v1_reason` có đang chứa mã cảnh báo thay vì mã loại.
- [ ] Đối chiếu K02 (arXiv) với bản LNCS, K39 (arXiv) với bản ACM trước khi trích số liệu vào bài.
- [ ] 5 bài ở Phụ lục A: thử lấy full text (email tác giả) nếu muốn đưa lại vào vòng 2.

## Phụ lục A — 5 bài loại ở V2 (EC-A: không có full text)

Các bài này **không** nằm trong bảng chính. Dữ liệu dưới đây chỉ từ abstract, không phải từ full text. Nếu lấy được full text thì đưa lại vào bảng chính.

| Mã | Paper (năm; venue; DOI) | Lý do loại / ghi chú v1 | Việc có thể làm |
|---|---|---|---|
| K04 | A Model-Based Testing Framework for Digital Battery Passport Lifecycle Systems (2027; APMS 2026; [10.1007/978-3-032-38594-9_4](https://doi.org/10.1007/978-3-032-38594-9_4)) | EC-A. V1: REST + BVA (EFSM 7 trạng thái, 19 transition, 42 test case; pre-operational) | Email tác giả liên hệ (Andrushchenko) |
| K08 | Requirements-Driven Model Checking and Test Generation for Comprehensive Verification (2022; NFM 2022; [10.1007/978-3-031-06773-0_31](https://doi.org/10.1007/978-3-031-06773-0_31)) | EC-A. V1 đã ghi: không nhắc REST/web API (IC-P) | Email tác giả; nhiều khả năng vẫn loại vì IC-P |
| K19 | Revealing inputs causing web API performance latency using response-time-guided genetic algorithm fuzzing (2024; Artificial Life and Robotics; [10.1007/s10015-024-00957-4](https://doi.org/10.1007/s10015-024-00957-4)) | EC-A. Abstract: GA fuzzing vs random fuzzing, 5 web API, seed PICT vs ngẫu nhiên; đo latency, không phải lỗi/mutant | Email tác giả (Shin-Jie Lee) |
| K24 | CAGE-SQL: Diagnostic Mutation Analysis for Execution-Based Text-to-SQL Verification (2027; APWeb-WAIM 2026; [10.1007/978-981-92-5696-9_1](https://doi.org/10.1007/978-981-92-5696-9_1)) | EC-A. V1 ghi IC-I (hộp trắng/search-based); đối tượng Text-to-SQL, không phải REST | Có thể loại hẳn vì lệch P |
| K27 | Making effective carbon-box testing technique using prioritised-selected test cases driven combinatorial approach (2025; Int. J. Syst. Assur. Eng. Manag.; [10.1007/s13198-024-02650-y](https://doi.org/10.1007/s13198-024-02650-y)) | EC-A. V1 ghi IC-P (không nhắc REST). Bản tiền thân miễn phí là bài khác: *Carbon-Box Testing* (ENASE 2023) | Không thay thế bằng bản ENASE khi trích dẫn |

## 4. Xác nhận lại EVIDENCE-TABLE

| # | Mã (gộp) | Paper (tên + năm + venue + DOI) | Nguồn | Tool/LLM | Dataset | Metric | Kết quả | Code | Hạn chế | Gần RQ |
|---|---|---|---|---|---|---|---|---|---|---|
| 41 | K02 | **Test Amplification for REST APIs via Single and Multi-agent LLM Systems** (2026, Testing Software and Systems) · DOI 10.1007/978-3-032-05188-2_11 | K.Duy · Springer | LLM đơn/đa tác tử khuếch đại test suite REST API, OpenAI GPT-4o mini (Sec. 6.4), đơn tác tử ReAct, đa tác tử LangGraph (Sec. 3, Fig. 1–2) | PetStore, 20 endpoint, 3 lần chạy lấy trung bình (Sec. 4, 6.3) | Số test sinh/pass/fail/bug-exposing (Table 1); độ phủ cấu trúc API (Table 3); thời gian, token, chi phí, năng lượng (Table 4) | Table 1: test sinh 118 (đơn) vs 145 (đa); bug-exposing 32 (27%) vs 43 (30%). Table 3: phủ Parameter 11% → 56% vs 82%; Response Type 51% vs 88%; Request Type 73% vs 97%; Operation 95% vs 100%. Table 4: chi phí $0,01848 vs $0,05213; thời gian 351 s vs 1149 s; năng lượng 4,27 vs 9,74 Wh |Có reproduction package (figshare) — theo evidence-table cá nhân; link: https://figshare.com/s/6c0d66b47181b0874305?file=56376179| Sec. 6: (6.1) coverage cao không đảm bảo test đúng phần quan trọng, mọi bug tính ngang nhau; (6.2) LLM có thể đã biết PetStore; (6.3) chỉ 1 ứng dụng; (6.4) LLM không tất định, chỉ 1 model, chấm khả đọc bằng đánh giá chủ quan của tác giả | 0/4 ✓ · chạm 1/4 (◐ O) |
| 42 | K33 | **Implementation of an Integrated Executive Dashboard on the PPMPP Portal as a Digital Instrument for Institutional Quality Assurance at Politeknik Negeri Bali** (2026, ICOSTAS-EAS) · DOI 10.2991/978-94-6239-805-4_13 | K.Duy · Springer | Black-box testing với **EP**; RESTful APIs, JSON | PPMPP Portal (e-Monev/e-AMI); 14 người trả lời | Hoàn thành kịch bản chức năng định trước; IPA (Importance–Performance Analysis) | Fig. 5: toàn bộ kịch bản đạt, tỉ lệ đạt 100%. Fig. 6: IPA độ quan trọng trung bình 4,47, hiệu năng cảm nhận 4,20. Cụm "chưa đánh giá định lượng" không đúng, bài có số | Không có  | Phần Discussion/Limitations: 100% chỉ là tỉ lệ đạt kịch bản định trước, không chứng minh khả năng mở rộng hay hiệu năng; IPA chỉ 14 người, là đánh giá ban đầu; không đo response time, throughput, số người dùng đồng thời, tài nguyên server | 0/4 ✓ · chạm 2/4 (◐ P, I) |
