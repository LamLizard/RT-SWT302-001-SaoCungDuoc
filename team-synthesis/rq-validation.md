# Kiểm chứng RQ — FA26-EXT-12 · SaoCungDuoc

**Cập nhật:** 20/10/2026. Trình bày theo mẫu nhóm của [RBL-2](RBL-2-Kiem-chung-RQ-full.md). Nguồn kiểm chứng chi tiết: [nhật ký đối chiếu](rq-validation-audit.md).

## 1. RQ (nguyên văn trên thẻ) + PICO

**RQ đang lưu trong hồ sơ nhóm:** Trên 45 yêu cầu của RESTestBench, phân hoạch tương đương kết hợp phân tích giá trị biên, so với sinh dữ liệu ngẫu nhiên đồng đều cùng ngân sách, khác nhau thế nào về số mutant riêng biệt bị phát hiện theo từng dạng yêu cầu, khi một mutant chỉ được tính nếu test vượt qua bản gốc nhưng thất bại trên mutant theo oracle của benchmark?

| Yếu tố | Nội dung |
|---|---|
| **P** | 45 yêu cầu RESTestBench; phương án phân bổ hiện tại: **16 FastAPI + 15 NestJS RealWorld + 14 TodoApp**, thay cho 15 yêu cầu/dịch vụ. Chưa khóa commit và danh sách ID. |
| **I** | Phân hoạch tương đương kết hợp phân tích giá trị biên (**EP+BVA**), sinh dữ liệu request từ yêu cầu và schema. |
| **C** | Sinh dữ liệu ngẫu nhiên đồng đều (**uniform random**), cùng ngân sách request với I. Miền lấy mẫu và ngân sách B chưa chốt. |
| **O** | Số mutant riêng biệt bị phát hiện theo từng dạng yêu cầu; test phải pass bản gốc và fail mutant theo oracle benchmark. |

**Điều kiện dùng chung:** cùng yêu cầu, schema, assertions nghiệp vụ và quy tắc tính budget cho hai kỹ thuật. Precise/vague, cách phân loại yêu cầu và cách xử lý reset/retry/timeout còn cần xác định. Kế hoạch hiện có là 10 lượt/kỹ thuật/yêu cầu; đây chưa phải kết quả thực nghiệm.

**Nội dung cần xác nhận trên thẻ:** phân bổ P đã đổi thành 16–15–14; chưa ghi nhận ngày thông báo thay đổi này cho GV. Câu RQ trên được giữ theo hồ sơ hiện có, chưa tự coi là bản thẻ đã cập nhật.

## 2. Bằng chứng làm nền (N = 42 paper)

**Bước 1 — kiểm evidence table:** người phụ trách xác nhận các thành viên đã kiểm các cổng P trước khi gộp. Bảng nhóm có **42 paper ≥12**; 42/42 hàng có Tool/LLM, kết quả số và hạn chế; metric được ghi cụ thể. P1 là ngưỡng của bảng nhóm, không phải chỉ tiêu 12 paper/người.

Tổng hợp từ [evidence-table-merged](evidence-table-merged.md) và [rq-evidence-map](rq-evidence-map.md):

| Yếu tố | ✓ | ◐ | Khác | Nhận xét chính |
|---|---:|---:|---:|---|
| P | 0 | 28 | 14 | Trong tập 42 chưa có paper dùng đúng RESTestBench; paper benchmark được xét bổ sung ở §3. |
| I | 2 | 21 | 19 | TD-0002 có EP/BVA trong prompt; TD-0015 có module G sinh lớp tương đương/giá trị biên. |
| C | 5 | 25 | 12 | K52/P53, K90, K34, K102, K49 đạt rubric rộng; chưa xác nhận cùng uniform input distribution và request budget như RQ. |
| O | 1 | 32 | 9 | TD-0002 đo mutation score; chưa tương đương đầy đủ số unique kills theo dạng yêu cầu/oracle của RQ. |

**Phân bố điểm:** 35 paper đạt 0/4, 6 paper đạt 1/4, 1 paper đạt 2/4; không paper nào đạt ≥3/4 trong tập 42.

