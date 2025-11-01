
# 📊 DAX Formulas & Giải thích

---

## 🏭 Hiệu suất sản xuất (Production Performance)

### Output Actual
```DAX
Output Actual = SUM('Data SX'[Actual Output])
````

**Giải thích:** Tính tổng sản lượng sản xuất thực tế.

---

### Max Output

```DAX
Max Output = SUM('Sản lượng mục tiêu'[Số lượng])
```

**Giải thích:** Tính tổng sản lượng mục tiêu (sản lượng tối đa có thể đạt được).

---

### Production Capacity Utilization

```DAX
Production Capacity Utilization = DIVIDE([Output Actual], [Max Output])
```

**Giải thích:** Đo lường tỷ lệ sử dụng công suất sản xuất, cho biết mức độ nhà máy hoặc dây chuyền đã tận dụng năng lực tối đa của mình.

---

## ⏱️ Thời gian trễ (Delay)

### Delay

```DAX
Delay =
CALCULATE(
    SUM('Data KH'[time (hours)]) - SUM('Data KH'[time (actual)]),
    FILTER('Data KH', 'Data KH'[time (actual)] <> 0)
)
```

**Giải thích:** Tính tổng thời gian trễ, loại trừ những trường hợp chưa có thời gian thực tế (chưa sản xuất).

---

### Delay %

```DAX
Delay % =
DIVIDE(
    [Delay],
    CALCULATE(
        SUM('Data KH'[time (hours)]),
        FILTER('Data KH', 'Data KH'[time (actual)] <> 0)
    ),
    0
)
```

**Giải thích:** Tính tỉ lệ thời gian trễ so với tổng thời gian theo kế hoạch.

---

## ⚙️ Thời gian ngưng máy (Downtime)

### Total Time Actual

```DAX
Total time actual = SUM('Data SX'[WorkHours])
```

**Giải thích:** Tổng thời gian sản xuất thực tế.

---

### Downtime Không Giờ Nghỉ

```DAX
Downtime Không Giờ Nghỉ =
CALCULATE(
    SUM('Nguyên nhân off máy'[downtime(hour)]),
    FILTER('Nguyên nhân off máy', 'Nguyên nhân off máy'[nội dung] <> "Giờ nghỉ")
)
```

**Giải thích:** Tổng thời gian ngưng máy không bao gồm giờ nghỉ giải lao, ăn cơm.

---

### % Downtime

```DAX
% downtime = DIVIDE([Downtime Không Giờ Nghỉ], SUM('Data SX'[WorkHours]))
```

**Giải thích:** Tỉ lệ thời gian ngưng máy so với tổng thời gian làm việc thực tế.

---

### Machine Utilization (%)

```DAX
Machine Utilization (%) = 1 - DIVIDE([Downtime Không Giờ Nghỉ], [Total time actual])
```

**Giải thích:** Tỉ lệ sử dụng máy thực tế, phản ánh phần trăm thời gian máy hoạt động (không bị ngưng) so với tổng thời gian làm việc.

---

## 🚚 Tỉ lệ giao hàng đúng hạn (OTD)

### Total Delivery

```DAX
Total Delivery = SUM('Ngày giao hàng- nhập kho'[On time]) + SUM('Ngày giao hàng- nhập kho'[Delay])
```

**Giải thích:** Tổng số lượng đơn hàng đã giao (bao gồm đúng hạn và trễ).

---

### % OTIF

```DAX
% OTD = 1 - DIVIDE(SUM('Ngày giao hàng- nhập kho'[Delay]), [Total Delivery])
```

**Giải thích:** Tỉ lệ giao hàng đúng hạn (On-Time Delivery), cho biết phần trăm đơn hàng được giao đúng thời hạn.

````


