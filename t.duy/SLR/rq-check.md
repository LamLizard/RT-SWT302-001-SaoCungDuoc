# Kiểm chứng RQ — phần của T.Duy

**Nguồn phụ trách:** Semantic Scholar + Google Scholar  
**Lớp bổ sung:** L 2 · **Ngày:** 18/10/2026 · **RQ:** FA26-EXT-12

**RQ:** Trên 45 yêu cầu của RESTestBench, phân hoạch tương đương kết hợp phân tích giá trị biên, so với sinh dữ liệu ngẫu nhiên đồng đều cùng ngân sách, khác nhau thế nào về số mutant riêng biệt bị phát hiện theo từng dạng yêu cầu?

**PICO:** P = 45 yêu cầu RESTestBench (15/dịch vụ); I = EP + BVA; C = random đồng đều cùng ngân sách request; O = số mutant riêng biệt được oracle xác nhận.

## 1. Bảng đối chiếu paper

Theo bản đồ nhóm: ✓ khớp, ◐ gần, · không khớp. O✓ cho mutation score là quy ước chấm của nhóm, **không đồng nghĩa unique mutant count**.

| Paper | P | I | C | O | Hạn chế paper nêu | Chi tiết |
|---|---|---|---|---|---|---|
| **TD-0002 — RestTSLLM** (2025), [DOI](https://doi.org/10.5753/sbes.2025.9670) | ◐: 6 REST API .NET | ✓: EP/BVA ở prompt và HTTP tests | ·: không random cùng budget | ✓: mutation score | “six open-source projects with relatively simple REST APIs” (§6, PDF p 9): phạm vi hệ phức tạp/công nghiệp còn hạn chế | **2✓, chạm 3/4**. §3/p 4: Category-Partition/EP/BVA. Table 3/p 8: Claude 3.5 Sonnet trung bình mutation **40,8%**, branch **71,7%**, success **100%** |
| **TD-0015 — Orchestration architecture** (2026), [DOI](https://doi.org/10.15587/2706-5448.2026.360928) | ◐: FastAPI, 42 yêu cầu | ✓: EP+BVA xác định | ·: không random | ·: coverage yêu cầu | “The behavior of the architecture on systems with 50+ endpoints was not tested” (PDF p 8/trang in 38): chưa thử hệ lớn | **1✓, chạm 2/4**. §3.2/p 5: EC(p), min/max±1. Table 3/p 6: coverage **90,2% / 75,1% / 68,3%** tương ứng tích hợp / OpenAPI / GPT-4; 20 lần chạy/cách |

**Kết luận cá nhân:** chưa thấy phản chứng đạt 3/4 hoặc 4/4 trong phạm vi kiểm. TD-0002 chưa dùng RESTestBench hoặc có nhánh random cùng request budget. Nhãn trên thẻ chưa có trong đầu vào để đối chiếu; PL chốt tính mới.

**Gap:** 2/2 bài Include, hai nhóm tác giả, tự nêu phạm vi thực nghiệm hạn chế → **GAP-D yếu**. Thiếu unique mutants/random là nhận xét đối chiếu, không phải hạn chế tác giả trực tiếp nêu. PL cần kiểm toàn bộ tập nhóm trước khi kết luận gap mạnh hay đã giải quyết.

**Đối chiếu 12 tháng gần nhất — 18/10/2025–18/10/2026:**

| Paper | Lý do chọn và khác RQ |
|---|---|
| TD-0015 (2026) | Gần I: EP+BVA; đo coverage yêu cầu, thiếu C và O của RQ |
| **TD-0029 — RESTestBench**, [arXiv](https://arxiv.org/abs/2604.25862), 28/04/2026 | Gần P/O: 106 yêu cầu, 228 mutants, 3 dịch vụ; không EP+BVA-vs-random. Không coi tập 106 yêu cầu là tập 45 của nhóm |
| **K100 — FDRRestTest**, [publisher](https://drops.dagstuhl.de/entities/document/10.4230/LIPIcs.ESEM.2026.20), 05/10/2026, ESEM | Gần baseline/ngân sách: 12 REST services, 5 đối chứng, budget 600 giây và một protocol fixed-request; FRE 0,9878 so 0,9294 là ước lượng có giới hạn. Không EP+BVA, không implementation-mutant outcome; không đáp ứng trọn RQ |

Ba bài được ưu tiên theo độ khớp I, P/O và thiết kế baseline; FDRRestTest bổ sung venue ESEM và benchmark 12 services. RestTSLLM tháng 09/2025 ngoài cửa sổ, vẫn là ứng viên chính. Overlay là đối chiếu L 2 riêng, không thay thử nghiệm EP+BVA; đã chạy hai query kết quả âm 18/10(search-log§6); chưa thấy phản chứng trực tiếp trong tập đã rà.

## 2. Lớp tìm kiếm bổ sung L 2

**Rà seed ngày 18/10:** K33 online 07/10, K100/FDRRestTest 05/10 mới hơn K19118/05. K02 năm in 2026 nhưng online 2025; K43 chỉ có năm 2026, chưa xác minh ngày: chưa khẳng định seed mới nhất toàn tập. K33/K100 là seed của tập Include nhóm, chỉ tra cứu, không thêm record của người khác vào 01.

| Lượt | Query/thao tác | Kết quả |
|---|---|---|
| L 2 mục tiêu | S 2 tra nguyên tiêu đề K33; nguyên tiêu đề K100 và `FDRRestTest` | Đều No Papers Found; không đọc được danh sách citations, không suy 0 citations |
| L 2 bổ trợ đã làm | K191, citing-papers |1/1 citation TD-0158, PDF 10 trang, EXCLUDE V2 IC-I; không có Include mới |
| Kết quả âm rộng | `"REST API" ("negative result" OR "did not improve" OR "fails") ("equivalence partitioning" OR "boundary value")` |~88 kết quả, thu 10 trangđầu; chưa bao phủ hết |
| Kết quả âm chặt | `"REST API" ("negative result" OR "did not improve") ("equivalence partitioning" OR "boundary value")` |7/7 kết quả; đã rà hết tập 7 |

**Kết quả:**17 lượt GS→11 bài mới; V 1 loại 9, V 2 loại 1(TD-0160:IC-E), Unsure 1(TD-0159:IC-T). TD-0159 có tên trong SRDS 2026 accepted/program nhưng bản proceedings chưa xác minh; không đưa vào 03/evidence. TD-0160 có EP/BVA§3.3/p 6, nhưng Table 1/2 chỉ cấu hình nên không đạtIC-E. Trích giới hạn tác giả “provides no marginal benefit over schema-driven baseline generation”(§6.1, PDF p 10) chỉ là đầu mối cho kết quả âm, không chứng minh EP+BVA kém random.

**L 2 chưa đủ bao phủ:** seed mục tiêu chưa tìm được trênS 2; không đủ 10–15 citations để đọc. Đã làm các bước tra cứu khả dụng và ghi giới hạn, không tự đánh dấu hoàn tất. [TD-0158 PDF](fulltext/TD-0158.pdf) được lưu làm dấu vết V2, không phải Include.

| Đối soát | Số hiện hành |
|---|---:|
| 01 / 02 (mỗi paper một dòng) |136/136|
| Lượt nguồn / gộp trùng |175/39|
| Loại V1 / cần toàn văn |76/60|
| Đã đọc / chưa lấy |59/1(FAMRES)|
| Loại V2 / Unsure đã đọc |55/2(Agentic, TD-0159)|
| 03 / evidence-table / luồng cá nhân |**2/2/2** —TD-0002, TD-0015|
| Snowball |91 lượt Tuần 6+1 L 2=92;64 bài mới;0 Include|

Kiểm:`175−39=136;136−76=60;60−1=59;59−55−2=2`. Search 72 unique+snowball mới 64=136. Ba bài Unsure tổng gồm một bài chưa toàn văn và hai bài đã đọc. SourceS 2/GS không cộng vào PRISMA tìm kiếm chính của nhóm. Nhật ký lệch hạn 05/10 và tra cứu mới:search-log§6–7.

## 3. Ghi chú khả thi từ các paper đã đọc

| Hạng mục | Bằng chứng và việc còn cần kiểm |
|---|---|
| Code | RestTSLLM có [GitHub](https://github.com/uffsoftwaretesting/RestTSLLM) và [Figshare](https://doi.org/10.6084/m9.figshare.29525768.v4), dùng .NET/xUnit/TSL; chưa xác minh chuyển nguyên sang harness RESTestBench |
| Dataset/oracle | [RESTestBench](https://github.com/casablancahotelsoftware/RESTestBench): paper 106 yêu cầu/228 mutants. Nhóm cần chốt đúng 45 ID, 15/dịch vụ, oracle và cách đếm mutant duy nhất |
| Ngân sách | Overlay: 10 phút/cách; Claude trong RestTSLLM: trung bình $0,47/dự án (Table 3). Đây là số của paper, không phải dự toán nhóm; cần cố định request budget, seeds và repeats |
| Rủi ro | Chưa chạy pilot trong lượt rà; chưa đủ số để chấm khả thi an toàn. Cần xác minh harness, mapping 45 yêu cầu và oracle trước chạy chính |

**Gửi PL:** đối chiếu nhãn new/extension/replication, kiểm gap trên toàn tập và tổng hợp vào `team-synthesis/rq-validation.md`; không đổi RQ trong lượt rà này.

**Đối chiếu tài liệu nhóm gửi 18/10:** đã kiểm PDF của đúng TD-0002/TD-0015 theo hàng 39–40 và explain. Điểm PICO và metric chính khớp; tách hạn chế tác giả/nhận xét người đọc. Riêng explain#40 nhầm baseline M_maint: Table 5, PDF p 7 là 65,7% specification/46,7%GPT-4/17,7%tích hợp, không phải 65,7%GPT-4. Đây là đối chiếu bằng tài liệu tham khảo, chưa có xác nhận tên/ngày của người kiểm chéo.

**Phần cần PL/thành viên xác nhận:** nhãn trên thẻ; gap ban đầu ghi trước khi đếm; đối chiếu gap trên tập nhóm; ngày dừng search chung. Không tự thay nhãn/đổiRQ hay xác nhận đã chạy pilot. Ba bài gần đây được chọn vì đúng phần P/O, I và baseline/ngân sách, không xếp hạng toàn ngành; PL tổng hợp cùng các nguồn khác.

**Mẫu kiểm chéo độc lập —chưa thực hiện:**

| Phần | Mẫu tối thiểu và mã bài | Người/ngày/kết quả |
|---|---|---|
|V1|28 paper:TD-0001, TD-0002, TD-0003, TD-0006, TD-0015, TD-0016, TD-0018, TD-0029, TD-0039, TD-0041, TD-0054, TD-0070, TD-0083, TD-0104, TD-0130, TD-0132, TD-0136, TD-0151, TD-0152, TD-0156, TD-0157, TD-0158, TD-0159, TD-0160, TD-0161, TD-0162, TD-0167, TD-0168|CHỜ|
|V2|12 paper:TD-0002, TD-0015, TD-0006, TD-0136, TD-0158, TD-0159, TD-0160, TD-0001, TD-0003, TD-0004, TD-0007, TD-0008|CHỜ|
|Evidence|TD-0002(1/2 hàng); khuyến nghị kiểm cảTD-0015|CHỜ|

Không tính kiểm số bằng script hoặc AI tự đọc lại là kiểm chéo độc lập.
