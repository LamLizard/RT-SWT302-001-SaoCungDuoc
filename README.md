# Prompt hướng dẫn EP+BVA vs single-step trên RESTestBench

**Topic:** RT-SWT302-001, RQ: FA26-EXT-12 · SWT302 · SaoCungDuoc, FA26/2026
**Thành viên:** Lam (PL), Khoi (DG), Tung (MS), T.Duy (LR), K.Duy (RW)
**Giảng viên:** L.T.Q.Chi

**RQ chính:** Trong điều kiện sinh single-step với cùng mô hình, cấu hình và ngân sách kiểm thử được quy định trước, việc bổ sung hướng dẫn EP+BVA vào prompt gốc ảnh hưởng như thế nào đến MS_φ trên các yêu cầu vague của RESTestBench tại phiên bản đóng băng?

**Cập nhật 22/10/2026:** hoàn thiện bản tài liệu và thiết kế mục 1–2 để nhóm review theo mail cô. Chưa làm bước 3, chưa golden tests/pilot/LLM, chưa được cô chốt RQ.

- Nguồn bằng chứng: **60 = 42 INCLUDE lịch sử + 18 nguồn nền**; GV-18 là Rodríguez/PDF60. PRISMA final giữ 42, không tái chấm 59 điểm nền.
- Dữ liệu kiểm tĩnh: commit `4decc1e36ea3dd41b64ce3e3ac6a85bc72df36ae`, **106 vague/228 mutant**. Chưa xác nhận chạy được trên máy nhóm.
- Model người dùng chọn: **DeepSeek-V4.1-Flash-1017**, **DeepSeek API chính thức** (`deepseek-flash`, alias cần kiểm phiên bản lúc chạy).
- Ngân sách tổng: **3 USD**, bao gồm pilot/main/retry. R=3 là kế hoạch review: 24 slot pilot + 636 slot main; chưa chạy. Dự toán off-peak 2.395008 USD với giả định 16k input/2048 output mỗi call, trước retry; chưa có token/chi phí thật.

## Thứ tự review

1. [RQ, đóng góp và bảng nghiên cứu gần nhất](team-synthesis/rq-validation.md) — mục 1.
2. [Thiết kế thực nghiệm, ngân sách và điều kiện còn thiếu](team-synthesis/experiment-design.md) — mục 2; [config](experiments/study-config.json), [manifest](experiments/benchmark-manifest.json), [C](experiments/prompts/C.txt), [I](experiments/prompts/I.txt), [lịch dự kiến](experiments/run-schedule.csv).
3. Sau khi người dùng review mới quyết định làm bước 3: môi trường/golden tests. Pilot, hồ sơ gửi cô và đánh giá chính là các bước sau; prompt/config chỉ final-freeze trước main.

[Protocol tài liệu](team-synthesis/review-protocol.md) phân biệt lượt bổ sung và screening lịch sử. [Notes](notes.md) giữ quyết định hiện hành và lịch sử. Không có runner, hard-budget enforcement hoặc kết quả thực nghiệm trong bản thiết kế này.

## Tiến độ môn học

- [ ] RBL-1: nghiệm thu tìm paper
- [ ] RBL-2 + RBL-3: chốt kiểm chứng RQ/Proposal với giảng viên
- [ ] RBL-4: môi trường/golden, pilot và đánh giá chính
- [ ] RBL-5: phân tích, báo cáo và trình bày
