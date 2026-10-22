# Báo cáo thay đổi mục 1 và mục 2 — hồ sơ để Leader kiểm chứng

**Cập nhật:** 22/10/2026 · Asia/Saigon
**Nhánh:** `Lam`
**Mốc so sánh:** HEAD `80a246d274eda79992173cf458b5d84538613e39` — `[RBL-2] Draft sync research docs and clarify PICO, MS_phi, and evidence`
**Phạm vi:** hoàn thiện nền tảng tài liệu (mục 1), sau đó soạn thiết kế thực nghiệm (mục 2). Dừng trước mục 3 để người dùng/Leader review.

Tên file vẫn là `TEMP_RESEARCH_SYNC_REVIEW_2026-10-21.md` theo yêu cầu, nhưng nội dung đã được **ghi đè bằng báo cáo ngày 22/10**. Báo cáo này thay thế bản tạm ngày 21/10; các locator/số dòng và tuyên bố “7 file” của bản cũ không còn là mô tả của đợt hiện tại.

## 1. Trạng thái cần hiểu trước khi review

**Đã có bản tài liệu và artifact thiết kế để review. Chưa có kết quả thực nghiệm và chưa đủ căn cứ xác nhận toàn bộ thí nghiệm chạy được trong 3 USD.**

- Mục 1: cập nhật RQ, đóng góp, đối chiếu Rodríguez, protocol bổ sung và phần hiện hành của hồ sơ cá nhân.
- Mục 2: tạo hai prompt, manifest dữ liệu, cấu hình, lịch dự kiến và quy tắc đo/phân tích/chi phí.
- Trước khi ghi đè báo cáo này có **16 file được Git theo dõi đã thay đổi** và **6 artifact thiết kế mới**. Báo cáo là một file hiện hữu được sửa thêm trong lượt bàn giao này.
- Model, provider và trần tiền do người dùng cung cấp: **DeepSeek-V4.1-Flash-1017 / DeepSeek API chính thức / tối đa 3 USD**. Những tham số khác là đề xuất thiết kế, còn cần review.
- Chưa dựng service, chạy golden tests, pilot, gọi DeepSeek hoặc đánh giá chính. Chưa viết runner/instrumentation/bộ chặn chi phí thực thi. Chưa stage, commit, push hoặc gửi hồ sơ cho giảng viên.
- `execution_permitted=false`, `main_runs_finalized=false`, lịch/prompt chưa final-freeze cho đánh giá chính. Đây là trạng thái review có chủ đích.
- Đợt triển khai mục 1–2 dùng một skill: **experimental-design v1.5**; nguồn phương pháp được ghi cuối [thiết kế thực nghiệm](team-synthesis/experiment-design.md). Skill không thay thế phê duyệt của Leader, kiểm tra độc lập hoặc bằng chứng chạy thật.

**Hai tài liệu nên đọc trước:**

1. [RQ, gap, đóng góp và nghiên cứu gần nhất](team-synthesis/rq-validation.md).
2. [Thiết kế thực nghiệm và các điều kiện còn thiếu](team-synthesis/experiment-design.md).

## 2. Đối chiếu với mail cô Chi