**Quy ước:** ✓ là đạt rubric đối chiếu hiện có, không bảo đảm khớp đầy đủ RQ. Rubric I chấp nhận EP và/hoặc BVA; C chấp nhận cùng số test/lời gọi/thời gian; O chấp nhận mutation score. Các khác biệt này phải được giữ rõ khi kết luận tính mới.

Nguồn cá nhân đã được đối chiếu: [Lâm](../lam/SLR/rq-check.md), [Khôi](../khoi/SLR/rq-check.md), [Tùng](../tung/SLR/rq-check.md), [T.Duy](../t.duy/SLR/rq-check.md), [K.Duy](../k.duy/SLR/rq-check.md). Phạm vi và sai lệch chuyển nội dung được lưu trong [bảng đối chiếu 42 dòng](rq-validation-source-check.csv); không thay cho tái screening toàn bộ IC/EC. Nguồn bổ sung không tự cộng vào N/PRISMA. Quy trình L1–L3 do thiếu số lượng không áp dụng vì N≥12.

## 3. Phản chứng tổng hợp mọi nguồn

### 3.1. Nhãn tính mới và kết luận phản chứng

**Nhãn nhóm: `extension`**, đã được GV bổ sung theo xác nhận của người phụ trách ngày 20/10/2026. Các nhãn cá nhân phản ánh phạm vi và thời điểm đối chiếu riêng.

- Trong tập 42, **TD-0002 đạt cao nhất 2/4**. Paper có EP/BVA và mutation score nhưng không có đối chứng random như RQ. TD-0015 có generator EP+BVA bằng Python nhưng không đo mutant.
- Ngoài tập 42, **Guo 2024 đạt 3/4 theo rubric rộng**; những khác biệt phương pháp được trình bày tại §3.3.
- Trong phạm vi đã đối chiếu, chưa xác minh được paper khớp đủ 4/4 điều kiện RQ. Kết luận này giới hạn trong tài liệu đã tìm, không khẳng định tính mới tuyệt đối.

RQ kế thừa benchmark/oracle RESTestBench và bổ sung phép so EP+BVA–uniform random. Nhãn `extension` đã được xác nhận; phần biện minh đóng góp vẫn cần phân biệt với điểm PICO rộng và bằng chứng gap ở §5.

### 3.2. Rà 2–3 nghiên cứu mạnh trong 12 tháng gần nhất

