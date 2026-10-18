# Search log — T.Duy · Semantic Scholar + Google Scholar

## 1. Nhật ký query

| Lần         | Chuỗi thực chạy (nguyên văn)                                                                                                                                                                                              | CSDL             | Trường/bộ lọc                    | Ngày      | Kết quả nguồn / thực thu | Ghi chú                                                                |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------- | ------------------------------------ | ---------- | ---------------------------- | ----------------------------------------------------------------------- |
| S2-A (exact) | `("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing") AND ("fault detection" OR "mutant detection" OR "bugs found")` | Semantic Scholar | Tìm mặc định                     | 15/10/2026 | Site báo không khớp / 0   | 250 là số gợi ý sau nới, không phải exact A.                     |
| GS-A         | `("REST API testing" OR "natural language requirement" OR "RESTestBench") AND ("equivalence partitioning" OR "boundary-value analysis" OR "boundary testing") AND ("fault detection" OR "mutant detection" OR "bugs found")` | Google Scholar   | Mặc định; IC-Y≥2020 áp khi lọc | 15/10/2026 | 27 (ước lượng đầu 37)  | Đã lấy hết 27; trang tiếp theo 0.                                  |
| S2-A-relaxed | `(REST API testing OR natural language requirement OR RESTestBench) AND (equivalence partitioning OR boundary-value analysis OR boundary testing) AND (fault detection OR mutant detection OR bugs found)`                   | Semantic Scholar | Mặc định; IC-Y≥2020 áp khi lọc | 15/10/2026 | 250 gợi ý / thu 10         | Site không khớp exact A, tự bỏ dấu nháy; chưa lấy hết gợi ý. |
| S2-seed      | `"Combining TSL and LLM to Automate REST API Testing"`                                                                                                                                                                       | Semantic Scholar | Mặc định; IC-Y≥2020 áp khi lọc | 15/10/2026 | 1 / thu 1                    | Tra title seed; bản trùng vẫn ghi 01.                                |
| GS-B-random  | `("REST API" OR "RESTful API") ("equivalence partitioning" OR "boundary value") random`                                                                                                                                      | Google Scholar   | Mặc định; IC-Y≥2020 áp khi lọc | 15/10/2026 | khoảng 206 / thu 10         | Mới lấy trang đầu.                                                  |
| S2-B-random  | `REST API equivalence partitioning boundary value random`                                                                                                                                                                    | Semantic Scholar | Mặc định; IC-Y≥2020 áp khi lọc | 15/10/2026 | 25 / thu 10                  | Mới lấy trang đầu; không coi TLDR là abstract.                    |
| GS-MacroHive | `"Automated functional and robustness testing of microservice architectures"`                                                                                                                                                | Google Scholar   | Mặc định; IC-Y≥2020 áp khi lọc | 15/10/2026 | thu 1                        | Tra cứu title từ đầu mối; không tạo nguồn mới ngoài GS.       |
| GS-budget    | `("REST API" OR "RESTful API") "equivalence partitioning" "boundary value" "budget" "random"`                                                                                                                                | Google Scholar   | Mặc định; IC-Y≥2020 áp khi lọc | 15/10/2026 | 7 / thu 7                    | Đã lấy hết 7 kết quả.                                             |

## 2. Xử lý dữ liệu

Đợt 15/10:66 lượt search/seed; snowball Tuần 6+L2:92 lượt. Bổ sung kết quả âm 18/10:17 lượt. Tổng 175 lượt, gộp 39 lượt trùng →136 paper duy nhất; 01/02 mỗi file 136 dòng.

Một dòng/paper trong 01/02 theo protocol§4. DOI là khóa ưu tiên; thiếu DOI dùng title+năm, không gộp chỉ vì tên tool giống nhau. Giữ nguyên các lượt nguồn trong occurrences_json và merged_record_ids;39 lượt trùng được gộp trước V1, không phải 39 paper bị loại ở V1. DOI/publisher/Crossref/OpenAlex và các lượt tìm lại full-text chỉ để xác minh; không cộng thành discovery mới. Không suy ra EC-A từ HTTP 403/429/timeout. Bài loại/chờ giữ trong 02; 03 chỉ Include.

