# Kiểm chứng RQ — phần của T.Duy

**Nguồn phụ trách:** Semantic Scholar + Google Scholar · **Lớp bổ sung:** L2 (đợt trước) · **Ngày:** 2026-10-18
**Bước 2 cá nhân:** bài **#31–#38** theo số hàng của `team-synthesis/evidence-table-merged.md`; RQ **FA26-EXT-12**. Đây là phân công đọc tập gộp, không phải tám bài mới của nguồn cá nhân.

**RQ:** Trên 45 yêu cầu của RESTestBench, phân hoạch tương đương kết hợp phân tích giá trị biên, so với sinh dữ liệu ngẫu nhiên đồng đều cùng ngân sách, khác nhau thế nào về số mutant riêng biệt bị phát hiện theo từng dạng yêu cầu?

**PICO:** P = 45 yêu cầu RESTestBench (15/dịch vụ); I = EP + BVA; C = random đồng đều cùng ngân sách request; O = số mutant riêng biệt được oracle xác nhận.

## 1. Bảng đối chiếu paper

Theo [bản đồ nhóm](../../team-synthesis/rq-evidence-map.md): ✓ khớp theo rubric; ◐ liên quan một phần; · không khớp. P◐ = REST mở/chạy được; I◐ = miền/ràng buộc liên quan; C◐ = fuzzing hoặc random chưa khớp budget; O◐ = bug/failure/vulnerability. Rubric I✓ cho EP và/hoặc BVA, O✓ cho mutation score; vẫn phải kiểm **EP+BVA kết hợp, uniform random, unique mutants** của RQ. Không suy I từ tính năng của công cụ đối chứng. Trang dưới đây là **trang PDF, đếm từ 1**.

