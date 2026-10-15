# PRISMA — phần cá nhân T.Duy

Theo quy định nhóm: GS/Semantic và phương pháp bổ sung ghi riêng; không đại diện PRISMA toàn nhóm. Các lượt nhập có nguồn search chưa xác nhận được ghi rõ, chưa được coi là lượt tìm của GS/Semantic.

```mermaid
flowchart TD
 A["Nguồn chính: 0 lượt trong bộ cá nhân"] --> C["Tổng đã nhập: 32 lượt"]
 B["Bổ sung: 5 seed GS + 10 Semantic + 7 backward + 10 CSV mới"] --> C
 C --> D["Bỏ trùng 3; còn 29 paper"]
 D --> E["V1 loại 11; chuyển toàn văn 18"]
 E --> F["Đã đọc toàn văn 5"]
 E --> G["Chờ toàn văn 13"]
 F --> H["Include 1; Exclude 2; Unsure 2"]
```

32−3=29;29=11+18;18=5+13;5=1+2+2. Không cộng 10 dòng re-export vào raw count. 250 Semantic là tổng UI do người dùng báo, không phải số bản ghi đã nhận. Chưa kết luận thất bại truy xuất cuối cùng: reportsNotRetrieved=0; 13 pending. Include cần nhóm xác nhận.
