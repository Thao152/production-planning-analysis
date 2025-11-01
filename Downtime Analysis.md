# 🧩 Phân tích chi tiết: Downtime Analysis

## 1️⃣ Tổng quan  
Tổng thời gian downtime trong giai đoạn phân tích: **5.12K giờ**, chiếm **7.65%** tổng thời gian vận hành.  
Tỷ lệ **hiệu suất máy (Machine Utilization)** đạt **92.35%**, cho thấy mức khai thác khá cao.  

Downtime có xu hướng tăng mạnh từ **tháng 8 đến tháng 10**, trùng với giai đoạn đơn hàng nhiều và yêu cầu sản phẩm phức tạp.  

---

## 2️⃣ Phân tích nguyên nhân downtime  

| Nguyên nhân chính         | Tỷ lệ (%) | Nhận xét |
|----------------------------|-----------|----------|
| **Machine issue**          | 38%       | Lỗi máy móc, hư hỏng cơ khí và sensor là nguyên nhân lớn nhất, đặc biệt ở nhóm máy SC06 và SC03. |
| **Lack of manpower**       | 20%       | Do sử dụng lao động thời vụ, mùa cao điểm thiếu nhân lực vận hành → máy phải ngừng chờ người. |
| **PM (Preventive Maintenance)** | 16% | Bảo trì định kỳ chiếm tỷ trọng lớn, tuy nhiên cần tối ưu lịch bảo trì vào giai đoạn thấp điểm. |
| **Setup / Changeover**     | 13%       | Thời gian setup kéo dài khi thay đổi mẫu mã hoặc khuôn phức tạp, ảnh hưởng tiến độ các máy chạy liên tục. |
| **Clean / Outage**         | 10%       | Tác động nhỏ, nhưng có thể giảm nếu tối ưu quy trình vệ sinh định kỳ và cấp điện ổn định. |

---

## 3️⃣ Phân tích theo máy  

| Máy  | % Downtime | Nhận xét |
|------|-------------|----------|
| **SC06** | 14.5% | Là máy có đơn hàng không ổn định, mẫu mã đa dạng, thường Leadtime dài, thiếu nhân lực sẽ ưu tiên ngưng máy |
| **PG02** | 11.2% | Máy backup, thường chỉ chạy khi có thiếu hụt công suất → downtime cao do thiếu nhân lực. |
| **SC03** | 9.9% | Hoạt động ít, độ khó của mẫu mã chạy trên máy này không ổn định. |
| **CT02**| 9.9% | Máy hoạt động full workload, chủ yếu ngưng máy do thiếu nhân lực.
| **SC04 / SC01** | 8–9% | Máy hoạt động full workload, mẫu sản phẩm có độ khó tăng dần dẫn đến thường xuyên ngưng máy để tinh chỉnh sản phẩm.|

---

## 4️⃣ Xu hướng downtime theo tháng  

Downtime giảm mạnh trong **quý 2 (tháng 4–6)**, sau đó tăng nhanh vào **tháng 8–10**, đạt đỉnh **896 giờ** vào tháng 8.  
Nguyên nhân chính là:  
- **Khối lượng đơn hàng tăng cao**,  
- **Sản phẩm yêu cầu kỹ thuật phức tạp**,  
- **Thiếu nhân lực thời vụ**,  
- Và **nhiều máy phải ngừng để căn chỉnh chất lượng sản phẩm**.

---

## ✅ 5️⃣ Kết luận & Đề xuất  

- **Tỷ lệ downtime 7.65%** là chấp nhận được nhưng vẫn có thể giảm thêm bằng tối ưu lịch bảo trì và setup.  
- Nhóm máy **SC06, SC03** cần được theo dõi sát, đặc biệt trong giai đoạn cao điểm.  
- **Thiếu nhân lực (20%)** là yếu tố khó khắc phục tức thời → cần có **kế hoạch nhân lực linh hoạt** và **pool dự phòng nhân sự**.  
- Đề xuất:  
  - Áp dụng **bảng cảnh báo downtime > 8%** theo tháng.  
  - Rà soát **chu kỳ bảo trì** để giảm chồng chéo với thời gian sản xuất cao điểm.  
  - Triển khai **chuẩn hóa quy trình setup & cleaning**, đào tạo nhân viên thao tác nhanh.  
