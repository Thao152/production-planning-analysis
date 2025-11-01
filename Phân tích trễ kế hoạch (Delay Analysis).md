# 📊 Phân tích chi tiết: Trễ kế hoạch (Delay Analysis)

## 1️⃣ Tổng quan
Tổng thời gian trễ trong giai đoạn phân tích: **-3.92K giờ (~ -6.35%)**.  
Tháng **8** ghi nhận mức trễ cao nhất (**-842 giờ, tương đương -14%**).  
Tình trạng trễ có xu hướng tăng về các tháng cuối năm, trùng với giai đoạn **khối lượng đơn hàng lớn và yêu cầu mẫu mã phức tạp hơn**.

---

## 2️⃣ Phân tích theo máy

| Máy  | Thời gian trễ (giờ) | % Delay so với kế hoạch | Nhận xét |
|------|----------------------|--------------------------|-----------|
| **SC04** | -503 | -10.46% | Máy chạy full công suất, sản phẩm phức tạp, thường xuyên phải ngưng để chỉnh khuôn đảm bảo chất lượng. |
| **CT02** | -434 | -9.0% | Tải máy cao, thường xuyên đổi mẫu, thời gian setup kéo dài, thường xuyên phải ngưng để chỉnh máy, máy chạy sản phẩm khó (4 màu) đôi khi phải chạy 2 lần. |
| **PG02** | -249 | -12.0% | Là máy backup, không được ưu tiên khi thiếu nhân lực, dẫn đến delay kéo dài. |

**Nhận xét tổng hợp:**  
Các máy **CT02, SC04** là nhóm máy chính, luôn chạy ở mức tải tối đa, nên khi khách hàng yêu cầu sản phẩm phức tạp, máy phải dừng thường xuyên để chỉnh thông số, làm giảm hiệu quả kế hoạch.  
Máy **PG02** hoạt động như **máy dự phòng**, tuy nhiên **khi thiếu nhân sự**, máy này **không được vận hành**, làm kéo dài tổng thời gian hoàn thành kế hoạch.

---

## 3️⃣ Phân tích theo thời gian

| Tháng | Delay (giờ) | % Delay | Ghi chú |
|-------|--------------|----------|----------|
| **Tháng 4** | -204 | -4.86% | Nhu cầu thấp, kế hoạch ổn định. |
| **Tháng 8** | -842 | -14.0% | Đơn hàng tăng sau đợt nhu cầu thấp, thiếu nhân lực, khách đặt hàng mẫu khó. |
| **Tháng 9** | -543 | -7.92% | Ảnh hưởng kéo dài từ tháng 9, backlog chưa xử lý hết. |
| **Tháng 10** | -371 | -6.24% | Đơn hàng tăng, khách có yêu cầu mẫu mã khó, thiếu nhân lực. |

---

## 4️⃣ Nguyên nhân chính
- **Thay đổi mẫu mã phức tạp** → tăng thời gian setup, phải ngưng để chỉnh khuôn.  
- **Máy chạy full công suất** → không có buffer, chỉ cần sự cố nhỏ là kéo dài toàn bộ kế hoạch.  
- **Thiếu nhân lực thời vụ** → không đủ người để vận hành máy.  
- **Máy móc hư hỏng nhẹ** → dừng ngắn nhưng lặp lại nhiều lần, gây trễ tích lũy.

---

## 5️⃣ Insight & Đề xuất

💡 **Insight:**
- Việc khách hàng yêu cầu mẫu mã phức tạp trong nửa cuối năm khiến kế hoạch mất ổn định.  
- Nhóm máy **SC** luôn chạy ở công suất cao, không có thời gian đệm.  
- Thiếu nhân sự thời vụ kéo dài.

💡 **Đề xuất:**
- Thiết lập **buffer time (thời gian dự phòng)** cho các máy chạy sản phẩm khó.  
- Rà soát **quy trình setup** và **quản lý khuôn**, tối ưu thời gian chuyển đổi.  
- **Tuyển dụng và đào tạo nhân sự chính thức** để tránh phụ thuộc vào nhân sự thời vụ. 
- Theo dõi **Delay by Machine** trên dashboard Power BI để phát hiện sớm máy có xu hướng trễ lặp lại.

---
