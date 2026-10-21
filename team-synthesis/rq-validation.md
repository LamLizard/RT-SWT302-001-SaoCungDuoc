# Kiểm chứng RQ — FA26-EXT-12 · SaoCungDuoc

Tài liệu giữ 6 mục của [mẫu RBL-2](RBL-2-Kiem-chung-RQ-full.md). Đầu vào: [merge 59 bài](evidence-table-merged.md), [map PICO](rq-evidence-map.md) và các PDF gốc được dẫn tại từng đối chiếu. Bộ evidence gồm **42 bài INCLUDE qua screening + 17 bài nền GV-01–GV-17 = 59 bài**; 17 bài nền không cộng vào PRISMA final.

## 1. RQ + PICO

**RQ nhóm:** Trên 106 yêu cầu bản vague của RESTestBench, prompt có hướng dẫn kỹ thuật EP+BVA và prompt single-step gốc của benchmark khác nhau thế nào về **MS_φ**, khi dùng cùng một mô hình ngôn ngữ và cùng temperature?

**H0:** Không có khác biệt về MS_φ giữa prompt có hướng dẫn EP+BVA và prompt single-step gốc, với cùng mô hình, cùng temperature và cùng 106 yêu cầu.

**H1:** Có khác biệt về MS_φ giữa hai prompt dưới cùng điều kiện.

| Yếu tố | Nội dung |
|---|---|
| **P** | **106 yêu cầu bản vague** của RESTestBench: 63 FastAPI + 29 NestJS RealWorld + 14 TodoApp. |
| **I** | Prompt yêu cầu LLM phân hoạch tương đương và chọn giá trị biên từ requirement + OpenAPI schema trước khi viết một test. |
| **C** | Prompt single-step gốc của RESTestBench, không có bước EP/BVA. |
| **O** | **MS_φ** = số mutant bị giết / **228 mutant** của benchmark; báo cáo tổng và theo từng dịch vụ. |
| **S** | Cùng một model, cùng temperature, **3 lần chạy độc lập**; so sánh paired theo requirement. |

**Điều kiện dùng chung:** mỗi requirement sinh **một test**, `INTERACTIVE=False` (không gọi SUT khi sinh), cùng model/temperature/max token, cùng phần hướng dẫn assertion gốc; chỉ khác phần hướng dẫn EP/BVA. Dùng bản vague, không trộn precise. Không đổi O hoặc cách tính MS_φ sau khi xem kết quả.

**Dữ liệu:** `data/requirements/` có đúng **106 file** (63/29/14), tất cả có `requirement_vague`; tổng **228 mutant** (141/65/22 theo dịch vụ). README ghi 26 NestJS/tổng 103 là bảng cũ; paper GV-02 và dữ liệu ghi **106/228** — dùng dữ liệu/paper, không dùng 103.

## 2. Bằng chứng làm nền (N = 59 paper evidence)

### 2.1. Phạm vi đầu vào và các cổng

| Phạm vi | Số bài | Cách sử dụng |
|---|---:|---|
| INCLUDE qua screening của các nguồn, sau khử trùng | **42** | Merge #1–#42; giữ số liệu và quyết định IC/EC theo [PRISMA](prisma-team.md). |
| Bài nền do leader bổ sung | **17** | GV-01–GV-17, merge #43–#59; đọc toàn văn phần liên quan và audit PICO, không mặc nhiên INCLUDE theo IC/EC. |
| Bộ evidence của merge/map | **59 = 42 + 17** | 0 bài trùng giữa hai tập. |
| Phản chứng ngoài ma trận | Không cộng vào 59 | Chỉ dùng để kiểm tra thêm, không đổi mẫu số. |

| Cổng | Kết quả |
|---|---|
| P1 — ≥12 INCLUDE | **Đạt: 42 ≥ 12.** 17 bài nền không dùng thay số INCLUDE. |
| P2 — ≥90% có Tool/LLM | **Đạt: 42/42 = 100%.** |
| P3 — ≥50% có kết quả số | **Đạt: 42/42 có số trong bảng**; 58/59 evidence có kết quả định lượng, GV-17 chỉ định tính. |
| P4 — ≥50% có hạn chế | **Đạt: 42/42 có dữ liệu hạn chế**; 59/59 có nội dung hạn chế nhưng phải tách AUTHOR_STATED khỏi REVIEWER_INFERRED. |
| P5 — metric cụ thể | **Đạt ở mức bảng: 42/42 ghi metric**; 58/59 evidence có metric thực nghiệm mô tả được. |

