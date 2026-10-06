# Giải thích thuật ngữ — EP+BVA và mutant REST API

Tài liệu này giải thích các thuật ngữ trong RQ và PICOS của đề tài **“Which REST API Mutants Are Found by Boundary versus Random Input Generation”**. Nội dung bám theo mô tả chủ đề và ảnh danh sách bài nền được cung cấp. Tiêu chí sàng lọc chính thức vẫn theo [IC/EC dùng chung](../../team-synthesis/ie_criteria.md) và [Review Protocol](../../team-synthesis/review-protocol.md).

## 1. Câu hỏi nghiên cứu và dữ liệu

| Thuật ngữ | Giải thích dễ hiểu |
|---|---|
| **RQ (Research Question)** | Câu hỏi nghiên cứu: trên 45 yêu cầu RESTestBench, EP+BVA và sinh dữ liệu ngẫu nhiên đồng đều với cùng ngân sách khác nhau thế nào về số mutant riêng biệt được phát hiện theo từng dạng yêu cầu? |
| **PICOS** | Khung mô tả nghiên cứu: **P**opulation, **I**ntervention, **C**omparison, **O**utcome, **S**tudy design. Với đề tài này: 45 yêu cầu từ 3 dịch vụ; EP+BVA; random đồng đều cùng số request; số mutant riêng biệt bị phát hiện theo dạng yêu cầu; 10 lần chạy có seed cố định và so sánh ghép cặp theo yêu cầu. |
| **REST API** | Giao diện HTTP để hệ thống khác gửi request và nhận response. API thường gồm các endpoint, tham số, kiểu dữ liệu và quy tắc phản hồi. |
| **RESTestBench** | Benchmark cho đánh giá test REST API, gồm yêu cầu ngôn ngữ tự nhiên, schema API, dịch vụ chạy được và mutant tương ứng. Theo mô tả RQ, nhóm dùng 45 yêu cầu, 15 yêu cầu mỗi dịch vụ, lấy từ bộ dữ liệu gốc. |
| **Yêu cầu ngôn ngữ tự nhiên (NL requirement)** | Mô tả chức năng bằng ngôn ngữ thường, chẳng hạn điều kiện hợp lệ của một request. Trong nghiên cứu, yêu cầu là căn cứ để chia lớp đầu vào và xác định điều gì cần được kiểm thử. |
| **Schema API / OpenAPI specification** | Mô tả máy đọc được về API như endpoint, tham số, kiểu dữ liệu, miền giá trị và response. Schema cung cấp cấu trúc cho việc tạo request. |
| **Docker** | Công nghệ đóng gói và chạy dịch vụ trong container. RESTestBench yêu cầu khởi chạy các dịch vụ benchmark bằng Docker; Docker Desktop/WSL2 là yêu cầu môi trường được nêu trong mô tả đề tài. |

## 2. Hai kỹ thuật được so sánh

| Thuật ngữ | Giải thích dễ hiểu |
|---|---|
| **EP (Equivalence Partitioning — phân hoạch tương đương)** | Chia miền đầu vào thành các nhóm mà các giá trị trong cùng nhóm được kỳ vọng có hành vi tương tự, rồi chọn đại diện để kiểm thử. Ví dụ, nếu tuổi hợp lệ từ 18 đến 65 thì có thể chia thành dưới 18, từ 18 đến 65, và trên 65. |
| **BVA (Boundary Value Analysis — phân tích giá trị biên)** | Chọn giá trị tại hoặc sát ranh giới của miền hợp lệ/không hợp lệ, vì lỗi hay xuất hiện ở biên. Với tuổi hợp lệ 18–65, ví dụ các giá trị cần chú ý là 17, 18, 19, 64, 65, 66. |
| **EP+BVA** | Phương pháp can thiệp trong RQ: chia lớp tương đương cho tham số request rồi chọn các giá trị biên tương ứng. Quy tắc ánh xạ yêu cầu sang partition cần được chốt trước và áp dụng nhất quán. |
| **Sinh dữ liệu ngẫu nhiên đồng đều (uniform random input generation)** | Chọn giá trị đầu vào ngẫu nhiên đồng đều từ miền được xác định. Đây là phương pháp đối chứng; miền giá trị và số request phải được so khớp với EP+BVA. |
| **Mốc so sánh / baseline** | Trong RQ này là sinh dữ liệu ngẫu nhiên đồng đều với cùng ngân sách request. |
| **Ngân sách request** | Số request được phép tạo/gửi cho mỗi yêu cầu hoặc mỗi lần chạy. So sánh cùng ngân sách nhằm tránh một kỹ thuật thắng chỉ vì gửi nhiều request hơn. |
| **Seed cố định** | Giá trị khởi tạo bộ sinh số ngẫu nhiên. Giữ seed theo kế hoạch giúp lần chạy có thể lặp lại; nếu so sánh hai kỹ thuật theo cặp, quy tắc seed phải được áp dụng thống nhất và ghi rõ. |

