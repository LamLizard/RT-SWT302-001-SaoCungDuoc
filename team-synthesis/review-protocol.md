# Review Protocol — nhóm 1 (SaoCungDuoc) · RQ FA26-EXT-12

Mọi thay đổi sau khi ban hành: ghi vào search-log.md kèm lý do + ngày (không sửa lặng lẽ). Đợt đồng bộ 21/10/2026 và các lượt bổ sung/rà tài liệu 22/10/2026 được ghi tại [nhật ký Lâm](../lam/SLR/search-log.md), §10–13; không xem mỗi lượt sửa tài liệu là một lượt chạy query mới.

## 1. Câu hỏi nghiên cứu hiện hành — 22/10/2026

- **RQ chính:** Trong điều kiện sinh single-step với cùng mô hình, cấu hình và ngân sách kiểm thử được quy định trước, việc bổ sung hướng dẫn EP+BVA vào prompt gốc ảnh hưởng như thế nào đến MS_φ trên các yêu cầu vague của RESTestBench tại phiên bản đóng băng?
- **Mục tiêu phân tích bổ trợ:** mô tả khác biệt về input, tiền điều kiện và oracle đi kèm cải thiện/suy giảm/không đổi MS_φ để diễn giải RQ chính; không đặt thành RQ riêng hoặc suy cơ chế nhân quả từ liên hệ quan sát. Nguồn gốc việc từng thêm “RQ phân tích” được giữ ở [rq-validation §1](rq-validation.md#1-rq--pico).
- **PICO:** P = các yêu cầu vague của RESTestBench tại phiên bản đóng băng, commit `4decc1e36ea3dd41b64ce3e3ac6a85bc72df36ae`; I = prompt gốc bổ sung hướng dẫn EP+BVA có căn cứ; C = prompt single-step gốc; O = MS_φ. Kiểm kê 106 vague / 228 mutant là dữ liệu tĩnh, chưa xác minh runtime.
- **Điều kiện kiểm soát, tách khỏi PICO:** cùng mô hình, cấu hình và ngân sách kiểm thử quy định trước. Người dùng chọn DeepSeek-V4.1-Flash-1017 qua DeepSeek API chính thức; tổng chi phí model tối đa 3 USD, gồm pilot/main/retry. Alias `deepseek-flash` không bảo đảm checkpoint bất biến; cần xác minh trước khi chạy.
- **H0/H1:** với Δ là chênh lệch MS_φ kỳ vọng I − C trên panel cố định dưới cùng điều kiện, H0: Δ = 0; H1: Δ ≠ 0 (hai phía). Phát biểu đầy đủ tại [rq-validation §1](rq-validation.md#1-rq--pico), kế hoạch phân tích và giới hạn số lần sinh ở [experiment-design](experiment-design.md); chưa chạy thực nghiệm, thiết kế chưa freeze.

Đóng góp đề xuất gồm phép so có kiểm soát, phân tích thành công/thất bại và gói tái lập. Nhãn extension cần được nhóm/cô review; không chứng minh novelty bằng điểm PICO hoặc tuyên bố thêm EP+BVA vào prompt là mới. Điểm nền được giữ lịch sử, xem [rq-validation](rq-validation.md).

## 2. Nguồn & phân công

| Thành viên | Nguồn |
|---|---|
| Tung | IEEE Xplore |
| Lam | ACM Digital Library |
| Khoi | OpenAlex |
| T.Duy | Semantic Scholar + Google Scholar (seed & bổ sung) |
| K.Duy |Springer |

<a id="3-phạm-vi-tìm"></a>

## 3. Phạm vi tìm và trạng thái protocol

### 3.1. Protocol kế thừa của hướng EP+BVA so với random

Các chuỗi và quy tắc dưới đây được giữ để truy vết cách tạo tập 42 INCLUDE; chưa phải protocol tìm kiếm đã khóa cho phép so prompt-guided EP+BVA/single-step. Đợt đồng bộ 21/10 không chạy query bổ sung. Protocol cũ chưa bao phủ đầy đủ RQ prompt/LLM; không sửa ngược số lượt tìm, số bài hoặc PRISMA.

- Trường tìm: Title / Abstract / Keywords
- Khoảng năm: từ 2020 (theo IC-Y)
- **String A (CHÍNH THỨC của protocol cũ — giữ nguyên văn để truy vết):** ("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing") AND ("fault detection" OR "mutant detection" OR "bugs found")
- String B/C (dùng khi cần nới — giữ bản nháp cũ làm dự phòng, bổ sung từ đồng nghĩa khi chạy): ("REST API" OR "RESTful API" OR "web API" OR "web service") AND ("boundary value analysis" OR "boundary value" OR "boundary testing" OR "equivalence partitioning") AND ("mutation testing" OR "mutants" OR "mutation score")
- Quy tắc chạy: >500 kết quả → AND thêm tên dataset ("RESTestBench"); <20 → bỏ khối O trước; ghi MỌI phiên bản chuỗi + số kết quả vào search-log.
- Chạy chính để đếm: IEEE / ACM / OpenAlex. Google Scholar & Semantic Scholar KHÔNG đếm vào PRISMA.

<a id="8-protocol-bổ-sung-cho-rq-prompt--phiên-bản-review-22102026"></a>

### 3.2. Bổ sung dự kiến cho RQ prompt/LLM — bản review 22/10/2026

Nội dung này trước đây được tách thành **mục 8** để bổ sung hướng tìm phù hợp RQ mới, vì protocol cũ chủ yếu tìm EP+BVA so với random. Nay gộp phần tìm kiếm vào §3 và phần trích xuất vào §5; đây vẫn là đề xuất chờ review, không làm cho protocol cũ mặc nhiên bao phủ RQ mới.

Hai lớp nguồn cần đối chiếu:

1. **REST API trực tiếp:** LLM sinh test/oracle từ yêu cầu hoặc tài liệu API; xét prompt engineering, lựa chọn input, oracle và ngân sách. Không bắt buộc mọi bài dùng RESTestBench hoặc MS_φ.
2. **Cơ sở phương pháp:** LLM + EP/BVA hoặc ảnh hưởng của đặc tả thiếu chi tiết trong unit/integration testing; gắn nhãn domain khác. GV-18/Rodríguez thuộc lớp này, là nguồn nền cô yêu cầu, không phải INCLUDE mới theo EC-O cũ.

Chuỗi **đề xuất cho lượt CSDL tiếp theo, chưa chạy**:

- A1: `(REST API OR RESTful API) AND (large language model OR LLM) AND (test generation OR oracle generation OR prompt OR test amplification)`.
- A2: `(large language model OR LLM) AND (equivalence partitioning OR boundary value analysis OR boundary testing) AND (test generation OR unit test OR integration test)`.
- A3: `(REST API OR RESTestBench) AND (vague OR underspecified OR natural language requirements OR oracle) AND (LLM OR prompt)`.

Cần nhóm duyệt chuỗi/tiêu chí và ghi biến thể cú pháp từng CSDL trước khi chạy. Chạy chính giữ IEEE/ACM/OpenAlex theo phân công; tra cứu web/snowballing ghi riêng và không tự cộng vào PRISMA. Cửa sổ ưu tiên đề xuất: 22/10/2025–22/10/2026; nguồn nền quan trọng ngoài cửa sổ vẫn được đối chiếu và gắn nhãn.

### 3.3. Lượt đã được ghi nhận và giới hạn

Theo [search-log §11](../lam/SLR/search-log.md), lượt bổ sung trước trong ngày 22/10 đã tra cứu web có hướng và đọc các phần liên quan của PDF GV-18, TD-0002, GV-02/GV-03/GV-04. Ba nguồn 2026 đã có trong tập cũ, không cộng trùng. Corpus có 60 nguồn sau thêm GV-18; PRISMA final vẫn 42. Chưa hoàn thành systematic search/screening mới theo A1–A3; không khẳng định bao phủ toàn lĩnh vực. Lượt rà tài liệu tiếp theo tại §13 chỉ đối chiếu nguồn local và chỉnh cách trình bày, không chạy lại các truy vấn này.

## 4. Tiêu chí lọc

Tiêu chí kế thừa tại [ie_criteria.md](ie_criteria.md) giải thích tập screening cũ; chưa được tái thẩm định đầy đủ cho RQ prompt mới. Tập trước bổ sung là **42 INCLUDE + 17 bài nền = 59 nguồn**; hiện có **60 nguồn = 42 INCLUDE + 18 nguồn nền** sau thêm GV-18, PRISMA final vẫn 42. Quy trình dưới đây là bản đã ban hành, không phải các bước vừa chạy lại:

- Bước 1: thu thập `01_all_records.csv` từ các query chính; trước khi screening, bỏ trùng theo DOI (nếu thiếu DOI thì theo title + năm); giữ một bản ghi cho mỗi paper.
- Bước 2: vòng 1 screening trên title + abstract; mỗi record gán `v1_decision` = `INCLUDE / EXCLUDE / Unsure` và `v1_reason` theo mã IC/EC.
- Bước 3: vòng 2 screening trên full-text; chỉ xét record có `INCLUDE` hoặc `Unsure` ở V1; gán `v2_decision` và `v2_reason`.
- Bước 4: snowballing áp dụng cùng quy trình V1–V2; record mới được thêm vào PRISMA như record bình thường và không được bỏ qua.
- Bước 5: kiểm chéo 20% số paper hoặc tối thiểu 1 paper per reviewer/ vòng; ghi vào `search-log.md` kèm ngày và lý do.

PRISMA đầu ra theo thứ tự: `01_all_records.csv` → `02_after_screening_v1.csv` → `03_final_included.csv`.

## 5. Cột Evidence Table

Paper (tên + năm + venue + DOI) · Tool/LLM · Dataset · Metric · Kết quả · Code · Hạn chế · Gần RQ.

Với phần đối chiếu RQ hiện hành, ghi thêm tác giả, DOI hoặc arXiv, phiên bản PDF, trang/mục, đầu vào được phép, can thiệp/comparator, metric/mẫu số, ngân sách và threats tác giả nêu. Phân biệt AUTHOR_STATED / REVIEWER_INFERRED / NOT_VERIFIED. Cùng tên mutation score không tự bằng MS_φ; phép so LLM với người viết test không bằng phép so hai prompt có/không EP+BVA.

Đối chiếu nội dung với RQ hiện hành riêng, không đổi tên dấu ✓ hoặc chấm lại các hàng điểm nền. Tái thẩm định toàn tập cũ cần lượt có log và kiểm tra độc lập; không gán x/N limitation hoặc số hit CSDL từ kết quả web.

## 6. Xử lý bất đồng

- Lọc: lưỡng lự ghi Unsure ở V1; bất đồng nhiều → PL làm rõ IC/EC cho cả nhóm.
- Trích xuất: lệch > 10% số ô được kiểm → người trích xuất rà lại toàn bộ bảng; không tự thống nhất được → hỏi PL.

## 7. Mốc thời gian

- Mốc của protocol ban đầu: **23:59 05/10/2026** · Snowballing: Ngày 3–4 (1 vòng bắt buộc, tối đa 2) · Screening xong: Ngày 4 · Evidence table + kiểm chéo: Ngày 4–5 · Gộp nhóm: cuối tuần. Search-log có các lượt thực tế sau mốc này; giữ lịch sử, không suy đây là ngày dừng thực tế đã xác minh. Mốc/protocol bổ sung cho RQ hiện hành chưa chốt.
