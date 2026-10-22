# Review Protocol — nhóm 1 (SaoCungDuoc) · RQ FA26-EXT-12

Mọi thay đổi sau khi ban hành: ghi vào search-log.md kèm lý do + ngày (không sửa lặng lẽ). Đợt đồng bộ 21/10/2026 được ghi tại [nhật ký Lâm](../lam/SLR/search-log.md); không phải một lượt chạy query mới.

## 1. Câu hỏi nghiên cứu hiện hành — 22/10/2026

- **RQ chính:** Trong điều kiện sinh single-step với cùng mô hình, cấu hình và ngân sách kiểm thử được quy định trước, việc bổ sung hướng dẫn EP+BVA vào prompt gốc ảnh hưởng như thế nào đến MS_φ trên các yêu cầu vague của RESTestBench tại phiên bản đóng băng?
- **RQ phân tích:** Các trường hợp cải thiện hoặc suy giảm MS_φ đi kèm những khác biệt nào về lựa chọn dữ liệu kiểm thử, thiết lập tiền điều kiện và tính đúng của oracle?
- **PICO:** P = 106 vague / 228 mutant tại commit `4decc1e36ea3dd41b64ce3e3ac6a85bc72df36ae`; I = C + hướng dẫn EP+BVA có căn cứ; C = single-step gốc; O = MS_φ và kết quả bổ sung.
- **Quyết định người dùng:** DeepSeek-V4.1-Flash-1017 qua DeepSeek API chính thức; tổng chi phí model tối đa 3 USD, kể cả pilot/retry.
- **H0/H1:** chênh lệch kỳ vọng MS_φ bằng 0 / khác 0 dưới điều kiện đã quy định; kế hoạch phân tích và giới hạn số lần sinh ở [experiment-design](experiment-design.md), chưa chạy thực nghiệm.

Đóng góp đề xuất gồm phép so có kiểm soát, phân tích thành công/thất bại và gói tái lập. Nhãn extension cần được nhóm/cô review; không chứng minh novelty bằng điểm PICO hoặc tuyên bố thêm EP+BVA vào prompt là mới. Điểm nền được giữ lịch sử, xem [rq-validation](rq-validation.md).

## 2. Nguồn & phân công
| Thành viên | Nguồn |
|---|---|
| Tung | IEEE Xplore |
| Lam | ACM Digital Library |
| Khoi | OpenAlex |
| T.Duy | Semantic Scholar + Google Scholar (seed & bổ sung) |
| K.Duy |Springer |

## 3. Phạm vi tìm — protocol kế thừa của hướng cũ

Các chuỗi và quy tắc dưới đây được giữ để truy vết cách tạo tập 42 INCLUDE; chưa phải protocol tìm kiếm mới được khóa cho phép so prompt-guided EP+BVA/single-step. Chưa có query bổ sung cho RQ mới trong đợt đồng bộ này. Cần nhóm chốt chuỗi có LLM/prompt và tiêu chí phù hợp RQ mới trước khi tìm bổ sung; không tự sửa số lượt tìm, số bài hoặc PRISMA.

- Trường tìm: Title / Abstract / Keywords
- Khoảng năm: từ 2020 (theo IC-Y)
- **String A (CHÍNH THỨC của protocol cũ — giữ nguyên văn để truy vết):** ("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing") AND ("fault detection" OR "mutant detection" OR "bugs found")
- String B/C (dùng khi cần nới — giữ bản nháp cũ làm dự phòng, bổ sung từ đồng nghĩa khi chạy): ("REST API" OR "RESTful API" OR "web API" OR "web service") AND ("boundary value analysis" OR "boundary value" OR "boundary testing" OR "equivalence partitioning") AND ("mutation testing" OR "mutants" OR "mutation score")
- Quy tắc chạy: >500 kết quả → AND thêm tên dataset ("RESTestBench"); <20 → bỏ khối O trước; ghi MỌI phiên bản chuỗi + số kết quả vào search-log.
- Chạy chính để đếm: IEEE / ACM / OpenAlex. Google Scholar & Semantic Scholar KHÔNG đếm vào PRISMA.

## 4. Tiêu chí lọc

Tiêu chí kế thừa tại `team-synthesis/ie_criteria.md` giải thích tập screening cũ; chưa được tái thẩm định đầy đủ cho RQ prompt mới. Giữ số **42 INCLUDE + 17 bài nền = 59 evidence**, không mặc nhiên xem 59 là số INCLUDE. Quy trình dưới đây là bản đã ban hành, không phải các bước vừa chạy lại:

- Bước 1: thu thập `01_all_records.csv` từ các query chính; trước khi screening, bỏ trùng theo DOI (nếu thiếu DOI thì theo title + năm); giữ một bản ghi cho mỗi paper.
- Bước 2: vòng 1 screening trên title + abstract; mỗi record gán `v1_decision` = `INCLUDE / EXCLUDE / Unsure` và `v1_reason` theo mã IC/EC.
- Bước 3: vòng 2 screening trên full-text; chỉ xét record có `INCLUDE` hoặc `Unsure` ở V1; gán `v2_decision` và `v2_reason`.
- Bước 4: snowballing áp dụng cùng quy trình V1–V2; record mới được thêm vào PRISMA như record bình thường và không được bỏ qua.
- Bước 5: kiểm chéo 20% số paper hoặc tối thiểu 1 paper per reviewer/ vòng; ghi vào `search-log.md` kèm ngày và lý do.

