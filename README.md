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

Runway **6 tháng** và ngày bắt đầu pilot **10/10/2026** là giả định bổ sung vì chưa có bảng dòng tiền hay lịch triển khai xác nhận. CAC thực tế, TTFV, activation, usage, tỷ lệ pilot chuyển trả tiền, GM thực tế và payback thực tế đều **chưa đo**. Các ngưỡng [TB] là tiêu chuẩn kiểm thử ban đầu, sẽ thay bằng baseline sau khi đủ dữ liệu. Không dùng benchmark [BM] không truy được nguồn.

**Cách đọc:** màu xanh/vàng/đỏ trong tài liệu là *ngưỡng quyết định*, không phải trạng thái hiện tại. Dấu `—` là chưa có quan sát hợp lệ. Không tô xanh cho số mô hình.

## Kiểm tra trước khi nộp

Dashboard có 8 đèn (3 Leading, 3 Operating, 2 Lagging), mỗi đèn có định nghĩa và ngưỡng có nguồn; 3 phép tính [MH] nằm trong worksheet và trang 2 PDF. Có 5 luật đủ các vế, 3 luật dừng ⏹, 3 cổng gác với đúng một metric/cổng, kill criteria có ngày và phần “Chưa đo được”. Hãy xác nhận giả định với người phụ trách sản phẩm và tự diễn đạt lại các luật/ngưỡng trước khi nộp theo quy định bài cá nhân.

**Nguồn đề:** [Lab Day 23 và mẫu](https://github.com/VinUni-AI20k/K4-L3-Day23-AI-Product-Growth) · [Rubric](https://github.com/VinUni-AI20k/K4-L3-Day23-AI-Product-Growth/blob/main/RUBRIC.md)
