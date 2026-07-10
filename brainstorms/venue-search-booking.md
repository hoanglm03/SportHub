---
type: brainstorm
feature: sport-matching
idea_slug: venue-search-booking
status: draft
mode: deep
lang: vi
owner: "@hoangle"
created: 2026-06-23
updated: 2026-06-23
complexity_flags: [has_state_machine, has_multi_role, has_async_flow, has_throttle_rules]
links:
  - docs/sport-matching/urd.md
  - docs/sport-matching/brd.md
  - docs/sport-matching/prd.md
  - docs/sport-matching/srs/spec.md
tags: [brainstorm, sport-matching, venue-booking]
stale_reason: ""
changelog:
  - '2026-06-23 | /brainstorm | resolved OQ-1: 500 user giai đoạn đầu'
  - 2026-06-23 | /brainstorm | initial brainstorm cho venue-search-booking, deep mode
---

# Tìm & Đặt sân thể thao

> Feature: sport-matching | Idea: venue-search-booking
> Tính năng bổ sung vào dự án Sport Matching — không phải feature độc lập.

## 1. Idea Seed

Người chơi thể thao hiện phải gọi điện từng sân để hỏi lịch trống, không biết giá trước, không so sánh được nhiều sân. Chủ sân thì khó tiếp cận khách hàng mới và quản lý lịch thủ công. Cần xây tính năng tìm kiếm sân theo nhiều tiêu chí và đặt sân online trong SportHub.

## 2. Context

- **Why now:** User request + đối thủ đã có feature tìm đặt sân.
- **Related:** Dùng chung hệ thống thanh toán premium-payment. Yêu cầu đăng nhập từ authentication. Tích hợp với matching flow hiện có (chọn sân khi ghép đôi).
- **Pain:** Cả người chơi lẫn chủ sân đều gặp khó khăn với quy trình thủ công.

## 3. User Types (preliminary)

| User Type | Pain Point | Primary Need |
|-----------|-----------|--------------|
| Người chơi (Player) | Khó tìm sân trống, phải gọi điện, không biết giá, không so sánh được | Tìm + đặt sân nhanh, xem giá và lịch trống, so sánh nhiều sân |
| Chủ sân (Venue Owner) | Khó tiếp cận khách mới, quản lý lịch thủ công | Đăng sân lên hệ thống, nhận booking online, quản lý lịch tập trung |
| Nhân viên sân (Staff) | Phụ thuộc chủ sân để xử lý booking | Hỗ trợ duyệt booking, quản lý lịch hàng ngày |
| Admin hệ thống | Cần kiểm soát chất lượng sân trên nền tảng | Duyệt sân mới, xử lý tranh chấp |

## 4. Capabilities Breakdown

### P0 — must have
- Tìm sân theo môn thể thao, khu vực, ngày, giá, hoặc combo tất cả
- Xem chi tiết sân: hình ảnh, giá, lịch trống, đánh giá, tiện ích
- Đặt sân: chọn sân con + khung giờ, thanh toán hoặc giữ chỗ
- Chủ sân duyệt/từ chối booking trong 30 phút
- Hoàn tiền tự động khi từ chối hoặc hết giờ duyệt
- Chủ sân đăng sân (admin duyệt trước khi hiển thị)
- Chủ sân block khung giờ (bảo trì, khách offline)
- Lịch trống cập nhật real-time
- Notification: in-app + push cho mọi sự kiện booking

### P1 — should have
- Đánh giá sân 5 sao + review text + điểm thưởng tích lũy
- Đổi giờ/sân 1 lần (trước 24h)
- Chính sách hủy + hoàn tiền 3 mức
- Cảnh báo/khóa chủ sân không duyệt nhiều lần

### P2 — nice to have
- Gợi ý sân theo lịch sử đặt
- Sân yêu thích (bookmark)
- So sánh nhiều sân cạnh nhau
- Ưu đãi/voucher cho user đặt thường xuyên

## 5. Core Flows (Happy Path)

### 5.1 Tìm & xem sân

1. User mở tab Tìm sân (từ tab chính / search bar / trang chủ / notification)
2. User chọn bộ lọc: môn thể thao, khu vực, ngày, khoảng giá (hoặc combo)
3. System hiển thị danh sách sân phù hợp (hình ảnh, giá, đánh giá, khoảng cách)
4. User chọn 1 sân để xem chi tiết
5. System hiển thị: hình ảnh, giá/giờ, lịch trống real-time, đánh giá, tiện ích, vị trí bản đồ
6. User chọn sân con cụ thể (Sân A, Sân B, ...) + xem khung giờ trống