PRISMA đầu ra theo thứ tự: `01_all_records.csv` → `02_after_screening_v1.csv` → `03_final_included.csv`.

## 5. Cột Evidence Table

Paper (tên + năm + venue + DOI) · Tool/LLM · Dataset · Metric · Kết quả · Code · Hạn chế · Gần RQ.

## 6. Xử lý bất đồng

- Lọc: lưỡng lự ghi Unsure ở V1; bất đồng nhiều → PL làm rõ IC/EC cho cả nhóm.
- Trích xuất: lệch > 10% số ô được kiểm → người trích xuất rà lại toàn bộ bảng; không tự thống nhất được → hỏi PL.

## 7. Mốc thời gian

- Mốc của protocol ban đầu: **23:59 05/10/2026** · Snowballing: Ngày 3–4 (1 vòng bắt buộc, tối đa 2) · Screening xong: Ngày 4 · Evidence table + kiểm chéo: Ngày 4–5 · Gộp nhóm: cuối tuần. Search-log có các lượt thực tế sau mốc này; giữ lịch sử, không suy đây là ngày dừng thực tế đã xác minh. Mốc/protocol bổ sung cho RQ hiện hành chưa chốt.

## 8. Protocol bổ sung cho RQ prompt — phiên bản review 22/10/2026

Phần §3–7 là hồ sơ tạo tập 42 INCLUDE, không sửa ngược query, IC/EC, ngày hoặc số screening. Phần này quy định lượt bổ sung, không tuyên bố đã chạy ba CSDL một lần nữa.

### 8.1. Hai lớp nguồn

1. **Lớp nghiên cứu REST API trực tiếp:** LLM sinh test/oracle từ yêu cầu/tài liệu API; tìm cả prompt engineering, input selection, oracle và budget. Không buộc mọi bài phải dùng đúng RESTestBench hoặc MS_φ mới được xem xét.
2. **Lớp cơ sở phương pháp:** LLM + EP/BVA hoặc ảnh hưởng của đặc tả thiếu chi tiết trong unit/integration testing. Đánh dấu domain khác. GV-18/Rodríguez thuộc lớp này, là nguồn nền cô yêu cầu, không phải INCLUDE mới theo EC-O cũ.

### 8.2. Chuỗi đề xuất cho lượt CSDL tiếp theo

- A1: `(REST API OR RESTful API) AND (large language model OR LLM) AND (test generation OR oracle generation OR prompt OR test amplification)`.
- A2: `(large language model OR LLM) AND (equivalence partitioning OR boundary value analysis OR boundary testing) AND (test generation OR unit test OR integration test)`.
- A3: `(REST API OR RESTestBench) AND (vague OR underspecified OR natural language requirements OR oracle) AND (LLM OR prompt)`.

Chuỗi là bản review, phải ghi biến thể cú pháp từng CSDL trước khi chạy. Chạy chính giữ IEEE/ACM/OpenAlex theo phân công; tra cứu web/snowballing ghi riêng và không tự cộng vào PRISMA. Cửa sổ ưu tiên nghiên cứu gần đây: 22/10/2025–22/10/2026; các nguồn nền quan trọng ngoài cửa sổ vẫn được đối chiếu và gắn nhãn.

### 8.3. Bằng chứng và chấm đối chiếu

Ghi title/author/year/DOI hoặc arXiv, phiên bản PDF, trang/mục, input được phép, can thiệp, comparator, metric/mẫu số, ngân sách thực nghiệm và threats tác giả nêu. Phân biệt AUTHOR_STATED / REVIEWER_INFERRED / NOT_VERIFIED. Cùng tên mutation score không tự bằng MS_φ; LLM với người viết test không bằng hai prompt có/không EP+BVA.

Mỗi bài được đối chiếu nội dung với RQ hiện hành riêng; không tái đặt tên dấu ✓ của bảng nền thành kết quả chấm mới. Muốn tái thẩm định toàn bộ tập cũ cần một lượt có log và kiểm tra độc lập. Không gán x/N limitation hoặc số hit của CSDL từ kết quả web.

### 8.4. Lượt đã thực hiện và phần còn mở

Ngày 22/10 thực hiện tra cứu web có hướng, đọc các phần liên quan của PDF GV-18, TD-0002, GV-02/GV-03/GV-04; log tại [search-log §11](../lam/SLR/search-log.md). Ba nguồn 2026 đã có trong tập cũ, không cộng trùng. Bộ đối chiếu có 60 nguồn sau thêm GV-18; PRISMA final vẫn 42. Chưa hoàn thành một lượt systematic search/screening mới theo A1–A3; không dùng bản cập nhật này để khẳng định bao phủ toàn lĩnh vực.