## 3. Nới chuỗi và cập nhật toàn văn

Giữ nguyên String A ở GS-A và S2-A. S2 tự bỏ dấu nháy được ghi riêng; các query random/budget và title lookup ghi đúng chuỗi thực chạy ở bảng trên. Không sửa IC/EC. Việc tìm sau hạn 05/10 được khai báo ở§7; không tự coi là hạn chung của nhóm đã được PL đổi.

Trạng thái bộ gốc 15/10/2026: FAMRES chưa có toàn văn; Agentic có PDF nhưng chưa xác minh journal/conference (IC-T). Cả hai giữ Unsure; lượt 18/10 có thêm TD-0159 Unsure(IC-T). Có toàn văn đã đọc (số cập nhật ở PRISMA); hai bài Include được giữ nguyên.

## 4. Snowballing — vòng 1

Seed TD-0002 · 10.5753/sbes.2025.9670 · RestTSLLM (SBES 2025): đã có PDF 11 trang và Include; sát Category-Partition/EP/BVA, có mutation metric. References từ S2 và PDF; citations từ GS và S2. Không chạy tiếp từ bài mới.

| Seed DOI               | Vòng | Hướng | Số đã lướt/ghi nhận | Số lượt ghi nhận vào 01 (lịch sử) | Include mới |
| ---------------------- | ----: | ------- | ------------------------: | ----------------: | -----------: |
| 10.5753/sbes.2025.9670 |     1 | Lùi    |                        84 |                84 |            0 |
| 10.5753/sbes.2025.9670 |     1 | Tiến   |                         7 |                 7 |            0 |

Lùi: S2 thu 27 references (header 50; chưa lấy đủ 50) +57 entries trong References PDF. Tiến: GS2 +S2 5 citations. Cùng bài có thể lặp giữa nguồn; các số 84/7 là lượt trước bỏ trùng. Bảng dưới giữ số lượt nhập lịch sử; sau chuẩn hóa, các lượt được gộp vào occurrences_json, không còn mỗi lượt là một dòngCSV.

Snowballing 92 lượt → 65 unique trong nhánh; giao search 1 → mới 64. Lọc: 64−36=28 đọc toàn văn; loạiV2 28; Include mới 0. Đợt gốc search 61+snowball mới 64=125. Sau 17 lượt bổ sung(11 bài mới), search 72+snowball mới 64=136.

Số Include cuối và các lý do loại theo từng nhánh: prisma-flow.md; quyết định từng ID: 02_after_screening_v 1.csv.

## 5. RBL-2 — L2 kiểm tra cập nhật tính mới (18/10/2026)

Semantic Scholar: tra đúng title K191, 1 kết quả; trang citing-papers hiển thị 1 citation, đã đọc 1/1 (không có đủ 10–15). K136: tra title hiển thị 29 kết quả rộng; chỉ dùng đối chiếu ngày seed, không thu 29 records. K191 ghi 18/05/2026 trên S2, mới hơn K13612/04/2026; publisher/nhóm ghi ICST 2026, không dùng venue tự gán sai trên S2.

Seed K191 DOI 10.1109/ICST 69053.2026.00064 → bài mới TD-0158 Using OAI Overlay to Enhance REST API Fuzzing (S2 be 94657 a 32 abfcd 5 f 2 c 2100748 cf 1 a 629 bb 6 f 56 b; arXiv 2607.04325). Thêm 1 vào 01, đọc PDF 10 trang, loạiV2 IC-I: can thiệp Overlay/examples, không EP/BVA. Không thêm seed-lookup K191/K136 thành paper mới vì chỉ đối chiếu seed của tập gộp. Không snowball tiếp từ TD-0158.

Tuần 6 vẫn 84 lùi+7 tiến=91 lượt; L2 thêm 1 tiến → tổng 92 lượt, đóng góp 64 bài mới sau bỏ trùng. Include mới 0. Query bổ trợ đã chạy: `"Using OAI Overlay to Enhance REST API Fuzzing"`; `"RESTestBench" "mutation" 2026 REST testing`; chỉ tra cứu/cập nhật paper đã có hoặc TD-0158, không nhân đôi lượt discovery.