### 5.2 Đặt sân (thanh toán ngay)

1. User chọn sân con + khung giờ
2. System tạm giữ khung giờ 10 phút (tránh concurrent booking)
3. User chọn "Thanh toán ngay"
4. System chuyển sang thanh toán (dùng chung premium-payment)
5. User thanh toán thành công
6. System tạo booking trạng thái **paid**, gửi noti chủ sân "Có booking mới, duyệt trong 30 phút"
7. Chủ sân nhận noti, mở app, xem chi tiết booking
8. Chủ sân duyệt (confirm)
9. System chuyển booking sang **confirmed**, gửi noti user
10. Đến giờ chơi, user đến sân
11. Sau buổi chơi, booking chuyển **completed**
12. System gửi noti nhắc đánh giá

```
┌─────────┐     ┌──────────┐     ┌──────────┐     ┌──────────┐
│  Chọn   │     │ Tạm giữ  │     │ Thanh    │     │  Chờ     │
│  sân +  │────▶│ 10 phút  │────▶│ toán     │────▶│  duyệt   │
│  giờ    │     │          │     │          │     │  30 phút │
└─────────┘     └──────────┘     └──────────┘     └────┬─────┘
                     │                                   │
                     │ Hết 10p                    ┌──────┴──────┐
                     ▼                            │             │
                ┌──────────┐              ┌───────▼──┐  ┌───────▼───┐
                │  Hủy     │              │ Duyệt   │  │ Từ chối   │
                │  tạm giữ │              │ ✓       │  │ → hoàn    │
                └──────────┘              │confirmed│  │   tiền    │
                                          └────┬────┘  └───────────┘
                                               │
                                          ┌────▼────┐
                                          │completed│
                                          └─────────┘
```

### 5.3 Đặt sân (giữ chỗ trước)

1. User chọn sân con + khung giờ
2. System tạm giữ khung giờ
3. User chọn "Giữ chỗ trước"
4. System tạo booking trạng thái **pending**, bắt đầu đếm 30 phút
5. System gửi noti user: "Đã giữ chỗ thành công! Bạn có 30 phút để thanh toán"
6. User thanh toán trong 30 phút
7. Tiếp tục như flow 5.2 bước 6 trở đi

```
┌─────────┐     ┌──────────┐     ┌──────────┐
│  Chọn   │     │ Giữ chỗ  │     │ Thanh    │
│  sân +  │────▶│ pending  │────▶│ toán     │──── (tiếp flow 5.2)
│  giờ    │     │ 30 phút  │     │          │
└─────────┘     └────┬─────┘     └──────────┘
                     │
                     │ Hết 30p
                     ▼
                ┌──────────┐
                │ expired  │
                │ hủy auto │
                └──────────┘
```

### 5.4 Chủ sân đăng sân

1. Chủ sân mở mục "Quản lý sân", chọn "Đăng sân mới"
2. Chủ sân nhập: tên sân, địa chỉ, tọa độ, môn thể thao, giá/giờ, khung giờ hoạt động, tiện ích
3. Chủ sân upload tối thiểu 3 hình ảnh (tổng quan, mặt sân, tiện ích)
4. Chủ sân thêm danh sách sân con (Sân A, Sân B, ...)
5. Chủ sân submit
6. System tạo sân trạng thái **pending_review**, gửi noti admin
7. Admin review thông tin + hình ảnh
8. Admin duyệt → sân chuyển **active**, hiển thị cho user
9. Admin từ chối → gửi lý do cho chủ sân, chủ sân chỉnh sửa và submit lại

### 5.5 Hủy booking + hoàn tiền

1. User mở "Booking của tôi", chọn booking muốn hủy
2. System hiển thị chính sách hoàn tiền dựa trên thời gian còn lại
3. User xác nhận hủy
4. System hủy booking, hoàn tiền theo chính sách, gửi noti chủ sân

### 5.6 Đổi giờ/sân

1. User mở booking (trạng thái confirmed), chọn "Đổi giờ/sân"
2. System kiểm tra: trước 24h so với giờ chơi + chưa đổi lần nào
3. User chọn giờ/sân mới
4. System cập nhật booking, gửi noti chủ sân về thay đổi

