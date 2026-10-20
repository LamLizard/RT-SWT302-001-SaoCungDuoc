# Trạng thái kiểm chứng RQ — FA26-EXT-12

**Cập nhật:** 20/10/2026. [Bản tổng hợp](rq-validation.md) · [Nguồn kiểm chứng](rq-validation-audit.md).

## 1. Những thay đổi trong lần chỉnh này

- Sắp xếp `rq-validation.md` theo **6 mục của mẫu RBL-2**, bỏ phần lịch sử và chi tiết triển khai lặp lại.
- Bổ sung bảng **Gap — Phát biểu gap — RQ lấp gap — Khác RQ ban đầu**, đặt GAP-T cạnh GAP-M và ghi rõ phần chưa đủ căn cứ.
- Chỉ chỉnh hai file tổng hợp `rq-validation.md` và file trạng thái này; giữ nguyên các file cá nhân, review protocol và H0/H1 so với đầu lần chỉnh.

## 2. Kết luận trọng tâm

- **Bước 1 đã xác nhận; nhãn `extension` đã được GV bổ sung.** Bước 2 còn vấn đề biện minh gap; Bước 3 đã lập bảng nhưng chưa chốt khả thi.
- **GAP-T:** giả định của nhóm, chưa có limitation tác giả tương ứng. **GAP-M:** bằng chứng P12 còn yếu, chưa đủ để lập RQ thay thế phù hợp. **GAP-D:** hạn chế lặp lại ở tối thiểu 18/42 paper, 10 cụm tác giả; RQ hiện tại không giải quyết việc thiếu đa dạng dịch vụ.
- **Khả thi: 0 ❌ / 6 ⚠️ / 1 ✅**, rủi ro cao; đã có kế hoạch xử lý, chưa có bằng chứng chạy thử của nhóm. Chưa đánh dấu RBL-2 hoàn tất.

## 3. Các vấn đề nhóm cần cô hỗ trợ

1. **Gap ban đầu ghi muộn:** nhóm bổ sung câu gap ngày 20/10 sau khi tổng hợp paper, chưa đáp ứng yêu cầu ghi trước khi đếm. Xin cô hướng dẫn cách ghi nhận sai lệch này trong hồ sơ.
2. **Chưa chốt cách biện minh GAP-T/GAP-M:** GAP-T phù hợp RQ nhưng chưa có limitation tác giả nêu trực tiếp; GAP-M hiện chỉ có hạn chế cụ thể của P12 và không tương ứng ngay với phép so EP+BVA–random. Xin cô góp ý nên giữ GAP-T như giả định của nhóm hay cần điều chỉnh hướng/RQ.
3. **Paper gần nhất và phần mở rộng:** Guo đạt 3/4 theo rubric rộng, nhưng phương pháp sinh test, random baseline và oracle vẫn khác RQ. Xin cô góp ý paper làm căn cứ chính và cách trình bày đóng góp; nhóm giữ nhãn `extension` đã được cô bổ sung.
4. **Số đếm GAP-D còn ở mức chủ đề:** nhiều paper cùng nêu giới hạn phạm vi dịch vụ nhưng không cùng một thiếu hụt dữ liệu cụ thể. RQ chỉ có 3 dịch vụ nên không lấp GAP-D; xin cô góp ý cách trình bày giới hạn này khi chọn gap chính.
5. **Phân bổ mẫu thay đổi:** TodoApp chỉ có 14 yêu cầu; hồ sơ đề xuất **16 FastAPI + 15 RealWorld + 14 TodoApp**, thay 15/dịch vụ. Xin cô xác nhận cách cập nhật P/thẻ RQ. Nhóm còn phải khóa phiên bản để xử lý chênh lệch README 103/paper 106 yêu cầu.
6. **Chưa đủ số liệu khả thi:** chưa chốt B, miền uniform random, dạng yêu cầu, precise/vague và runtime; chưa có log kiểm generator/oracle. Xin cô góp ý mức thu hẹp chấp nhận được nếu pilot cho thấy thiết kế 45 yêu cầu × 2 kỹ thuật × 10 lượt vượt nguồn lực/thời gian.

**Nhóm cần tự hoàn thiện:** danh sách 45 ID/mutant, đặc tả hai kỹ thuật và chính sách chạy, máy/người phụ trách, pilot và dự toán có ≥3 ngày dự phòng. Không dùng việc chưa chạy toàn bộ thực nghiệm làm tiêu chí duy nhất để kết luận RBL-2 chưa xong.