| Paper | P | I | C | O | Hạn chế paper nêu | Chi tiết |
| --- | --- | --- | --- | --- | --- | --- |
| **#31 K93 — DynER** (Electronics 2024), [DOI](https://doi.org/10.3390/electronics13173476), [PDF](../../Paper-source/31-K93.pdf) | ◐ | · | ◐ | ◐ | “limited number of services tested” (§7.1, p21): chỉ hai dịch vụ; khả năng khái quát bị giới hạn. | Sửa request từ phản hồi lỗi, có LLM; WordPress/GitLab, 3 giờ/dịch vụ (§6.3). Table 3/p17: PRTT DynER/foREST **47,71/6,50%** và **34,90/8,57%**, nhưng bugs **7/9** và **4/5**. PRTT là tỷ lệ request trả 20X hoặc 50X, không phải mutant count. **0✓; chạm 3/4**. |
| **#32 K100 — FDRRestTest** (ESEM 2026), [DOI](https://doi.org/10.4230/LIPIcs.ESEM.2026.20), [PDF](../../Paper-source/32-K100.pdf) | ◐ | · | ◐ | ◐ | “The benchmark excludes enterprise-level APIs” (§5, p17): chưa kiểm hệ doanh nghiệp; oracle có false positives. | Feedback/dependency/repair và logical oracles; 12 services, 5 baselines. 600 giây × 10 lần; có fixed-request 1.000/3.000/6.000 (§4.3.6, p15–16), thiếu uniform-random arm. Table 2/p11: **FRE 0,9878/0,9294**, chênh lệch là ước lượng trên do baseline lower bound. FRE đếm tín hiệu/request, không mutant. **0✓; chạm 3/4**. |
| **#33 K127 — Automated Black-Box and Manual Basis Path Testing on E-OBE Application** (bit-Tech 2026), [DOI](https://doi.org/10.32877/bt.v9i1.4098), [PDF](../../Paper-source/33-K127.pdf) | · | · | · | ◐ | “without achieving new defect diversity or broader endpoint coverage” (Discussion, p8): các lần chạy lặp trạng thái, ít đa dạng lỗi/endpoint hơn mong đợi. | EvoMaster và kiểm basis path thủ công trên một ứng dụng nội bộ; 10 lần × 1 giờ, không đối chứng random cùng budget (p3–4). Table 5/p7: **49 HTTP calls, 27 fault findings = 22 schema mismatch + 4 HTTP500 + 1 auth**; chưa chứng minh 27 root causes. Schema tự viết có thể tạo mismatch giả (p7–8). **0✓; chạm 1/4**. |
| **#34 K136 — SBFT Tool Competition 2026: REST League** (SBFT 2026), [DOI](https://doi.org/10.1145/3786155.3795704), [PDF](../../Paper-source/34-K136.pdf) | ◐ | · | ◐ | ◐ | “none exceeded 23%” (§3.2, p4): branch coverage thấp; khó chạm logic sâu, công cụ gặp lỗi thực thi. | So 5 công cụ với RestTestGen; 11 APIs/317 operations, 1 giờ × 10 lần (§2). Table 2/p3: AutoRestTest **67,09** unique server-error findings trung bình/API; Table 4: branch **21%**, RestTestGen **23%**. Đây là tổng hợp so công cụ, không thí nghiệm chính EP+BVA hay source mutants. **0✓; chạm 3/4**. |
| **#35 K166 — Deep Learning-Based Prediction of Test Input Validity for RESTful APIs** (DeepTest 2021), [DOI](https://doi.org/10.1109/DeepTest52559.2021.00008), [PDF](../../Paper-source/35-K166.pdf) | · | ◐ | · | · | “Our approach has been validated on five subject APIs” (§V, p7): số API nhỏ; tác giả còn nêu rủi ro nhãn và độ đa dạng invalid inputs. | DNN TensorFlow/Keras, không LLM; RESTest tạo valid/invalid inputs có ràng buộc. 5 APIs thương mại/8 operations, **16.000 calls** (p6). Table III/p6: accuracy dự đoán tính hợp lệ **97,3% test**, không fault detection. **0✓; chạm 1/4**. Mục Verifiability/p8 có code/dataset, xem đính chính dưới. |
| **#36 K168 — Automated Black-Box Testing of Mass Assignment Vulnerabilities in RESTful APIs** (ICSE 2023), [DOI](https://doi.org/10.1109/ICSE48619.2023.00213), [PDF](../../Paper-source/36-K168.pdf) | ◐ | · | · | ◐ | “we only considered open-source projects” (§IV.E, p8): chưa biết mức khái quát sang hệ công nghiệp; ground truth có yếu tố đánh giá thủ công. | RestTestGen, suy CRUD/read-only fields, attack templates và oracle đọc lại trạng thái. 5 APIs mở/47 operations; 10 lần chạy (p7). Table IV/p9: precision **100%**, recall **90% OWASP**, **100%** bốn hệ còn lại. Lỗi cấy tay trên một số hệ không thành phép đo source-mutant chuẩn của RQ. **0✓; chạm 2/4**. |
| **#37 K191 — Automated REST API Black-box Test Generation in Practice: An Experience Report from Industry** (ICST 2026), [DOI](https://doi.org/10.1109/ICST69053.2026.00064), [PDF](../../Paper-source/37-K191.pdf) | · | · | ◐ | ◐ | “findings may not generalize to APIs in other domains” (§V.D, p8): một doanh nghiệp/lĩnh vực; không phân tích false negatives. | RestTestGen/DeepREST; Qwen3 14B tạo dictionary offline. 5 APIs SES/204 operations; **200 × số operations requests/API/lần**, 10 lần (§IV, p5). Tables II–III/p6: cùng **151/204 operations** (median); tổng median faults **17/18**. Faults được gom từ 5XX, developer xác nhận; không mutant. **0✓; chạm 2/4**. |
| **#38 K192 — RESTing-LLAMA: Large Language Model based REST API Fuzzing** (ASIACCS 2026), [DOI](https://doi.org/10.1145/3779208.3785383), [PDF](../../Paper-source/38-K192.pdf) | ◐ | · | ◐ | ◐ | “specifications exceeded the maximum token limits” (Appendix C, p14): cắt spec có thể bỏ dependency; giới hạn model/ngữ cảnh khác nhau. | LLM suy dependency/functionality; 15 apps, 6 baselines và 4 models. §5.2/p9 (diễn giải Table 3): **11 vulnerability findings theo endpoint**, không 11 CVE riêng biệt; HTTP500 ratio **6,585%/0,42% RESTler** không phải số bugs. Appendix B/p14: fixed-time throughput chạy 1 giờ × 2, **không kiểm vulnerability trong các lượt đó**. **0✓; chạm 3/4**. |

**Kết luận phần của tôi:** cả 8 bài có 0 dấu ✓ theo rubric nhóm, nhưng có mức liên quan 1–3/4 như trên. Không bài nào khớp 3 hoặc 4 yếu tố đầy đủ, không bài đo trọn EP+BVA so uniform random cùng request budget trên 45 yêu cầu và unique oracle-confirmed mutants. **RQ đứng vững trong phạm vi tám bài đã đọc**; chưa thể kết luận thay cho toàn tập nhóm. “Chạm 3/4” bằng ◐ không có nghĩa đã giống 3/4 đầy đủ để tự gán extension. Nhãn trên thẻ RQ chưa có trong đầu vào; **CHỜ PL đối chiếu**, không tự nhận new/extension/replication.

