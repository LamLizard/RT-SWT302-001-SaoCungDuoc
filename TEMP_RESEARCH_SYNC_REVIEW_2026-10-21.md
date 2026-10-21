# Báo cáo tạm — đồng bộ tài liệu nghiên cứu ngày 21/10/2026

Tài liệu để người dùng đọc lại các sửa đổi, có thể xóa độc lập. Đây không phải kết quả thí nghiệm hoặc xác nhận phê duyệt của giảng viên.

## 1. Phạm vi và trạng thái

- Bắt đầu trên nhánh **Lam**, HEAD `6658a63de7250dd7a41bbd6d140b3cdb3f9f5f51`, working tree sạch. Không nhận các đề xuất từ phiên trước thành việc đã làm.
- Đã sửa **7 tài liệu hiện hữu**: README, notes, bốn tài liệu tổng hợp và nhật ký Lâm. Nhật ký chỉ thêm mục mới để tuân thủ quy định ghi thay đổi trong review-protocol; không phải báo cáo phụ.
- Giữ nguyên RQ mới, H0/H1, nhãn nhóm `extension`, **106 vague / 228 mutant**, và **42 INCLUDE + 17 bài nền = 59 evidence**.
- Theo lựa chọn người dùng trong phiên này: **giữ điểm nền, chỉ ghi rõ chỗ chưa đồng nhất**; không tái chấm toàn bộ 59 bài theo RQ mới.
- Chỉ dùng agent chính. Không tạo mã thí nghiệm, cài package, chạy Docker/golden tests/LLM/pilot; không stage, commit hoặc push.

## 2. Đã sửa gì, vì sao và ở đâu sau sửa

Số dòng dưới đây tính từ 1 trên nội dung sau sửa trong đợt này; có thể thay đổi nếu tài liệu tiếp tục được chỉnh.

