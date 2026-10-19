# Kiểm chứng RQ — FA26-EXT-12 (nhóm 1 · SaoCungDuoc)

*Nguồn: 5 file `SLR/rq-check.md` + `team-synthesis/rq-evidence-map.md` + `team-synthesis/evidence-table-merged.md` (N = 42).

## 1. RQ (nguyên văn trên thẻ) + PICO

**RQ:** Trên 45 yêu cầu của RESTestBench, phân hoạch tương đương kết hợp phân tích giá trị biên, so với sinh dữ liệu ngẫu nhiên đồng đều cùng ngân sách, khác nhau thế nào về số mutant riêng biệt bị phát hiện theo từng dạng yêu cầu, khi một mutant chỉ được tính nếu test vượt qua bản gốc nhưng thất bại trên mutant theo oracle của benchmark?

**PICO:** P = 45 yêu cầu RESTestBench (15/dịch vụ) · I = EP + BVA · C = random đồng đều, cùng request budget · O = số mutant riêng biệt, phân tầng theo dạng yêu cầu, chỉ tính khi test pass bản gốc và fail trên mutant theo oracle requirements-based. **S:** 10 lần chạy, seed cố định, Wilcoxon + Holm.

## 2. Bằng chứng làm nền (tóm tắt `rq-evidence-map.md`, N = 42 paper)

| Yếu tố | ✓ khớp đúng RQ | ◐ gần | · khác | Kết luận |
|---|---:|---:|---:|---|
| P · dataset | **0** | 28 | 14 | **Không paper nào dùng RESTestBench** — yếu tố yếu nhất |
| I · can thiệp | **2** (TD-0002, TD-0015) | 21 | 19 | 2 bài dùng EP/BVA ở mức prompt/module, chưa phải black-box request generator |
| C · đối chứng | **5** (K52/P53, K90, K34, K102, K49) | 25 | 12 | Có random cùng ngân sách ở một số bài, nhưng không phải uniform-random trên RESTestBench |
| O · thước đo | **1** (TD-0002) | 32 | 9 | Chỉ mutation score, **chưa tách unique mutant/theo dạng yêu cầu** |

**Tổng điểm:** 35/42 bài 0 ✓ · 6/42 bài 1 ✓ · 1/42 bài 2 ✓ (**TD-0002**) · **0/42 bài ≥ 3 ✓**. Không có ứng viên phản chứng theo ngưỡng ≥ 3/4.

## 3. Phản chứng tổng hợp mọi nguồn

**Mức giống cao nhất:** **TD-0002 — 2/4 ✓ (I, O)**. Đây là bài gần RQ nhất nhưng vẫn thiếu:
- **C:** không có nhánh random đồng đều cùng request budget (chỉ so 8 LLM với nhau).
- **P:** 6 dự án .NET, không phải 45 yêu cầu RESTestBench.
- **O:** có mutation score 40,8% (Stryker.NET) nhưng **chưa tách unique mutant/theo từng dạng yêu cầu**.

Các bài 1/4 ✓: K52/P53, K90, K34, K102, K49 (đều ở C) và TD-0015 (I). **Không bài nào đạt 3/4 hoặc 4/4.**

**Kết luận phản chứng:** Trong phạm vi 42 paper đã tìm, **không có phản chứng** cho RQ: chưa ai làm đủ 3/4 yếu tố, càng chưa ai làm đủ 4/4. RQ đứng vững trong phạm vi tài liệu đã tìm; không khẳng định “chưa ai làm” ngoài phạm vi này.

### Nhãn tính mới của nhóm

**Nhãn chọn theo số đông: `new`.**

| Thành viên | Nhãn ghi trong `rq-check.md` | Ghi chú |
|---|---|---|
| Lâm | `new` | 10 bài; cao nhất TD-0002 2/4 |
| Khôi | `new` | 8 bài; 0/4; có ghi rõ thẻ không hiển thị nhãn |
| T.Duy | chưa ghi nhãn riêng | kết luận 0/8, không bài ≥3/4 → nghiêng `new` |
| K.Duy | `new` | 8 bài; 0/4 |
| Tùng | `extension` | tự quyết, **chưa xác thực**; chưa có paper 3/4 làm căn cứ |

