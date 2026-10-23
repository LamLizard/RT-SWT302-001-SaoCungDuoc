# Báo cáo rà soát tài liệu RQ/PICO/protocol — gửi Leader

**Ngày thực hiện/cập nhật:** 22/10/2026 · Asia/Saigon. **Nhánh:** `Lam`.
**Mốc đối chiếu lượt này:** HEAD `9cdc33dd0e3e096e30e591c65f08fa683741f863` — `[RBL-2] Update RQ and experiments design`.

**Yêu cầu:** giữ một RQ chính của cô Chi; làm rõ PICO, H0/H1; tinh gọn protocol tìm tài liệu và đồng bộ mô tả hiện hành. Người dùng đã cho phép implement tài liệu. Chỉ agent chính, chỉ áp dụng skill **scientific-critical-thinking v1.5**; nguồn thư viện phương pháp đã được ghi nhận ở cuối [experiment-design](team-synthesis/experiment-design.md), không cộng vào corpus.

## 1. Thay đổi cụ thể và lý do

| File | Thay đổi trong lượt này | Lý do |
|---|---|---|
| [review-protocol.md](team-synthesis/review-protocol.md) | Gộp nội dung mục 8 vào §3 (tìm kiếm/trạng thái) và §5 (trích xuất/đối chiếu); giữ anchor cũ để truy vết. Giữ query cũ, A1–A3 dự kiến và lịch sử lượt web riêng biệt; làm rõ 60 nguồn / PRISMA 42. | Mục 8 được thêm vì protocol cũ chủ yếu tìm EP+BVA so random, chưa bao phủ đầy đủ RQ prompt/LLM. Gộp nội dung giúp đọc liền mạch, không biến đề xuất thành tìm kiếm đã thực hiện. |
| [rq-evidence-map.md](team-synthesis/rq-evidence-map.md) | Viết rõ P/I/C/O ngay vị trí khai báo; tách model/cấu hình/ngân sách và số liệu kiểm kê khỏi PICO. | P là yêu cầu vague tại phiên bản đóng băng; mutant là đối tượng đo, model/budget là điều kiện kiểm soát. Giữ nguyên phần ma trận/điểm nền. |
| [rq-validation.md](team-synthesis/rq-validation.md) | Giữ nguyên văn một RQ chính; chuyển “RQ phân tích” thành mục tiêu bổ trợ; giải thích nguồn gốc từ mail cô. Viết đầy đủ H0/H1 và phân biệt Δ kỳ vọng với Δ_hat quan sát. | Cô gợi ý phân tích cải thiện/suy giảm để diễn giải kết quả; nội dung này không cần đứng thành RQ thứ hai. H0: Δ = 0 và H1: Δ ≠ 0 vẫn bổ sung nhau; cách viết rút gọn trước gây khó hiểu, bản chất giả thuyết không đổi. |
| [experiment-design.md](team-synthesis/experiment-design.md) | Đồng bộ §1, §8 và tên §9 theo một RQ + phân tích bổ trợ; làm rõ ký hiệu chênh lệch và định hướng kiểm định hai phía; ghi nhận skill của lượt rà. | Không mặc định EP+BVA tốt hơn; liên hệ giữa nhãn test và kết quả không tự chứng minh cơ chế nhân quả. Không chọn thêm phép kiểm định hoặc sửa thiết kế chạy. |
| [notes.md](notes.md) | Sửa mô tả hiện hành, thêm quyết định ngày 22/10 và link báo cáo mới; giữ các mục lịch sử. | Truy vết được việc trước đây đã thêm RQ phân tích và nay đổi tư cách thành mục tiêu bổ trợ. |
| [search-log.md](lam/SLR/search-log.md), §13 | Thêm nhật ký lý do/phạm vi lượt rà, giữ nguyên §1–12. | Tuân thủ quy tắc ghi mọi amendment của protocol; không tạo một lượt tìm kiếm mới. |
| Báo cáo này | Đổi tên từ `TEMP_RESEARCH_SYNC_REVIEW_2026-10-21.md` sang ngày thực hiện **2026-10-22** và viết lại phần bàn giao ngắn gọn. | Tên và ngày nội dung cùng là 22/10/2026; mô tả đúng lượt sửa hiện tại, không dùng mốc HEAD hoặc trạng thái untracked của đợt trước. |

## 2. Nội dung nghiên cứu được giữ

**RQ chính:** Trong điều kiện sinh single-step với cùng mô hình, cấu hình và ngân sách kiểm thử được quy định trước, việc bổ sung hướng dẫn EP+BVA vào prompt gốc ảnh hưởng như thế nào đến MS_φ trên các yêu cầu vague của RESTestBench tại phiên bản đóng băng?