**Hạn chế để PL gộp:** các trích dẫn trên là lời tác giả, khác với nhận xét PICO của người đọc. K93/K100/K166/K168/K191 cùng nêu giới hạn mẫu hoặc domain ở các mức khác nhau; K136/K168/K191 có chung tác giả Corradini nên không đếm thành ba nhóm độc lập. K191 đã thử hệ công nghiệp, vì vậy không gộp thành câu tuyệt đối “chưa thử công nghiệp”. Trong tám bài chưa thấy tác giả phát biểu trực tiếp đúng gap EP+BVA–uniform random–unique mutants của RQ: hiện là giả định cần đối chiếu toàn tập, chưa tự chốt gap mạnh hoặc viết kết luận nhóm.

**Rà 12 tháng gần nhất (2025-10-18–2026-10-18):** ưu tiên cùng task/metric, sau đó venue/benchmark và thời điểm; ba bài chọn từ tập đã có, không khẳng định xếp hạng toàn ngành. Truy vấn bổ trợ ngày 18/10 ở search-log §8.

| Paper chọn | Lý do ưu tiên | RQ đo thêm điều gì |
| --- | --- | --- |
| K100 — FDRRestTest | ESEM; 12 services, 5 baselines; có fixed-request nên sát kiểm soát ngân sách | EP+BVA so uniform random và số mutant riêng biệt theo dạng yêu cầu; FRE/logical yield không trả lời phép so này |
| K136 — REST League | SBFT; benchmark 11 APIs/317 operations, nhiều công cụ và 10 lần lặp | Fixed request budget và oracle source-mutant; xếp hạng lỗi 5XX/coverage với cùng thời gian khác phép đo của RQ |
| K192 — RESTing-LLAMA | ASIACCS; 15 apps, 4 models, 6 baselines | Unique source mutants và uniform random; vulnerability endpoints/5XX ratio và throughput riêng không thay thế được |

K191 sát điều kiện ngân sách nhưng ưu tiên thấp hơn do SUT công nghiệp đóng và cùng hướng công cụ với K136; K127 chỉ một ứng dụng nội bộ; K93/K166/K168 ngoài cửa sổ. Hai bài nguồn cá nhân đã rà trước vẫn giữ: **TD-0002/RestTSLLM: 2✓, chạm 3/4** (thiếu C, P chưa đúng); **TD-0015/Orchestration: 1✓, chạm 2/4** (thiếu C/O). Xem [evidence cá nhân](evidence-table.md); không thay bằng tám bài phân công.

**Điểm cần leader review trên bảng gộp:**

