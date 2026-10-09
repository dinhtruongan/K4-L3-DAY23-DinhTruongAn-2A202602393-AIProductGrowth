# OPERATING DASHBOARD — P-145

**Loại:** B2B · **Cập nhật:**09/10/2026 · Đinh Trường An —2A202602393  
**Câu chốt:** P-145 là B2B vì doanh nghiệp duyệt ngân sách vận hành HR, nhân viên/HR dùng nội bộ chính doanh nghiệp đó; nhân viên không phải khách hàng downstream và Teams chỉ là điểm nhúng, chưa có partner phân phối.  
**NORTH STAR:** TTFV — hiện N/A; mục tiêu≤16 ngày. **Nhịp:** ngày5 phút, tuần30 phút, tháng/quý kiểm chứng; Trường An lấy số, HR xác nhận; cổng có người ngoài được mời (chưa xác nhận). Đơn vị tiền USD.

### Đèn báo sớm — Leading

| # Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn | Báo trước / luật |
|---|---|---|---|---|
| 1 TTFV (ngày) | N/A: chưa pilot | ≤16 ngày / >16–30 ngày / >30 ngày | [TB] dự kiến | POC→paid (#6), sau 2–4 tuần; CAC payback (#8), sau 1–3 tháng; R1 |
| 2 Pipeline coverage | N/A: chưa CRM | ≥4 × / ≥3 × và <4 × / <3 × | [MH] M1 | POC→paid (#6) và payback (#8), sau 4–12 tuần; R2 |
| 3 p95 AI/infra budget ratio | N/A; model 0.332376 | ≤0.332376 / >0.332376 và ≤1 / >1 | [MH] M2 | GM (#7), sau 1–4 tuần; R3 |

### Đèn vận hành — Operating

| # Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn | Báo trước / luật |
|---|---|---|---|---|
| 4 FAQ completion rate | N/A; proxy offline 19/42=45.24% | ≥45% / ≥35.1152% và <45% / <35.1152% | [MH] M3 | GM (#7) và payback (#8), sau 2–4 tuần; R4 |
| 5 Implementation cost / ACV | N/A; model 4.1152% | ≤4.1152% / >4.1152% và ≤17.9000% / >17.9000% | [MH] M4 | GM (#7), CAC payback hiệu chỉnh setup (#8), sau 1–3 tháng; R5 |
| 6 POC→paid | N/A: chưa pilot kết thúc | ≥60% / ≥40% và <60% / <40% | [TB] dự kiến | CAC payback (#8), sau 1–2 tháng; R2: xử lý phễu trước giảm giá |

### Đèn kết quả — Lagging

| # Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn | Luật |
|---|---|---|---|---|
| 7 Gross margin | N/A; model 75.7153% | ≥75.7153% / ≥60% và <75.7153% / <60% | [MH] M5 | R3/R4: sửa chi phí/chất lượng |
| 8 CAC payback (tháng) | N/A; model 2.6089 tháng | ≤2.6089 tháng / >2.6089 và ≤12 tháng / >12 tháng | [MH] M6 | R2/R5: chặn tăng acquisition |

N/A=chưa đo, không tô màu; số model không phải actual. [TB] tạm: đo2 chu kỳ rồi lập baseline (TTFV08/12; POC07/01). Ngưỡng cố định r/ACV/chi phí theo baselineDay22; đổi gói/volume thì tính lại theo worksheet. Vàng: lập ticket trong1 ngày, hạn14 ngày giải thích bằng chứng. Xanh: giữ; không tự động tăng ngân sách.

### 5 luật quyết định (⏹=dừng)

1. ⏹ R1 — NẾU TTFV >30 ngày TRÊN cả 2 pilot gần nhất đã đủ tuổi 30 ngày, THÌ Trường An dừng nhận pilot rộng trong ngày làm việc kế tiếp và cắt xuống một nhóm/một bộ FAQ, dành 14 ngày sửa data onboarding; KHÔNG THÌ không tuyển sales hoặc thêm khách vào luồng chưa tạo value. Khách pending quá30 ngày cũng kích hoạt, không đợi họ có value.
2. R2 — NẾU pipeline coverage <3 × TRONG 2 lần chốt tuần liên tiếp sau ngày30, THÌ Trường An dành tuần kế tiếp liên hệ6 HR đúng ICP, loại cơ hội thiếu sponsor và hẹn2 buổi xác minh nhu cầu; KHÔNG THÌ không giảm giá hoặc cộng lead chưa đủ điều kiện để làm đẹp coverage.
3. ⏹ R3 — NẾU p95 AI/infra budget ratio >1 TRONG 2 cửa sổ 7 ngày liên tiếp VÀ mỗi cửa sổ ≥100 attempts thật đã được log đủ (từng tenant vi phạm vẫn được kiểm tra riêng), THÌ Trường An đóng băng tăng quota/tích hợp tốn phí trong24 giờ, áp hard cap đã thống nhất và chạy lại token/retry/QA trong48 giờ; KHÔNG THÌ không chuyển sang model rẻ hơn khi chưa qua eval và không bỏ log hoặc QA. Chỉ mở cap khi 2 cửa sổ kế tiếp ≤1.
4. ⏹ R4 — NẾU FAQ completion <35.1152% TRONG 2 cohort14 ngày đã trưởng thành VÀ mỗi cohort≥100 attempts, THÌ Trường An dừng chào bán thêm quota, chuyển ca không chắc cho HR và sửa retrieval trên50 ca lỗi trong14 ngày; KHÔNG THÌ không tính citation hay im lặng là completion và không tăng acquisition để bù ca thất bại.
5. ⏹ R5 — NẾU implementation cost/ACV >17.9000% TRÊN 2 khách triển khai liên tiếp đã đóng sổ giờ công, THÌ Trường An dừng nhận tùy biến cùng gói ngay tuần kế tiếp, chuẩn hóa1 connector và báo giá phần setup riêng trước nhận khách tiếp; KHÔNG THÌ không lấy giờ founder miễn phí để che cost hoặc ký thêm khách cùng scope/giá.

### Cổng gác 90 ngày

| Ngày | Metric (1) | Ngưỡng | Bằng chứng | Nếu trượt |
|---|---|---|---|---|
| 30 · 08/11/2026 | Pilot learning-ready count | ≥2 pilot bắt đầu thật | 2 biên bản HR xác nhận, phạm vi/consent và Evidence Pack v1 gắn từng pilot | GO nếu đạt; FIX30 ngày nếu thiếu thủ tục có HR sponsor; PIVOT nếu ICP không cho data; KILL nếu đã FIX vẫn0. |
| 60 · 08/12/2026 | TTFV của 2 pilot gần nhất | Mỗi pilot ≤30 ngày | Timeline ký/bắt đầu, log FAQ đầu, HR/nhân viên xác nhận, kiểm tra reopen7 d; pending >30 là trượt | GO nếu đạt; FIX30 ngày nếu lỗi onboarding xác định và chưa FIX; PIVOT nếu không tìm được value; KILL nếu hết lần FIX vẫn trượt. |
| 90 · 07/01/2027 | Evidence-backed expansion count | ≥1 cơ hội mở rộng trong tenant cũ | Pilot Report có n/r/chi phí trước-sau + biên bản HR sponsor xác nhận scope/giá/lịch quyết định của cơ hội | GO nếu đạt; FIX30 ngày nếu chỉ thiếu hồ sơ và chưa FIX; PIVOT nếu khách không có nhu cầu; KILL khi cùng lỗi đã FIX và vẫn0. |

**GO** khi qua metric, trong ngân sách được duyệt; **FIX** tối đa1 lần cùng lỗi/30 ngày; giả định gốc sai→**PIVOT**, FIXkhông cải thiện→**KILL**. Runway chưa rõ: không GO tăng chi tiêu.

**KILL CRITERIA:** Tại 07/01/2027, nếu số pilot đã đạt TTFV≤30 ngày vẫn bằng0 sau một lần FIX30 ngày cho cùng vấn đề, dừng hướng FAQ onboarding của ICP này; không gia hạn thử nghiệm hoặc tăng acquisition.

**CHƯA ĐO ĐƯỢC:** TTFV/pipeline/POC: cần consent và CRM, log kickoff/value/payment; 2 chu kỳ dự kiến08/11–08/12 (TTFV) và08/12–07/01 (POC). Cost/r/GM/payback: cần token, retry, giờQA, xác nhận/reopen7 d, invoice và ledger; tracking bản thử16/10, số thật đầu15/11 nếu pilot01/11 được xác nhận. Runway: thiếu cash/burn, lấy số16/10; chưa được duyệt thì không GO tăng chi tiêu. Chủ trì: Trường An.
