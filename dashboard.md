# OPERATING DASHBOARD — Agent luyện tập tư vấn sales VinFast

**Phạm Quốc Đạt · 2A202602384 · 09/10/2026 · B2B.** Đại lý trả tiền, sales mới của đại lý dùng; LMS/portal là điểm tích hợp dự kiến. **Đèn bật trước: TTFV.** Kỳ pilot giả định 10/10/2026–07/01/2027. `—` = chưa có quan sát hợp lệ; số dự phóng không được coi là trạng thái xanh.

**NORTH STAR:** Ca mô phỏng đạt chuẩn / ca học đủ điều kiện đã đến hạn; **hiện tại —**, mục tiêu thử nghiệm **≥60% [TB]**. Chỉ tính cặp sales–ca đạt rubric, nguồn hiện hành, không nhân đôi retry.

| Tầng | Đèn (hiện tại) | 🟢 / 🟡 / 🔴 | Nguồn; báo trước cho |
| --- | --- | --- | --- |
| **LEADING** | TTFV (—) | `<30d` / `30–60d` / `>60d` | [TB] Usage → gia hạn |
| | Activation xem phản hồi (—) | `≥70%` / `50–<70%` / `<50%` | [TB] North Star → usage |
| | Cost/Job (—; mô hình $0.2486) | `≤$0.2983` / `>$0.2983–$0.396` / `>$0.396` | [MH-1] GM |
| **OPERATING** | Usage depth (—) | `≥60%` / `30–<60%` / `<30%` | [TB] Gia hạn/NRR |
| | POC → paid (—) | `≥50%` / `35–<50%` / `<35%` | [TB] CAC payback; chỉ màu khi ≥5 pilot kết thúc |
| | Ca đạt chuẩn / ca đến hạn (—) | `≥60%` / `40–<60%` / `<40%` | [TB] Usage và gia hạn |
| **LAGGING** | GM thực tế (—; mô hình 74.89%) | `≥74.89%` / `60–<74.89%` / `<60%` | [MH-2] |
| | CAC payback (—; mục tiêu 12 tháng) | `≤12m` / `>12–15m` / `>15m` | [MH-3] |

**5 LUẬT QUYẾT ĐỊNH** — áp dụng khi đủ mẫu; vế “KHÔNG THÌ” chặn phản xạ sai khi đỏ.

1. **⏹ TTFV:** NẾU `>60d` TRÊN ≥2 pilot, THÌ PM **dừng pilot rộng** tuần sau, thu còn 1 use case/1 đội, demo ca đầu trong 14d. KHÔNG THÌ tuyển thêm sales/ký pilot rộng.
2. **Activation:** NẾU `<50%` TRONG 2 cohort VÀ mỗi cohort ≥10 sales, THÌ product lead sửa luồng nộp bài → phản hồi trong sprint tới, xem 10 session rơi. KHÔNG THÌ tăng thông báo/đẩy thêm ca.
3. **⏹ Cost/Job:** NẾU `>$0.396` TRONG 2 tuần VÀ mỗi tuần ≥50 ca, THÌ infra lead **dừng quota miễn phí và escalation tự động** trong 48h, kiểm tra token/retry/HITL. KHÔNG THÌ tăng volume/giảm giá.
4. **Usage:** NẾU `<30%` TRONG 2 tuần VÀ đại lý ≥20 seat, THÌ CS mở 1 buổi hướng dẫn 30 phút, giao 1 module và kiểm tra sau 7d. KHÔNG THÌ bán thêm seat/module.
5. **⏹ POC→paid:** NẾU `<35%` TRÊN ≥5 pilot đóng, THÌ sales lead **dừng mở kênh mới** 2 tuần, làm Pilot Report có số và sửa bộ lọc pilot. KHÔNG THÌ giảm giá hàng loạt hoặc tính LOI là trả tiền.

**CỔNG GÁC 90 NGÀY** — GO nếu qua ngưỡng; FIX tối đa một lần cho cùng một vấn đề.

| Cổng | Một metric; ngưỡng GO | Bằng chứng phải có | Nếu trượt |
| --- | --- | --- | --- |
| **D30 · 08/11** | Số pilot có log đủ `start→assessment→feedback`: **≥2** | `pilot_registry.csv` + event export | **FIX** 14 ngày cho telemetry/phạm vi pilot |
| **D60 · 08/12** | TTFV trung vị của ≥2 pilot: **<30 ngày** | `first_value_log.csv` + xác nhận quản lý | **FIX** 1 lần nếu nguyên nhân rõ; nếu đã FIX cùng lỗi: **PIVOT** phân khúc/use case |
| **D90 · 07/01** | Usage depth gộp ở các pilot đủ điều kiện: **≥60%** | `seat_roster.csv` + event nộp ca tuần | **PIVOT** nếu giả định sử dụng sai; **KILL** nếu đã FIX mà vẫn `<30%` |

**KILL CRITERIA:** Đến **07/01/2027**, nếu usage depth `<30%` trong 2 tuần liên tiếp ở ≥2 pilot có mỗi pilot ≥20 seat, sau đúng một chu kỳ FIX 30 ngày mà vẫn không tăng, **dừng hướng bán cho đại lý này** và không rót thêm ngân sách mở rộng.

**CHƯA ĐO ĐƯỢC:** Chưa có pilot/hợp đồng và event thực nên TTFV, activation, usage, North Star, POC→paid, CAC/GM/payback thực đều `—`. Cần pilot registry, event schema/định danh, rubric và nguồn chính sách đã duyệt, seat roster, ledger COGS, hóa đơn, chi phí kênh; baseline học tập D30, TTFV D60, kinh tế đơn vị và usage D90. Runway 6 tháng cũng cần bảng dòng tiền xác nhận. Chi tiết định nghĩa, nguồn [MH] và điều kiện mẫu: [worksheet.md](worksheet.md).