| Yêu cầu trong mail | Nội dung đã chuẩn bị | Trạng thái thực tế |
|---|---|---|
| Chứng minh câu hỏi bổ sung, không dựa vào tổ hợp PICO chưa xuất hiện | Viết lại lập luận gap, các khả năng cạnh tranh và phạm vi đóng góp | Đã sửa tài liệu; chưa chứng minh bao phủ toàn bộ literature |
| Đối chiếu Rodríguez et al. (2025) | Thêm GV-18/PDF60 vào bảng nguồn, map, audit và bảng nghiên cứu gần nhất | Đã đọc phần liên quan; chưa tái lập artifact của bài |
| Đóng băng commit, thống kê dữ liệu thực tế | Manifest định danh commit, requirement, native mutant index và source/OAS blob hashes | Đã có kiểm kê tĩnh; chưa xác minh runtime/môi trường |
| Hai prompt đầy đủ, không thêm thông tin ngầm | C gốc, I giữ C và nối hướng dẫn EP+BVA có căn cứ | Đã có file; chưa gọi model kiểm tra adherence |
| Ngân sách kiểm thử và công bằng hai nhánh | Quy định lượt sinh, retry, token, timeout, cap request và đo mức dùng thật | Mới là đặc tả; chưa có runner/bộ đếm/bộ chặn được kiểm chứng |
| Pilot xác minh evaluator | Thiết kế mẫu pilot, lịch và tiêu chí đối soát mất output/mẫu số | Chưa chạy; chưa có kết quả pilot để nộp |
| Freeze trước đánh giá chính, tái lập và phân tích thất bại | Có quy trình, hash artifact, codebook và các điều kiện freeze | Chưa final-freeze, chấm độc lập hoặc tạo gói kết quả tái lập |

Phần “gửi cô trước khi chốt” vẫn chưa hoàn tất: đã chuẩn bị bản đối chiếu, manifest, prompt và ngân sách; **còn thiếu kết quả pilot xác minh evaluator** và việc duyệt thiết kế. Không xem bản cập nhật này là cô đã chốt RQ.

## 3. Mục 1 — thay đổi nền tảng tài liệu

