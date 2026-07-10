---
type: urd
feature: sport-matching
status: in-review
lang: vi
owner: "@hoangle"
created: 2026-06-04
updated: 2026-06-23
links:
  - docs/sport-matching/brainstorms/geo-skill-matching.md
  - docs/sport-matching/brainstorms/venue-search-booking.md
  - docs/sport-matching/brd.md
  - docs/sport-matching/prd.md
  - docs/sport-matching/srs/spec.md
tags: [urd, sport-matching]
stale_reason: ""
changelog:
  - '2026-06-25 | /review | fix BLOCKING: Mục 8 Out of Scope align với P1/P2 roadmap (chat CAP-22, social CAP-29, giải đấu CAP-27/28)'
  - 2026-06-23 | /urd | thêm user needs #8-#11 (tìm đặt sân), Partner needs #4-#6, Journey 4+5 từ brainstorm venue-search-booking
  - 2026-06-23 | /gap | status draft→in-review, added forward links BRD/PRD/SRS
  - '2026-06-04 | /urd | resolved OQ-1,OQ-2,OQ-3: peak hours, shared app, stats win/loss'
  - 2026-06-04 | /urd | initial URD draft từ brainstorm geo-skill-matching
---

# Sport Matching — User Requirements Document

> Người dùng *cần* gì ở feature Sport Matching? (góc user/persona)
> KHÔNG phải: kỹ thuật (SRS), business case (BRD).

## 1. Purpose

Doc này capture nhu cầu người dùng cho tính năng **Sport Matching** — ứng dụng ghép đối thủ thể thao theo vị trí GPS và trình độ, kết hợp đặt sân trực tiếp, và **tìm & đặt sân độc lập** (không cần ghép đôi). Dành cho UX, PM, BA review trước khi chuyển sang BRD/PRD/SRS.

Feature giải quyết 2 pain point chính:
1. Người chơi phải tìm đối thủ qua group Facebook — không lọc được trình độ hay vị trí.
2. Người chơi phải gọi điện từng sân hỏi lịch trống, không biết giá trước, không so sánh được nhiều sân.

## 2. User Types

| Tier | User Type | Role | Primary Goal | Pain Points |
|------|-----------|------|--------------|-------------|
| primary | Player (Người chơi) | Người chơi thể thao muốn tìm đối thủ ngang trình gần mình | Tìm đối thủ phù hợp nhanh, đặt sân tiện, chơi ngay | Phải qua group FB mất thời gian, không lọc được trình độ, không biết ai gần mình, đặt sân phải gọi điện |
| secondary | Partner (Chủ sân) | Chủ sở hữu/quản lý cơ sở thể thao | Lấp đầy slot sân, tiếp cận player mới qua nền tảng | Sân trống nhiều slot, khó tiếp cận người chơi ngoài khu vực, quản lý đặt sân thủ công |
| secondary | Staff (Nhân viên đối tác) | Nhân viên vận hành của Partner | Quản lý slot, xác nhận đặt chỗ, hỗ trợ player tại sân | Dễ trùng lịch, xử lý thủ công, thiếu công cụ quản lý |
| secondary | Admin (Quản trị viên) | Quản trị viên hệ thống | Giám sát toàn hệ thống, xử lý gian lận, moderate đánh giá | Cần dashboard tổng quan, phát hiện hành vi bất thường, quản lý user/partner |

**Persona Player chi tiết:**
- **Độ tuổi:** 25-40 (người đã đi làm, có thu nhập ổn định)
- **Thành thạo công nghệ:** quen dùng app mobile, mong muốn giao diện trực quan và quy trình đơn giản (ít thao tác nhất có thể)
- **Thói quen thể thao:** chơi thường xuyên theo nhóm hoặc cá nhân, chủ yếu vào khung giờ cao điểm (sau giờ làm, cuối tuần)
- **Môn ưu tiên:** cầu lông, pickleball (đang hot), mở rộng multi-sport

## 3. User Needs

