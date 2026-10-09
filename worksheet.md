# Worksheet — Agent luyện tập tư vấn sales VinFast

**Học viên:** Phạm Quốc Đạt · **MSSV:** 2A202602384 · **Ngày làm:** 09/10/2026

## Đầu vào mô hình và quy ước

| Đầu vào | Giá trị | Trạng thái / xuất xứ |
| --- | ---: | --- |
| Giá mỗi ca hoàn thành hợp lệ | $0.99/ca | Mô hình Day 22, Value Metric Outcome |
| Cost/Job | $0.2486/ca | Dự phóng Day 22: $203.87 / 820 ca hoàn thành |
| ARPU | $300/đại lý/tháng | Mục tiêu Day 22; xấp xỉ 303 ca × $0.99 |
| Gross margin | 74.89% | Dự phóng `(0.99−0.2486)/0.99`, chưa phải GM thực tế |
| CAC | Chưa đo | Day 22 có *ngân sách CAC* $2,695.92, không phải CAC đã quan sát |
| CAC payback mục tiêu | 12 tháng | Giả định mục tiêu Day 22 cho SMB |
| Runway | 6 tháng | Giả định của bài này, chưa có bảng dòng tiền xác nhận |
| North Star / Value Metric | Ca đạt chuẩn tư vấn trên ca học được giao / ca hoàn thành có assessment hợp lệ | Metrics Pack Day 20 / mô hình Day 22; cần rubric thật để đo “đạt chuẩn” |

