# rq-check — K.Duy · Bước 2 (phần cá nhân)

**Phạm vi:** 8 bài được phân công: #17–#22 (K46, K49, K56, K60, K67, K68) và #41–#42 (K02, K33), theo `evidence-table-merged.md`.

**Ngày:** 18/10/2026

**Nguồn đối chiếu:** PDF trong `Paper-source/` (17-K46 … 22-K68, 41-K02, 42-K33). 

**Quy ước chấm:** theo `rq-evidence-map.md` §1. ✓ = khớp đúng giá trị RQ; ◐ = gần (không tính vào số ✓); "Không" = không có. Ngưỡng phản chứng: ≥ 3 ô ✓.

## 1. RQ của nhóm (nguyên văn trên thẻ FA26-EXT-12)

> Trên 45 yêu cầu của RESTestBench, phân hoạch tương đương kết hợp phân tích giá trị biên, so với sinh dữ liệu ngẫu nhiên đồng đều cùng ngân sách, khác nhau thế nào về số mutant riêng biệt bị phát hiện theo từng dạng yêu cầu?

- **P:** 45 yêu cầu RESTestBench
- **I:** EP kết hợp BVA
- **C:** random đồng đều cùng ngân sách
- **O:** số mutant riêng biệt được oracle xác nhận

## 2. Bảng phản chứng P/I/C/O

| # | Paper | P | I | C | O | Số ✓ | Hạn chế paper nêu (tóm tắt) |
|---|---|---|---|---|---|---|---|
| 17 | K46 · Black-Box and White-Box Test Case Generation for RESTful APIs: Enemies or Allies? (2021) | ◐ | ◐ | ◐ | ◐ | 0/4 | Chỉ 4 SUT; lỗi của công cụ có thể ảnh hưởng kết luận; yếu tố ngẫu nhiên |
| 18 | K49 · Open Problems in Fuzzing RESTful APIs: A Comparison of Tools (2023) | ◐ | Không | **✓** | ◐ | 1/4 | Cấu hình sai công cụ; tác giả là chủ EvoMaster nên có thể thiên lệch; EMB có thể thiên về EvoMaster; ngẫu nhiên |
| 19 | K56 · Bootstrapping Automated Testing for RESTful Web Services (2021) | Không | ◐ | ◐ | ◐ | 0/4 | Không hỗ trợ binary array; định dạng riêng của ứng dụng cần mở rộng FET; bug 8 và 9 chỉ có status code |
| 20 | K60 · FuzzTheREST: An Intelligent Automated Black-Box RESTful API Fuzzer (2025) | ◐ | Không | Không | ◐ | 0/4 | Mã không dùng làm tăng mẫu số coverage; cách lưu unique identifier cần cải tiến; chỉ 1 Petstore; không có baseline |
| 21 | K67 · Exploring behaviours of RESTful APIs in an industrial setting (2024) | ◐ | Không | ◐ | Không | 0/4 | Mới chỉ hướng tới CRUD; 8 SUT; ngẫu nhiên |
| 22 | K68 · APIRL: Deep Reinforcement Learning for REST API Fuzzing (2025) | ◐ | ◐ | ◐ | ◐ | 0/4 | Chỉ thêm key có trong schema nên bỏ sót bug; không đo coverage cho BitBucket, Spree |
| 41 | K02 · Test Amplification for REST APIs via Single and Multi-agent LLM Systems (2026) | Không | Không | Không | ◐ | 0/4 | 1 ứng dụng (PetStore); LLM có thể đã biết PetStore; mọi bug tính ngang nhau; 1 model, không tất định |
| 42 | K33 · Integrated Executive Dashboard on the PPMPP Portal (2026) | ◐ | ◐ | Không | Không | 0/4 | IPA chỉ 14 người; không đo hiệu năng; 100% chỉ là tỉ lệ đạt kịch bản định trước |


**Kết luận phần của K.Duy:** trong 8 bài được giao, **không bài nào ≥ 3/4 ô ✓**. Cao nhất là K49 với 1/4 (ô C: random search cùng thời gian, Table 8). Các bài còn lại 0/4. Phần của K.Duy cho kết quả: **RQ đứng vững trong phạm vi tài liệu đã tìm**, không khẳng định tuyệt đối.

Lưu ý với K49: random search ở đây là gray-box trong EvoMaster, chưa chắc đồng đều trên không gian input. Bảng gộp đã ghi điểm này, nên ô C của K49 nên xem là ✓ yếu.

## 3. Hạn chế cụ thể và trích nguyên văn (mỗi paper một câu trích)

