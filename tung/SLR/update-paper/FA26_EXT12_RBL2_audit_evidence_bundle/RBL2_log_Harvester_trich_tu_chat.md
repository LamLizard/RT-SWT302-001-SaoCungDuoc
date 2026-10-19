# Nhật ký Harvester — bản chép từ nội dung người dùng đã cung cấp

**Tính chất bằng chứng:** bản chép từ nhật ký Harvester được cung cấp ngày 18/10/2026, không phải bản xuất phản hồi HTTP gốc của SerpAPI. Chuỗi truy vấn và số liệu bên dưới được giữ theo nhật ký nguồn.

## Nhật ký chạy query (tạo bởi RBL Paper Harvester)

| Lần | Chuỗi gửi đi (nguyên văn người dùng báo) | CSDL | Trường tìm | Bộ lọc | Ngày chạy | Số kết quả nguồn báo | Số lấy về | Ghi chú |
|---|---|---|---|---|---|---:|---:|---|
| v1 | `"RESTestBench"` | Google Scholar (SerpAPI) | Google Scholar | as_ylo = 2025 | 18/10/2026 16:33 | 3 | 3 | không đếm vào PRISMA (review-protocol §3); dữ liệu qua dịch vụ bên thứ ba SerpAPI; không có DOI/abstract đầy đủ; đã dùng 1 lượt search SerpAPI |
| v2 | `("REST API" OR "RESTful API" OR "web API") ("mutation testing" OR "mutation score" OR "mutant detection" OR "mutant killing")` | Google Scholar (SerpAPI) | Google Scholar | as_ylo = 2025 | 18/10/2026 16:33 | 62 | 100 | không đếm vào PRISMA (review-protocol §3); dữ liệu qua dịch vụ bên thứ ba SerpAPI; không có DOI/abstract đầy đủ; đã dùng 5 lượt search SerpAPI |
| v3 | `("REST API" OR "RESTful API" OR "web API") ("equivalence partitioning" OR "boundary value analysis" OR "boundary-value analysis" OR "boundary testing")` | Google Scholar (SerpAPI) | Google Scholar | as_ylo = 2025 | 18/10/2026 16:34 | 90 | 82 | không đếm vào PRISMA (review-protocol §3); dữ liệu qua dịch vụ bên thứ ba SerpAPI; không có DOI/abstract đầy đủ; đã dùng 5 lượt search SerpAPI |

## Tổng hợp

- Tổng trước dedup: **185** · Sau dedup: **139** (bỏ **46** bản trùng) · Đã chọn xuất vào 01: **139**.
- Ghi chú: bản ghi từ Semantic Scholar / Google Scholar (SerpAPI) **KHÔNG đếm vào PRISMA** theo `review-protocol.md §3` (đây là tuyên bố của log, không phải tự kiểm tra file review-protocol).

**Giới hạn diễn giải:** v2 báo 62 hits nhưng lấy 100; cột `query` trong CSV có thêm `AND` cho Q2 và Q3 so với log. Nguyên nhân khác biệt chưa được xác minh.

**Xác nhận loại trùng — 18/10/2026:** người phụ trách xác nhận công cụ đã loại 46 bản trùng từ 185 bản ghi, giữ 139 bản ghi. Phần xử lý này thuộc phạm vi của người phụ trách; việc không lưu phản hồi HTTP gốc không được xem là yêu cầu phải kiểm lại dedup trong hồ sơ cá nhân.