- **PICO:** P = các yêu cầu vague của RESTestBench tại phiên bản đóng băng; I = prompt gốc bổ sung hướng dẫn EP+BVA có căn cứ; C = prompt single-step gốc; O = MS_φ. Model, cấu hình và ngân sách là điều kiện kiểm soát riêng.
- **Giả thuyết:** Δ = μ_I − μ_C, với μ là MS_φ kỳ vọng qua các lần sinh trên cùng panel và điều kiện so sánh. H0: Δ = 0; H1: Δ ≠ 0. Giữ hai phía; không có ý nghĩa thống kê không chứng minh bằng nhau/tương đương. R=3 vẫn là phương án review, chưa chốt kiểm định confirmatory.
- **Benchmark:** commit `4decc1e36ea3dd41b64ce3e3ac6a85bc72df36ae`; 106 yêu cầu vague / 228 mutant (FastAPI 63/141, RealWorld 29/65, TodoApp 14/22). Đây là kiểm kê tĩnh kế thừa manifest, chưa xác minh runtime.
- **Model/tiền:** DeepSeek-V4.1-Flash-1017, DeepSeek API chính thức; tối đa **3 USD tổng pilot + main + retry**. Alias `deepseek-flash` không bảo đảm checkpoint bất biến; mapping, tham số, giá và chi phí thật phải xác minh trước khi chạy.
- **Evidence:** corpus 60 nguồn = 42 INCLUDE lịch sử + 18 nguồn nền; PRISMA final vẫn 42. Không chấm lại hoặc sửa 59 hàng điểm nền cũ.

**Lịch sử được bảo toàn:** hai bước nền tảng tài liệu và thiết kế/artifacts đã có từ lượt trước. Lượt đó thêm “RQ phân tích” theo gợi ý của cô, bổ sung GV-18/Rodríguez và mục 8 của protocol; xem [search-log §11–12](lam/SLR/search-log.md). Lượt hiện tại chỉ sửa cách tổ chức/diễn đạt và ghi amendment §13, không viết lại lịch sử như thể các phần đó chưa từng tồn tại.

## 3. Kiểm tra trong lượt này

Nguồn đối chiếu: [mail/trao đổi cô Chi](lam/SLR/AI%20cua%20lam%20response.txt), [PDF60](Paper-source/60-Martin%20Rodriguez.pdf), thiết kế và các artifact local. Không tra cứu web/CSDL mới hoặc kiểm lại metadata/giá API trực tuyến trong lượt này.

| Kiểm tra tĩnh | Kết quả và giới hạn |
|---|---|
| Git/phạm vi | Nhánh và HEAD giữ nguyên; chỉ sửa 7 tài liệu kể cả báo cáo đổi tên. File mail untracked có sẵn được giữ nguyên, không stage. |
| RQ/PICO/giả thuyết | Nguyên văn RQ chính giữ nguyên; PICO rõ tại dòng 5 của map; các mô tả hiện hành đã thống nhất một RQ + phân tích bổ trợ. H0/H1 vẫn hai phía; không có phép kiểm định nào được chạy. |
| Truy vết tìm kiếm/lịch sử | String A/B-C, quy tắc chạy và A1–A3 giữ nguyên; A1–A3 vẫn là dự kiến. Nội dung nhật ký §1–12 và lịch sử notes giữ nguyên; mục 8 cũ có anchor dẫn đến phần đã gộp. |
| File bảo toàn | SHA256 prompt C/I, config, manifest, lịch, file mail, bảng evidence gộp và PRISMA không đổi. Toàn bộ phần map từ §1 trở đi giữ nguyên; không sửa hàng điểm cũ. |
| Số lượng | Đối soát manifest local: 106 khóa requirement duy nhất / 228 mutant, vague không rỗng; map và bảng gộp có 60 dòng nguồn, PRISMA vẫn 42. Không tải lại 106 JSON hoặc xác minh runtime trong lượt này. |
| Liên kết/định dạng | Đã rà đích file local, anchor liên quan và diff/whitespace. Không kiểm mọi URL bên ngoài hoặc xác minh các phát biểu lịch sử bằng chạy lại thực nghiệm. |

## 4. Chưa thực hiện và giới hạn bàn giao

- Thiết kế vẫn chờ nhóm/cô review, **chưa freeze**. Chưa duyệt số run, phương pháp suy luận cuối, người chấm độc lập và deadline.
- Chưa triển khai bước 3: môi trường, dependency lock, golden tests, reset/patch/mutant/evaluator và đối soát mất output. Chưa chứng minh evaluator đúng hoặc benchmark chạy được trên máy nhóm.
- Chưa runner, instrumentation, bộ chặn tiền hoặc token/accounting preflight; chưa pilot/main, gọi API hoặc phát sinh chi phí model. Dự toán hiện có không chứng minh toàn lịch chạy vừa 3 USD.
- Không đổi prompt C/I, manifest, cấu hình, lịch chạy hay số liệu thực nghiệm; không cài thư viện, chạy Docker, build/test benchmark, stage, commit hoặc push.
- Chưa systematic search/screening mới theo A1–A3, tái thẩm định toàn bộ corpus, chấm độc lập hoặc gửi hồ sơ cho cô. Không có MS_φ, Δ_hat, CI/p-value thực nghiệm hay kết luận ưu thế để báo cáo.
