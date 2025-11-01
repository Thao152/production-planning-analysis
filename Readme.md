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
| **Plan Adherence (%)** | Tỷ lệ sản lượng thực tế đạt so với kế hoạch | ≈ 99% |
| **Delay Time (%)** | Tỷ lệ thời gian trễ so với kế hoạch | ≈ -6.35% |
| **Downtime (%)** | Thời gian ngừng máy trên tổng thời gian chạy | 7.65% |
| **On-time Delivery (OTIF)** | Tỷ lệ đơn hàng giao đúng hạn | 99.9% (chỉ 1 đơn trễ) |

---
## 🧭 4. Phương pháp phân tích (Methodology Introduction)

Dự án được thực hiện theo **khung phân tích hiệu suất sản xuất (Manufacturing Performance Analysis Framework)** — một phương pháp dựa trên KPI, kết hợp giữa **phân tích dữ liệu vận hành**, **trực quan hóa bằng Power BI**, và **đánh giá nguyên nhân gốc (Root Cause Analysis)**.  

Phương pháp này giúp nhà máy:
- **Đo lường mức độ tuân thủ kế hoạch sản xuất** (Plan Adherence, Delay).  
- **Phân tích downtime máy móc và nhân sự** để xác định điểm nghẽn.  
- **Đánh giá hiệu suất sử dụng máy móc (Machine Utilization)** và năng lực nhà máy.  
- **Theo dõi tỷ lệ giao hàng đúng hạn (On-time Delivery – OTD)** và phát hiện sớm rủi ro tiềm ẩn.  
- **Đưa ra khuyến nghị cải tiến vận hành** dựa trên dữ liệu thực tế.  

---

### ⚙️ Cấu trúc phân tích

Phân tích được chia thành nhiều module, mỗi module phản ánh một nhóm chỉ số hiệu suất chính (KPI):

| Module | Mục tiêu phân tích | File |
|---------|--------------------|------|
| 1️⃣ **Delay Analysis** | Phân tích chênh lệch giữa kế hoạch và thực tế sản xuất | [`01.Delay_Analysis.md`](./01.Delay_Analysis.md) |
| 2️⃣ **Downtime Analysis** | Xác định nguyên nhân ngưng máy và mức độ ảnh hưởng | [`02.Downtime_Analysis.md`](./02.Downtime_Analysis.md) |
| 3️⃣ **Machine Utilization** | Đánh giá hiệu suất sử dụng máy móc theo thời gian | [`03.Machine_Utilization.md`](./03.Machine_Utilization.md) |
| 4️⃣ **OTD Analysis** | Phân tích tỷ lệ giao hàng đúng hạn (On-time Delivery) | [`04.OTD_Analysis.md`](./04.OTD_Analysis.md) |
| 5️⃣ **Capacity Analysis** | Đánh giá năng lực sản xuất và giới hạn công suất nhà máy | [`05.Capacity_Analysis.md`](./05.Capacity_Analysis.md) |

---

### 🔍 Quy trình triển khai

1. **Thu thập & xử lý dữ liệu**  
   - Nguồn: Google Sheets nội bộ (10 tháng gần nhất).  
   - Chuẩn hóa dữ liệu đầu vào
      + Loại bỏ các dòng trống, dữ liệu lỗi hoặc đơn hàng test.
      + Chuẩn hóa định dạng ngày (`yyyy-mm-dd`), mã máy, mã sản phẩm.
      + Kiểm tra trùng lặp giữa **WO (Work Order)** và **Order ID**.
      + Phát hiện và đánh dấu các giá trị **outlier** để kiểm tra lại thủ công  
  (do đây là dữ liệu sản xuất thực tế, việc loại bỏ hoàn toàn có thể gây sai lệch kết quả).

   - Xử lý dữ liệu thiếu
      + Thay thế giá trị null trong downtime hoặc actual quantity bằng 0.

