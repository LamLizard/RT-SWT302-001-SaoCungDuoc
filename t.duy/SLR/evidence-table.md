# Evidence Table — T.Duy (Google Scholar + Semantic Scholar) · 8 cột

**Nhóm 1 — SaoCungDuoc · RQ FA26-EXT-12 · 07/10/2026 · bản theo mẫu nhóm**

**Chú thích:** 8 cột nội dung + cột số thứ tự. “Kết quả” lấy từPDF đã có; vị trípage/Table/Listing ghi rõ. N/A = chưa xác minh, không tự điền số. Bảng gồm5 paper đã đọc toàn văn, kể cảUnsure/Exclude để minh bạch; **không phải5 paperIncluded**. Code làlink tác giả công bố, chưa chạy tái lập.

| # | Paper (tên + năm + venue + DOI) | Tool/LLM | Dataset | Metric | Kết quả | Code | Hạn chế | Gần RQ |
|---|---|---|---|---|---|---|---|---|
| 1 · R001 | Combining TSL and LLM to Automate REST API Testing: A Comparative Study (2025; Anais do XXXIX Simpósio Brasileiro de Engenharia de Software (SBES 2025)) · 10.5753/sbes.2025.9670 | RestTSLLM; TSL + 8 LLMs | 6 dự án REST API .NET nhỏ | Success rate; coverage; mutation score; số test trung bình | Claude 3.5 Sonnet: success rate **100%**, coverage **71,7%**, mutation score **40,8%**, trung bình **38,3 test** (Table 3, PDF tr. 8). | https://github.com/uffsoftwaretesting/RestTSLLM | API nhỏ; không đối chứng uniform random cùng ngân sách; mutation score không phải số mutant riêng biệt theo từng yêu cầu. | 2/4 — P,I; O chỉ là proxy |
| 2 · R123 | Empirical Comparison of Black-box Test Case Generation Tools for RESTful APIs (2021; 2021 IEEE 21st International Working Conference on Source Code Analysis and Manipulation (SCAM)) · 10.1109/scam52516.2021.00035 | RestTestGen; RESTler; bBOXRT; RESTest | 14 REST API;114 endpoints;234 operations (Table II/PDF tr. 7–8) | Robustness của công cụ; các metric coverage theo OpenAPI | Chạy thành công: RESTler **14/14**, RestTestGen **11/14**, bBOXRT **8/14**, RESTest **2/14** (Table III, PDF tr. 9). Đây là độ ổn định công cụ, không phải số bug tìm được. | N/A — chưa xác minh replication package riêng của study; tool links được bài dẫn ở mụcIII. | Tool/version và cấu hình ảnh hưởng kết quả; không suy kết quả2021 thành năng lực tool hiện tại. Section V-E/PDF tr. 8–9: mẫu API không đảm bảo đại diện. EP/BVA trong cấu hình đánh giá chưa được xác minh. | 1/4 — P; coverage là proxy O |
| 3 · R130 | Restats: A Test Coverage Tool for RESTful APIs (2021; 2021 IEEE International Conference on Software Maintenance and Evolution (ICSME)) · 10.1109/icsme52107.2021.00063 | Restats — đo coverage từ OpenAPI và HTTP traffic | Pet Store;4 endpoints/7 operations; bộ request minh họa (Section III-A, PDF tr. 4) | 8 metric input/output coverage; Test Coverage Level | Operation coverage **2/7 =0,285714…** (Listing 2, PDF tr. 5). Đây là output minh họa; **N/A** cho kết quả số trongTable/Figure đã xác minh theoIC-E. | https://github.com/SeUniVr/restats | Minh họa mộtAPI; chỉ JSON payload được hỗ trợ ở bước thu thập; không sinh input bằng EP/BVA. Số ởListing không tự thay điều kiệnTable/Figure. | 1/4 — P; hỗ trợ đoO |
| 4 · R132 | LlamaRestTest: Effective REST API Testing with Small Language Models (2025; Proceedings of the ACM on Software Engineering) · 10.1145/3715737 | LlamaRestTest; LlamaREST-IPD/EX; fine-tuning và quantization; nền ARAT-RL | 12 dịch vụREST thực; so sánhMoRest,RESTler,ARAT-RL,EvoMaster (Table 1, PDF tr. 11) | Method/branch/line coverage; operations; HTTP 500 errors sau bỏ trùnglog | **204 server errors qua 10 runs** (Section 4.5/PDF tr. 17; Table 2/PDF tr. 11). Method **55,8%**, branch **28,3%**, line **55,3%** (Figure 4/Section 4.4/PDF tr. 16). Không diễn giải204 thành204 root-cause bugs được xác nhận. | https://github.com/codingsoo/LlamaRestTest | Section 4.7/PDF tr. 19: mẫu12 API, lựa chọnbaseline/cấu hình, scripts coverage có rủi ro; kém hiệu quả khi phản hồiAPI ít thông tin. Chưa có bằng chứng EP/BVA cho thiết kế tham sốrequest. | 1/4 — P; lỗi500/coverage là proxy O |
| 5 · R133 | Leveraging Large Language Models to Improve REST API Testing (2024; Proceedings of the 2024 ACM/IEEE 44th International Conference on Software Engineering: New Ideas and Emerging Results) · 10.1145/3639476.3639769 | RESTGPT; GPT; trích rules + sinh example values từ mô tả OpenAPI | 9 dịch vụREST từ NLP2REST;333 ground-truthrules (Table 1, PDF tr. 4) | Precision/recall/F1 củarule extraction; accuracy củatest input values | Ruleextraction: precision **97%**, recall **92%**, F1 **94%** (Table 1). Input-valueaccuracy trung bình **72,68%** vs ARTE **16,93%** (Table 2); đềuPDF tr. 4. Không phải mutation score hayfaultcount. | https://github.com/selab-gatech/RESTGPT | Ground truth từ9 API/NLP2REST; chưa đánh giáEP+BVA vsuniform random; chưa suy hiệu quả tìm lỗi từprecision/accuracy. Future work còn đề xuất mở rộng fault detection. | 1/4 — P |