- **Số đông:** 3/5 thành viên ghi rõ `new`; 1/5 ghi `extension`; 1/5 chưa ghi nhãn → **`new`**.
- **Nhãn trên thẻ RQ:** không hiển thị (thẻ chỉ có mã/loại/độ khó). GV chưa trả lời email hỏi nhãn.
- **Lý do:** không paper nào đạt ≥3/4 theo bảng 4 kết quả; TD-0002 chỉ 2/4. `EXT` trong mã RQ **không phải** nhãn `extension`.
- **Nếu GV xác nhận `extension`:** cập nhật nhãn và ghi paper 3/4 tương ứng; **không đổi RQ** (nhãn không làm thay đổi PICO).

## 4. Khả thi: 0 ❌ / 2 ⚠️ → An toàn

| Tiêu chí | Trạng thái | Ghi chú / kế hoạch |
|---|---|---|
| Dataset | ⚠️ | RESTestBench public (GitHub/Docker, 3 dịch vụ, requirements + mutant). **Cần chốt quy tắc lấy 45 yêu cầu (15/dịch vụ)** trước pilot: repo ghi 103, paper ghi 106, RQ dùng 45. |
| API/Tool | ✅ | RESTestBench chạy local; EP+BVA và random viết bằng Python; không cần API trả phí. |
| Tính toán | ✅ | CPU laptop/Colab đủ; 45 yêu cầu × 2 kỹ thuật × 10 lần = 900 lượt; mutant chạy local. |
| Ground truth | ✅ | RESTestBench có mutant + oracle requirements-based; định nghĩa “mutant riêng biệt” chốt trong protocol trước khi chạy. |
| Code base | ✅ | Repo RESTestBench + script EP/BVA/random; không phải code từ đầu. |
| Kỹ năng | ✅ | Python/Docker/JUnit; nhóm 5 người đã đọc paper; chạy thử RESTestBench ở pilot. |
| Thời gian | ⚠️ | 900 lượt + ~97 mutant; dự kiến 1–2 ngày local. Cần pilot 5 yêu cầu để đo thời gian, chừa ≥3 ngày dự phòng. |

**Kết luận:** 0 ❌, 2 ⚠️ (dataset subset + thời gian) → **An toàn** theo quy tắc ≤2 ⚠️; hai ⚠️ đã có kế hoạch xử lý trước pilot.

## 5. Gap mà RQ lấp (kết quả Bước 2)

### Bảng gap

| Hạn chế | Paper nêu | Paper đã giải quyết | Còn lại | Mạnh/yếu | Loại |
|---|---|---|---|---|---|
| EP+BVA chưa được thử như can thiệp chính trên request black-box; 0/42 trên RESTestBench | **40/42 paper không dùng EP+BVA làm can thiệp chính** (dùng fuzz/RL/LLM/constraint; cột Tool/LLM); **2/42 chỉ prompt/module**: TD-0002, TD-0015; **0 paper tự nêu “chưa thử”** | Không — 2 bài chỉ prompt/module, chưa phải black-box request generator trên RESTestBench | 40/42 | **Mạnh theo Tool/LLM** (40/42); không có author-stated | **GAP-T** |
| Chưa đo số mutant riêng biệt/oracle-confirmed; metric coverage/bug xấp xỉ | **1 paper trực tiếp:** K49 (chưa có tool mutation cho system testing); **6 paper metric gián tiếp:** TD-0002 (mutation score 40,8% nhưng chưa tách unique), K07, K21, K02, K162/bBOXRT, K33 | TD-0002 có mutation score nhưng không tách unique/theo dạng yêu cầu → chưa giải quyết; K49 không có | 1 trực tiếp + 6 gián tiếp | **Yếu** | **GAP-M** |

### Phát biểu gap (dùng thẳng trong proposal §2)

> Trong **42 paper** đã xem xét, **40/42 paper không dùng EP+BVA làm can thiệp chính** (dùng fuzz/RL/LLM/constraint); **2/42 paper chỉ dùng EP/BVA ở prompt/module** (TD-0002, TD-0015); **0/42 paper thử trên RESTestBench**. Đây là **khoảng trống kỹ thuật quan sát từ cột Tool/LLM**, không phải hạn chế tác giả tự nêu; trong phạm vi tài liệu đã tìm, chưa có paper nào lấp.