### Primary user: Player

1. "Tôi muốn mở app là tìm được người chơi gần tôi ngay" — xem bản đồ khu vực, thấy ngay ai đang tìm trận, không phải đăng bài chờ reply.
2. "Tôi muốn biết đối thủ chơi có tốt không trước khi nhận trận" — xem trình độ, rating từ người chơi khác, lịch sử trận để quyết định có chơi không.
3. "Tôi muốn đặt sân luôn, không phải gọi điện hỏi" — chọn sân + giờ ngay trong app, biết slot nào còn trống, không cần liên hệ riêng.
4. "Tôi muốn được ghép đúng trình độ" — không chơi với người quá giỏi (nản) hay quá yếu (chán), hệ thống tự điều chỉnh trình độ qua thời gian.
5. "Tôi muốn biết rõ khi nào, ở đâu, chơi với ai" — sau khi match thành công, nhận thông tin đầy đủ: tên đối thủ, sân, giờ, vị trí trên bản đồ.
6. "Tôi muốn đánh giá đối thủ sau trận" — để giúp hệ thống ghép tốt hơn lần sau, và để mình biết ai chơi fair.
7. "Tôi muốn xem lịch sử trận và biết mình tiến bộ thế nào" — danh sách trận đã chơi (sân, giờ, đối thủ), thống kê win/loss, rating nhận được từ đối thủ sau mỗi trận.
8. "Tôi muốn tìm sân theo khu vực, môn, ngày, giá — không cần ghép đối thủ" — tìm sân độc lập khi đã có nhóm chơi, xem hình ảnh, giá, lịch trống, đánh giá, tiện ích để so sánh.
9. "Tôi muốn đặt sân online, thanh toán hoặc giữ chỗ trước" — chọn sân con + khung giờ, thanh toán ngay hoặc giữ chỗ 30 phút, chờ chủ sân duyệt trong 30 phút.
10. "Tôi muốn hủy hoặc đổi giờ khi có việc đột xuất" — hủy booking với chính sách hoàn tiền rõ ràng (trước 24h hoàn 100%, 2-12h hoàn 50%, dưới 2h không hoàn). Đổi giờ/sân 1 lần nếu trước 24h.
11. "Tôi muốn đánh giá sân sau khi chơi" — chấm 1-5 sao + review, nhận điểm thưởng tích lũy. Giúp người chơi khác chọn sân tốt hơn.

### Secondary users

**Partner (Chủ sân):**
1. Muốn đăng thông tin sân lên nền tảng (tên, địa chỉ, môn hỗ trợ, slot giờ, giá, hình ảnh tối thiểu 3 tấm) để player tìm thấy. Admin duyệt trước khi hiển thị.
2. Muốn biết slot nào đã được đặt, slot nào còn trống — quản lý dễ dàng.
3. Muốn tiếp cận lượng player mới ngoài tệp khách quen.
4. Muốn duyệt hoặc từ chối booking trong 30 phút — nhận noti khi có booking mới.
5. Muốn block khung giờ khi sân bảo trì hoặc đã có khách offline.
6. Muốn xem đánh giá sân từ player để cải thiện dịch vụ.

**Staff (Nhân viên đối tác):**
1. Muốn xem và xác nhận đặt chỗ nhanh, tránh trùng lịch.
2. Muốn hỗ trợ player khi có vấn đề tại sân.

**Admin (Quản trị viên):**
1. Muốn giám sát tổng quan hệ thống: số user, số trận, revenue.
2. Muốn phát hiện và xử lý gian lận (fake trình độ, đánh giá ác ý).
3. Muốn quản lý user/partner: kích hoạt, tạm khóa, moderate nội dung.

## 4. User Journeys

### Journey 1: Player tìm đối thủ + đặt sân (luồng chính)

