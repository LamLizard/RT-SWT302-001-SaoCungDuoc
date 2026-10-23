# Kiểm chứng RQ — FA26-EXT-12 · SaoCungDuoc

**Amendment trạng thái 23/10/2026 (Asia/Saigon):** RQ/phương pháp dưới đây giữ nguyên bản review ngày 22/10; chưa được giảng viên chốt. Đã có golden và pilot thực; [pilot đối soát offline](../.local/pilot-preparation/pilot-reconciliation-20261023-01/report.json) có 24/24 evaluation resolved, C 19/25 (76%), I 18/25 (72%). [Hồ sơ review/provenance](../.local/pilot-preparation/pilot-reconciliation-20261023-01/HO-SO-GUI-GIANG-VIEN.md) công bố một amendment original-quality-failure, không đổi prompt/benchmark/generated test. Main chưa chạy/chưa freeze; không suy tác động từ một pilot run.

## 1. RQ + PICO

**RQ chính:** Trong điều kiện sinh single-step với cùng mô hình, cấu hình và ngân sách kiểm thử được quy định trước, việc bổ sung hướng dẫn EP+BVA vào prompt gốc ảnh hưởng như thế nào đến MS_φ trên các yêu cầu vague của RESTestBench tại phiên bản đóng băng?

**Mục tiêu phân tích bổ trợ (không phải RQ riêng):** mô tả những khác biệt về lựa chọn dữ liệu kiểm thử, thiết lập tiền điều kiện và tính đúng của oracle đi kèm các trường hợp MS_φ cải thiện, suy giảm hoặc không đổi, nhằm hỗ trợ diễn giải kết quả của RQ chính.

**Nguồn gốc và điều chỉnh:** tại mục 5 của [mail cô Chi](../lam/SLR/AI%20cua%20lam%20response.txt), cô gợi ý có thể bổ sung câu hỏi phân tích các trường hợp cải thiện/suy giảm. Bản cập nhật trước đã tách gợi ý này thành “RQ phân tích”; lượt rà 22/10/2026 giữ nội dung hữu ích dưới dạng mục tiêu/kế hoạch phân tích, chỉ giữ một RQ chính. Các đặc điểm đi kèm là liên hệ quan sát, không chứng minh cơ chế nhân quả chỉ từ tương quan hoặc vài ví dụ.

| Thành phần | Thiết kế hiện hành |
|---|---|
| P | 106 requirement vague tại commit RESTestBench `4decc1e36ea3dd41b64ce3e3ac6a85bc72df36ae`: 63 FastAPI, 29 RealWorld, 14 TodoApp. |
| I | Toàn bộ prompt C, bổ sung hướng dẫn EP+BVA có căn cứ và cách xử lý khi thiếu thông tin. |
| C | Prompt single-step gốc của benchmark, nguyên văn; không gọi SUT trong lúc sinh. |
| O | MS_φ. |

**Điều kiện kiểm soát, tách khỏi PICO:** hai nhánh dùng cùng mô hình, cấu hình và ngân sách kiểm thử được quy định trước. Model người dùng chọn là **DeepSeek-V4.1-Flash-1017** qua **DeepSeek API chính thức**; trần tổng chi phí model là **3 USD**, gồm pilot, main và retry. Cấu hình chi tiết ở [thiết kế thực nghiệm](experiment-design.md); đây vẫn là bản review, chưa freeze đánh giá chính.

**Chỉ số phân tích bổ trợ:** khả năng thực thi/pass-valid, lựa chọn dữ liệu, tiền điều kiện, oracle, request/assertion, token và chi phí hỗ trợ trả lời RQ chính; không tạo thêm RQ hoặc thay outcome chính MS_φ.

