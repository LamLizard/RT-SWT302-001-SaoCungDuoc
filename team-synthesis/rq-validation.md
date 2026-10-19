# Kiểm chứng RQ — FA26-EXT-12 (nhóm 1 · SaoCungDuoc)

*Cập nhật đối chiếu: 20/10/2026 (Asia/Saigon). N = 42 là số paper trong bảng gộp hiện tại; các nguồn rà bổ sung được trình bày riêng, không cộng vào N.*

**Phạm vi kiểm chứng:** tính lại ma trận P/I/C/O, đối chiếu 5 file cá nhân, đọc các mục PDF được dẫn ở dưới và kiểm nguồn công khai của Guo/RESTestBench. Đây không phải lần screening lại toàn văn cả 42 bài hoặc kết quả chạy benchmark. “Theo rubric” khác với “khớp đầy đủ RQ”; quyết định thiết kế khác với bằng chứng thực nghiệm.

## 0. Bảng đối chiếu cá nhân

| Thành viên | File nguồn | Paper chính | Nhãn trong nguồn cá nhân | Điểm theo rubric nhóm |
|---|---|---|---|---|
| Lâm | [rq-check](../lam/SLR/rq-check.md) | 8 (#6, #10–#16) | `new` trong phạm vi đã xét | 8 bài 0/4 |
| Khôi | [rq-check](../khoi/SLR/rq-check.md) | 8 (#23–#30) | `new` trong phạm vi đã xét | 8 bài 0/4 |
| Tùng | [rq-check §1.2](../tung/SLR/rq-check.md) | 8 (#1–#5, #7–#9), thêm 4 nguồn tham chiếu | Chưa xác thực `extension` | **4 bài 1/4:** K52/P53, K90, K34, K102; **4 bài 0/4** |
| T.Duy | [rq-check](../t.duy/SLR/rq-check.md) | 10 (#31–#40) | `new` trong phạm vi đã xét | TD-0002: 2/4; TD-0015: 1/4; 8 bài 0/4 |
| K.Duy | [rq-check §2.1–2.3](../k.duy/SLR/rq-check.md) | 8 (#17–#22, #41–#42) | `new` trong phạm vi đã xét | **K49: 1/4; 7 bài 0/4** |

Tổng: **42 paper = 35 bài 0/4 + 6 bài 1/4 + 1 bài 2/4**. Số thứ tự # theo [bảng gộp](evidence-table-merged.md), không phải thứ tự trong [ma trận](rq-evidence-map.md). Nhãn cá nhân được giữ đúng phạm vi nguồn, không dùng như phiếu biểu quyết tính mới.

## 1. RQ và thiết kế P/I/C/O/S

**RQ đang lưu trong repo:** Trên 45 yêu cầu của RESTestBench, phân hoạch tương đương kết hợp phân tích giá trị biên, so với sinh dữ liệu ngẫu nhiên đồng đều cùng ngân sách, khác nhau thế nào về số mutant riêng biệt bị phát hiện theo từng dạng yêu cầu, khi một mutant chỉ được tính nếu test vượt qua bản gốc nhưng thất bại trên mutant theo oracle của benchmark?

- **P — đã thống nhất phương án ngày 20/10/2026:** 45 yêu cầu riêng biệt: **16 FastAPI + 15 NestJS RealWorld + 14 TodoApp**. Thay cho quy tắc cũ 15/dịch vụ; chưa có danh sách 45 ID hoặc snapshot benchmark được khóa.
- **I:** EP+BVA kết hợp, chọn dữ liệu request từ yêu cầu và schema API; giữ cùng thông tin đầu vào và oracle giữa hai nhánh.
- **C:** uniform random cùng số request cho từng yêu cầu; miền lấy mẫu và B cụ thể còn phải khóa theo §1.2.
- **O:** số mutant riêng biệt pass bản gốc/fail mutant theo oracle requirements-based. Lưu khóa `(service, requirement_id, mutant_index)` và đối chiếu định danh mutant trong artifact; không tự coi index cục bộ là ID toàn benchmark. Một mutant bị phát hiện nhiều lần trong cùng lượt chỉ đếm một lần; không cộng số kill của 10 lượt thành số mutant riêng biệt.
- **S — kế hoạch, chưa thực hiện:** 10 lượt/kỹ thuật/yêu cầu; lịch seed tái lập được; Wilcoxon signed-rank hai phía và Holm là phương án phân tích có điều kiện, chưa phải kiểm định đã xác nhận phù hợp dữ liệu.

**Trạng thái thẻ W6/ý kiến GV:** bản nháp cũ ghi nhãn thẻ là `extension`, nhưng các rq-check cá nhân mô tả trạng thái thẻ khác nhau. Lần đối chiếu này chưa có bản thẻ hoặc phản hồi GV gốc để xác minh. Không suy nhãn từ `EXT` trong mã đề tài và không khẳng định thẻ đã được cập nhật. Cần ghi nhận thay đổi P khi đối chiếu với GV/thẻ chính thức.

### 1.1. Quy tắc lấy mẫu cần áp dụng

1. Khóa commit RESTestBench, đếm file requirement/mutant thực tế và lưu manifest. [README Dataset](https://github.com/casablancahotelsoftware/RESTestBench#dataset) ghi 63/26/14 = 103; [paper Table 3](https://arxiv.org/html/2604.25862v1#S3.T3) ghi 63/29/14 = 106. Chưa giải thích được đầy đủ chênh lệch RealWorld; không trộn mẫu số từ hai phiên bản.
2. Định nghĩa dạng yêu cầu từ requirement/schema trước khi xem kết quả hai kỹ thuật. Lập ánh xạ ID → dạng và quy tắc xử lý yêu cầu có nhiều dạng. Danh mục cụ thể chưa được kiểm kê, nên chưa gán hạn ngạch hoặc khẳng định đủ mẫu mỗi dạng.
3. Trong FastAPI/RealWorld, lấy mẫu không hoàn lại, phân tầng theo dạng với phân bổ gần tỷ lệ của từng dịch vụ; lưu quy tắc làm tròn, thuật toán, thứ tự ID và seed. TodoApp lấy cả 14 nếu đáp ứng tiêu chí dữ liệu/chạy được đã công bố. Nếu không đủ yêu cầu hợp lệ, báo lệch kế hoạch thay vì tự thêm/trùng mẫu.
4. Cố định cùng 45 yêu cầu và tập mutant tương ứng cho cả hai kỹ thuật trong mọi lượt. Không chọn lại mẫu vì kết quả bất lợi. Báo cáo theo dịch vụ/dạng; không coi phân bổ 16–15–14 là mẫu tỷ lệ đại diện toàn dataset.

### 1.2. Các điều kiện phải khóa trước lần chạy chính

| Nội dung | Quy tắc / trạng thái hiện tại |
|---|---|
| Request budget B | **Chưa chốt số.** Pilot dùng để chọn B khả thi, sau đó cố định trước chạy chính; quy định request chuẩn bị trạng thái, xác thực, retry và replay tính vào đâu. Hai nhánh phải theo cùng quy tắc. |
| Uniform random | **Chưa chốt miền.** Công bố giới hạn số/độ dài, bảng ký tự, enum, null/optional và cách ghép nhiều tham số. Không dùng từ “uniform” cho miền chưa xác định; không tự cho random quota theo các phân hoạch EP nếu điều đó đổi baseline đã nêu. |
| EP+BVA | Công bố cách lập lớp, chọn đại diện, chọn biên và xử lý trường hợp số test thiết kế khác B; cùng requirement/schema/oracle với random. Chưa có generator được xác minh chạy. |
| Phiên bản mô tả yêu cầu | Benchmark có precise/vague; **chưa chốt biến thể dùng cho thí nghiệm**. Chọn và giữ cùng biến thể cho hai kỹ thuật. Nếu chạy cả hai, tách thành hai điều kiện; không đếm thành 90 requirement riêng biệt và phải tính lại khối lượng. |
| Oracle và lỗi chạy | Kiểm tĩnh evaluator xác nhận điều kiện pass bản gốc mới tính kill; chưa chứng minh harness của nhóm hoạt động. Phải phân biệt lỗi hạ tầng/timeout với assertion phát hiện mutant, công bố chính sách trước chạy. |
| Seed | Lưu lịch 10 seed khác nhau theo lượt, tái lập được; seed lấy mẫu tách khỏi seed sinh input. Nếu EP+BVA tất định, nói rõ các lượt có thể trùng; không gọi chúng là 10 mẫu độc lập. |
| Đơn vị phân tích | **Đề xuất:** với mỗi requirement và kỹ thuật, lấy trung bình số unique kills của 10 lượt; ghép cặp theo cùng requirement, không coi 45×10 là 450 requirement độc lập. Lưu cả phân bố từng lượt. |
| Kiểm định / CI | Wilcoxon chỉ dùng sau khi xem xét tính ghép cặp, giả định của phân phối chênh lệch và phụ thuộc trong cùng dịch vụ/endpoint. Chốt xử lý ties/zeros, phương pháp p-value, effect size, cách tính CI 95%, alpha và họ kiểm định Holm trước chạy chính. Với nhóm nhỏ hoặc giả định không bảo vệ được, chỉ báo cáo mô tả hoặc khóa phương án khác trước chạy; không khẳng định có power đủ. |
| Ngưỡng thực tiễn θ | Chưa có con số/nguồn thống nhất. Tách khỏi H0 và khóa trước chạy chính; không tự chọn θ theo kết quả thuận lợi. |

Nguồn kiểm oracle: [RESTestBench evaluator, `evaluate_test`](https://github.com/casablancahotelsoftware/RESTestBench/blob/master/src/evaluator.py). Giới hạn Wilcoxon/ties/zeros: [SciPy 1.17, `wilcoxon`](https://docs.scipy.org/doc/scipy-1.17.0/reference/generated/scipy.stats.wilcoxon.html). Các quy tắc đề xuất trên là thiết kế của nhóm, không phải kết quả đã chạy hoặc nguyên văn thẻ W6.

## 2. Bằng chứng làm nền (N = 42)

Điểm bên dưới tính lại từ **42 hàng trong §3 của rq-evidence-map**, giữ rubric hiện có để đối chiếu; không đổi điểm nguồn chỉ để khớp nhãn mong muốn.

| Yếu tố | ✓ theo rubric | ◐ gần | · khác | Giới hạn |
|---|---:|---:|---:|---|
| P | 0 | 28 | 14 | Ma trận hiện tại không có bài dùng RESTestBench |
| I | 2 | 21 | 19 | TD-0002: prompt có boundary/equivalence classes; TD-0015: module G sinh test bằng EP/BVA |
| C | 5 | 25 | 12 | K52/P53, K90, K34, K102, K49; rubric chấp nhận cùng số test/call hoặc thời gian, chưa xác nhận uniform cùng request budget |
| O | 1 | 32 | 9 | TD-0002 có mutation score, chưa chứng minh cùng cách đếm/oracle/phân tầng của RQ |

**Tổng điểm:** 35 bài 0 ✓, 6 bài 1 ✓, 1 bài 2 ✓; **0/42 bài ≥3 ✓**. Có 8 ô ✓ trên toàn ma trận (2 I + 5 C + 1 O).

**Không đồng nhất rubric với RQ:** I chấp nhận EP và/hoặc BVA, C chấp nhận cả cùng thời gian, O chấp nhận mutation score. RQ yêu cầu EP+BVA kết hợp, uniform random cùng request budget và unique kills theo oracle/dạng yêu cầu. Điểm ✓ chưa xác nhận đầy đủ các điều kiện đó.

**Về số lượng tài liệu:** N = 42 vượt ngưỡng 12 đang dùng trong bản nháp; việc này không tự chứng minh độ phủ tìm kiếm/tính mới và không phải căn cứ miễn L1/L2/L3. [rq-evidence-map §4](rq-evidence-map.md) vẫn ghi cần săn tìm có mục tiêu; chưa có hướng dẫn GV gốc cho phép bỏ bước này. N cũng chưa được tái xác nhận bằng một vòng screening IC/EC mới trong lần sửa này.

## 3. Phản chứng và nhãn tính mới

### 3.1. Trong 42 paper

- Cao nhất theo rubric: **TD-0002 2/4 (I, O)**; 6 dự án .NET, không có nhánh random cùng budget. Đối chiếu [PDF](../Paper-source/39-TD-0002.pdf): §3/PDF4 (prompt), §4/PDF6–7 (dataset/Stryker.NET), Table 3/PDF8 (mutation score 40,8%).
- Nhóm 1/4: K52/P53, K90, K34, K102, K49 (C), TD-0015 (I). [TD-0015 §3.2/PDF6](../Paper-source/40-TD-0015.pdf) thực sự có script Python tạo lớp tương đương/biên; không mô tả nó chỉ là prompt hoặc khẳng định chưa phải generator.
- **Kết luận giới hạn:** chưa có ứng viên ≥3/4 trong tập 42 theo rubric hiện tại. Các nguồn cá nhân dùng nhãn `new` trong phạm vi đã xét; điều đó không xác nhận nhãn cho toàn bộ tài liệu.

### 3.2. Nguồn bổ sung ngoài 42

[Khôi §5](../khoi/SLR/rq-check.md) ghi ngày rà **18/10/2026**; 04–06/2026 là mốc bài, không phải ngày tìm kiếm. Bộ lọc 2025–2026 cũng không tự bảo đảm cửa sổ đúng 12 tháng (20/10/2025–20/10/2026).

| Nguồn | Kết quả đối chiếu và mức kiểm chứng |
|---|---|
| [RESTestBench](https://arxiv.org/html/2604.25862v1) | Theo rubric: P/O, 2/4; benchmark và metric làm nền, không có phép so EP+BVA–random của nhóm. Table 3: 106 yêu cầu/228 mutations theo paper; §6 nêu giới hạn 3 dịch vụ và 3 repetitions. Đây không phải số đếm đã xác nhận cho artifact nhóm sẽ chạy. |
| Req2REST-Guard | Khôi ghi 2/4 (P/O), nhưng cũng ghi tên dịch vụ không khớp RESTestBench và Table I mâu thuẫn văn bản. Lần sửa này chưa có full text nguồn trong repo để kiểm độc lập; **P và điểm 2/4 chỉ là ghi nhận từ rq-check, chưa xác nhận**, không dùng để khẳng định đã có một nghiên cứu khác dùng đúng dataset. |
| [MASTOR](https://arxiv.org/abs/2606.10465) | Trang tác giả xác nhận hướng sinh oracle. Khôi chấm O, 1/4; điểm chi tiết kế thừa nguồn cá nhân, chưa tái chấm toàn văn trong lần sửa này. |
| MioHint, RESTOR, R2R-04 amplification | [Tùng §2](../tung/SLR/rq-check.md) chấm 0/4 theo rubric. Đây là kết quả nguồn cá nhân, không phải ba phép tái lập đã thực hiện; chưa thấy bằng chứng về phép so input của RQ trong các đối chiếu đó. |

Không dùng bảng này để khẳng định đã rà hết nghiên cứu mới nhất hoặc xác nhận tính mới tuyệt đối. Guo được xét riêng ở §3.3, nên câu “không paper nào ≥3/4” chỉ áp dụng cho tập 42 ở §3.1.

### 3.3. Guo 2024: gần theo rubric, khác khi đối chiếu đầy đủ RQ

[Guo, Okamura & Dohi (2024), *Optimal test case generation for boundary value analysis*, Software Quality Journal 32, 543–566](https://link.springer.com/article/10.1007/s11219-023-09659-9), DOI `10.1007/s11219-023-09659-9`.

| Yếu tố | Theo toàn văn | Điểm rubric / giới hạn so với RQ |
|---|---|---|
| P | 5 chương trình non-REST (§5.4) | ·; khác dataset |
| I | BCD/BVA; phân hoạch và biên lấy từ phân tích mã (§5.4–5.5) | ✓ rộng; khác generator black-box từ requirement/schema |
| C | RT và bộ tối ưu cùng cỡ test; RT sinh riêng từng phân hoạch (§5.2, §5.5) | ✓ rộng; chưa chứng minh uniform trên toàn miền. Uniform ở §5.5 nói về proposal khi tối ưu |
| O | Kill rates; mutant được tính khi đường thực thi khác bản đúng (§5.1; kết quả §5.6) | ✓ rộng; khác oracle requirements-based pass/fail |

**Kết luận:** Guo là ứng viên **3/4 theo rubric rộng**, có giá trị đối chiếu. Không được viết “chỉ khác P” hoặc tự hạ thành 2/4 vì chưa xác nhận uniform: rubric C hiện tại không đòi điều kiện đó, và 5 bài C✓ trong N=42 cũng đang dùng cùng quy tắc rộng.

**Nhãn làm việc: `extension` theo rubric rộng có ứng viên 3/4; chưa xác thực nhãn chính thức trên thẻ/GV.** Không đổi tự động sang `new` từ việc C chưa khớp hoàn toàn. Nếu sửa rubric cho sát RQ, phải chấm lại nhất quán toàn bộ tập liên quan và giải thích nhãn sau đó. Không dùng nhãn thẻ chưa xác minh làm bằng chứng cho điểm paper.

## 4. Khả thi: trạng thái có bằng chứng

| Hạng mục | Đã có căn cứ | Chưa xác nhận |
|---|---|---|
| Dataset | README công bố đủ số lượng cho phân bổ 16–15–14 | Commit, 45 ID, tiêu chí hợp lệ và tổng mutant của mẫu |
| API/tool | Repo có hướng dẫn Docker và tool adapter Python | Build/chạy 3 dịch vụ, golden test và adapter của nhóm |
| Generator/oracle | Có evaluator upstream; định nghĩa I/C đã nêu | Chưa có bằng chứng 2 generator EP+BVA/random của nhóm chạy đúng |
| Khối lượng | 45×2×10 = **900 lượt kỹ thuật–yêu cầu cho một điều kiện precise hoặc vague** | B, HTTP executions, replay/reset/retry, số mutant thật, số điều kiện và runtime |
| Nguồn lực/thời gian | Chưa có số đo pilot trong repo | Không xác nhận RAM 16 GB đủ hoặc hoàn thành 1–2 ngày |

Bỏ ước lượng **~97 mutant** làm căn cứ tài nguyên: đó là phép nội suy 228/106×45 từ toàn benchmark theo paper, không phản ánh phân bổ 16–15–14 hoặc số mutant thật của mẫu. Giữ 900 như số lượt kế hoạch, không gọi là số HTTP executions. Không đánh dấu khả thi ✅ khi chưa chạy.

**Pilot dự kiến:** 5 yêu cầu có mặt cả 3 dịch vụ, chọn trước khi so kết quả; kiểm setup, oracle, ngân sách, reset và runtime. Đây là đề xuất thử kỹ thuật, chưa thực hiện và chưa chứng minh power thống kê. Phải ghi rõ nếu dữ liệu pilot dùng để điều chỉnh thiết kế; không trộn vào kết quả xác nhận mà không công bố.

## 5. Gap và lợi ích có thể bảo vệ

### 5.1. GAP-T — nhận định của nhóm, không phải hạn chế tác giả tự nêu

Câu “chưa ai thử EP+BVA” trong bản nháp cũ là giả thuyết tìm kiếm, không phải kết luận được chứng minh. Ma trận có **2 bài I✓ và 40 bài không I✓**; không suy từ đó thành “40 tác giả nêu thiếu EP+BVA” hoặc “40 bài hoàn toàn không có EP/BVA”.

- TD-0002 có EP/BVA trong prompt; TD-0015 có module G tạo test bằng EP/BVA.
- Trong đối chiếu 42 bài hiện tại, **chưa tìm thấy phép so kết hợp EP+BVA với uniform random cùng request budget trên RESTestBench**, đo unique kills theo dạng yêu cầu và oracle đã định nghĩa.
- Đây là **khoảng trống quan sát trong phạm vi đối chiếu**, còn phụ thuộc độ phủ tìm kiếm và kiểm chứng phương pháp; không gọi là gap mạnh author-stated.

### 5.2. GAP-D — các hạn chế trực tiếp đã truy vết

Bản cũ ghi “11 nhóm, chỉ K89/K32 có quote” không còn phản ánh đủ nguồn hiện có. Lần sửa này đối chiếu được các đoạn sau (diễn giải, không phải trích nguyên văn):

| Paper đại diện | Hạn chế tác giả nêu | Vị trí đã đọc trong PDF repo |
|---|---|---|
| [K46](../Paper-source/17-K46.pdf) | Chỉ 4 REST APIs; thực nghiệm system-level tốn thời gian | Threats to Validity, External validity, PDF10 |
| [K32](../Paper-source/26-K32.pdf) | Không suy kết quả cho REST API bất kỳ; cần case studies mới | §V.E, External validity, PDF9 |
| [P12/K81/K55](../Paper-source/03-P12-K81-K55.pdf) | Benchmark 20 services có thể không khái quát | §4.6, PDF10 |
| [K66](../Paper-source/10-K66.pdf) | Chỉ đánh giá 11 REST APIs; có thể khác hiệu năng trên API/miền ứng dụng khác; xác thực/quota cản trở đánh giá rộng hơn | §5, External threats to validity, PDF10 |
| [TD-0015](../Paper-source/40-TD-0015.pdf) | 5 endpoints chỉ là quy mô tối thiểu; chưa thử hệ 50+ endpoints | PDF8, đoạn bàn về giới hạn thực nghiệm trước §3.4 |
| [K02](../Paper-source/41-K02.pdf) | Một ứng dụng PetStore; khó suy sang API có đặc điểm khác | §6.3, PDF14 |
| [K89](../Paper-source/30-K89.pdf) | Chỉ hai targets; chưa repeated randomized trials/statistical testing | §5.4, PDF27 |
| [K93](../Paper-source/31-K93.pdf) | Ít dịch vụ, lựa chọn dịch vụ ảnh hưởng khả năng khái quát | §7.1, PDF21 |
| [K166](../Paper-source/35-K166.pdf) | Năm subject APIs có thể chưa khái quát tiếp | §V.B, PDF7 |

Đây là **9 paper có đoạn trực tiếp đã đọc**, không phải 9 nhóm tác giả độc lập; có thể chồng lấn tác giả/lab. Chưa hoàn tất quy tắc gộp nhóm nên không chốt con số nhóm độc lập hoặc gọi gap “mạnh” chỉ bằng số đếm. K66 được bổ sung ở lượt double-check thứ hai ngày 20/10/2026.

Danh sách cũ còn cụm Karlsson K37/K67: chưa xác nhận đủ phát biểu trực tiếp cùng hạn chế “ít SUT” trong lần đối chiếu này; không cộng vào số trên. K67/PDF34 nói 8 SUT và bàn external validity, chưa đủ để diễn giải thành tác giả tự thừa nhận mẫu nhỏ. **K33** là đánh giá portal/IPA 14 người, không dùng 14 người làm cỡ mẫu API/SUT.

**Quan hệ với RQ:** 45 yêu cầu vẫn thuộc 3 dịch vụ; thiết kế này **không giải quyết GAP-D** và không kiểm định khả năng khái quát sang dịch vụ mới. GAP-D là giới hạn/tham chiếu phụ, không phải đóng góp đã lấp.

### 5.3. GAP-M — bằng chứng trực tiếp và nhận định phải tách riêng

[K49, §4.5.1/PDF17](../Paper-source/18-K49.pdf) nêu tác giả chưa biết công cụ mutation testing hướng system testing và khó khăn khi test/SUT khác ngôn ngữ. Đây là nhận định tại thời điểm bài đó, không phải chứng minh hiện nay không có tool.

TD-0002 có mutation score (Table 3/PDF8); việc chưa báo cáo cùng cách đếm unique kills/theo dạng yêu cầu là nhận định khi đối chiếu với RQ. Không gộp K07/K21/K02/bBOXRT/K33 thành “6 tác giả cùng nêu hạn chế metric” khi chưa có phát biểu trực tiếp tương ứng. **GAP-M chỉ giữ như động cơ chọn phép đo, chưa xác nhận gap mạnh hoặc mới trên toàn tài liệu.**

### 5.4. Paper gần để trình bày và phạm vi đóng góp

Dùng **Guo ở §3.3** để trình bày quan hệ BVA–random–mutation, kèm khác biệt phương pháp/oracle; dùng **RESTestBench ở §3.2** để trình bày nguồn benchmark/oracle. Không gọi Guo là paper gần nhất tuyệt đối khi chưa có xếp hạng tìm kiếm đầy đủ. Đóng góp dự kiến là phép so input EP+BVA–uniform random cùng ngân sách trên mẫu đã định, không phải kết quả chứng minh kỹ thuật nào tốt hơn hoặc giải quyết hạn chế ít SUT.

### 5.5. Lợi ích và cách diễn giải kết quả

Người dùng kết quả là kỹ sư kiểm thử REST API và nhóm nghiên cứu benchmark; họ có thể cân nhắc kỹ thuật theo dạng yêu cầu **trong phạm vi mẫu và ngân sách đã chạy**.

- **H0 không bị bác bỏ:** chưa đủ bằng chứng về khác biệt theo phép kiểm định; không kết luận tương đương, random tốt bằng EP+BVA hoặc EP+BVA không có lợi ích. Xem CI/độ lớn hiệu ứng và giới hạn thiết kế.
- **H0 bị bác bỏ, EP+BVA có kết quả tốt hơn:** chỉ cân nhắc ưu tiên sau khi xét chiều, độ lớn hiệu ứng, CI, ngưỡng thực tiễn và hiệu chỉnh so sánh.
- **H0 bị bác bỏ, EP+BVA có kết quả kém hơn:** báo cáo lợi thế của random trong phạm vi đó; không tự ưu tiên EP+BVA.
- **Kết quả chưa kết luận:** báo cáo bất định/giới hạn. Không tự tăng số lượt đến khi p có ý nghĩa; mọi nghiên cứu bổ sung phải có kế hoạch và báo cáo riêng.
- **GAP-D:** p-value của phép so hai kỹ thuật không xác nhận tính đại diện của dataset hoặc RESTestBench là “benchmark chuẩn”. Muốn xét khái quát cần thêm dịch vụ và thiết kế đánh giá tương ứng.

Cơ sở diễn giải: [ASA, nguyên tắc về p-values](https://www.amstat.org/asa/files/pdfs/P-ValueStatement.pdf); ý nghĩa thống kê không đo độ lớn hay tầm quan trọng của hiệu ứng.

## 6. Quyết định và việc còn mở

- **Giữ câu RQ 45 yêu cầu và I/C/O; đã đổi quy tắc chọn P** từ 15/dịch vụ sang **16 FastAPI + 15 RealWorld + 14 TodoApp**, theo thống nhất 20/10/2026. Không viết “mọi thay đổi: không có”. Ghi nhật ký và đối chiếu thẻ/GV; chưa xác nhận đã thông báo.
- **Nhãn làm việc:** `extension` **theo rubric rộng**, với Guo 3/4; **nhãn chính thức chưa xác minh**. Không dùng đồng nhất “3/4 rộng” với “chỉ đổi P, I/C/O giống hệt”.
- **Gap chính:** GAP-T là nhận định quan sát của nhóm trong phạm vi nguồn đã đối chiếu. **GAP-D:** giới hạn chưa được RQ giải quyết; có 9 paper trực tiếp đã truy vết, chưa chốt số nhóm độc lập. **GAP-M:** động cơ phép đo, bằng chứng trực tiếp chủ yếu từ K49.
- **Chưa hoàn tất:** commit/danh sách 45 ID, tổng mutant thật, phân loại yêu cầu, B/miền uniform, hai generator, pilot/runtime, kế hoạch suy luận/CI/θ và đối chiếu thẻ/GV. Các việc này chưa có dữ liệu hoặc quyết định đủ để đánh dấu hoàn thành.

## 7. Dấu vết đối chiếu ngày 20/10/2026

- Tính lại đúng 42 hàng ma trận: P 0/28/14; I 2/21/19; C 5/25/12; O 1/32/9 (thứ tự ✓/◐/·). Tổng điểm và bảng cá nhân đối chiếu theo mã paper.
- Đọc các mục PDF cụ thể được dẫn ở §3.1, §5.2–5.3; không tuyên bố tái screening toàn văn 42 bài. Các nguồn bổ sung kế thừa rq-check được ghi rõ mức kiểm chứng ở §3.2.
- Đối chiếu Guo toàn văn web (§5.2, §5.4–5.6); RESTestBench paper Table 3/§3/§6, README và evaluator; SciPy 1.17 và ASA cho giới hạn thống kê. Chưa khóa commit artifact, chưa chạy Docker/benchmark hoặc tạo số đo thực nghiệm.
- Bản này thay các kết luận không đủ căn cứ trong draft v3; các file cá nhân giữ nguyên như nguồn lịch sử. Nội dung thiết kế hiện hành lấy theo §1/§6, không dùng các câu 15/dịch vụ cũ trong nguồn cá nhân để chạy mẫu mới.
- **Double-check lần hai, cùng ngày:** xác nhận bảng gộp có 42 mã khác nhau, thứ tự #1–#42; bổ sung K66/§5/PDF10 cho GAP-D (9 paper, chưa đếm nhóm độc lập); sửa locator K49 thành §4.5.1/PDF17 và mô tả locator TD-0015 chính xác theo PDF8. Bổ sung điều kiện precise/vague và giới hạn của phép tính 900 lượt. Không thay N, điểm ma trận, mẫu P hoặc nhãn làm việc.