1. Player mở app, bản đồ hiện vị trí hiện tại (GPS tự động)
2. Player chọn môn thể thao muốn chơi
3. Bản đồ hiện danh sách đối thủ gần, kèm trình độ và rating
4. Player điều chỉnh bán kính/trình độ nếu cần
5. Player chọn đối thủ muốn chơi cùng
6. Player chọn sân + slot giờ phù hợp
7. Đối thủ nhận thông báo mời, xem thông tin trận
8. Đối thủ nhấn chấp nhận
9. Cả 2 nhận thông báo xác nhận: thông tin đối thủ + sân + giờ
10. Trước trận 1 giờ, cả 2 nhận nhắc nhở

```
Player mở app ──► Bản đồ + GPS
       │
       ▼
  Chọn môn ──► Hiện đối thủ gần
       │
       ▼
  Chọn đối thủ ──► Chọn sân + giờ
       │
       ▼
  Gửi lời mời ──► Đối thủ nhận thông báo
       │                    │
       │              Accept / Reject
       │                    │
       ▼                    ▼
  Match xác nhận ◄── Cả 2 nhận thông tin
```

### Journey 2: Player đăng ký + setup profile

1. Player tải app, mở lần đầu
2. Nhập email + mật khẩu + tên hiển thị
3. Nhận OTP qua email, nhập xác thực
4. Chọn ít nhất 1 môn thể thao yêu thích
5. Tự đánh giá trình độ cho từng môn (Mới chơi / Trung bình / Nâng cao)
6. Profile sẵn sàng, app hiện bản đồ chính

### Journey 3: Player đánh giá sau trận

1. Trận đấu kết thúc, Player nhận nhắc nhở đánh giá
2. Mở app, vào trận vừa chơi
3. Chấm rating cho đối thủ + nhận xét ngắn (optional)
4. Gửi đánh giá, hệ thống cập nhật rating đối thủ
5. Nếu đánh giá cho thấy trình độ thực tế khác khai báo, hệ thống tự điều chỉnh dần

### Journey 4: Player tìm & đặt sân độc lập (không ghép đối thủ)

1. Player mở tab Tìm sân (từ tab chính / search bar / trang chủ)
2. Chọn bộ lọc: môn thể thao, khu vực, ngày, khoảng giá
3. Xem danh sách sân phù hợp (hình ảnh, giá, đánh giá, khoảng cách)
4. Chọn sân, xem chi tiết: lịch trống real-time, tiện ích, vị trí bản đồ
5. Chọn sân con (Sân A, Sân B) + khung giờ
6. Chọn thanh toán ngay hoặc giữ chỗ 30 phút
7. Chờ chủ sân duyệt trong 30 phút
8. Chủ sân duyệt → nhận noti xác nhận với đầy đủ thông tin
9. Sau buổi chơi → nhận nhắc đánh giá sân, được điểm thưởng

```
Player mở Tìm sân ──► Lọc môn/khu vực/ngày/giá
       │
       ▼
  Danh sách sân ──► Chọn sân chi tiết
       │
       ▼
  Chọn sân con + giờ ──► Thanh toán / Giữ chỗ 30p
       │
       ▼
  Chờ chủ sân duyệt (30p)
       │
  ┌────┴────┐
  │         │
 Duyệt   Từ chối
  │         │
  ▼         ▼
Confirmed  Hoàn tiền
  │
  ▼
Đánh giá sân + điểm thưởng
```

### Journey 5: Chủ sân đăng sân + quản lý booking

1. Chủ sân mở "Quản lý sân", chọn "Đăng sân mới"
2. Nhập thông tin: tên, địa chỉ, tọa độ, môn, giá/giờ, tiện ích, upload ≥3 ảnh
3. Thêm danh sách sân con + khung giờ hoạt động
4. Submit → chờ Admin duyệt
5. Admin duyệt → sân hiển thị cho player
6. Nhận noti khi có booking mới → duyệt/từ chối trong 30 phút
7. Block khung giờ khi cần (bảo trì, khách offline)

## 5. User-side Constraints

