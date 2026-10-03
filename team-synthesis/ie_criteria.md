# IC/EC dùng chung — nhóm 1 (SaoCungDuoc) · RQ FA26-EXT-12

## A0. Phân công nguồn tìm kiếm
| Thành viên | Nguồn phụ trách |
|---|---|
| Tung |  |
| Lam |  |
| Khoi |  |
| T.Duy |  |
| K.Duy |IEEE Explore , Google Scholar ,OpenAlex |

Cả nhóm phủ ≥ 3 cơ sở dữ liệu (IEEE · ACM · OpenAlex = 3 nguồn đếm chính).

## IC/EC CỐ ĐỊNH (không sửa)
| Mã | Ý nghĩa |
|---|---|
| IC-L | Paper viết bằng tiếng Anh |
| IC-T | Đăng trên conference hoặc journal (không phải blog, thesis) |
| IC-E | Có ít nhất 1 con số kết quả trong Table hoặc Figure |
| EC-D | Trùng với paper đã có |
| EC-A | Không tải được full-text |
| EC-S | Dưới 4 trang (abstract, poster) |
| EC-N | Không có thực nghiệm (vision paper, tutorial) |

## ĐIỀN THEO RQ (⬜ nhóm rà chốt trước khi search)
| Mã | Nội dung |
|---|---|
| IC-Y | Từ 2020 trở đi — lý do: giữ bài gần với các công cụ/benchmark REST API hiện đại (mutation + sinh test từ yêu cầu); hướng này tăng tốc từ ~2020. Nếu thiếu paper: nới theo quy trình (ghi vào search-log). |
| IC-P | REST API: kiểm thử ở mức request cho dịch vụ HTTP (yêu cầu NL + schema API); bài toán gắn với mutant/coverage của API |
| IC-I | Kỹ thuật thiết kế test black-box: phân hoạch tương đương (EP) và/hoặc phân tích giá trị biên (BVA) cho tham số request (gồm cả so sánh với sinh dữ liệu ngẫu nhiên) |
| EC-O | Loại sẵn ≥ 2 chủ đề dễ lẫn: (1) KHÔNG về UI/E2E web testing; (2) KHÔNG về unit test thư viện nội bộ (package-level, không phải API); (3) KHÔNG thuần bug report / fault localization |

## Ghi chú
- Mọi nguồn lọc theo CÙNG tiêu chí này thì mới gộp được.
- Paper dẫn chứng trên thẻ RQ là điểm xuất phát — đưa vào 01 như record thường, vẫn qua 2 vòng screening.
- Google Scholar & Semantic Scholar: chỉ dùng tìm seed + snowballing — không đếm số vào PRISMA.