### 2.2. Đối chiếu PICO cho RQ hiện hành

Bảng đầy đủ 59 dòng nằm ở [evidence table](evidence-table-merged.md); dưới đây là các paper sát RQ nhất. Không ghép P/I/C/O của nhiều paper để tạo một phản chứng.

| Paper | P | I | C | O | ✓ | Kết luận |
|---|---|---|---|---|---|---|
| **GV-02 / RESTestBench** (EASE 2026) | ✓ | · | ✓ | ✓ | **3/4** | Dùng đúng 106 yêu cầu vague; có prompt single-step làm baseline và MS_φ; **không có prompt hướng dẫn EP/BVA**. |
| **TD-0002** — Combining TSL and LLM to Automate REST API Testing (2025) | ◐ | ✓ | · | ✓ | **2/4** | Có EP/BVA trong prompt và mutation score; 6 dự án REST, không phải RESTestBench; không có baseline single-step của paper. |
| **TD-0015** — Orchestration architecture of AI agents for automated API testing (2026) | ◐ | ◐ | · | · | **0/4** | Module G sinh EP+BVA nhưng không phải prompt-guided trên RESTestBench; outcome là coverage, không phải MS_φ. |

**Kết luận trong 59:** GV-02 đạt **3/4** theo RQ hiện hành; TD-0002 đạt 2/4; TD-0015 đạt 0/4; **không có paper nào khác đạt ≥2/4** cho đúng P/I/C/O này. Các paper còn lại là nền về REST testing, mutation, oracle hoặc LLM generation, không phải phản chứng trực tiếp.

**Quy ước:** ✓ = đạt rubric rộng của map; ◐ = gần; · = không đáp ứng. `P✓` là dùng RESTestBench; `C✓` là có prompt single-step làm baseline; `O✓` là có MS_φ. Không suy nhãn hoặc ưu thế thực nghiệm chỉ từ tổng số ✓.

## 3. Phản chứng và nhãn

### 3.1. Paper gần nhất và bảng căn hàng

**Nhãn nhóm: `extension`.**

Paper gần nhất là **GV-02/RESTestBench**, đạt **3/4** so với RQ hiện hành:

| Yếu tố | GV-02 | RQ nhóm | Giống/khác | Căn cứ |
|---|---|---|---|---|
| **P** | 106 yêu cầu RESTestBench, có bản vague | 106 yêu cầu bản vague | **Giống** | GV-02 §3–4/PDF3–8; dữ liệu `data/requirements` có đủ 106 vague. |
| **I** | Prompt single-step, không hướng dẫn EP/BVA | Prompt có hướng dẫn EP+BVA | **Khác** | GV-02 §4/PDF6–8 dùng single-step/refinement; không có bước phân hoạch tương đương/boundary. |
| **C** | Prompt single-step là baseline của paper | Prompt single-step gốc | **Giống** | GV-02 §4/PDF6–8; đây là đối chứng nguyên văn của RQ. |
| **O** | MS_φ trên 228 mutant | MS_φ trên 228 mutant | **Giống** | GV-02 §3.4/PDF5–6 định nghĩa MS_φ = killed / 228; evaluator của repo dùng cùng công thức. |

Vì **P, C, O trùng** và chỉ **I khác**, đây là một **extension một yếu tố**, không phải replication. Trong 59 không có paper 4/4; TD-0002 (2/4) và TD-0015 (0/4) là các mốc tham chiếu, không đổi nhãn.

**Đóng góp dự kiến:** bổ sung bằng chứng thực nghiệm về việc **prompt-guided EP/BVA** có cải thiện MS_φ so với prompt single-step gốc hay không; không đề xuất thuật toán EP/BVA mới, không tuyên bố mutation testing cho REST chưa tồn tại. Kết quả có thể dương, âm hoặc không khác biệt; cả ba đều là kết quả hợp lệ.

## 4. Khả thi của gap đang cân nhắc