### 5.7 Đánh giá sân

1. Sau buổi chơi, user nhận noti nhắc đánh giá
2. User mở đánh giá: chọn 1-5 sao + viết review text (optional)
3. System lưu đánh giá, cập nhật đánh giá trung bình của sân
4. System cộng điểm thưởng cho user
5. Nếu quá 7 ngày: vẫn đánh giá được nhưng không nhận điểm thưởng

## 6. System Behavior Deep Dive

### 6.1 Decision Points

| ID | Flow | Khi nào | YES | NO |
|---|---|---|---|---|
| D1 | Đặt sân | Khung giờ còn trống? | Cho phép tạm giữ 10 phút | "Khung giờ này đã có người đặt, vui lòng chọn giờ khác" |
| D2 | Đặt sân | User chọn thanh toán hay giữ chỗ? | Thanh toán → flow 5.2 | Giữ chỗ → flow 5.3, đếm 30 phút |
| D3 | Giữ chỗ | Thanh toán trong 30 phút? | Chuyển sang paid → chờ duyệt | Hết 30p → expired, hủy tự động |
| D4 | Duyệt | Chủ sân duyệt trong 30 phút? | Booking confirmed | Hết 30p → auto hủy + hoàn tiền |
| D5 | Duyệt | Chủ sân chấp nhận? | Confirmed + noti user | Rejected + hoàn tiền tự động |
| D6 | Hủy | Trước 24h? | Hoàn 100% | Kiểm tra tiếp D7 |
| D7 | Hủy | Trước 2-12h? | Hoàn 50% | Dưới 2h hoặc no-show → 0% |
| D8 | Đổi giờ/sân | Trước 24h + chưa đổi lần nào? | Cho đổi, cập nhật booking | Từ chối, hướng dẫn hủy + đặt mới |
| D9 | Đăng sân | Admin duyệt? | Sân active, hiển thị | Từ chối + gửi lý do |
| D10 | Đánh giá | Trong 7 ngày sau buổi chơi? | Đánh giá + nhận điểm thưởng | Đánh giá được nhưng không nhận điểm |
| D11 | Concurrent | User khác đã tạm giữ khung giờ? | Báo "khung giờ không còn trống" | Cho phép tạm giữ |
| D12 | Chủ sân | Không duyệt 3 lần? | Cảnh báo | Tiếp tục bình thường |
| D13 | Chủ sân | Không duyệt 5 lần? | Tạm khóa sân | Tiếp tục cảnh báo |

### 6.2 Scenario Matrix

| From State | To State | Rule | Action | Result |
|------------|----------|------|--------|--------|
| Guest xem sân | Đặt sân | Chưa đăng nhập | Redirect login | Quay lại flow đặt sau login |
| User có 3 booking | Đặt thêm | Max 3 pending/confirmed | Từ chối | "Bạn đang có 3 booking, vui lòng hoàn tất hoặc hủy trước khi đặt thêm" |
| User đặt sân | Sân bị chủ block giờ đó | Chủ sân block sau khi user vào trang | Báo hết slot | Quay lại chọn giờ khác |
| Booking confirmed | User đổi giờ | Trước 24h, lần đầu | Cho đổi | Cập nhật booking + noti chủ sân |
| Booking confirmed | User đổi giờ | Trong 24h hoặc đã đổi 1 lần | Từ chối đổi | Hướng dẫn hủy + đặt mới |
| Booking paid | Chủ sân không duyệt | Quá 30 phút | Auto hủy | Hoàn tiền 100% + noti user |

### 6.3 State Transitions

**Booking:**

```
pending → paid → confirmed → completed
  │         │        │
  │         │        └──→ cancelled (user hủy)
  │         │
  │         └──→ rejected (chủ sân từ chối → hoàn tiền)
  │         └──→ auto-cancelled (hết 30p duyệt → hoàn tiền)
  │
  └──→ expired (hết 30p giữ chỗ không thanh toán)
```