## Quyết định V2 — theo protocol hiện hành 1.2

| #/ID | Trang PDF đã đọc | Quyết định đề xuất | Lý do |
|---|---|---|---|
| 1 / R001 | 11 | **INCLUDE** | IC-I: Published SBES 2025; 11 trang; tiếng Anh. Mục 3, PDF p4 mô tả boundary testing/equivalence classes cho sinh integration tests từ OpenAPI; Table 3 p8 có coverage/mutation score. |
| 2 / R123 | 13 | **UNSURE** | IC-I: Bài so sánh 4 công cụ REST, PDF 13 trang; chưa xác minh EP/BVA là thành phần thiết kế test được thực sự triển khai trong các cấu hình đánh giá. |
| 3 / R130 | 6 | **EXCLUDE** | IC-I: Restats đo test coverage từ HTTP logs/OpenAPI, không đề xuất/ap dụng EP/BVA để sinh input request. |
| 4 / R132 | 23 | **UNSURE** | IC-I: Published PACMSE/FSE 2025 metadata verified; author PDF 23 trang. Tập trung realistic values/IPD/ARAT-RL; bboxes boundary là tọa độ địa lý, chưa chứng minh BVA request-design. |
| 5 / R133 | 5 | **EXCLUDE** | IC-I: RESTGPT trích rules và example values từ descriptions; fulltext không xác lập EP/BVA cho sinh request. |

**Tổng V2:** Include đề xuất 1; Unsure2; Exclude2. T.Duy/nhóm chưa xác nhận cuối. 13 paper khác đã qua V1 đang chờ toàn văn; không tính vào bảng số liệu đã thẩm định. Chưa khẳng định đạt≥6paper/người.

PICO mở rộng hiện là đề xuất 1.3, chưa thay IC-I của protocol 1.2. Paper LLM/RL không bị loại vì dùng AI; quyết định ở đây căn cứ có/không bằng chứng EP/BVA cho request parameters.

## Nguồn bản đọc miễn phí và vị trí bằng chứng

