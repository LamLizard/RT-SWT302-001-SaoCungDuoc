# Trạng thái kiểm chứng RQ — FA26-EXT-12

**Cập nhật:** 20/10/2026. [Bản tổng hợp](rq-validation.md) · [PRISMA](prisma-team.md) · [Audit 17 PDF](pico-audit-17-papers.md).

## 1. Tiến độ đồng bộ theo kế hoạch

| Bước | Trạng thái |
|---|---|
| 1. Khóa đầu vào/phạm vi | Đã kiểm nhánh `Lam`, diff ban đầu chỉ có `.gitignore`; phân biệt 42 screening, 17 nền và 59 evidence; đối chiếu 5 cổng trên tập screening. |
| 2. Tổng hợp bằng chứng gap | Đã đối chiếu đủ 17 bài theo audit, giữ GV-13/P? và xét Guo/MioHint ngoài ma trận; có checkpoint nội dung trước sửa. Chưa xác nhận gap mạnh khớp RQ. |
| 3. Đồng bộ PRISMA | Đã giữ phễu 47−5=42 và bổ sung nhánh 17 nền; bộ evidence 59 không được ghi thành 59 INCLUDE. |
| 4. Đồng bộ rq-validation mục 1–3 | Đã cập nhật thống kê 59, phản chứng, 3 nghiên cứu gần đây và bảng 17 bài; có checkpoint nội dung. Bảng căn hàng còn mở, nhãn `extension` giữ theo xác nhận người phụ trách. |
| 5. Đồng bộ mục 4–6 | Đã ghi gap dự kiến của RQ đang giữ, phần đã có/chưa có bằng chứng, lợi ích, khả thi và 12 hạng mục checklist. Không đặt RQ thay thế hoặc tự chốt thông số thực nghiệm. |
| 6. Kiểm chứng và cập nhật tiến độ | Đã đối chiếu số đếm/PICO, SHA256, bảng Markdown, liên kết nội bộ và phạm vi thay đổi; chạy `git diff --check`. Các giới hạn nội dung ghi tại mục 3 dưới đây. |

## 2. Kết quả kiểm tra tài liệu

- Merge/map: **59 = 42 + 17**; P **1✓/28◐/29·/1?**, I **2✓/27◐/30·**, C **7✓/26◐/26·**, O **5✓/39◐/15·**; phân bố số ✓ **46/11/2** cho mức 0/1/2.
- 17 dòng PICO trong bản tổng hợp khớp JSON audit; **17/17 SHA256 PDF khớp**, **67/68 ô phân loại được**, GV-13/P? giữ nguyên. Không đọc lại toàn bộ hoặc tái chấm 42 bài cũ.
- Kiểm nội dung cột kết quả: **58/59** bài có kết quả định lượng ghi trong merge; GV-17 chỉ định tính. Giữ đủ **6 mục** của mẫu và đối chiếu **12 hạng mục** checklist cuối hướng dẫn.
- Bỏ các liên kết thiếu khỏi vai trò nguồn bằng chứng; ghi rõ `rq-validation-audit.md`, `rq-validation-source-check.csv`, `gap-ban-dau.txt` hiện không có trong workspace. Không tạo nguồn thay thế giả định.
- Phạm vi sửa: `rq-validation.md`, `prisma-team.md` và file tiến độ này. Bảo toàn `.gitignore`, rq-check cá nhân, hướng dẫn và audit đã hoàn tất. Không xóa file, commit hoặc push.

## 3. Việc còn mở sau đồng bộ

1. **Biện minh gap và căn hàng:** giữ RQ/`extension` theo hướng đã được người phụ trách làm rõ sau trao đổi với GV. GAP-T là gap dự kiến từ đối chiếu, chưa có đếm limitation trực tiếp để gọi là gap mạnh. Guo đạt 3/4 rộng nhưng khác nhiều điều kiện đầy đủ; nhóm/GV còn cần xem xét cách biện minh. Không đặt lại bài toán chọn RQ chỉ vì gap được ghi muộn.
2. **Lịch sử và thẻ RQ:** giữ nguyên câu gap cũ, ghi nhận bổ sung sau tổng hợp; chưa có bằng chứng ngày báo GV/cập nhật thẻ P. Mẫu hiện giữ **16 FastAPI + 15 NestJS RealWorld + 14 TodoApp**; chưa khóa snapshot/45 ID. Không bịa ngày hoặc chấp thuận hồi tố.
3. **Nguồn còn thiếu:** GV-13/P cần bằng chứng deployment/source của SUT được thử nếu muốn phân loại. Thống kê GAP-D **18/42, 10 cụm** chỉ kế thừa; chưa kiểm lại sổ quote/gộp tác giả, không đổi thành 18/59 hoặc coi RQ ba dịch vụ lấp GAP-D.
4. **Thiết kế và khả thi:** vẫn **0 ❌ / 6 ⚠️ / 1 ✅**, rủi ro cao; ✅ chỉ về nguồn ground truth. Còn B/miền random, dạng yêu cầu, precise/vague, assertions/oracle, mutant manifest và chính sách chạy; máy/người/giờ công, pilot và dự toán có ≥3 ngày dự phòng chưa chốt. Chưa chạy generator, benchmark, build hay thực nghiệm trong lượt này.

**Đã hoàn tất đồng bộ hai tài liệu theo đầu vào hiện có; chưa đánh dấu toàn bộ RBL-2 hoàn tất.** Việc tiếp theo là xử lý căn cứ/checklist còn mở và khóa thiết kế, không làm lại lượt audit 17 PDF đã xong. Quota chưa chạm ngưỡng còn ≤10% trong lượt đồng bộ nên chưa phát sinh checkpoint khẩn hoặc sử dụng reset.