- **K166 Code:** PDF p8, *Verifiability* dẫn [kho code và dataset](https://anonymous.4open.science/r/8954c607-8d6c-4348-a23c-d57c920cdc22/); ô NOT_REPORTED cần đối chiếu lại. Đây là link tác giả công bố, chưa xác minh tải/chạy được hiện nay.
- **K100:** 96/120 = 80% là mẫu thẩm định gộp từ oracle findings của nhiều công cụ, không phải “toàn bộ 96 lỗi của FDRRestTest đã xác nhận”. Baseline logs không có đầy đủ để tái đếm (§4.2/p9); giữ giới hạn ước lượng FRE.
- **K93:** Table 3 cho DynER ít bugs hơn foREST dù PRTT cao hơn. Chênh PRTT 41,21/26,33 là **điểm phần trăm**, không tăng tương đối tương ứng.
- **K192:** không dùng Table 8 throughput để tuyên bố thắng vulnerability dưới cùng budget; đọc điều kiện Appendix B/p14. Không tự đổi số hay nội dung file nhóm trong lượt này.

## 2. Lớp tìm kiếm bổ sung

Không có phân công L1/L3 mới; lần này đọc tám bài đã thuộc tập gộp. Tra cứu nguyên tiêu đề ba bài gần đây chỉ xác minh/đối chiếu, **không tạo record discovery mới**.

**L2 đã làm 18/10 (search-log §5–6):** S2 tra title K33 và K100/FDRRestTest đều không tìm được record, không đọc được citations; không suy thành 0 citations. Lượt bổ trợ seed K191 đọc **1/1** citing paper → TD-0158/Overlay, toàn văn 10 trang, loại V2 **IC-I**. Chưa có đủ 10–15 citations để khẳng định bao phủ L2; không lặp snowball Tuần 6.

**Dò kết quả âm đã làm ngày 18/10:**

| Query nguyên văn trên Google Scholar | Nguồn báo / thực thu | Kết luận |
| --- | --- | --- |
| `"REST API" ("negative result" OR "did not improve" OR "fails") ("equivalence partitioning" OR "boundary value")` | Khoảng 88 / 10 kết quả trang đầu | Dò rộng, chưa bao phủ hết |
| `"REST API" ("negative result" OR "did not improve") ("equivalence partitioning" OR "boundary value")` | 7 / 7 | Chưa thấy thí nghiệm âm trực tiếp đúng RQ trong tập 7 |

17 lượt → 11 paper mới: V1 loại 9; V2 loại TD-0160 vì IC-E; TD-0159 giữ Unsure IC-T. Không có Include mới. Không biến việc chưa thấy phản chứng thành khẳng định “chưa ai thử”.

**Đối soát sáu file SLR nguồn cá nhân (không đổi khi phân công đọc bài nhóm):** 01/02 = **136/136** paper; **175** lượt nguồn − **39** trùng; V1 loại **76**, cần toàn văn **60**, đã đọc **59**, thiếu **1**; V2 loại **55**, Unsure đã đọc **2**. **03 = evidence-table = PRISMA included = 2** (TD-0002, TD-0015). Search 72 + snowball mới 64 = 136; snowball 92 lượt, Include mới 0. Kiểm: `175−39=136;136−76=60;60−1=59;59−55−2=2`. Ba Unsure tổng vẫn giữ; S2/GS không cộng vào PRISMA tìm kiếm chính của nhóm.

## 3. Ghi chú khả thi từ các paper tôi đọc

Đây là đầu vào cá nhân cho Bước 3, chưa phải bảng chấm khả thi của nhóm; các repo dưới đây mới xác định từ paper, **chưa chạy pilot**.

| Hạng mục | Dữ liệu từ paper | Việc cần nhóm xác minh |
| --- | --- | --- |
| Code/harness | K93: [DynER](https://github.com/starrychen1122/DynER); K100: [artifact](https://doi.org/10.5281/zenodo.21964240); K136: [RESTgym](https://github.com/SeUniVr/RESTgym), [replication](https://doi.org/10.5281/zenodo.18434145); K168: [RestTestGen](https://github.com/SeUniVr/RestTestGen), [artifact](https://doi.org/10.5281/zenodo.7348518); K166 có link Verifiability ở trên | Khả năng tải, license, phiên bản và thích nghi harness; có repo không đồng nghĩa đã chạy được |
| Ngân sách/lặp | K100: 600 giây × 10 và cap 1.000/3.000/6.000 requests; K136: 1 giờ × 10; K191: 200 requests/operation × 10, tổng 204 operations | Chốt B requests/cách/yêu cầu, seeds và repeats; cùng thời gian không đảm bảo cùng requests. K100 còn báo overhead ở cùng request budget |
| Oracle/đếm | K100 manual precision 80% trên mẫu; K127 schema tự viết; K191 gom 5XX rồi developer thẩm định; K168 có lỗi cấy thủ công | Với RESTestBench cần mapping đúng 45 yêu cầu (15/dịch vụ), mutant ID và oracle; đếm một mutant một lần, không dùng tỷ lệ 5XX hay mutation score thay số đếm |
| Môi trường/chi phí | K136 dùng Docker, 8 cores/16GB mỗi worker; K191 dùng API công nghiệp và dictionary LLM offline; K192 có truncation và chi phí gọi model | Chọn cấu hình laptop, quyền truy cập, thời gian chạy đo từ pilot. RQ EP+BVA-vs-random không mặc nhiên cần LLM; không dùng chi phí paper làm dự toán nhóm |

**Trạng thái hiện tại:** Bước 2 — RQ check cá nhân cho bài #31–#38. Cổng evidence cá nhân P2/P3/P4 đạt 2/2 (100%), P5 có tên metric cụ thể ở cả hai hàng.

**Phần chuyển PL:** xác nhận P1–P5 của tập gộp, kiểm nhãn trên thẻ, gộp/gạch hạn chế đã được giải quyết và chốt gap/tính mới trên toàn tập. T.Duy chưa sửa RQ, file nhóm hoặc quyết định screening của người khác.