- **#1 / R001:** [Nguồn bài](https://doi.org/10.5753/sbes.2025.9670) · [PDF bản đọc](https://sol.sbc.org.br/index.php/sbes/article/download/36987/36772) · Published; 11trang. Vị trí: Section 3, PDF tr. 4; Table 3, PDF tr. 8.
- **#2 / R123:** [Nguồn bài](https://doi.org/10.1109/scam52516.2021.00035) · [PDF bản đọc](https://arxiv.org/pdf/2108.08196) · Author manuscript / preprint (published metadata separate); 13trang. Vị trí: Table II, PDF tr. 7–8; Table III, PDF tr. 9; Section V-E, PDF tr. 8–9.
- **#3 / R130:** [Nguồn bài](https://doi.org/10.1109/icsme52107.2021.00063) · [PDF bản đọc](https://arxiv.org/pdf/2108.08209) · Author manuscript / preprint (published metadata separate); 6trang. Vị trí: Section II-B, PDF tr. 3; Section III-A, PDF tr. 4; Listing 2–3, PDF tr. 5.
- **#4 / R132:** [Nguồn bài](https://doi.org/10.1145/3715737) · [PDF bản đọc](https://arxiv.org/pdf/2501.08598) · Author manuscript / preprint (published metadata separate); 23trang. Vị trí: Table 1–2, PDF tr. 11; Section 4.4/Figure 4, PDF tr. 16; Section 4.5, PDF tr. 17; Section 4.7, PDF tr. 19.
- **#5 / R133:** [Nguồn bài](https://doi.org/10.1145/3639476.3639769) · [PDF bản đọc](https://arxiv.org/pdf/2312.00894) · Author manuscript / preprint (published metadata separate); 5trang. Vị trí: Section 4.1, PDF tr. 3; Table 1–2, PDF tr. 4; FutureDirections, PDF tr. 4; artifact links, PDF tr. 5.

PDF bản tác giả/preprint và bản xuất bản đã đối chiếu không tính thành 2 paper. R001 do T.Duy cung cấp seed sau Google Scholar; bốn bài còn lại tìm ngược trong References của seed RestTSLLM. IEEE/ACM/SBC là venue/nguồn metadata hoặc PDF, không tự đổi thành nguồn tìm kiếm của T.Duy.

## Mô hình nghiên cứu — dùng để trình bày

- **R001:** OpenAPI → LLM tạo TSL/scenarios và input → sinh/xử lý integration tests → chạy trên API → so sánh 8 LLM bằng success rate/coverage/mutation score.
- **R123:** Cùng14 API →4 công cụ black-box → ghi khả năng chạy thành công → so sánh input/output coverage; không cô lập EP+BVA vsrandom.
- **R130:** OpenAPI + HTTP request/response logs → chuẩn hóa/lưu SQLite → tínhinput/output coverage → báo cáo JSON. Đây là đo kiểm, không phải phương pháp sinh test.
- **R132:** SLM fine-tuned → khai thác mô tả/thông báo server → suy IPD + sinh realistic values → phối hợp ARAT-RL → chạy12 API → so sánh coverage/server errors; có ablation.
- **R133:** OpenAPI descriptions → GPT tríchparameter constraints/IPD vàexample values → so sánhNLP2REST/ARTE bằng rule precision/recall/F1 vàinput accuracy.

## Ghi chú cho nhóm

- “Gần RQ” là phân loại hỗ trợ đọc theo PICO gốc: P=miền REST API; I=EP/BVA cho input request; C=uniform random cùng ngân sách; O=distinctmutants theo yêu cầu. P không có nghĩa đã dùng45 yêu cầu RESTestBench. Coverage/mutation score/HTTP500 là proxy, không tự tính thànhO chính xác.
-5/5 hàng có số đọc từPDF; R130 làListing minh họa, chưa tính là bằng chứngTable/Figure cho IC-E. Không đồng nhất dataset size/sốmetric với kết quả thí nghiệm.
- Chưa paper nào trong5 bài này trả lời đầy đủ PICO gốc; kết luận này không chứng minh cả lĩnh vực chưa có nghiên cứu. Không dùng2/4–1/4 để thay quyết địnhIC/EC.
