# Nhật ký đọc 20 nguồn giảng viên — Lâm

Ngày kiểm: **20/10/2026 (Asia/Saigon)**. Nhánh làm việc: `Lam`. Bảng đích: [evidence-table.md](evidence-table.md#b-bổ-sung-20-paper-do-giảng-viên-cung-cấp--20102026). ID theo đúng thứ tự danh sách người phụ trách gửi: SLR → 2 nền → 16 mới → 1 khác.

Đã thử mở cả 20 link đầu vào; nhiều DOI/Semantic Scholar trả lỗi truy cập nên tìm nguồn publisher, tác giả hoặc preprint đúng tên. `FT` chỉ xác nhận đã đọc phần phương pháp, thực nghiệm/kết quả và giới hạn liên quan trong toàn văn; không có nghĩa đã tái lập hoặc screening chính thức. `ABS` dùng bằng chứng abstract/preview; `META` chưa có nội dung nghiên cứu. Các URL dưới đây là nguồn thực sự đọc được, không phải chỉ link DOI được chuyển tiếp thành công.

| Mã | Mức | Nguồn đã đọc / bản dùng | Locator kiểm tra và điểm cần theo dõi |
|---|---|---|---|
| GV-01 | ABS | [Publisher preview](https://link.springer.com/article/10.1134/S0361768825700422) | Abstract; Publication information. Phân biệt issue 2025 với online 27/02/2026. Thân bài subscription. |
| GV-02 | FT | [PDF tác giả, 12 trang](https://damorim.github.io/publications/fazzini-etal-issta18.pdf) | §§3–4; §5.1/PDF7; §5.2/PDF8–9, Table 1; §5.3/PDF9–10. Năm 2018 là nguồn nền theo chỉ định. |
| GV-03 | ABS | [Publisher abstract](https://www.sciencedirect.com/science/article/pii/S0920548924001119) | Highlights, Abstract, Data availability. Issue April 2025; thông tin đầu vào 2024 có thể chỉ online-first, chưa xác minh publication history. |
| GV-04 | FT | [HTML v1](https://arxiv.org/html/2604.25862v1); [PDF trong repo](../../tung/SLR/update-paper/R2R-01-RESTestBench-2026.pdf) | §3.3–3.4/PDF4–6; Table 3/PDF6; §4, Fig.3/PDF7; §6/PDF9. Không thay số paper bằng mẫu 45 của nhóm. |
| GV-05 | FT | [HTML v1](https://arxiv.org/html/2601.17903v1); [PDF trong repo](../../tung/SLR/update-paper/R2R-04-Prompt-Based-REST-API-Test-Amplification-in-Industry-2026.pdf) | §§3–4; Tables 2–3; §5.3; §7. Ba prompts không phải ba lần chạy độc lập. Không gộp với K02 (PetStore) dù có quan hệ prior work. |
| GV-06 | FT | [HTML v1](https://arxiv.org/html/2607.23963v1); [PDF trong repo](../../tung/SLR/update-paper/R2R-03-RESTOR-2026.pdf) | §§3–5; Fig.3, §5.4/Fig.7; §7; Appendix B. F1 là key-field identification, adoption là proxy utility. |
| GV-07 | ABS | [Abstract trên trang đồng tác giả](https://homes.cs.washington.edu/~mernst/pubs/rest-oracle-tosem2025-abstract.html); [PDF index](https://idus.us.es/server/api/core/bitstreams/8062d4b0-2153-4d5c-9a0a-5e607d8a6edc/content) | Abstract đọc được và kết quả khớp trang tác giả; thân PDF trả 403. Không nhầm AGORA 2023 hoặc RCR DOI 10.1145/3771281 với bài này. |
| GV-08 | FT | [Preprint HTML v1](https://arxiv.org/html/2501.02875v1); [artifact tác giả](https://github.com/specs-feup/paper-metford) | §§3–4; Tables 12–13; §5. Số liệu từ preprint; bản JSS trả 403, chưa kiểm khác biệt phiên bản xuất bản. |
| GV-09 | FT | [PDF từ trang tác giả](https://jhe16.github.io/files/FSE26.pdf) | §§3–4, Tables 4–7; §5.2/PDF20; §7 Data Availability. C đối chiếu random/search dưới time cap; không suy uniform input. |
| GV-10 | FT | [HTML v1](https://arxiv.org/html/2507.18316v1) | §§3–4; Table 1; Tables 9–10; §7. Dùng số mutation score Table 9 cho đúng class/method, không trộn total/average từ bảng khác. |
| GV-11 | FT | [HTML v2](https://arxiv.org/html/2508.16318v2); [supplement tác giả](https://zenodo.org/records/15529767) | §III; §IV-A (OKAMI, AGORA+ unary), §IV-B–C (response mutations/bugs); §V. 90% oracle coverage của kết hợp không phải 90% killed mutants. |
| GV-12 | FT | [HTML v1](https://arxiv.org/html/2501.12862v1); [PDF bản FSE trên UCL](https://discovery.ucl.ac.uk/10218052/1/fse25_industry_paper_arXiv.pdf) | §2; §§3–6, Table 8; §8. Header HTML v1 có DOI/template cũ không khớp; giữ DOI FSE 2025 người phụ trách gửi, không sao chép DOI header. |
| GV-13 | ABS | [Abstract hội nghị chính thức](https://conf.researchr.org/details/icsme-2025/icsme-2025-papers/36/N-wa-Enhancing-MLIR-Fuzzing-with-LLM-Driven-Generation-and-Adaptive-Mutation) | Abstract. Số 55 là reported bugs, chỉ 18 confirmed/fixed; chưa kiểm mẫu/budget/model trong PDF. |
| GV-14 | FT | [Publisher record](https://phes.com.ua/ojs/index.php/www/en/article/view/239); [bản toàn văn do tác giả đăng](https://www.researchgate.net/publication/411970875_BEYOND_FLAKY_TEST_DETECTION_USING_THE_MODEL_CONTEXT_PROTOCOL_FOR_INTELLIGENT_TEST_FAILURE_DIAGNOSIS_IN_CICD) | Materials and methods; pp.72–73/Table 1; pp.78–79 limitations. Chỉ đọc phần article, không lấy thông tin từ recommendations/references bên dưới. |
| GV-15 | FT | [HTML v1](https://arxiv.org/html/2609.27806v1) | §IV-D; §V dataset/Table I; §V-E; §V-F. Abstract “39 APIs” khác thân bài “39 endpoints/7 services”; dùng thân bài. Chỉ xác nhận preprint. |
| GV-16 | ABS | [Abstract ASE chính thức](https://conf.researchr.org/details/ase-2025/ase-2025-papers/69/Multi-dimensional-Assessment-of-CrowdSourced-Testing-Reports-via-LLMs) | Abstract: ba dimensions và ba applications; chưa có số agreement/time. Chưa dùng bài TOSEM mở rộng 2026 để điền số cho ASE 2025. |
| GV-17 | ABS | [Hồ sơ nghiên cứu Waseda](https://waseda.elsevierpure.com/en/publications/llm-based-fuzzing-method-using-ui-based-input-value-generation-fo/) | Abstract + metadata pp.16–20; IEEE yêu cầu JavaScript/kiểm tra truy cập. Không nhầm bài ICCE 2025 về so sánh model hoặc bài IoT seed generation khác. |
| GV-18 | FT | [HTML v1](https://arxiv.org/html/2607.09345v1); [artifact tác giả](https://zenodo.org/records/21295460) | §§III–IV, Table V, §IV-C; §VI. 58% là chưa quy được nguyên nhân từ code+log, không phải recall của detector. Chỉ xác nhận preprint, không gán accepted ICSE 2027. |
| GV-19 | FT | [Publisher PDF, 8 trang](https://www.ijsat.org/papers/2025/1/2232.pdf) | §§3–4/PDF2–3; §6/PDF4–5; Appendix/PDF5–7. Không thấy quantitative outcome Table/Figure; 2 figures là sơ đồ. |
| GV-20 | META | [IEEE landing page](https://ieeexplore.ieee.org/document/10707721) | Trang chỉ hiện title/khung IEEE. Tên/năm/DOI giữ theo đầu vào; chưa có bằng chứng tool, dataset, metric hay kết quả. |

## Kiểm tra trước khi gộp chính thức

- 20 nguồn đầu vào có ID duy nhất; không có DOI/arXiv trùng trong các dòng chính của bảng gộp 42 khi kiểm ngày này. RESTestBench/RESTOR/Prompt-Based đã xuất hiện ở tài liệu bổ sung RBL-2 và PDF Tùng, nên phải khử trùng theo paper khi gộp.
- Giữ riêng provenance “GV cung cấp”; không ghi thành lượt search ACM của Lâm. Chưa thay CSV screening, N=42, PRISMA, rq-evidence-map hoặc RQ.
- Ưu tiên lấy toàn văn cho **GV-01, GV-03, GV-07, GV-13, GV-16, GV-17**, và cả abstract/toàn văn **GV-20**. Các ô chưa xác minh được giữ nguyên trạng thái chờ; không điền từ tiêu đề, nguồn tổng hợp hoặc trí nhớ.
- Khi xét vào tập SLR chính, áp dụng lại IC/EC. Việc dùng nguồn 2018 hoặc nguồn ngoài REST làm nền không tự nới protocol của tập chính.