| Hạng mục | Trước cập nhật tại HEAD | Sau cập nhật | Leader kiểm chứng ở đâu? |
|---|---|---|---|
| RQ chính | So hai prompt trên 106 vague, nêu cùng model/temperature | Theo câu cô đề xuất: cùng model, cấu hình và ngân sách quy định trước trên phiên bản đóng băng | [rq-validation §1](team-synthesis/rq-validation.md#1-rq--pico) |
| RQ phân tích | Chưa có câu hỏi phân tích được tách rõ | Bổ sung khác biệt về lựa chọn dữ liệu, tiền điều kiện và oracle đi kèm tăng/giảm MS_φ; không mặc định là cơ chế nhân quả | [rq-validation §1](team-synthesis/rq-validation.md#1-rq--pico) |
| H0/H1 và outcome | Phát biểu khác biệt MS_φ; công thức gắn ba run | Phát biểu chênh lệch kỳ vọng; công thức tổng hợp theo R đã chốt, giữ trọng số mutant và validity gate | [rq-validation §1.1](team-synthesis/rq-validation.md#11-outcome-và-đơn-vị-phân-tích) |
| Đóng góp/gap | Trọng tâm là phép so EP+BVA chưa được ghi nhận trên đúng benchmark | Nêu điều cần biết, lợi ích và hai khả năng giúp/hại; đóng góp là so sánh có kiểm soát, phân tích test và gói tái lập | [rq-validation §3–5](team-synthesis/rq-validation.md#3-đóng-góp-dự-kiến-và-nhãn) |
| Bài 60 | Có PDF local, chưa tích hợp vào bộ evidence | Mã GV-18; thêm đúng một nguồn nền; phân biệt unit Java/specification + implementation/human comparator/PIT với phép so của nhóm | [bảng đối chiếu](team-synthesis/rq-validation.md#2-bằng-chứng-và-nghiên-cứu-gần-nhất), [audit nguồn](lam/SLR/teacher-papers-audit.md) |
| Quy mô evidence | 59 = 42 INCLUDE lịch sử + 17 nguồn nền | 60 = 42 INCLUDE lịch sử + 18 nguồn nền; PRISMA final vẫn 42 | [merge](team-synthesis/evidence-table-merged.md), [map](team-synthesis/rq-evidence-map.md), [PRISMA](team-synthesis/prisma-team.md) |
| Điểm PICO cũ | Giữ điểm nền, còn bất nhất rubric | Giữ nguyên 59 dòng cũ; GV-18 được đối chiếu nội dung, không gán lại điểm nền hoặc tính vào tổng dấu cũ | [map](team-synthesis/rq-evidence-map.md) |
| Protocol tìm tài liệu | Query/IC-EC chủ yếu kế thừa hướng EP+BVA truyền thống so random | Thêm tuyến REST trực tiếp và nền phương pháp; đề xuất A1–A3 phù hợp LLM/prompt; bảo toàn hồ sơ screening cũ | [review-protocol §8](team-synthesis/review-protocol.md#8-protocol-bổ-sung-cho-rq-prompt--phiên-bản-review-22102026), [IC/EC bổ sung](team-synthesis/ie_criteria.md) |
| Tra cứu mới | Không có lượt bổ sung được ghi cho RQ mới trong đợt đồng bộ trước | Ghi bốn query web có hướng và nguồn sử dụng; không đổi chúng thành số hit hoặc screening CSDL | [search-log §11](lam/SLR/search-log.md) |
| Hồ sơ cá nhân | Cả năm rq-check còn mô tả RQ cũ, thường là 45 requirement/random | Thêm phần hiện hành; đánh dấu phần cũ là lịch sử. Không tái chấm hoặc viết lại nội dung đối chiếu cũ | Năm file trong danh mục §8 dưới đây |
| Trạng thái và số liệu khả thi | Nhiều lựa chọn còn mở; ba run được nêu rộng như kế hoạch | Ghi quyết định người dùng, R=3 là dự kiến cần review, đủ thông tin để soạn thiết kế nhưng chưa đủ xác nhận chạy được | [README](README.md), [notes](notes.md), [rq-validation §4](team-synthesis/rq-validation.md#4-khả-thi-và-điều-kiện-còn-thiếu) |

### 3.1. Bằng chứng mới và giới hạn kết luận

- GV-18/Rodríguez có hướng dẫn EP+BVA trong prompt nhưng so LLM với test thủ công, đầu vào gồm đặc tả và mã Java; không có ablation LLM bỏ hướng dẫn EP+BVA. Vì vậy, không tuyên bố thêm EP+BVA vào prompt là phát minh mới, cũng không coi bài này đã trả lời RQ của nhóm.
- Bảng nghiên cứu gần nhất gồm **GV-02, GV-18, TD-0002, GV-03, GV-04**, với locator phương pháp/metric/hạn chế trong từng PDF. Ba nguồn 2026 được chọn theo mức liên quan; không tuyên bố là ba bài mạnh nhất toàn lĩnh vực.
- Chưa systematic search/screening mới theo A1–A3, chưa đọc/tái thẩm định toàn bộ 59 nguồn theo RQ mới, chưa audit lại toàn bộ quote/cổng P1–P5 hoặc có người chấm độc lập.
- Một số candidate tìm thấy ngoài năm nguồn đối chiếu chưa được đọc toàn văn; đã ghi giới hạn trong search-log, chưa cộng vào corpus hoặc dùng để khẳng định gap.
- Nhãn `extension` là định vị đề xuất để review. Replication không bị loại chỉ vì kỹ thuật đã được so sánh trước đây.

## 4. Mục 2 — artifact mới và ý nghĩa

| Artifact mới | Đã tạo gì? | Chưa chứng minh điều gì? |
|---|---|---|
| [experiment-design.md](team-synthesis/experiment-design.md) | Thiết kế ghép cặp; model; ngân sách; lỗi; lịch; đo lường; phân tích; codebook; các điều kiện freeze | Chưa phải kết quả hoặc protocol được Leader/cô duyệt |
| [benchmark-manifest.json](experiments/benchmark-manifest.json) | 106 requirement, 228 vị trí mutant; commit và Git blob hashes của requirement/OAS/source | Chưa chứng minh service, mutant, golden hoặc evaluator chạy đúng |
| [C.txt](experiments/prompts/C.txt) | Literal prompt baseline đã trích từ source pinned | Chưa kiểm API thực sự render/gửi đúng input |
| [I.txt](experiments/prompts/I.txt) | Toàn bộ nội dung C, nối sáu chỉ dẫn EP+BVA/không suy đoán; giữ ba placeholder | Chưa có bằng chứng model tuân thủ hoặc sinh test tốt hơn |
| [study-config.json](experiments/study-config.json) | Cấu hình review, điều kiện/budget, hash, reviewer gate và mẫu qualitative dự kiến | JSON không tự chạy hay cưỡng chế trần chi phí |
| [run-schedule.csv](experiments/run-schedule.csv) | 660 slot kế hoạch, ghép C/I, xáo thứ tự có thể kiểm lại | Không phải 660 request đã gọi hoặc execution log |

### 4.1. Dữ liệu và định danh

Benchmark commit: `4decc1e36ea3dd41b64ce3e3ac6a85bc72df36ae`.

| Dịch vụ | Requirement | Mutant |
|---|---:|---:|
| FastAPI | 63 | 141 |
| RealWorld | 29 | 65 |
| TodoApp | 14 | 22 |
| **Tổng** | **106** | **228** |

Lượt kiểm kê nguồn trước đó trong cùng chat đã đọc 106 JSON tại commit này, xác nhận vague không rỗng và tổng mutant. **Lượt lập báo cáo này chỉ đối soát lại manifest/artifact local; không tải lại 106 JSON hoặc chạy service.** Leader có thể kiểm lại từng `path` và `git_blob_sha1` ở manifest với nguồn tại commit khóa.

Native mutant locator là **index 0-based trong mảng `mutants`**. Khóa `service/requirement_id/mutant_index` do nghiên cứu ghép để truy vết, không phải trường ID native có sẵn. README benchmark ở cùng commit ghi 26 RealWorld, trong dữ liệu là 29; manifest dùng dữ liệu 29, không lấy tổng README 103 làm mẫu số.

### 4.2. Phân biệt quyết định người dùng và đề xuất còn chờ duyệt

| Hạng mục | Giá trị trong bản review | Nguồn quyết định/trạng thái |
|---|---|---|
| Model | DeepSeek-V4.1-Flash-1017 | Người dùng cung cấp |
| Provider | DeepSeek API chính thức | Người dùng xác nhận |
| Tổng chi phí | Tối đa 3 USD, kể cả pilot/main/retry | Trần người dùng; phạm vi chi phí được đặc tả để review |
| API ID | `deepseek-flash` | Mapping tài liệu DeepSeek đã đối chiếu; alias có thể đổi, chưa xác minh qua request thật |
| Thinking/temperature/top_p | disabled / 0.2 / 1.0 | Đề xuất của bản thiết kế, chưa được Leader duyệt |
| Output cap/API timeout | 2.048 token / 360 giây mỗi attempt | Đề xuất, chưa có số đo adherence/truncation/runtime |
| Retry | SDK retry=0; tối đa một transport retry/slot, không semantic repair hoặc chọn output tốt nhất | Đặc tả, chưa có runner thực thi |
| Ngân sách execution | Đề xuất 64 HTTP request tính setup/cleanup; timeout 60 giây/context | Chưa có instrumentation được kiểm chứng; không đồng nghĩa cùng số request thực dùng |
| Main | R=3, 106 × 2 × 3 = 636 slot | Kế hoạch nguồn lực, `main_runs_finalized=false`; không phải power analysis |
| Pilot | 12 requirement, bốn/service, C/I một run = 24 slot | Mẫu/lịch đề xuất, chưa chạy; không dùng tune prompt trên panel 106 |
| Qualitative | 12 requirement, hai arm, ba run = 72 output nếu đủ; hai người chấm độc lập | Danh sách mẫu có trong config; chưa có output, nhãn, agreement hoặc tên reviewer |
| Phân tích | Effect/Δ từng run, mean/SD/range; interval t chỉ tham khảo có giả định; bootstrap requirement là sensitivity về case mix | Cần Leader/người phụ trách thống kê review; chưa chạy phân tích kết quả |

Thông tin model/provider/budget đủ để soạn cấu hình review. Thông tin về máy chạy, dependency/tokenizer, API parameter support thực tế, thời hạn, giờ công và reviewer vẫn chưa được xác nhận.

### 4.3. Chi phí: dự toán có điều kiện

Dùng bảng giá đã ghi nguồn ngày 22/10 trong thiết kế: off-peak cache-miss input **0,15 USD/1M token**, output **0,60 USD/1M token**. Không giả định được cache hit hoặc miễn phí.

Giả định mỗi slot có **16.000 input token + 2.048 output token**:

- Một slot: `(16.000 × 0,15 + 2.048 × 0,60) / 1.000.000 = 0,0036288 USD`.
- Pilot 24 slot: **0,0870912 USD**.
- Main 636 slot: **2,3079168 USD**.
- Tổng 660 slot: **2,395008 USD trước retry**; cùng giả định ở giá peak là **4,790016 USD**, vượt trần.
- Phân bổ kế hoạch: **0,15 pilot + 2,45 main + 0,40 dự phòng = 3 USD**. Không phải tiền đã chi.

**16.000 là envelope dự toán, chưa phải token count thật.** Số ký tự OAS không phải số token. Cần preflight tokenizer/accounting và pilot trước khi cam kết toàn bộ lịch phù hợp 3 USD. File config chỉ đặt yêu cầu reserve cả cặp/attempt, giữ phí chưa rõ, kiểm giá và dừng khi vượt trần; bộ chặn này **chưa được lập trình hoặc thử nghiệm**.

### 4.4. Kiểm soát hợp lệ và giới hạn khoa học

- Hai nhánh nhận cùng vague/OAS/base URL, cấu hình, chính sách budget và preprocessing code-fence gốc. Precise/golden/mutant/điểm không được đưa vào prompt.
- I có cả hướng dẫn chọn dữ liệu, tránh suy đoán và comment khi thiếu căn cứ. Hiệu quả đo được là hiệu quả **cấu hình prompt I**; không tách riêng EP, BVA, từng câu chỉ dẫn hoặc số đầu vào được tạo.
- Giữ MS_φ pass-valid/fail-mutant và mẫu số manifest. Không biến lỗi hạ tầng, timeout hoặc cap do instrumentation thành mutant kill chưa được xác minh.
- Chưa có bảo đảm power cho R=3; interval t chỉ có nghĩa dưới giả định được nêu. Bootstrap composition không thay thế biến động sinh của model hoặc chứng minh khái quát cho mọi dịch vụ. Không suy tương đương chỉ từ việc chưa phân biệt được.
- `deepseek-flash` là alias, không phải cam kết endpoint snapshot bất biến. Việc khóa weights/checkpoint thực tế và metadata model vẫn cần xác minh.

## 5. Kiểm tra đã thực hiện — kết quả và phạm vi

Các kiểm tra sau được đối soát local khi lập báo cáo; không phải chạy benchmark:

| Kiểm tra | Kết quả quan sát | Giới hạn |
|---|---|---|
| Git baseline | Nhánh Lam, HEAD đúng mốc ghi đầu báo cáo | Không fetch/push hoặc xác nhận remote mới nhất |
| Corpus | Merge và phần ma trận có đúng 60 ID; 59 dòng nghiên cứu cũ giữ nguyên so HEAD | Không tái thẩm định nội dung khoa học toàn bộ 59 |
| Hồ sơ cá nhân | Phần hiện hành được bổ sung; nội dung đối chiếu cũ được giữ dưới nhãn lịch sử | Không phải năm thành viên đã chấm lại RQ mới |
| Manifest | 106 khóa service/requirement duy nhất, tổng 228; indices khớp m_i; đúng 63/29/14 và 141/65/22 | Không xác minh runtime hoặc nghĩa của mutant bằng kiểm tra local này |
| Lịch | 660 slot = 24 pilot + 636 main; 330 cặp liền nhau, mỗi cặp đủ C/I | Đây là lịch dự kiến |
| Ba main run | Mỗi run có đủ 106 requirement × 2 arm; 53 cặp C-trước, 53 cặp I-trước | Không phải ba lần sinh đã hoàn thành |
| Prompt | C khớp literal source pinned sau chuẩn hóa newline; I có C làm tiền tố; mỗi prompt có đúng ba placeholder | Chưa xác minh request render hoặc output API |
| SHA256 artifact | Bốn hash tham chiếu trong config khớp file hiện tại | Hash đảm bảo định danh byte, không đảm bảo phương pháp đúng |
| Phép tính ngân sách | Tính lại đúng 2,395008 USD theo giả định ở §4.3 | Không phải charge thực tế hoặc chứng minh token ≤16k |
| Liên kết/định dạng | Đã kiểm đích file local và whitespace | Không mặc định đã kiểm mọi anchor/URL bên ngoài |

**Làm rõ phát biểu “C khớp từng byte” ở trao đổi trước:** phép so nội dung prompt dùng văn bản sau chuẩn hóa CRLF → LF. File C hiện có 19 newline CRLF; SHA256 file thô khác SHA256 literal LF. Nội dung C sau chuẩn hóa khớp source, nhưng không nên mô tả file CRLF là giống byte thô với literal LF. Hai loại hash được ghi riêng ở bảng dưới. Việc render thực tế phải ghi nhận newline policy và request/input hash.

### 5.1. SHA256 của artifact tại thời điểm báo cáo

| Artifact | SHA256 byte thô |
|---|---|
| [C.txt](experiments/prompts/C.txt) | `af717c86e54149aef250e98fa471b0c7942144d3011e9e83786399962c1c9275` |
| [I.txt](experiments/prompts/I.txt) | `43abf1588e21b5e5c026182eeabf5f479cca57d3ff915751333c8929da49cce2` |
| [benchmark-manifest.json](experiments/benchmark-manifest.json) | `77d43970252f1d668a3ad73f6d948f3da60aad3fbff2a5c135e330eb266f59f6` |
| [run-schedule.csv](experiments/run-schedule.csv) | `77af2025d9919f5a217661ec43d01f05d1f474a2f4605ea7e255356530bb5d01` |
| [study-config.json](experiments/study-config.json) | `307e70a8df4ec098a38a1c28a052ce4895f6e3962c8493a613342ff8d738df07` |

C sau chuẩn hóa LF, UTF-8: `0e4545b94ccd257bceaa7d8644cd49cc9c6e0f412024a1cd45556838a175280d`. Đây không thay cho hash file thô trong config. Nếu thay newline hoặc nội dung artifact thì cần cập nhật hash trước final-freeze.

PDF60 do người dùng cung cấp có SHA256 `f5ac7e8b3a1222276a32bdae6f8594fe313e7c8486616346ef1c9651a7700ed2`; báo cáo này không sửa PDF.

## 6. Phần chưa làm và bằng chứng còn thiếu

| Phần còn thiếu | Cần có để xác nhận hoàn thành | Ảnh hưởng hiện tại |
|---|---|---|
| Leader review mục 1–2 | Nhận xét/chấp thuận hoặc yêu cầu sửa cụ thể | Chưa chuyển sang mục 3 |
| Rà literature có hệ thống cho RQ mới | Lượt A1–A3 có log CSDL, screening, kiểm độc lập; cập nhật số liệu khi thực sự có | Chưa chứng minh bao phủ literature hoặc gap mạnh |
| Chốt phương pháp | Duyệt intervention/budget, R, pilot, qualitative sample và kế hoạch bất định | Các default không tự trở thành quyết định nhóm |
| Môi trường bước 3 | OS/Python/Docker, image digest/dependency lock, ba service khởi động, reset/patch đúng | Chưa xác nhận benchmark chạy được trên máy nhóm |
| Golden/evaluator | Golden trên original/mutant; kiểm mất output, mẫu số, cap/timeout và phân loại lỗi | Chưa có kết quả pilot xác minh evaluator để nộp cô |
| Runner và log | Sinh/chạy đúng C/I; lưu raw/cleaned output, attempt/usage/result theo khóa; không retry ngầm | CSV/config hiện tại không thực thi thí nghiệm |
| Bộ chặn 3 USD | Cận trên token/cost tin cậy, pair reservation, unknown charges, giá/alias check và hard stop | Trần tiền mới là yêu cầu thiết kế |
| Token/model thật | Token count, parameter acceptance, finish_reason, alias/response metadata và chi phí | Không khẳng định 660 slot vừa 3 USD hoặc checkpoint đã khóa bất biến |
| Pilot bước 4 | Chạy mẫu đã duyệt, usage/runtime/lỗi/biến động; không tune trên điểm panel | R=3/envelope/cap chưa có bằng chứng pilot |
| Đánh giá độc lập | Hai reviewer, giờ công, codebook thử, nhãn độc lập và hòa giải bất đồng | Chưa có tỷ lệ oracle đúng/sai/unsupported hoặc IAA |
| Freeze/main | Hash cuối sau duyệt/pilot, amendment log, đánh giá đủ manifest | Chưa có MS_φ, Δ, CI/p-value hoặc kết luận hiệu quả |
| Hồ sơ gửi cô/tái lập | Năm đầu ra cô yêu cầu và sau đó gói code/môi trường/log/kết quả | Chưa gửi cô, chưa xác nhận thẻ đăng ký hoặc GV chốt RQ |

Các con số “15 mutant” từ trao đổi GV cũ chưa có danh sách ID và phân loại độc lập, không dùng làm trần tăng điểm hoặc căn cứ power. Không có kết quả nào được điền thay bằng dữ liệu giả.

## 7. Những điểm Leader nên quyết định

- [ ] RQ chính và câu hỏi phân tích có bám đúng mail, đóng góp đã đủ rõ trong phạm vi nguồn hiện có chưa?
- [ ] Giữ lớp nền GV-18 và cách báo 60 evidence / 42 INCLUDE lịch sử; có yêu cầu rà systematic search thêm trước khi gửi cô không?
- [ ] Chấp nhận so sánh toàn bộ cấu hình prompt I, gồm hướng dẫn tránh suy đoán, và giới hạn suy luận tương ứng?
- [ ] Duyệt hoặc sửa thinking disabled, temperature 0.2, cap output 2048, request cap64, timeout60/360 và retry policy?
- [ ] R=3 và pilot12 có phù hợp mục tiêu/nguồn lực, cần độ chính xác hoặc kế hoạch suy luận khác không?
- [ ] Phương án reserve/đối soát chi phí và model alias có đủ điều kiện để triển khai bộ chạy ở bước sau?
- [ ] Chỉ định hai người chấm độc lập, deadline và giờ công; duyệt cách chọn/chấm mẫu qualitative?
- [ ] Sau review, phần nào cần sửa lại và có cho chuyển sang **mục 3: môi trường/golden tests** hay chưa?

Các ô trên là nội dung chờ quyết định, không phải kết quả duyệt được báo cáo thay Leader.

## 8. Danh mục file để kiểm chứng diff

### 8.1. Mười sáu file hiện hữu đã thay đổi ở mục 1–2

| File | Mục đích thay đổi |
|---|---|
| [README.md](README.md) | Điểm vào review, RQ/model/budget, phạm vi thực hiện |
| [notes.md](notes.md) | Quyết định hiện hành, điều kiện còn mở, giữ lịch sử |
| [rq-validation.md](team-synthesis/rq-validation.md) | RQ/PICO, contribution, nghiên cứu gần nhất, gap, khả thi và mốc review |
| [review-protocol.md](team-synthesis/review-protocol.md) | Protocol bổ sung §8, phân biệt screening cũ và tra cứu mới |
| [ie_criteria.md](team-synthesis/ie_criteria.md) | Phân tuyến REST trực tiếp/nền phương pháp; giữ IC/EC lịch sử |
| [evidence-table-merged.md](team-synthesis/evidence-table-merged.md) | Thêm GV-18, cập nhật 60 nguồn, giữ 59 dòng cũ |
| [rq-evidence-map.md](team-synthesis/rq-evidence-map.md) | Đối chiếu hiện hành, GV-18 chưa gán điểm nền |
| [prisma-team.md](team-synthesis/prisma-team.md) | Banner đối soát 60/18; không sửa phễu final42 |
| [Lâm — evidence-table.md](lam/SLR/evidence-table.md) | Bổ sung nguồn GV-18 và số lượng hiện hành |
| [Lâm — teacher-papers-audit.md](lam/SLR/teacher-papers-audit.md) | Metadata/PDF hash/locator và giới hạn nguồn60 |
| [Lâm — search-log.md](lam/SLR/search-log.md) | Thêm §11–12, nguồn/tra cứu/thay đổi/kiểm tra và phần chưa làm |
| [Lâm — rq-check.md](lam/SLR/rq-check.md) | Hiện hành + giữ hồ sơ cũ có nhãn lịch sử |
| [Khôi — rq-check.md](khoi/SLR/rq-check.md) | Hiện hành + giữ hồ sơ cũ có nhãn lịch sử |
| [Tùng — rq-check.md](tung/SLR/rq-check.md) | Hiện hành + giữ hồ sơ cũ có nhãn lịch sử |
| [T.Duy — rq-check.md](t.duy/SLR/rq-check.md) | Hiện hành + giữ hồ sơ cũ có nhãn lịch sử |
| [K.Duy — rq-check.md](k.duy/SLR/rq-check.md) | Hiện hành + giữ hồ sơ cũ có nhãn lịch sử |

### 8.2. Sáu artifact mới của mục 2

Danh mục tại §4 gồm `team-synthesis/experiment-design.md` và năm file trong `experiments/`. Chúng đang **untracked**, chưa được đưa vào commit. Git diff thông thường của file tracked không hiện đầy đủ nội dung sáu file này; cần mở trực tiếp để review.

Hai đầu vào do người dùng đã cung cấp là [PDF60](Paper-source/60-Martin%20Rodriguez.pdf) và [file chat/mail](lam/SLR/AI%20cua%20lam%20response.txt), cũng đang untracked; không được tạo hoặc sửa trong lượt viết báo cáo này. Không tự đưa file chat/mail vào commit.

Báo cáo này là file thứ 17 được thay đổi so HEAD sau khi ghi đè; không phải một paper hoặc artifact thực nghiệm mới.

## 9. Cách kiểm tra nhanh bằng lệnh chỉ đọc

Chạy từ thư mục gốc repository:

```powershell
git status --short
git diff --name-status 80a246d274eda79992173cf458b5d84538613e39
git diff 80a246d274eda79992173cf458b5d84538613e39 -- team-synthesis/rq-validation.md team-synthesis/review-protocol.md team-synthesis/rq-evidence-map.md
Get-Content -LiteralPath "team-synthesis/experiment-design.md" -Raw
Get-Content -LiteralPath "experiments/study-config.json" -Raw
Get-FileHash -Algorithm SHA256 -LiteralPath "experiments/prompts/C.txt","experiments/prompts/I.txt","experiments/benchmark-manifest.json","experiments/run-schedule.csv","experiments/study-config.json"
git diff --check
```

Các lệnh trên không chạy model hoặc service. Kiểm hash theo byte thô như §5.1; riêng việc so C với source literal cần thống nhất newline policy. Không coi diff/JSON/hash hợp lệ là bằng chứng thí nghiệm có hiệu quả.

## 10. Phạm vi của lượt ghi đè báo cáo

Lượt này chỉ sửa `TEMP_RESEARCH_SYNC_REVIEW_2026-10-21.md`, đối soát các artifact có sẵn và ghi rõ giới hạn. Không chỉnh lại các tài liệu/config/prompt để làm khớp báo cáo, không cài package, không chạy thực nghiệm hoặc tự chuyển sang mục 3. Chưa stage/commit/push. Nội dung là hồ sơ bàn giao cho Leader kiểm tra, không thay cho quyết định của nhóm hoặc giảng viên.