## 3. Mutant, oracle và kết quả đo

| Thuật ngữ | Giải thích dễ hiểu |
|---|---|
| **Mutant** | Một phiên bản dịch vụ đã bị cấy một thay đổi nhỏ có chủ ý để mô phỏng lỗi. Benchmark gắn mutant với yêu cầu hoặc dạng lỗi cụ thể. |
| **Mutation testing / kiểm thử đột biến** | Cách đánh giá test bằng cách chạy test trên bản gốc và các mutant để xem test có phát hiện được thay đổi lỗi được cấy vào hay không. |
| **Requirements-based mutation oracle** | Oracle dựa trên yêu cầu của benchmark để xác định một test có làm lộ lỗi của mutant hay không. Theo mô tả RQ, một mutant chỉ được tính là phát hiện khi test pass trên dịch vụ gốc nhưng fail trên mutant theo oracle này. |
| **Test oracle** | Quy tắc quyết định test có cho kết quả đúng hay sai. Ở đây oracle của benchmark dựa trên yêu cầu; chỉ thấy response khác nhau chưa chắc đã đủ để tính mutant là bị phát hiện. |
| **Phát hiện / kill mutant** | Test được tính là phát hiện mutant khi đáp ứng điều kiện oracle đã định nghĩa. Cần dùng cùng quy tắc cho cả EP+BVA và random. |
| **Mutant riêng biệt được phát hiện** | Đếm mỗi mutant tối đa một lần trong đơn vị phân tích đã quy định, kể cả khi nhiều request làm test fail trên mutant đó. Đây khác với số tổng request fail. |
| **Theo từng dạng yêu cầu (requirement type)** | Kết quả được phân tầng/nhóm theo các loại yêu cầu hoặc partition đã định nghĩa trong benchmark, thay vì chỉ báo cáo một tổng chung. Cách gán mỗi yêu cầu vào nhóm cần được xác định rõ. |
| **Mutation score** | Thường là tỷ lệ mutant bị kill trên tổng mutant được tính vào mẫu số. RQ này nêu outcome là **số mutant riêng biệt được phát hiện**, không nên tự đổi outcome thành mutation score; nếu báo cáo score bổ sung thì phải ghi rõ công thức và mẫu số. |
| **Coverage (độ bao phủ)** | Mức độ test chạm tới mã, endpoint, operation hoặc đặc tả. Coverage không đồng nghĩa với phát hiện mutant: bao phủ cao không đảm bảo tìm được nhiều lỗi. |

## 4. Thiết kế so sánh và thống kê