| Điểm | Nội dung và lý do sửa | File và vị trí sau sửa |
|---|---|---|
| A — bảng căn hàng | I phía GV-02 mô tả **refinement loop**, C là single-step; nhóm kế thừa nhánh single-step để bổ sung phép so guided EP+BVA. Tránh bảng khiến paper giống so single-step với chính nó. | [rq-validation.md](team-synthesis/rq-validation.md#31-paper-gần-nhất-và-bảng-căn-hàng), dòng **74–85**, đặc biệt **81**. |
| B — số lượt hai arm | Sửa full thành **636 lượt sinh test**, **636 lượt kiểm valid**, **1.368 lượt mutant = 684/arm**, trước setup/reset/retry. Fail valid có thể skip mutant; retry có thể tăng lượt. Đây là kế hoạch, chưa phải runtime đã đo. | [rq-validation.md](team-synthesis/rq-validation.md#4-khả-thi-của-gap-đang-cân-nhắc), dòng **97**; [notes.md](notes.md), dòng **6**. |
| C — ba run và phụ thuộc | Bỏ cách viết bootstrap/McNemar như kế hoạch đã chốt. Nêu khóa service/requirement/mutant/arm/run, ghép I/C theo requirement, giữ ba run và cụm mutant dùng chung test. Bootstrap cụm chỉ là phương án; không mặc định 228 mutant hoặc 684 mutant-run độc lập. | [rq-validation.md](team-synthesis/rq-validation.md#4-khả-thi-của-gap-đang-cân-nhắc), dòng **113–115**, việc tiếp theo dòng **168**; [review-protocol.md](team-synthesis/review-protocol.md), dòng **12**; [notes.md](notes.md), dòng **8**. |
| D — MS_φ và assertions | Bổ sung pass-valid/fail-mutant; test fail valid có điểm 0, không bỏ mẫu số. Viết công thức từng run, trung bình mô tả ba run, mẫu số dịch vụ **141/65/22**. Phân biệt trung bình với union kill và trung bình không trọng số theo requirement. Hai arm dùng cùng hướng dẫn assertion; model vẫn sinh assertions; golden tests không làm đáp án cho LLM. | [rq-validation.md](team-synthesis/rq-validation.md#11-định-nghĩa-outcome-và-tổng-hợp-ba-run), dòng **18**, **25–35**, **98**. |
| E — ma trận và tổng hợp | Giữ mọi nhãn P/I/C/O và số ✓ của 59 dòng map. Ghi rõ C✓ của GV-02 dựa vào single-step, khác C random của rubric nền; I◐ của TD-0015 cần quyết định sau. Đồng bộ bản sao TD-0015 trong merge **1✓ → 0✓** theo map, không coi là tái chấm. Sửa chạm của TD-0015 **0/4 → 2/4** do P◐ và I◐. Sửa tổng I/C theo số đếm thực tế. | [rq-evidence-map.md](team-synthesis/rq-evidence-map.md#1-quy-tắc-chấm-ma-trận-nền-giữ-điểm-đã-ghi), dòng **7–30**, tổng dòng **153**; [evidence-table-merged.md](team-synthesis/evidence-table-merged.md), dòng **7**, **56**, **84–85**; [rq-validation.md](team-synthesis/rq-validation.md#22-đối-chiếu-pico-cho-rq-hiện-hành), dòng **58–68**. |
| F — điểm, chạm, ưu tiên | Giữ TD-0002 **2✓ (I,O), chạm 3/4**. Xếp cả ma trận và danh sách ưu tiên theo ✓ trước/chạm sau: **GV-02 trước TD-0002**; các dòng 1✓ cũng đứng trước TD-0015 0✓. Bỏ nhận định TD-0002 “cao nhất toàn bảng gộp”. | [rq-evidence-map.md](team-synthesis/rq-evidence-map.md), ma trận bắt đầu dòng **49**, ưu tiên bắt đầu dòng **120**; [evidence-table-merged.md](team-synthesis/evidence-table-merged.md), dòng **55**, **84**. |
| G — P của GV-02 | Viết rõ 106 requirement **mỗi requirement có precise và vague**, paper đánh giá cả hai; điều kiện vague trùng P nhóm chọn. Không gọi phát biểu vague trước đây là sai dữ liệu, không hàm ý toàn paper chỉ nghiên cứu vague. | [rq-validation.md](team-synthesis/rq-validation.md), dòng **62**, **80**; [rq-evidence-map.md](team-synthesis/rq-evidence-map.md), dòng **49**, **120**; [evidence-table-merged.md](team-synthesis/evidence-table-merged.md), dòng **85**. |
| H — hiện hành và lịch sử | Đổi tiêu đề README theo RQ prompt mới; thêm phần hiện hành trong notes. Đánh dấu mẫu 45, không dùng LLM và kế hoạch 10 lượt/Wilcoxon–Holm là lịch sử. Protocol giữ nguyên chuỗi, tiêu chí, mốc cũ dưới nhãn kế thừa; không bịa query, screening, PRISMA hoặc GV duyệt mới. B/miền uniform random không còn là tham số chờ khóa của thiết kế hiện hành. | [README.md](README.md), dòng **1–10**; [notes.md](notes.md), dòng **3–26**, nhật ký dòng **32**; [review-protocol.md](team-synthesis/review-protocol.md), dòng **23–36**, **57**; [rq-evidence-map.md](team-synthesis/rq-evidence-map.md), dòng **154**. |
| I — 15 mutant và suy luận | Gắn nguồn **email GV**, chưa có ID/phân loại độc lập. Giữ 15/228 = 6,58 điểm phần trăm nhưng chỉ là giới hạn trong giả định hẹp về input và 213 mutant còn lại giữ nguyên; không phải trần của prompt có thể đổi setup/assertions. Giữ p-value đúng và nêu giả định 15 cặp discordant độc lập; không dùng làm power hay suy tương đương/vô ích. | [rq-validation.md](team-synthesis/rq-validation.md), dòng **117–119**, diễn giải kết quả dòng **155**. |
| Giới hạn novelty | Phân biệt mutation score Stryker.NET của TD-0002 với MS_φ. Không dùng điểm nền để khẳng định toàn bộ 59 bài đã được chấm theo RQ mới hoặc chứng minh novelty; thu hẹp câu gap theo phạm vi bằng chứng đã rà. | [rq-validation.md](team-synthesis/rq-validation.md), dòng **63–68**, **85**, **127–151**, **159**; [rq-evidence-map.md](team-synthesis/rq-evidence-map.md), dòng **112**; [evidence-table-merged.md](team-synthesis/evidence-table-merged.md), dòng **55**, **85**. |
| Truy vết thay đổi | Chỉ bổ sung một mục ngày 21/10, giữ nguyên các mục nhật ký trước đó. Phân biệt đồng bộ tài liệu với chạy query/thí nghiệm. | [lam/SLR/search-log.md](lam/SLR/search-log.md), mục **10**, dòng **103–110**; [review-protocol.md](team-synthesis/review-protocol.md), dòng **3**. |

## 3. Đã kiểm tra thực tế

- Đọc AGENTS.md và skill scientific-writing; không sinh scaffold, manifest hoặc checklist phụ. Rà diff nội dung các file đã sửa, đối soát thay đổi từng dòng dữ liệu theo mã paper để không nhầm số thứ hạng với số dòng merge.
- Đọc lại [paper RESTestBench](https://arxiv.org/html/2604.25862), các phần §3.2–4.2/Table 3, để kiểm precise/vague, single-step/refinement, công thức và ba run.
- Đọc [`src/evaluator.py`](https://github.com/casablancahotelsoftware/RESTestBench/blob/4decc1e36ea3dd41b64ce3e3ac6a85bc72df36ae/src/evaluator.py) tại snapshot `4decc1e36ea3dd41b64ce3e3ac6a85bc72df36ae`: `evaluate_test` có validity gate và xóa kills/đặt score 0 khi fail valid; không kết luận code metric đang sai. Đọc lại prompt single-step và phần sinh test, xác nhận yêu cầu assertions cụ thể và `INTERACTIVE=False`.
- Đọc lại các phần liên quan của `Paper-source/39-TD-0002.pdf`: hướng dẫn boundary testing/equivalence classes, TSL và mutation evaluation Stryker.NET. Đọc abstract gốc [Durkalski et al. (2003)](https://pubmed.ncbi.nlm.nih.gov/12872299/) về matched-pair có cụm; không nhận là đã đọc toàn văn bài phương pháp.
- Dùng kiểm tra Python trong bộ nhớ, không lưu script/file kiểm tra: **59 ID duy nhất** khớp map–merge; mọi nhãn P/I/C/O và số ✓ trong map khớp HEAD trước sửa; số ✓ và chạm của **59/59** dòng merge khớp map; tập **27 bài** ưu tiên giữ nguyên và được sắp đúng ✓/chạm. Cột của các bảng Markdown nhất quán.
- Đếm lại từ chính 59 dòng, mỗi yếu tố tổng 59:

| Yếu tố | ✓ | ◐ | · | ? |
|---|---:|---:|---:|---:|
| P | 1 | 28 | 29 | 1 |
| I | 1 | 28 | 30 | 0 |
| C | 8 | 26 | 25 | 0 |
| O | 5 | 39 | 15 | 0 |

- Kiểm phép tính: 63 + 29 + 14 = 106; 141 + 65 + 22 = 228; 106 × 2 × 3 = 636; 228 × 2 × 3 = 1.368; 228 × 3 = 684. Tính lại 15/228 × 100 = 6,578947…; exact binomial hai phía cho 12/3 = **0,03515625**, 10/5 = **0,3017578125**. Đây chỉ là kiểm số học minh họa, không phải phân tích dữ liệu thí nghiệm.
- So nguyên văn RQ/H0/H1 với HEAD trong ba tài liệu tổng hợp liên quan: không đổi. Kiểm **69 liên kết Markdown nội bộ** của 7 tài liệu đã sửa, gồm đường dẫn và các anchor được dùng: không thấy lỗi. Không nhận là đã health-check mọi URL ngoài repo.
- `git diff --check` không báo lỗi whitespace; Git index trống thay đổi. Phần kiểm cuối xác nhận chỉ 7 file hiện hữu đổi và đúng một file mới là báo cáo tạm này; không có tài liệu khác nhắc tên/link báo cáo. Không sửa .gitignore, CSV, PDF, AGENTS.md hoặc mã thực nghiệm.

## 4. Còn chưa xác minh hoặc chưa chốt

1. **Rubric:** các nhãn nền còn trộn cách chấm; đặc biệt C của GV-02 và I của TD-0015 vẫn để người dùng/nhóm quyết định. Đã đồng bộ bản sao và ghi rõ bất nhất, chưa giải quyết bằng tái chấm. O✓ nền của TD-0002 không xác nhận MS_φ.
2. **Bằng chứng:** chưa tái thẩm định toàn văn cả 59 bài theo RQ mới, chưa kiểm lại toàn bộ trích dẫn/hạn chế hoặc các cổng P1–P5. Các số kế thừa như 18/42 paper, 10 cụm hạn chế chưa được audit lại. Chưa đọc lại toàn văn Reid (1997); phản hồi về Reid không phải một kết quả thực nghiệm mới của nhóm.
3. **Dataset:** kiểm kê đủ 106 JSON, requirement_vague không rỗng và 228 mutant là kết quả từ lượt rà soát trước do người dùng chuyển context, được đối chiếu với Table 3; đợt này không tải/đếm lại 106 JSON. Snapshot tham chiếu chưa thay cho khóa artifact, danh sách ID và môi trường chạy của nhóm.
4. **15 mutant:** chưa có danh sách từ GV, chưa biết phân bố dịch vụ/requirement và chưa phân loại độc lập. Không nhận đây là danh sách nhóm đã kiểm hoặc trần tác động chung của prompt.
5. **Thực nghiệm:** prompt I, model/version/cấu hình, môi trường, phân công, lịch, lỗi/retry và pilot chưa khóa/chưa thực hiện. Công thức trung bình ba run mới làm rõ báo cáo mô tả; estimand, ghép/tổng hợp run cho suy luận, resampling, CI, phân tầng service, multiple comparisons và phép kiểm vẫn chưa chốt.
6. **Tìm kiếm và phê duyệt:** protocol/IC-EC cho hướng prompt mới chưa khóa; không có lượt search/screening hoặc PRISMA mới trong đợt này. Chưa xác minh thẻ đăng ký hoặc GV duyệt. Các tài liệu cá nhân/lịch sử khác được giữ nguyên, không tự chuẩn hóa thành quyết định hiện hành.

## 5. Tính độc lập của báo cáo tạm

Báo cáo chưa được stage/commit/push. Không có tên/link của báo cáo trong README, notes, tài liệu tổng hợp, nhật ký hoặc danh mục tài liệu; không có khai báo mới trong .gitignore. Có thể xóa riêng file này mà không làm hỏng liên kết từ các tài liệu còn lại. Báo cáo không tự quyết định việc đưa file vào Git sau này.