| # | Paper | Hạn chế paper tự nêu | Trích nguyên văn | Mục / trang |
|---|---|---|---|---|
| 17 | K46 | Lỗi trong RESTest hoặc EvoMaster (đã mở rộng cả hai) có thể ảnh hưởng kết luận; thuật toán ngẫu nhiên; tác giả muốn thêm case study | "Faults in such tools might compromise the validity of our conclusions." | §VIII Internal validity, tr. 10 |
| 18 | K49 | Có thể cấu hình sai 7 công cụ; tác giả là chủ EvoMaster nên so sánh có thể thiên lệch; EMB có thể thiên về EvoMaster; ngẫu nhiên (3 hoặc 10 lần chạy) | "we might have misconfigured them" | §5 Threats to Validity, tr. 26 |
| 19 | K56 | Không hỗ trợ binary array; bug 8 và 9 chỉ có status code nên khó phân tích nguyên nhân | "Binary arrays can be supported by adding a FET" | §5.1, tr. 13 (bug 8 và 9 ở tr. 16) |
| 20 | K60 | Mã không dùng làm tăng mẫu số coverage; cách lưu unique identifier cần cải tiến (tr. 9); chỉ 1 Petstore; không có thí nghiệm so baseline | "if the unused code was removed, the coverage would increase" | §4, tr. 8 |
| 21 | K67 | Mới hướng tới CRUD; 8 SUT; ngẫu nhiên là mối đe dọa cho construct và conclusion validity | "more than CRUD-based APIs" | §9 Conclusions, tr. 34 (Threats ở §8, tr. 34) |
| 22 | K68 | Chỉ thêm key có trong schema nên không kích hoạt được một số bug; BitBucket là closed-source và Spree đa máy chủ nên không đo được coverage | "can only include parameter keys from the schema" | §4, tr. 5 (coverage ở tr. 4) |
| 41 | K02 | Chỉ 1 ứng dụng; LLM có thể biết PetStore; mọi bug tính ngang nhau; 1 model, không tất định | "Our evaluation is conducted on a single application, PetStore." | §6.3, tr. 14 |
| 42 | K33 | IPA chỉ 14 người, mang tính ban đầu; không đo response time, throughput, tài nguyên | "were not quantitatively measured" (nói về các chỉ số hiệu năng) | §3.2 Discussion, tr. 126 (PDF tr. 9) |

Ghi chú: ở K46, K49 và K67, hạn chế "gần RQ" như random cùng ngân sách hoặc mutant riêng biệt là nhận xét của người chấm (REVIEWER_INFERRED), không phải của tác giả. Tôi chỉ đưa vào cột này những hạn chế tác giả tự nêu.

**Gợi ý hạn chế để nhóm xét khi tìm gap** (chưa phải kết luận):
- **GAP-D (dữ liệu):** K02, K60 và K33 chỉ chạy trên 1 hệ thống; K46 chỉ 4 SUT; K67 8 SUT. Chưa bài nào dùng RESTestBench.
- **GAP-M (khía cạnh đo):** K46, K49, K56, K60, K67, K68 đo coverage, độ chính xác suy luận kiểu hoặc đếm 5XX/bug, không phải mutant riêng biệt theo oracle.
- **GAP-T (công cụ):** chưa bài nào làm EP+BVA kết hợp đúng nghĩa trên tham số request, có đối chứng random cùng ngân sách.

## 3b. Kết quả đối chiếu với `evidence-table-merged.md` và `rq-evidence-map.md`