So nghiên cứu gần đây (18/10/2025–18/10/2026): TD-0015, RESTestBench TD-0029 và TD-0158. Chọn do gần I, P/O, và baseline fuzzing/cùng thời gian tương ứng; không khẳng định đây là 3 bài mạnh nhất toàn ngành. RestTSLLM 09/2025 ngoài cửa sổ 12 tháng, vẫn là ứng viên cá nhân chính. Chi tiết kết quả, gap và khả thi: rq-check.md.

Phân nhánh theo lần phát hiện đầu(discovery_branch):search 72+snowball 64=136. Trong 175 occurrences, search riêng 73 unique, snowball riêng 65 unique, giao 2. TD-0130 được snowball tìm trước rồi xuất hiện lại ởGS-NEG-wide nên giữ nhánh snowball; không đổi lịch sử để khớp số.


## 6. Bổ sung kết quả âm và kiểm seed —18/10/2026

| Lần | Query nguyên văn | Nguồn/trường/lọc | Nguồn báo/thực thu | Kết quả |
|---|---|---|---|---|
| GS-NEG-wide | `"REST API" ("negative result" OR "did not improve" OR "fails") ("equivalence partitioning" OR "boundary value")` | GoogleScholar, mặc định; IC-Y áp khi lọc | khoảng 88/10 trangđầu |5 bài đã có+5 bài mới; đây là lượt dò rộng, chưa thu hết 88 |
| GS-NEG-exact | `"REST API" ("negative result" OR "did not improve") ("equivalence partitioning" OR "boundary value")` | GoogleScholar, mặc định; IC-Y áp khi lọc |7/7; không có trang tiếp |1 bài đã có+6 bài mới; hoàn tất tập 7 kết quả |
| S2-L2-K33 | `Implementation of an Integrated Executive Dashboard on the PPMPP Portal as a Digital Instrument for Institutional Quality Assurance at Politeknik Negeri Bali` | S2, mặc định |No Papers Found/0 record |không truy cập được citing-list; không đồng nghĩa 0 citations |
| S2-L2-K 100 a | `FDRRestTest: Feedback-Driven Logical Testing for REST APIs` | S2, mặc định |No Papers Found/0 record |lookup seed nhóm, không thêmdiscovery |
| S2-L2-K 100 b | `FDRRestTest` | S2, mặc định |No Papers Found/0 record |xác nhận giới hạn tìm seed trên S2 |

17 lượt GS bổ sung →11 paper mới TD-0159–TD-0169;6 lượt khớp bài đã có(TD-0003, TD-0130, TD-0132, TD-0070, TD-0016, TD-0156). Tất cả lưu metadata/query trong occurrences_json. Không coi snippet là abstract.

Kết quả 11 bài mới: V1 loại 9(TD-0161/69:IC-Y; TD-0162:EC-S; TD-0163/64/65/66:IC-T; TD-0167/68:IC-P); đọcV2 hai PDF(TD-0159:UnsureIC-T; TD-0160:EXCLUDE IC-E). Không có Include mới.

**Chọn seed theo ngày, không theo năm in:** rà 11 DOI đang ghi 2026 trong 03 của các nguồn bằng Crossref và PDF/publisher. K33 online 07/10/2026(10.2991/978-94-6239-805-4_13); K100 publisher 05/10/2026; K12710/08; K19204/06; TD-001529/05; K8926/05; K19118/05; K13612/04; K8203/02. K02 online 16/09/2025 dù năm in 2026. K43 metadata chỉ ghi 2026, chưa xác minh ngày cụ thể: **chưa kết luận chắc seed mới nhất toàn tập**. K33 là ngày online mới nhất đã xác minh, thử trước K100; cả hai không tìm thấy recordS2. Lượt K191 trước đó giữ là phương án bổ trợ(1/1 citation), không gọi là seed mới nhất. Không đủ 10–15 citation để đọc trên seed mục tiêu; L2 ghi giới hạn, chưa đánh dấu hoàn tất bao phủ.