**Đại lượng giả thuyết:** trên panel vague cố định tại commit trên, gọi `μ_a = E[MS_φ(a,r)]` với `a ∈ {C, I}` là MS_φ kỳ vọng qua các lần sinh ngẫu nhiên dưới điều kiện so sánh đã quy định. Đặt `Δ = μ_I − μ_C`; `100 × Δ` là chênh lệch tính bằng điểm phần trăm. Đây là kỳ vọng trên panel cố định, không phải kỳ vọng cho mọi REST API/LLM.

- **H0: Δ = 0.** Trong điều kiện sinh single-step với cùng mô hình, cấu hình và ngân sách kiểm thử được quy định trước, MS_φ kỳ vọng của prompt gốc bổ sung hướng dẫn EP+BVA có căn cứ bằng MS_φ kỳ vọng của prompt single-step gốc trên cùng các yêu cầu vague của RESTestBench tại phiên bản đóng băng.
- **H1: Δ ≠ 0.** Trong cùng điều kiện sinh single-step, mô hình, cấu hình và ngân sách kiểm thử được quy định trước, MS_φ kỳ vọng của hai prompt khác nhau trên cùng các yêu cầu vague của RESTestBench tại phiên bản đóng băng; khác biệt có thể dương hoặc âm.

**Làm rõ trước/sau:** cách viết trước “chênh lệch kỳ vọng MS_φ bằng 0” / “khác 0” đã mang nghĩa H0: Δ = 0 và H1: Δ ≠ 0. Đây vẫn là hai giả thuyết bổ sung nhau: loại trừ nhau và bao quát hai khả năng của Δ. Cách viết rút gọn, nhất là H1 chỉ ghi “khác 0”, làm thiếu rõ đại lượng và điều kiện so sánh; lượt này viết đầy đủ, không đổi bản chất giả thuyết.

Định hướng kiểm định là **hai phía**, phù hợp RQ “ảnh hưởng như thế nào”, không mặc định EP+BVA tốt hơn. Phép kiểm định cụ thể, số lần sinh và cách diễn giải bất định phải được duyệt trước đánh giá chính; bản thiết kế R=3 hiện chưa chốt kiểm định p-value confirmatory. Không bác bỏ H0 hoặc không có ý nghĩa thống kê không xác nhận Δ = 0, không chứng minh hai prompt bằng nhau hoặc tương đương.

Mỗi requirement/arm/run sinh một test; cùng đầu vào vague + toàn bộ OAS + base URL, cùng cấu hình và chính sách thực thi. Một hàm pytest có thể chứa nhiều request, nên số hàm không thay thế việc đo/giới hạn ngân sách thực dùng.

<a id="11-định-nghĩa-outcome-và-tổng-hợp-ba-run"></a>

### 1.1. Outcome và đơn vị phân tích

Với requirement i có m_i mutant, k[a,r,i] là số mutant được test tương ứng pass-valid/fail-mutant phát hiện. Test fail trên bản gốc có k = 0. Kết quả chính giữ mẫu số manifest; lỗi sinh hoặc thiếu output không được âm thầm làm mất requirement.

- `MS_φ(a,r) = Σ_i k[a,r,i] / 228`.
- Theo dịch vụ chia 141 FastAPI / 65 RealWorld / 22 TodoApp.
- Với R lần sinh được chốt: `mean_MS_φ(a) = Σ_r Σ_i k[a,r,i] / (R × 228)`; chênh lệch quan sát `Δ_r = MS_φ(I,r) − MS_φ(C,r)` và `Δ_hat = mean_MS_φ(I) − mean_MS_φ(C) = Σ_r Δ_r / R`. `Δ_hat` ước lượng chênh lệch kỳ vọng Δ; nhân 100 để báo điểm phần trăm.
- Trung bình không phải union kill, không phải trung bình không trọng số của 106 tỷ lệ. Mutant cùng requirement dùng chung test; các lần sinh là đo lặp trên cùng benchmark.