Lưu ý: số thứ tự (#) trong `rq-evidence-map.md` **khác** `evidence-table-merged.md` (map xếp theo thứ hạng, bảng gộp xếp theo nguồn). Tôi đối chiếu theo **Mã (gộp)**.

| Mã | # trong bảng gộp | # trong map | Gần RQ (bảng gộp) | Ma trận P/I/C/O (map) | Rq-check của tôi |
|---|---|---|---|---|---|
| K46 | 17 | 12 | 0/4 ✓ · chạm 4/4 | ◐ ◐ ◐ ◐ | Khớp |
| K49 | 18 | 6 | 1/4 ✓ (C) · chạm 3/4 | ◐ · ✓ ◐ | Khớp |
| K56 | 19 | 22 | 0/4 ✓ · chạm 3/4 | · ◐ ◐ ◐ | Khớp |
| K60 | 20 | 30 | 0/4 ✓ · chạm 2/4 | ◐ · · ◐ | Khớp |
| K67 | 21 | 31 | 0/4 ✓ · chạm 2/4 | ◐ · ◐ · | Khớp |
| K68 | 22 | 13 | 0/4 ✓ · chạm 4/4 | ◐ ◐ ◐ ◐ | Khớp |
| K02 | 41 | 42 | 0/4 ✓ · chạm 1/4 | · · · ◐ | Khớp |
| K33 | 42 | 36 | 0/4 ✓ · chạm 2/4 | ◐ ◐ · · | Khớp |

Cả 8 dòng khớp giữa 3 nguồn (bảng gộp, map, rq-check). Hai ghi chú của map cần nhớ:
- **K49 (C ✓):** map ghi "uniform input distribution chưa xác nhận", nên đây là ✓ yếu. Tôi đã ghi điểm này ở mục 2.
- **K56 (C ◐):** map ghi ngân sách hai bên không bằng nhau (TnT 1.000/param lớn hơn Leif), nên chỉ ◐.

## 4. Đối chiếu nhãn tính mới trên thẻ RQ

- Thẻ FA26-EXT-12 trong `SWT302_Tuan_7.docx` chỉ liệt kê paper nền, không thấy nhãn new / extension / replication.
- Nhãn của tôi theo bảng mục 2: không paper nào giống ≥ 3/4, nên nghiêng về **new** trong phạm vi nguồn của tôi.
- Nếu nhãn máy gán trên thẻ web khác, ghi lý do tại đây: ___ (chờ PL xác nhận).

## 5. Rà nghiên cứu mạnh nhất gần đây (12 tháng gần nhất, từ 10/2025)

Thứ tự chọn: cùng bài toán/metric, rồi venue/benchmark lớn, rồi mới nhất. Tôi chỉ đọc abstract, trang bài hoặc trang replication package, chưa đọc toàn văn.

| Paper | Ngày | Đo gì | Chưa đo gì so với RQ của nhóm |
|---|---|---|---|
| RESTestBench: A Benchmark for Evaluating the Effectiveness of LLM-Generated REST API Test Cases from NL Requirements (arXiv 2604.25862; EASE 2026) | 28/04/2026 | Benchmark 3 dịch vụ REST cùng yêu cầu NL, metric mutation theo yêu cầu, đánh giá test do LLM sinh | Theo abstract: đối tượng so sánh là LLM với mức chi tiết yêu cầu. Không thấy so EP+BVA với random đồng đều cùng ngân sách. |
| Assessing REST API Test Generation Strategies with Log Coverage (arXiv 2604.07073) | 04/2026 | So EvoMaster, LLM và test viết tay trên Light-OAuth2 bằng log coverage | Metric là log coverage, không phải mutant. Không có EP/BVA. Dataset khác. |
| Vibe Testing for REST APIs: A Context-Taxonomic Benchmark of LLM-Generated Test Suites (replication package, Mendeley) | 25/06/2026 | LLM sinh, chạy, sửa test trên Bookstore 50 endpoint, có ma trận mutation | Can thiệp là LLM và ngữ cảnh, không phải EP/BVA. Dataset khác. Chỉ đọc mô tả package. |

**RQ của nhóm đo được điều gì mà các paper trên chưa đo:** so kỹ thuật thiết kế test không dùng AI (EP+BVA) với random đồng đều cùng ngân sách request, trên cùng RESTestBench, đếm số mutant riêng biệt theo dạng yêu cầu. Khác biệt nằm ở can thiệp (không phải LLM) và ở metric, không chỉ là "model mới hơn".

**Cần kiểm khi tải dataset:** bài RESTestBench và blog tác giả nêu 106 yêu cầu NL, còn thẻ RQ ghi 103. Có thể là khác phiên bản.

## 6. Ghi vào `search-log.md` (người chạy: K.Duy, ngày 17–18/10/2026)

| # | Truy vấn | Kết quả | Quyết định |
|---|---|---|---|
| 1 | `RESTestBench LLM-generated REST API test cases natural language requirements mutation benchmark` | Bài RESTestBench (arXiv 2604.25862), gợi ý Vibe Testing | Giữ cả hai (cùng benchmark/metric) |
| 2 | `boundary value analysis equivalence partitioning REST API random testing 2026` | Chủ yếu blog; 1 bài học thuật từ 2020 (arXiv 2001.06652) | Loại: ngoài 12 tháng gần nhất |
| 3 | `Assessing REST API Test Generation Strategies with Log Coverage` | arXiv 2604.07073 | Giữ (cùng bài toán REST API, 04/2026) |

## 7. Chưa kiểm chứng / cần lưu ý

- Số liệu K46, K49, K56, K60, K67, K68 đã đối chiếu với PDF và khớp bảng gộp. Chưa kiểm: "5 lần chạy" của K68.
- Hai ý trong cột Hạn chế của bảng gộp mà tôi **không tìm thấy** trong PDF nên không đưa vào cột hạn chế: K67 "prototype limitation (rest-news POST format)" và K56 "application-specific formats cần mở rộng FET". Cả hai đang gắn nhãn AUTHOR_STATED, nên Khôi (người chấm) nên kiểm lại nguồn.
- Ý "cải tiến cách lưu identifier" của K60 đã xác nhận ở tr. 9.
- Trang của K02 (LNCS) và K33 chưa đối chiếu số trang bản in; số trang trong bảng là trang trong PDF.
- Các paper ở mục 5 mới đọc abstract hoặc trang mô tả.
- Nhãn tính mới trên thẻ web chưa có, chờ PL.

## 8. Chỗ cần sửa trong `evidence-table-merged.md`

- **#42 (K33), cột Kết quả:** còn dính ghi chú của người chấm: "Cụm 'chưa đánh giá định lượng' không đúng, bài có số". Nên xoá cụm này, chỉ giữ số liệu.
- **#41 (K02), cột Code:** còn chữ "theo evidence-table cá nhân". Nên bỏ và ghi "Có reproduction package (figshare)" kèm link.
- **#17 (K46), cột Kết quả:** câu "hơn WB 1,2–60,3%, hơn BB 1,1–4,8% ở 3/4 SUTs" dễ hiểu nhầm. Theo PDF (tr. 8), HYBRID hơn WB ở cả 4 SUT và hơn BB ở 3/4 SUT.