**Theo bảng “Không dòng nào khớp”:** không paper nào **tự nêu** “chưa thử EP+BVA”, nên phát biểu trên là **giả định của nhóm**; không có câu trích author-stated nên **không được gọi là gap mạnh author-stated**. Nếu GV yêu cầu gap đủ 5 điều kiện, quay lại GAP-M (yếu).

**Vì sao gap còn trống:** các bài 2020–2026 tập trung fuzz/RL/LLM; EP+BVA cổ điển ít được dùng làm can thiệp chính; RESTestBench mới công bố (2026) với requirements + mutant/oracle.

**Loại gap chính:** **GAP-T** (công cụ/kỹ thuật chưa được thử).

### Rà future work 42 PDF (kiểm tra trích dẫn “chưa thử”)

Đã rà **42/42 PDF** ở các mục Conclusion / Future Work / Limitations cho ba cụm `equivalence partitioning`, `boundary value analysis`, `classical test design`:

- **0/42 paper tự nói “chưa thử”** một trong ba kỹ thuật này.
- Các lần xuất hiện chỉ ở **method / related work**, không phải future work:
  - **K52**: EP/BVA dùng cho **203 unit tests của IDLReasoner**, không phải HTTP request (§5.3–6, PDF10–12).
  - **K90**: EP/BVA dùng để **test chính tool** RESTest/IDLReasoner (§5, PDF13).
  - **R021**: nhận xét **related work [5] không tích hợp BVA**, không phải hạn chế của R021 (§2, PDF2).
  - **TD-0015**: EP+BVA trong **module G**; future research list không nhắc EP+BVA (§3.2/PDF5–6, §4/PDF9).
  - **TD-0002**: EP/BVA trong **prompt**; không phải future work (§3/PDF4).
  - **K02**: BVA ở **motivation**; **K33**: EP ở **method**; **K162/K101/K167**: boundary/fault operators ở **method**.
- **Kết luận:** không có trích dẫn “chưa thử” nào để thêm; **không bịa**. Vì vậy GAP-T chỉ được ghi là **giả định của nhóm**, đúng như bảng “Không dòng nào khớp”.

### Trích dẫn kiểm chứng (tiêu biểu)

- **K52** §5.3–6, PDF10: *“we developed a test suite of 203 test cases using standard testing techniques including equivalence partitioning, boundary-value analysis, … and combinatorial testing.”* — EP/BVA dùng cho **unit tests của IDLReasoner**, không phải HTTP request.
- **K90** §5, PDF13: *“both tools have been thoroughly tested using standard testing techniques such as equivalence partitioning and combinatorial testing.”* — test chính tool, không phải request generator.
- **TD-0015** §3.2, PDF5: *“It applies classical test design techniques (equivalent decomposition, boundary value analysis, and negative scenario generation)…”* — module G, 1 service; future list không nhắc EP+BVA.
- **TD-0002** §3, PDF4: *“boundary testing, equivalence classes”* — trong prompt, không phải black-box request generator.
- **K49** tr.17: *“we are not aware of any such tool aimed at system testing (i.e., they all seem to be tailored for unit testing)”* — chứng cứ cho GAP-M, không phải EP+BVA.
- **TD-0002** §5, PDF8: *“the tests had a relatively low mutation rate given the black-box test generation…”* — chứng cứ cho GAP-M.

## 6. Quyết định: giữ RQ

- **Giữ nguyên RQ FA26-EXT-12**, không đổi I (EP+BVA), C (uniform random cùng request budget) hay O (unique mutant/oracle).
- **Gap chính:** **GAP-T** — mạnh theo cột Tool/LLM (**40/42** paper không dùng EP+BVA làm can thiệp chính), nhưng **không có paper tự nêu** → chỉ dùng như **giả định của nhóm** trong proposal §2; không gọi là gap author-stated.
- **Gap phụ:** **GAP-M yếu** (1 trực tiếp K49 + 6 gián tiếp) — RQ đo O.
- **Nhãn:** `new` theo số đông (3/5 ghi rõ; Tùng `extension` là thiểu số; T.Duy chưa ghi). GV chưa trả lời email hỏi nhãn; nếu GV xác nhận `extension`, chỉ cập nhật nhãn + lý do, **không đổi RQ**.
- **Đã báo GV:** email hỏi nhãn (chưa có trả lời). Không đổi RQ nên không cần báo lại về RQ.
