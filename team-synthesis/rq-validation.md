# Kiểm chứng RQ — FA26-EXT-12 · SaoCungDuoc

**Cập nhật 22/10/2026 (Asia/Saigon):** bản thiết kế để nhóm review theo mail cô Chi. Đã được người dùng cho phép triển khai mục 1–2; chưa phải giảng viên chốt RQ, chưa cho phép bước 3. Không có kết quả golden tests, pilot hoặc đánh giá chính thức.

## 1. RQ + PICO

**RQ chính:** Trong điều kiện sinh single-step với cùng mô hình, cấu hình và ngân sách kiểm thử được quy định trước, việc bổ sung hướng dẫn EP+BVA vào prompt gốc ảnh hưởng như thế nào đến MS_φ trên các yêu cầu vague của RESTestBench tại phiên bản đóng băng?

**RQ phân tích:** Các trường hợp cải thiện hoặc suy giảm MS_φ đi kèm những khác biệt nào về lựa chọn dữ liệu kiểm thử, thiết lập tiền điều kiện và tính đúng của oracle?

RQ phân tích mô tả các đặc điểm đi kèm; không chứng minh một cơ chế chỉ từ tương quan hoặc vài ví dụ. Chi phí và lượng kiểm thử là biến đo bổ sung cho cả hai RQ.

| Thành phần | Thiết kế hiện hành |
|---|---|
| P | 106 requirement vague tại commit RESTestBench `4decc1e36ea3dd41b64ce3e3ac6a85bc72df36ae`: 63 FastAPI, 29 RealWorld, 14 TodoApp. |
| I | Toàn bộ prompt C, bổ sung hướng dẫn EP+BVA có căn cứ và cách xử lý khi thiếu thông tin. |
| C | Prompt single-step gốc của benchmark, nguyên văn; không gọi SUT trong lúc sinh. |
| O | MS_φ chính; khả năng thực thi/pass-valid, lựa chọn dữ liệu, tiền điều kiện, oracle, request/assertion, token và chi phí là kết quả bổ sung. |
| Điều kiện | Model người dùng chọn: **DeepSeek-V4.1-Flash-1017**, **DeepSeek API chính thức**, trần tổng chi phí gọi model **3 USD**, gồm pilot và retry. Cấu hình chi tiết ở [thiết kế thực nghiệm](experiment-design.md). |

**H0 định hướng:** chênh lệch kỳ vọng MS_φ giữa hai cấu hình prompt bằng 0 trong điều kiện đã quy định. **H1:** khác 0. Không chọn kiểm định sau khi nhìn điểm; số lần sinh và cách diễn giải bất định phải được duyệt trước đánh giá chính.

Mỗi requirement/arm/run sinh một test; cùng đầu vào vague + toàn bộ OAS + base URL, cùng cấu hình và chính sách thực thi. Một hàm pytest có thể chứa nhiều request, nên số hàm không thay thế việc đo/giới hạn ngân sách thực dùng.

<a id="11-định-nghĩa-outcome-và-tổng-hợp-ba-run"></a>

### 1.1. Outcome và đơn vị phân tích

Với requirement i có m_i mutant, k[a,r,i] là số mutant được test tương ứng pass-valid/fail-mutant phát hiện. Test fail trên bản gốc có k = 0. Kết quả chính giữ mẫu số manifest; lỗi sinh hoặc thiếu output không được âm thầm làm mất requirement.

- `MS_φ(a,r) = Σ_i k[a,r,i] / 228`.
- Theo dịch vụ chia 141 FastAPI / 65 RealWorld / 22 TodoApp.
- Với R lần sinh được chốt: `mean_MS_φ(a) = Σ_r Σ_i k[a,r,i] / (R × 228)`; `Δ = mean_MS_φ(I) − mean_MS_φ(C)`; nhân 100 để báo điểm phần trăm.
- Trung bình không phải union kill, không phải trung bình không trọng số của 106 tỷ lệ. Mutant cùng requirement dùng chung test; các lần sinh là đo lặp trên cùng benchmark.

Validity gate được xác nhận trong [Evaluator.evaluate_test](https://github.com/casablancahotelsoftware/RESTestBench/blob/4decc1e36ea3dd41b64ce3e3ac6a85bc72df36ae/src/evaluator.py). Hàm aggregate chỉ thấy requirement có score, nên bước 3/pilot phải kiểm tra đối soát manifest khi mất output/kết quả; chưa tái hiện lỗi bằng thực thi.

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
| Model/provider/budget | Người dùng chọn DeepSeek-V4.1-Flash-1017 / API chính thức / tối đa 3 USD | Đã có quyết định; chưa gọi API |
| Prompt, ngân sách, manifest | Hồ sơ review ở [experiment-design](experiment-design.md) và [experiments](../experiments/) | Cần nhóm review; không phải freeze đánh giá chính |
| Môi trường | Chưa có log Docker/golden tests, phiên bản máy chạy hoặc reset/mutant validation | Thuộc bước 3, chưa triển khai |
| Pilot và chi phí thật | Chưa có output/usage thực tế; dự toán không phải hóa đơn hoặc kết quả pilot | Chưa triển khai |
| Nhân lực/deadline | Có vai trò trong [authorship](authorship.md); chưa có cam kết giờ công, deadline cụ thể và tên hai người chấm oracle | Cần nhóm chốt trước khi chạy |

**Đủ thông tin để hoàn thiện tài liệu và soạn thiết kế review cho mục 1–2. Chưa đủ để xác nhận thực nghiệm khả thi trên máy nhóm hoặc chốt đánh giá chính.** Không tự điền API key, kết quả pilot, runtime hay sự đồng ý của cô.

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
| 3 · Môi trường/golden tests | Log xác minh ba service, reset, mutant và evaluator | Chưa làm; chỉ tiếp tục sau khi người dùng review |
| 4 · Pilot | Xác minh pipeline, đo usage/chi phí/runtime; kiểm mất output và mẫu số | Chưa làm |
| 5 · Gửi cô | Bảng nghiên cứu gần nhất + commit/thống kê + hai prompt + ngân sách + pilot evaluator | Chưa đủ hồ sơ, chưa gửi |
| 6 · Đánh giá chính | Prompt/config đã freeze, đánh giá, phân tích và gói tái lập | Chưa được triển khai |

**Ghi chú lịch sử:** con số 15 mutant từ trao đổi GV trước đây chưa có danh sách ID và phân loại độc lập; không dùng làm trần tăng điểm hoặc căn cứ power. Kế hoạch 45 requirement/random/10 run đã được thay thế, không phải thiết kế hiện hành.