| Entity | Từ | Sang | Trigger | Quay lại được? |
|--------|------|------|---------|-------------|
| Booking | (mới) | pending | User chọn "Giữ chỗ" | Không |
| Booking | (mới) | paid | User thanh toán ngay | Không |
| Booking | pending | paid | User thanh toán trong 30p | Không |
| Booking | pending | expired | Hết 30 phút không thanh toán | Không |
| Booking | paid | confirmed | Chủ sân duyệt | Không |
| Booking | paid | rejected | Chủ sân từ chối | Không, hoàn tiền auto |
| Booking | paid | auto-cancelled | Hết 30 phút chủ sân không duyệt | Không, hoàn tiền auto |
| Booking | confirmed | completed | Qua giờ chơi | Không |
| Booking | confirmed | cancelled | User hủy (hoàn tiền theo chính sách) | Không |

**Venue (Sân):**

| Entity | Từ | Sang | Trigger | Quay lại được? |
|--------|------|------|---------|-------------|
| Venue | (mới) | pending_review | Chủ sân submit | Không |
| Venue | pending_review | active | Admin duyệt | Có (admin khóa) |
| Venue | pending_review | rejected | Admin từ chối | Có (sửa + submit lại) |
| Venue | active | suspended | Admin khóa hoặc 5 lần không duyệt | Có (admin mở lại) |
| Venue | active | inactive | Chủ sân tạm đóng | Có (mở lại) |

### 6.4 Interrupted Transactions

| Tình huống | Hệ thống còn lại gì | Resume | Cleanup |
|---|---|---|---|
| Mất mạng giữa thanh toán | Check trạng thái payment gateway | Đã trừ tiền → paid. Chưa → giữ chỗ hiệu lực 30p | Hết 30p → expired |
| Đóng app sau giữ chỗ | Booking pending, timer 30p chạy | Mở lại → thấy pending + thời gian còn lại | Hết 30p → expired |
| Chủ sân không online | Booking paid, timer duyệt 30p | Mở app → thấy booking cần duyệt | Hết 30p → auto-cancelled + hoàn tiền |
| 2 user đặt cùng sân cùng giờ | Tạm giữ 10p cho user đầu | User sau thấy "hết slot" | User đầu hết 10p → giải phóng |
| User đặt mới khi có 3 booking | Từ chối tạo mới | Thông báo max 3 | Không cần |

### 6.5 Other Edge Cases

- **Empty state:** Tìm sân không có kết quả → gợi ý mở rộng bộ lọc hoặc chọn ngày khác.
- **Chủ sân sửa giá** khi user đang xem → giá tính theo thời điểm confirm đặt.
- **Sân bị khóa** sau khi user đặt → booking confirmed giữ, pending/paid hoàn tiền.
- **Chủ sân xóa sân con** có booking tương lai → từ chối xóa.
- **Đánh giá spam** → giới hạn 1 đánh giá per booking.

## 7. Validation, Limits & Wording

### 7.1 Validation rules

| Field | Rule |
|---|---|
| Tên sân | Bắt buộc, 5-100 ký tự |
| Địa chỉ sân | Bắt buộc, 10-200 ký tự |
| Giá/giờ | Bắt buộc, số dương, đơn vị VND |
| Hình ảnh sân | Tối thiểu 3 tấm, tối đa 10 tấm, max 5MB/tấm |
| Khung giờ đặt | Nằm trong khung giờ hoạt động của sân |
| Ngày đặt | Từ hôm nay đến tối đa 14 ngày tới |
| Giờ đặt | Tối thiểu 2 giờ trước giờ chơi |
| Đánh giá sao | 1-5 sao, bắt buộc |
| Review text | Tùy chọn, tối đa 500 ký tự |

### 7.2 Limits & Quotas (exact values)

| Tham số | Giá trị | Window | Behavior khi vượt |
|---|---|---|---|
| Giữ chỗ chưa thanh toán | 30 phút | Per booking | Auto hủy (expired) |
| Tạm giữ khung giờ | 10 phút | Per slot | Giải phóng slot |
| Chủ sân duyệt | 30 phút | Per booking | Auto hủy + hoàn tiền |
| Booking đồng thời tối đa | 3 | Per user | Từ chối tạo mới |
| Đặt sân trước tối đa | 14 ngày | — | Không hiển thị ngày quá 14 ngày |
| Đặt sân sớm nhất | 2 giờ trước | — | Từ chối |
| Hình ảnh sân | 3-10 tấm | Per venue | Bắt buộc tối thiểu 3 |
| Đổi giờ/sân | 1 lần | Per booking, trước 24h | Hướng dẫn hủy + đặt mới |
| Deadline đánh giá có thưởng | 7 ngày | Sau buổi chơi | Không nhận điểm |
| Chủ sân không duyệt — cảnh báo | 3 lần | — | Gửi cảnh báo |
| Chủ sân không duyệt — khóa | 5 lần | — | Tạm khóa sân |