Nguồn nội bộ đã công khai: [Day 22](https://github.com/PhamDat-05/Track1_Day22_2A202602384_PhamQuocDat) và [Day 20](https://github.com/PhamDat-05/Track1_Day20_2A202602384_PhamQuocDat). Các mốc [TB] dưới đây là **giả thuyết quản trị**, không phải benchmark ngành hoặc dữ liệu đang có. Ngày pilot giả định 10/10/2026; ngày 30/60/90 tương ứng 08/11, 08/12/2026 và 07/01/2027.

## Trạm 1 — Chốt loại mô hình

- **Ai trả tiền?** Đại lý/showroom mua quyền sử dụng cho đội sales; đơn vị tính tiền dự phóng là ca hoàn thành hợp lệ. Chưa có hợp đồng thật.
- **Ai dùng?** Sales mới trong đội onboarding của chính đại lý; trưởng nhóm xem báo cáo chấm.
- **Có chạm người dùng cuối qua trung gian?** Theo thiết kế, event theo `learner_id` sẽ đo sales trong pilot của đại lý. LMS/portal chỉ là điểm nhúng dự định, chưa có bằng chứng đối tác vận hành kênh tới tập khách hàng cuối của họ.
- **Câu chốt:** Chúng tôi là **B2B** vì đại lý trả tiền, sales của đại lý là người thực hiện ca mô phỏng và nhận phản hồi, còn LMS/portal hiện là điểm tích hợp dự kiến chứ chưa tạo một phễu B2B2C độc lập.
- **Đèn bật trước:** TTFV — từ lúc pilot bắt đầu đến lần đầu đại lý nhận được một ca hoàn thành hợp lệ, sales xem phản hồi và quản lý xác nhận giá trị học tập; không tính “đã cài xong”.

### Kiểm kê đầy đủ bảng đèn B2B trong HANDBOOK §3.2

Không có số vận hành thực tế tính đến 09/10/2026. `🔧` = có thiết kế đo, cần triển khai/đủ mẫu trong hai tuần; `❌` = còn thiếu điều kiện nền tảng hoặc chu kỳ quan sát dài hơn.

| Đèn trong bảng B2B | Trạng thái | Số nằm ở đâu / cần gì để đo |
| --- | --- | --- |
| Time-to-first-value (TTFV) | 🔧 | Hợp đồng/pilot start + event assessment/feedback + biên bản quản lý xác nhận giá trị |
| Pipeline coverage | 🔧 | CRM với giá trị cơ hội đủ điều kiện và target quý đã duyệt |
| % deal chết ở security/procurement | 🔧 | CRM bắt buộc mã lý do closed-lost và mốc vào vòng duyệt |
| POC → paid | 🔧 | Danh sách pilot kết thúc và hợp đồng/hóa đơn đã thanh toán |
| Sales cycle | 🔧 | Timestamp cơ hội đủ điều kiện và ký hợp đồng trong CRM |
| Usage depth trong tài khoản | 🔧 | Danh sách seat được giao và event nộp ca hợp lệ từng tuần; loại tài khoản test |
| Chi phí triển khai ÷ ACV | ❌ | Chưa có timesheet, đơn giá công triển khai và ACV ký thật |
| Tập trung doanh thu | ❌ | Chưa có doanh thu thực từ ≥2 khách |
| NRR | ❌ | Chưa có cohort khách trả tiền và kỳ gia hạn |
| Gross Margin | 🔧 | Hóa đơn thu tiền + ledger token/infra/HITL theo ca; hiện chỉ có mô hình |
| CAC payback | ❌ | Chưa có CAC thực, thời gian bán và GM thực theo khách |

**Đèn bổ sung theo sản phẩm:** tỷ lệ xem phản hồi lần đầu, tỷ lệ ca đạt chuẩn (North Star), Cost/Job. Chúng dùng schema trong Metrics Pack Day 20 và bảng chi phí Day 22; tất cả vẫn cần log pilot.

## Trạm 2 — Cây ba tầng và thẻ đèn

**North Star:** tỷ lệ ca mô phỏng đạt chuẩn tư vấn trên tổng ca học đủ điều kiện đã đến hạn. Hiện tại `—` (chưa có rubric/pilot); mục tiêu thử nghiệm `≥60% [TB]`, rà lại sau 30 ngày có baseline. Một cặp `learner_id × case_id × case_version` tối đa một lần đạt chuẩn; retry không làm phình tử số. “Đạt chuẩn” chỉ khi assessment theo rubric được duyệt, nguồn chính sách còn hiệu lực và không có lỗi trọng yếu.

| # | Tầng | Đèn và định nghĩa chặt (đếm / không đếm) | Công thức | Nhịp; ai lấy số | Báo trước cho; luật đỏ |
| --- | --- | --- | --- | --- | --- |
| 1 | L | **TTFV**: ngày từ pilot start đến ca hợp lệ đầu tiên có phản hồi được sales xem và quản lý xác nhận giá trị; không tính ngày chỉ cài SDK. Pilot chưa tạo giá trị tới ngày rà soát được ghi là “chưa đạt”, không tự tính 0 ngày. | `date(first_value) − date(pilot_start)` theo lịch ngày | Mỗi pilot; PM + quản lý đại lý | Usage depth → GM/renewal; R1 |
| 2 | L | **Activation phản hồi**: sales đủ điều kiện xem phản hồi của ca hợp lệ đầu tiên trước hạn module đầu; không tính đăng nhập, mở ca hay feedback từ assessment lỗi. | `số learner activated / số learner bắt đầu lộ trình có module đầu đã đến hạn` | Tuần/cohort; product analyst | NSM, usage depth; R2 |
| 3 | L | **Cost/Job thực tế**: toàn bộ LLM, infra, retry, QA và escalation của ca đã hoàn thành; không tính chi phí R&D hay lấy số ca thử làm mẫu số. Ghi cả chi phí attempt thất bại vào tử số. | `COGS AI + infra + retry + HITL / số ca hoàn thành hợp lệ` | Tuần; finance + infra | GM; R3 |
| 4 | O | **Usage depth**: seat đã mua/được giao có ≥1 ca nộp hợp lệ trong tuần; không tính tài khoản test, chỉ login hoặc ca nháp. | `seat hoạt động hợp lệ / seat được giao đủ điều kiện` | Tuần/đại lý; CS | Gia hạn/NRR; R4 |
| 5 | O | **POC → paid**: pilot đã kết thúc có hợp đồng trả tiền và thanh toán; không tính LOI, đề xuất giá hoặc pilot còn mở. | `pilot kết thúc chuyển trả tiền / pilot đã kết thúc trong kỳ` | Tháng/quý; sales ops | CAC payback; R5 |
| 6 | O | **North Star — tỷ lệ ca đạt chuẩn**: ca được giao đã đến hạn có ít nhất một bài nộp đạt rubric, nguồn current; không tính retry cùng ca, ca hủy/chưa đến hạn. Báo kèm số ca và số sales. | `cặp learner–case đạt chuẩn / cặp learner–case đủ điều kiện đến hạn` | Theo module, tổng hợp tuần; đội đào tạo | Usage depth, renewal/GM; R2/R4 |
| 7 | G | **GM thực tế**: doanh thu ca đã thu trừ COGS tương ứng; không dùng GM dự phóng làm thực tế, không gộp doanh thu chưa thu. | `(doanh thu thuần − COGS thực) / doanh thu thuần` | Tháng; finance | Đèn kết quả; R3 |
| 8 | G | **CAC payback thực tế**: chi phí kênh/triển khai bán hàng cho khách mới chia lợi nhuận gộp tháng từ khách mới; không lấy *ngân sách* CAC thay số thực. | `CAC thực / (ARPU thực × GM thực)` tháng | Quý; finance | Đèn kết quả; R5 |

**Đèn chi phí AI:** #3. Chuỗi nhân quả cần kiểm chứng: #1/#2 → #4/#6 → #5 → #8; #3 → #7. “Báo trước” là giả thuyết có thể bác bỏ, chưa khẳng định quan hệ nhân quả từ dữ liệu chưa có.

## Trạm 3 — Ngưỡng và nguồn

Quy ước biên: chạm giới hạn nguy hiểm thì vào màu nguy hiểm hơn; khi thiếu mẫu, trạng thái là `—`, không ép màu. [MH] = tính từ mô hình Day 22; [TB] = tiêu chuẩn pilot tự đặt có lịch đo lại. Không sử dụng [BM].

| # | Đèn | 🟢 | 🟡 | 🔴 | Nguồn và lý do |
| --- | --- | --- | --- | --- | --- |
| 1 | TTFV | `<30 ngày` | `30–60 ngày` | `>60 ngày` | [TB] Cổng ngày 60 cần first value trong 30 ngày; 60 ngày là hai chu kỳ cần đổi phạm vi pilot. Đo lại sau ≥2 pilot ngày 08/12/2026. |
| 2 | Activation phản hồi | `≥70%` | `50–<70%` | `<50%` | [TB] Giả thuyết: ít nhất một nửa sales phải thấy phản hồi trước khi tối ưu chuyển đổi; thay bằng baseline cohort đầu ngày 08/11/2026. |
| 3 | Cost/Job | `≤$0.2983` | `>$0.2983–$0.3960` | `>$0.3960` | [MH] $0.2983 là 120% cost mô hình; $0.3960 là trần COGS tại GM tối thiểu 60% với giá $0.99. Xem MH-1. |
| 4 | Usage depth | `≥60%` | `30–<60%` | `<30%` | [TB] Thử nghiệm mức dùng trong tài khoản; đọc theo từng đại lý để tránh tài khoản lớn che tài khoản nhỏ. Đo lại ngày 08/12/2026. |
| 5 | POC → paid | `≥50%` | `35–<50%` | `<35%` | [TB] Mốc vận hành khởi đầu từ bảng B2B §3.2; chưa gọi là benchmark vì chưa xác minh nguồn gốc phù hợp với pilot nhỏ. Chỉ phân màu khi ≥5 pilot đã kết thúc. |
| 6 | North Star | `≥60%` | `40–<60%` | `<40%` | [TB] Mục tiêu học tập tạm để thử rubric và nguồn chính sách; cần baseline từ cohort đầu đủ hạn vào 08/11/2026. |
| 7 | GM thực tế | `≥74.89%` | `60–<74.89%` | `<60%` | [MH] 74.89% là biên mô hình; 60% là sàn quản trị tương ứng Cost/Job ≤$0.396. Chỉ tính khi có doanh thu/COGS thực. Xem MH-2. |
| 8 | CAC payback | `≤12 tháng` | `>12–15 tháng` | `>15 tháng` | [MH] 12 tháng từ ARPU $300, GM 74.89% và ngân sách CAC $2,695.92; 15 tháng là biên chịu đựng 1.25× do bài này đặt. Xem MH-3. |

### Phụ lục [MH] — phép tính có thể đối chiếu

**MH-1 — Cost/Job:** Day 22 dự phóng `203.87 / 820 = $0.24862 ≈ $0.2486/ca`. Vùng xanh có đệm 20% cho sai số pilot: `0.2486 × 1.20 = $0.29832 ≈ $0.2983`. Với giá `$0.99/ca`, sàn GM 60% cho phép COGS tối đa `0.99 × (1−0.60) = $0.3960/ca`. Vậy xanh `≤0.2983`, vàng `(0.2983, 0.3960]`, đỏ `>0.3960`. Đệm 20% là quyết định quản trị, không phải benchmark.

**MH-2 — Gross margin:** Biên từ số chưa làm tròn: `(0.99−0.2486)/0.99 = 74.8889% ≈ 74.89%`. Nếu Cost/Job lên `$0.3960`, GM chỉ còn `(0.99−0.396)/0.99 = 60%`. Bởi vậy GM xanh `≥74.89%`, vàng `[60%,74.89%)`, đỏ `<60%`. Đây là phép tính ngưỡng, không chứng minh GM thực tế đã đạt.

**MH-3 — CAC payback:** Lãi gộp mô hình mỗi đại lý/tháng: `$300 × 0.7489 = $224.67`. Ngân sách CAC để hoàn vốn 12 tháng: `$224.67 × 12 = $2,696.04`; bài Day 22 dùng GM chưa làm tròn để ra `$2,695.92`. Chênh lệch **$0.12** do làm tròn GM. Để khớp đầu vào Day 22, dùng chính `$2,695.92 / ($300 × 0.7488667) ≈ 12 tháng`. Biên vàng 15 tháng tương đương `1.25 × $2,695.92 = $3,369.90` nếu ARPU/GM không đổi. Đèn chỉ sáng khi có CAC, ARPU và GM **thực tế**; hiện chưa có.

**Lưu ý kiểm định số học:** Day 22 nêu $0.2486/ca và GM 74.89%, nên `$300 × 74.89% × 12 = $2,696.04`, không phải $2,695.92. Worksheet giữ ngân sách đã công bố nhưng chỉ rõ sai khác làm tròn thay vì ngầm coi chúng bằng nhau tuyệt đối.

## Trạm 4 — Năm luật quyết định

Chỉ kích hoạt khi có dữ liệu hợp lệ. “KHÔNG THÌ” là hành động bị cấm khi điều kiện đỏ xảy ra, không phải nhánh `else` trong lập trình.

1. **R1 ⏹ TTFV.** **NẾU** TTFV `>60 ngày` **TRÊN** ít nhất 2 pilot đã bắt đầu, **THÌ** PM dừng nhận pilot diện rộng trong tuần kế tiếp, cắt mỗi pilot còn 1 use case/1 đội và chốt ngày demo ca đầu trong 14 ngày. **KHÔNG THÌ** tuyển thêm sales hay ký pilot rộng để che thời gian đưa giá trị tới khách.
2. **R2 Activation.** **NẾU** activation phản hồi `<50%` **TRONG** 2 cohort/module đầu liên tiếp **VÀ** mỗi cohort có ≥10 sales đủ điều kiện, **THÌ** product lead sửa luồng từ nộp bài tới xem phản hồi trong sprint tuần sau và đối chiếu 10 session bị rơi. **KHÔNG THÌ** tăng thông báo hay đẩy thêm ca học trước khi phản hồi đầu tiên đến được sales.
3. **R3 ⏹ Chi phí AI.** **NẾU** Cost/Job `>$0.3960` **TRONG** 2 tuần liên tiếp **VÀ** mỗi tuần có ≥50 ca hoàn thành, **THÌ** infra lead dừng quota ca miễn phí và tắt escalation tự động trong 48 giờ, sau đó kiểm tra token, retry và HITL theo `attempt_id`. **KHÔNG THÌ** tăng volume hoặc giảm giá khi mỗi ca đã vượt trần COGS.
4. **R4 Usage depth.** **NẾU** usage depth `<30%` **TRONG** 2 tuần liên tiếp **VÀ** đại lý có ≥20 seat đủ điều kiện, **THÌ** CS cùng quản lý đại lý mở 1 ca hướng dẫn 30 phút, giao 1 module cụ thể và kiểm tra bài nộp sau 7 ngày. **KHÔNG THÌ** bán thêm seat/module cho đại lý chưa dùng seat hiện có.
5. **R5 ⏹ POC → paid.** **NẾU** POC → paid `<35%` **TRÊN** ≥5 pilot đã kết thúc, **THÌ** sales lead dừng mở rộng kênh mới 2 tuần, hoàn thiện 1 Pilot Report có số và sửa điều kiện chọn pilot ngay sprint tới. **KHÔNG THÌ** giảm giá hàng loạt hoặc dùng LOI chưa thanh toán để báo “chuyển đổi”.

**Quy tắc thiếu mẫu:** chưa đạt mẫu tối thiểu thì ghi “chưa đủ mẫu”, thu log hoặc hoàn thành pilot; không bật luật đỏ và không báo xanh giả. Luật dừng R1/R3/R5 áp dụng cho hoạt động được nêu, không tự ý dừng sản phẩm toàn bộ.

## Đối chiếu bài nộp

- **Trạm 1:** 11/11 đèn bảng B2B được phân trạng thái; loại mô hình dựa trên người trả tiền/người dùng và vai trò LMS.
- **Trạm 2:** 8 thẻ, 3 Leading, có Cost/Job và đường báo trước; North Star giữ logic Day 20.
- **Trạm 3:** 8/8 đèn có ba màu, nguồn, lý do; MH-1/2/3 có phép tính; không dùng [BM] chưa kiểm chứng.
- **Trạm 4:** 5 luật có NẾU/TRONG hoặc TRÊN/THÌ/KHÔNG THÌ; 3 luật dừng ⏹; điều kiện mẫu cho metric dễ nhiễu.
