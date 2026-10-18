# Bộ bằng chứng RBL-2 — FA26-EXT-12

**Ngày đối chiếu:** 18/10/2026 (Asia/Saigon).

Bộ dữ liệu gồm 139 bản ghi sau loại trùng để hỗ trợ lựa chọn nghiên cứu bổ sung. Người phụ trách xác nhận công cụ đã loại 46 bản trùng từ 185 bản ghi. Kết quả dedup được ghi theo xác nhận này; các phép kiểm trong bộ hồ sơ chỉ đối chiếu tính nhất quán của 139 bản ghi đã xuất.

## Hồ sơ hiện tại

| Tệp | Vai trò |
| --- | --- |
| [RBL2_audit_trail.md](RBL2_audit_trail.md) | Phương pháp tìm kiếm, dedup, triage, lựa chọn toàn văn và giới hạn kết luận. |
| [RBL2_bang_chung_tim_kiem_va_sang_loc.xlsx](RBL2_bang_chung_tim_kiem_va_sang_loc.xlsx) | Đối chiếu dữ liệu từng bản ghi; cập nhật lựa chọn toàn văn và xác nhận dedup. |
| [RBL2_log_Harvester_trich_tu_chat.md](RBL2_log_Harvester_trich_tu_chat.md) | Bản chép log nguồn; giữ nguyên chuỗi truy vấn, thời điểm và số liệu báo cáo. |

Phân tích P/I/C/O/S và kết luận tính mới hiện tại nằm tại [rq-check.md](../../rq-check.md). Bốn PDF toàn văn nằm trong thư mục [update-paper](../). Nhãn triage của 139 bản ghi được phân biệt với ba nghiên cứu chính và một dự phòng đã đọc toàn văn; seed ngoài CSV không được cộng vào 139.

## Nguồn lịch sử được bảo toàn

| Tệp | Vai trò và giới hạn |
| --- | --- |
| [du lieu buoc 2.csv](du%20lieu%20buoc%202.csv) | Dữ liệu Harvester sau dedup; giữ nguyên metadata/snippet và membership. |
| [RBL2_sang_loc_139_papers.xlsx](RBL2_sang_loc_139_papers.xlsx) | Snapshot triage ban đầu, trước khi hoàn tất đọc bốn PDF. Shortlist, trạng thái đọc và venue trong snapshot có thể là nhận xét sơ bộ; hồ sơ hiện tại nêu trên thay thế các kết luận đó. |

Các trạng thái đọc và nhãn venue trong workbook triage ban đầu phản ánh thời điểm lập bản sơ bộ. Phân tích hiện tại được trình bày trong workbook audit và `rq-check.md`. Bài amplification hiện chỉ được xác nhận là preprint; venue chính thức chưa được xác minh.

## Đối chiếu dữ liệu

CSV và hai workbook có thể được đối chiếu theo ID, metadata, membership truy vấn và nhãn triage. Workbook audit lưu riêng quy tắc và căn cứ từng bản ghi. Việc đối chiếu 139 bản ghi không đồng nghĩa đánh giá toàn văn toàn bộ hoặc kiểm lại quá trình dedup.

Các giới hạn tìm kiếm còn được ghi nhận: Q2 báo 62 hits nhưng lấy về 100, Q2/Q3 khác cách ghi `AND`, cấu hình phân trang/sắp xếp chưa xác minh, và 139 bản ghi chưa được đánh giá toàn văn toàn bộ. Đây là giới hạn của bằng chứng tìm kiếm, không phải yêu cầu kiểm lại dedup đã được người phụ trách xác nhận.
