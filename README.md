# Prompt hướng dẫn EP+BVA vs single-step trên RESTestBench

**Topic:** RT-SWT302-001, RQ: FA26-EXT-12 · SWT302 · SaoCungDuoc, FA26/2026
**Thành viên:** Lam (PL), Khoi (DG), Tung (MS), T.Duy (LR), K.Duy (RW)
**Giảng viên:** L.T.Q.Chi

**RQ chính:** Trong điều kiện sinh single-step với cùng mô hình, cấu hình và ngân sách kiểm thử được quy định trước, việc bổ sung hướng dẫn EP+BVA vào prompt gốc ảnh hưởng như thế nào đến MS_φ trên các yêu cầu vague của RESTestBench tại phiên bản đóng băng?

**Cập nhật 23/10/2026:** đã có golden và pilot thực; pilot đóng qua đối soát offline có công bố, 24/24 evaluation resolved, C 19/25 (76%), I 18/25 (72%). [Hồ sơ gửi giảng viên](.local/pilot-preparation/pilot-reconciliation-20261023-01/HO-SO-GUI-GIANG-VIEN.md) và [provenance](.local/pilot-preparation/pilot-reconciliation-20261023-01/provenance.json). Chưa gửi cô, chưa chốt RQ/freeze/main; một pilot run chưa cho phép kết luận tác động.

- Nguồn bằng chứng: **60 = 42 INCLUDE lịch sử + 18 nguồn nền**; GV-18 là Rodríguez/PDF60. PRISMA final giữ 42, không tái chấm 59 điểm nền.
- Commit `4decc1e36ea3dd41b64ce3e3ac6a85bc72df36ae`, **106 vague/228 mutant**. Golden: 106 original pass, 227 assertion kill, 1 mutant compile lỗi (NestJS 5/0), 106 restored pass; giữ mẫu số 228. Bước 1 hoàn thành với lỗi đã ghi nhận, không chặn bước 2; không nhận mọi mutant runtime-valid.
- Model người dùng chọn: **DeepSeek-V4.1-Flash-1017**, **DeepSeek API chính thức** (`deepseek-flash`, alias cần kiểm phiên bản lúc chạy).
- Ngân sách tổng: **3 USD**, bao gồm pilot/main/retry. Pilot có 24 model attempt, ledger bound USD0.0655344, ước tính off-peak từ usage USD0.022192608; chưa xác nhận hóa đơn. R=3/636 main slot còn là phương án review. Hai người chấm/annotation, căn cứ R/độ bất định, xác nhận cô và freeze/revalidation mã mới trước main còn pending.

## Thứ tự review

1. [RQ, đóng góp và bảng nghiên cứu gần nhất](team-synthesis/rq-validation.md) — mục 1.
2. [Thiết kế thực nghiệm, ngân sách và điều kiện còn thiếu](team-synthesis/experiment-design.md) — mục 2; [config](experiments/study-config.json), [manifest](experiments/benchmark-manifest.json), [C](experiments/prompts/C.txt), [I](experiments/prompts/I.txt), [lịch dự kiến](experiments/run-schedule.csv).
3. [Pilot đối soát](.local/pilot-preparation/pilot-reconciliation-20261023-01/REPORT.md), [hồ sơ](.local/pilot-preparation/pilot-reconciliation-20261023-01/HO-SO-GUI-GIANG-VIEN.md) và [email nháp](.local/pilot-preparation/pilot-reconciliation-20261023-01/EMAIL-NHAP.md) để người dùng review/gửi; main cần quyết định riêng và final-freeze.

[Protocol tài liệu](team-synthesis/review-protocol.md) phân biệt lượt bổ sung và screening lịch sử. [Notes](notes.md) giữ quyết định hiện hành và lịch sử. Runner/guard đã có; smoke/preflight cũ chỉ xác minh mã trước amendment, cần kiểm lại theo hash nguồn mới trước live run tương lai. Prompt/config/manifest/lịch giữ nguyên baseline review.

## Tiến độ môn học

- [ ] RBL-1: nghiệm thu tìm paper
- [ ] RBL-2 + RBL-3: chốt kiểm chứng RQ/Proposal với giảng viên
- [ ] RBL-4: môi trường/golden, pilot và đánh giá chính
- [ ] RBL-5: phân tích, báo cáo và trình bày
