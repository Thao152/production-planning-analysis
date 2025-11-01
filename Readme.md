# 🏭 Phân tích hiệu suất kế hoạch sản xuất & nguyên nhân trễ giao hàng tại nhà máy nhựa

## 📊 1. Tổng quan (Overview)
Dự án nhằm đánh giá **mức độ tuân thủ kế hoạch sản xuất (Plan Adherence)**, **thời gian trễ (Delay Time)**, **downtime máy móc**, và **tỷ lệ giao hàng đúng hạn (On-time Delivery)** tại **nhà máy nhựa**.  
Phân tích giúp xác định khu vực hoặc máy có hiệu suất thấp, từ đó đề xuất hướng cải thiện trong công tác lập và thực hiện kế hoạch sản xuất.

Các **dashboard** được xây dựng bằng **Power BI**, sử dụng dữ liệu nội bộ từ hệ thống kế hoạch và báo cáo sản xuất thực tế.

---

## 🧩 2. Dữ liệu sử dụng (Dataset)
**Nguồn dữ liệu:** Google Sheets nội bộ (10 tháng gần nhất)

Gồm các bảng:
- **Kế hoạch sản xuất:** Mã máy, sản lượng kế hoạch, thời gian kế hoạch  
- **Thực tế sản xuất:** Sản lượng thực tế, thời gian thực tế, downtime  
- **Đơn hàng:** Mã khách hàng, ngày giao hàng, sản lượng đặt  
- **Bảng downtime:** Lý do ngừng máy (setup, test, thiếu nhân lực, bảo trì, v.v.)

---

## 📈 3. Các chỉ số chính (Key Metrics)

| Chỉ số | Diễn giải | Giá trị |
|--------|------------|---------|
| **Plan Adherence (%)** | Tỷ lệ sản lượng thực tế đạt so với kế hoạch | ≈ 98% |
| **Delay Time (%)** | Tỷ lệ thời gian trễ so với kế hoạch | ≈ -6.35% |
| **Downtime (%)** | Thời gian ngừng máy trên tổng thời gian chạy | 10.6% |
| **On-time Delivery (OTIF)** | Tỷ lệ đơn hàng giao đúng hạn | 99.9% (chỉ 1 đơn trễ) |

---

## 📊 4. Dashboard & Phát hiện chính (Key Findings)

### 🔹 1. Production Quantity Analysis
- Tổng sản lượng kế hoạch với sản phẩm ống đạt **63.2M**, so với công suất tối đa **72M**.  
- Sản lượng thực tế đạt **62M** (≈ 98% kế hoạch) → mức tuân thủ rất tốt.  
- Giai đoạn tháng 4 - tháng 7 sản lượng giảm mạnh do **nhu cầu đặt hàng của khách giảm**, trong khi **khả năng lưu kho hạn chế** khiến nhà máy **không thể sản xuất vượt nhu cầu thực tế**.  
- 👉 **Đề xuất:** Xem xét **mở rộng kho lưu trữ** hoặc **đa dạng hóa khách hàng trong mùa thấp điểm** để duy trì sản lượng ổn định.
### 🔹 2. Delay Time Analysis
- Tổng thời gian trễ: **-3.92K giờ (~ -6.35%)**.  
- Tháng 9 ghi nhận chênh lệch cao nhất (**-842 giờ, -14%**).  
- Các máy **PG02, SC04, SC01** có tỷ lệ delay cao nhất (>9%)
- Phân tích:
  + SC01 và SC04 thường chạy full công suất để đáp ứng các đơn hàng đặc thù, nên không thể phân bổ sang máy khác.
Trong giai đoạn đầu năm, khách hàng chủ yếu đặt các sản phẩm tiêu chuẩn, dễ gia công, nên tiến độ được đảm bảo.
Tuy nhiên, từ giữa năm trở đi, tỷ lệ sản phẩm phức tạp và yêu cầu kỹ thuật cao tăng, khiến máy phải dừng thường xuyên để tinh chỉnh, kiểm tra chất lượng, dẫn đến delay tăng đáng kể.
  + PG02 là máy backup, được kích hoạt khi máy chính gặp sự cố hoặc cần bù tiến độ.
Tuy nhiên, thực tế cho thấy máy ít được vận hành kịp thời do thiếu nhân lực và chưa có quy trình rõ ràng về việc kích hoạt máy dự phòng, dẫn đến delay cục bộ trong giai đoạn cao điểm.

👉 **Đề xuất:**

- Tăng cường bảo trì phòng ngừa (Preventive Maintenance) cho nhóm máy chạy full load (SC01, SC04).

- Theo dõi xu hướng delay theo độ phức tạp sản phẩm để lập kế hoạch hợp lý hơn.

- Thiết lập cảnh báo sớm khi thời gian tinh chỉnh vượt ngưỡng cho phép.

- Rà soát quy trình kích hoạt máy backup (PG02) và bố trí nhân lực dự phòng trong giai đoạn cao điểm để đảm bảo máy backup hoạt động hiệu quả.
### 🔹 3. Downtime Analysis
- Tổng downtime: **1.47K giờ (10.6%)**.  
- Nguyên nhân chính:
  - Machine issue: **46%**
  - Setup: **20%**
  - Thiếu nhân lực: **12%**