| Thuật ngữ | Giải thích dễ hiểu |
|---|---|
| **Lần chạy lặp (repeated run)** | Chạy lại mỗi kỹ thuật nhiều lần để quan sát biến thiên do quá trình sinh dữ liệu. Mô tả đề tài quy định 10 lần chạy với seed cố định cho mỗi kỹ thuật-yêu cầu. |
| **So sánh ghép cặp (paired comparison)** | So sánh hai kỹ thuật trên cùng yêu cầu (và theo thiết kế, cùng mức ngân sách), thay vì so hai tập yêu cầu khác nhau. Việc ghép cặp giúp hạn chế ảnh hưởng do độ khó khác nhau giữa các yêu cầu. |
| **Wilcoxon signed-rank test** | Kiểm định phi tham số cho dữ liệu ghép cặp, dùng để đánh giá liệu chênh lệch giữa hai điều kiện có khác 0 một cách có ý nghĩa hay không. Cần nêu đơn vị ghép cặp và cách tổng hợp các lần chạy. |
| **Hiệu chỉnh Holm (Holm correction)** | Điều chỉnh ngưỡng kiểm định khi thực hiện nhiều phép so sánh để hạn chế nguy cơ kết luận dương tính giả do kiểm định lặp nhiều lần. RQ nhắc Holm cho các kiểm định nhiều nhóm/nhóm yêu cầu. |
| **Mức ý nghĩa và kích thước ảnh hưởng** | Mức ý nghĩa cho biết ngưỡng quyết định thống kê; kích thước ảnh hưởng mô tả độ lớn thực tế của khác biệt. Khi báo cáo, không nên chỉ nêu p-value. Cần theo kế hoạch phân tích đã chốt. |

## 5. Tìm kiếm tài liệu và snowballing

| Thuật ngữ | Giải thích dễ hiểu |
|---|---|
| **SLR (Systematic Literature Review)** | Tổng quan tài liệu theo quy trình có thể kiểm tra lại: nêu nguồn, truy vấn, ngày tìm, tiêu chí nhận/loại và số record ở từng bước. |
| **Seed paper** | Bài đã được xác nhận phù hợp và được chọn làm điểm bắt đầu để lần theo tài liệu tham khảo và bài trích dẫn. Bài xuất hiện trên thẻ đề tài chưa tự động là bài được include hoặc seed hợp lệ. |
| **Snowballing backward (lùi)** | Xem References của seed để tìm các bài mà seed đã trích dẫn. |
| **Snowballing forward (tiến)** | Tìm bài mới đã trích dẫn seed, thường qua “Cited by” hoặc “Citations”. |
| **Screening** | Sàng lọc tiêu đề/abstract rồi toàn văn theo IC/EC. Bài tìm thấy trong citation search chỉ là record ứng viên cho đến khi được sàng lọc. |
| **IC/EC** | Inclusion Criteria là điều kiện nhận bài; Exclusion Criteria là điều kiện loại. Dùng nguyên tiêu chí đã chốt của nhóm, không suy ra include chỉ vì bài nói về REST API testing hoặc mutant. |
| **Deduplication (bỏ trùng)** | Hợp nhất các record trỏ tới cùng một bài bằng DOI, tiêu đề, tác giả/năm. Tổng lượt thấy qua nhiều seed không đồng nghĩa với số bài độc nhất. |
| **Search log** | Nhật ký truy vấn hoặc citation search: lưu seed/DOI, hướng, vòng, nguồn, ngày, số bài xem, số trùng và số record được chuyển vào danh sách screening. |

## 6. Nguyên tắc diễn giải danh sách bài nền

1. Đề tài tập trung vào **mutant REST API nào được tìm thấy bởi EP+BVA so với random** trên RESTestBench.
2. Một bài nói về REST API, LLM, fuzzing, oracle hoặc mutation testing vẫn chưa chắc khớp RQ. Cần kiểm tra xem nội dung có liên quan tới đầu vào biên/phân hoạch hoặc cách đánh giá mutant theo phạm vi đã chốt hay không.
3. Bài SLR về microservices, unit testing, GUI/mobile, bug reports hoặc flaky-test diagnosis có thể là bối cảnh phụ; không mặc nhiên tính là bằng chứng trực tiếp cho RQ.
4. Giữ riêng **candidate**, **đã qua screening**, và **included cuối cùng**. Không tự nâng trạng thái record nếu chưa có quyết định theo quy trình nhóm.
5. Số liệu về mutation score, coverage, số bug thực tế và số mutant riêng biệt là các đại lượng khác nhau; ghi đúng định nghĩa nguồn khi trích xuất.
