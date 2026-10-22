# IC/EC dùng chung — nhóm 1 (SaoCungDuoc) · RQ FA26-EXT-12

## A0. Phân công nguồn tìm kiếm
| Thành viên | Nguồn phụ trách |
|---|---|
| Tùng | IEEE Xplore |
| Lâm | ACM Digital Library |
| Khôi | OpenAlex |
| T.Duy | Semantic Scholar + Google Scholar (seed & bổ sung) |
| K.Duy | Springer|

Cả nhóm phủ ≥ 3 cơ sở dữ liệu (IEEE · ACM · OpenAlex = 3 nguồn đếm chính).

## IC/EC CỐ ĐỊNH của lượt screening lịch sử (không sửa ngược)

| Mã   | Ý nghĩa                                                     |
| ---- | ----------------------------------------------------------- |
| IC-L | Paper viết bằng tiếng Anh                                   |
| IC-T | Đăng trên conference hoặc journal (không phải blog, thesis) |
| IC-E | Có ít nhất 1 con số kết quả trong Table hoặc Figure         |
| EC-D | Trùng với paper đã có                                       |
| EC-A | Không tải được full-text                                    |
| EC-S | Dưới 4 trang (abstract, poster)                             |
| EC-N | Không có thực nghiệm (vision paper, tutorial)               |

## ĐIỀN THEO RQ

| Mã | Nội dung |
| --- | --- |
| IC-Y | Từ 2020 trở đi — lý do: giữ bài gần với các công cụ/benchmark REST API hiện đại (mutation + sinh test từ yêu cầu); hướng này tăng tốc từ ~2020. Nếu thiếu paper: nới theo quy trình (ghi vào search-log). |
| IC-P | REST API: kiểm thử ở mức request cho dịch vụ HTTP (yêu cầu NL + schema API); bài toán gắn với mutant/coverage của API |
| IC-I | Kỹ thuật thiết kế test black-box: phân hoạch tương đương (EP) và/hoặc phân tích giá trị biên (BVA) cho tham số request (gồm cả so sánh với sinh dữ liệu ngẫu nhiên) |
| EC-O | Loại sẵn ≥ 2 chủ đề dễ lẫn: (1) KHÔNG về UI/E2E web testing; (2) KHÔNG về unit test thư viện nội bộ (package-level, không phải API); (3) KHÔNG thuần bug report / fault localization |

## Bổ sung 22/10/2026 — phân tuyến cho RQ LLM/prompt

Các tiêu chí trên giải thích tập 42 INCLUDE lịch sử; EC-O về unit test không cấm sử dụng bài unit test làm nền phương pháp. Bổ sung này là thiết kế cho lượt tìm mới, không thay kết quả screening đã ghi.

| Tuyến | Phạm vi được xét | Cách ghi nhận |
|---|---|---|
| REST trực tiếp | LLM/prompt sinh test hoặc oracle cho REST API từ requirement/schema; có thiết kế và kết quả thực nghiệm | Screening riêng theo protocol bổ sung §8; không đòi phải đúng đủ P/I/C/O mới được đọc |
| Nền phương pháp | LLM + EP/BVA hoặc chất lượng đặc tả/oracle ở domain khác | Ghi background/domain khác, không gán P khớp REST; không tự cộng INCLUDE lịch sử |
| GV-18 / PDF60 | Unit test Java; specification + implementation; LLM với EP/BVA so human | Thêm nguồn nền thứ 18; bộ evidence 60, PRISMA final giữ 42 |

Mọi record mới phải kiểm trùng DOI/arXiv/title với tập cũ. Preprint được ghi đúng là preprint; không tự tuyên bố đã đạt IC-T conference/journal. Bảng đối chiếu hiện hành và quyết định nguồn khác với điểm PICO nền đang được giữ lịch sử.
