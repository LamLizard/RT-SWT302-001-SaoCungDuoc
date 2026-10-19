# Kiểm chứng RQ — FA26-EXT-12 (nhóm 1 · SaoCungDuoc)

*Nguồn: 5 file `SLR/rq-check.md` + `team-synthesis/rq-evidence-map.md` + `team-synthesis/evidence-table-merged.md` (N = 42)*

## 0. Bảng đối chiếu cá nhân (5 nguồn)

| Thành viên | File | Số paper chính | Nhãn cá nhân | Ghi chú |
|---|---|---|---:|---|
| Lâm | `lam/SLR/rq-check.md` | 8 (#6 + #10–#16) | `new` | 8/8 bài 0/4 |
| Khôi | `khoi/SLR/rq-check.md` | 8 (#23–#30) | `new` | 8/8 bài 0/4 |
| Tùng | `tung/SLR/rq-check.md` | 8 (#1–#5, #7–#9) + 4 tham chiếu | **chưa xác thực** (không tự chọn `extension`) | 8 bài nền 0/4; 4 paper bổ sung; có phân tích kế thừa/bổ sung RESTBench; dòng 120 ghi rõ “chưa xác thực nhãn extension” |
| T.Duy | `t.duy/SLR/rq-check.md` | 10 (8 phân công #31–#38 + #39–#40) | `new` | TD-0002 2/4; TD-0015 1/4 |
| K.Duy | `k.duy/SLR/rq-check.md` | 8 (#17–#22, #41–#42) | `new` | 8/8 bài 0/4 |

**Tổng:** 8 + 8 + 8 + 10 + 8 = **42 paper**. Mỗi file cá nhân có bảng P/I/C/O + hạn chế + câu trích/mục trang; bảng gộp chuẩn là `team-synthesis/evidence-table-merged.md`.

## 1. RQ (nguyên văn trên thẻ) + PICO

**RQ:** Trên 45 yêu cầu của RESTestBench, phân hoạch tương đương kết hợp phân tích giá trị biên, so với sinh dữ liệu ngẫu nhiên đồng đều cùng ngân sách, khác nhau thế nào về số mutant riêng biệt bị phát hiện theo từng dạng yêu cầu, khi một mutant chỉ được tính nếu test vượt qua bản gốc nhưng thất bại trên mutant theo oracle của benchmark?

**PICO (theo thẻ W6):**
- **P:** phát hiện mutant API trên **45 yêu cầu**, gồm **15 yêu cầu từ mỗi dịch vụ** RESTestBench. **Cảnh báo dữ liệu:** TodoApp chỉ có **14 requirement** (README 63/14/26 = 103; paper 63/14/29 = 106), nên **không thể lấy 15 từ TodoApp**; cần xác nhận phiên bản dữ liệu hoặc cách xử lý P trước khi khoá RQ — **không tự đổi RQ**.
- **I:** phân hoạch tương đương kết hợp phân tích giá trị biên để chọn dữ liệu request **từ yêu cầu và schema API**.
- **C:** sinh dữ liệu ngẫu nhiên đồng đều với **cùng số request cho từng yêu cầu**.
- **O:** số mutant riêng biệt, phân tầng theo dạng yêu cầu; mutant chỉ tính khi test pass bản gốc và fail trên mutant theo **oracle requirements-based mutation**.
- **S:** 10 lần chạy, seed cố định cho mỗi cặp kỹ thuật–yêu cầu; **Wilcoxon signed-rank** trên số mutant theo yêu cầu, kèm **Holm** theo nhóm yêu cầu.

**Nhãn trên thẻ W6:** `extension` (ô “Tính mới”). `EXT` trong mã là **nhóm đề tài**, không phải nhãn.

## 2. Bằng chứng làm nền (N = 42 paper)

| Yếu tố | ✓ đạt tiêu chí rubric nhóm | ◐ gần | · khác | Kết luận |
|---|---:|---:|---:|---|
| P · dataset | **0** | 28 | 14 | **Không paper nào dùng RESTestBench** |
| I · can thiệp | **2** (TD-0002, TD-0015) | 21 | 19 | 2 bài dùng EP/BVA ở prompt/module, chưa phải black-box request generator |
| C · đối chứng | **5** (K52/P53, K90, K34, K102, K49) | 25 | 12 | Có random cùng ngân sách ở một số bài, nhưng không phải uniform-random trên RESTestBench |
| O · thước đo | **1** (TD-0002) | 32 | 9 | Chỉ mutation score, **chưa tách unique mutant/theo dạng yêu cầu** |

**Tổng điểm:** 35/42 bài 0 ✓ · 6/42 bài 1 ✓ · 1/42 bài 2 ✓ (**TD-0002**) · **0/42 bài ≥ 3 ✓**. Không có ứng viên phản chứng ≥ 3/4 trong 42 bài.

**Lưu ý:** ✓ chỉ là **đạt rubric nhóm**, không phải khớp tuyệt đối: C “cùng ngân sách” chưa chứng minh uniform; O mutation score chưa đồng nhất unique kills/theo dạng yêu cầu; I EP hoặc BVA chưa chắc đáp ứng EP+BVA kết hợp.

**P1:** N = 42 ≥ 12 → đạt; **không cần L1/L2/L3**.

## 3. Phản chứng tổng hợp các nguồn đã rà + nhãn tính mới

### 3.1. Trong 42 paper
- **Cao nhất: TD-0002 — 2/4 ✓ (I, O)**; thiếu **C** (không có random cùng request budget), **P** (6 dự án .NET, không phải 45 RESTestBench), **O** chỉ mutation score chưa tách unique.
- Các bài 1/4 ✓: K52/P53, K90, K34, K102, K49 (C) và TD-0015 (I).
- **Không bài nào đạt 3/4 hoặc 4/4** → nếu chỉ tính 42 paper thì nhãn là `new`.

### 3.2. Rà 2–3 paper mạnh nhất 12 tháng (ngoài 42)
Ba paper này **không nằm trong 42** (rà riêng của Khôi, 04–06/2026), chỉ dùng để định vị đóng góp:
- **RESTestBench — 2/4 (P, O):** 3 dịch vụ, 106 yêu cầu, 228 mutant; chỉ đánh giá LLM; tác giả tự nêu *“Our benchmark includes only three services”* và *“Each experiment was executed only three times”* (§6).
- **Req2REST-Guard — 2/4 (P, O):** dùng RESTestBench (106 yêu cầu/228 mutations), GPT-4o; không có EP+BVA hay random cùng ngân sách; bài chưa có venue, Table I lệch — **chỉ đối chiếu tính mới, không dùng số liệu**.
- **MASTOR — 1/4 (O):** sinh oracle, không sinh input; không lấp I/C.
- **Bổ sung từ Tùng (không vào bảng chính):** **MioHint — 0/4** (request mutation/coverage, không killed mutant), **RESTOR — 0/4** (sinh oracle, không sinh request), **R2R-04 amplification — 0/4** (1 microservice/6 endpoint, không mutation). Không bài nào ≥3/4; chỉ dùng để kiểm tra không bỏ sót, không đổi nhãn.

**Mốc 2/4 để so:** trong 42 có **TD-0002 2/4**; ngoài 42 có **RESTestBench 2/4**, **Req2REST-Guard 2/4**; **Guo 2024 3/4 là paper gần nhất**, không paper nào khác ≥3/4.

**Kết luận:** không bài nào ≥3/4; đóng góp không phải “model mới hơn” mà là **phép so EP+BVA với uniform random cùng ngân sách, đo mutant riêng biệt theo dạng yêu cầu trên RESTestBench**.

### 3.3. Paper gần nhất + nhãn nhóm
Theo hướng dẫn của GV, đã soát hướng **BVA so với random trên hệ không phải REST API**. Paper gần nhất:

**Guo, Okamura & Dohi (2024), “Optimal test case generation for boundary value analysis”, Software Quality Journal 32(2), 543–566, DOI `10.1007/s11219-023-09659-9`.**
- **P:** 5 chương trình non-REST — **khác** 45 yêu cầu RESTestBench.
- **I:** BVA/BCD — **giống** theo rubric I ✓ (EP và/hoặc BVA).
- **C:** random testing với cùng `n` test — **giống** (cần xác nhận uniform cùng budget).
- **O:** mutation score — **giống** theo rubric O ✓ (chưa tách unique).
- → **3/4 (I, C, O)**, chỉ khác P → **`extension`**, khớp thẻ W6.

**Nhãn nhóm chốt: `extension`.**
- Nếu chỉ tính 42 paper: `new` (cao nhất 2/4).
- Theo hướng dẫn GV: soát **paper gần nhất ngoài 42** (không rà rộng); Guo 2024 đạt 3/4 → `extension`.
- 4/5 file cá nhân ghi `new` vì chỉ xét 42 bài; **Tùng ghi “chưa xác thực nhãn extension”, không tự chọn `extension`** — không tính Tùng là phiếu extension; nhãn nhóm lấy theo paper gần nhất 3/4 + thẻ W6.
- **Cảnh báo:** nếu kiểm full text thấy C không cùng `n`/không uniform, Guo chỉ còn 2/4 → nhãn `new`; khi đó phải ghi lý do lệch thẻ.

## 4. Khả thi: ước tính sơ bộ từng gap (chưa chạy benchmark)

| Tiêu chí | GAP-T (chọn) | GAP-D | GAP-M |
|---|---|---|---|
| Dataset | 45/103 yêu cầu, 3 dịch vụ; **TodoApp chỉ 14** → không đủ 15/dịch vụ; README 103 vs paper 106; ⚠️ xác nhận version/cách xử lý P | same — cùng vướng P | same — cùng vướng P |
| API/Tool | 3 dịch vụ Docker, Python adapter; ✅ | 3 dịch vụ Docker; ✅ | 3 dịch vụ Docker; ✅ |
| Tính toán | **900 lượt kỹ thuật–yêu cầu** (45×2×10), **chưa phải tổng HTTP executions**; cộng B/replay/reset/retry; ~**97 mutant** là ước lượng từ 228/106×45, chưa phải mẫu 45; RAM 16 GB dự kiến, chưa đo runtime; ⚠️ | same — cùng ước tính | same — cùng ước tính |
| Ground truth | 228 mutant/106 yêu cầu; ~97 cho 45 là ước lượng; oracle requirements-based; ⚠️ chưa chạy | same | same |
| Code base | RESTestBench + 2 script (EP/BVA, random); ✅ chưa chạy | same | same |
| Kỹ năng | 5 người; Python/Docker/JUnit; ✅ | same | same |
| Thời gian | 900 lượt + 97 mutant; **1–2 ngày là ước tính**, chưa tính B/replay/reset/retry; pilot 5 yêu cầu; +3 ngày dự phòng; ⚠️ | same — cùng ước tính | same — cùng ước tính |
| **Kết luận** | **Sơ bộ không thấy ❌; chưa đủ dữ liệu — cần pilot** | Chưa đủ dữ liệu — cần pilot | Chưa đủ dữ liệu — cần pilot |

**Không gọi “An toàn”**: chưa chạy benchmark, chưa có B/runtime; 900 chỉ là lượt kỹ thuật–yêu cầu, chưa phải HTTP executions; ~97 mutant là ước lượng. Cần pilot 5 yêu cầu (TodoApp 14 → chốt cách xử lý P) trước khi chấm lại.

## 5. Gap mà RQ lấp

### 5.1. Câu gap RQ ban đầu (viết trước khi đếm)

> “Chưa ai thử **EP+BVA làm can thiệp chính** để sinh request black-box trên REST API/RESTestBench.”

- **Khớp GAP-T** — **tín hiệu kỹ thuật 40/42** theo cột **Tool/LLM**, **không phải gap mạnh author-stated**: **40/42 paper không dùng EP+BVA làm can thiệp chính**; 2/42 chỉ prompt/module; 0/42 trên RESTestBench.
- **Về author-stated:** **không dòng nào khớp** — 0/42 paper tự nêu “chưa thử EP+BVA”; do đó đây là **giả định của nhóm**, không được gọi là gap mạnh author-stated.

### 5.2. Bảng gap

| Hạn chế | Paper nêu | Paper đã giải quyết | Còn lại | Mạnh/yếu | Loại |
|---|---|---|---|---|---|
| EP+BVA chưa được thử như can thiệp chính trên request black-box; 0/42 trên RESTestBench | **40/42 paper không dùng EP+BVA làm can thiệp chính** (fuzz/RL/LLM/constraint; cột Tool/LLM); **2/42 chỉ prompt/module:** TD-0002, TD-0015; **0 paper tự nêu “chưa thử”** | Không — 2 bài chỉ prompt/module, chưa phải black-box request generator trên RESTestBench | 40/42 | **Giả định của nhóm** (tín hiệu 40/42; không author-stated) | **GAP-T** |
| Ít SUT/dataset nhỏ (2–20 API/SUT; 1 app/service) | **11 nhóm tác giả (ít nhất một paper trong nhóm nêu):** SCORE Lab (K52/K46/K76/K90/K34/K102), Corradini (K32/K167/K168/K191), Kim (P12/P17), Karlsson (K37/K67), Wu (K66), Moskalenko (TD-0015), K02, K33, He (K89), Chen (K93), Mirabella (K166) | Không — 0/42 dùng RESTestBench; P12 20 services nhưng khác metric/oracle | 11 nhóm | **Tiềm năng — chưa đủ truy vết** (mới K89/K32 có quote trực tiếp) | **GAP-D** |
| Chưa đo số mutant riêng biệt/oracle-confirmed; metric coverage/bug xấp xỉ | **1 paper trực tiếp:** K49 (chưa có tool mutation cho system testing); **6 paper gián tiếp:** TD-0002 (mutation score 40,8% nhưng chưa tách unique), K07, K21, K02, K162/bBOXRT, K33 | TD-0002 có mutation score nhưng không tách unique/theo dạng yêu cầu; K49 không có | 1 trực tiếp + 6 gián tiếp | **Yếu** | **GAP-M** |

**Gộp nhóm tác giả:** SCORE Lab (K52/K46/K76/K90/K34/K102) = **1 nhóm**; Corradini (K32/K167/K168/K191) = **1 nhóm**; Kim (P12/P17) = **1 nhóm**; Karlsson (K37/K67) = **1 nhóm**; còn lại K66, TD-0015, K02, K33, K89, K93, K166 mỗi bài 1 nhóm → **11 nhóm**, không đếm 20+ paper.

**Lưu ý GAP-D:** 11 nhóm mới là **tín hiệu từ bảng**; hiện chỉ **K89 (§5.4/PDF27)** và **K32 (§V.E/PDF9)** có trích trực tiếp. 9 nhóm còn lại cần truy vết quote/mục/trang trước khi gọi gap mạnh. **RQ dùng 45 yêu cầu/3 dịch vụ RESTestBench — lặp lại hạn chế ít SUT/khó khái quát, không chứng minh giải quyết GAP-D**; không dùng D làm gap chính, không claim D đã được lấp.

**Đã gạch:** Không có dòng nào đủ điều kiện gạch (cùng bài toán + metric + dataset/cỡ mẫu + kết quả số). Vì vậy bảng không có dòng “đã giải quyết”; các near-miss chỉ dùng tham khảo.

### 5.3. Phát biểu gap

**GAP-T (chính):**
> Trong **42 paper**, **40/42 paper không dùng EP+BVA làm can thiệp chính** (dùng fuzz/RL/LLM/constraint); **2/42 paper chỉ dùng EP/BVA ở prompt/module** (TD-0002, TD-0015); **0/42 paper thử trên RESTestBench**. Đây là **khoảng trống kỹ thuật quan sát từ cột Tool/LLM**, không phải hạn chế tác giả tự nêu; trong phạm vi tài liệu đã tìm, chưa có paper nào lấp.

**GAP-D (phụ, tín hiệu author-stated — cần truy vết):**
> Trong **42 paper**, **11 nhóm tác giả (ít nhất một paper trong nhóm nêu)** (SCORE Lab: K52/K46/K76/K90/K34/K102; Corradini: K32/K167/K168/K191; Kim: P12/P17; Karlsson: K37/K67; cùng K66, TD-0015, K02, K33, K89, K93, K166) cùng nêu hạn chế **ít SUT/dataset nhỏ hoặc không đại diện** (2–20 API/SUT; 1 app/service); **0/42 paper dùng RESTestBench**. Không paper nào trong bảng giải quyết đồng thời quy mô mẫu và benchmark có mutant/oracle requirements-based (trong phạm vi tài liệu đã tìm). **Mới K89 (§5.4/PDF27) và K32 (§V.E/PDF9) có trích trực tiếp; 9 nhóm còn lại cần truy vết trước khi gọi gap mạnh.**

**GAP-M (yếu):**
> Trong **42 paper**, **1 paper (K49)** nêu trực tiếp chưa có tool mutation cho system testing; **6 paper** (TD-0002, K07, K21, K02, K162/bBOXRT, K33) nêu hạn chế metric gián tiếp; **không paper nào** báo cáo số mutant riêng biệt theo từng dạng yêu cầu trên RESTestBench. Đây là **gap yếu** — không viết quá mạnh trong proposal.

**Vì sao gap còn trống:**
- **GAP-T:** các bài 2020–2026 tập trung fuzz/RL/LLM; EP+BVA cổ điển ít được dùng làm can thiệp chính; RESTestBench mới công bố (2026) với requirements + mutant/oracle.
- **GAP-D:** benchmark RESTestBench mới có; các nhóm trước phải tự dựng API/spec nên quy mô nhỏ.
- **GAP-M:** mutation testing cho system testing còn khó/tốn kém; K49 (2023) nêu chưa có công cụ phù hợp.

### 5.4. Paper gần nhất + bảng căn hàng (dùng làm slide đầu)

**Paper gần nhất:** Guo, Okamura & Dohi (2024), *Optimal test case generation for boundary value analysis*, Software Quality Journal 32(2), 543–566, DOI `10.1007/s11219-023-09659-9`.

| Yếu tố | RQ nhóm | Paper gần nhất | Giống/khác | Bằng chứng / lý do |
|---|---|---|---|---|
| **P** | 45 yêu cầu RESTestBench (15/dịch vụ; **TodoApp chỉ 14 — xem §1**) | 5 chương trình non-REST | **Khác** | Paper thử trên 5 chương trình; RQ dùng RESTestBench — đây là yếu tố đổi; 3 dịch vụ vẫn là ít SUT, không giải quyết GAP-D |
| **I** | EP + BVA | BVA/BCD | **Giống** (BVA) | Paper dùng BVA; rubric I ✓ cho EP và/hoặc BVA; nếu yêu cầu EP+BVA kết hợp thì I chỉ ◐ |
| **C** | Uniform random cùng request budget | Random test set cùng `n` test | **Giống** (cần xác nhận uniform) | Paper dùng random testing với `n` test; nếu khác budget/uniform → C ◐ |
| **O** | Số mutant riêng biệt/oracle | Mutation score | **Giống** theo rubric | Paper dùng mutation testing; chưa tách unique mutant |
| **Kết luận** |  |  | **3/4 → `extension`** | Chỉ P khác; khớp nhãn thẻ W6 |

*Nếu full text xác nhận C không cùng `n`/không uniform → Guo chỉ 2/4 → nhãn `new`; khi đó ghi lý do lệch thẻ.*

*Trích kiểm chứng: **P** — “We conducted the experiments on five programs” (§5); **C** — “In the RT approach, we randomly generate a test set consisting of n test inputs…” (§5); **O** — “execute each mutated program with this test set to study the fault detection ability” (§5).*

### 5.5. RQ cho từng gap + lợi ích

| Gap | RQ | P/I/C/O | O đo bằng số | Khác RQ ban đầu |
|---|---|---|---|---|
| **GAP-T (chọn)** | RQ gốc FA26-EXT-12 | P 45 RESTestBench; I EP+BVA; C uniform random cùng budget; O unique mutant/oracle | số mutant riêng biệt, 10 lần chạy | Không — RQ gốc |
| **GAP-D (tín hiệu phụ, không chọn)** | Không tạo RQ riêng | RQ gốc dùng P = RESTestBench 3 dịch vụ — lặp lại hạn chế ít SUT | same | Không — P đã là RESTestBench; không claim D được giải quyết |
| **GAP-M (yếu)** | Không cần RQ riêng | RQ gốc đo O = mutant | same | Không |

**Câu lợi ích — GAP-T + RQ:**
- **Ai dùng:** kỹ sư kiểm thử REST API và nhóm nghiên cứu benchmark.
- **Hiểu/quyết định gì:** EP+BVA có phát hiện nhiều mutant riêng biệt hơn random cùng ngân sách hay không, theo từng dạng yêu cầu.
- **Nếu H0 không bị bác bỏ:** họ có thể dùng random/đơn giản hơn, không đầu tư EP+BVA; báo cáo “không thấy lợi ích”.
- **Nếu H0 bị bác bỏ:** ưu tiên EP+BVA cho các dạng yêu cầu tương ứng; dùng kết quả để chọn kỹ thuật sinh input.
- **Nếu kết quả không kết luận:** báo cáo CI/power, tăng số lần chạy; không tuyên bố “tốt hơn”.

**Câu lợi ích — GAP-D + RQ:**
- **Ai dùng:** người xây benchmark/đánh giá công cụ REST API.
- **Hiểu/quyết định gì:** kết quả trên 45 yêu cầu có khái quát được hay chỉ do tập con nhỏ.
- **Nếu H0 không bị bác bỏ:** mở rộng dataset/không overclaim; dùng kết quả làm giả thuyết.
- **Nếu H0 bị bác bỏ:** dùng RESTestBench làm benchmark chuẩn cho so sánh.
- **Nếu không kết luận:** báo cáo giới hạn cỡ mẫu và độ phủ dịch vụ.

## 6. Quyết định

- **Giữ nguyên RQ FA26-EXT-12**, không đổi I/C/O. **Mọi thay đổi RQ: không có** → không cần báo GV lại; nếu sau này đổi I/C sẽ báo trước khi khoá.
- **Gap chính:** **GAP-T** (**giả định của nhóm**; tín hiệu kỹ thuật 40/42; **không author-stated** — ghi rõ trong proposal §2, không gọi “gap mạnh”).
- **Gap phụ:** **GAP-D tiềm năng** (11 nhóm tín hiệu; mới K89/K32 có quote trực tiếp; cần truy vết 9 nhóm còn lại) — **không chọn làm gap chính** vì RQ vẫn dùng 3 dịch vụ, lặp lại hạn chế ít SUT; **GAP-M yếu** (1 trực tiếp + 6 gián tiếp).
- **P chưa chốt:** TodoApp chỉ có 14 requirement, không đủ 15/dịch vụ; README 103 vs paper 106. Cần xác nhận phiên bản dữ liệu và cách xử lý P trước khi khoá; **không tự đổi RQ**.
- **Nhãn nhóm:** **`extension`** — theo thẻ W6 và paper gần nhất Guo 2024 (3/4; chỉ P khác); **Tùng chưa xác thực, không tính là phiếu extension**. Nếu chỉ tính 42 paper thì `new`; nếu GV không chấp nhận paper ngoài 42 hoặc C không cùng budget → ghi lý do lệch thẻ và dùng `new`.