Chỉ đánh giá **GAP-T — prompt-guided EP/BVA + RQ tại §1**. Các số dưới đây là ước tính từ benchmark và repo, **chưa phải kết quả pilot**.

| Tiêu chí | Căn cứ hiện có | Chấm | Việc cần xử lý |
|---|---|---|---|
| Dataset | 106 requirement vague/228 mutant đã kiểm; dùng commit benchmark và `data/requirements`, không dùng README 103. | ✅ | Khóa commit, danh sách 106 ID và manifest mutant trước khi chạy. |
| API/Tool | Cần Docker cho 3 service và một API key/model cố định; repo có `single_step_tool` và evaluator. | ⚠️ | Dựng 3 service, chạy golden test 1 requirement, xác nhận model/temperature. |
| Tính toán | **106 × 2 arm × 3 run = 636 lượt sinh test**; **228 mutant × 3 run = 684 lượt chạy mutant**, chưa kể test valid/setup/reset. | ⚠️ | Đo runtime, RAM, lỗi API trên pilot; chưa có số đo nhóm. |
| Ground truth | Golden tests, mutant/oracle và MS_φ có sẵn trong benchmark. | ✅ | Kiểm evaluator, assertions dùng chung và định danh mutant. |
| Code base | Chỉ cần **một tool mới** copy `single_step_tool`, thay prompt; không sửa evaluator/harness. | ⚠️ | Viết prompt I, kiểm `INTERACTIVE=False`, cùng interface. |
| Kỹ năng | 5 thành viên; chưa có log tích hợp prompt tool hoặc phân công giờ công. | ⚠️ | Chốt người phụ trách setup, prompt, chạy, phân tích. |
| Thời gian | Chưa có pilot; dự kiến pilot 10 requirement × 2 arm × 1 run, sau đó full 106 × 2 × 3. | ⚠️ | Đặt hạn pilot/full và ≥3 ngày dự phòng. |

**Đếm: 2 ✅ / 5 ⚠️ / 0 ❌ — rủi ro trung bình, chưa đủ để gọi “an toàn”.** Hai ✅ chỉ xác nhận có dữ liệu và ground truth để kế thừa, chưa xác nhận môi trường chạy.

**Kế hoạch xử lý có đầu ra kiểm được:**

1. Khóa commit benchmark, 106 requirement ID và mutant manifest.
2. Viết prompt I và tool wrapper; giữ nguyên prompt C, model, temperature, assertion instructions.
3. Pilot 10 requirement thuộc một service × 2 arm × 1 run: kiểm prompt adherence, test validity, pipeline; không dùng pilot để tuyên bố effect.
4. Full 106 × 2 arm × 3 run; lưu prompt hash, token count, output, cost.
5. Tính MS_φ tổng và theo dịch vụ; paired bootstrap theo requirement; McNemar trên 228 mutant; subgroup 15 mutant nếu có danh sách.

**Giới hạn tác động:** nếu prompt I chỉ tác động đến việc chọn dữ liệu đầu vào, trần lý thuyết là **15/228 = 6,58 điểm phần trăm**; 3 run không làm tăng số mutant. Với 15 cặp discordant, exact test cần khoảng **12/15** theo hướng I mới đạt p < 0,05; 10/15 cho p ≈ 0,30. Nếu 15 mutant tập trung ở TodoApp (22 mutant), MS_φ tổng bị FastAPI 141 mutant pha loãng; bắt buộc báo **per-service** và xin GV danh sách ID/requirement.

## 5. Gap mà RQ lấp

**Gap nhóm chọn: GAP-T — đánh giá prompt-guided EP/BVA trên RESTestBench.**

### 5.1. Phát biểu gap

> Trong 59 tài liệu đã đối chiếu, nhóm chưa tìm thấy nghiên cứu đánh giá **prompt có hướng dẫn EP+BVA** so với **prompt single-step gốc** của RESTestBench trên **106 yêu cầu bản vague**, đo **MS_φ** trên 228 mutant.

Đây là **giả định/đề xuất của nhóm**, không phải gap mạnh AUTHOR_STATED: không có tập x/N tác giả cùng nêu limitation này. GV-02 chỉ đánh giá single-step/refinement, không đánh giá prompt-guided EP/BVA; việc paper không thử không đồng nghĩa tác giả đã thừa nhận thiếu.