2. **Thiết kế mô hình dữ liệu (Data Modeling)**  
 - Dữ liệu gốc gồm hơn **10 bảng (sheet)**, được nhóm và kết nối lại thành 4 nhóm chính:
  1. **Production Plan** – dữ liệu kế hoạch sản xuất theo máy, sản phẩm và ngày.  
  2. **Production Actuals** – sản lượng thực tế, thời gian thực tế, downtime.  
  3. **Downtime Log** – lý do ngừng máy (Setup, Maintenance, Machine Issue, Thiếu nhân lực, v.v.).  
  4. **Order & Delivery Data** – thông tin đơn hàng, khách hàng, ngày giao và sản lượng đặt.  

- Các bảng được kết nối qua các trường khóa chính:
  - `Machine_ID`
  - `Work_Order`
  - `Date`
  - `Customer_Code`

3. **Xây dựng KPI bằng DAX**  
   - Plan Adherence (%),Production Capacity Utilization(%), Delay Rate (%), Downtime (%), OTD (%).  
   - Các measure được tối ưu để cho phép lọc theo tháng, máy, hoặc khách hàng.  

4. **Trực quan hóa (Visualization)**  
   - Sử dụng Power BI để biểu diễn xu hướng, so sánh và phát hiện bất thường.  
   - Dashboard được thiết kế dạng tương tác giúp người dùng phân tích sâu.  

5. **Phân tích nguyên nhân & đề xuất cải tiến (Root Cause & Recommendation)**  
   - Xác định máy hoặc nhóm sản phẩm có hiệu suất thấp.  
   - Phân tích theo thời gian, nguyên nhân downtime, và đặc thù khách hàng.  
   - Đề xuất hướng cải thiện dựa trên dữ liệu thực tế.  

> 📊 Toàn bộ quá trình được triển khai bằng **Power BI + DAX + Data Modeling**, kết hợp phân tích định lượng và định tính để đảm bảo tính chính xác và khả năng ứng dụng trong thực tế sản xuất.

---

## 📊 5. Dashboard & Phát hiện chính (Key Findings)

### 🔹 1. Production Quantity Analysis
- Tổng sản lượng kế hoạch với sản phẩm ống đạt **62.6M**, so với **công suất tối đa 72M**, tương ứng **Production Capacity Utilization = 86%**.  
  → Điều này cho thấy nhà máy hoạt động **gần ngưỡng tối ưu**, tuy nhiên vẫn còn khoảng **14% năng lực dư thừa** có thể khai thác khi nhu cầu tăng.
- Sản lượng thực tế đạt **62M** (≈ 99% kế hoạch) → mức tuân thủ rất tốt.  
- Giai đoạn **tháng 4 - tháng 7** sản lượng giảm mạnh do **nhu cầu đặt hàng của khách hàng giảm**, trong khi **khả năng lưu kho hạn chế** khiến nhà máy **không thể sản xuất vượt nhu cầu thực tế**.  
- 👉 **Đề xuất:** Xem xét **mở rộng kho lưu trữ** hoặc **đa dạng hóa khách hàng trong mùa thấp điểm** để **duy trì sản lượng ổn định và tận dụng tối đa năng lực sản xuất**.

### 🔹 2. Delay Time Analysis
- Tổng thời gian trễ: **-3.92K giờ (~ -6.35%)**.  
- Tháng 8 ghi nhận chênh lệch cao nhất (**-842 giờ, -14%**).  
- Các máy **PG02, SC04** có tỷ lệ delay cao nhất (>9%)
- Phân tích:
  + SC04 thường chạy full công suất để đáp ứng các đơn hàng đặc thù, nên không thể phân bổ sang máy khác.
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
- Tổng downtime: **5.12K giờ (7.65%)**.  
- Nguyên nhân chính:
  - Machine issue: **38%**
  - Thiếu nhân lực: **20%**
  - PM: **16%**
- Downtime tăng mạnh ở **tháng 8–10**, đặc biệt ở **MC SC06, SC03, SC04**.  
- Riêng **tháng 10**, downtime do **thiếu nhân lực** chiếm **30% tổng thời gian ngừng máy**, cho thấy ảnh hưởng đáng kể từ thiếu hụt nhân sự tạm thời.

