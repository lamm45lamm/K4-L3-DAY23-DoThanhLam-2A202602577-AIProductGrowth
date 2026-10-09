# Worksheet — [Tên sản phẩm]

Họ tên: Đỗ Thanh Lâm · MSSV: 2A202602577 · Ngày làm: 09/10/2026

## Trạm 1 — Loại mô hình

### Ba câu hỏi (thực tế hôm nay)

1. **Ai trả tiền?** Doanh nghiệp / tổ chức vận hành an ninh: trung tâm VinSOC hoặc ban quản lý khu đô thị mua gói phần mềm + triển khai trên gateway của họ. Không có cá nhân nào trả. → B2B.
2. **Ai dùng sản phẩm?** Nhân viên giám sát và điều tra viên của chính tổ chức đó (người ngồi rà video). Người trả tiền và người dùng cùng một tổ chức. Cư dân, khách ra vào xuất hiện trong video nhưng chỉ là đối tượng bị ghi hình, không đăng nhập, không phải khách hàng dùng sản phẩm. → không phải B2B2C.
3. **Có bên trung gian không, chạm được người dùng cuối không?** Hôm nay không có trung gian: bán và triển khai trực tiếp cho tổ chức, nên chạm được người dùng qua giao diện tìm kiếm trên máy chủ edge và log truy vấn của họ. (Nếu sau này bán qua nhà tích hợp camera thì phải xét lại.)

**Câu chốt loại:** Chúng tôi là B2B vì tiền đến từ tổ chức vận hành an ninh (VinSOC / ban quản lý khu đô thị), người dùng thật là nhân viên giám sát và điều tra viên của chính tổ chức đó, và chúng tôi chạm được họ trực tiếp qua giao diện tìm kiếm tiếng Việt chạy trên gateway tại chỗ, nơi mỗi truy vấn, clip mở ra và lần làm mờ/bỏ làm mờ mặt đều được ghi log.

**Bảng đèn §3.2 B2B** (đủ 11 đèn). Hiện trạng: CamSearch NL mới ở giai đoạn thiết kế / prototype, chưa ký hợp đồng và chưa có khách trả tiền. Mọi đèn về doanh thu và deal vì thế chưa có dữ liệu thật.

| Đèn | ✅ / 🔧 / ❌ | Số nằm ở đâu / cần gì để đo |
|---|---|---|
| L · Time-to-first-value (TTFV) ⭐ | 🔧 | Chưa có khách ký nên chưa có số. Cần: ghi ngày ký, ngày cài xong và ngày lần đầu một điều tra viên tìm đúng clip cần (event "first_verified_hit" trong log truy vấn). Làm được trong 2 tuần ngay khi có một pilot. |
| L · Pipeline coverage | 🔧 | Chưa có pipeline đủ điều kiện. Cần: bảng theo dõi cơ hội (sheet hoặc CRM) với giá trị ước tính, giai đoạn và target doanh thu quý. Bản thân target quý cũng chưa đặt. |
| L · % deal chết ở khâu security/procurement | ❌ | Chưa có deal nào đi qua khâu này nên chưa có mẫu số, và chưa biết cách tính cho ra nghĩa khi dưới ~10 deal. Rủi ro dự đoán cao (video riêng tư, làm mờ mặt, nhận dạng), nhưng đó là dự đoán, không phải số đo. |
| O · POC → paid | ❌ | Chưa chạy POC nào. Chưa có khách để chuyển đổi. |
| O · Sales cycle (tuần) | ❌ | Chưa có cơ hội đủ điều kiện nào đi tới chữ ký. Không có ngày bắt đầu và ngày kết thúc để đo. |
| O · Usage depth trong tài khoản | 🔧 | Cần log truy vấn theo tài khoản và theo người dùng trên edge (offline, lưu cục bộ, xuất báo cáo định kỳ khi khách đồng ý). Đo % operator được cấp quyền có ít nhất một truy vấn mỗi tuần. Mẫu số (số seat đã bán) chưa có vì chưa có hợp đồng. |
| O · Chi phí triển khai ÷ ACV | 🔧 | Tử số đo được trong 2 tuần: ghi giờ công cài gateway, nối camera/VMS, lập chỉ mục ban đầu và tinh chỉnh. Mẫu số ACV chưa có vì chưa chốt giá. |
| O · Tập trung doanh thu | ❌ | Chưa có doanh thu, nên chưa có khách lớn nhất để chia. Chỉ trở nên có nghĩa khi có ≥3 khách trả tiền. |
| G · NRR | ❌ | Chưa có khách trả tiền nên chưa có kỳ đầu để so. Chưa biết cách định nghĩa "mở rộng" cho sản phẩm tính theo gateway/camera. |
| G · Gross Margin | 🔧 | Không có hóa đơn token vì suy luận chạy offline trên edge của khách. Chi phí giá vốn chủ yếu là khấu hao phần cứng GPU/NPU, điện, hỗ trợ. Cần: đo chi phí/giờ video lập chỉ mục và chi phí/truy vấn trên phần cứng chuẩn (Cost/Job), cộng định giá. Hôm nay mới có thể ước lượng, chưa có số thật. |
| G · CAC payback | ❌ | Chưa có khách, chưa có chi phí bán hàng và chưa có doanh thu hằng tháng, nên không tính được. |