Validity gate được xác định tại [Evaluator.evaluate_test](https://github.com/casablancahotelsoftware/RESTestBench/blob/4decc1e36ea3dd41b64ce3e3ac6a85bc72df36ae/src/evaluator.py). Aggregate được đối soát theo manifest/slot ID vì hàm benchmark chỉ thấy requirement có score. Đã có bằng chứng golden/pilot và regression offline; một mutant compile lỗi chưa được runtime-validated. Smoke/preflight trước amendment không xác minh mã mới; cần revalidation trước live run tương lai.

<a id="22-đối-chiếu-pico-cho-rq-hiện-hành"></a>

## 2. Bằng chứng và nghiên cứu gần nhất

**Bộ evidence: 60 nguồn = 42 INCLUDE lịch sử + 18 nguồn nền bổ sung.** Bài 60 là GV-18/Rodríguez; chưa nhập vào phễu screening cũ. Không đổi PRISMA final 42 hoặc CSV lịch sử. Điểm P/I/C/O của 59 bài cũ được giữ để truy vết, không đổi thành điểm hiện hành.

| Nghiên cứu | Đầu vào / phép so thực sự | Đã cung cấp gì? | Điều chưa trả lời trực tiếp cho RQ này | Locator |
|---|---|---|---|---|
| GV-02 · RESTestBench (2026) | NL precise/vague + OAS; single-step so với refinement | Benchmark và MS_φ; đánh giá ảnh hưởng độ chi tiết và tương tác SUT | Không có phép so C với C + hướng dẫn EP+BVA | [PDF 44](../Paper-source/44-GV-02-RESTestBench.pdf), §3.2–4.2/PDF4–8; §5–6/PDF9 |
| **GV-18 · Rodríguez et al. (2025)** | Đặc tả + mã Java; GPT-4-0613 có hướng dẫn EP+BVA so với test thủ công; 10 scenario | EP+BVA trong prompt đã tồn tại; 30 lớp test LLM/10 lớp thủ công; đánh giá PIT, coverage và định tính | Không có đối chứng LLM bỏ hướng dẫn EP+BVA; không thực nghiệm vague REST API/MS_φ | [PDF 60](../Paper-source/60-Martin%20Rodriguez.pdf), §3/PDF4–8; Tables1–2/PDF9–10; §5–6/PDF10–13; [arXiv](https://arxiv.org/abs/2505.09830) |
| TD-0002 · RestTSLLM (2025) | OpenAPI → TSL → integration tests; so các LLM trên 6 dự án .NET | Có equivalence/boundary trong hướng dẫn; đo mutation bằng Stryker.NET | Không phải baseline single-step của RESTestBench; mutation score không tự là MS_φ | [PDF 39](../Paper-source/39-TD-0002.pdf), §3/PDF3–4; §4.3–4.6/PDF6–8; Table3/PDF8 |
| GV-03 · Prompt-Based REST API Test Amplification in Industry (2026) | Test có sẵn + ngữ cảnh; amplification cho 6 endpoint công nghiệp | Bằng chứng replication công nghiệp, coverage và công sửa test | Không so hai prompt trên vague RESTestBench; coverage không thay MS_φ | [PDF 45](../Paper-source/45-GV-03-Prompt-Based-REST-API-Amplification.pdf), §4–5/PDF3–6; §7/PDF7 |
| GV-04 · RESTOR (2026) | Một request–response quan sát được; oracle generation với GRPO | Đánh giá chất lượng oracle trong REST API | Không phải sinh test single-step chỉ từ vague + OAS, không đối chứng EP+BVA/MS_φ | [PDF 46](../Paper-source/46-GV-04-RESTOR.pdf), §3–5; §7/PDF18–19 |

Ba bài 2026 GV-02/GV-03/GV-04 được chọn để đối chiếu nghiên cứu trong 12 tháng gần nhất theo mức liên quan bài toán/metric; không tuyên bố chúng là ba bài mạnh nhất toàn lĩnh vực. GV-18 là nguồn cô yêu cầu; TD-0002 gần về can thiệp, cả hai nằm ngoài cửa sổ 12 tháng tại 22/10/2026. Tra cứu web bổ sung có ghi truy vấn, nguồn và giới hạn tại [search-log §11](../lam/SLR/search-log.md). Không phải một lượt systematic screening mới của ACM/IEEE/OpenAlex.

<a id="31-paper-gần-nhất-và-bảng-căn-hàng"></a>

## 3. Đóng góp dự kiến và nhãn

**Định vị đề xuất: extension của phép sinh single-step trên RESTestBench.** Kế thừa P ở điều kiện vague, baseline và outcome; bổ sung phép so prompt có kiểm soát cùng phân tích test. Đây là định vị cần nhóm/cô review, không phải xác nhận chốt đề tài.

Ba đầu ra dự kiến:

1. So sánh C/I dưới cùng điều kiện và ngân sách đã quy định.
2. Phân tích có tiêu chí và kiểm tra độc lập về lựa chọn dữ liệu, tiền điều kiện, oracle và giả định thiếu căn cứ trong cả trường hợp tăng, giảm, không đổi điểm.
3. Gói tái lập gồm phiên bản nguồn, manifest, prompt/hash, cấu hình, lịch chạy, output thô, kết quả và quy trình phân tích.

Không tuyên bố phát minh EP/BVA hoặc thêm EP/BVA vào prompt. Không bác bỏ replication chỉ vì kỹ thuật đã được so sánh. Kết quả dương, âm hoặc chưa phân biệt được đều có thể hữu ích nếu báo đúng phạm vi và độ bất định.

<a id="4-khả-thi-của-gap-đang-cân-nhắc"></a>

## 4. Khả thi và điều kiện còn thiếu

| Hạng mục | Bằng chứng thực tế | Trạng thái |
|---|---|---|
| Dữ liệu tĩnh | Đã đọc 106 JSON, 228 mutant; vague không rỗng; đúng 63/29/14 và 141/65/22 tại commit trên. README cùng commit ghi 26 RealWorld, khác dữ liệu 29. | Đã kiểm tĩnh; không đồng nghĩa chạy được |
| Model/provider/budget | DeepSeek-V4.1-Flash-1017 / API chính thức / tối đa 3 USD; pilot 24 attempt | Có usage thật; alias/giá phải kiểm lại trước main |
| Prompt, ngân sách, manifest | Hồ sơ review ở [experiment-design](experiment-design.md) và [experiments](../experiments/) | Cần nhóm review; không phải freeze đánh giá chính |
| Môi trường | Golden 106 original pass, 227 assertion kill, 1 compile lỗi, 106 restored pass | Bước 1 hoàn thành với lỗi NestJS 5/0; giữ mẫu số 228, không chặn bước 2; không nhận mọi mutant runtime-valid |
| Pilot và chi phí | 24/24 resolved qua đối soát; ledger bound USD0.0655344, ước tính usage USD0.022192608 | Pilot đã đóng, hóa đơn chưa xác nhận; chưa suy biến động từ một run |
| Nhân lực/deadline | Có vai trò trong [authorship](authorship.md); chưa có cam kết giờ công, deadline cụ thể và tên hai người chấm oracle | Cần nhóm chốt trước khi chạy |

**Có hồ sơ và bằng chứng để gửi review có công bố giới hạn. Chưa đủ để chốt đánh giá chính:** thiếu người chấm/annotation, căn cứ R và độ bất định, xác nhận cô, freeze và revalidation mã mới. Không tự điền quyết định hoặc kết quả chưa có bằng chứng.

<a id="5-gap-mà-rq-lấp-kết-quả-bước-2"></a>

<a id="5-gap-mà-rq-lấp"></a>

## 5. Vì sao câu hỏi bổ sung đáng kiểm tra?

### 5.1. Bằng chứng, suy luận và điều chưa biết

- **Đã kiểm chứng:** GV-18 dùng EP+BVA trong prompt; nghiên cứu unit test có mã nguồn và đối chứng con người. GV-02 cung cấp bối cảnh vague và MS_φ nhưng không thử I của nhóm.
- **Suy luận nghiên cứu:** trong đầu vào thiếu chi tiết, hướng dẫn có thể giúp chọn đại diện/biên có căn cứ và tránh bỏ sót; cũng có thể dẫn đến thêm điều kiện/oracle thiếu căn cứ hoặc bỏ qua BVA vì không có miền rõ. Đây là các khả năng cạnh tranh, chưa phải kết quả.
- **Chưa biết:** chiều/độ lớn tác động, độ biến động, tỷ lệ lỗi oracle, mức dùng ngân sách và tỷ lệ requirement có cơ hội EP/BVA thực sự. Chưa tái thẩm định toàn bộ 59 nguồn theo rubric mới; không khẳng định chưa ai làm trên toàn lĩnh vực.

### 5.2. Phát biểu gap có giới hạn

> Các nghiên cứu gần nhất được đối chiếu chưa trả lời trực tiếp việc bổ sung hướng dẫn EP+BVA có căn cứ vào baseline single-step ảnh hưởng thế nào đến MS_φ và đặc điểm thành công/thất bại khi sinh test từ vague requirement, với đầu vào và ngân sách quy định trước trên RESTestBench đã khóa phiên bản.

Đây là gap do nhóm tổng hợp trong phạm vi đã đọc, không phải limitation được cả năm tác giả cùng tuyên bố. Không suy độ mạnh khoa học chỉ từ số dấu P/I/C/O hoặc x/N. Các hạn chế về ít dịch vụ là giới hạn của đề tài, không phải GAP-D mà nhóm tuyên bố đã giải quyết.

Cần kiểm kê cơ hội áp dụng EP/BVA từ vague + OAS bằng quy tắc có trước, không dùng mutant để chọn case thuận lợi. Tài liệu precise/golden/mutant chỉ dùng phía kiểm kê/hậu kiểm, không chuyển vào prompt, ví dụ hoặc quy tắc riêng từng requirement.

## 6. Quyết định và mốc review

Giữ hướng hai prompt và chuẩn bị bộ hồ sơ cho cô; chỉ kết luận tác động của **cấu hình prompt I** trong điều kiện này. Hai arm không tách riêng tác động EP khỏi BVA, hay tác động từng câu chỉ dẫn tránh suy đoán. Phân tích ở vague không chứng minh sự khác biệt so với precise.

| Bước | Đầu ra | Trạng thái |
|---|---|---|
| 1 · Nền tảng tài liệu | RQ, đóng góp, đối chiếu bài 60, protocol bổ sung, đồng bộ tài liệu cá nhân | Bản cập nhật ngày 22/10 để review |
| 2 · Thiết kế thực nghiệm | Manifest, C/I đầy đủ, cấu hình, ngân sách, lịch và kế hoạch phân tích | Xem experiment-design; cần review, chưa freeze đánh giá chính |
| 3 · Môi trường/golden tests | Log ba service, reset/restore và golden | Hoàn thành với một mutant compile lỗi; release không chặn bước 2 |
| 4 · Pilot | 24 output/evaluation resolved; usage và metric từ artifact, một amendment công bố | Đã đóng offline; cần smoke/preflight mã mới trước live run tiếp theo |
| 5 · Gửi cô | Bảng nghiên cứu + commit/thống kê + prompt + ngân sách + pilot | Hồ sơ sẵn sàng để người dùng review/gửi; chưa gửi, chưa có xác nhận cô |
| 6 · Đánh giá chính | Prompt/config đã freeze, đánh giá, phân tích và gói tái lập | Chưa được triển khai |

**Ghi chú lịch sử:** con số 15 mutant từ trao đổi GV trước đây chưa có danh sách ID và phân loại độc lập; không dùng làm trần tăng điểm hoặc căn cứ power. Kế hoạch 45 requirement/random/10 run đã được thay thế, không phải thiết kế hiện hành.