- Downtime tăng mạnh ở **tháng 8–10**, đặc biệt ở **MC SC06, SC03, SC04**.  
- Riêng **tháng 10**, downtime do **thiếu nhân lực** chiếm **27% tổng thời gian ngừng máy**, cho thấy ảnh hưởng đáng kể từ thiếu hụt nhân sự tạm thời.

### 🔹 4. On-time Delivery Analysis
- Tổng đơn giao: **839**, chỉ **1 đơn trễ** → **OTD = 99.9%**.  
- Khách hàng **QHA** có sản lượng lớn nhất → cần theo dõi sát do khối lượng cao.  
- Biểu đồ **Total Work Orders in Storage < 1 Day (by Customer)** phản ánh các đơn hàng có thời gian lưu kho dưới 1 ngày — tức là sản xuất và xuất hàng gần như liên tục, không có tồn đệm.

- Đáng chú ý, trong tháng 10, khách hàng QHA chiếm 6.5 triệu sản phẩm, khiến có 9 đơn hàng chỉ lưu kho dưới 1 ngày trước khi giao. Điều này cho thấy áp lực giao hàng cao và mức tồn kho thành phẩm đang ở ngưỡng tối thiểu, dễ phát sinh rủi ro trễ nếu có sự cố bất ngờ trong sản xuất hoặc vận chuyển.

👉 **Đề xuất:**
- Xem xét mở rộng năng lực lưu kho thành phẩm tạm thời cho nhóm khách hàng có sản lượng lớn (như QHA).

- Phân bổ lịch giao hàng hợp lý hơn, tránh dồn sản lượng lớn vào cùng kỳ ngắn.

- Đánh giá mức tồn kho an toàn tối thiểu (safety stock) cho từng nhóm khách hàng để hạn chế rủi ro trễ khi khối lượng tăng đột biến.
---

## 🧠 5. Công cụ & Phương pháp (Tools & Methods)
- **Power BI** – trực quan hóa dữ liệu & dashboard tổng hợp  
- **Google Sheets** – xử lý & chuẩn hóa dữ liệu gốc  
- **DAX** – xây dựng measure KPI (Plan Adherence, Delay, OTD, v.v.)  
- **Data Modeling** – ghép bảng kế hoạch, thực tế và đơn hàng  

---
## ✅ 6. Kết luận & Đề xuất (Insights & Recommendations)

- **Hiệu suất sản xuất** duy trì ổn định (Plan Adherence > 95%).  
- Cần theo dõi **downtime tăng** ở một số máy (đặc biệt nhóm SC).  
- **Nguyên nhân Setup (20%)** cần được phân tích sâu hơn → có thể tối ưu bằng **kế hoạch batch sản phẩm tương đồng**.  
- **Thiếu nhân lực** là yếu tố ảnh hưởng đáng kể đến tiến độ sản xuất, đặc biệt trong tháng 10 khi chiếm tới 27% tổng downtime.  
  Nguyên nhân chủ yếu đến từ việc **công ty sử dụng lao động thời vụ**, khiến **giai đoạn cao điểm dễ xảy ra thiếu hụt nhân sự**, dù kế hoạch máy móc đã được cân đối hợp lý.  
  Tình trạng này kéo dài làm giảm khả năng phản ứng linh hoạt khi phát sinh sự cố hoặc cần tăng ca bù sản lượng.  
- **OTD đạt 99.9%** → quy trình giao hàng và kiểm soát tiến độ vẫn hoạt động rất hiệu quả.

### 💡 Đề xuất:
- Áp dụng **cảnh báo tự động khi Delay > 2%**.  
- Rà soát **kế hoạch bảo trì định kỳ** cho nhóm máy SC.  
- Phân tích chi tiết **setup time theo sản phẩm** để giảm thời gian chuyển đổi.  
- **Theo dõi và đánh giá năng lực nhân sự theo ca**, xây dựng **chính sách nhân lực linh hoạt** (pool nhân sự dự phòng hoặc đào tạo chéo) để hạn chế rủi ro thiếu người trong mùa cao điểm.


---

## 🔗 Dashboard Power BI

📁 Tải Power BI file: [Report Plan.pbix](./Report%20Plan.pbix)

---
## Dax Formulas
(/DAX_formulas.md).

## 🔍 Phân tích chi tiết
1. [Delay Analysis](./01.Delay%20Analysis.md)
2. [Downtime Analysis](./02.Downtime%20Analysis.md)
3. [Machine Utilization Analysis](./03.Machine%20Utilization%20Analysis.md)
4. [OTD Analysis](./04.OTD%20analysis.md)
5. [Capacity Analysis](./05.%20Capacity%20Analysis.md)


---

📅 *Thực hiện bởi:* Nguyễn Thị Phương Thảo 
📍 *Công cụ:* Power BI | Google Sheets | DAX | Data Modeling  