Tổng: ✅ 0 · 🔧 5 · ❌ 6. Hai ô đáng chú ý nhất: TTFV (🔧, cần đo ngay ở pilot đầu tiên) và % deal chết ở security/procurement (❌, rủi ro lớn nhất của loại sản phẩm này). Danh sách ❌ sẽ chuyển thành mục "Chưa đo được" ở dashboard cuối.

## Trạm 2 — Thẻ đèn

**North Star:** Time-to-first-value (TTFV): số ngày từ ký hợp đồng đến lần đầu một điều tra viên tìm được và xác nhận đúng clip họ cần — hiện tại chưa đo được (chưa có khách ký, xem Trạm 1) — mục tiêu <30 ngày ở mỗi khách. Chọn TTFV vì đây là đèn bật trước của B2B: sản phẩm edge cần cài đặt, nối camera và lập chỉ mục trước khi có giá trị, nên deal chết ở khoảng trống đó chứ không chết ở giá.

| # | Tầng (L/O/G) | Đèn | Định nghĩa (đếm gì · **không** đếm gì) | Công thức | Nhịp · ai lấy số | Báo trước cho |
|---|---|---|---|---|---|---|
| 1 | L | **TTFV** ⭐ | Số ngày lịch từ ngày ký hợp đồng đến lần đầu có truy vấn được điều tra viên đánh dấu "clip đúng". **Không** tính "đã cài xong", truy vấn demo của đội mình, hay truy vấn do nhân viên của mình gõ thay khách. | Ngày "clip đúng" đầu tiên − ngày ký | Mỗi khách, cập nhật hằng tuần · tôi lấy từ log truy vấn trên gateway (có sự đồng ý của khách) | Usage depth (#3) → gia hạn năm đầu (NRR, chưa đo được) |
| 2 | L | **Tỷ lệ truy vấn có kết quả được xác nhận** | % truy vấn trả ≥1 clip mà người dùng bấm "đúng" trong vòng 7 ngày đầu sau go-live và các tuần sau. Chỉ tính truy vấn có kết quả. **Không** tính truy vấn không ra kết quả, truy vấn trùng lặp trong 5 phút, hay truy vấn của tài khoản test. Kết quả không có timestamp/clip thật là lỗi grounding, đếm riêng và phải bằng 0. | Số truy vấn có ≥1 clip được bấm "đúng" ÷ số truy vấn có kết quả | Hằng tuần, theo khách · tôi lấy từ log feedback trên edge | Usage depth (#3): người dùng không tin kết quả thì thôi dùng → gia hạn năm đầu (NRR, chưa đo được) |
| 3 | O | **Usage depth** | % người dùng được cấp quyền có ≥1 truy vấn thật mỗi tuần. **Không** tính đăng nhập không truy vấn, truy vấn test, tài khoản quản trị chỉ cấu hình. | Số user có ≥1 truy vấn thật trong tuần ÷ số user đã cấp quyền | Hằng tuần, theo khách · tôi lấy từ log truy vấn | Gia hạn năm đầu (NRR, chưa đo được); cờ churn sớm sau 60 ngày go-live |
| 4 | O | **Độ trễ truy vấn p95** | Thời gian từ lúc gửi câu hỏi tiếng Việt đến lúc hiện danh sách clip có timeline, trên phần cứng edge của khách, chạy offline, đo ở phân vị 95. **Không** tính thời gian xem clip, hay truy vấn lúc đang lập chỉ mục nặng (tách ra báo riêng). | p95 của (thời điểm trả kết quả − thời điểm gửi) | Hằng tuần, theo khách · tự động ghi trong log gateway | Usage depth (#3): chậm thì điều tra viên quay lại tua tay |
| 5 | O | **Chi phí triển khai ÷ ACV** | Giờ công cài gateway, nối camera/VMS, lập chỉ mục ban đầu và tinh chỉnh, nhân đơn giá giờ, cộng chi phí tích hợp, chia cho giá trị hợp đồng năm đầu. **Không** tính chi phí bán hàng (đã nằm trong CAC) hay hỗ trợ sau go-live. | (Giờ công × đơn giá + chi phí tích hợp) ÷ ACV | Mỗi khách, khi go-live · tôi ghi timesheet | Gross margin (#7); cho biết mình là sản phẩm hay dịch vụ |
| 6 | O | **Chi phí AI trên giờ video lập chỉ mục (kèm kích thước index)** | Chi phí khấu hao phần cứng GPU/NPU + điện để trích đặc trưng và lập chỉ mục 1 giờ video từ 1 camera, trên phần cứng chuẩn tại khách; ghi kèm GB index tạo ra cho giờ đó. Truy vấn tính riêng ở cuối kỳ. **Không** tính chi phí huấn luyện model hay chi phí R&D. | (Chi phí phần cứng/giờ + điện/giờ) ÷ số giờ video lập chỉ mục được trong giờ đó; GB index ÷ giờ video | Hằng tháng, theo khách · tôi đo từ log tải máy chủ | Gross margin (#7); chi phí tăng theo số camera thì lỗ hơn khi khách mở rộng |
| 7 | G | **Gross Margin** | (Doanh thu − giá vốn) ÷ doanh thu. Giá vốn gồm khấu hao phần cứng edge, điện, hỗ trợ vận hành, chi phí triển khai phân bổ theo năm hợp đồng. **Không** tính R&D hay bán hàng. | (Doanh thu hợp đồng − giá vốn) ÷ doanh thu hợp đồng | Hằng quý · tôi tính từ các đèn #5, #6 và hợp đồng | Là kết quả cuối: quyết định có đủ tiền nuôi đội và mở rộng không |

Đèn chi phí AI là đèn số: 6 (chi phí AI trên giờ video lập chỉ mục, kèm kích thước index). Đèn #4 (độ trễ) và #2 (grounding) cũng là điều kiện bắt buộc của đề tài nên được theo dõi cùng.

Số đèn: 7 · Leading 2 (#1, #2) · Operating 4 (#3–#6) · Lagging 1 (#7). Đã cắt NRR, CAC payback, POC→paid, sales cycle, pipeline coverage, tập trung doanh thu và % deal chết ở security/procurement vì chưa có dữ liệu (đều ❌ ở Trạm 1) — các đèn này sẽ nằm ở mục "Chưa đo được".

## Trạm 3 — Ngưỡng

Ngày làm bài: 09/10/2026. Số liệu HANDBOOK §8 chốt 27/08/2026, cách 43 ngày (<3 tháng) nên không bắt buộc cập nhật nguồn gốc.

| # | Đèn | 🟢 | 🟡 | 🔴 | Nguồn [BM]/[MH]/[TB] | Lý do (1 câu) · ngày kiểm tra nếu [BM] |
|---|---|---|---|---|---|---|
| 1 | TTFV ⭐ | <30 ngày | 30–60 ngày | >60 ngày | [TB] | Chưa có chuẩn, đo 2 chu kỳ rồi lấy làm baseline: ba mốc này là giả thuyết khởi điểm lấy từ HANDBOOK §3.2 (cũng ghi [TB]), thay bằng baseline sau 2 pilot hoàn thành; chưa có pilot nên chưa có ngày chắc, dự kiến Q1/2027. |
| 2 | Tỷ lệ truy vấn có kết quả được xác nhận | ≥70% | 50–70% | <50% | [TB] | Chưa có chuẩn, đo 2 chu kỳ rồi lấy làm baseline: ba mốc là giả thuyết khởi điểm, chưa có cơ sở nào ngoài việc dưới 50% nghĩa là người dùng bấm "sai" nhiều hơn "đúng"; thay bằng baseline sau 2 chu kỳ tuần đầu của pilot đầu tiên, chưa có ngày chắc, đo thử trên bộ clip nội bộ trước 06/11/2026. |
| 3 | Usage depth | ≥60% | 30–60% | <30% | [TB] | Chưa có chuẩn, đo 2 chu kỳ rồi lấy làm baseline: mốc lấy từ HANDBOOK §3.2 (ghi [TB]); có số sau 2 chu kỳ tuần của pilot đầu tiên, chưa có ngày chắc. |
| 4 | Độ trễ truy vấn p95 | ≤3 giây | 3–10 giây | >10 giây | [TB] | Chưa có chuẩn, đo 2 chu kỳ rồi lấy làm baseline: mốc là giả thuyết khởi điểm của tôi; đo được ngay trên prototype offline, có baseline 2 chu kỳ tuần dự kiến ngày 23/10/2026, rồi đo lại trên phần cứng của khách. |
| 5 | Chi phí triển khai ÷ ACV | <15% | 15–25% | >25% | [MH] | Suy từ ngưỡng Gross Margin (🟢 ≥55%, 🔴 <45%) trừ phần giá vốn lặp lại; xem phụ lục [MH] 1. Đầu vào là giả định cần thay bằng số Day 24–25 của tôi. |
| 6 | Chi phí AI trên camera-giờ lập chỉ mục | ≤125 ₫ | 125–250 ₫ | >250 ₫ | [MH] | Suy từ giá bán giả định và ngân sách giá vốn lặp lại 30% doanh thu; xem phụ lục [MH] 2. Kích thước index (GB/camera-ngày) ghi kèm để theo dõi, chưa đặt ngưỡng. |
| 7 | Gross Margin | ≥55% | 45–55% | <45% | [BM] | ICONIQ, *State of AI 2026* (07/2026): gross margin AI-native 45% (2025) → 53% (2026P), qua HANDBOOK §8 mục 7. Ngày kiểm tra 09/10/2026: đã đối chiếu tuổi số liệu với ngày chốt sổ tay 27/08/2026 (43 ngày), chưa mở lại báo cáo gốc. |

### Phụ lục [MH] — phép tính (≥2)

Lưu ý trung thực: repo này không chứa mô hình Day 24–25 của tôi, nên các đầu vào bên dưới là **giả định minh hoạ**, đánh dấu (G). Phải thay bằng số thật của mình (Cost/Job, giá hợp đồng) trước khi nộp; phép tính giữ nguyên.

**[MH] 1 — Chi phí triển khai ÷ ACV**

```
Đầu vào (từ mô hình tài chính / Cost/Job của tôi):
  - Ngưỡng GM năm đầu: 🟢 ≥55%, 🔴 <45% (HANDBOOK §3.2, [BM] ICONIQ mục 7).
  - Giá vốn lặp lại (khấu hao phần cứng edge + điện + hỗ trợ) = 30% ACV (G)
  - Chi phí triển khai tính hết vào năm đầu (không phân bổ nhiều năm).
Phép tính:
  GM năm đầu = 1 − 30% − triển_khai%
  🟢: 1 − 0,30 − t ≥ 0,55  →  t ≤ 0,15
  🔴: 1 − 0,30 − t < 0,45  →  t > 0,25
Kết quả → 🟢 <15% · 🟡 15–25% · 🔴 >25%
```

**[MH] 2 — Chi phí AI trên camera-giờ lập chỉ mục**

```
Đầu vào:
  - Giá bán = 600.000 ₫ / camera / tháng (G, chưa chốt giá)
  - Giờ trong tháng = 24 × 30 = 720
  - Ngân sách giá vốn lặp lại = 30% doanh thu (cùng giả định với [MH] 1);
    phần AI/hạ tầng suy luận không được vượt nửa ngân sách (15%) để còn chỗ cho điện + hỗ trợ.
Phép tính:
  Doanh thu / camera-giờ = 600.000 ÷ 720 = 833 ₫
  🟢: ≤15% × 833 = 125 ₫
  🔴: >30% × 833 = 250 ₫ (chi phí AI một mình ăn hết ngân sách giá vốn lặp lại)
Kết quả → 🟢 ≤125 ₫ · 🟡 125–250 ₫ · 🔴 >250 ₫ mỗi camera-giờ
```

## Trạm 4 — 5 luật quyết định

Đánh dấu ⏹ cho luật dừng (cần ≥2).

1. ⏹ **TTFV (đèn #1)** — **NẾU** TTFV >60 ngày **TRÊN** 2 khách gần nhất (chưa đủ 2 khách thì tính từ khách duy nhất sau ngày thứ 60) **VÀ** nguyên nhân không phải do khách chưa cấp quyền truy cập camera/VMS (loại trường hợp chờ khách, tách riêng khỏi số), **THÌ** trong 1 tuần kể từ ngày thấy đèn đỏ, tôi cắt phạm vi pilot kế tiếp xuống 1 khu vực, 1 nhóm camera, 1 đội giám sát, và không ký pilot rộng hơn cho tới khi TTFV <30 ngày. **KHÔNG THÌ** không tuyển hay thuê thêm người bán hàng, không hứa thêm camera hay thêm tính năng để "giữ khách", vì thêm deal vào một đường triển khai tắc chỉ làm tắc nặng hơn.

2. ⏹ **Tỷ lệ truy vấn có kết quả được xác nhận (đèn #2)** — **NẾU** tỷ lệ <50% **TRONG** 2 tuần liên tiếp, đo trên ít nhất 30 truy vấn có kết quả mỗi tuần (dưới 30 thì chưa kết luận, vì quá nhiễu), **THÌ** tôi khoá việc mở thêm camera hay thêm khách mới, và trong 5 ngày làm việc kể từ ngày đèn đỏ, tôi lấy 20 truy vấn bị bấm "sai" gần nhất, gán nguyên nhân (mô tả sai thuộc tính, sai giờ, sai camera, câu hỏi không hiểu) và sửa nhóm nguyên nhân lớn nhất. **KHÔNG THÌ** không giảm ngưỡng độ tương đồng để "trả nhiều kết quả hơn", không trả kết quả không có timestamp/clip thật, vì đó là bịa và phá vỡ cam kết grounded của sản phẩm.

3. **Usage depth (đèn #3)** — **NẾU** usage depth <30% **SAU** 60 ngày kể từ go-live ở một khách, **THÌ** trong 2 tuần kể từ ngày đèn đỏ, tôi cử người đến làm buổi đào tạo tại chỗ với đội giám sát và phỏng vấn 3 người dùng vắng mặt để biết vì sao họ quay lại tua tay, và báo kết quả cho đầu mối của khách. **KHÔNG THÌ** không bán thêm camera, thêm module hay thêm gói cho khách đó, không bàn gia hạn trước khi usage depth lên trên 30%, vì bán thêm vào một khách chưa dùng là cách nhanh nhất mất cả hợp đồng.

4. ⏹ **Chi phí triển khai ÷ ACV (đèn #5)** — **NẾU** chi phí triển khai >25% ACV **TRÊN** 3 khách liên tiếp (chưa đủ 3 khách: áp dụng ngay khi 2 khách liên tiếp vượt 40%, vì mức đó cho thấy cấu trúc chứ không phải ngẫu nhiên), **THÌ** trong 2 tuần kể từ ngày đèn đỏ, tôi hoặc tăng giá cho khách mới, hoặc đóng gói bước tốn giờ nhất (cài đặt gateway, nối camera/VMS) thành bộ cài và connector dựng sẵn. **KHÔNG THÌ** không nhận khách mới ở mức giá cũ và không làm tuỳ biến riêng, vì mỗi khách mới ở mức giá đó làm biên lợi nhuận xấu thêm.

5. **Chi phí AI trên camera-giờ lập chỉ mục (đèn #6)** — **NẾU** chi phí >250 ₫ mỗi camera-giờ **TRONG** 1 tháng đo trên phần cứng chuẩn **VÀ** khối lượng camera đủ lớn để loại trừ chi phí khởi động (dưới 5 camera thì đo lại rồi mới kết luận), **THÌ** trong 2 tuần kể từ ngày đèn đỏ, tôi giảm chi phí lập chỉ mục bằng cách lập chỉ mục theo khung thưa hơn hoặc chỉ khi có chuyển động, hoặc dùng model nhỏ hơn, và đo lại chất lượng (đèn #2) trước khi áp dụng cho khách. **KHÔNG THÌ** không tăng cấu hình phần cứng lên mức cao hơn để "cho chắc" và không báo giá cho khách mới trước khi chi phí xuống dưới 250 ₫, vì phần cứng mạnh hơn làm giá vốn lặp lại tăng ngay, đẩy gross margin xuống dưới 45%.