# 🔬 SWT302 · Lộ trình nghiên cứu khoa học · Tuần 6–10

> **Nguồn:** [Tài liệu giảng viên – Tuần 7, RBL-2 · Kiểm chứng RQ](https://swt302.chiltq.workers.dev/fa26-se2043/)  
> **Phạm vi:** Toàn bộ nội dung RBL-2 được cung cấp trong bản sao văn bản từ website, bao gồm các mục mở rộng và mẫu sao chép. Các liên kết RBL-0 được bảo lưu; nội dung của trang đích không nằm trong bản sao.  
> **Ghi chú chuyển đổi:** Chỉ chuẩn hóa cấu trúc Markdown (tiêu đề, bảng, danh sách, khối mã, liên kết). Các thành phần điều khiển giao diện như nút mở/gập, nút copy, bộ đếm tick và chế độ nền tối không phải hướng dẫn học thuật.

**Tuần:** 7 (ngày 1–2)  
**Tài liệu RBL:** RBL-2 · Kiểm chứng RQ · [RBL-3 · Proposal](https://swt302.chiltq.workers.dev/fa26-se2043/)

## RBL-2 · Kiểm chứng RQ

**5 mục** · theo trình tự

**Tuần:** 7 (ngày 1–2) · **Đầu vào:** thẻ RQ đã đăng ký + `team-synthesis/rq-evidence-map.md` + `evidence-table-merged.md` · **Output cá nhân:** `SLR/rq-check.md` · **Output nhóm:** `team-synthesis/rq-validation.md` · **Thời gian:** khoảng 5–6 giờ/người.

**Mục tiêu Tuần 7:** biết RQ của nhóm lấp **khoảng trống (gap)** nào, gap đó mạnh hay yếu, và chưa paper nào đã làm đúng RQ này.

- **Phản chứng và gap** (Bước 2): từ một bảng đối chiếu paper với RQ rút hai kết luận. RQ đã có ai làm chưa (1 trong 4 kết luận) [**📖 3 câu hỏi và 4 kết luận**](https://swt302.chiltq.workers.dev/fa26-se2043/#ly-kiem-chung); gap mà RQ ban đầu nhắm tới là gì, gap đó mạnh hay yếu (từ hạn chế nhiều paper cùng nêu) [**📖 Gap là gì, vì sao tìm từ hạn chế**](https://swt302.chiltq.workers.dev/fa26-se2043/#ly-khoang-trong).
- **Ghi gap và RQ cho từng gap** (cuối Bước 2): phát biểu gap đúng mẫu, mỗi gap mạnh một RQ đo được.
- **Khả thi** (Bước 3): mỗi cặp gap + RQ nhóm đang cân nhắc (gap ban đầu, và gap mạnh khác nếu định đổi RQ) có làm được trong thời gian còn lại không, chấm bằng số cụ thể của nhóm.

**Hạn chót:** mọi thay đổi RQ phải xong **trước khi giảng viên khoá (hết buổi 1 Tuần 7)**.

**Cách đọc:** làm lần lượt 3 bước bên dưới. Gặp từ hay lý do chưa rõ thì bấm **📖** để xem phần giải thích ở RBL-0 trong khung bên phải, xem xong bấm **✕** để đóng. Mục **▸** chứa mẫu file hoặc code thì gập sẵn, mở khi cần.

| # | Việc | Khi nào | Ai | Nộp / cập nhật |
|---|---|---|---|---|
| 1 | Kiểm tra evidence table (5 cổng) | ngày 1, 30 phút | PL | không có file riêng; qua đủ 5 cổng mới làm tiếp |
| 2 | Đối chiếu paper với RQ: phản chứng và gap | ngày 1 (cá nhân), ngày 1–2 (nhóm gộp) | mỗi người, PL gộp | `SLR/rq-check.md` (mục 1, 2), `team-synthesis/rq-validation.md` (mục 3, 5) |
| 3 | Rà khả thi lần cuối (mỗi gap đang cân nhắc một cột) | ngày 1–2 | cả nhóm | `rq-check.md` (mục 3), `rq-validation.md` (mục 4) |

**Chỉ hoàn tất khi:** mỗi người có bảng đối chiếu paper (P/I/C/O + hạn chế), nhóm có **câu gap RQ ban đầu ghi trước khi đếm** và kết quả đối chiếu với bảng gap (hạn chế đã gạch cái paper khác giải quyết, gap mạnh có loại), nhóm có nhãn tính mới kèm lý do, khả thi của từng gap đang cân nhắc không còn ❌ (hoặc đã có kế hoạch downscope), và mọi thay đổi RQ đã báo giảng viên trước khi khoá. Checklist đầy đủ ở cuối tài liệu.

## Bước 1 · Kiểm tra evidence table (PL, ngày 1, 30 phút)

1. Mở `team-synthesis/evidence-table-merged.md`.
2. Đối chiếu 5 cổng P1–P5 trong bảng dưới.
3. Cổng nào Fail thì làm theo cột “Fail → làm gì”. Chỉ sang Bước 2 khi qua đủ 5 cổng.

| Cổng | Pass khi | Fail → làm gì |
|---|---|---|
| P1 | ≥ 12 paper included (mức tối thiểu của bảng gộp, RBL-1) | Quay lại tìm thêm |
| P2 | Cột Tool/LLM: ≥ 90% hàng có dữ liệu | Đọc lại Section 3 của paper |
| P3 | Cột Kết quả: ≥ 50% hàng có con số | Đọc lại Table/Figure của paper |
| P4 | Cột Hạn chế: ≥ 50% hàng có dữ liệu | Đọc Threats to Validity / Future Work |
| P5 | Cột Metric: tên cụ thể (không phải “accuracy” chung chung) | Đọc lại Evaluation Metrics |

## Bước 2 · Đối chiếu paper với RQ: phản chứng và gap (mỗi người ngày 1, nhóm gộp ngày 1–2)

Đọc mỗi paper **một lần**, ghi cả hai thứ vào cùng một bảng: paper giống RQ ở mấy yếu tố P/I/C/O (để biết RQ đã có ai làm chưa) và hạn chế cụ thể paper nêu (để tìm gap). Từ bảng đó rút hai kết luận.

### Phần cá nhân (mỗi người, paper nguồn của mình, ngày 1)

1. Với mỗi ứng viên, ghi một dòng (mẫu ở mục ▸ dưới): P/I/C/O có giống RQ không, và **hạn chế cụ thể** paper nêu (lấy từ cột Hạn chế của bảng gộp; câu chung chung như “cần thêm dữ liệu” bỏ). Ghi kèm **câu trích nguyên văn và mục/trang** của paper; paper không nêu hạn chế thì ghi “không nêu”, không bỏ trống. [**📖 Phản chứng là gì**](https://swt302.chiltq.workers.dev/fa26-se2043/#t-phan-chung)
2. Đọc kết quả theo bảng “Kết quả / Nghĩa là / Làm gì” rồi ghi kết luận phần của mình.
3. Đối chiếu nhãn tính mới trên thẻ RQ (ô **“Tính mới: …”** cạnh độ khó; new / extension / replication, do máy so với kho paper). Mã RQ (W4, W5, EXT) chỉ là nhóm đề tài, không phải nhãn. Nhãn của nhóm khác nhãn trên thẻ thì ghi lý do: paper giống nhất và yếu tố nào khác.
4. **Rà nghiên cứu mạnh nhất gần đây:** tìm thêm 2–3 paper mạnh nhất trong 12 tháng gần nhất cùng chủ đề (venue lớn, benchmark lớn, nhiều model). Nêu rõ RQ đo được điều gì mà các paper đó chưa đo (dataset khác bản chất, metric khác, điều kiện thực tế khác). **Thêm các paper này vào bảng đối chiếu ở việc 1** (P/I/C/O + hạn chế): chúng được tính khi gán nhãn, như paper trong bảng gộp. Cùng chủ đề chưa phải là giống; chỉ đếm yếu tố P/I/C/O giống. Ghi truy vấn và ngày tìm vào `search-log.md`; chọn theo thứ tự: cùng bài toán/metric, rồi venue/benchmark lớn, rồi mới nhất; ghi lý do chọn và loại. [**📖 Vì sao “model mới hơn” là chưa đủ**](https://swt302.chiltq.workers.dev/fa26-se2043/#ly-dong-gop)

**Cách gán nhãn:** đếm theo **từng paper** (một paper phải giống cùng lúc các yếu tố, không ghép yếu tố của nhiều paper), lấy mức giống cao nhất. Phạm vi so: paper trong `evidence-table-merged.md` cộng 2–3 paper tìm thêm ở việc 4, không cần rà rộng hơn.

| Kết quả | Nghĩa là | Làm gì |
|---|---|---|
| Không paper nào giống từ 3/4 yếu tố trở lên (cao nhất 2/4) | RQ là **mới** (new) trong phạm vi đã tìm | Giữ RQ; ghi “xác nhận trong phạm vi tài liệu đã tìm”, không khẳng định tuyệt đối |
| Có paper giống 3/4 yếu tố | RQ là **mở rộng** (extension) | Giữ RQ; ghi rõ khác ở yếu tố nào. Đó chính là đóng góp của nhóm |
| Có paper giống đủ 4/4 | RQ đã có paper làm cùng 4 yếu tố: nếu nhóm giữ RQ thì đây là **tái hiện** (replication) | Báo PL và giảng viên ngay. Giữ và ghi rõ là tái hiện (được phép); so thêm protocol, phiên bản, cỡ mẫu và kết quả với paper đó |
| Giống đủ 4/4 và nhóm không muốn làm tái hiện | **Cần đổi I hoặc C** | Đổi kỹ thuật (I) hoặc đối chứng (C) theo luật của tab Đăng ký RQ, trước khi giảng viên khoá |

#### Mẫu bảng đối chiếu paper (phản chứng + hạn chế) và công cụ P/I/C/O

**RQ:** [câu RQ nguyên văn trên thẻ]  
*(Có = giống RQ ở yếu tố đó)*

| Paper | P | I | C | O | Hạn chế paper nêu |
|---|---|---|---|---|---|
| Chen 2023 | Có | Không | Có | Không | Chỉ đo coverage |
| Liu 2024 | Có | Có | Không | Không | Chỉ thử trên Java |
| Dakhel 2024 | Có | Có | Có | Không | Chỉ đo coverage |

→ Kết luận phần của tôi: Dakhel 2024 giống 3/4 (khác ở O) nên RQ là extension; chưa có paper giống 4/4. Hạn chế đã ghi để nhóm gộp tìm gap. (Bảng trên là ví dụ minh họa cách ghi.)

#### 🔎 So một ứng viên phản chứng với RQ

*Tick yếu tố mà paper giống RQ:*

- P · dữ liệu / task
- I · can thiệp (công cụ, model, prompt)
- C · đối chứng (baseline)
- O · thước đo (metric)

**0/4** yếu tố giống RQ

**Không phản chứng:** Paper chỉ giống 0/4 yếu tố: dùng làm nền cho RQ, không phải lời giải sẵn.

**Làm gì:** Ghi vào bảng phản chứng. Không paper nào ≥ 3/4 thì kết luận “RQ đứng vững trong phạm vi tài liệu đã tìm”, không khẳng định tuyệt đối.

### Phần nhóm (PL gộp mọi bảng cá nhân, ngày 1–2)

Gap chắc nhất là điều **nhiều paper tự thừa nhận chưa làm được**. [**📖 Vì sao tìm gap từ hạn chế**](https://swt302.chiltq.workers.dev/fa26-se2043/#ly-khoang-trong)

1. **Ghi gap của RQ ban đầu (RQ nhóm đã chọn, là điểm xuất phát tìm gap), TRƯỚC khi gộp và đếm:** đọc câu RQ và PICO trên thẻ, tự hỏi “RQ này làm điều gì mà theo nhóm chưa ai làm?”. Viết thành **một câu**: “Chưa ai [thử công cụ I / đo O / làm trên dữ liệu P] …” và gắn loại GAP-T/M/D (bảng dưới). Ví dụ: “Chưa ai đo khả năng phát hiện lỗi (mutation score) của unit test do LLM sinh ra, các nghiên cứu trước chỉ đo coverage” (GAP-M). Ghi vào mục 5 của `rq-validation.md` **nguyên văn, không sửa lại** sau khi thấy kết quả đếm: viết sau khi đã thấy số thì dễ “nhìn ra” đúng gap mà RQ đang lấp. [**📖 Vì sao ghi trước**](https://swt302.chiltq.workers.dev/fa26-se2043/#ly-khoang-trong)
2. **Phản chứng của nhóm:** lấy mức giống cao nhất trong mọi bảng cá nhân, ghi vào mục 3 của `rq-validation.md` (theo bảng Kết quả ở trên).
3. **Liệt kê hạn chế:** gộp cột hạn chế của mọi bảng cá nhân, mỗi hạn chế một dòng, ghi paper nào nêu. Hạn chế cùng nghĩa thì gộp một dòng.
4. **Gạch cái đã giải quyết:** nếu một paper khác trong bảng đã làm đúng điều hạn chế nói chưa làm, **và làm đủ tin** (cùng bài toán và metric, nêu rõ dataset và cỡ mẫu, có kết quả số) thì gạch dòng đó và ghi tên paper đã giải quyết. Làm sơ sài thì giữ dòng, ghi “chưa đủ chắc”.
5. **Đếm:** với dòng còn lại, đếm số paper cùng nêu (paper cùng nhóm tác giả đếm là 1). Từ **3 paper** trở lên là **gap mạnh**; 1–2 paper là gap yếu. Ghi mẫu số: “x trên N paper có nêu hạn chế”. Đếm chỉ cho biết nhiều paper nhắc tới hạn chế đó, chưa chứng minh gap quan trọng. [**📖 Vì sao**](https://swt302.chiltq.workers.dev/fa26-se2043/#ly-khoang-trong)
6. **Gắn loại và đối chiếu:** mỗi gap mạnh gắn một loại trong bảng dưới, rồi đặt **câu gap RQ ban đầu** (việc 1) cạnh bảng gap để xem nó rơi vào trường hợp nào ở bảng “Quyết định về gap”.
7. **Viết phát biểu gap và RQ cho từng gap mạnh** theo mục “Ghi gap cho hợp lệ và viết RQ cho từng gap” ngay bên dưới.

| Loại | Nghĩa là | Ví dụ hạn chế | Lọc cột nào của bảng gộp |
|---|---|---|---|
| GAP-T | Công cụ/kỹ thuật chưa được thử | Chưa thử model nhỏ, chi phí thấp | Tool/LLM |
| GAP-M | Khía cạnh chưa được đo | Chỉ đo coverage, chưa đo khả năng phát hiện lỗi | Metric |
| GAP-D | Domain hoặc quy mô dữ liệu còn thiếu | Chỉ thử trên Java, hoặc trên dataset dưới 100 hàm | Dataset |

**Cách gạch:** lọc đúng cột ở bảng trên (ví dụ GAP-M, thiếu metric X thì lọc cột **Metric** lấy các paper có nhắc X).

**Paper có làm nhưng khác bài toán của RQ:** không gạch, dùng làm tham khảo (cách tính, baseline, nguồn ngưỡng). [**📖 Vì sao**](https://swt302.chiltq.workers.dev/fa26-se2043/#ly-khoang-trong)

#### Quyết định về gap (so câu gap RQ ban đầu với bảng gap)

| Gap RQ ban đầu rơi vào | Nghĩa là | Làm gì |
|---|---|---|
| Khớp một **gap mạnh** (còn lại ≥ 3 paper) | Giả định ban đầu của nhóm có bằng chứng từ paper | Giữ RQ; ghi gap đó và số paper vào mục 5 của `rq-validation.md` |
| Khớp một **gap yếu** (1–2 paper) | Có người nhắc tới nhưng chưa nhiều | Vẫn giữ được; ghi rõ là gap yếu, không viết quá mạnh trong proposal |
| **Không dòng nào** trong bảng khớp | Gap này mới chỉ là suy đoán của nhóm, chưa paper nào trong bảng nêu | Ghi “chưa có paper nêu, là giả định của nhóm”. Đọc lại cột Hạn chế xem có bỏ sót không; nếu có gap mạnh khác gần RQ thì cân nhắc đổi RQ (báo giảng viên trước khi khoá) |
| Khớp dòng **đã gạch** (paper khác đã giải quyết đủ tin) | Điều RQ cho là “chưa ai làm” thực ra đã có người làm | Báo PL và giảng viên ngay; đổi I hoặc C, hoặc giữ và ghi rõ là tái hiện / mở rộng (xem bảng Kết quả ở trên) |

#### Gap còn trống có thể có lý do

Với gap mà RQ lấp, trả lời một dòng: **vì sao gap này còn trống?**

1. **Chưa ai để ý, hoặc công cụ/dữ liệu mới có gần đây:** gap đáng làm.
2. **Khó hoặc tốn kém** (thiếu ground truth, API đắt): chuyển sang Bước 3 rà khả thi.
3. **Có thể đã có người thử nhưng không hiệu quả:**
   - Đọc các paper giống RQ từ 2 yếu tố P/I/C/O (cột `near_rq`, hoặc `rq-evidence-map.md`): họ có thử gần gap này không, kết quả ra sao, hạn chế họ ghi gì.
   - Tìm thêm một lượt trên Scholar hoặc arXiv với từ khoá “negative result”, “did not improve”, “fails” cùng chủ đề (kết quả âm thường không nằm trong bảng gộp).
   - Có paper đã thử mà không hiệu quả: nêu RQ khác điều kiện nào, hoặc giữ RQ và coi kết quả âm là kết quả hợp lệ.

Không tìm được dấu hiệu nào thì ghi “chưa thấy trong phạm vi tài liệu đã tìm”, không khẳng định “chưa ai thử”. Ghi một dòng này vào mục 5 của `rq-validation.md`, dưới phát biểu gap. [**📖 Vì sao phải hỏi**](https://swt302.chiltq.workers.dev/fa26-se2043/#ly-khoang-trong)

### Ghi gap cho hợp lệ và viết RQ cho từng gap (kết quả Bước 2, mục 5 của `rq-validation.md`)

Có bảng gap rồi, mỗi **gap mạnh** nhóm còn cân nhắc phải có hai thứ: **phát biểu gap** viết đúng cách, và **RQ lấp gap đó**. RQ ban đầu của nhóm là RQ của gap mà nó khớp; gap mạnh khác thì viết RQ nháp để so khả thi ở Bước 3. Gap yếu không cần RQ riêng. Phát biểu gap dùng thẳng trong proposal §2. [**📖 Gap**](https://swt302.chiltq.workers.dev/fa26-se2043/#t-gap)

**Phát biểu gap viết theo mẫu:** “Trong [N] paper đã xem xét, [x] paper ([tên paper]) cùng nêu hạn chế [điều cụ thể còn thiếu]; không paper nào trong bảng giải quyết điều đó (trong phạm vi tài liệu đã tìm).” Gap hợp lệ khi đủ 5 điều:

1. **Có mẫu số và tên paper:** “x trên N paper”, kèm tên.
2. **Cụ thể, một gap một ý, một loại:** nói rõ thiếu cái gì (đo gì, thử gì, trên dữ liệu nào), gắn đúng một loại T/M/D.
3. **Có căn cứ:** mỗi hạn chế trong bảng gap đã có câu trích nguyên văn và mục/trang của paper.
4. **Chỉ khẳng định trong phạm vi tài liệu đã tìm:** không viết “chưa ai làm”.
5. **Chỉ mô tả chỗ còn thiếu:** không chứa giải pháp của nhóm (giải pháp thuộc RQ) và không báo trước kết quả.

| Viết chưa hợp lệ | Sai ở đâu | Viết lại |
|---|---|---|
| “Chưa ai nghiên cứu LLM sinh unit test.” | Khẳng định tuyệt đối, không mẫu số, không nguồn (và thực tế đã có nhiều paper) | “Trong 12 paper, 4 paper (P2, P4, P5, P8) cùng nêu hạn chế chỉ đo coverage, chưa đo khả năng phát hiện lỗi; không paper nào trong bảng đo mutation score đủ tin.” |
| “Các nghiên cứu trước còn nhiều hạn chế.” | Mơ hồ, không chỉ ra thiếu gì, không kiểm lại được | Nêu từng hạn chế cụ thể, mỗi hạn chế một gap, kèm paper nêu |
| “Cần dùng GPT-4o mini để đo mutation score.” | Đây là giải pháp (thuộc RQ), không phải chỗ còn thiếu; “model mới hơn” cũng chưa đủ làm gap [**📖**](https://swt302.chiltq.workers.dev/fa26-se2043/#ly-dong-gop) | “… 3 paper (P1, P5, P10) cùng nêu chưa thử model nhỏ, chi phí thấp; không paper nào trong bảng giải quyết điều đó.” |
| “Chưa đo mutation score, nên RQ sẽ cho thấy LLM sinh test tốt hơn.” | Báo trước kết quả; gap không được nói RQ sẽ ra gì | Bỏ vế sau; kết quả mong đợi thuộc giả thuyết H0/H1 ở RBL-3 |

**RQ cho từng gap:** yếu tố nào của PICO bị thiếu theo loại gap thì đó là phần mới của RQ (GAP-T: I mới; GAP-M: O mới; GAP-D: P mới). Giữ nguyên các yếu tố còn lại của RQ ban đầu để RQ mới đổi ít nhất và vẫn dùng được kết quả Bước 1–2. RQ hợp lệ khi:

1. Đủ P/I/C/O; **O đo được bằng số**, tính được bằng công cụ hoặc ground truth có sẵn.
2. **Một RQ một gap:** không ghép hai gap bằng chữ “và”.
3. Ghi rõ RQ **khác RQ ban đầu ở yếu tố nào** (nếu khác) và nhãn tính mới (new / extension / replication). Đổi RQ thì báo giảng viên trước khi khoá.
4. Còn làm được trong thời gian thực nghiệm: kiểm ở Bước 3, mỗi cặp gap + RQ một cột chấm.

#### Lợi ích nếu lấp gap: trả lời “vì sao làm gap này?”

Mỗi cặp gap + RQ cần thêm **một câu lợi ích**, viết riêng với phát biểu gap: phát biểu gap nêu *điều các nghiên cứu trước còn thiếu* (điều 5 ở trên), câu lợi ích nêu *kết quả của RQ giúp ai, và giúp họ hiểu hoặc quyết định được điều gì*. [**📖 Vì sao, nguồn**](https://swt302.chiltq.workers.dev/fa26-se2043/#ly-loi-ich)

**Mẫu câu:** “Nhóm muốn biết [câu hỏi của RQ] để giúp [ai] [hiểu / quyết định điều gì], điều hiện nay họ chưa có căn cứ vì [gap]. Nếu kết quả [hướng 1] thì họ [làm gì]; nếu [hướng 2 hoặc chưa thấy khác biệt] thì họ [làm gì].”

Câu lợi ích hợp lệ khi đủ 4 điều:

1. **Có người dùng cụ thể:** vai trò và bối cảnh (đội kiểm thử dự án Java, người chọn công cụ sinh test, nhà nghiên cứu mảng X), không “mọi người”, “cộng đồng”.
2. **Có hậu quả của gap:** vì thiếu kết quả này nên hiện họ chưa quyết được, hoặc đang quyết dựa trên số đo không phù hợp.
3. **Đúng với mọi kết quả:** mỗi hướng kết quả (kể cả không bác bỏ H0) đều cho họ một việc làm được.
4. **Không hứa quá phần RQ đo:** qua phép thử “nếu [ai] muốn [mục tiêu], biết kết quả RQ có giúp họ làm được không?”.

| Viết chưa hợp lệ | Sai ở đâu |
|---|---|
| “Vì chưa ai làm.” | Đó là gap (chỗ thiếu), chưa nói lấp xong thì được gì |
| “Góp phần nâng cao chất lượng phần mềm.” | Đúng với mọi đề tài; không nêu ai, quyết định gì |
| “Chứng minh LLM sinh test tốt hơn người.” | Báo trước kết quả; kết quả ngược lại thì lợi ích mất |
| “Giúp doanh nghiệp tiết kiệm chi phí kiểm thử.” | RQ không đo chi phí doanh nghiệp: hứa quá phần đo được |

Hai gap cùng mạnh và cùng khả thi thì ưu tiên gap có câu lợi ích rõ hơn. Câu lợi ích dùng thẳng trong proposal §2 và slide GAP.

#### Ví dụ gap và RQ cho hai gap mạnh (12 paper trong bảng gộp)

| Gap | Phát biểu gap | RQ lấp gap | Khác RQ ban đầu |
|---|---|---|---|
| **A** (GAP-M), cũng là gap RQ ban đầu | Trong 12 paper, 4 paper (P2, P4, P5, P8) cùng nêu hạn chế chỉ đo coverage, chưa đo khả năng phát hiện lỗi; không paper nào trong bảng đo mutation score đủ tin (trong phạm vi tài liệu đã tìm). | Với 60 hàm Java từ repo của P4, unit test do GPT-4o mini sinh ra đạt mutation score (PIT) khác bộ test viết tay bao nhiêu? | Không khác (đây là RQ ban đầu) |
| **B** (GAP-T) | Trong 12 paper, 3 paper (P1, P5, P10) cùng nêu chưa thử model nhỏ, chi phí thấp; không paper nào trong bảng giải quyết điều đó (trong phạm vi tài liệu đã tìm). | Với cùng 60 hàm Java, unit test do model 7B chạy cục bộ đạt mutation score (PIT) khác GPT-4o mini bao nhiêu? | Khác ở I (model 7B) và C (GPT-4o mini thành đối chứng); P và O giữ nguyên |

*(Ví dụ minh họa.)* Cả hai gap đều mạnh, đi tiếp sang Bước 3: chấm khả thi cho cặp A và cặp B. Mỗi gap còn phải trả lời “vì sao gap này còn trống” (khối vàng ở trên).

#### Lợi ích nếu lấp gap (ví dụ)

- **Gap A:** Nhóm muốn biết unit test do GPT-4o mini sinh ra đạt mutation score khác bộ test viết tay bao nhiêu, để giúp đội kiểm thử dự án Java quyết định có dùng test do LLM sinh thay một phần test viết tay không; hiện họ chỉ có số coverage, mà coverage cao chưa cho biết test bắt được lỗi. Thấp hơn rõ: giữ test viết tay, LLM chỉ làm bản nháp. Đạt ngưỡng: có căn cứ dùng LLM cho phần test lặp lại. Chưa thấy khác biệt: báo khoảng tin cậy để biết cần mẫu lớn hơn hay đã đủ để quyết.
- **Gap B:** Nhóm muốn biết model 7B chạy cục bộ đạt mutation score khác GPT-4o mini bao nhiêu, để giúp đội không được gửi mã nguồn ra dịch vụ ngoài chọn có dùng model cục bộ không. Kém rõ: biết phải chấp nhận mất bao nhiêu điểm khi giữ mã trong nội bộ. Không kém quá ngưỡng: có căn cứ dùng model cục bộ.

#### Ví dụ bảng gap (12 paper trong bảng gộp)

| Hạn chế (viết gọn) | Paper nêu | Paper đã giải quyết | Còn lại | Kết luận |
|---|---|---|---|---|
| Chỉ đo coverage, chưa đo khả năng phát hiện lỗi | P2, P4, P5, P8 | không có | 4 paper | **Gap mạnh, GAP-M** |
| Chưa thử model nhỏ, chi phí thấp | P1, P5, P10 | không có | 3 paper | **Gap mạnh, GAP-T** |
| Chỉ thử trên Java | P3, P6 | không có | 2 paper | Gap yếu, GAP-D |
| Dataset nhỏ (dưới 100 hàm) | P7 | P9 (dùng 2.000 hàm) | 0 | Đã giải quyết, gạch |

*(Ví dụ minh họa.)* Gap RQ ban đầu (“chưa ai đo mutation score”, GAP-M) khớp dòng đầu tiên, còn lại 4 paper, nên rơi vào trường hợp “khớp gap mạnh”: giữ RQ, ghi “4 trên 12 paper”.

#### Nếu N_included < 12 (chưa đạt cổng P1): tìm bổ sung theo lớp L1–L3

1. Kiểm tra lỗi dedup/screening và xem yếu tố P/I/C/O nào còn thiếu.
2. PL phân công **một cách tìm bổ sung có mục tiêu** từ các lớp L1–L3 (bảng dưới).
3. Snowballing lùi + tiến mà từng thành viên đã làm ở Tuần 6 không cần lặp lại; chỉ dùng L2 nếu lượt đó bị bỏ sót hoặc cần kiểm tra cập nhật tính mới.
4. Cập nhật CSV, evidence table và PRISMA cho mọi record mới.
5. Vẫn dưới 12: báo PL và giảng viên để quyết định downscope hoặc điều chỉnh RQ trước khi khoá. Không đánh dấu P1 là đạt.

| Lớp | Hành động | Ghi gì |
|---|---|---|
| L1 | Search thẳng vào RQ: `"[can thiệp I]" AND "[task P]" AND "[metric O]"` trên Scholar + IEEE | Số kết quả + có phản chứng không |
| L2 | Chỉ khi cần bổ sung/kiểm tra cập nhật: vào Semantic Scholar, lấy paper mới nhất trong tập included, xem 10–15 paper đã cite nó (không lặp nếu đã làm ở Tuần 6) | Có paper nào trả lời RQ không |
| L3 | Tìm 1 bài survey/SLR về chủ đề (`"systematic review" AND [topic]`, từ 2023) | Survey có nhắc tới đúng cách tiếp cận của RQ không |

### Paper gần nhất và bảng căn hàng: gap đi từ paper nào

**Paper gần nhất** là paper trong bảng đối chiếu (bảng gộp và 2–3 paper tìm thêm ở việc 4) giống **RQ đã chốt** ở nhiều yếu tố P/I/C/O nhất. Mỗi RQ có một paper gần nhất; nhiều paper giống ngang nhau thì chọn paper có hạn chế trùng với gap, rồi đến paper mới hơn. Paper này đồng thời là căn cứ của nhãn tính mới là “paper gần nhất” trong bảng khác biệt ở proposal §3 (RBL-3), và là paper đầu tiên để đối chiếu kết quả ở phần bàn luận (RBL-5a). [**📖 Paper gần nhất**](https://swt302.chiltq.workers.dev/fa26-se2043/#t-paper-gan-nhat)

Gap được đề xuất từ **yếu tố PICO mà paper gần nhất còn hạn chế**; RQ đổi đúng yếu tố đó và giữ nguyên các yếu tố còn lại. Lập **bảng căn hàng** cho mỗi RQ:

1. **Cột Paper gần nhất:** P/I/C/O của paper đó. Paper không có đối chứng thì ô C ghi “không có”.
2. **Cột RQ nhóm:** giá trị của RQ; yếu tố giữ nguyên ghi “=”.
3. **Cột Khác ở đâu, căn cứ:** yếu tố có gap ghi loại gap kèm **bằng chứng**: câu trích hạn chế của paper gần nhất (mục/trang) **hoặc** số đếm từ bảng gap (“x trên N paper”). Yếu tố khác bị đổi theo chỉ hợp lệ khi là hệ quả bắt buộc của yếu tố có gap, kèm lý do (ví dụ: đổi I nên C phải là đối chứng phù hợp với I).

| Yếu tố | Paper gần nhất: P4 (2024) | RQ nhóm (gap A) | Khác ở đâu, căn cứ |
|---|---|---|---|
| P | 60 hàm Java trong repo của P4 | = | = |
| I | Unit test do GPT-4o mini sinh | = | = |
| C | Bộ test viết tay | = | = |
| O | Coverage | Mutation score (PIT) | **Gap A (GAP-M).** P4 tự nêu chỉ đo coverage (mục Threats, trích nguyên văn + trang); 4 trên 12 paper cùng nêu |

*(Ví dụ minh họa, tiếp ví dụ gap A ở trên.)* Một cột khác, có bằng chứng: RQ là extension so với P4.

**Đọc bảng:**

| Số yếu tố khác | Nghĩa là | Làm gì |
|---|---|---|
| 0 | Tái hiện (replication) | Báo PL và giảng viên; giữ và ghi rõ là tái hiện, hoặc đổi I hoặc C |
| 1 (yếu tố có gap) | Mở rộng (extension) | Giữ |
| 2, yếu tố thứ hai có lý do | Mới (new) | Giữ; ghi lý do ở cột căn cứ |
| 2 không có lý do, hoặc từ 3 | Paper đã chọn chưa phải paper gần nhất, hoặc RQ đi quá xa paper đó | Tìm lại paper gần nhất trong bảng đối chiếu; vẫn vậy thì thu hẹp RQ về gần paper gần nhất |
| Yếu tố có gap không có bằng chứng | Gap chưa có căn cứ | Lấy lại từ hạn chế paper nêu hoặc từ bảng gap |

Độ mạnh của gap vẫn theo phép đếm ở trên: paper gần nhất cho **chỗ neo**, bảng gap cho **độ mạnh**; gap được biện minh bằng cả mảng tài liệu, không dựa vào một paper (Creswell & Creswell 2023, chương 5, tr. 143 bản PDF). Bảng căn hàng ghi vào mục 3 của `rq-validation.md`, dùng lại ở proposal §3 (thêm dòng quy mô và metric) và là **slide đầu** khi trình bày gap. Ở RBL-3 tìm được paper gần hơn thì thay paper gần nhất, làm lại bảng và nhãn tính mới.

## Bước 3 · Rà khả thi lần cuối (cả nhóm, ngày 1–2)

Lúc đăng ký, nhóm đã xác nhận tải được dataset và chạy được 1 prompt trên vài mẫu. Bước này rà phần còn lại cho **toàn bộ thực nghiệm**: cỡ mẫu, ground truth, chi phí, thời gian. [**📖 Vì sao ưu tiên ground truth có sẵn**](https://swt302.chiltq.workers.dev/fa26-se2043/#ly-kha-thi)

1. **Chọn các cặp gap + RQ cần chấm:** gap và RQ ban đầu (bắt buộc), cộng gap mạnh khác kèm RQ nháp của nó (viết ở Bước 2) nếu nhóm đang cân nhắc đổi RQ sang đó. Mỗi cặp một cột chấm, để so sánh được.
2. Với mỗi gap, **ghi số cụ thể của nhóm** cho từng tiêu chí (bao nhiêu mẫu, bao nhiêu giờ, bao nhiêu đô la, repo nào) rồi mới chấm: ✅ an toàn, ⚠️ cần xử lý, ❌ không làm được. Chấm không kèm số thì không kiểm lại được.
3. Đếm số ❌ và ⚠️ của từng gap rồi quyết định theo quy tắc bên dưới. Ví dụ đã điền đủ ở mục ▸ ngay sau bảng quyết định.

| Tiêu chí | ✅ An toàn | ⚠️ Cần xử lý | ❌ Không làm được |
|---|---|---|---|
| Dataset | Public, tải được ngay (GitHub/Zenodo) | Cần crawl < 1 tuần | Phải thu thập > 1 tháng |
| API/Tool | Có free tier đủ cho N mẫu | Cần trả ≤ $5 tổng | Cần license đặc biệt |
| Tính toán | CPU laptop hoặc Colab T4 | GPU: dùng Kaggle/Colab free (hạn mức thay đổi, không đảm bảo) | Cần cluster riêng |
| Ground truth | Có sẵn hoặc không cần | Gán nhãn tay ≤ 5 giờ cả nhóm | Cần domain expert hoặc > 20 giờ |
| Code base | Paper liên quan có GitHub, adapt được | Có nhưng framework cũ | Không có, phải code từ đầu |
| Kỹ năng | Thư viện sẵn có | Cần học thêm < 1 tuần | Cần kiến thức research-level |
| Thời gian | Xong với ≥ 3 ngày dự phòng | Xong nhưng tight | Không đủ thời gian |

**Quyết định:**

- **Có bất kỳ ❌:** downscope ngay (bảng ▸ dưới) hoặc báo giảng viên để đổi RQ trước khi khoá.
- **Có ≥ 3 ⚠️:** rủi ro cao, viết kế hoạch xử lý trước khi viết proposal.
- **≤ 2 ⚠️ và không có ❌:** an toàn.
- **Nhiều gap cùng được chấm:** chọn gap có ít ❌ rồi ít ⚠️ nhất trong các gap mà RQ lấp được; gap mạnh nhưng khả thi thấp thì không chọn chỉ vì mạnh.

### Ví dụ chấm khả thi cho hai gap (số liệu minh họa)

Nhóm có 2 gap để cân nhắc, cả hai đều là gap mạnh ở Bước 2. **Cặp A** (gap A, GAP-M, là RQ ban đầu): đo mutation score của unit test do GPT-4o mini sinh ra. **Cặp B** (gap B, GAP-T): thử model 7B chạy cục bộ thay vì GPT-4o mini. RQ của hai cặp lấy từ ví dụ ở Bước 2.

| Tiêu chí | Gap A: chấm + số của nhóm | Gap B: chấm + số của nhóm |
|---|---|---|
| Dataset | ✅ 60 hàm Java lấy từ repo GitHub của paper P4, tải ngay | ✅ Dùng lại 60 hàm trên |
| API/Tool | ⚠️ 60 hàm × 5 lần × khoảng $0,003 ≈ $1, không còn free tier | ✅ Model chạy cục bộ, không tốn API |
| Tính toán | ✅ PIT chạy trên laptop, ước 2 giờ cho 300 lượt | ⚠️ Cần GPU ≥ 16 GB nhiều giờ; Kaggle free, hạn mức không đảm bảo |
| Ground truth | ✅ Mutation score tính tự động, không cần gán nhãn | ✅ Giống A |
| Code base | ⚠️ P4 có GitHub nhưng dùng Maven 3 cũ, phải sửa pom | ⚠️ Không paper nào có code chạy model này cho bài toán sinh test, phải tự viết |
| Kỹ năng | ⚠️ Chưa ai dùng PIT, ước học 3 ngày | ⚠️ Chưa ai chạy model cục bộ, ước học 4 ngày |
| Thời gian | ✅ Chạy 1 ngày trong Tuần 9, còn 3 ngày dự phòng | ⚠️ Chờ hàng đợi GPU, xong nhưng tight |
| **Đếm** | **0 ❌, 3 ⚠️** | **0 ❌, 4 ⚠️** |

**Quyết định:** cả hai gap không có ❌ nhưng đều từ 3 ⚠️ trở lên nên là rủi ro cao, phải có kế hoạch xử lý. Gap A ít ⚠️ hơn và là gap RQ ban đầu, nên giữ gap A. Kế hoạch ghi vào mục 4 của `rq-validation.md`: (1) API: chốt trần $5, dùng GPT-4o mini; (2) Maven: giao một người sửa pom trong Tuần 8, kiểm bằng pilot 5 hàm; (3) PIT: học trong Tuần 8, nếu sau 3 ngày chưa chạy được thì downscope xuống 30 hàm. *(Ví dụ minh họa.)*

### Bảng downscope: thu hẹp thế nào khi gặp vấn đề

| Vấn đề | Cách downscope |
|---|---|
| Dataset quá lớn | Lấy tập con nhỏ hơn, ghi rõ cách lấy và là limitation |
| API quá đắt | Dùng model nhỏ hơn (GPT-4o mini thay GPT-4o) |
| Cần annotation nhiều | Giảm N mẫu hoặc dùng proxy tự động |
| Pipeline quá phức tạp | Bỏ RQ2, chỉ làm RQ1 |

## Mẫu hai file nộp

Điền dần trong Bước 2 và Bước 3: cá nhân vào `SLR/rq-check.md` (ngày 1), PL tổng hợp vào `team-synthesis/rq-validation.md` (ngày 2).

### Mẫu `SLR/rq-check.md` (cá nhân)

```markdown
# Kiểm chứng RQ — phần của [Họ tên]

**Nguồn phụ trách:** [IEEE Xplore | ACM DL | ...]  
**Lớp bổ sung:** [L1 | L2 | L3 | không]  
**Ngày:** YYYY-MM-DD

## 1. Bảng đối chiếu paper (ứng viên từ nguồn của tôi)

| Paper | P | I | C | O | Hạn chế paper nêu | Chi tiết |
|---|---|---|---|---|---|---|

Kết luận phần của tôi: không có / có phản chứng [paper, giống mấy yếu tố]

## 2. Lớp tìm kiếm bổ sung (nếu được phân công)

[query nguyên văn, số kết quả, có phản chứng không]

## 3. Ghi chú khả thi từ các paper tôi đọc

[code có sẵn, cỡ mẫu họ dùng, chi phí, khó khăn họ báo]
```

### Mẫu `team-synthesis/rq-validation.md` (nhóm)

```markdown
# Kiểm chứng RQ — [mã RQ, ví dụ FA26-W4-03]

## 1. RQ (nguyên văn trên thẻ) + PICO

## 2. Bằng chứng làm nền (tóm tắt rq-evidence-map.md, N = [số] paper)

## 3. Phản chứng tổng hợp mọi nguồn

Nhãn tính mới của nhóm: new / extension / replication (nhãn trên thẻ: ...), lý do

Paper gần nhất: [tên, năm] (giống RQ chốt [x]/4 yếu tố)

| Yếu tố | Paper gần nhất | RQ nhóm | Khác ở đâu, căn cứ (bằng chứng gap / lý do đổi theo) |
|---|---|---|---|
| P | ... | = | = |
| I | ... | ... | ... |
| C | ... | ... | ... |
| O | ... | ... | ... |

## 4. Khả thi của từng gap đang cân nhắc (Bước 3)

| Tiêu chí | Gap A: số của nhóm | Chấm | Gap B (nếu có): số của nhóm | Chấm |
|---|---|---|---|---|

Đếm: A = [số] ❌ / [số] ⚠️; B = [số] ❌ / [số] ⚠️ → An toàn / Rủi ro cao (+ kế hoạch) / Downscope

Gap chọn: [A | B], vì ...

## 5. Gap mà RQ lấp (kết quả Bước 2)

Gap RQ ban đầu (1 câu, ghi TRƯỚC khi đếm, không sửa lại): "Chưa ai ..."

Loại: GAP-T / M / D

| Hạn chế | Paper nêu | Paper đã giải quyết | Còn lại | Mạnh/yếu | Loại |
|---|---|---|---|---|---|

Gap RQ ban đầu rơi vào: khớp gap mạnh / khớp gap yếu / không dòng nào khớp (giả định của nhóm) / khớp dòng đã gạch

Phát biểu gap (theo mẫu "Trong N paper, x paper (tên) cùng nêu ...; không paper nào trong bảng giải quyết"), mỗi gap mạnh một dòng, dùng thẳng trong proposal §2:

Gap A (loại ...): [...]  
RQ lấp gap A (P/I/C/O, O đo được bằng số): [...]  
Khác RQ ban đầu ở: [...]  
Gap B (nếu cân nhắc): [...]  
RQ nháp: [...]

Lợi ích nếu lấp gap (mỗi gap một câu, không gộp vào phát biểu gap):

Nhóm muốn biết [...] để giúp [ai] [hiểu / quyết định gì]; nếu [kết quả 1] thì [...]; nếu [kết quả 2 / chưa thấy khác biệt] thì [...]

Vì sao gap còn trống: chưa ai để ý / khó, tốn kém / có thể đã thử nhưng không hiệu quả (paper: ...)

Loại: GAP-T (công cụ/kỹ thuật chưa được thử) / GAP-M (khía cạnh chưa được đo) /
      GAP-D (domain hoặc quy mô dữ liệu còn thiếu)

## 6. Quyết định: giữ RQ / đổi I hoặc C (đã báo giảng viên ngày ...)
```

## Checklist trước khi nộp

- [ ] Mỗi người có bảng đối chiếu P/I/C/O và hạn chế với từng paper cụ thể từ nguồn của mình
- [ ] Nhóm đã ghi **gap RQ ban đầu** bằng một câu, viết trước khi đếm, và nói rõ nó khớp gap mạnh, gap yếu, không dòng nào, hay dòng đã gạch
- [ ] Nhóm có bảng gap: hạn chế đã gạch cái paper khác giải quyết, gap mạnh (≥ 3 paper) có loại GAP-T/M/D
- [ ] Nếu N < 12: đủ 3 lớp L1, L2, L3
- [ ] Nhãn tính mới của nhóm có lý do, đã so với nhãn trên thẻ RQ
- [ ] Có paper gần nhất (giống RQ chốt nhất trong bảng đối chiếu) và bảng căn hàng: yếu tố có gap có bằng chứng, yếu tố đổi theo có lý do; bảng là slide đầu khi trình bày gap
- [ ] Đã so với 2–3 paper mạnh nhất 12 tháng gần đây; đóng góp không chỉ là “model mới hơn”
- [ ] Khả thi chấm cho từng gap đang cân nhắc, mỗi tiêu chí có số cụ thể của nhóm (không chỉ ✅/⚠️/❌); gap chọn không có ❌, hoặc đã có kế hoạch downscope
- [ ] Mỗi gap mạnh có phát biểu theo mẫu (có “x trên N paper” và tên paper, không “chưa ai làm”, không chứa giải pháp), kèm một dòng “vì sao gap còn trống”; gap yếu thì ghi rõ là gap yếu
- [ ] Mỗi cặp gap + RQ có **câu lợi ích**: ai dùng kết quả, để hiểu hoặc quyết định gì, mỗi hướng kết quả (kể cả không bác bỏ H0) thì họ làm gì; không “vì chưa ai làm”, không “nâng cao chất lượng phần mềm”
- [ ] Mỗi gap mạnh đang cân nhắc có một RQ đủ P/I/C/O, O đo được bằng số, một RQ một gap, ghi rõ khác RQ ban đầu ở yếu tố nào
- [ ] Mọi thay đổi RQ đã báo giảng viên trước khi khoá

**Bước tiếp theo:** cả nhóm họp chốt kết quả kiểm chứng, viết proposal → xem RBL-3.

---

© L.T.Q.Chi · SWT302 · Tài liệu học tập trong học phần; không sao chép hoặc phân phối lại khi chưa được phép.
