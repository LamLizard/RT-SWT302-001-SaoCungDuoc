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

## IC/EC CỐ ĐỊNH (không sửa)

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

## TIÊU CHÍ BỔ SUNG VỀ SCREENING 2 VÒNG

| Mã | Nội dung |
| --- | --- |
| IC-S1 | Mỗi record từ search string và paper dẫn chứng trên thẻ RQ phải qua 2 vòng screening: V1 (title + abstract) và V2 (full-text). |
| IC-S2 | Trước khi screening, bỏ trùng theo DOI; nếu DOI thiếu, dùng chuẩn hóa title + năm; chỉ giữ 1 bản ghi cho mỗi paper. |
| IC-S3 | V1: gán quyết định `INCLUDE / EXCLUDE / Unsure` và `v1_reason` bằng mã IC/EC; `EXCLUDE` khi rõ vi phạm tiêu chí; `Unsure` chỉ được giữ lại để xem full-text. |
| IC-S4 | V2: chỉ xét full-text đối với record có `INCLUDE` hoặc `Unsure` từ V1; ghi `v2_decision` và `v2_reason`. |
| IC-S5 | Snowballing phải áp dụng cùng quy trình screening V1–V2; record mới được thêm vào 01_all_records.csv/02_after_screening_v1.csv như một record bình thường và không được bỏ qua quy tắc này. |
| IC-S6 | Kiểm chéo: ít nhất 20% số paper ban đầu hoặc 1 paper/ reviewer/ vòng phải được reviewer khác rà lại; ghi vào search-log.md với ngày và lý do. |

## Ghi chú

- Mọi nguồn lọc theo CÙNG tiêu chí này thì mới gộp được.
- Paper dẫn chứng trên thẻ RQ là điểm xuất phát — đưa vào 01 như record thường, vẫn qua 2 vòng screening.
- Google Scholar & Semantic Scholar: chỉ dùng tìm seed + snowballing — không đếm số vào PRISMA.
- Kết quả cuối cùng tuân theo quy trình PRISMA: `01_all_records.csv` → `02_after_screening_v1.csv` → `03_final_included.csv`, với V1/ V2 được ghi rõ quyết định và lý do. 
