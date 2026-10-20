# Nhật ký đọc 17 paper nền giảng viên — Lâm

Ngày cập nhật: **20/10/2026 (Asia/Saigon)**. Nhánh `Lam`. Bảng đích: [evidence-table.md](evidence-table.md#b-paper-nền-giảng-viên-cung-cấp--17-bài-có-toàn-văn).

**Tập hiện hành: 17 bài, đều có PDF local và đã đọc toàn văn các phần liên quan.** Ba nguồn không có PDF đã bị loại theo yêu cầu người phụ trách, ghi vết loại tại [search-log §9](search-log.md#9-loại-nguồn-không-có-pdf-và-đổi-tên-file--20102026). Không còn hàng chờ đọc/ABS/META trong evidence table.

## Mapping mã và PDF hiện hành

- Dòng #1–#2 trong bảng Lâm là hai bài ACM cũ; dòng #3–#19 là GV-01–GV-17.
- Tên file PDF có dạng `NN-GV-XX-Ten-ngan.pdf`: NN = 43–59 trong thư mục nguồn chung; GV-XX = mã khớp evidence table. Cột “Vị trí gốc” giữ thứ tự bài trong danh sách 20 link ban đầu; không phải mã GV hiện hành.
- Đã kiểm SHA256 trước/sau đổi tên: nội dung của 17 PDF không đổi. Các file #01–#42 giữ nguyên.
- Trang là **số trang PDF đếm từ 1**. Các URL artifact lấy từ text/references/URI annotations; chưa xác minh khả năng tải hoặc chạy artifact.
- Đã render và xem bảng AGORA+ (PDF18/27), Nüwa (PDF8), IoT (PDF4), Crowdsourced (PDF9/10) để đối chiếu cột, đơn vị và mẫu số.

| Mã hiện hành | Dòng Lâm | PDF local / số trang | Vị trí gốc trong 20 link | Locator đọc lại | Kết quả đối chiếu |
|---|---|---|---|---|---|
| GV-01 | 3 | [43 · YAKUSU](../../Paper-source/43-GV-01-YAKUSU.pdf), 12 trang | 2 | §§3–5/PDF3–10; Table 1/PDF9; ref.[13]/PDF11 | FT giữ 37/62 = 59,7%; 62 là phần tái hiện được sau lọc từ 100 report. Bổ sung trang dự án được paper dẫn. |
| GV-02 | 4 | [44 · RESTestBench](../../Paper-source/44-GV-02-RESTestBench.pdf), 10 trang | 4 | §3.3–3.4/PDF4–6; Table 3/PDF6; Fig.3/PDF7; §§4–6/PDF7–9 | FT, arXiv v1; giữ 106/228 và Sonnet 92% precise single-step. Không đổi thành cỡ mẫu 45 của nhóm. |
| GV-03 | 5 | [45 · Prompt-Based](../../Paper-source/45-GV-03-Prompt-Based-REST-API-Amplification.pdf), 8 trang | 5 | §§3–4/PDF3–4; Tables 2–3/PDF5; §§5.3–7/PDF6–7; ref.[10]/PDF8 | FT; giữ số liệu prompt 3; thêm URL RESTCov. Header có FSE 2026, vẫn nhận diện bằng arXiv:2601.17903v1; không tự xác minh xuất bản từ template header. |
| GV-04 | 6 | [46 · RESTOR](../../Paper-source/46-GV-04-RESTOR.pdf), 22 trang | 6 | §4/PDF9; §5/PDF10–17; §5.2.1/PDF11 (Fig.3/PDF12), Fig.7/PDF16; §7/PDF18–19; Data Availability/PDF20 | FT; PDF1 ghi PACMSE 3/ISSTA, Article ISSTA094, October 2026, DOI 10.1145/3832185. Bổ sung metadata này; một lần training/evaluation và không công khai artifact vẫn giữ. |
| GV-05 | 7 | [47 · AGORA+](../../Paper-source/47-GV-05-AGORA-Plus.pdf), 37 trang | 7 | §4.1/PDF17–19; Table 3/PDF18; §4.3/PDF25–28, Table 4/PDF27; §5/PDF28–30; §6–7/PDF30–31 | **ABS → FT**. Precision 68% ở 50 calls và 80% ở 10K; 1.369 assertions, 2,5M output errors, FDR 48%; 32 bugs chỉ 17 confirmed. P·/I◐/C·/O◐; không có nhánh random-input đối chứng. |
| GV-06 | 8 | [48 · METFORD](../../Paper-source/48-GV-06-METFORD.pdf), 25 trang | 8 | §§3–4/PDF4–17; Tables 12/13/PDF16/17; §5/PDF18–19 | FT, **vẫn là preprint 2501.02875v1**, không phải bản JSS cuối. Giữ score 15,6/17,5 và runtime 6,45%; khác biệt kills chịu ảnh hưởng flakiness. |
| GV-07 | 9 | [49 · ArrayDiff](../../Paper-source/49-GV-07-ArrayDiff.pdf), 24 trang | 9 | §§3–4/PDF6–19; RA/GA baseline/PDF13; Table 7/PDF19; §5.2/§7/PDF20; ref.[83]/PDF24 | FT; giữ 19 bugs/8 changes/10 FP trong 37 reviewed differences. Bổ sung Zenodo. C✓ theo rubric rộng: RA ablation cùng 10h × 5, không phải uniform REST requests. |
| GV-08 | 10 | [50 · YATE](../../Paper-source/50-GV-08-YATE.pdf), 12 trang | 10 | §§3–4/PDF3–7; Table 1/PDF6; Tables 9–10/PDF10; §7/PDF10–11 | FT, arXiv v1; xác nhận **Total** 41,6/47,9 khác **Average** 44,0/51,1. Giữ totals và 4.296/21.249 LLM calls; chưa có artifact riêng được xác minh. |
| GV-09 | 11 | [51 · SATORI](../../Paper-source/51-GV-09-SATORI.pdf), 13 trang | 11 | §III/PDF3–5; §IV/PDF5–10; Tables II/III/IV/PDF7/8/9; §V/PDF10 | FT, arXiv v2; giữ F1 74,3% vs 69,3% cho unary-comparable oracles, 18 detected bugs. Mutation trên JSON response; không đổi thành O✓. |
| GV-10 | 12 | [52 · Meta ACH](../../Paper-source/52-GV-10-Mutation-Guided-Meta.pdf), 12 trang | 12 | §2/PDF2–3; Table 2/PDF5; Tables 5–8/PDF8–9; §8/PDF10 | FT; sửa diễn giải **9.095 là build và pass existing tests**, 31.677 là generated, 4.660 candidate non-equivalent. Giữ 571 tests và 277 không thêm line coverage. |
| GV-11 | 13 | [53 · Nüwa](../../Paper-source/53-GV-11-Nuwa.pdf), 12 trang | 13 | §III/PDF3–6; §IV–V/PDF6–9; Table II/PDF8; §VI-B/PDF10; §IX/ref.[56]/PDF11–12 | **ABS → FT**. Thêm GPT-4o, 24h × 5, GitHub; Table II có 56/16/18 bugs, khác tập 55 báo cáo/18 confirmed (16 fixed) ở §V-A. Dùng số bảng thay headline tỉ số không rõ mẫu số; C✓ nhờ random syntax generator cùng time budget. |
| GV-12 | 14 | [54 · Beyond Flaky](../../Paper-source/54-GV-12-Beyond-Flaky-Test.pdf), 23 trang | 14 | Methods/PDF9–13; Table 1/PDF14; Table 2/PDF15; limitations/PDF19–20 | FT; giữ time ranges; 167 là sessions (có phiên không gặp failure), không phải số failures. Tỉ lệ 52/31/17% là ước lượng không có per-session logs, không dùng như accuracy. |
| GV-13 | 15 | [55 · DualMine](../../Paper-source/55-GV-13-DualMine.pdf), 12 trang | 15 | §IV/PDF3–6; §V/Table I/PDF6; ablations/PDF9; §V-E–F/PDF10; Data Availability/ref.[6]/PDF11 | FT; giữ 39 endpoints/7 services, mean qua 5 runs. **Bổ sung artifact riêng** anonymous.4open.science/r/dualmine; trước chỉ tìm thấy APIPilot. |
| GV-14 | 16 | [56 · Crowdsourced](../../Paper-source/56-GV-14-Crowdsourced-Report-Assessment.pdf), 13 trang | 16 | §§III–IV/PDF3–7; §V-A/PDF7–8; Tables IV/VI/PDF9/10; §V-C/PDF10–11 | **ABS → FT**. Thêm 64 crowdworkers, 1.588 tests/235 defect reports, models và 6 experts; QWK theo app/dimension. Avg.* là metric so với điểm trung bình, không trung bình 6 metric. Không suy κ thành detection accuracy. |
| GV-15 | 17 | [57 · IoT UI fuzzing](../../Paper-source/57-GV-15-IoT-UI-Fuzzing.pdf), 5 trang | 17 | §III/PDF2–3; §IV-A–B/PDF3–4; Table II/PDF4; §IV-C/PDF4–5 | **ABS → FT**. Thêm Mistral-7B, G/M 20/80, seeded buffer overflow và DVWA; 3 lần đo time-to-first-crash gồm inference. I◐/C◐/O◐ chỉ rubric gần, không program mutation score. |
| GV-16 | 18 | [58 · How Far](../../Paper-source/58-GV-16-How-Far-Flaky-Tests.pdf), 15 trang | 18 | §§III–IV/PDF4–9; Table V/PDF8; §VI/PDF10–11; ref.[22]/PDF14 | FT; giữ flaky-class F1 và 42%/58%; PDF dẫn artifact **21102431**, khác record web **21295460** của lượt trước. Bảng hiện hành ưu tiên DOI được PDF dẫn; chưa khẳng định hai record là cùng phiên bản. |
| GV-17 | 19 | [59 · ITA](../../Paper-source/59-GV-17-Intelligent-Test-Automation.pdf), **9 trang** | 19 | §§3–4/PDF2–3; Figures 1–2/PDF2–3; §6/PDF4–5; Appendix/PDF5–7 | FT; bản local 9 trang, khác 8 trang web đã đọc. Vẫn chỉ workflow và mô tả định tính, chưa có quantitative outcome để đáp ứng IC-E; không thay kết luận bằng số trang hay config values. |

## Phạm vi sử dụng

- FT là mức truy cập và trích xuất, không tự thay quyết định screening. METFORD vẫn dùng preprint; ITA vẫn thiếu bằng chứng định lượng IC-E dù có toàn văn.
- Merge/map hiện có59 bài; PRISMA42 không thay đổi. RESTestBench, Prompt-Based và RESTOR có bản sao ở tài liệu của Tùng, phải khử trùng theo paper khi gộp.
- Các mã GV trong search-log §7–8 thuộc danh sách 20 nguồn trước khi lọc. Từ §9, tra mã hiện hành theo mapping trên. Không dùng mã lịch sử để chọn file theo tên mới.

## Tái thẩm định PICO trực tiếp từ PDF —20/10/2026

Đã đọc các trang phương pháp/thực nghiệm liên quan trong 17 PDF, xem bảng/figures khi cần. Dấu, lý do và locator cho 68 ô được đồng bộ trong [bảng evidence](evidence-table.md) và [đối chiếu cá nhân](rq-check.md); phạm vi trang đã đọc nằm ở bảng mapping phía trên, SHA256 được ghi trong hồ sơ kiểm chứng của đợt đọc PDF. 67 ô phân loại được; P của GV-13 giữ ? vì chưa xác minh deployment/source đủ điều kiện P◐, không suy thành ·.

- GV-05: P◐→·; I·→◐ ở mức domain/type request generators thực sự được cấu hình và chạy, không phải EP+BVA primary.
- GV-09: P◐→· do APIs online/source unavailable; giữ I·C·O◐.
- GV-13: P◐→?; giữ I◐C·O◐; chạm đã xác nhận2/4, ghi riêng?P.
- GV-04/12/14/16/17 giữ····, nay có căn cứ riêng từngô. RESTOR KillRate là reward trên response variants; Crowdsourced rarity score chấm reports đầu vào; random CV củaHowFar không phải random input baseline.
- Sửa locator RESTOR Fig3/Fig4→PDF12 (phân tíchF1 ởPDF11); GV-10 9095 build và pass existing tests; GV-14 64 crowdworkers.

Đợt đọc PDF đã đồng bộ kết quả vào bảng Lâm, merge, map và rq-check Lâm; chưa chạy artifact. Câu RQ và trạng thái kiểm chứng hiện hành được tổng hợp tại [rq-validation](../../team-synthesis/rq-validation.md).
