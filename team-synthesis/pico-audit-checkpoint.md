# Checkpoint — PICO 17 bài bổ sung

Cập nhật: **2026-10-20T15:43:52+07:00 (Asia/Saigon)**.

## Quota và yêu cầu người dùng

- **Đã chạm ngưỡng còn5%**: get_usage_limits báo cửa sổ5giờ dùng95%, còn5%; tuần dùng15%, còn85%.
- User yêu cầu lưu checkpoint tại ngưỡng này để khôi phục khi hết quota. Checkpoint này đã được ghi đúng lúc chạm ngưỡng.
- Công việc đang được giao: làm bước1 (kiểm PICO trực tiếp từ17PDF) và bước2 (hiệu chỉnh merge/map/rq-check), rồi báo cáo. **Hai bước đã hoàn tất ở phạm vi nguồn có sẵn;1ô được ghi chưa xác minh thay vì ép kết luận.**

## Đã hoàn tất

- Đọc phương pháp/thực nghiệm trực tiếp trong17PDF GV-01–GV-17; render và kiểm các bảng/figures cần thiết. Không chỉ kế thừa bảng trích xuất cũ.
- Có lý do và locator riêng cho68ô; **67ô phân loại được, P củaGV-13 còn?**.
- **4ô thay đổi trên3bài**: GV05P◐→· vàI·→◐; GV09P◐→·; GV13P◐→?.14bài khác giữ dấu.
- **GV04/12/14/16/17 vẫn····**, đã có chứng cứ riêng từngô. RESTOR KillRate là training reward trên response bodies; kết quả thực nghiệm F1/assertion/adoption. RandomCV củaHowFar không phải random request baseline. Crowdsourced rarity score đánh giá reports đầu vào, không generator fault yield.
- AGORA+I◐ được root chốt theo rubric rộng: domain/type request generators thật sự được cấu hình/chạy cho224inputs để thu corpus, không EP+BVA primary và khôngI✓. SATORI chỉ tái dùng corpus nên I·.
- Đồng bộ merge59/map59/rq-checkLâm25/nguồnLâm và teacher audit. Sửa metadata9095 build và pass existing tests;64crowdworkers; RESTOR Fig3/Fig4 ởPDF12.
- Đã kiểm221local links/heading anchors, cấu trúcMarkdown, IDs, thống kê, SHA256 của17PDF,42dòng merge cũ/điểm42map cũ, và git diff --check. QA nội dung độc lập cũng đạt.
- JSON status hiện là **synchronized**. Không commit/push.

## Tài liệu chính để tiếp tục

- [Báo cáo chi tiết17bài/68ô](pico-audit-17-papers.md): lý do từngô, locator, trang đã đọc, SHA256, bảng thay đổi và vấn đề chưa xác minh.
- [JSON kiểm chứng](pico-audit-17-papers.json):17records, old/new signs, confidence, pages, hash và kết quảverification. Đây là dữ liệu bền vững, không phụ thuộc ngữ cảnh chat hoặc ảnh tạm.
- [Evidence merge](evidence-table-merged.md), [map](rq-evidence-map.md), [rq-checkLâm](../lam/SLR/rq-check.md), [evidenceLâm](../lam/SLR/evidence-table.md), [teacher audit](../lam/SLR/teacher-papers-audit.md).
- Tổng P nhóm: **1✓/28◐/29·/1?**; I **2✓/27◐/30·**; C **7✓/26◐/26·**; O **5✓/39◐/15·**. Histogram số✓ vẫn46×0,11×1,2×2; ? không được gộp vào·.
- Rq-checkLâm25: P1✓/6◐/17·/1?; I0✓/12◐/13·; C2✓/7◐/16·; O4✓/13◐/8·.
- Mẫu hiện giữ16FastAPI+15NestJSRealWorld+14TodoApp; nhãn nhóm`extension`.

## Việc còn mở thực sự

1. **GV-13/P?**: PDF xác nhận39RESTendpoints/7services nhưng chưa xác minh tested GitLab instance/deployment/source đủ điều kiện SUT chạy/sửa/gieo mutant được. Không suy APIproprietary từ việc thiếu thông tin. Cần artifact/deployment/source-version evidence của chính evaluation để chọn◐hay·. Hiện chạm đã xác nhận2/4, ghi riêng`+?P`.
2. **Chưa làm lại rq-validation.** Khi user cho triển khai bước sau: dùng report/JSON mới làm đầu vào, rà cả nguồn ngoài59 (ví dụGuo2024 đã ghi trong hồ sơ), không suy novelty chỉ từ không có≥3✓ trong59.
3. Chưa khóa benchmark commit/45requirementIDs, B, uniformdomains, requirementtypes, precise/vague, assertions/oracle chung, mutantmanifest, reset/retry/flakiness và runtimepilot. Chưa chạy artifact/benchmark hoặc chứng minh hiệu quảEP+BVA.
4. PRISMA và rq-validation/status/criteria giữ nguyên trong đợt này. Không sửa rq-check của thành viên khác.

## Lưu ý bảo toàn workspace

Git đã có PDF renames/untracked và thay đổi tài liệu từ trước. **Không reset/checkout hoặc xóa các thay đổi đó.** Các file mới của đợt audit là báo cáoMarkdown, JSON, checkpoint này; ảnh/text/review trung gian còn ở`tmp/pdfs/pico-review-2026-10-20/` (manifest/baseline-hashes/review-GV-XX.json). Không cần đọc lại17PDF nếu chỉ tiếp tục từ checkpoint; dùng JSON và xác nhận SHA256 nếu PDF đã đổi.

## Khi tiếp tục sau hết quota

Đọc checkpoint này rồi báo cáoMD/JSON; xác nhận user muốn xử lý P? hay bắt đầu rq-validation. Không tự làm lại các bước1–2 đã hoàn tất. Yêu cầu checkpoint còn5% tiếp tục được giữ ở các lượt công việc sau; kiểm usage tại mốc công việc và ghi lại tiến độ trước khi rời phiên.
