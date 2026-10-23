# Thiết kế thực nghiệm để review — mục 2 · FA26-EXT-12

**Thiết kế ngày 22/10/2026; amendment trạng thái 23/10/2026, Asia/Saigon.** RQ/phương pháp/ngân sách giữ nguyên, chưa freeze main. Đã có golden và pilot thực; [đối soát offline có công bố](../.local/pilot-preparation/pilot-reconciliation-20261023-01/provenance.json) đóng 24/24 evaluation, C 19/25 (76%), I 18/25 (72%), không điều chỉnh prompt theo điểm. [Hồ sơ review](../.local/pilot-preparation/pilot-reconciliation-20261023-01/HO-SO-GUI-GIANG-VIEN.md). `study-config.json` giữ nguyên baseline review, không sửa thành giấy phép main; trạng thái thực thi mới nhất đọc ở report/provenance. Chưa được cô chốt, main chưa chạy/chưa được phép trong lượt đóng pilot.

## 1. Câu hỏi, đơn vị và điều kiện

Một RQ chính và mục tiêu phân tích bổ trợ theo [rq-validation §1](rq-validation.md#1-rq--pico); phân tích input, tiền điều kiện và oracle hỗ trợ diễn giải kết quả, không đặt thành RQ thứ hai. Thiết kế ghép cặp: mỗi requirement nhận cả C và I trong từng lần sinh; mutant nằm trong requirement, các run là đo lặp. Không coi 228 mutant hoặc 684 mutant-run/arm là mẫu độc lập.

- Đối tượng đích trực tiếp là **106 vague requirement/228 mutant tại commit đã chọn**. Ước lượng tác động trung bình của cấu hình prompt trên tập cố định này, qua các lần sinh có ngẫu nhiên; không suy cho mọi REST API/LLM.
- Cùng vague, toàn bộ OAS, base URL, system-message policy, model, thinking mode, temperature, max output, timeout và quy tắc retry. Không cắt OAS để làm vừa tiền hoặc đưa oracle từ precise vào prompt.
- Kế thừa evaluator/định nghĩa pass-valid/fail-mutant; không sửa công thức để tăng điểm. Mọi instrumentation ngân sách phải được xác minh không làm thay đổi hành vi test hợp lệ.
- Cả hai nhánh có cùng ngân sách được cấp; vẫn đo lượng thực dùng. Số request/assertion khác nhau là đặc điểm của toàn bộ cấu hình prompt. Hai arm này không tách riêng hiệu quả EP, BVA, chỉ dẫn tránh suy đoán hoặc số lượng đầu vào.

## 2. Artifact và provenance

| Artifact | Nội dung |
|---|---|
| [benchmark-manifest.json](../experiments/benchmark-manifest.json) | Repository/commit, 106 requirement và Git blob SHA1, 228 chỉ số mutant, OAS/source blob hashes, số lượng theo service |
| [C.txt](../experiments/prompts/C.txt) | `DEFAULT_PROMPT_TEMPLATE` nguyên văn từ `tools/single_step_tool/single_step_tool.py` tại commit khóa |
| [I.txt](../experiments/prompts/I.txt) | Toàn bộ C làm tiền tố, chỉ nối sáu chỉ dẫn EP+BVA có căn cứ; không thêm ví dụ hoặc đổi output format |
| [study-config.json](../experiments/study-config.json) | Model/API, điều kiện chung, ngân sách, số run dự kiến, các gate và SHA256 artifact |
| [run-schedule.csv](../experiments/run-schedule.csv) | Lịch baseline giữ nguyên: 24 slot pilot đã thực hiện; 636 slot main còn dự kiến, R chưa chốt |

Commit benchmark: `4decc1e36ea3dd41b64ce3e3ac6a85bc72df36ae`. Đã kiểm tĩnh: FastAPI 63/141, RealWorld 29/65, TodoApp 14/22; vague không rỗng ở cả 106 file. Native mutant locator là vị trí **0-based trong `mutants`** của từng JSON; `service/requirement_id/mutant_index` là khóa ghép của nghiên cứu, không phải trường ID do tác giả đặt.

OAS tương ứng `services/<service>/spec.json`: 38.478 / 36.766 / 8.962 ký tự theo nội dung đã đọc, **không phải token count**. Bằng chứng môi trường/dependency/image/tokenizer đã có trong `.local/environment-verification/`, `.local/pilot-preparation/LIVE-VERIFICATION.md` và `CHECKPOINT.md`; đó là lịch sử nguồn trước amendment. Main cần khóa phiên bản và revalidation mã mới, không nhận smoke/preflight cũ là xác minh mới.

## 3. Prompt và ngăn rò rỉ

C có hướng dẫn assertion strict gốc. I giữ toàn bộ C, thêm: phân hoạch có căn cứ; BVA chỉ khi có miền có thứ tự và ranh giới được hỗ trợ; không tự đặt ngưỡng/quy tắc/oracle; bỏ BVA ở chiều chưa đặc tả; tiền điều kiện/assertion bám đầu vào; suy luận nội bộ và chỉ trả mã Python. Comment ngắn về thiếu căn cứ được I cho phép, nên đây cũng là một phần của gói chỉ dẫn được đánh giá.

Ba placeholder duy nhất: `{scenario_description}`, `{spec_content}`, `{service_base_url}`. Chỉ nạp `requirement_vague` khi render. JSON đầy đủ, precise, golden, mã mutant và điểm đánh giá thuộc phía kiểm kê/hậu kiểm; không đi vào prompt, ví dụ, preprocessing theo requirement hoặc lượt sửa test. Không dùng source code SUT trong đầu vào.

Cả hai arm dùng đúng bước `_clean_code_fences` của tool gốc; giữ raw response và code sau bước này, không sửa lỗi bằng preprocessing mới. Một lượt sinh tạo một hàm pytest tự chứa; không bổ sung test thủ công, không chọn response tốt nhất, không cho một arm vòng feedback. Output nhiều hàm test, rỗng, sai cú pháp hoặc bị cắt được lưu nguyên vẹn và gắn nhãn theo quy tắc chung; không xin sinh lại để cứu điểm.

## 4. Model và cấu hình chung

| Trường | Giá trị đề xuất cho review |
|---|---|
| Provider / base URL | DeepSeek chính thức / `https://api.deepseek.com` |
| Endpoint / API model ID | `/chat/completions` / `deepseek-flash` |
| Phiên bản mong đợi | `DeepSeek-V4.1-Flash-1017` theo mapping chính thức ngày 22/10 |
| Thinking | `{"type":"disabled"}`; explicit để tránh default thinking và chi phí khác |
| Temperature / top_p | 0.2 / 1.0; không truyền sampling seed chưa được provider xác nhận |
| Max output | 2.048 token/response, như nhau cho C/I; output bị cắt là thất bại được ghi nhận |
| Context/system/tools | Context mới cho mỗi slot; một user message; không custom system prompt, tool, search, SUT feedback hoặc multimodal |
| API timeout / concurrency | 360 giây/attempt; một request model tại một thời điểm |
| SDK retry | 0; bộ điều phối kiểm soát retry minh bạch, không cộng thêm retry ngầm |

Nguồn: [DeepSeek changelog](https://api-docs.deepseek.com/updates/), [API parameters](https://api-docs.deepseek.com/api/create-chat-completion/). Tài liệu API nói temperature không tác động trong thinking mode; lựa chọn disabled làm cấu hình temperature có nghĩa.

**Giới hạn phiên bản:** `deepseek-flash` là alias do provider cập nhật, không phải endpoint snapshot bất biến. Ghi request model ID, response model, fingerprint nếu có, timestamp UTC, mapping/release và bảng giá kiểm trước/sau mỗi batch. Nếu mapping thay đổi hoặc không xác nhận được, dừng; không trộn checkpoint. Không tuyên bố đã khóa weights chỉ nhờ tên model người dùng chọn. Pilot có 24 response lưu metadata/usage, response ghi alias `deepseek-flash`; model mapping và giá phải xác minh lại trước live run tương lai, không tra lại trong lượt đối soát offline.

## 5. Ngân sách kiểm thử và lỗi

| Đơn vị | Quy định chung |
|---|---|
| Lượt sinh | Một response có nội dung cho mỗi requirement/arm/run; không semantic repair, không best-of |
| Test | Một test function; ghi số trường hợp đầu vào thực tế, vòng lặp, HTTP request và assertion |
| HTTP request trong một execution | Đề xuất cap 64, tính cả setup/cleanup; áp dụng ngoài prompt cho cả hai arm, phải xác minh instrumentation ở pilot |
| Thực thi test | 60 giây/context gốc hoặc mutant, cùng reset ban đầu của benchmark |
| Token đầu vào | Toàn bộ prompt/OAS; 16.000 là **envelope dự toán**, cần tokenizer/accounting xác minh. Không cắt input hoặc bỏ requirement nếu vượt dự toán |
| Assertions | Ghi lượng thực dùng; không khẳng định hai arm có cùng số assertion chỉ vì cùng cap |

Quy tắc trước khi chạy:

1. Empty/truncated/invalid generated code hoặc output không đúng một test: lưu output, không sửa bằng tay/LLM; báo thất bại. Khi test fail bản gốc do chất lượng output, toàn bộ mutant của requirement vẫn ở mẫu số và k=0.
2. Chỉ retry tối đa một lần/slot khi có lỗi transport/rate-limit retryable rõ ràng và chưa nhận generation dùng được. Giữ mọi attempt, usage và khoản phí chưa biết; SDK không retry ngầm. Empty response/finish_reason=length không là lỗi transport để sinh lại.
3. Service không healthy, reset/patch lỗi hoặc kết quả bị thiếu: lỗi hạ tầng, không kết luận là oracle sai hoặc mutant được phát hiện. Giữ slot pending, không xóa khỏi manifest; sửa lỗi có log và chạy lại block theo cùng chính sách trong ngân sách.
4. Không đưa lỗi do instrumentation cap hoặc lỗi hạ tầng vào evaluator như một mutant kill. Nếu cap/timeout không phân biệt được với assertion failure hợp lệ thì đánh dấu chưa xác minh và dừng kết luận benchmark đầy đủ cho đến khi đối soát. Không giả tạo pass/fail để làm đầy dữ liệu. Pilot phải chứng minh đường xử lý này trước khi freeze main.
5. Kết quả chính chỉ công bố như full benchmark khi manifest và kết quả đối soát đủ. Một study dừng vì tiền/hạ tầng được báo incomplete, không đổi mẫu số, N hoặc R sau khi xem điểm.

## 6. Trần tiền 3 USD và dự toán

Trần áp dụng tổng chi phí DeepSeek của pilot, main và retry; không gọi DeepSeek trong mục 1–2. Không tính credit/cache-hit như khoản giảm giá chắc chắn. Không tự nạp tiền hoặc tăng ngân sách.

Bảng giá chính thức kiểm ngày 22/10/2026, USD/1M token: cache-miss input 0.15 off-peak / 0.30 peak; output 0.60 / 1.20. Dự toán dưới đây giả sử **mọi response chạm cap 2.048 token**, toàn bộ input cache miss. [Bảng giá DeepSeek](https://api-docs.deepseek.com/quick_start/pricing/).

| Input token/call — giả định | 24 slot pilot off-peak | 636 slot main off-peak | Tổng 660 slot off-peak | Tổng peak |
|---|---:|---:|---:|---:|
| 8.000 | 0.0582912 USD | 1.5447168 USD | 1.603008 USD | 3.206016 USD |
| 12.000 | 0.0726912 USD | 1.9263168 USD | 1.999008 USD | 3.998016 USD |
| 16.000 | 0.0870912 USD | 2.3079168 USD | 2.395008 USD | 4.790016 USD |

Phân bổ dự kiến: 0.15 USD pilot + 2.45 USD main + 0.40 USD retry/dự phòng = 3 USD. Không phải các khoản đã chi. Nếu pilot/accounting không hỗ trợ envelope này, dừng và trình phương án sửa trước main; không tự cắt OAS, output budget của một arm, requirement hoặc số run để báo hoàn thành.

Ưu tiên chạy sau 17:15 đến trước 07:30 giờ Việt Nam, tránh peak công bố theo UTC; kiểm lại bảng giá ở ngày chạy. Chỉ bắt đầu một cặp khi còn đủ cửa sổ cho cả hai arm/attempt tối đa và margin. Không dựa hoàn toàn vào lịch để bảo đảm tiền: một call vẫn được reserve theo giá peak.

**Bộ chặn chi phí (đã triển khai trong runner, cần revalidation trước live run mới):** trước khi bắt đầu một cặp phải reserve đủ cho cả hai arm và số transport attempt tối đa; trước từng dispatch phải có cận trên token/cost đã được kiểm chứng, reserve theo peak cache-miss input + peak output, bảo đảm `spent + unknown_reservations + next_reservation <= 3`. Nếu không xác minh được cận trên/giá thì không dispatch. Sau response đối soát usage và phí thật; không giải phóng khoản phí chưa rõ. Concurrency=1. Giá tăng, alias đổi, charge không rõ hoặc không đủ tiền cho cặp tiếp theo đều khiến study dừng với trạng thái incomplete. JSON baseline không tự thực thi các chốt; runner/ledger lưu bằng chứng riêng. Pilot: ledger bound USD0.0655344, ước tính off-peak từ usage USD0.022192608, chưa phải hóa đơn. Các dự toán phía trên giữ nguyên giả định ngày 22/10.

## 7. Lịch, pilot và số lần sinh

**Main dự kiến R=3:** 106 × 2 × 3 = 636 slot; 636 lượt valid và tối đa 1.368 lượt mutant trước skip/reset/retry. Đây là lựa chọn nguồn lực để review, chưa phải power analysis, không chứng minh ba run đủ mạnh hoặc hai prompt tương đương. Không chọn R sau khi nhìn effect hoặc run tốt nhất. Pilot/cost/precision gate có thể buộc sửa thiết kế có ghi nhận trước main; `main_runs_finalized=false` cho tới khi nhóm duyệt.

**Pilot:** 12 requirement, bốn mỗi service, một lần sinh C/I: 24 slot riêng. Chọn theo SHA256 từ service/ID, không dùng mutant hoặc điểm; chưa khẳng định mẫu ngẫu nhiên này bao phủ mọi loại EP/BVA. Golden tests ở bước 3 kiểm môi trường ba service; pilot bước 4 kiểm cả pipeline, input budget, instrumentation, charge, missing output và evaluator. Pilot không dùng để tune prompt trên tập 106. Nếu muốn phát triển prompt, dùng ví dụ ngoài panel; mọi thay đổi sau nhìn output benchmark phải được khai báo và cần tập đánh giá khác hoặc định vị exploratory.

Lịch được sinh trước output, seed `SaoCungDuoc-20261022-v1`. Hàm rank là SHA256 UTF-8 của các trường nối bằng `|`, bắt đầu bằng seed:

- Pilot: lấy bốn ID/service có rank(`pilot-selection`, service, ID) nhỏ nhất.
- Trong mỗi phase/run/service, sắp bằng rank(`order`, phase, run, service, ID). Vị trí 0-based cùng service index 0/1/2 và run-1 có tổng chẵn thì C trước; lẻ thì I trước.
- Trộn requirement giữa service bằng rank(`interleave`, phase, run, service, ID), nhưng giữ hai arm của một cặp liền nhau; không chạy hết C rồi mới I.
- Chạy pilot trước; ba run main dùng thứ tự riêng. Lưu timestamp/batch/model metadata. `pair_id` có phase/run/service/ID, còn mutant keys theo manifest.

Mỗi main run có 53 cặp C-trước và 53 cặp I-trước; 106 requirement đều có đủ C/I. Lịch model sampling không dùng seed giả định API hỗ trợ. Reset SUT giữa original/mutant và execution không có carry-over.

## 8. Kế hoạch đo và phân tích trước main

Một record cần giữ: phase, run, pair/slot/attempt ID, service/requirement/mutant index, arm, benchmark commit, prompt/config hashes, timestamp, request/response model, usage/cache tokens, charge/reservation, finish_reason, raw output, cú pháp/số test, pass-valid, kết quả từng mutant, request/input-case/assertion counts, thời gian và error category. Không lưu credential vào artifact.

**Chính:** MS_φ từng arm/run và `Δ_r = MS_φ(I,r) − MS_φ(C,r)` ghép theo run; `Δ_hat = mean_r(Δ_r)` ước lượng chênh lệch kỳ vọng `Δ = μ_I − μ_C` ở rq-validation §1. Báo Δ_hat, SD và min/max của ba Δ_r; per-service và per-requirement giữ nguyên trọng số mutant khi tổng hợp. Không union kills, không chọn run cao nhất, không bỏ generated failure khỏi mẫu số.

**Bất định:** với chỉ ba run, không có bảo đảm power. Có thể báo thêm interval Student-t 95% của trung bình ba Δ_r (`mean ± 4.30265273 × SD/sqrt(3)`) dưới giả định ba aggregate run độc lập và gần chuẩn; đánh dấu model-based/exploratory, không coi giả định đã được kiểm chứng. Nếu giả định không bảo vệ được, báo raw Δ_r/SD/range và giới hạn, không ngụy tạo CI. Không chốt một kiểm định p-value confirmatory trong thiết kế nguồn lực này. Nếu chốt phép kiểm định trước main, phải dùng hai phía cho H0: Δ = 0 và H1: Δ ≠ 0; không chọn một phía theo kỳ vọng hoặc kết quả quan sát.

**Phân tích nhạy theo composition:** bootstrap 10.000 lần, seed `SaoCungDuoc-20261022-v1-bootstrap`, lấy lại cụm requirement trong từng service, giữ toàn bộ mutant, hai arm và ba run rồi tính lại tỷ số. Đây là sensitivity về case mix của panel, **không thay thế bất định giữa các lần sinh và không là CI cho mọi REST service**. Không dùng McNemar thông thường cho 228/684 quan sát giả độc lập. Kết quả không phân biệt được không chứng minh tương đương; chưa có equivalence margin/power.

## 9. Codebook và kiểm tra độc lập cho phân tích bổ trợ

Trước khi nhìn kết quả, đánh dấu cơ hội EP/BVA bằng vague + OAS: có căn cứ / không có căn cứ / chưa xác định; trích locator schema/requirement. Không đọc mutant để chọn case thuận lợi. Danh sách này chưa được người chấm hoàn thành trong mục 2.

| Chiều chấm | Các nhãn | Căn cứ |
|---|---|---|
| Lựa chọn input | Phù hợp miền có căn cứ / sai miền / chưa xác định | Vague + OAS và code thực sinh |
| Biên | Có ranh giới được hỗ trợ / tự thêm ranh giới / không áp dụng / chưa rõ | Locator từ đầu vào cho phép; không suy từ precise |
| Tiền điều kiện | Đủ và đúng / thiếu hoặc sai / lỗi môi trường / chưa rõ | Authentication, resource/state setup và trace |
| Căn cứ oracle | Được đầu vào hỗ trợ / không được hỗ trợ / chưa rõ | Requirement/OAS; không đồng nhất unsupported với sai |
| Đúng với benchmark | Đúng / sai / chưa xác minh | Hậu kiểm độc lập dùng nguồn reference; pass-valid một mình chưa chứng minh đúng hoàn toàn |
| Hành vi cần kiểm tra | Đã kiểm / bỏ sót / ngoài scope / chưa rõ | Mục tiêu requirement; không mặc định mỗi mutant là một hành vi độc lập |

Mẫu chấm dự kiến 12 requirement, bốn/service, chọn hash độc lập với pilot bằng nhãn `qualitative-selection`; giữ cả hai arm và ba run = 72 output. Hai người chấm độc lập trên cùng mẫu; che tên arm/điểm khi khả thi, ghi hạn chế nếu nội dung prompt lộ qua code. Lưu nhãn ban đầu, agreement, bất đồng và quyết định hòa giải; không bịa IAA hoặc reviewer. Tên người chấm và giờ công còn cần nhóm chốt.

Báo số lượng/mẫu số theo service và nhãn; nếu ước lượng tỷ lệ toàn panel từ mẫu cân bằng service phải dùng trọng số 63/106, 29/106, 14/106 và coi requirement là cụm. Case giải thích tăng/giảm/không đổi chọn theo quy tắc công bố, không chỉ ví dụ thuận lợi; case ngoài mẫu ghi rõ minh họa, không cộng vào tỷ lệ mẫu. Không quy quan hệ nhân quả cho một cơ chế riêng từ các nhãn đi kèm Δ.

## 10. Điều kiện freeze và phần chưa làm

- [x] Người dùng đã cho phép môi trường, runner/pilot và đối soát; không cấp quyền main ở nhiệm vụ hiện tại.
- [x] Có bằng chứng môi trường, image/dependency/tokenizer và cost guard lịch sử; cần kiểm lại theo mã mới trước live run.
- [x] Golden/reset/patch/restore qua ba service; 106 original pass, 227 assertion kill, 1 compile lỗi NestJS 5/0 giữ mẫu số 228. Release chấp nhận bước 1 với lỗi, không nhận mọi mutant runtime-valid.
- [x] Pilot 24/24 resolved qua amendment có bằng chứng, không tune prompt; usage/request/assertion/runtime có trong report dẫn xuất. Hóa đơn chưa xác nhận.
- [ ] Chốt căn cứ R và phân tích bất định trước main; một pilot run không đo biến động giữa các lần sinh.
- [ ] Nhóm chốt hai người chấm độc lập, deadline, giờ công và cách xử lý bất đồng.
- [ ] Model mapping/giá không thay đổi; khóa SHA256 C/I/config/manifest/schedule và mọi amendment trước main.

**Phạm vi hoàn thành hiện tại:** có runner/guard và bằng chứng golden/pilot; [hồ sơ gửi cô](../.local/pilot-preparation/pilot-reconciliation-20261023-01/HO-SO-GUI-GIANG-VIEN.md) sẵn sàng để người dùng review/gửi, chưa gửi hoặc được cô duyệt. Hai người chấm/annotation/giờ công/deadline/hòa giải, căn cứ R/uncertainty, freeze/model/price/preflight/smoke mã mới còn pending. Không đổi RQ, giả thuyết, quy tắc chấm, N/R dự kiến, ngân sách hoặc prompt theo điểm; chưa main/freeze. Lượt đóng pilot không chạy SUT/model.

## Nguồn phương pháp và hỗ trợ

Lượt rà tài liệu ngày 22/10/2026 áp dụng **scientific-critical-thinking v1.5** (01/10/2026) để làm rõ RQ/PICO, giả thuyết, chênh lệch kỳ vọng/quan sát và giới hạn suy luận. Skill thuộc cùng thư viện phương pháp đã được ghi nguồn dưới đây; không thêm một nguồn vào corpus thực nghiệm. Ghi nhận experimental-design bên dưới thuộc lượt soạn thiết kế trước, không phải skill được dùng trong lượt rà này.

Thiết kế đơn vị, blocking/thứ tự và tránh pseudoreplication được hỗ trợ bởi skill **experimental-design v1.5** (30/09/2026). Có sử dụng AI hỗ trợ soạn thiết kế; nhóm chịu trách nhiệm review độc lập và nội dung cuối. Nguồn thư viện: Timothy Kassis, Vinayak Agarwal, Yuhuan He, Darshil Patel, Aubrey M. Brueckner (2026), *Scientific Agent Skills: A Library of Procedural Knowledge for Research Agents*, bản arXiv hiện hành v2 khi kiểm ngày 22/10, [DOI](https://doi.org/10.48550/arXiv.2609.00065). Đây là nguồn phương pháp/phần mềm hỗ trợ, không cộng thành bài thực nghiệm thứ 61 của corpus.
