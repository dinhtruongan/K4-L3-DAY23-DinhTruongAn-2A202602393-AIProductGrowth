# Worksheet — P-145 Onboarding Buddy

Họ tên: Đinh Trường An · MSSV/MHV: 2A202602393 · Ngày làm:09/10/2026

## Số liệu đầu vào

| Input Day22 | Giá trị | Nguồn / trạng thái |
|---|---|---|
| ARPU | $121.50/tháng | 4_Channel_Fit!B5 · dự toán |
| GM | 75.7153% | 2_Pricing!B21 · dự toán |
| CAC | $240 | 4_Channel_Fit!B22 · CPO60/win25%, chưa thực đo |
| Payback cap | 12 tháng | 4_Channel_Fit!B8 · giả định SMB của model |
| Runway | Chưa có | Chưa có cash và net burn; Trường An bổ sung16/10, không tự đặt6 tháng |
| COGS/job / đủ overhead | $0.06556878 / $0.08779100 | 1_Cost_Job!B66:B67; 1,000 attempts×45%=450 |
| Value Metric | $18/tenant + $0.23/FAQ; hiệu dụng$0.27 | 3_Value_Metric!B30/B32; chưa billing thực |
| Quota/ACV mục tiêu90 ngày | 3 paid×$1,458=$4,374 | Day22 5_90 Day_Plan!C13 và4_Channel_Fit!B10 |

