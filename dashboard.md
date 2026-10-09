# OPERATING DASHBOARD — CamSearch NL

**Loại mô hình:** B2B · **Cập nhật:** 09/10/2026 · Đỗ Thanh Lâm – 2A202602577
**NORTH STAR:** TTFV (ngày từ ký đến lần đầu điều tra viên xác nhận "clip đúng") — hiện tại chưa đo (chưa có khách) — mục tiêu <30 ngày

### Đèn báo sớm (Leading — nhìn hằng ngày/tuần)

| Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn | Báo trước cho |
|---|---|---|---|---|
| TTFV ⭐ | chưa đo | <30 / 30–60 / >60 ngày | [TB] | Usage depth → gia hạn năm đầu |
| Tỷ lệ truy vấn có kết quả được xác nhận | chưa đo | ≥70% / 50–70% / <50% | [TB] | Usage depth → gia hạn năm đầu |

### Đèn vận hành (Operating — nhìn hằng tuần/tháng)

| Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn | Báo trước cho |
|---|---|---|---|---|
| Usage depth | chưa đo | ≥60% / 30–60% / <30% | [TB] | Gia hạn năm đầu (NRR) |
| Độ trễ truy vấn p95 | chưa đo | ≤3 / 3–10 / >10 giây | [TB] | Usage depth |
| Chi phí triển khai ÷ ACV | chưa đo | <15% / 15–25% / >25% | [MH] | Gross margin |
| Chi phí AI / camera-giờ lập chỉ mục | chưa đo | ≤125 / 125–250 / >250 ₫ | [MH] | Gross margin |

### Đèn kết quả (Lagging — nhìn hằng quý)

| Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn |
|---|---|---|---|
| Gross Margin | chưa đo | ≥55% / 45–55% / <45% | [BM] ICONIQ 07/2026, kiểm tra 09/10/2026 |

### 5 luật quyết định (⏹ = luật dừng)

1. ⏹ NẾU TTFV >60 ngày TRÊN 2 khách gần nhất (không tính thời gian chờ khách cấp quyền) THÌ trong 1 tuần tôi cắt pilot kế tiếp xuống 1 khu vực, 1 đội; KHÔNG THÌ không thuê thêm người bán, không hứa thêm tính năng để giữ khách.
2. ⏹ NẾU tỷ lệ truy vấn được xác nhận <50% TRONG 2 tuần liên tiếp VÀ ≥30 truy vấn/tuần THÌ khoá thêm camera/khách mới, trong 5 ngày làm việc phân loại 20 truy vấn bị bấm "sai" và sửa nhóm lỗi lớn nhất; KHÔNG THÌ không hạ ngưỡng tương đồng, không trả kết quả thiếu timestamp/clip thật.
3. NẾU usage depth <30% SAU 60 ngày go-live THÌ trong 2 tuần đào tạo tại chỗ và phỏng vấn 3 người vắng mặt; KHÔNG THÌ không bán thêm camera/module, không bàn gia hạn.
4. ⏹ NẾU chi phí triển khai >25% ACV TRÊN 3 khách liên tiếp THÌ trong 2 tuần tăng giá hoặc đóng gói bước cài/nối camera thành bộ dựng sẵn; KHÔNG THÌ không nhận khách mới ở giá cũ, không tuỳ biến riêng.
5. NẾU chi phí AI >250 ₫/camera-giờ TRONG 1 tháng VÀ ≥5 camera THÌ trong 2 tuần lập chỉ mục thưa hơn/chỉ khi có chuyển động hoặc model nhỏ hơn, đo lại đèn #2 trước khi áp dụng; KHÔNG THÌ không nâng phần cứng "cho chắc", không báo giá khách mới.

### Cổng gác 90 ngày

| Ngày | Metric (1) | Ngưỡng qua cổng | Bằng chứng | Nếu trượt |
|---|---|---|---|---|
| 30 (08/11/2026) | Số pilot đã go-live | ≥1 pilot, 0 kết quả thiếu timestamp/clip trên bộ 50 truy vấn kiểm thử | Biên bản go-live có chữ ký + log truy vấn đầu tiên + file kết quả 50 truy vấn | FIX (chưa có đối tác thì 1 lần, 30 ngày; trượt lần 2 → PIVOT sang bán qua nhà tích hợp camera) |
| 60 (08/12/2026) | TTFV của pilot đầu tiên | ≤30 ngày, có ngày ký và ngày "clip đúng" đầu tiên | Hợp đồng/biên bản + log `first_verified_hit` | PIVOT (giả định "cài nhanh" sai → thu hẹp phạm vi pilot hoặc đổi kênh bán) |
| 90 (07/01/2027) | Tỷ lệ truy vấn được xác nhận | ≥50% trong 2 tuần liên tiếp, ≥30 truy vấn/tuần | Log feedback trên edge + Pilot Report có số | FIX (1 lần, đúng nhóm lỗi lớn nhất); trượt lần 2 → KILL |

**KILL CRITERIA:** Dừng hẳn hướng này nếu đến 07/01/2027 vẫn chưa có khách nào ký pilot hoặc hợp đồng, hoặc tỷ lệ truy vấn được xác nhận vẫn <50% (≥30 truy vấn/tuần, 2 tuần liên tiếp) sau 1 lần FIX.

**CHƯA ĐO ĐƯỢC**:
- ❌ % deal chết ở security/procurement, POC→paid, sales cycle: cần ≥1 vòng bán thật, ghi ngày từng giai đoạn; có số sau khi hoàn thành 5 deal hoặc POC (chưa có ngày chắc, dự kiến sau 07/01/2027).
- ❌ NRR, CAC payback, tập trung doanh thu: cần ≥3 khách trả tiền và ≥12 tháng dữ liệu; chưa biết cách định nghĩa "mở rộng" (theo camera hay gateway); không có số trước 2028.
- 🔧 TTFV, usage depth, tỷ lệ xác nhận: cần log truy vấn + nút "clip đúng/sai" trên edge, có số khi pilot đầu tiên chạy 2 chu kỳ tuần (dự kiến ~12/2026).
- 🔧 Độ trễ p95: đo được trên prototype offline, dự kiến 23/10/2026; đo lại trên phần cứng khách.
- 🔧 Chi phí triển khai ÷ ACV: cần timesheet + giá hợp đồng; 🔧 Chi phí AI/camera-giờ, Gross Margin: cần đo trên phần cứng chuẩn và chốt giá, dự kiến 06/11/2026; hai phép tính [MH] đang dùng giả định (giá 600.000 ₫/camera/tháng, giá vốn lặp lại 30%).