**Cửa sổ:** 20/10/2025–20/10/2026; ưu tiên cùng bài toán/metric, rồi venue/quy mô, sau đó độ mới. Kế thừa lượt rà 18/10, kiểm lại nguồn ngày 20/10. Truy vấn, ngày tìm và lý do chọn/loại: [nhật ký tìm kiếm](rq-validation-audit.md#3-tìm-kiếm-bổ-sung-ngày-20102026).

| Paper và lý do chọn | P/I/C/O theo rubric | Hạn chế trực tiếp; phần RQ chưa được đánh giá |
|---|---|---|
| **RESTestBench**, EASE 2026, arXiv v1 28/04/2026; đúng benchmark và metric nền. [PDF](../tung/SLR/update-paper/R2R-01-RESTestBench-2026.pdf), §3–4/PDF3–8 | ✓ / · / · / ✓ — **2/4** | §6/PDF9: “Our benchmark includes only three services”; “Each experiment was executed only three times”. Thử LLM single-step/refinement, chưa có phép so EP+BVA–uniform random cùng request budget theo dạng yêu cầu. |
| **MioHint**, ICSE 2026 Research, bản conference 04/2026; thực nghiệm nhiều SUT. [PDF](../tung/SLR/update-paper/R2R-02-MioHint-2026.pdf), §3–5/PDF5–10 | ◐ / · / ◐ / · — **0/4** | §5/PDF10: “fuzzers best at achieving coverage, may not be best at finding bugs”. White-box MIO/LLM sửa request; mutation hit rate không phải source-mutant kill, không thực hiện phép so của RQ. |
| **FDRRestTest/K100**, ESEM 2026, công bố 05/10/2026; sát black-box REST testing, có fixed-request comparison và nhiều baseline. [PDF](../Paper-source/32-K100.pdf), §4–6/PDF8–18 | ◐ / · / ◐ / ◐ — **0/4** | PDF17: “The benchmark excludes enterprise-level APIs”. Đo logical-oracle findings/FRE, không phải unique source mutants; không cô lập phép so EP+BVA–uniform random. Riêng equal-request budget đã có nghiên cứu thực hiện. |

K100 đã nằm trong tập 42, không tính thêm một paper. LlamaRestTest (06/2025) nằm ngoài cửa sổ, chỉ dùng làm nền; MioHint được xét theo bản conference, phân biệt với preprint đầu 04/2025. Req2REST-Guard chưa xác minh được P vì tên dịch vụ không khớp benchmark; MASTOR có mutation score/killed counts nhưng nghiên cứu sinh oracle. Các nguồn này không chứng minh phép so input của RQ đã được thực hiện; chi tiết ở nhật ký đối chiếu.

### 3.3. Paper gần nhất và bảng căn hàng

**Paper gần nhất theo rubric rộng trong phạm vi đã đối chiếu:** Guo, Okamura & Dohi (2024), *Optimal test case generation for boundary value analysis*, [DOI 10.1007/s11219-023-09659-9](https://link.springer.com/article/10.1007/s11219-023-09659-9), **3/4 (I/C/O)**. Guo là nguồn phương pháp ngoài cửa sổ rà mới; RESTestBench là nguồn benchmark/oracle được kế thừa.

| Yếu tố | Paper gần nhất: Guo 2024 | RQ nhóm | Khác ở đâu, căn cứ (bằng chứng gap / lý do đổi theo) |
|---|---|---|---|
| P | 5 chương trình non-REST (§5.4) | 45 yêu cầu RESTestBench | Chuyển sang kiểm thử REST theo yêu cầu; chưa giải quyết hạn chế đa dạng dịch vụ. |
| I | Tối ưu BCD, lấy biên từ phân tích mã (§5.4–5.5) | EP+BVA từ yêu cầu/schema, không AI | Khác cách xây lớp/biên. Chưa có limitation tác giả nêu đúng GAP-T của nhóm. |
| C | Random theo phân hoạch, cùng cỡ test (§5.2/5.5) | Uniform random trên miền xác định, cùng request budget | Chưa đồng nhất baseline; miền và B của nhóm chưa chốt. |
| O | Kill rate theo khác biệt đường thực thi (§5.1) | Unique kills theo pass bản gốc/fail mutant và dạng yêu cầu | Oracle và cách tổng hợp khác; chưa thể ghi “=” hoặc coi chỉ đổi P. |

**Điểm cần làm rõ:** 3/4 theo rubric rộng không chứng minh chỉ khác một yếu tố đầy đủ của RQ. Bằng chứng limitation cho GAP-T và lý do những yếu tố còn lại thay đổi chưa đủ để chốt bảng căn hàng theo yêu cầu của cô.

## 4. Khả thi của từng gap đang cân nhắc (Bước 3)

Đánh giá **A — GAP-T + RQ đang đăng ký**. Hướng GAP-M được đặt cạnh A tại §5.3 nhưng chưa có RQ thay thế đủ căn cứ để chấm như một cặp thực nghiệm. Các số kế hoạch bên dưới không phải số đo; chưa có kết luận hai hướng khả thi ngang nhau.

| Tiêu chí | A — GAP-T: số liệu/căn cứ hiện có | Chấm | Việc cần xử lý |
|---|---|---|---|
| Dataset | Public; kế hoạch **45=16+15+14**. README ghi 103, paper ghi 106 yêu cầu; chưa khóa 45 ID/mutant tương ứng. | ⚠️ | Chốt phiên bản, tiêu chí hợp lệ, ID/seed và dạng yêu cầu. |
| API/Tool | Dự kiến **0 lời gọi API LLM trả phí**, **3 dịch vụ cục bộ**; cần Docker, Python và Git. | ⚠️ | Xác nhận môi trường máy nhóm và chạy golden tests trên cả 3 dịch vụ. |
| Tính toán | **900 lượt kỹ thuật–yêu cầu/1 điều kiện**; chưa có số đo RAM/runtime của thiết kế. | ⚠️ | Pilot đo tài nguyên; ưu tiên chạy tuần tự trước khi ước lượng toàn bộ. |
| Ground truth | Có golden tests và mutant/oracle; dự kiến **0 giờ gán nhãn ground truth mới**. | ✅ về nguồn sẵn có | Kiểm oracle, assertions dùng chung và định danh mutant. |
| Code base | **1 framework upstream**, **2 generator cần tích hợp**; chưa có bằng chứng generator nhóm chạy đúng. | ⚠️ | Kiểm sinh input, budget, pass-valid/fail-mutant và chính sách lỗi chạy. |
| Kỹ năng | **5 thành viên**; chưa có log xác nhận tích hợp được hai generator. | ⚠️ | Chốt người phụ trách/giờ công; pilot dự kiến **5 yêu cầu trên đủ 3 dịch vụ**. |
| Thời gian | **45×2×10=900 lượt**; chưa chốt B, runtime và hạn triển khai cụ thể. | ⚠️ | Dự toán từ pilot; bố trí **≥3 ngày dự phòng** hoặc đề xuất downscope. |

**Đếm A: 0 ❌ / 6 ⚠️ / 1 ✅ → rủi ro cao.** Số lượng cảnh báo yêu cầu kế hoạch xử lý trước proposal; chưa đủ căn cứ xác nhận khả thi. Với hướng B, cần chốt RQ/PICO trước khi lập cột khả thi riêng nếu nhóm tiếp tục cân nhắc.

**Kế hoạch xử lý:** khóa dữ liệu và đặc tả generator → kiểm setup/oracle → pilot → dự toán tài nguyên/thời gian. Trước hết xét một điều kiện precise hoặc vague với cùng thông tin cho hai kỹ thuật. Nếu vẫn vượt nguồn lực, trình phương án giảm mẫu/số lượt hoặc thu hẹp dạng yêu cầu cho GV, kèm hệ quả phương pháp; đây chưa phải thay đổi được áp dụng.

900 là số lượt kỹ thuật–yêu cầu cho một điều kiện, không phải số HTTP executions. Replay trên mutant, setup/reset/retry phải được tính riêng. Nguồn artifact: [README benchmark](https://github.com/casablancahotelsoftware/RESTestBench#setup), [evaluator](https://github.com/casablancahotelsoftware/RESTestBench/blob/master/src/evaluator.py).

## 5. Gap mà RQ lấp (kết quả Bước 2)

### 5.1. Gap RQ ban đầu và kết quả đối chiếu

**Loại: GAP-T.** Nguyên văn từ [context gap ban đầu](gap-ban-dau.txt):

> Chưa có nghiên cứu nào so sánh trực tiếp EP+BVA với sinh dữ liệu ngẫu nhiên đồng đều dưới cùng ngân sách request trong kiểm thử REST API dựa trên yêu cầu.

**Ghi nhận bổ sung ngày 20/10/2026, sau tổng hợp paper**, không phải bản ghi đã có trước khi đếm. Giữ nguyên câu giả thuyết; không dùng câu này như kết luận tuyệt đối trong proposal.

**Đối chiếu theo bốn trường hợp của cô:** hiện chưa xác nhận dòng limitation tác giả nào khớp đầy đủ câu trên → **“chưa có paper nêu, là giả định của nhóm”**. Không tự xếp thành gap yếu/mạnh theo số bài không có I✓. Trình tự ghi trước khi đếm chưa được đáp ứng và không thể sửa hồi tố.

### 5.2. Bảng hạn chế, kiểm đã giải quyết và độ mạnh

Mẫu số **N_L=42** là số paper có dữ liệu ở cột hạn chế của bảng gộp. Tử số chỉ tính phát biểu trực tiếp đã kiểm; paper có tác giả trùng được gộp theo [sổ quote và quy tắc đếm](rq-validation-audit.md#4-sổ-bằng-chứng-gap-d-và-quy-tắc-đếm). Số đếm là mức tối thiểu đã xác minh.

| Hạn chế | Paper nêu | Paper đã giải quyết | Còn lại | Mạnh/yếu | Loại |
|---|---|---|---|---|---|
| Thiếu phép so EP+BVA–uniform random cùng request budget trong kiểm thử REST theo yêu cầu | Chưa xác nhận phát biểu trực tiếp tương ứng; đây là giả thuyết ban đầu | Chưa xác minh paper làm đúng phép so; Guo khác bài toán/oracle, TD-0002/TD-0015 thiếu C/O tương ứng | 0 phát biểu được xác nhận/42 | Chưa có dòng khớp; giả định của nhóm | GAP-T |
| Giới hạn số lượng/phạm vi dịch vụ làm hạn chế khái quát | Tối thiểu **18/42 paper, 10 cụm**: K46/K76/K166; P12/P17/K32/K167/K168/K191; K66/K101; K37; K89; K93; TD-0015; K02; TD-0002; K100 | K191 giảm nhẹ hạn chế bằng thực nghiệm công nghiệp nhưng vẫn một tổ chức. Đổi tool/metric không đủ để gạch hạn chế của paper khác | Chủ đề hạn chế còn ở ≥10 cụm | Lặp lại mạnh theo đếm; chưa mặc nhiên là một gap cụ thể thống nhất | GAP-D |
| Chưa đánh giá bằng mutation trong phép so 10 công cụ của P12 | **P12/K81/K55**, §6/PDF11: “using mutation to further evaluate the tools’ fault-detection ability” | RESTestBench đánh giá LLM, chưa chứng minh đánh giá lại đúng tập công cụ P12 với metric đó | **1/42 paper, 1 cụm** đã xác minh | Yếu | GAP-M |
| ~~Chưa có đánh giá mutation cấp hệ thống cho REST API nói chung~~ | Khái quát hóa của người tổng hợp; không phải limitation chung đã được xác nhận | RESTestBench có requirements-based mutation; TD-0002 có mutation score | Không giữ phát biểu khái quát | Bị phản chứng; không tính thành gap mạnh | GAP-M |

K49 (§4.5.1/PDF17) bàn thiếu mutation tool cấp system tại thời điểm bài viết; không cộng với P12 như hai tác giả nêu cùng một hạn chế. Tương tự, số yêu cầu hoặc số người tham gia không được dùng thay số dịch vụ khi đếm GAP-D.

**Phát biểu GAP-D ở mức bằng chứng hiện có:** trong 42 paper có dữ liệu hạn chế, tối thiểu 18 paper thuộc 10 cụm tác giả nêu giới hạn khái quát do số lượng/phạm vi dịch vụ thực nghiệm; tên, quote và vị trí có trong sổ bằng chứng. Chưa đủ căn cứ kết luận các nghiên cứu khác đã giải quyết đầy đủ hạn chế của từng phương pháp với cùng bài toán/metric. Đây là chủ đề hạn chế lặp lại; cần cụ thể hóa P nếu phát triển thành RQ khác. RQ hiện tại vẫn chỉ có 3 dịch vụ nên không nhận là đã lấp GAP-D.

### 5.3. Đối chiếu gap và RQ theo mẫu

| Gap | Phát biểu gap | RQ lấp gap | Khác RQ ban đầu |
|---|---|---|---|
| **A — GAP-T**, giả định ban đầu | Trong 42 paper và các nguồn bổ sung đã đối chiếu, nhóm chưa xác minh được phép so EP+BVA–uniform random cùng request budget cho REST API dựa trên yêu cầu. Chưa xác nhận limitation tác giả tương ứng; đây là giả định trong phạm vi đã tìm. | **RQ hiện tại (§1):** trên 45 yêu cầu RESTestBench, EP+BVA khác uniform random cùng budget thế nào về số mutant riêng biệt theo dạng yêu cầu, với điều kiện pass bản gốc/fail mutant theo oracle benchmark? | **Không đổi RQ**; phân bổ mẫu P đã điều chỉnh thành 16–15–14 và cần xác nhận với GV. |
| **B — GAP-M**, bằng chứng hiện tại còn yếu | Trong 42 paper, P12/K81/K55 nêu chưa dùng mutation để đánh giá tiếp khả năng phát hiện lỗi của các công cụ trong nghiên cứu; chưa xác minh paper khác đánh giá lại đúng phạm vi đó. | **Chưa chốt RQ thay thế đủ căn cứ.** Hạn chế của phép so 10 công cụ P12 chưa chứng minh thiếu O cho phép so EP+BVA–random hiện tại. Cần xác định phạm vi trước khi viết RQ nháp; hướng dẫn không bắt buộc gap yếu có RQ riêng. | **Chưa xác định.** Nếu kế thừa thiết kế P12, P/I/C đều có thể khác RQ hiện tại; chưa thể coi là chỉ đổi O. |

Bảng này thể hiện hai hướng để trao đổi, không xác nhận cả hai là gap mạnh hoặc đã có hai RQ khả thi. Với GAP-D, chưa có phương án mở rộng dịch vụ được đặc tả thành cặp gap–RQ để so chọn.

### 5.4. Vì sao gap còn trống

**GAP-T:** nguyên nhân chưa được xác nhận. RESTestBench mới công bố năm 2026 cung cấp hạ tầng phù hợp, nhưng chưa có bằng chứng đây là lý do thiếu phép so. Lượt dò kết quả âm của T.Duy ngày 18/10 và kiểm có mục tiêu ngày 20/10 chưa thấy kết quả âm trực tiếp trong phạm vi đã tìm; không suy thành chưa ai thử.

**GAP-M của P12:** paper nêu hướng đánh giá tiếp bằng mutation nhưng chưa xác nhận nguyên nhân chưa thực hiện. Nhận định thiếu tool của K49 chỉ là bối cảnh tham khảo. **GAP-D:** một số nguồn nêu chi phí thực nghiệm hệ thống, quota và khả năng triển khai; không suy mọi paper có cùng nguyên nhân.

### 5.5. Lợi ích của cặp GAP-T + RQ hiện tại

Nhóm muốn biết chênh lệch khả năng phát hiện mutant giữa EP+BVA và uniform random dưới cùng budget để giúp kỹ sư kiểm thử lựa chọn cách sinh input theo dạng yêu cầu; hiện chưa có kết quả đối chiếu phù hợp trong phạm vi tài liệu đã kiểm. Nếu EP+BVA có lợi thế thực tiễn thì cân nhắc ưu tiên EP+BVA; nếu random có lợi thế thì cân nhắc random; nếu chưa đủ bằng chứng khác biệt thì báo cáo bất định, không kết luận hai kỹ thuật tương đương. Lợi ích giới hạn trong mẫu, oracle và ngân sách đã đánh giá.

## 6. Quyết định: giữ RQ / đổi I hoặc C

**RQ đang giữ:** RQ tại §1; nhãn **`extension`** đã được GV bổ sung theo xác nhận của người phụ trách. GAP-T hiện là giả định cần tiếp tục biện minh; GAP-M chưa có RQ thay thế đủ căn cứ. Bảng §5.3 là cơ sở trao đổi trước khi chốt lựa chọn cuối cùng, không tự đổi RQ hoặc H0/H1.

**Thay đổi P:** phương án 16–15–14 đã được ghi trong hồ sơ nhóm; **chưa xác nhận ngày báo GV**. Chênh lệch README 103/paper 106 cần được xử lý bằng phiên bản benchmark và kiểm kê mẫu thực tế.

**Trạng thái RBL-2:** Bước 1 đã xác nhận; Bước 2 có bảng đối chiếu/gap/RQ nhưng còn vấn đề căn cứ GAP-T, bảng căn hàng và thời điểm ghi gap; Bước 3 có bảng rà khả thi và kế hoạch xử lý, chưa đủ số liệu để chốt. Không yêu cầu chạy toàn bộ thực nghiệm để hoàn tất RBL-2.

**Việc cần chốt trước triển khai:** xác nhận gap/RQ và điều chỉnh P với GV; khóa dữ liệu, B/miền random, oracle và dạng yêu cầu; xác nhận máy/nhân lực/thời gian, kiểm hai generator và pilot. Kế hoạch phân tích thống kê được hoàn thiện trước chạy chính. Danh sách ngắn các vấn đề cần cô hỗ trợ: [rq-validation-status.md](rq-validation-status.md).