- **Mobile only:** Android + iOS (TestFlight giai đoạn đầu). Tất cả roles (Player, Partner, Staff, Admin) dùng chung 1 app với quyền khác nhau. Không có phiên bản web hay dashboard riêng.
- **Internet liên tục:** yêu cầu kết nối ổn định để GPS hoạt động, nhận push notification real-time, và thực hiện giao dịch thanh toán liền mạch.
- **GPS bắt buộc:** Player phải bật quyền truy cập vị trí để hệ thống matching hoạt động. Không có GPS thì không thể tìm đối thủ/sân.
- **Tiếng Việt only:** giao diện và nội dung tiếng Việt, phục vụ thị trường Việt Nam.
- **1 match tại 1 thời điểm:** Player chỉ được có 1 trận đang chờ xác nhận, không tạo song song nhiều match.

## 6. Assumptions

- Player sở hữu smartphone Android/iOS đời từ 2020 trở lên, có GPS.
- Player có Internet 4G+ ổn định khi sử dụng app.
- Player biết đọc tiếng Việt.
- Player chơi thể thao ít nhất 1-2 lần/tuần (có nhu cầu tìm đối thủ thường xuyên).
- Player 25-40 tuổi, đi làm, có thu nhập để chi trả dịch vụ đặt sân.
- Player sẵn sàng tự đánh giá trình độ ban đầu (hệ thống điều chỉnh dần qua ELO-based rating).
- Partner (chủ sân) cung cấp dữ liệu slot giờ chính xác và cập nhật thường xuyên.
- Thị trường: Việt Nam, tập trung thành phố lớn (TP.HCM, Hà Nội, Đà Nẵng) giai đoạn đầu.
- Khung giờ cao điểm: 17h-22h ngày thường + cả ngày cuối tuần — Partner cần tập trung slot vào khung này, system ưu tiên gợi ý.

## 7. Success Criteria (user-facing)

- Player tìm được đối thủ phù hợp trong vòng **3 phút** kể từ khi mở app (trung bình).
- Player đặt sân trực tiếp trên app mà **không cần gọi điện** hỏi chủ sân.
- Đối thủ được ghép **đúng trình độ** — tỷ lệ Player hài lòng với trình độ đối thủ ≥ 70%.
- Player nhận đủ thông tin trận (đối thủ + sân + giờ) **ngay khi match xác nhận** qua notification.
- Player quay lại chơi trận thứ 2 ≥ **40%** (retention tuần đầu).
- Rating trung bình đánh giá trải nghiệm app ≥ **4.0/5**.
- Tỷ lệ invite được chấp nhận ≥ **50%**.

## 8. Out of Scope

- **Không phải mạng xã hội (v1.0):** không có chat, feed, đăng bài, theo dõi bạn bè, bình luận trong phiên bản đầu. Chat 1-1 thuộc P1 roadmap (CAP-22); Social Feed thuộc P2 roadmap (CAP-29).
- **Không tổ chức giải đấu / tournament (v1.0):** v1.0 chỉ ghép trận đơn lẻ. Giải đấu + ghép đội thuộc P2 roadmap (CAP-27, CAP-28).
- **Không bán dụng cụ thể thao:** không có marketplace, không e-commerce sản phẩm.
- **Không có phiên bản web cho Player:** chỉ mobile app.
- **Không hỗ trợ offline:** tất cả tính năng yêu cầu internet liên tục.
- **Không hỗ trợ đa ngôn ngữ:** chỉ tiếng Việt giai đoạn hiện tại.

## 9. Open Questions

- [x] OQ-1: Khung giờ cao điểm — Resolved: 17h-22h ngày thường + cả ngày cuối tuần.
- [x] OQ-2: Partner/Staff truy cập — Resolved: dùng chung app với role khác nhau, không dashboard riêng.
- [x] OQ-3: Lịch sử trận — Resolved: cần cả danh sách trận cơ bản (sân, giờ, đối thủ) VÀ thống kê chi tiết (win/loss, rating từ đối thủ sau mỗi trận) để Player theo dõi tiến bộ.
