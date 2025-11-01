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
- Một số tháng (tháng 4, 5) sản lượng giảm mạnh → khả năng do **downtime** hoặc **thiếu nguyên liệu**.

### 🔹 2. Delay Time Analysis
- Tổng thời gian trễ: **-3.92K giờ (~ -6.35%)**.  
- Tháng 9 ghi nhận chênh lệch cao nhất (**-842 giờ, -14%**).  
- Các máy **PG02, SC04, SC01** có tỷ lệ delay cao nhất (>9%) → cần xem xét lại **phân bổ kế hoạch** và **setup**.

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
- Ngoài ra, biểu đồ **Total Work Orders in Storage < 1 Day (by Cus)** giúp theo dõi các đơn hàng có nguy cơ trễ cao.  
Các đơn này được hệ thống đánh dấu để ưu tiên xử lý, nhằm đảm bảo duy trì tỷ lệ OTD ở mức gần tuyệt đối (99.9%).  
Cơ chế cảnh báo sớm này hỗ trợ đáng kể trong việc **phòng ngừa trễ hàng**, thay vì chỉ phát hiện sau khi vi phạm lịch giao.
- **Hệ thống cảnh báo sớm** đã giúp kiểm soát các đơn có thời gian lưu kho <1 ngày.

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
👉 [Xem Dashboard Power BI](https://github.com/Thao152/production-planning-analysis/blob/main/Report%20Plan.pbix)

---

## 🔍 Phân tích chi tiết
- [Phân tích trễ kế hoạch (Delay Analysis)](analysis/Delay_Analysis.md)  
- [Phân tích hiệu suất máy (Machine Utilization)](analysis/Utilization_Analysis.md)  
- [Phân tích downtime (Downtime Analysis)](analysis/Downtime_Analysis.md)  
- [Phân tích giao hàng đúng hạn (OTD Analysis)](analysis/OTD_Analysis.md)

---

📅 *Thực hiện bởi:* Nguyễn Thị Phương Thảo 
📍 *Công cụ:* Power BI | Google Sheets | DAX | Data Modeling  