### 5.2. Bảng hạn chế và độ mạnh

| Hạn chế | Paper nêu | Paper đã giải quyết | Còn lại | Mạnh/yếu | Loại |
|---|---|---|---|---|---|
| Chưa đánh giá prompt-guided EP+BVA so với prompt single-step trên 106 yêu cầu vague, đo MS_φ | Không có paper nào trong 59 nêu trực tiếp; GV-02 chỉ đánh giá single-step/refinement | GV-02 cung cấp P/C/O và baseline single-step; **không có I guided** | Chưa có x/N; đây là giả định của nhóm | **Giả định**, chưa xếp mạnh/yếu theo đếm | GAP-T |
| Ít dịch vụ/khó khái quát | 18/42 paper, 10 cụm — số kế thừa, chưa kiểm lại sổ quote; K89/K32 có nêu trực tiếp | GV-02 chỉ có 3 dịch vụ; không giải quyết | RQ dùng 3 dịch vụ, **không lấp GAP-D** | Tham khảo | GAP-D |
| Coverage chưa đo fault detection | GV-03 §7.3: “does not directly measure fault detection or overall test adequacy” | GV-02/TD-0002 có mutation ở thiết kế khác | 1/17 bài nền; yếu | Yếu | GAP-M |

**GAP-D** giữ làm giới hạn/bàn luận, không phải đóng góp chính. **GAP-M** chỉ hỗ trợ chọn outcome, không chứng minh thiếu phép so I/C.

### 5.3. Đối chiếu gap và RQ

**Gap:** prompt-guided EP/BVA chưa được đánh giá trên 106 yêu cầu vague của RESTestBench, với MS_φ và baseline single-step.

**RQ:** Trên 106 yêu cầu bản vague của RESTestBench, prompt có hướng dẫn EP+BVA và prompt single-step gốc khác nhau thế nào về MS_φ, cùng model và temperature?

**So với GV-02:** giữ P (106 vague), C (single-step prompt) và O (MS_φ); đổi I (thêm hướng dẫn EP/BVA). Đây là extension một yếu tố.

### 5.4. Vì sao gap còn trống

GV-02 tập trung vào single-step/refinement và chất lượng requirement; chưa thử một prompt hướng dẫn kỹ thuật EP/BVA. Trong 59 tài liệu chưa có paper nào đánh giá đúng tổ hợp này. Nguyên nhân chưa được tác giả xác nhận; nhóm chỉ kết luận **“chưa thấy trong phạm vi tài liệu đã tìm”**, không khẳng định “chưa ai làm”.

### 5.5. Lợi ích

Kỹ sư kiểm thử cần biết prompt nào giúp LLM tạo test phát hiện mutant tốt hơn trên yêu cầu vague. Nếu prompt-guided EP/BVA cao hơn, có thể ưu tiên hướng dẫn kỹ thuật trong prompt; nếu thấp hơn hoặc không khác, tránh thêm hướng dẫn không hiệu quả. Kết quả không khác biệt vẫn hữu ích để tránh suy đoán; không suy thành “hai cách tương đương” nếu thiếu power.

## 6. Quyết định

**Giữ RQ tại §1 và nhãn `extension`.** Gap là **GAP-T — prompt-guided EP/BVA**, được xác định từ đối chiếu 59 tài liệu; paper gần nhất là GV-02/RESTestBench với 3/4 (P/C/O trùng, I khác). Không đổi H0/H1.

**Trạng thái dữ liệu:** P = **106 yêu cầu vague**, 228 mutant. Chưa có pilot; API key, Docker 3 service, prompt I, phân công và thời gian còn phải khóa.

**Việc tiếp theo:**

1. Khóa commit benchmark, 106 ID và mutant manifest.
2. Viết prompt I, kiểm tra bằng 10 requirement; giữ prompt C nguyên văn.
3. Pilot và ghi runtime/lỗi; nếu ổn, chạy full 106 × 2 arm × 3 run.
4. Tính MS_φ tổng/per-service, paired bootstrap và McNemar; lưu prompt/model/version.
5. Báo GV danh sách 15 mutant và kết quả pilot trước khi khóa thực nghiệm.