### 7.3 Wording samples (exact strings)

#### Error messages

| Tình huống | Wording | Code |
|---|---|---|
| Khung giờ đã có người đặt | "Khung giờ này đã có người đặt, vui lòng chọn giờ khác" | E-? |
| Hết thời gian giữ chỗ | "Đã hết 30 phút giữ chỗ, booking đã được hủy" | E-? |
| Chủ sân từ chối | "Chủ sân đã từ chối booking, tiền sẽ được hoàn trong 24h" | E-? |
| Quá 3 booking | "Bạn đang có 3 booking, vui lòng hoàn tất hoặc hủy trước khi đặt thêm" | E-? |
| Đặt sát giờ | "Chỉ có thể đặt sân trước tối thiểu 2 giờ" | E-? |

#### Success messages

| Tình huống | Wording |
|---|---|
| Giữ chỗ thành công | "Đã giữ chỗ thành công! Bạn có 30 phút để thanh toán" |
| Thanh toán thành công | "Thanh toán thành công! Đang chờ chủ sân xác nhận" |
| Chủ sân duyệt | "Chủ sân đã xác nhận! Hẹn gặp bạn tại {tên sân} lúc {giờ}, {ngày}" |
| Đánh giá thành công | "Cảm ơn đánh giá! Bạn nhận được {X} điểm thưởng" |

#### Info / neutral messages

| Tình huống | Wording |
|---|---|
| Nhắc thanh toán | "Còn {X} phút để thanh toán, sau đó booking sẽ tự động hủy" |
| Nhắc đánh giá | "Bạn đã chơi tại {tên sân} — đánh giá ngay để nhận điểm thưởng!" |

## 8. Assumptions

- User đã có tài khoản SportHub (feature authentication).
- Thanh toán dùng chung hệ thống premium-payment.
- Sân có tọa độ GPS (Google Maps hoặc tương đương).
- Mỗi venue có thể có nhiều sân con, user chọn sân con khi đặt.
- Chủ sân tự quản lý thông tin sân + lịch trống.
- Admin duyệt sân mới trước khi hiển thị.
- Hoàn tiền tự động qua phương thức thanh toán gốc.
- Notification qua in-app + push (không email/SMS giai đoạn đầu).
- Khoảng 500 user giai đoạn đầu.

## 9. Risks

| Rủi ro | Khả năng | Hậu quả nghiệp vụ | Cách phòng |
|--------|----------|-------------------|-----------|
| Chủ sân không dùng app, ít sân trên hệ thống | Thường | Mất user do trải nghiệm trống, adoption thấp | Chủ động onboard chủ sân, ưu đãi đăng ký sớm |
| User đặt rồi no-show nhiều | Thỉnh thoảng | Chủ sân rời nền tảng, giảm supply | Chính sách 0% dưới 2h, flag user no-show |
| Đối thủ đã có feature, cần ra nhanh | Thường | Delay launch, mất lợi thế cạnh tranh | Giữ scope P0 cho MVP, P1/P2 ra sau |

## 10. Success Criteria (preliminary)

- Booking conversion rate (xem sân đến đặt thành công) >= 20%
- Thời gian từ mở app đến đặt xong < 3 phút
- Tỷ lệ chủ sân duyệt trong 30 phút >= 80%
- Đánh giá trung bình sân >= 3.5 sao
- Tỷ lệ hủy booking < 15%

## 11. Open Questions

Không có OQ còn mở (đã resolve OQ-1: 500 user giai đoạn đầu).

## 12. Next Steps

Tính năng này bổ sung vào tài liệu sport-matching hiện có:
- Cập nhật `/urd sport-matching` — thêm user needs đặt sân
- Cập nhật `/brd sport-matching` — thêm business objectives
- Cập nhật `/prd sport-matching` — thêm capabilities
- Cập nhật `/srs sport-matching` — thêm FR/NFR/BR/Error

*KHÔNG tạo folder riêng — mọi thứ nằm trong `docs/sport-matching/`.*