> Lưu ý: Trong báo cáo này, **Delay Time** được hiểu là phần thời gian trễ so với kế hoạch sản xuất. 
> trong khi **Downtime** phản ánh thời gian máy ngừng hoạt động do các nguyên nhân kỹ thuật hoặc vận hành.  
> Hai chỉ số này được phân tích độc lập để xác định mối liên hệ giữa **nguyên nhân (downtime)** và **hậu quả (delay)**.

**Mối tương quan giữa Delay Time và Downtime:**

Phân tích cho thấy các giai đoạn có **tỷ lệ downtime cao (tháng 8–10)** cũng là thời điểm **delay time tăng mạnh**.  
Đặc biệt, downtime do **thiếu nhân lực và hư hỏng máy** chiếm hơn 50% tổng thời gian ngừng máy, là nguyên nhân chính khiến **kế hoạch bị trễ so với thực tế**.  
Điều này khẳng định downtime không chỉ làm giảm hiệu suất máy mà còn ảnh hưởng trực tiếp đến **Plan Adherence** và **Ontime Delivery**.

### 🔹 4. On-time Delivery Analysis
- Tổng đơn giao: **837**, chỉ **1 đơn trễ** → **OTD = 99.9%**.  
- Khách hàng **QHA** có sản lượng lớn nhất → cần theo dõi sát do đây là khách hàng chính, sản lượng cao.  
- Biểu đồ **Total Work Orders in Storage < 1 Day (by Customer)** phản ánh các đơn hàng có thời gian lưu kho dưới 1 ngày — tức là sản xuất và xuất hàng gần như liên tục, không có tồn đệm.

- Đáng chú ý, trong tháng 10, khách hàng QHA chiếm 6.5 triệu sản phẩm, khiến có 9 đơn hàng chỉ lưu kho dưới 1 ngày trước khi giao. Điều này cho thấy áp lực giao hàng cao và mức tồn kho thành phẩm đang ở ngưỡng tối thiểu, dễ phát sinh rủi ro trễ nếu có sự cố bất ngờ trong sản xuất hoặc vận chuyển.

👉 **Đề xuất:**
- Xem xét mở rộng năng lực lưu kho thành phẩm tạm thời cho nhóm khách hàng có sản lượng lớn (như QHA).

- Phân bổ lịch giao hàng hợp lý hơn, tránh dồn sản lượng lớn vào cùng kỳ ngắn.

- Đánh giá mức tồn kho an toàn tối thiểu (safety stock) cho từng nhóm khách hàng để hạn chế rủi ro trễ khi khối lượng tăng đột biến.
---

## 🧠 6. Công cụ & Phương pháp (Tools & Methods)
- **Power BI** – trực quan hóa dữ liệu & dashboard tổng hợp  
- **Google Sheets, Power Query** – xử lý & chuẩn hóa dữ liệu gốc 
- **DAX** – xây dựng measure KPI (Plan Adherence, Delay, OTD, v.v.)  
- **Data Modeling** – ghép bảng kế hoạch, thực tế và đơn hàng  

---
## ✅ 7. Kết luận & Đề xuất (Insights & Recommendations)

- **Hiệu suất sản xuất** duy trì ổn định (Plan Adherence > 95%).  
- Cần theo dõi **downtime tăng** ở một số máy (đặc biệt nhóm SC).  
- **Thiếu nhân lực** là yếu tố ảnh hưởng đáng kể đến tiến độ sản xuất, đặc biệt trong tháng 10 khi chiếm tới 30% tổng downtime.  
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
👉 Xem chi tiết các công thức DAX tại [DAX_formulas.md](./DAX_formulas.md)

---

📅 *Thực hiện bởi:* Nguyễn Thị Phương Thảo 
📍 *Công cụ:* Power BI | Google Sheets | DAX | Data Modeling  