Nguồn: [Day22 model](https://github.com/dinhtruongan/Track1_Day22_2A202602393_DinhTruongAn/blob/main/DinhTruongAn_Day22_model.xlsx). Input thương mại là giả định Day22, không phải kết quả khách hàng; chưa có runway. Ngày0 của kế hoạch:09/10/2026, D30/D60/D90 cộng đúng30/60/90 ngày. Thời điểm có số phụ thuộc pilot và quyền dữ liệu; quá hẹn vẫn N/A, không điền số0.

## Trạm 1 — Loại mô hình

**Câu chốt loại:** P-145 là B2B vì doanh nghiệp duyệt ngân sách vận hành HR, nhân viên/HR dùng nội bộ chính doanh nghiệp đó; nhân viên không phải khách hàng downstream và Teams chỉ là điểm nhúng, chưa có partner phân phối.

**Bảng đèn §3.2** (đủ11 đèn B2B):

| Đèn | ✅/🔧/❌ | Số nằm ở đâu / cần gì để đo |
|---|---|---|
| TTFV | 🔧 | Pilot kickoff/value + reopening log;16/10 instrument,08/12 hai chu kỳ |
| Pipeline coverage | 🔧 | CRM qualified/sponsor/ACV/expected close;16/10 có schema, chưa có deal |
| Deal chết security/procurement | 🔧 | CRM closed lost reason/closed denominator;16/10 schema,2 tháng mới đủ mẫu |
| POC→paid | 🔧 | Pilot end + payment ledger;16/10 schema,07/01/2027 baseline |
| Sales cycle | 🔧 | Qualified→signed timestamps;16/10 schema, chưa có chữ ký |
| Usage depth | 🔧 | Roster có quyền + distinct completed FAQ theo tuần;16/10 schema,15/11 số đầu nếu có pilot |
| Implementation cost/ACV | 🔧 | Timesheet + rate + integration invoice;16/10 biểu mẫu,08/12 đối chiếu2 khách |
| Revenue concentration | 🔧 | Revenue tenant ledger;16/10 schema;15/11 nếu phát sinh paid |
| NRR | ❌ | Chưa có cohort doanh thu gia hạn, không thể quan sát90 ngày; tối thiểu2 quý sau paid đầu mới có ý nghĩa |
| Gross margin | 🔧 | COGS ledger + revenue nhận diện;16/10 schema,15/11 số đầu nếu có paid |
| CAC payback | 🔧 | Acquisition labor/cash + paid cohort contribution;16/10 ledger,15/11 số đầu nếu có paid |

🔧 nghĩa là có thể dựng cách đo trong2 tuần, không hứa đã có cohort2 chu kỳ trong2 tuần. NRR❌ nghĩa là chưa đo được trong horizon90 ngày; đã biết phải đợi cohort thật, không bịa giá trị gia hạn.

## Trạm 2 — Thẻ đèn

**North Star:** TTFV khách B2B — hiện N/A — mục tiêu≤16 ngày; hiển thị từng pilot và pending để không lọc bỏ khách thất bại.

| # | Tầng | Đèn | Định nghĩa (đếm / không đếm) | Công thức | Nhịp / người lấy | Báo trước cho |
|---|---|---|---|---|---|---|
| 1 | L | TTFV (ngày) | Từ văn bản đồng ý bắt đầu pilot đến FAQ đầu đúng, có nguồn, được nhân viên thật xác nhận và không mở lại 7 ngày; không tính demo, cài xong hoặc tài khoản test. Khách chưa có value vẫn nằm trong danh sách với tuổi pilot, không loại khỏi mẫu. | Ngày xác minh value đầu − ngày bắt đầu pilot; median trên khách, kèm từng khách và số pending | Mỗi ngày; Trường An + HR xác minh | POC→paid (#6), sau 2–4 tuần; CAC payback (#8), sau 1–3 tháng |
| 2 | L | Pipeline coverage | Cơ hội đủ điều kiện cho đúng ICP, có HR sponsor, quyền dùng tài liệu và lịch quyết định trong quý 90 ngày; không tính lead lạnh, demo không sponsor, cơ hội hết hạn hoặc bị đếm hai lần. | Σ ACV cơ hội đủ điều kiện / target new ACV quý ($4,374 = 3 ×$1,458) | Hằng tuần; Trường An | POC→paid (#6) và payback (#8), sau 4–12 tuần |
| 3 | L | p95 AI/infra budget ratio | Dự báo chi phí LLM+retry+embedding+infra từng tenant cho 1 tháng; chia ngân sách biến đổi còn lại sau QA để giữ GM60%. Không dùng trung bình tenant, không chỉ đếm token output. | p95(V_i/[0.4 ×Revenue_i−QA_i]); V_i gồm actual + dự báo; ngân sách ≤0 là đỏ; p95 nearest-rank | Hằng ngày/7 ngày; Trường An | GM (#7), sau 1–4 tuần |
| 4 | O | FAQ completion rate | FAQ đúng đủ, nguồn hợp lệ, người thật xác nhận, không HR xử lý và không mở lại 7 ngày. Không coi retrieval/citation/không trả lời lại là thành công. | Số conversation đủ điều kiện / toàn bộ FAQ attempts trong cohort đã hết cửa sổ 7 ngày; thất bại, retry và bỏ ngang vẫn trong mẫu; retry không là attempt mới | Hằng tuần/cohort 14 ngày; Trường An + HR | GM (#7) và payback (#8), sau 2–4 tuần |
| 5 | O | Implementation cost / ACV | Giờ thiết lập, phê duyệt/map dữ liệu, connector, hướng dẫn, QA trước go-live × giá fully-loaded + phí tích hợp. Không gộp sales acquisition hay chi phí chạy đã tính theo job. | Chi phí triển khai một lần / ACV hợp đồng (baseline $1,458); pilot chưa có ACV dùng quote dự kiến và ghi riêng | Mỗi khách/hằng tuần; Trường An | GM (#7), CAC payback hiệu chỉnh setup (#8), sau 1–3 tháng |
| 6 | O | POC→paid | Pilot đã hết hạn 30 ngày, chuyển hợp đồng trả tiền và có invoice được thanh toán trong 14 ngày tiếp theo. Không đếm LOI, hứa mua, invoice chưa trả hoặc pilot đang chạy. | Pilot đã trả tiền / mọi pilot đã hết cửa sổ chuyển đổi (gồm từ chối và im lặng) | Hằng tháng; Trường An | CAC payback (#8), sau 1–2 tháng |
| 7 | G | Gross margin | Doanh thu phí nền+usage đã ghi nhận trừ toàn bộ COGS AI/infra/retry/QA/support trực tiếp; loại test nội bộ. Overhead R&D/sales trình bày riêng, không giấu support trực tiếp. | (Revenue−COGS)/Revenue; doanh thu0 → N/A | Hằng tháng, rà quý; Trường An | Bảng điểm cuối; đối chiếu đèn #3/#4/#5 |
| 8 | G | CAC payback (tháng) | Chi phí acquisition đã trả + giờ founder quy đổi / contribution tháng tenant trả phí; dùng cohort trả tiền, không dùng người trial hay khoản doanh thu chưa xác nhận. | CAC / (ARPU×GM); cohort chưa có paid hoặc contribution≤0 → N/A/không hữu hạn; setup theo #5 báo riêng | Hằng tháng, rà quý; Trường An | Bảng điểm cuối; đối chiếu pipeline và POC |

Đèn chi phí AI: **#3**, dùng forecast theo tenant trước khi hóa đơn làm xấu GM. Cây3 tầng: TTFV→POC→paid→CAC payback; pipeline→POC→paid→payback; AI budget ratio→completion/chi phí vận hành→GM. Độ trễ là giả thuyết cần kiểm tra, không phải quan hệ nhân quả đã chứng minh.

## Trạm 3 — Ngưỡng

| # | Đèn | 🟢 | 🟡 | 🔴 | Nguồn | Lý do |
|---|---|---|---|---|---|---|
| 1 | TTFV (ngày) | ≤16 ngày | >16–30 ngày | >30 ngày | [TB] dự kiến | Chưa có chuẩn, đo 2 chu kỳ rồi lấy baseline; mốc dự kiến 08/12. Tạm chọn 16 vì pilot 30 ngày dành 7 ngày kiểm tra mở lại và 7 ngày cho sửa/đối chiếu. |
| 2 | Pipeline coverage | ≥4 × | ≥3 × và <4 × | <3 × | [MH] M1 | Win 25% cần 1/0.25=4 ×; 3 × chỉ kỳ vọng 75% mục tiêu. Không dùng 3 × như benchmark ngành. |
| 3 | p95 AI/infra budget ratio | ≤0.332376 | >0.332376 và ≤1 | >1 | [MH] M2 | Baseline V=$9.505952; budget=$28.60; ngưỡng đỏ hết phần tiền giữ GM60%. Phải cập nhật revenue/QA thật theo tenant. |
| 4 | FAQ completion rate | ≥45% | ≥35.1152% và <45% | <35.1152% | [MH] M3 | Hybrid đủ overhead cần r≥35.1152% cho biên60% tại 1.000 attempts; xanh45% từ baseline, chưa phải số vận hành. |
| 5 | Implementation cost / ACV | ≤4.1152% | >4.1152% và ≤17.9000% | >17.9000% | [MH] M4 | Xanh từ setup60/ACV; đỏ khi setup không thu hồi trong 3 tháng contribution sau support, mục tiêu thu hồi do đội đề xuất cho pilot90 ngày. |
| 6 | POC→paid | ≥60% | ≥40% và <60% | <40% | [TB] dự kiến | Chưa có chuẩn, đo 2 chu kỳ rồi lấy baseline; dự kiến 07/01/2027. Tạm dùng 3/5, 2/5 pilot trưởng thành để phân biệt đủ/thiếu mục tiêu3 paid; không phải benchmark. |
| 7 | Gross margin | ≥75.7153% | ≥60% và <75.7153% | <60% | [MH] M5 | Xanh là baseline Day22; đỏ là GM tối thiểu dùng suy CAC và AI budget; chi phí thiếu chưa được tô xanh. |
| 8 | CAC payback (tháng) | ≤2.6089 tháng | >2.6089 và ≤12 tháng | >12 tháng | [MH] M6 | Baseline240/(121.5 ×75.7153%)=2.6089; đỏ vượt payback cap12 của Day22, chưa kiểm chứng churn/LTV. |

Không dùng ngưỡng[BM], vì chọn suy từ chính model và baseline chờ đo. Vì vậy không lấy các số lịch sử19 tuần/101%/53% trong handbook làm benchmark hiện hành. [TB] là ngưỡng tạm, chưa có chuẩn, đo2 chu kỳ rồi lấy làm baseline vào ngày ghi trên thẻ; N/A không được tô xanh/đỏ. Tỷ lệ mẫu nhỏ hiển thị cả tử/mẫu và tạm ngừng luật thống kê, không dừng xử lý lỗi an toàn.

### Phụ lục [MH] — phép tính

### M1 — Pipeline coverage [MH]
Mục tiêu new ACV quý=3 ×1.458=4.374 USD. Win giả định25% → coverage cần1/0.25=4 ×, pipeline17.496 USD. Ngưỡng vàng3 ×=13.122 USD chỉ cho expected booking3.280,50 USD, bằng75% target. Đỏ<3 × vì đã thiếu ít nhất25% target theo model; không giả vờ coi win25% là số thật.

### M2 — AI/infra budget ratio [MH]
Baseline revenue121.50; GM minimum60%; QA20/tháng. Budget biến đổi=(1−0.6)×121.50−20=28.60 USD/tenant/tháng. V baseline=1.3944 LLM+0.111552 retry+8 infra/embedding=9.505952. Ratio xanh≤9.505952/28.60=0.33237594; đỏ>1. Forecast_i thay input bằng revenue/QA thực hoặc theo gói đã thống nhất; nếu budget≤0, đánh đỏ và ngừng tăng quota. N<20 tenant vẫn hiển thị p95 nearest-rank kèm n và max; pilot2 tenant thì p95=max, không tự coi là thống kê đại diện thị trường.

### M3 — FAQ completion [MH]
N=1.000 attempts; tổng chi phí gồm overhead39.505952. Gói thật doanh thu18+0.23 ×1.000 ×r. Muốn biên sau overhead≥60%:18+230 r≥39.505952/0.4=98.76488 → r≥(98.76488−18)/230=0.351151652=35.1152%. Xanh45% là giả định Day22; vàng35.1152–<45%; đỏ<35.1152. Chỉ áp các mốc số trên ở volume/gói baseline; khi volume thay đổi tính r_min=((Cost_full/0.4)−18)/(0.23 ×N), chặn miền0..1 và ghi infeasible nếu>1. Eval19/42 offline không dùng làm actual completion.

### M4 — Implementation/ACV [MH]
ACV=121.50 ×12=1.458. Setup baseline60 → xanh60/1.458=4.115226%. Đội đề xuất thu hồi setup trong3 tháng pilot, không coi đây là chuẩn ngành. Contribution tháng trước setup=121.50−29.505952−5 support/R&D=86.994048; cap3 tháng=260.982144 → đỏ>260.982144/1.458=17.900010%; vàng>4.1152–≤17.9000%. Khoản5 đã có trong overhead Day22, không trừ thêm2 lần; cash acquisition240 và setup60 khác nhau, cần kiểm tra thực chi trước áp dụng.

### M5 — Gross margin [MH]
GM=(121.50−29.505952)/121.50=75.7152658%. Xanh≥baseline; vàng60%–<baseline; đỏ<60% là yêu cầu chất lượng kinh tế model. Nếu support5 là direct COGS, phải phân loại lại: GM=(121.50−34.505952)/121.50=71.6000% (vàng), không giấu chi phí bằng nhãn overhead. So sánh phải cùng định nghĩa COGS.

### M6 — CAC payback [MH]
Lãi gộp91.994048 USD/tháng. Baseline240/91.994048=2.6088644 tháng; budget12 ×91.994048=1.103,928576 USD. Xanh≤2.6089, vàng>2.6089–≤12, đỏ>12. Với GM60% budget12 ×121.50 ×0.6=874.80; chỉ ngân sách baseline không bảo đảm sống khi GM giảm. Setup60 báo riêng: payback acquisition+setup=(240+60)/91.994048=3.26108 tháng; nếu đã đưa setup vàoCAC thì không cộng lần hai.


## Trạm 4 — 5 luật quyết định

1. ⏹ R1 — NẾU TTFV >30 ngày TRÊN cả 2 pilot gần nhất đã đủ tuổi 30 ngày, THÌ Trường An dừng nhận pilot rộng trong ngày làm việc kế tiếp và cắt xuống một nhóm/một bộ FAQ, dành 14 ngày sửa data onboarding; KHÔNG THÌ không tuyển sales hoặc thêm khách vào luồng chưa tạo value. Khách pending quá30 ngày cũng kích hoạt, không đợi họ có value.
2. R2 — NẾU pipeline coverage <3 × TRONG 2 lần chốt tuần liên tiếp sau ngày30, THÌ Trường An dành tuần kế tiếp liên hệ6 HR đúng ICP, loại cơ hội thiếu sponsor và hẹn2 buổi xác minh nhu cầu; KHÔNG THÌ không giảm giá hoặc cộng lead chưa đủ điều kiện để làm đẹp coverage.
3. ⏹ R3 — NẾU p95 AI/infra budget ratio >1 TRONG 2 cửa sổ 7 ngày liên tiếp VÀ mỗi cửa sổ ≥100 attempts thật đã được log đủ (từng tenant vi phạm vẫn được kiểm tra riêng), THÌ Trường An đóng băng tăng quota/tích hợp tốn phí trong24 giờ, áp hard cap đã thống nhất và chạy lại token/retry/QA trong48 giờ; KHÔNG THÌ không chuyển sang model rẻ hơn khi chưa qua eval và không bỏ log hoặc QA. Chỉ mở cap khi 2 cửa sổ kế tiếp ≤1.
4. ⏹ R4 — NẾU FAQ completion <35.1152% TRONG 2 cohort14 ngày đã trưởng thành VÀ mỗi cohort≥100 attempts, THÌ Trường An dừng chào bán thêm quota, chuyển ca không chắc cho HR và sửa retrieval trên50 ca lỗi trong14 ngày; KHÔNG THÌ không tính citation hay im lặng là completion và không tăng acquisition để bù ca thất bại.
5. ⏹ R5 — NẾU implementation cost/ACV >17.9000% TRÊN 2 khách triển khai liên tiếp đã đóng sổ giờ công, THÌ Trường An dừng nhận tùy biến cùng gói ngay tuần kế tiếp, chuẩn hóa1 connector và báo giá phần setup riêng trước nhận khách tiếp; KHÔNG THÌ không lấy giờ founder miễn phí để che cost hoặc ký thêm khách cùng scope/giá.

Màu vàng: Trường An lập ticket nguyên nhân trong1 ngày làm việc, hạn14 ngày phải có bằng chứng/kết luận. Màu xanh: giữ phạm vi vận hành, không tự động tăng tiền. N/A: dựng cách đo trước; thiếu telemetry không được diễn giải là cost=0. Đèn#6/#7/#8 là kiểm chứng chuỗi và mức kinh tế, hành động qua luật được tham chiếu trên dashboard; không thêm luật thứ6 ngoài phạm vi bài.

## Trạm 5 — Cổng gác và điều chưa đo được

| Ngày | Metric duy nhất | Qua cổng | Bằng chứng | Nếu trượt |
|---|---|---|---|---|
| 30 · 08/11/2026 | Pilot learning-ready count | ≥2 pilot bắt đầu thật | 2 biên bản HR xác nhận, phạm vi/consent và Evidence Pack v1 gắn từng pilot | GO nếu đạt; FIX30 ngày nếu thiếu thủ tục có HR sponsor; PIVOT nếu ICP không cho data; KILL nếu đã FIX vẫn0. |
| 60 · 08/12/2026 | TTFV của 2 pilot gần nhất | Mỗi pilot ≤30 ngày | Timeline ký/bắt đầu, log FAQ đầu, HR/nhân viên xác nhận, kiểm tra reopen7 d; pending >30 là trượt | GO nếu đạt; FIX30 ngày nếu lỗi onboarding xác định và chưa FIX; PIVOT nếu không tìm được value; KILL nếu hết lần FIX vẫn trượt. |
| 90 · 07/01/2027 | Evidence-backed expansion count | ≥1 cơ hội mở rộng trong tenant cũ | Pilot Report có n/r/chi phí trước-sau + biên bản HR sponsor xác nhận scope/giá/lịch quyết định của cơ hội | GO nếu đạt; FIX30 ngày nếu chỉ thiếu hồ sơ và chưa FIX; PIVOT nếu khách không có nhu cầu; KILL khi cùng lỗi đã FIX và vẫn0. |

Pilot learning-ready là1 metric đếm pilot thỏa định nghĩa có scope/consent/đã bắt đầu và evidencev1; không phải2 metric gộp tùy ý. Expansion count chỉ đếm cơ hội có report đo số và xác nhận HR sponsor, không đếm lời hứa. Mỗi cổng GO chỉ mở chặng kế tiếp trong ngân sách đã duyệt; runway/cash chưa rõ thì không GO tăng chi tiêu. Cùng nguyên nhân chỉ FIX1 lần, ghi ngày/lỗi/hành động trong gate-log; quá30 ngày mà không cải thiện thì KILL, nếu giả định ICP sai thì PIVOT. Không được đổi metric để reset số lần FIX.

**KILL CRITERIA:** Tại 07/01/2027, nếu số pilot đã đạt TTFV≤30 ngày vẫn bằng0 sau một lần FIX30 ngày cho cùng vấn đề, dừng hướng FAQ onboarding của ICP này; không gia hạn thử nghiệm hoặc tăng acquisition.

**CHƯA ĐO ĐƯỢC:** TTFV/pipeline/POC: cần consent và CRM, log kickoff/value/payment; 2 chu kỳ dự kiến08/11–08/12 (TTFV) và08/12–07/01 (POC). Cost/r/GM/payback: cần token, retry, giờQA, xác nhận/reopen7 d, invoice và ledger; tracking bản thử16/10, số thật đầu15/11 nếu pilot01/11 được xác nhận. Runway: thiếu cash/burn, lấy số16/10; chưa được duyệt thì không GO tăng chi tiêu. Chủ trì: Trường An.

## Đối chiếu phản biện

Theo HANDBOOK§5.1–5.2: không coi FAQ đúng offline45.24% là actual containment; không lấy pipeline3 × làm chuẩn ngành; không bỏ khách pending khi đoTTFV; không dùng trung bình chi phí tenant; không tô xanh các forecast. Bản sửa có3 L/3 O/2 G,6 ngưỡng[MH],2 ngưỡng[TB] tạm và4 luật dừng. Không có pilot hay phản hồi khách được tạo ra để làm bằng chứng.