**Kết quả âm:** TD-0159§VI.D, p 9:Structured làm các model trùng bộ failure modes(Jaccard 1.00), không phải EP+BVA-vs-random. TD-0160§6.1, p 10:CBIE không có lợi ích thêm khi mô tả<5 tokens; bài loại IC-E nên chỉ làm đầu mối, không làm bằng chứng kết quả định lượng. Trong 7 kết quả query chặt chưa thấy thử nghiệm âm trực tiếp cho RQ; không khẳng định chưa ai thử.

Tra cứu xuất bản/full-text 18/10 chỉ xác minh paper đã ghi nhận: [Agentic arXiv](https://arxiv.org/abs/2510.27417) chưa có journal-ref/DOI conference; [FAMRES publisher](https://link.springer.com/chapter/10.1007/978-981-95-1746-6_39) chưa có toàn văn mở; TD-0159 có [accepted list](https://srds-conference.org/index.php/accepted-papers/) và [program](https://srds-conference.org/index.php/program/), chưa xác minh proceedings. [TD-0160 publisher](https://www.svedbergopen.com/index.php/ijaiml/article/view/1603) xác nhận 05/09/2026,12 trang; Table 1/2 là cấu hình, không thỏa IC-E.

## 7. Lệch protocol và trạng thái kiểm

| Ngày ghi | Việc thực tế | Lý do/trạng thái |
|---|---|---|
|18/10/2026|Ghi hồi cứu tìm bổ sung 15/10 và cập nhật L2/kết quả âm 18/10 sau hạn protocol 05/10|Theo yêu cầu T.Duy hoàn thiện cá nhân/RBL-2; ghi riêng phụ lục cập nhật. Chưa có xác nhận PL thay hạn nhóm; không ghi lùi ngày hay tự sửa protocol |
|18/10/2026|Trường GS/S2 mặc định, không ép Title/Abstract/Keywords; lọc năm khi screening|Giới hạn giao diện; giữ query thật và số thực thu; IC/EC không đổi |
|18/10/2026|Chuẩn hóa 01/02 từ 158 lượt thành một dòng/paper, sau bổ sung có 136 dòng|Đúng bước dedup trướcV1;175 occurrences và 39 lượt trùng vẫn truy vết trongCSV, không mất dữ liệu nguồn |
|18/10/2026|Phân biệt Tuần 6 snowball 91 lượt với L2 cập nhật 1 lượt|Không lặp snowball từ seed Tuần 6; không chạy tiếp từTD-0158 |
|18/10/2026|AI/tool hỗ trợ thu metadata, đọcPDF, đối soát và sửa hồ sơ|Giữ dấu vết nguồn và đối chiếu kết quả với toàn văn |

**Kiểm chứng tool:** đối soát 175 occurrences/136 canonical; nguồn GS báo 88 ước lượng nhưng chỉ 10 được thu, query chặt 7/7; so 5 mẫu metadata TD-0002/TD-0015/TD-0158/TD-0159/TD-0160 với PDF/publisher, giữ raw metadata riêng. Chưa chạy lại đúngquery để đánh giá độ ổn định số kết quả; không ghi PASS cho kiểm này. Lịch sử đã đọc giữ trong CSV; bản PDF dùng chung được dẫn tới Paper-source. Bản lưu toàn văn cá nhân đã được bỏ sau khi chuyển sang RQ check.

**Giai đoạn hiện tại:** Bước 2 — RQ check cá nhân, bài #31–#38 theo phân công; xem rq-check.md.

**Tự kiểm evidence P2–P5 (18/10/2026):** P2=2/2 hàng có Tool/LLM (100%); P3=2/2 có kết quả số từ Table 3 (100%); P4=2/2 có hạn chế tác giả nêu (100%); P5=2/2 metric có tên, đơn vị/định nghĩa. Mở lại TD-0002 PDF p8 và TD-0015 PDF p6 xác nhận số chính. Đã giữ 8 cột nội dung, không thêm cột Evidence vào bảng nộp. Không thay quyết định, số Include hoặc PRISMA.


## 8. Bước 2 cá nhân — bài #31–#38 (18/10/2026)

Theo phân công mới, đọc đúng số hàng trong `team-synthesis/evidence-table-merged.md`: **31 K93, 32 K100, 33 K127, 34 K136, 35 K166, 36 K168, 37 K191, 38 K192**. Đọc Methods/Evaluation/Threats/Discussion và các Table/Figure tương ứng trong tám PDF `Paper-source/`; trích hạn chế nguyên văn kèm trang vào rq-check §1. Không đổi quyền sở hữu nguồn, không cộng tám bài vào 01/02/03.

**Tra cứu nghiên cứu gần đây, 18/10/2026, cửa sổ 18/10/2025–18/10/2026:** công cụ web-search mặc định, không lọc năm trên giao diện; năm/venue đối chiếu PDF và nguồn chính thức. Không chạy lại query Scholar/S2 trong lượt này.

| Query nguyên văn | Kết quả dùng / lý do chọn | Phạm vi ghi nhận |
| --- | --- | --- |
| `"FDRRestTest" REST APIs 2026` | [Dagstuhl/publisher](https://drops.dagstuhl.de/entities/document/10.4230/LIPIcs.ESEM.2026.20): ESEM, 05/10/2026; 12 services, fixed-time và fixed-request | Lookup K100 đã có; 0 record mới |
| `"SBFT Tool Competition 2026" "REST League"` | [University of Verona](https://www.di.univr.it/?ent=pubbdip&id=1193127&lang=it), [artifact tác giả](https://zenodo.org/records/18434145): benchmark 11 APIs/317 operations trong PDF | Lookup K136 đã có; 0 record mới |
| `"RESTing-LLAMA" REST API Fuzzing` | Lookup K192, đối chiếu PDF ASIACCS2026: 15 apps/4 models. Mở [ACM DOI](https://dl.acm.org/doi/10.1145/3779208.3785383) trả 403; dùng bản PDF đã lưu để đọc | 0 record mới; không suy thiếu full-text do web 403 |

Web-search không cung cấp tổng số kết quả đáng tin cho ba query này: **không ghi số ước lượng**. Ba paper được chọn vì cùng task, thiết kế ngân sách và quy mô/venue; K191 thấp hơn vì SUT đóng, K127 một ứng dụng; K93/K166/K168 ngoài cửa sổ. Không gọi ba bài là mạnh nhất toàn ngành. Chưa thấy bài nào trong tám bài trả lời trọn RQ; giữ kết luận trong phạm vi đã đọc.

**Phát hiện cần PL review:** K166 PDF p8/Verifiability có link code + dataset dù bảng gộp ghi NOT_REPORTED; K100 96/120 là mẫu kiểm oracle gộp, không phải toàn bộ 96 lỗi riêng của FDRRestTest; K93 ít bugs hơn foREST trong Table 3 dù PRTT cao; K192 lượt đo throughput cùng thời gian không kiểm vulnerabilities. Chỉ ghi đính chính tại rq-check cá nhân, không sửa bảng gộp.

**Số giữ nguyên:** 175 lượt − 39 trùng = 136 paper; V1 loại 76 → cần toàn văn 60 → đã đọc 59; V2 loại 55, Unsure đã đọc 2, Include 2. Snowball 92 lượt/64 paper mới/0 Include. 03/evidence/PRISMA = **2/2/2**, không phát sinh screening hay snowball mới. Nhãn trên thẻ cần PL đối chiếu khi tổng hợp RQ check; phần nhóm/Bước 3 do nhóm thực hiện.


**Dọn bản toàn văn cá nhân — 18/10/2026:** theo yêu cầu T.Duy sau khi phần Include đã được chốt trong bảng gộp, bỏ thư mục fulltext cá nhân. Hai PDF Include giữ nguyên tại `Paper-source/39-TD-0002.pdf` và `Paper-source/40-TD-0015.pdf`. Các trường fulltext_file/pdf_file chuyển sang bản dùng chung nếu khớp SHA-256; các bản không còn lưu được bỏ đường dẫn cục bộ. Giữ metadata, nguồn toàn văn, số trang, trạng thái và quyết định đã đọc trong lịch sử; không coi việc xóa bản lưu là chưa từng đọc hoặc là EC-A. Số 59 đã đọc (55 PDF + 4 text) là lịch sử screening, không phải số file còn lưu; Include vẫn 2, snowball Include mới 0.
