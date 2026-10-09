# Lab Day 23 — Operating Dashboard

- **Học viên:** Phạm Quốc Đạt
- **MSSV:** `2A202602384`
- **Sản phẩm:** Agent luyện tập tư vấn cho sales xe VinFast mới (AI Sales Training & Simulation Agent)
- **Ngày lập:** 09/10/2026 · **Kỳ vận hành giả định:** 10/10/2026–07/01/2027

**Chốt loại mô hình:** Sản phẩm là **B2B** ở giai đoạn hiện tại: đại lý/showroom trả tiền, nhân viên sales của chính đại lý dùng agent để hoàn thành ca mô phỏng và xem phản hồi; LMS/portal là điểm tích hợp hoặc kênh bán, chưa phải một đối tác phân phối tới tập khách hàng cuối độc lập. Vì vậy dashboard dùng bảng đèn B2B, với **time-to-first-value (TTFV)** là đèn bật trước.

## Bốn file nộp

| File | Nội dung |
| --- | --- |
| [README.md](README.md) | Danh tính, sản phẩm, loại mô hình và xuất xứ số liệu |
| [worksheet.md](worksheet.md) | Trạm 1–4: kiểm kê đèn, định nghĩa, ngưỡng, phép tính, 5 luật |
| [dashboard.md](dashboard.md) | Dashboard điều hành 1 trang, nguồn để xuất PDF |
| [dashboard.pdf](dashboard.pdf) | Trang 1 dashboard, trang 2 phụ lục phép tính [MH] |

## Nguồn đầu vào và trạng thái bằng chứng

Đây là **bài thiết kế dashboard cho một pilot giả định**, không phải báo cáo vận hành đã chạy. Các trị số tài chính lấy từ [bài Day 22 của cùng sản phẩm](https://github.com/PhamDat-05/Track1_Day22_2A202602384_PhamQuocDat): giá $0.99/ca hoàn thành, Cost/Job **$0.2486** (mô hình ở 820 ca hoàn thành/tháng), gross margin mô hình **74.89%**, ARPU mục tiêu **$300/đại lý/tháng**, payback mục tiêu **12 tháng**, ngân sách CAC tối đa **$2,695.92/đại lý**. Value Metric là **ca mô phỏng hoàn thành có báo cáo đánh giá hợp lệ**. Định nghĩa event và North Star kế thừa [Metrics Pack Day 20](https://github.com/PhamDat-05/Track1_Day20_2A202602384_PhamQuocDat). Các số trên là **dự phóng/giả định của mô hình**, không phải kết quả pilot.
